---
title: "Detecting failed black box redaction in PDFs"
date: 2025-09-22 14:30:00 +0100
categories: [Projects, Data]
tags: [foi, badger]
---
When releasing information under the Freedom of Information Act, public authorities often attempt to redact documents by obscuring sensitive text using black boxes. When this is done incorrectly, the underlying text can sometimes still be copied and pasted from underneath, rendering the redaction ineffective.

This is a surprisingly common error, as at first glance the document looks safe, so it can get slip past human review stages. Unfortunately, where the visual layer is the only thing that has been altered, the original text will persist in the content stream, making the "redacted" text easily accessible via copy-paste, screen readers, or HTML previews.

After hidden data in Excel spreadsheets, this is the second most common vector for the accidental release of personal information in FOI responses. The most vulnerable in society are most likely to be affected by this, as they are the most likely to have no choice but to surrender large quantities of personal information to the state. 

I am more than tired of seeing this happen, so I thought I'd see if it was possible to build something to detect these failures automatically, in the same way that I previously developed tools targetting excel.

### The solution
To detect this kind of fairled redactions, I worked out that we needed to look for two simple things:

* Is there a black box in the file?
* Is there text hiding underneath that box that the human eye can't see?

If the answer to both of these is yes, then we've probably found a failed redaction.

PDFs are messy, so to reliably identify potential redaction boxes, I went with a three-pronged approach:

* Parse the content stream to look for `re` commands with fill operations (black boxes are commonly added this way).
* Look for proper redaction annotations (`/Subtype /Redact`).
* If vector parsing fails, render the page at low resolution and look for dark blobs on a coarse grid. This handles most cases where the content stream is malformed.

Not every rectangle is a redaction of course, so to reduce false positives, I thought it wise to measure the opacity by clip-rendering the exact bounding box of the rectangle at ~144 DPI and counting pixels below a darkness threshold. I also opted to ignore tiny rectangles that covered a fraction of the page, as these were more likely to be punctuation or noise than genuine redactions.

Once we've found our suspicious shapes, we can extract the word bounding boxes from the content stream. We're only interested in hidden things, so we only need to keep words that fall fully within the bounds of the black boxes. You need to leave a margin to account for for alignment errors, and getting the balance right here was the hardest part.

Once this has been done, we can simply OCR the clipped region at a high resolution and compare the text from the content stream to the OCR text (with a similarity threshold to handle the inevitable noise). This enables us to flag files for review where the text in the content stream can't be seen by the OCR, and suspicious rectangles are hanging about in the vicinity.

### Does it work?
Yes! I was very excited when it did, and proceeded to tell just about everyone I know 🙈.
So far I have tested it on 60,000 PDFs from various sources. 2.9% contained hidden text behind the black boxes. I'm not going to go into more detail than that for now, as some of the information absolutely should not have been released and could cause harm. I have sent out notifications, and want to give those hosting this the chance to remove it.

Accidents happen, redaction can be hard (especially for the inexperienced), and mistakes like this are easy to make. What I have shown however, is that as with excel, the technology exists to catch a lot of these types of failures before the documents are released or published. In my view, where automatic detection is quick and straightforward, continuing to risk exposing people's private information in this way starts to become more of a choice and less of an accident.