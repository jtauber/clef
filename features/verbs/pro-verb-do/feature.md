---
tags: [pro-verb, biber-1988]
unit: pro-verb form
---
# Pro-verb do

Forms of *do* used in place of an action or predicate understood from context, as in *Lee sings and Kim does too* or *she promised to leave and did so*.

## Conventions

- Finite and non-finite forms count: *do*, *does*, *did*, *doing* and *done*.
- *Do so*, *do it*, *do that* and *do the same* count when they refer to an action understood from the text or situation. Mark only the form of *do*, not its complement.
- Substitution in short answers, comparisons and elliptical statements counts: *yes, I did*, *more than I do*, *so do I*. This includes uses analysed grammatically as auxiliary ellipsis.
- Negative substitution counts: *Lee walks to work, but I don't*. Mark only the verbal part of a contraction: *[do]n't*, *[does]n’t*, *[did]n't*.
- Auxiliary *do* used for negation or emphasis with an expressed verb does not count: *I do not know*, *I do know*.
- Question-forming *do* and question tags do not count, including an elliptical question such as *did you?*. A pro-verb inside a question can still count: *did you do it?* has one occurrence, on the second *do*.
- Ordinary lexical uses do not count when *do* has a specified meaning rather than standing in for an understood action: *do the accounts*, *do the washing up*.
- Noun uses, adjectival *done* meaning finished, and mentions of word forms do not count.

## Notes

Feature 12 in [@biber_1988, p. 226]. CLEF distinguishes verbal substitution from ordinary lexical *do* and from question-forming auxiliaries. Biber's local exclusions only partly capture those distinctions.

The biber rule matches the source's DO forms. It excludes a DO candidate when a verb follows with at most one intervening adverb, or when an ALL-P punctuation mark or WHP word immediately precedes it. It uses Penn tags as approximations to the source's verb and adverb categories. Split and fused negative contractions are supported; a separated *n't* is treated as part of the listed negative DO form.

The tone-unit exclusion is omitted because the current format has no tone-unit annotations. Preceding punctuation in another sentence is also unavailable to a pattern. Initial questions can therefore be overcounted, while genuine substitution after a comma or *who* can be missed. The rule does not recover the action referred to, distinguish lexical *do*, or reject nominal and adjectival homographs.
