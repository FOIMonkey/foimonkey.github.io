---
title: "Unlocking FOI Data, voice cloning, and other things"
date: 2025-09-11 14:55:00 +0100
categories: [Projects, Data, AI]
tags: [foi, AI, experiments, own-models]
---
## FOI data
After years of chipping away at it, I finally worked out how to extract the answers from FOI responses in a way that is not susceptible to hallucination, and that, as a welcome byproduct, enables you to reliably identify what the purpose of each message is. So far, I have used these learnings to clean, label and extract data from ~3.2 million emails that I have taken from WhatDoTheyKnow.

Anonymisation was not as challenging as I had imagined it was going to be, thanks to the special tooling that have I developed for this purpose.

There is immense value in this data that has never been fully unlocked, and it has always been my ambition to change that. The work that I have done allows you to gain a real understanding of how the public and the state are interacting in practice, rather than in theory. Beyond the sorting and labeling, I have created a matched question and answer set of public sector information stretching back well over a decade. This elevates the information above the noise, which, when combined with the added structure, makes it possible to connect and enhance the data in ways that I would have once thought impossible. It has the potential to unlock things like better, smarter notifications and has already measurably improved the accuracy of the machine classification project that I have been quietly working on. In short, it is everything that I ever imagined it would be, and I am glad that I have persisted with this for so many years.

Here are some things that I found interesting, which you might too:

* ~68% of correspondence text on WhatDoTheyKnow is automated junk and filler that can be removed without impacting the information flow.
* For just over 5% of requests, the requesters wrote to the authority for no other reason than to thank them or to praise the FOI team for their response. After more than a decade of moderating misuse, reading these was balm for my weary soul.
* For ~12% of requests, the requester had to chase the authority over a late response - a tad higher than I was expecting.
* For ~13% of requests, the requester asked the authority follow-on questions or for clarification of the answer. Requesters who did this showed increased positive sentiment towards the authority as the correspondence chain progressed, suggesting they were happy with what was provided.
* Positive sentiment on the part of the requester was greater where the authority used more accessible language and less legalese. This was true for successful requests and refusals.
* Just over 1% of requests veered off-topic into personal correspondence, complaints and non-foi matters (reactive moderation means this will never be zero).
* Less than 1% of requesters had to write about some sort of tech issue - this was usually Alaveteli eating an attachment/table or the authority forgetting to attach the same.
* Of the requesters who write back when asked to provide a real name, ~87% comply, often apologising for not understanding the requirements of the act. Of those who do push back, a large percentage would appear to be correct to do so.

## VibeVoice and misinformation

A few weeks ago, Microsoft released some new text-to-speech models called VibeVoice, with the bigger of the two being able to handle four-person multi-turn conversations up to 45 minutes in length. They have since pulled it, citing "out of scope" use, but mirrors are widely available. I’m not sure what they thought was going to happen. Having played about with it, I can say that it is an exceptionally good voice cloner. Some of the outputs that I have generated are so convincing, that I would have been taken in by them had I heard them “in the wild”. The barrier to creating convincing deepfakes and fraud has never been lower.

Personally, I am using the 1.5B parameter version in combination with the FOI project mentioned above. Whilst I am logged on, every hour, it selects a random message from the database and creates a .wav file of it. This is then played on the hour, as some sort of bad non-cuckoo cuckoo clock. Of course I have subbed out the default voice files for a curated collection of my own choosing, and the results are just the right blend of chaos and absurdity to keep me amused for now.

## The model that is yet to be named.

I trained a small model over the weekend that I’m pretty proud of, pushing it all the way to convergence. So far I have successfully finetuned it to generate FOI requests, do basic NER, and to write python. Currently, it is worse at coding than I am, and when I got AI to review the outputs, Gemini started pleading with me to use a more competent tool 😅. But some of what it writes runs, and even vaguely does what I want it to. I stopped the finetune whilst it was still learning, so there is room for further improvement there. For something that I have brought into existence using my own training code, it is pretty cool that it can do this at all.

I want to release the base model, so have been aquainting myself with the detail of the new EU AI regulations. I’ve done the calculations around FLOPS and so on, and unsurprisingly my model is not powerful enough to accidentally trigger any high level controls. I found a lot of the guidance to be a bit impenetrable, and am unsure as to what good practice is meant to look like. It seems like a regular model card will do, but I guess that it is much like GDPR, and the test is going to be how this is all enforced in practice. I could always copy the big players and just ban EU users, but I can’t bring myself to do that. I’m still annoyed that Civit is blocking UK traffic from accessing loras because of the Online Safety Act.

## Closing thoughts and storage

All of the above has left me in the rather familiar position of being sat on a large pile of tools and learnings that I don't know what to do with, and that do not have an obvious home. There would have been a time where that would bother me, but I am ok with it now. I have always found satisfaction in burying myself into large, messy and seemingly unsolvable problems, and carving a path through them. Following my curiosity and doing something that brings me joy has a value in and of itself. The FOI project in particular would still have been worthwhile even if I were to delete it all tomorrow. Above all else, it is another closed loop.

Speaking of delete it all tomorrow, at several points this week I thought I might well have to. I am on my second 1TB SSD drive now and my data hoarding problem is not getting any better. I managed to completely fill up my laptop storage twice this week, and was struggling to see what was left to jettison until I thought to check the huggingface model cache dir. There were 172GB of cached models waiting for me there - I really must remember to clear that out more often 🙈