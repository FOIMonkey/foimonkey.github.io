---
title: "In Scotland, disclosure rarely wins"
date: 2026-02-06 19:55:00 +0100
categories: [Projects, Data]
tags: [foi, AI, data, scotland]
---
As part of a new project that I'm working on, I've gathered every decision notice published by the Scottish Information Commissioner. I've extracted nearly 10,000 public interest arguments for and against disclosure that were cited in 1,275 decisions. My goal was to understand what factors actually make a difference when a case has reached the Commissioner.

Across all the decisions where a public interest test was carried out, the public interest was found to favour the release of some or all of the information in just 16.4% of those tests.

At first glance, that might sound like bad news for requesters, but I think it might also be a sign that the legislation is working exactly as intended. If the majority of tests were successful, it would suggest to me that qualified exemptions were being routinely misapplied. 

The "win" rate for appeals more generally is much higher, with ~65% finding partially or fully in favour of the requester. A lot of these wins are on procedural points such as late responses or reviews, or concern exemptions that were found not to apply at all.

## Arguments that lead to disclosure
Here are some of the kinds of argument that appeared most often in cases where the public interest favoured disclosure, along with a few less common ones that I hadn't considered before.

### The information would inform public debate
This is one of the most frequently cited arguments where disclosure wins. The main idea is that disclosure would give the public the necessary facts to engage properly with important issues that affect them. This works best where the requester can point to a live discussion about something specific, such as a controversial development, or a matter where misinformation is circulating and could be countered by the release of accurate information.

### The need for transparency in decision-making
This centres on the public's right to understand how and why specific decisions were reached and not just the outcome. It is particularly effective against section 29 safe space arguments, and has also won out in planning cases where the requested information would shed light on the reasoning behind a decision.

### Better accountability for the use of public funds
Another common argument, this comes up whenever there is a question about how public money has been spent or whether value for money has been achieved. It works well where information has been requested about procurement and contract performance, particularly where substantial sums of public money are involved. This argument has been successfully used in cases involving overspends, PPP contracts, procurement and waste management deals.

### The information is already in the public domain
If similar information is already public, then the authority's case for withholding what remains is considerably weaker. This is a useful argument to use if an authority has released partial information, or when the substance of the withheld material has already been discussed elsewhere. It can be particularly effective in cases where information is claimed to be commercially sensitive.

### The passage of time
This argument claims that the specific harm that the exemption was designed to prevent has diminished since the information was created. It is particularly effective against safe space arguments under sections 29 and 30, where the decision has already been made and the policy process has concluded.

### Controversial or high-profile issues
The fact that an issue has attracted a large amount of public attention or controversy can be an important factor in favour of disclosure. This is particularly true where the matter has been the subject of parliamentary questions, media coverage, public protest or other debate. For this to be effective, you would need to show that there is specific, identifiable public interest in the issue, rather than general public curiosity.

### Scrutiny of public bodies
The public has a right to scrutinise the performance of the public bodies that act on its behalf. This is distinct from arguments about the accountability for the use of public funds because it can apply even where money is not at issue. It can cover requests for information about governance, regulatory performance, as well as general decision-making processes.

### Fairness, justice and procedural propriety
Where information relates to the way that individuals have been treated by public bodies, the Commissioner has accepted this argument, even against exemptions where the public interest test often goes the other way. This would cover disciplinary processes, and situations where individuals or the local community believed that they may have been treated unfairly. 

Closely related to this argument would be information that showed whether a public body followed its own procedures. There is a strong public interest in knowing whether processes have been followed properly. The Commissioner has ordered disclosure of information such as the generic criteria used in public appointment decisions, finding that the public had a legitimate interest in understanding the factors involved, even where individual performance information was withheld.

### Enabling informed choices
An argument that is a bit less obvious, but also effective, is where the public needs the information to be able to make practical decisions. In one notable group of cases, the Commissioner ordered disclosure of the names of care homes where Covid-19 deaths had occurred. The authority had argued that disclosure would prejudice its commercial interests, but the Commissioner found those submissions speculative and concluded that older people and their families needed this information to make informed decisions about care.

### Revealing malpractice or mismanagement
This is effective where there is evidence, or a reasonable suspicion, that a public body may have acted improperly. You can argue that the information should be disclosed if it would shed light on conduct that falls below the standard the public is entitled to expect.

### Dispelling rumour and speculation
The Commissioner has occasionally found a public interest in releasing information that would set the record straight where rumours or other misinformation are circulating. The argument in such cases is essentially that secrecy is only making things worse.

### Understanding and monitoring major projects
Where a publicly funded project is still underway, there is a public interest in tracking how it is progressing and scrutinising any assumptions that are informing ongoing work. If a project has failed, then it is in the public interest to release information that aids understanding about what might have gone wrong.

### Environmental impacts
Where information relates to the environmental consequences of a decision or activity, there is a public interest in disclosure. This is particularly effective in planning or other development cases where the environmental impact is disputed. It is worth noting that the Environmental Information Regulations carry a presumption in favour of disclosure. When environmental information is at stake, the authority has to work much harder to justify withholding it, and the Commissioner often references this presumption directly.

## General tips

If I were to try and summarise the above as a series of things that you might consider when challenging an exemption on public interest grounds, it'd look something like this:

- Frame your arguments around why disclosure is important to the public, and not just to you. If the topic has attracted media coverage, parliamentary questions or public protest, then provide evidence of this.
- Make your arguments as specific and linked to practical outcomes as possible. This may be difficult, as you will usually not have had sight of the disputed information, but nevertheless very effective. 
- If public funds are involved, particularly very large sums, make that explicit.
- If the decision has already been made, the policy making process has concluded, or the project has ended, the safe space argument is much weaker.
- If similar information has been released by another authority, or the substance of what you're asking for has already been discussed in public, such as in a press release, then it may weaken the case for withholding.

## Methodology and caveats
I used a combination of regex, AI and AI-guided regex to extract the public interest arguments from the full decision texts. I validated what I had extracted, including manually reviewing a sample. I clustered the arguments into themes using intelligent keyword matching, further regex and manual review.

Despite validation, because the initial extraction was done by AI, and not a human, there may still be some noise. In some cases, the same decision has two entries for the same exemption with different outcomes, representing the fact that different conclusions were reached about different pieces of information.

The dataset this is based on only captures cases that reached the Commissioner. By the time that has happened, the public authority has already said no and usually upheld its own refusal at the internal review stage. The cases I have looked at will be the most contested ones. It tells us nothing about the many thousands of requests where authorities have found the public interest favoured disclosure themselves, or where requesters accepted their reasoning and moved on. For the subset of requests that it does cover, however, the accuracy is sufficient for the patterns to be useful.
