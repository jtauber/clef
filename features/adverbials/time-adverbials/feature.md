---
tags: [adverbial, time, biber-1988]
unit: adverbial word
---
# Time adverbials

Single words used adverbially to express time, including when something happens, how long it lasts or how often it happens.

## Conventions

- Each adverbial word counts once. In examples, mark only that word: *very [soon]*. Adjacent adverbials count separately: *[early] [today]*.
- Repetition and frequency uses count: *try again*, *I saw her once*.
- Adjectival and nominal uses do not count: *the early train*, *tomorrow is a holiday*.
- Words introducing temporal clauses do not count: *once* in *once you arrive, call me*.
- Uses that only organise discourse, without a temporal meaning, do not count.
- Multiword prepositional and noun phrases, such as *on Monday* and *all night*, are outside this feature's scope.
- The feature is not restricted to Biber's word list: temporal *already* and *then* count.

## Notes

This is feature 5 in section B of [@biber_1988, p. 224]. Biber supplies a list of 28 words, drawn from Quirk et al., and explains that he excludes items with other major functions, such as *last* and *next*. The list is stored in `lexicons/biber_1988/time-adverbials.txt`.

The biber rule matches the listed forms without testing their function in context. It can therefore count non-adverbial or non-temporal uses and miss time adverbials absent from the list, including *already* and *then*.

MAT 1.3.2 [@mat] adds the spellings *to-day*, *to-morrow* and *to-night*. It excludes *soon* immediately before *as* and retags *now* after punctuation as a discourse particle. The mat rule includes these exclusions within a sentence; its note explains the source's additional behaviour at input and sentence boundaries. The word list is stored in `lexicons/mat/time-adverbials.txt`. Like Biber's rule, it does not require an adverb tag or otherwise distinguish temporal uses from nominal, adjectival or clause-introducing uses.

Pybiber 0.3.1 [@pybiber] uses 29 forms with an R-prefixed tag: Biber's list without *afterwards* or *soon*, plus *to-day*, *to-morrow* and *to-night*. Its inventory is stored in `lexicons/pybiber/time-adverbials.txt`. The pybiber rule preserves tag-prefix and word-boundary matching and excludes tokens marked as punctuation by spaCy's dependency labels. It has no special exclusion for *now* after punctuation. It tests forms and tags separately, deliberately omitting the source's matches on apparent tags inside unusual forms such as *today_rb*. Its notes document this reconstruction difference.
