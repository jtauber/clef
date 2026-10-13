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

The contextual rule is a CLEF proposal using Penn POS tags, auxiliary lemmas and local word order. It includes *who*, *whom*, *whose* and *which*, longer and coordinated WH-phrases, fronted prepositions, contractions, quotation and conjunction contexts, subject questions, WHY with a bare infinitive, elliptical questions and echoes. Inversion provides evidence without requiring a question mark; the other branches require one. Later WH-words in a coordinated phrase are excluded so that its first WH-word remains the anchor. A verb before the conjunction permits separate question clauses.

The contextual rule excludes *whether*, confines -ever forms to the inversion branch, and checks for a likely subject after the inverted auxiliary. These choices reject the non-question sequences *whatever is chosen must fit* and *whether doing less would help*. A separate exclusion handles comma-delimited relatives after nominal antecedents. These checks are heuristics: unpunctuated subject questions such as *Who called* remain within the feature definition but are missed. Complex phrase structures, tagger errors, ambiguous quotation and punctuation, and a question mark belonging to a later clause can still cause errors. The rule note describes the supported contexts and remaining limits.
