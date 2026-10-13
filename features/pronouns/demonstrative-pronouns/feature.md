---
tags: [pronoun, demonstrative, biber-1988]
unit: demonstrative-pronoun form
---
# Demonstrative pronouns

*This*, *that*, *these* and *those* used as the head of a noun phrase to point to people, things or situations, as in *this matters* or *I prefer those*.

## Conventions

- Subject, object and complement uses count. The referent may be in the text or in the surrounding situation.
- A demonstrative modified by a phrase or relative clause counts: *those near the door*, *those who stayed*.
- Determiner uses do not count: *this book*, *those three chairs*. Mark only the demonstrative in pronominal uses.
- Relative *that*, clause-introducing *that* and degree *that* do not count: *the bag that broke*, *I know that she left*, *not that tall*.
- Contracted forms count once. Mark only the pronoun part: *[That]'s*, *[That]’ll*.
- Mentions of word forms do not count.

## Notes

Feature 10 in [@biber_1988, p. 226]. This is distinct from Biber's feature 51, which excludes demonstrative pronouns.

The biber rule reconstructs the automatic contexts that can be expressed with the current annotation layers. It uses Penn verb and modal tags for the following verb or auxiliary, and WDT as a proxy for relative *that*. It handles the separately listed *that's* in fused or split form.

Biber's tone-unit conditions and manual disambiguation are not implemented. A sentence boundary is not a substitute for a tone-unit boundary. The rule can therefore miss pronouns before intervening material or at the end of an unpunctuated utterance. It can also count non-pronominal *that* when the following token satisfies a pattern; its success depends partly on the supplied tags.

The MAT reconstruction uses local following-token tests, including commas and quotes, and selected earlier complement/relative exclusions. It also preserves MAT's separate THAT + lowercase *is* or straight-apostrophe *'s* branch, which can override those exclusions and count relative *that*. The rule notes describe the case-sensitive suffix test, tokenization limits and earlier retagging not fully reconstructed.
