---
tags: [question, clause, biber-1988]
unit: direct WH-question
---
# Direct WH-questions

Direct questions containing an interrogative WH-expression that asks for a person, thing, property or circumstance, as in *who called?*, *which book did you read?* or *where are they?*.

## Conventions

- Count each direct WH-question once, including subject questions, rhetorical questions and questions with contracted auxiliaries.
- Include questions with a longer WH-phrase, such as *how many people came?*, and fronted prepositions, such as *to whom did you speak?*.
- Include echo questions with a WH-expression in place, such as *you bought what?*, and elliptical questions such as *why?* when they function as direct questions.
- Count coordinated question clauses separately. A single clause with several WH-expressions, or a coordinated WH-phrase, counts once: *who gave what to whom?* and *who and what caused this?* each contain one occurrence.
- Direct questions in quotations count. A question mark alone does not establish a WH-question, and omission of the mark does not rule one out.
- Exclude embedded questions, relative clauses, exclamatives and mentions of WH-words. A direct yes/no question containing an embedded WH-question does not count: *can you tell me where she went?*.
- Mark only the first interrogative WH-word of each question. Leave the rest of its phrase, auxiliaries, other clause material and punctuation outside the marked piece. In a contraction, mark only the WH-word: *[Where]'s she gone?*.

## Notes

Feature 13, the sole feature in section D of [@biber_1988, p. 227]. Its printed algorithm is narrower than the linguistic definition here: it requires clause punctuation or a tone-unit boundary, a word in the WHO category, and an immediately following uncontracted AUX. WHO excludes the separately defined WHP forms *who*, *whom*, *whose* and *which* [@biber_1988, pp. 222–223]. These exclusions belong to the detection method, not the feature conventions.

The biber rule accepts sentence start or clause punctuation before WHO. Sentence start approximates the unavailable boundary information and allows questions whose preceding sentence-ending punctuation falls outside the supplied sentence. It is not a tone-unit annotation and does not recover tone-unit boundaries inside sentences. A boundary is still required: *I know what can help* does not match. An intervening quotation mark can still prevent a match, as can a longer WH-phrase or other material outside the printed pattern. The rule can also count non-question sequences. Its note describes the boundary, inventory and tokenization choices.

The contextual rules are CLEF proposals using Penn POS tags, auxiliary lemmas, local word order and dependencies. The `contextual` variant uses UD v2 dependencies; `contextual-spacy` uses spaCy's ClearNLP-derived labels. Both include *who*, *whom*, *whose* and *which*, longer and coordinated WH-phrases, fronted prepositions, contractions, quotation and conjunction contexts, subject questions, WHY with a bare infinitive, elliptical questions and echoes. Inversion provides evidence without requiring a question mark. A separate dependency alternative also recognizes some subject questions without one; the other sequential branches require a question mark. Later WH-words in a coordinated phrase are excluded so that its first WH-word remains the anchor. A verb before the conjunction permits separate question clauses.

The contextual inversion branch also permits one adverb-tagged *exactly* immediately before the WH-word, as in *exactly where is the exit?* and *exactly where does she live?*. The WH-word remains the anchor. The boundary and inversion requirements remain in place, so this does not admit *I know exactly where she lives*. This exception does not extend to other pre-WH modifiers or the subject and elliptical question branches.

The dependency alternative recognizes *who*, *what*, *which* or *whose* as a direct `nsubj` dependent of the sentence root, provided that root has a finite-verb tag (`VBD`, `VBP` or `VBZ`). Thus *Who called* counts without a question mark. A subordinate predicate does not satisfy the root requirement. A WH-word with an attached relative clause is also excluded, covering parses that promote *what* to the main subject in *What happened surprised me*. The dependency alternative does not follow determiners, conjuncts, auxiliaries or copulas.

The UD variant has a narrow fallback for a complete two-token sentence: *what* tagged as an interrogative pronoun (`PronType=Int`) and sentence root, followed by a finite verb tagged `acl:relcl`. This recovers *What happened* and *What matters* under Stanza's alternative analysis. Relative pronouns (`PronType=Rel`) and larger sentences do not qualify. The supplied parse is preserved; the fallback uses its morphology and dependency labels together.

The contextual rules exclude *whether*, confine -ever forms to the inversion branch, and check for a likely subject after the inverted auxiliary. These choices reject the non-question sequences *whatever is chosen must fit* and *whether doing less would help*. A separate exclusion handles comma-delimited relatives after nominal antecedents. These checks are heuristics: root attachment is evidence for a standalone question, not proof of interrogative meaning. An isolated title or nominal fragment with the same text and annotations as a question remains indistinguishable to the two-token fallback. The relative-clause exclusion can also reject an interrogative WH-word modified by a relative clause. Complex phrase structures, parser errors, ambiguous quotation and punctuation, and a question mark belonging to a later clause can still cause errors. The rule notes describe the supported contexts and remaining limits.

The MAT reconstruction follows version 1.3.2 [@mat]. It requires preceding punctuation within the supplied sentence, accepting quotation marks but rejecting commas. It excludes *however* and *whatever*, permits several contracted auxiliaries and accepts split negative contractions. An ungrouped regular expression lets words such as *somewhere* supply a WH context. Its extra pattern for an intervening token before WHO and BE tags that intervening token rather than the WH-word; the reconstruction preserves that anchor error. These are properties of the source detector, not changes to the feature definition or example markings. The rule note distinguishes them from the limits of reconstructing MAT's preprocessing and cross-sentence context.
