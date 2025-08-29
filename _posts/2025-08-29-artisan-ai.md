---
title: "Artisan AI"
date: 2025-08-29 16:15:00 +0100
categories: [Projects, Data, AI]
tags: [foi, AI, experiments, own-models]
---
I recently trained a `~645M` parameter LLM from the ground up. This was by far the largest model that I have attempted to create to date. I wanted to train a “good enough” base model that was fully my own, yet was smart enough to be able to be adapted for basic specialised tasks across different domains. I really like that I can account for the source of every piece of text that has gone into it.

The initial pre-training phase used `~36B` tokens of data from the Common Pile, and took about 26 hours on `4xH100s`. Training went well, and whilst it is not state of the art, the resulting base model is able to reliably produce coherent text. I have named it *Wihtgar*.

Following on from [my last experiment](https://foimonkey.github.io/posts/12-training-a-22M-parameter-model-from-scratch/), and as an initial test, I taught it to generate FOI requests from public authority and keyword combinations in the exact style that I write them. This involved a very small amount of domain specific continued pretraining, standard fine-tuning to align the model to the task and DPO on a judged preference set to teach it further nuance, and the ability to stay on topic.

The results were excellent, with the final model's perplexity on the task related eval set dropping to 7.35 from 12.83. For context, I ran the same evaluation on *request_writer_olmo* (1.48B) which achieved a perplexity of 3.97. Perplexity doesn't always translate to task performance, but my model can reliably generate requests from authority and keyword pairs that are valid, focused, on topic, and at a level that is very close to my previous leading finetunes. I think there are still further performance gains to be found.

The key was putting in the work to create a series of high quality yet varied datasets. Domain specific experience helped here. I should probably write about this part at some point.

Beyond FOI requests, *Wihtgar* has shown similar promising early results on generative tasks in other domains - this afternoon I have adapted it to process some files from the national storage mechanism. Whilst it is never going to win any awards, I think this demonstrates that it's possible to build and refine a basic yet useful specialist model on a modest budget. The training and finetuning together cost less than £250.

More importnantly I've really enjoyed working on this. It has provided me with a focused creative outlet during a bit of a transitional period, and there has always been something about having ownership over every aspect of a model that appeals to me. I don't know if I'll ever reach the point where I'm able to return to properly helping out with FOI related things again, but this feels like a solid foundation to build something interesting from regardless.

All these request generator models are crying out to be hooked up to a one armed bandit UI 👀