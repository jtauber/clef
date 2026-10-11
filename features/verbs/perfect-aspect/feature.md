---
tags: [aspect, biber-1988]
unit: perfect verb phrase
---
# Perfect aspect

Verb phrases in the perfect: a form of the auxiliary *have* followed by a past participle, as in *she has left*, *they had been warned* or *to have known*.

## Conventions

- Each perfect counts once, however many words come between the auxiliary and the participle: *has she really left* is one.
- Every form of *have* counts: present (*has left*), past (*had left*) and non-finite (*having left*, *to have left*, *should have left*).
- Contracted *'ve*, *'d* and *'s* count when they are HAVE: *they'd left*, *it's been raining*, but not *the window's broken*.
- Perfect progressives and perfect passives count once: *has been working*, *had been told*.
- *have got* expressing possession or obligation (*I've got a car*, *she's got to go*) does not count. *have gotten*, and *have got* in other senses (*he's got much better*), count.
- *have* with an object and a participle (*she had her car repaired*, *we had it fixed*) is not a perfect.
- An auxiliary whose participle is left out (*Have you finished? Yes, I have.*) does not count.
- In examples, brackets mark HAVE and the participles in its verb sequence, as in *[has been working]*. Subjects, adverbs and non-verbal complements are left outside the brackets. Separate pieces of one occurrence share a subscript label.

## Notes

[@biber_1988, p. 223] gives two patterns: HAVE, then up to two optional adverbs, then a past participle; and, for questions, HAVE, a noun or pronoun, then a past participle. His HAVE includes *'ve* and *'d* but not *'s*, and his past participle category includes any past tense form (p. 222). The biber rule reconstructs these patterns. Its second pattern also matches *have* with an object and a participle (*had it fixed*), and so do MAT's and MFTE's.

Biber's tagger marked the perfect on the past participle, as in his sample output (Table II.1, p. 218): in *had been warned* the perfect is on *been* and the passive on *warned*. MFTE also tags the participle, while MAT and pybiber count the auxiliary. The examples allow a detection to be anchored on HAVE or any participle in the same verb sequence. A detection's anchor must overlap a marked piece of the occurrence; its surrounding span does not determine whether it receives credit.

The ud rule also anchors on HAVE. It follows the dependency links to check the predicate and its auxiliaries or copula. In *has been there* and *have you been on a student exchange*, UD makes *there* and *exchange* the heads. The rule uses those heads to find the construction but reports *has* or *Have*, so the non-verbal complements stay outside the brackets.
