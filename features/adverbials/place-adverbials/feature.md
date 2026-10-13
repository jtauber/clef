---
tags: [adverbial, place, biber-1988]
unit: adverbial word
---
# Place adverbials

Single words used adverbially to indicate a physical location, direction or distance, as in *wait outside* or *walk uphill*.

## Conventions

- Each adverbial word counts once. In examples, mark only that word: *just [behind]*, *[uphill] and [north]*.
- Locative complements of *be* count: *she is inside*.
- A word introducing a prepositional phrase does not count: *outside* in *outside the station*. Multiword prepositional and noun phrases, such as *in the garden* and *a long way*, are outside this feature's scope.
- Adjectival and nominal uses do not count: *the outside wall*, *the north of England*.
- Degree uses (*far better*) and references to positions in a text (*see above for the calculation*) do not count.
- The feature is not restricted to Biber's word list: *here* and locative *there* count. Existential *there* in *there is a problem* does not count.

## Notes

This is feature 4 in section B of [@biber_1988, p. 224]. Biber supplies a list of 42 words, drawn from Quirk et al., and explains that he excludes items with other major functions, such as *in* and *on*. The list is stored in `lexicons/biber_1988/place-adverbials.txt`.

The biber rule matches the listed forms without testing their function in context. It can therefore count non-adverbial or non-spatial uses and miss place adverbials absent from the list, including *here* and *there*.

MAT 1.3.2 [@mat] uses the same word list but excludes proper-noun tags (NNP and NNPS). Its earlier indefinite-pronoun pass removes that tag from *nowhere*, so *nowhere* still counts. The mat rule preserves this exception. Other POS tags are accepted, leaving the same contextual overcounts and lexical omissions as the biber rule. MAT's list is recorded separately in `lexicons/mat/place-adverbials.txt`.

Pybiber 0.3.1 [@pybiber] accepts the same 42 forms with an R-prefixed tag, or a subset of 15 with an I-prefixed tag. Its inventories are stored under `lexicons/pybiber/`. The pybiber rule preserves these tag-prefix and word-boundary tests and excludes tokens marked as punctuation by spaCy's dependency labels. It still counts qualifying prepositional, degree and textual uses. It tests forms and tags separately, deliberately omitting the source's matches on apparent tags inside unusual forms such as *west_rb* and *outside_in*. Its notes document these reconstruction differences and the limits of reconstructing counts as token anchors.
