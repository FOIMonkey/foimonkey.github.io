---
title: "Training a 22M parameter model from scratch to beat billion-parameter LLMs at writing FOI requests"
date: 2025-08-24 14:34:00 +0100
categories: [Projects, Data, AI]
tags: [foi, AI, experiments, own-models]
---

This week I wanted to explore whether a model that is smaller than the average Android app could outperform billion-parameter LLMs on a specialised task. To test this out, I trained a 22 million parameter model from scratch with the sole purpose of writing valid Freedom of Information requests.

The training data consisted entirely of correspondence that is published on WhatDoTheyKnow (requests and responses, but no attachments). Nothing else. After cleaning the data, deduplicating acknowledgements and batch requests, and removing sensitive data and other harmful content, I was left with approximately 300 million words to work with. 

### Training and evaluation
Following Chinchilla scaling laws, it seemed enough to train a 22 million parameter model with 8 layers, built on the GPT-2 tokenizer. The training run took about 4 hours on a single H100 SXM. I used my own basic training code. The result was a model with no general knowledge, but that is fully fluent in the language of FOI in the UK.

As part of another project, I recently generated [keywords for over 1 million FOI requests](https://github.com/FOIMonkey/foi-keywords) using small keyword models that I fine-tuned. I sampled a range of these keyword-authority pairs and used [Mistral-Small](https://huggingface.co/mistralai/Mistral-Small-24B-Instruct-2501) to generate over 50,000 synthetic requests that followed my personal template for making requests. After a few hours of cleaning and improvement, I was left with a [fine-tuning dataset](https://huggingface.co/datasets/HMC83/synthetic_foi_requests) that was good enough for this experiment.

I wanted to see how my custom 22M parameter model would perform against other small models that were taught in the same way, so I fine-tuned three models:

  * My custom 22M parameter model (request\_writer\_sbp)
  * OLMo 2 Instruct 1B (request\_writer\_olmo)
  * SmolLM2 360M (request\_writer\_smol)

To test how the models performed, I generated 25 requests using each model using identical prompts and temperature settings. I then asked Gemini 2.5 pro to evaluate the outputs against my criteria for what makes a successful request:

1.  Does it ask for recorded information from the correct public authority?
2.  Is the output clean, correctly formatted, and free of errors, and so able to be sent as-is?
3.  Is the core request sound, requiring only minor tweaks or edits?
4.  Does it stay on topic and stick to the provided keywords?
5.  Does it ask for specific, retrievable data?
6.  Is the language clear and understandable?
7.  Is the scope narrow enough to stay within the cost limit?

-----
### Results
As you can see, my models were the clear winners 🎉:

| Model (Parameters) | Valid Request? | Send As-is? | Light Editing? | On Topic? | Focused? | Clear? | Likely Success? |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| request\_writer\_smol (361M) | 25 | 24 | 25 | 24 | 25 | 25 | 25 |
| request\_writer\_olmo (1.48B) | 25 | 25 | 25 | 23 | 25 | 25 | 25 |
| request\_writer\_sbp (22M) | 25 | 15 | 20 | 18 | 24 | 23 | 18 |
| OLMo 2 Instruct 1B (1.48B) | 25 | 0 | 15 | 23 | 14 | 0 | 14 |
| SmolLM2-Instruct (361M) | 12 | 3 | 8 | 12 | 8 | 12 | 5 |
| Llama-3.2-3B-Instruct (3.21B) | 7 | 1 | 6 | 7 | 5 | 7 | 4 |

request\_writer\_smol (361M) tied for first place. This was a highly reliable model overall, and only stumbled once when it misinterpreted ULEZ as being the Underground Light Rail Extension.

The other joint winner, request\_writer\_olmo (1.48B) produced requests that were extremely precise and specific. It only lost points for occasionally omitting to build a request that was relevant to all three keywords.

My tiny model request\_writer\_sbp (22M) came third\!🙂 Despite its very limited semantic understanding, it consistently stuck to the correct format and produced valid requests. Its main weaknesses were repeating words or concepts and hallucinating new topics when confronted with an area that it had not come across before. While the requests often need editing before sending to account for this, the fact that a 22M parameter model could compete at all is remarkable.

OLMo 2 Instruct 1B (1.48B) suffered from being excessively formal and including unnecessary waffle. It tended to request vague, broad categories of information that were likely to hit the cost limits. It stuck to topic well, however.

SmolLM2-Instruct (361M) frequently misunderstood the task entirely. It generated complaints, how-to guides, and Subject Access Requests - anything but FOI. When it did generate requests, it occasionally threatened legal action against authorities. You'd want to check its output carefully before opting to use it, and without fine-tuning, it's just not capable of this task.

Llama-3.2-3B-Instruct (3.21B) was the biggest surprise. This model fundamentally failed to stick to the task, hallucinating entire responses from authorities rather than generating requests to send to them. It even went so far as to make up fake statistics. It would be a bit cheeky to claim that my model beat this one. A more specific prompt would likely help to fix the issues that it was having, but it was given the same information as all the rest, so I'll take it. Despite its larger size, it came last in this particular test.

-----
### Conclusion
This was just a bit of fun, and it's worth acknowledging the limitations of my experiment. I used a relatively small sample of 25 requests per model, and relied on a single LLM judge (Gemini 2.5 pro). FOI requests have a relatively standardised format and vocabulary that makes them quite formulaic. Smaller models might be particularly well suited to this task for that reason, and my success here might not translate to other tasks that are more creative.

However, a 22M parameter model trained exclusively on FOI data outperformed a much more complex model 145x its size. This shows that you don't always need to throw data and money at a big corporate API somewhere to get acceptable results. There's value to be had in using tiny, task-specific models that can run on minimal hardware, not least in terms of independence and control.

I've made the top performing model available here: [https://huggingface.co/HMC83/request\_writer\_smol](https://huggingface.co/HMC83/request_writer_smol). To get the best results, you should keep the temperature low and add a repetition penalty. I see the main use case for models such as these as being to create request templates, perhaps as part of a pipeline eg news article is published -\> keyword extraction model picks out key themes -\> request writing model creates an on-topic request that is ready to send. 

I personally preferred the OLMo 2 fine-tune, and am going to see if I can't squeeze some more performance out of it before publishing it. I've not made the tiny model public either, as I'd also want to publish the training data and copyright of WhatDoTheyKnow content is best filed under "there be dragons". If you'd like to try it out, let me know.

### Sample Outputs

#### request\_writer\_smol (361M)
Cardiff Council | Keywords: fly-tipping, fines, cleanup costs*

> Dear Cardiff Council,
> 
> Please provide me with a copy of the following information:
> 
> 1. The total amount spent on cleaning up fly-tipping incidents in Cardiff over the past 12 months, broken down by month and waste type.
> 2. The number of fines issued for fly-tipping offences in Cardiff during the same period, along with the average fine paid per case.
> 
> Yours faithfully,
> 
> [Your Name]

#### request\_writer\_olmo (1.48B)
Department for Transport | Keywords: costs, spending, consultants

> Dear Department for Transport,
> 
> Please provide me with a copy of the following information:
> 
> 1. A breakdown of the total expenditure by your department on external consultancy services (including fees paid to third-party consultants) for the last financial year, including the names of the top five most expensive consultants and the amount spent with each.
> 
> Yours faithfully,
> 
> [Your Name]

#### request\_writer\_sbp (22M)
Environment Agency | Keywords: sewage, rivers, pollution (Model: sbp)

> Dear Environment Agency,
> 
> Please provide me with a copy of the following information:
> 
> 1. Any internal reports, assessments, or correspondence (from the last three years) regarding the impact of sewage on water quality in rivers within your area, including any findings or recommendations made as a result.
> 2. Records of any complaints or incidents reported to your agency regarding sewage-related pollution in rivers over the past three years, excluding personal or sensitive details.
> 
> Yours faithfully,
> 
> [Your Name]