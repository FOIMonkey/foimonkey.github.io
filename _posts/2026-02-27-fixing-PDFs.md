---
title: "Day 18 Fixing PDFS"
date: 2026-02-27 14:30:00 +0000
categories: [Projects]
tags: [plan-B, foi, wdtk]
---
This post was written to [the victory music](https://www.youtube.com/watch?v=VlBaX19B-jY) of FOI battles past.

I have managed to get censor rules working on pdfs in alaveteli.

I can't explain clearly enough just how annoying the old approach is to work around. It uses binary string replacement that almost never works. PDFs don't store text the way you might think, and the text you see on opening one might be stored as complete gibberish in the content stream. Sometimes I have had to solve what are essentially Caesar ciphers that change based on the font just to remove a surname. The current approach searches for the text you want to remove as is, which is why it finds nothing and shrugs about it. 

It is no exaggeration to say that manually creating rules that work has consumed entire weeks of my life. Songs and verse have been composed about the frustration of it. It has been a stone in my shoe for ~15 years.

Yesterday, I built a document redaction pipeline for the FOISA project I've been working on. In doing so, I realised that most of the things it used for the PDFs were already alaveteli dependencies, and I started to wonder what if. If you know me, you'll know that I have to chase my curiosity and find out.

The approach I used works more like a human would than what is there now, targeting the visual layer. It extracts the text and the exact coords of each word on each page. It runs the censor rules on that text, and if there is a hit, it maps the range back to the bounding boxes of the words. It then opens the PDF and draws a black rectangle as an overlay, with some safety padding. 

Just drawing a black box doesn't remove the text of course, so for every page that has had at least one redaction, it renders that page to a 200 DPI PNG, and embeds it back into the PDF as a full-page image, replacing the original content. The original text is gone. Pages without redactions are left untouched.

The reason this works where the old approach didn't is that I stopped trying to hack the PDF's internal text encoding and focused on the visual layer.

I put in a [draft PR](https://github.com/mysociety/alaveteli/pull/9136) upstream if you want to find and play with it. 

I can guarantee that it will not carry a fraction of the same sense of satisfaction for you. 

Regardless as to whether this leads to anything, or is too complicated, makes files too large, breaks something else, etc, what matters is that I have felt what it is like to have this be possible. To enter a test rule and watch the document be redacted in real time. To see the default rules already working. It was deeply satisfying, in a way that only watching a longstanding annoyance melt away can be. Now that I know it is possible, I can happily put the PDFs down.

Following my own advice from yesterday, I [published the failed PDF redaction detection](https://github.com/FOIMonkey/Homer) as a standalone thing. The redaction part is meant for emergencies only, so I'd recommend only running the detection part unless you have need of it. It detects failed pdf redactions where there are rectangles obscuring text that you can still copy-paste out of the document. After the nightmare that was spreadsheets, this is the next biggest cause of nasty data breaches that I've had to deal with over the years. As with the censor rules, getting this working has been a deeply satisfying thing.

Revisiting the homer tool led me to discover that I have been miscategorising these sorts of failed redactions all of my life. Only 4% of them have the text behind the black boxes, most of the rest render it IN FRONT.

Nothing is true.
