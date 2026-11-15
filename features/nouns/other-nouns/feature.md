---
tags: [noun, biber-1988]
unit: noun word
---
# Other nouns

Noun uses other than nominalizations and gerunds, including common and proper nouns, as in *the dog*, *two houses* and *London*.

## Conventions

- Count each noun word once, including plural nouns, proper nouns and nouns modifying other nouns. *Student exchange* contains two occurrences.
- Count the noun words of a multiword name separately, such as *New York*, when they function together as a proper name.
- Exclude nominalizations and nominal participle forms under their respective feature definitions, even when the Biber suffix detector misses them.
- Exclude pronouns, adjectives, verbal uses and mentions of word forms. A noun sharing a suffix with the nominalization rule still counts if it is not a nominalization, as with *cement*, *moment* and *city*.
- Mark only the noun word; leave possessive endings and other surrounding material outside the marked piece.

## Notes

Feature 16, total other nouns, in section E of [@biber_1988, p. 228]. Biber counts dictionary nouns apart from nominalizations and gerunds. CLEF does not have his original dictionary and tagging pipeline. The Biber reconstruction uses supplied Penn noun tags (NN, NNS, NNP and NNPS) as an explicit approximation to that lookup.

The rule excludes detections from nominalizations/biber and gerunds/biber. This follows the source's residual counting procedure, so errors in those detections propagate here: a suffix false positive removes a genuine other noun, while a missed nominalization can remain. Human gerund annotations must cover the whole input text before this rule is evaluated, even if a parser labels every gerund as VBG or finds no noun candidates. Missing annotation does not establish that there are no gerunds. Parser errors and disagreements with the unavailable dictionary remain additional limits.

The contextual alternatives use the same Penn noun candidates and Biber nominalization suffix exclusion, replacing the manual gerund exclusion with `gerunds/contextual` or `gerunds/contextual-spacy`. They run automatically on the corresponding dependency scheme. The gerund detector's errors propagate into this residual category: for example, treating an object-denoting *building* or *painting* as a gerund removes a genuine other noun. These are CLEF proposals; the Biber rule still requires independently supplied manual gerund results.
