---
title: "Mapping FOI Disclosure Logs: Part 1"
date: 2025-11-18 11:55:00 +0100
categories: [Projects, Data]
tags: [foi, AI, experiments, wdtk]
---
Public authorities answer hundreds of thousands of FOI and EIR requests every year, but most of the information that is released is not searchable or available for wider use. Some authorities do publish responses in disclosure logs, but these are scattered and incomplete.

In an attempt to find out exactly what data is out there, I've started a project to index and categorise as many FOI responses as possible. I already have ~1.25 million requests scraped from WhatDoTheyKnow. This may seem substantial, but my preliminary research suggests that this is only around 5-7% of all requests which is a tiny fraction of the total. For my dataset, I am going to try to gather these key fields:

`id, authority reference, authority name, date, topic, legislation, summary, request text, response text, status, url`

This is not the sort of dataset that one person could keep refreshed, so it will be more of a snapshot of what was available at a given point in time. I'm also aware that I won't be able to obtain all of that information for all of the authorities.

I've started by collating links to the disclosure logs for central and local government, universities and NHS organisations. I used AI search agents to help me with this, and manually verified what they found, which has saved me quite a bit of time.

Scraping the data is not straightforward. There is no one standard way to publish a disclosure log and the quality of the data and the formats used to publish it vary wildly across authorities. The most common method seems to be to link to individual response PDFs, but I've also encountered:

- Excel workbooks containing embedded pdf responses
- Power BI dashboards that don't allow downloads
- Password protected logs, that are available to authority staff only
- Massive "annual compendiums" combining all requests and responses into a single, unstructured PDF
- Logs that are embedded as part of the request form, that are not indexed, linkable or properly searchable
- Files that are only accessible by talking to an ai chatbot
- Logs that are only available by making an FOI request for them
- Responses that are only accessible as javascript popups

I'll have some good stats on this when the project is complete, but most of the above are really bad for accessibility.

The time range covered is wildly inconsistent. Some authorities publish only the last few months of data, others have years of detailed archives, and some seem to pick and choose responses randomly. Then you find the abandoned logs that have say, 3 months of responses from mid 2018 and nothing before or after. A monument to past good intentions. Some authorities run their logs on a rolling basis, removing responses that are over 1 year old automatically, which means that you can't rely on a response that you saw today still being there tomorrow.

What data is included also depends entirely on the authority. Some authorities publish all requests that have been received, some only a narrowly curated selection of successful responses. Some logs have dates, summaries, legislation used, categories, status, the full text of the request and the response, and any attachments. Others are just a list of topics and dates, nothing more.

I've been trying to match the data to requests on WDTK to try to avoid duplication, but this is easier said than done. WhatDoTheyKnow hides the subject lines for incoming messages, but this is often where the reference number is. As a result, matching has been largely done on text similarity, topic and correspondence date.

Where the logs lack authority generated summaries or topic data, I've been using [Apertus](https://www.swiss-ai.org/apertus) running on an api I set up to generate them. That model launched without much fanfare, but offers the same openness and performance as OLMo but with a much better context window. I used this to generate topics and summaries for all the requests in the WhatDoTheyKnow archive as well, which I should really run stats on.

I've also used AI to categorise all the requests into FOI and EIR, where that information was missing. I did this previously for WhatDoTheyKnow requests with a work hat on, but as far as I am aware, mySociety has never published that data, leaving it trapped in a spreadsheet somewhere gathering dust. Perhaps that was a blessing - I've learnt a lot since then and checking my results against what law the authorities actually used suggests my new way is likely much more accurate.

If these challenges can be overcome, a unified, searchable index of FOI responses would be a very valuable resource. The more I've worked on this project, the more I've felt that my sellotape and string version is going to be worthwhile.