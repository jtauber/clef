---
tags: [noun, gerund, biber-1988]
unit: nominal participle form
---
# Gerunds

Participle forms used nominally to name an activity or event, as in *swimming relaxes me* or *she enjoys reading novels*.

## Conventions

- Count the participle form once when it heads an activity or event expression used as a subject, object, predicative complement or complement of a preposition.
- Include nominal event uses with a determiner, such as *the singing of the anthem*. Exclude lexical nouns naming objects or results, such as *the painting on the wall* and *a tall building*.
- Count coordinated nominal participle forms separately: *swimming and running* contains two occurrences.
- Exclude participles used in progressive predicates, adjectivally, or in adverbial clauses. A form inside a larger nominal expression is not automatically a gerund: *being* counts in *being watched worries her*, while *watched* does not.
- Exclude participial labels for people, such as *the accused*, and mentions of word forms. The conventions here concern activity and event readings.
- Leave an example unresolved when the available context does not distinguish an event from an object or an attributive participle from a nominal use.
- Mark only the nominal participle form, leaving its subject, modifiers, objects and other complements outside the marked piece.

## Notes

Feature 15 in section E of [@biber_1988, p. 227]. Biber describes participle forms in nominal functions and says that they were edited by hand. He supplies no automatic algorithm or detailed annotation protocol. The conventions above make CLEF's interpretation explicit; they are not a recovered protocol from his study.

The Biber rule therefore contains human annotation instructions. Its results must be supplied independently of the catalogue's marked examples. A completed annotation with no occurrences is a measured zero. Missing or incomplete annotation is not evaluated, including when this rule is used to exclude gerunds from other nouns. A POS tag alone is not a replacement for this manual step.

The contextual rules detect candidates automatically from dependency structure and Penn POS tags. `contextual` uses UD v2; `contextual-spacy` uses spaCy's ClearNLP-derived labels. Both include singular noun-tagged and VBG forms ending in *-ing* in nominal or clausal argument positions, and inherit those positions through one coordination edge. BE/HAVE/GET auxiliary structures identify *being*, *having* or *getting* as the counted form instead of a later participle. A finite or infinitival progressive does not become a gerund merely because its clause is a complement.

The UD rule also recognises selected prepositions attached as clause markers, such as *before leaving* and *by working*. The spaCy variant uses its prepositional-complement relations. Copular nominal predicates count when the input analysis distinguishes them from progressives. A parser can instead analyse *her favourite activity is walking* as progressive, producing a miss. Longer chains of coordinated attachments are outside these initial rules.

These contextual rules approximate syntactic distribution, not the activity/event distinction in full. They can count lexical nouns such as *building*, *painting* and *ceiling*, and can confuse mentions with uses. Broad clausal-complement relations do not by themselves guarantee a nominal reading. Such disagreements remain visible in validation; the rules neither copy the gold annotations nor require human gerund records. The manual Biber rule is retained as a separate method.
