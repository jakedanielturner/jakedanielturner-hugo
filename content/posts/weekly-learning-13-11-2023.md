---
title: >
    Weekly Learning #5: Git tricks and associated wizardry 🧙‍♂️
date: 2023-11-13T12:20:01Z
draft: false
tags: ["DVSA", "CDDO", "Weekly Learning"]
url: "posts/weekly-learning-13-11-2023"
---

I'm again quickly typing this out on a Tuesday lunchtime, before I forget what I have done.

I was switching between *quite a few* branches of Terraform using git, quickly merging some and rebasing my others against the new develop branch. I've used ```git fetch -p``` before for removing stuff which has been merged, but it wasn't quite cutting it. I wanted to be able to remove all my local branches if they'd been merged or deleted on the remote repository. With some light Stack Overflow-ing, I found the following command which did exactly as I wanted:

```bash

git fetch -p && git branch -vv | awk '/: gone]/{print $1}' | xargs git branch -D

```

I thought I would also take the time to detail some of the other git commands which I've been taught and found useful, in case of head injury, memory loss, or anything similar.