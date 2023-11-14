---
title: >
    Weekly Learning #4: Back to basics (sort of?) 🏫
date: 2023-11-10T15:20:46Z
draft: false
tags: ["DVSA", "CDDO", "Weekly Learning"]
url: "posts/weekly-learning-06-11-2023"
---

(I'm writing this while watching [Richard Towers' talk at DevOpsDays 2023](https://www.youtube.com/watch?v=mpY1lxkikqM&t=1224s) for what must be the hundredth time, which speaks to how enjoyable it is.)

I wasn't sure what to title this, and I'm not sure if it accurately reflects what I want to describe, but I guess it'll do. I'm also not sure that the task I want to talk about was from *this* week, but, we move.

I recently had a ticket to do a bit of refactoring on a Lambda at work. I'm, as always, going to try and keep this high-level, just because I'm not sure how much I can really disclose without getting in trouble.

For context, this Lambda was written some time ago, was set to work and had been quietly doing it's job since then, without issue. As part of the ongoing migration to Github Actions, however, some issues had been identified with its design. We have a fairly standard pipeline which consists of standard tasks: security checks, testing, linting, building and, if all are successful, uploading the build artefact to our cloud provider for deployment when we want. For this Lambda specifically, however, the linting action had been disabled - which wasn't a great sign. 

The ticket, therefore, was to fix the Lambda enough so the linting action could be re-enabled, consistent with the other Lambdas in our estate. I thought this would be fairly straightforward, and it sort of fell into my 'ideal' ticket zone. These are tickets where I believe I know most of what is needed to complete it, but it might require a bit of learning and exploring on my part to get it over the line. With these, I am able to stretch myself a bit to get them completed, without feeling like I am way out of my comfort zone and having to deal with the stress and anxiety which comes with that. Occasionally, those feelings are inevitable if you want to progress, but I've found that you can have both sometimes, which is ideal - hence the 'ideal' ticket zone.

I pulled the Lambda down, ran the linting locally and found a rough total of 80 (!!) linting errors and warnings. *All* of these would need fixing before the linting action could be re-enabled.

