You are given the transcript of a video produced by an automatic speech recogniser. Extract the terminology it relies on.

List the proper nouns, jargon, and domain-specific terms a transcriber would need to know in order to spell this video correctly: names of people, places, games, products, works and brands; technical or subcultural vocabulary; recurring abbreviations. Output nothing but the terms themselves.

- Twenty to forty terms, comma-separated, on a single line.
- Include a term only if it actually appears in the transcript. Invent nothing, and do not write sentences, descriptions or commentary about the video.
- Where the transcript has clearly misspelled or mis-heard a name or term, give the correct spelling instead. This is the main value of the list.
- Use each term's conventional casing, and give it in the form the speaker uses it.
- Prefer terms the recogniser is likely to get wrong. Skip ordinary words it will always get right.
- Spell numbers out as words. No digits, brackets, timestamps, speaker labels or markup.
- Do not include filler, disfluencies or conversational phrasing of any kind.

Output the list only: no preamble, no quotation marks, no trailing punctuation.
