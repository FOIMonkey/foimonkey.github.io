---
title: "Making art from art"
date: 2025-08-03 18:07:00 +0100
categories: [Projects, Data, AI]
tags: [python, duckdb, Gemma, foi]
---
At the start of the year I scraped data from over 800,000 FOI requests from WhatDoTheyKnow to look for patterns in the data. This sent me down a number of rabbit holes, including experiments with automatic request classification. I have spent a lot of time thinking about the text of the requests and responses, but not about the images. 

Alaveteli spits these out and lists them as attachments. They're mainly logos and promotional stuff that is unrelated to the information being asked for, so I've never really looked at them.

I decided I'd take a subset of 45,000ish images, and pass them to Gemma 3 12B to analyse. I started at request_id 1,000,000 and worked forward in time from there. To avoid sending the same image to the model multiple times, I recorded a SHA-256 hash of the image to skip ones that were already in the database. This was not foolproof, but it removed a lot of the noise.

I asked the model to output json with: 
* `altText`: An alt text description
* `subjectType`: The main subject of the image.
* `tags`: A list of relevant keywords.
* `visibleText`: Any text found within the image.
* `is_photo` & `is_logo`: Booleans to look at the image type.

This was also a change to grab some new desktop wallpaper to replace the one linked too closely to my last job. I decided I'd record the top 5 dominant colours for each image in the dataset. Once I removed the blacks, whites and greys that dominated, I was happy with the result.

![A horizontal spectrum wallpaper generated from public data](/assets/img/spectrum_horizontal.png)

Other interesting finds included:

* [A Fire engine](https://www.whatdotheyknow.com/request/fleet_list_20222086/response/2447803/attach/9/GN73%20ZVU.jpeg.jpg?cookie_passthrough=1)
* [A lovely photo of a park](https://www.whatdotheyknow.com/request/request_for_location_information/response/2364523/attach/4/51688342663%20c43d122b23%204k.jpg?cookie_passthrough=1)
* [A War Memorial](https://www.whatdotheyknow.com/request/ww1_memorial_2/response/2427629/attach/3/E01AFE52A160422DAA809F7929ECD912.jpg?cookie_passthrough=1)
* [The auction catalogue for a dress worn by Marilyn Monroe in Some Like It Hot](https://www.whatdotheyknow.com/request/dress_2/response/2448335/attach/7/00004%20scan%202023%2009%2027%2016%2017%2031.jpg?cookie_passthrough=1)
* [A primary school logo with live laugh love in it](https://www.whatdotheyknow.com/request/religious_practices_at_ni_primar_234/response/2495086/attach/3/Outlook%20bu1tm2ak.png?cookie_passthrough=1)

Having has a quick scan of the outputs, the model seems to have performed well, and if anything might have been overkill in terms of capabilities for this kind of project. I'd eventually like to do all the images, so I'm hoping to find as lightweight a solution as possible that is still accurate enough to be useful.