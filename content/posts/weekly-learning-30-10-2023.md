---
title: >
    Weekly Learning #3: Mocking with Jest 🎭
date: 2023-10-31T17:39:51Z
draft: false
tags: ["DVSA", "CDDO", "Weekly Learning"]
url: "posts/weekly-learning-30-10-2023"
---
To preface: I first wrote this on Tuesday having just solved something, and needing to write it loosely somewhere. I ended up talking a bit more and it turned into a full-fledged post, so I'm keeping it and using it for this week. This is **Mocking with Jest**. 

I don't know if this will form the basis of this weeks Weekly Learning, but I've just cracked something which *I know* has caused me issues before, and thought it best to write it down before I forget it.

I'm trying to mock a class in Jest, which has a method which is used for retrieving secrets. I'll try and keep this high-level and generic, for the sake of future me (and any potential readers).

To add context to the below, I have a method which first instantiates a class, and then uses methods of that class to provide values to a returned object. Therefore, I need to mock the class and its method, without importing it, for my test case. I tried many options, but was presented with an array of error messages (I've also provided the code which threw such error):

**SomeClass.someFunction is not a constructor**
```typescript
const mockMethod = () => jest.fn();
jest.mock('my-imported-library', () => ({
  method: () => mockMethod,
}));
```

**SomeClass.someFunction is not a function**
```typescript
const method = jest.fn().mockResolvedValue('Some string');

jest.mock('my-imported-library', () => ({
  libraryClass: jest.fn().mockReturnValue(() => ({
    method,
  })),
}));
```

And, perhaps the most annoying...

**ReferenceError: Cannot access 'method' before initialization**

```typescript
const mockMethod = jest.fn();

jest.mock('my-imported-library', () => ({
  libraryClass: jest.fn().mockReturnValue({
    method: mockMethod,
  }),
}));
```

I found this one particularly galling, as I distinctly remember having the issue before. Some answers involved using `var` instead of `const` or `let` - this, however, is not permitted by ESLint, and also just looks bad. There were other 'solutions', such as putting the mocks before imports (not really relevant), doing some wacky stuff with regards to manipulating the hoisting of variables, and other left-field answers. I was confident that this issue wasn't 

This finally worked for me: 

```typescript
const mockMethod = jest.fn();

jest.mock('my-imported-library', () => ({
    libraryClass: jest.fn().mockImplementation(() => ({
        method: mockMethod,
    })),
}));
```

We can then use it in our tests as follows:

```typescript
describe('My test suite', () => {
    it('should do some tests', async () => {
        mockMethod.mockResolvedValueOnce('Some string');
        const value = await someMethodWhichUsesTheLibraryClass();
        expect(value).toEqual('Some string');
    })
})
```

Is this the right way to do what I want to do? I can't be sure. I've had exposure to Jest through work, and I'm quite fond of it. Test Driven Development is also something I have had exposure to, although do not practice. It is something I am keen to do more of, and am planning to take up some courses teaching it. I was lucky enough to receive an excellent session on it recently, which really showed how powerful it can be. It obviously becomes more complicated as you introduce things like mocks, but that isn't something I think I should be afraid of. 

I have, for probably too long, been the sort of developer who writes their code, then spends even more time than it took to write the original code writing tests, or bodging the original tests to fit my new code. *Apparently*, this is bad. I agree - it was approaching the point where I hated writing tests, didn't consider myself good at doing so and would frequently be hitting my head against the desk, wondering if it had been long enough before I could call my line manager for help. I am hopeful of reverting this mindset, and getting in to one where tests are done first, and not something to be afraid of - hallmarks of Test Driven Development, I am sure.