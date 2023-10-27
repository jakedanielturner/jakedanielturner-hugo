---
title: >
    Weekly Learning #1: SQL Recursion  📚
date: 2023-10-20T15:20:46Z
draft: false
tags: ["DVSA", "CDDO", "Weekly Learning"]
url: "posts/weekly-learning-16-10-2023"
---

To try to prove to myself, and everyone else, that I am serious about doing something with this site, I blocked out an hour of my calendar on a Friday afternoon to work on it. That hour started 53 minutes ago, and I'm only just starting.

As mentioned before, I want to create a habit of documenting my learning. I intend to do this in conjunction with a new tracker I have been provided, which is for my own use. Here, I will go into a bit more detail about the things *on* the tracker, as I find trying to stuff stuff (eh) into Microsoft Word tables a bit cumbersome.

I expect the theme of the week to likely revolve around what tickets I have done this week, or the previous week, at work. I'm fortunate to be exposed to many different technologies and languages in my work, so there should be a consistent stream of learning - and, in turn, stuff to write about. Even if I do struggle one week, I'm sure I can also document some stuff about how I have solved such and such a ticket, as it may well come up again in the future.

This week's topic: **SQL Recursion**

I haven't done too much about recursion so far - it did come up on one project I worked on at the start of the year, but nothing since then. I remember briefly studying it at A-Level, but that as a whole didn't go great. It's the kind of thing I think I might have got knowledge from by doing a Computer Science degree, and I then regret not doing that. I think it's important to remember all the things I have learned *without* a Computer Science degree, though - and there's no reason this can't join that list.

Side note: the first page of the big book of recursion being the cover page of the big book of recursion is one of my favorite Computer Science jokes.

For the task in hand, we had to devise a mechanism for identifying all the payments in a 'family' - that is where there is some relation to another payment. When a payment is refunded, for example, it creates a child payment (basically just the negative amount of the original payment). The two payments are then linked, creating a family. This can spiral due to partial refunds, reallocations (I'm not sure what they are) and more scenarios. It's a rare scenario but these families *could* extend to be many, many payments long (wide?), and it's important all are accounted for.

Fortunately, there will always be a 'root' payment - where it all began. By finding this root payment, we can then find all it's associated payments, and do what we need with them. We just need to find the root payment, which is easier said than done.

This is where the recursion comes in. We are given a payment, which could be anywhere in the family, and we need to find its parent payment. If that payment has a parent, we need to get that payment - and so on, until we find a payment which *doesn't* have a parent. Fortunately for me, this recursion had already been written in a similar SQL script, which is used elsewhere. It was a case of adapting it and dropping the bits which I didn't need. It was made possible by CTE - Common Table Expressions - which is a new feature in MySQL. I tried adapting some of the SQL to show here, but to little success - maybe I'll try again later.

I was also fortunate to receive great support here, by people more knowledgeable about SQL than myself. I definitely feel more confident with SQL than I did before taking on the ticket, and I was actually quite proud of the solution.

I'm conscious that I've not actually provided too much detail here, more just described recursion, but I am somewhat struggling with what I can post without getting in trouble. I'd love to just dump the whole SQL script in to show off, but that might be revealing a bit too much for something which is stored in a private repo 😅 nonetheless, it's good to actually note *something* down, which hopefully I can look back on in the future.
