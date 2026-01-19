---
title: "Things AI models can't (yet) do"
date: 2026-01-19 14:15:00 +0000
categories: [Misc]
tags: [AI, art]
---
Testing frontier AI models is getting harder as they are now able to ace practically every task that used to rely on to benchmark performance. The pace of innovation still feels to be accelerating, with tools like Claude Code appearing to speed up the development cycles for Anthropic themselves and GPT 5.2 reportedly tackling previously unsolved math problems. However, in recent weeks, I've found some niche things that these models still struggle to do, which felt worth noting.

## Vision models

I have spent the past month or so disconnecting by immersing myself in offline pursuits. I can't recommend doing so enough. As part of this, I've started drawing properly for the first time in years.

To give you an idea of my style, the image below is the piece I am currently working on about masking. This one is destined for the wall of my craft space. It is in part a memento mori, and I like using clean lines and playing about with symbolism.

![Ink sketch on a green cutting mat. The drawing features a stylized human head, split into a metal mask, skull, and human faces. Additional elements include an ouroboros in the shape of infinity, a crescent and full moon, an hourglass, and roses.](/assets/img/2026-01-19/2025.jpg)

I recently worked on a separate drawing of a double Ouroboros wrapped around a Triquetra to form an eye that. It featured multiple elements that were loops or representing infinity, including a DNA double helix. I wanted to mimic that spiral when illustrating the phases of the moon, so I drew the half-moon as it would [appear from the Southern Hemisphere](https://www.open.edu/openlearn/mod/oucontent/view.php?id=69107&section=3.11) alongside other phases depicted as in the north, to try to create a sense of continuous travel around the globe.

This is quite a rare depiction, and it left all of the vision models I tested stumped. When I showed the design to Claude Opus 4.5, GPT 5.2, and Gemini 3 Pro, none of them recognised that part of the image as being representative of a half-moon. Gemini strongly pushed back when I tried to correct it, insisting I had only drawn five phases, not seven. When I asked it to use Nano Banana to manipulate the depth of the shading, it either skipped that phase entirely or "corrected" it to what the more standard Northern Hemisphere version would be. It seems that the training data is so overloaded with the standard rendering that imagining the alternative is a real struggle.

Obscure typography presented a similar challenge. On a separate acrylic painting, I included a stylized disk of calligraphy rendered in [Litterae Ignotae](https://en.wikipedia.org/wiki/Lingua_ignota) (an alphabet constructed by St. Hildegard of Bingen). Even with clear information as to the source, and an image added to the prompt to show how the alphabet maps to the latin alphabet, none of the vision models could interpret it. They could only render new text in the alphabet if I wrote it by hand first and gave them that image to manipulate. When I asked what they thought it was, Gemini went for the Tree of Life and GPT went for a spider web or star map. Claude came closest with "asemic writing", but was technically wrong, as it it is not asemic, rather means something in the form of German spoken at the time the alphabet was invented. Given the same information, I think that a person could be able to decipher it.

## Dead Languages

I recently learnt to read Old English (OE). I'd been put off in the past after hearing how difficult it was, but having studied Old and Middle High German (OHG & MHG) in depth at university, I found the grammar and vocabulary surprisingly familiar, so it wasn't too tricky.

I wanted to see how well AI could handle both of these dead languages, particularly for new composition. As the models should have all known texts and relevant academic works in their training data, I thought it might be something that they would able to master. 

In practice, whilst they seem to create passable translations of known texts, they did a bad job at translating my original works from OHG to OE. In terms of grammar, they favour selecting cognates over preserving meaning and tend to stick rigidly to more modern word order. GPT also misunderstood the meaning of several words, and relented only when presented with a dictionary. It also treated my kennings as being errors, arguing that they were unattested, rather than considering whether they were plausible, or what the meaning might be. Conversely, it rejected heofoncandel alltogether, even though that is attested. This strictness would tend to stifle creativity over time.

In terms of composition in OHG, all of the models tended to mix dialects, the odd Old Saxon/OE word would creep in from time to time and they added articles more often that you would find in the surviving texts - this might just be a stylistic choice as I also do this. In both OE and OHG GPT and Claude made significant grammatical errors. GPT misinterpreted an imperative form of a verb as being a noun which caused an amusing collapse of meaning. When I asked it to label the parts of speech word by word, it made enough mistakes to lead me to think that it has not seen enough text to have a perfect understanding of the function of the language.

I achieved the best results by exploiting Gemini's extremely large context window and giving it a grammar book and dictionary as part of a detailed prompt, and telling it to check the output as it went along.

I've been writing alliterative verse, which is designed more to be performed than read, so stress is key. Unfortunately, I have not found a text-to-speech model that can get this right. Somewhat surprisingly, Suno did better than other regular speech models, perhaps due to having [bardcore](https://www.youtube.com/watch?v=drDs-Y5DNH8) in its training data.

With OHG, It struggled to consistently pronounce 'w' as a 'w' and not 'v' and couldn't handle the guttural 'h' sound at all. I couldn't fix the latter issue, even with phonetic spellings. I did manage to get it to [over-pronounce the rolled 'R' in a way is satisfying](https://suno.com/song/3ffa1a48-318c-4bb1-a932-50cbef97f0e3) by taking a detour through various heavy metal genres. That text is two experimental verses formed solely of S and W alliteration to see what was possible - there are still errors, and musically it is lacking a lot!

With OE, it couldn't read the letter ash at all (æ), struggled to know when to use the soft 'g' (y-sound), and consistently misplaced the stress. When I tried to fix this by writing it out phonetically, it assumed the text was Arabic and so read the whole thing with an accent.

It seems that the training data for these languages doesn't have enough depth to support original creation. It will be interesting to track if this changes moving forward.

## Logic & Popular Culture

Finally, I tested the models on the quiz that I send around at christmas to give people a distraction during awkward festive family time.

This year, one of the cryptic clues had the answer "[Le Poisson Steve](https://www.youtube.com/watch?v=Zg6snq_oceg)". None of the main models could solve it. Although this particular trend occurred outside of their training cut-off, the answer was in a word search grid that I showed them, so a vision model should have been able to confirm the answer by checking grid. Gemini 3 eventually got it right, but only after thinking for over half an hour and searching the internet (despite being instructed not to).

Interestingly, when I had finished the Christmas Radio Times crossword (a family tradition), I was stuck on the anagram, so asked GPT to solve it. It sourced the answer from a Reddit thread posted by someone who'd asked GPT the same question, which GPT had failed to answer. It seems anagrams of obscure UK TV shows still need the human touch, for now at least.