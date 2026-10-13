# CLEF: The Catalogue of Lexico-grammatical English Features

CLEF is a unified, structured, machine-readable catalogue of linguistic features for multi-dimensional register analysis, corpus stylistics, authorship attribution, and any research that relies on counting lexico-grammatical features in English text.

CLEF synthesizes feature sets from multiple sources and will allow the addition of contributed features and detection rules. Each feature has a human-readable definition, machine-readable detection rules, annotated examples, and source provenance. The catalogue is implementation-agnostic: it defines what each feature is and how to detect it declaratively.

Detection rules so far include matching text, lemma, POS tag, or more complex corpus query patterns (CQL) and dependency tree patterns (Semgrex). Work is also planned to support semantic tagging (USAS), and LLM-based and human annotation.

The forthcoming companion library `pyclef` will provide a Python engine that interprets the catalogue’s rules against text using pluggable taggers. Others are free to also build implementations that consume this catalogue.

## This release

Work is considerably further along privately but, for initial feedback, I have released this proof-of-concept which defines the first thirteen of the 67 features in Biber (1988):

- Past tense
- Perfect aspect
- Present tense
- Place adverbials
- Time adverbials
- First-person pronouns
- Second-person pronouns
- Third-person personal pronouns
- Pronoun it
- Demonstrative pronouns
- Indefinite pronouns
- Pro-verb do
- Direct WH-questions

All thirteen carry the `biber-1988` tag; coverage of that inventory is currently partial. Past tense, present tense and perfect aspect have MAT, MFTE and pybiber reconstructions; perfect aspect also has a Biber rule. The adverbial features have Biber and MAT rules; the pronoun and pro-verb features currently have Biber rules only. Direct WH-questions have both a Biber rule and a CLEF contextual proposal.

Further Biber features will follow, a few at a time. The catalogue also includes five features used by the contextual past-tense rule: contracted perfect HAD, BE passives, GET passives, possessive and obligation HAVE GOT, and HAVE/NEED TO. They have their own definitions and examples. A broader passive feature brings BE and GET passives together. These additions do not extend the stated coverage of the Biber inventory.

Each feature is a directory under `features/` with its definition, the rules that detect it, and examples. [FORMAT.md](FORMAT.md) describes how the files are written.

Past tense also has a `contextual` rule alongside the `mfte` reconstruction. It references contextual rules belonging to six other features, including the existing perfect-aspect feature. Rules can reuse one another through `use: feature-id/rule-id`; each still detects and is evaluated against its own feature. The contextual rules are CLEF proposals. MFTE's influence and deliberate departures from its implementation are documented in their notes.

The `contextual` direct WH-question rule uses word order, POS tags and punctuation to cover inverted, subject, elliptical and echo questions. It counts the first WH-word in each question clause and retains the Biber reconstruction for comparison. Its notes distinguish these heuristics from a full grammatical analysis.

Features can declare strictly broader features with `subsumed_by` in their definitions. BE and GET passives are subsumed by passives; contracted perfect HAD is subsumed by past tense. These relationships describe feature occurrences independently of detection rules. The validation report presents their transitive reduction as a Hasse diagram.

## Validation

The companion `clef-validation` repository provides structural checks, saved tagged inputs, regression tests and comparisons with MAT, MFTE and pybiber.

## Source citations

The initial features follow Biber [@biber_1988]. Examples credited to Le Foll [@le_foll_2024] come from Appendix C, "Linguistic Features", of the book's [online supplements](https://elenlefoll.github.io/TextbookMDA/AppendixC.html), available under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). CLEF has adapted their formatting and added occurrence annotations and explanatory notes.

For MAT, we cite Nini's 2019 chapter [@nini_2019], as [requested by its author](https://sites.google.com/site/multidimensionaltagger/about). The MAT rules and lexicons in this catalogue are reconstructed from version 1.3.2 [@mat].

MFTE is described by Le Foll and Shakir [@le_foll_shakir_2025]. Following its authors' [citation guidance](https://github.com/mshakirDr/MFTE#citation), we also cite MFTE Python 1.0 [@mfte_python_2023] and Stanza [@stanza_2020]. The rules labelled `mfte` and the MFTE lexicons in this catalogue are reconstructed from version 1.6.0.2 [@mfte]. The contextual tense, aspect and passive rules draw on that method as CLEF proposals; their notes describe differences from the implementation.

For pybiber, we cite David Brown's software, version 0.3.1 [@pybiber], from which the rules are reconstructed.

Full references are in [references.bib](references.bib).

## Licence

Copyright © 2026 James K. Tauber.

CLEF's original content is licensed under the [Creative Commons Attribution-ShareAlike 4.0 International licence](https://creativecommons.org/licenses/by-sa/4.0/) (CC BY-SA 4.0). See [LICENSE](LICENSE) for the full terms.

This licence covers the rights held by CLEF's contributors. Any third-party rights and licence terms applying to source material remain unaffected.

## Who is responsible

This work is being undertaken by James K. Tauber, a doctoral candidate in Michaela Mahlberg’s Text and Language Lab at Friedrich-Alexander-Universität Erlangen-Nürnberg.
