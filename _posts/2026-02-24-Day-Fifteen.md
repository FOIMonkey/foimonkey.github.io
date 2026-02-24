---
title: "Day 15"
date: 2026-02-24 13:53:00 +0000
categories: [Projects]
tags: [plan-B, foi]
---
Ran the data refresh pipeline for the first time in anger today and nothing fell over. I am taking that as a win. Ran clustering on the PIT arguments and used that to pick out the most common ones. This works much better than being able to see all of them. I am not yet sure where I am going to present these in the appeal writing workflow, and it needs proper thought. For now, I've shoved it underneath the tool and the template box.

Have also been working on the dynamic part, and how best to connect that in whilst minimising denial of wallet risk. If I didn't want it to be queryable in detail, the dataset is small enough that I could serve all the content cached on the CDN, and the thing is essentially be free to run. The problem with only having talked this through with self-confessed data nerds is that their biases are very similar to my own. 

I need to balance the added complexity vs the extra utility over just using something like pagefind and some curated views/data subsets. The data is only going to be refreshed monthly, so I need to work out what would be lost if I switched to a simpler appoach and shoved an export in a bucket somewhere. I suspect less than I orginally thought.
