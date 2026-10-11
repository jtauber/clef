---
tags: [tense, biber-1988]
unit: finite verb form
---
# Present tense

Finite verbs in present tense form: the third person singular *-s* form (*she knows*, *is*, *has*) and the other present forms (*they know*, *am*, *are*).

## Conventions

- Auxiliaries count: *is* in *is waiting*, *has* in *has left*, *does* in *does not know*. The verb after the auxiliary does not.
- Contracted *'s*, *'m*, *'re* and *'ve* count. Possessive *'s* does not.
- Reduced *dunno* (DO NOT KNOW) counts once. In examples, mark *du*, the reduced finite auxiliary; *n* and *no* represent negation and the base form KNOW.
- Modal auxiliaries (*can*, *may*, *must*, *shall*, *will*) do not count.
- Imperatives (*Close the door*) and subjunctives (*I insist that he be told*) do not count.
- Present time reference is neither necessary nor sufficient: *the train leaves tomorrow* counts.

## Notes

[@biber_1988, p. 224] counts every verb form in his tagger's dictionary that is a base form or a third person singular present form, except infinitives. His tagset has no separate tag for the non-third-person present, which is a base form, and he does not say how imperatives and subjunctives were treated. Penn tags separate the present forms (VBP, VBZ) from the base form (VB), and every rule here relies on them or on UD's Tense feature.
