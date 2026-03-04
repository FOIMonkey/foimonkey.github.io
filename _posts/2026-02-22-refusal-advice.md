---
title: "Building the refusal advice tool"
date: 2026-02-22 16:30:00 +0000
categories: [Projects]
tags: [plan-B, foi, AI]
---
I wrote in an email recently that AI development might render business models redundant before the technology could replace any given job. I've been wondering today if that might not apply to some civic tech projects too.

This weekend I built an internal review refusal advice tool for FOISA and EIR to add to my project. With the help of Claude Opus 4.6 it took me 7.5 hours, with 6 hours of that being checking it for accuracy. It builds on what a similar but more limited WhatDoTheyKnow tool does well, whilst fixing the bits about it that don't work as well. It covers every FOISA exemption and EIR exception, as well as procedural issues. It has custom templating and advice built in. It will subtly nudge you to stop and reflect around vexatious requests. There is a master version that covers all of the refusal reasons, alongside single-exemption versions designed to sit directly on relevant advice pages.

I built this all in less than a day for the cost of ~10% of my weekly Claude quota. I am very excited to have gotten to the stage where I can have people come and try and break it/give feedback this quickly. If I'm honest, it is good enough that I could probably merge the dev branch and ship it without that. I don't think this would have been possible this time last year. 

This is both exciting and unsettling. If that's possible, why would anyone fund someone to do something similar? It might be a question that will need a serious answer soon, and I suspect that for now, it will centre around trust, maintainability and sectoral knowledge. 

At the moment this tool has 275 questions branching across 824 options that lead to 391 possible outcomes. 337 of these including a draft review template. Generating the content is one thing, but for something like this, it is important to verify it to catch bad advice, and that needed my existing knowledge. There were about 72 changes needed that impacted the meaning, and a lot of them were me being pedantic.

If you have not tried using AI for development on a simple task in a while, I'd like to leave you with this graph of the time horizon of software tasks different LLMs can complete 50% of the time. It has just gone full hockey stick. 

!["A graph showing an exponential growth curve, with Opus 4.6 well ahead of the rest"](/assets/img/2026-02-22/metr.png)
[source](https://metr.org/time-horizons/)

Benchmarks are never real life of course, and this post is certainly too simplistic, but don't sleep on this.
