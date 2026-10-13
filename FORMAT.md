# CLEF format

This document describes the layout of this repo and the format used for features.
The format will be expanded as new features are added.

## 1. Layout

```
README.md                      catalogue overview
LICENSE                        CC BY-SA 4.0 licence text
FORMAT.md                      this file
references.bib                 every work cited
lexicons/
  <origin>/                    source citation key
    <name>.txt                 a word list from that source
features/
  <group>/                     a grouping of features
    README.md                  the group’s name and description
    <feature-id>/              a feature
      feature.md               definition, conventions and notes
      rules.yaml               ways of detecting it
      examples.txt             examples, ambiguities, and non-examples
```

Names in angle brackets are placeholders. Each group can contain multiple features, and each source can have multiple lexicons.

Every feature belongs to a group. A group’s `README.md` has a `# Name` line, then a one-paragraph description.

## 2. Identifiers

- A feature’s id is the name of its directory, in lower case with hyphens (`past-tense`). Ids are unique across all groups.
- A rule’s id is unique within its `rules.yaml`.
- A reference to a rule is `<feature-id>/<rule-id>`, for example `be-passives/contextual`. Feature ids are unique across groups, so the group is omitted.
- A citation key is a key in `references.bib`: letters, digits and underscores (`biber_1988`).

## 3. feature.md

```markdown
---
tags: [tense, biber-1988]
unit: finite verb form
---
# Past tense

Finite verbs in past tense form.

## Conventions

- Irrealis *were* counts: *if I were rich*.
- *had* in *had better* is treated as a modal auxiliary and does not count.

## Notes

[@biber_1988, p. 223] defines past tense through his tagger.
```

- The **front matter** (YAML between `---` lines) requires `tags` and `unit`, and optionally accepts `subsumed_by`. `tags` is a list of facets for browsing: linguistic categories (`tense`, `aspect`) and membership in source inventories (`biber-1988`). `unit` says what one occurrence is: a `finite verb form`, a `perfect verb phrase`.
- `subsumed_by`, when present, is a list of ids of strictly broader features (section 3.1). It is independent of tags and rule references.
- The first line of the body is `# Name`: the feature’s **name**.
- The first paragraph after the name is the **definition**. It must stand alone: someone who has never met the feature should be able to recognise an occurrence from it.
- `## Conventions` is a bullet list of the decisions that affect what counts: borderline cases, contractions, senses left out. Each bullet is one decision. Explanation goes in the notes.
- `## Notes` describe the feature and how it is detected. They do not report findings about it, such as factor loadings or which registers use it more: those are results of particular studies on particular corpora.

The `biber-1988` tag identifies membership in Biber’s inventory [@biber_1988]. The README states how much of each source inventory is currently included. Rule provenance is recorded separately with `from:` in `rules.yaml`.

Citations use Pandoc’s syntax: `[@biber_1988]`, `[@biber_1988, p. 223]`. The key must be in `references.bib`.

A feature’s value for a text is the number of its occurrences.

### 3.1 Feature subsumption

A feature may declare that its occurrences are a proper subset of those of another feature:

```yaml
# In be-passives/feature.md
---
tags: [voice]
unit: passive predication
subsumed_by: [passives]
---
```

`subsumed_by` lists feature ids, not group names, tags or rule ids. Omit it, or use an empty list, when no broader relationship is declared. An omission leaves the relationship unspecified; it does not assert disjointness. Each listed id must be valid, unique within the list, and identify a different feature present in the catalogue. Multiple broader features are allowed.

Every occurrence of the narrower feature must also be an occurrence of the broader feature, with the same underlying counted object. Unit descriptions may differ in specificity, as with a contracted perfect auxiliary and a finite verb form, but the counting conventions must be compatible. This is an assertion about feature definitions, independent of what particular detection rules return. Structural validation cannot establish linguistic subsumption or unit compatibility from their prose descriptions.

The initial relationships are BE passives and GET passives under passives, and contracted perfect HAD under past tense. Contracted perfect HAD is not placed under perfect aspect: the contracted auxiliary and the perfect predicate are different counted objects. The presence of one can entail the presence of the other without being occurrence subsumption. Neither presence entailment nor rule dependency belongs in this relation.

Relations compose transitively: if A is subsumed by B and B by C, A is subsumed by C. The stored links express strict subsumption, so self-links and cycles are invalid. Together with implicit self-comparisons, this defines a partial order on feature ids. Equivalent definitions must not be encoded as a cycle; an explicit equivalence mechanism is outside this version of the format.

Authors may list a broader feature even when it is already implied through another listed feature. Consumers can derive the transitive closure and the cover relation (the transitive reduction). A Hasse diagram displays only cover links, with broader features above narrower ones. Unconnected features have no declared relationship; the diagram does not infer one from names, tags, shared examples or rule references.

Subsumption does not inherit rules, copy examples, generate detections or add feature counts together. A broader detector may miss a narrower detector's result, or the narrower detector may overcount. Such disagreements concern detection methods and do not automatically invalidate the semantic declaration. Comparing detector outputs requires compatible annotations and an explicit choice of rule pair and occurrence alignment; this format does not select those implicitly.

## 4. rules.yaml

A feature’s `rules.yaml` lists the ways it has been, or could be, detected: rules CLEF proposes, and rules taken from publications and tools. Each **rule** is a complete, alternative way of finding the feature’s occurrences, and an engine runs one at a time. The first rule is the default. CLEF’s own rules come first, then those from publications, then those from tools.

```yaml
rules:
  - id: xpos
    match:
      - cql: |
          [xpos="VBD"]
    note: |
      Taggers give *had* in *had better* VBD, so this rule counts it against
      the conventions.

  - id: mat
    from: mat
    match:
      - cql: |
          [xpos="VBD"]
    unless:
      - cql: |
          [form=$mat/quantifiers%c]
      - cql: |
          [form=$mat/emphatics%c]
      - cql: |
          @[form="do|does|did|doing|done"%c] [xpos="V.*" & form!=$mat/quantifiers%c]
    note: |
      MAT 1.3.2 retags DO directly followed by a verb as an emphatic.
      It also retags its quantifier forms as QUAN and its unconditional
      emphatic forms as EMPH, regardless of their supplied POS tags.
      Quantifiers are retagged first and cannot supply the verb after DO.
      Emphatics are retagged from left to right, so a following emphatic
      still supplies its input tag to the DO check. Other lexical and
      contextual retagging remains only partly represented.
```

| Key | Meaning |
|---|---|
| `id` | required; lower case with hyphens, unique in the file |
| `match` | a list of patterns producing candidate occurrences |
| `unless` | a list of exclusion patterns; a candidate is dropped when its anchor token is also an exclusion match’s anchor |
| `from` | the citation key of the publication or tool whose rule this is; left out for a rule CLEF proposes |
| `at` | where in that work: page, file and line |
| `tagsets` | the tagsets the rule’s patterns use, where they differ from the defaults (section 5.1) |
| `note` | Markdown: known misses and over-counts, and why the rule is written as it is |

Each entry under `match` or `unless` has exactly one key: `cql`, `semgrex` or `use`. The first two contain a pattern; `use` references a particular feature rule (section 5.4). Write patterns as YAML literal blocks (`cql: |`): YAML applies no escaping inside them, so what you type is what the engine sees.

### Whose rule it is

A rule with `from:` aims to reconstruct the cited source's detection behaviour within CLEF's annotation model and sentence-local evaluation. Preserve source quirks that can be represented faithfully in that model. A rule without `from:` is one CLEF proposes.

Documented exceptions are allowed where the source's processing model cannot be represented faithfully, for example when behaviour depends on unavailable document context or preprocessing. The rule's note must describe the difference and why it is retained. It must also identify other known approximation limits, such as omitted retagging passes. Recorded differences remain mismatches in reconstruction-fidelity comparisons.

Every rule is measured against the same annotated examples, using input annotations compatible with its declared tagsets. A miss or over-count can arise from the input annotations, a difference between the reconstruction and its source, or the source's treatment of the feature differing from CLEF's conventions. Comparisons with source output on the same supplied annotations check reconstruction fidelity separately. Rule notes distinguish known reconstruction limits from the source's own misses and over-counts.

### Occurrences and anchors

Every match produces a candidate occurrence with a **span**, containing the match and its context, and an **anchor**, a single token identifying what the rule has detected.

| Pattern | Span | Anchor |
|---|---|---|
| `cql` | the whole match | the token marked `@`; for a single-token pattern, that token is the implicit anchor |
| `semgrex` | from the leftmost to the rightmost matched node | the pattern’s first node |
| `use` | the referenced rule's surviving matches and their context | the rule's anchors after its own exclusions |

Every pattern must produce exactly one anchor token per match. A CQL pattern that can match more than one token must explicitly mark its anchor with `@`. This requirement applies to both `match` and `unless` patterns.

Anchors determine exclusions, counting and evaluation:

- **Exclusions**: drop a candidate when its anchor token is also the anchor of an `unless` match.
- **Counting**: after exclusions, candidates sharing the same anchor token count as one detection.
- **Evaluation**: compare the detection’s anchor with the marked pieces of an annotated occurrence, as described in section 7. The surrounding span does not determine whether the detection is correct.

An exclusion can therefore name context without excluding that context. For example, `@[form="did"%c] [xpos="VB.*"]` excludes a candidate anchored on *did*, not one anchored on the following verb.

A detection has one anchor token. An annotated occurrence may have several marked pieces, allowing different rules to identify the same construction through different anchor positions. The span remains available for displaying the detection in context.




## 5. Patterns

Evaluate patterns within individual sentences, using the sentence boundaries supplied by the annotation pipeline. A match, including its context and any exclusion pattern, must stay within one sentence. CQL `<s>` marks the start of that sentence. Apply exclusions and merge duplicate anchors within each sentence before summing counts for the text.

### 5.1 Annotation layers

Patterns refer to token annotations by their [CoNLL-U](https://universaldependencies.org/format.html) field names:

| Attribute | Contents | Default tagset |
|---|---|---|
| `form` | the word as written | none |
| `lemma` | the lemma | none |
| `upos` | universal part of speech | Universal Dependencies |
| `xpos` | language-specific part of speech | Penn Treebank |
| `feats.<Name>` | one UD morphological feature, such as `feats.Tense` | none |
| `deprel` | the dependency relation to the head | Universal Dependencies v2 |

A rule whose tool uses other labels says so with `tagsets`. pybiber’s dependency-based rules use the ClearNLP-derived dependency labels produced by spaCy’s standard English models, so they declare `tagsets: {deprel: clearnlp}`.

### 5.2 CQL

Token patterns use a subset of the [CQP](https://cwb.sourceforge.io/files/CQP_Manual/) Corpus Query Language, plus lexicon references and `feats.X`:

```
[xpos="VBD"]                                      one token
[form="did"%c]                                    %c: ignore case
[upos="VERB|AUX" & feats.Tense="Past"]            & and, | or
[(form="'s" & xpos="VBZ") | form="hath"%c]        ( ) grouping
[xpos!="VBD|VBN"]                                 != not equal
[form!=$mfte/stative-verbs%c]                     a lexicon: lexicons/mfte/stative-verbs.txt
@[lemma="have"] [xpos="RB.*"]{0,2} [xpos="VBN"]   a sequence; {n,m} repetition
[] @[xpos="VBN"]                                  [] is any token
[lemma="be"] @[xpos="VBD"]                        @ marks the anchor token
(<s> | [xpos="W.*"]) @[lemma="have"]              alternatives; <s> is the start of a sentence
@[xpos="VBN"] ([form="and|or"%c] [xpos="VBN"])*   a repeated group; * allows zero or more repetitions
```

- A quoted value is a regular expression (Python syntax) that must match the **whole** attribute value: `"VB.*"` matches VBD, and `".*ed"` matches *walked* but not *walking*.
- Matching is case-sensitive unless `%c` is given.
- Parentheses can group token sequences. `*` repeats a token or group zero or more times, with no fixed upper limit.
- `$origin/name` matches if the attribute equals any entry of the lexicon `lexicons/origin/name.txt` (with `%c`, ignoring case).
- Within a quoted CQL regular expression, `${origin/name}` inserts a non-capturing group of literal lexicon alternatives. Entries are escaped, so punctuation in them retains its literal meaning. The reference must match the attribute named in the lexicon metadata and must occur outside a character class. Escape the dollar sign to match a literal `${...}` string. The complete expression still matches the whole attribute value, and `%c` applies to the complete expression.

For example, `[form=".*\b${mat/place-adverbials}(_.*)?"%c]` matches a listed place adverbial at a word boundary within the token. The optional ending `(_.*)?` allows a literal underscore followed by zero or more characters. An underscore has no special meaning in CQL. Here it matches a character in `form`; CLEF keeps the word form and its POS tag in separate attributes.

That optional ending reproduces a detail of MAT's matching. MAT combines each word and its tag into a string such as `west_RB`, then searches for patterns such as `\bwest_`. The underscore it finds can be either the separator before the tag or an underscore already inside the word form:

| CLEF `form` (with `xpos="RB"`) | MAT's combined string | What `(_.*)?` matches in CLEF |
|---|---|---|
| `north-west` | `north-west_RB` | Nothing: `west` is at the end of `form`. |
| `west_extra` | `west_extra_RB` | `_extra`, which is part of `form`. |

The first case would match without `(_.*)?`; the second needs it to reproduce MAT's behaviour on a supplied form containing an underscore. In both cases, the whole token is the anchor.

### 5.3 Semgrex

Dependency patterns use [Stanford Semgrex](https://nlp.stanford.edu/software/tregex.shtml) syntax, with node attributes named as in section 5.1 and relation names from the rule’s `deprel` tagset:

```
{xpos:VBN} >aux {lemma:have}                  a node with an aux dependent
{} >aux {lemma:have} >/aux|cop/ {xpos:VBN}    two relations from the same node
{xpos:VBN} >aux {form:/'d/}                   a /regex/ value
{lemma:have} </aux|auxpass/ {}                a node that is the aux or auxpass dependent of another
{lemma:have} <aux ({} >cop {form:been})      an auxiliary whose head has copular been
```

`{}` is any node, and `/.../` is a regular expression that must match the whole value or relation name. Relations written after a node all start from that node. Parentheses let a related node have its own relations: in the last example, `>cop` starts from the head of HAVE. The anchor of a match is still the first node, HAVE in that example.

### 5.4 Reusing feature rules

Any feature rule can reference another rule with `use: <feature-id>/<rule-id>` in its `match` or `unless` list. The reference identifies an ordinary entry in the named feature's `rules.yaml`; reusable rules have no separate directory or format. Always specify the rule id: references do not choose a feature's default rule automatically.

For example, the contextual past-tense rule uses:

```yaml
match:
  - cql: |
      [xpos="VBD"]
  - use: contracted-perfect-had/contextual
unless:
  - use: perfect-aspect/contextual
  - use: be-passives/contextual
  - use: get-passives/contextual
  - use: have-got/contextual
  - use: have-need-to/contextual
```

Evaluate the referenced rule within the same supplied sentence as its caller. Apply its own exclusions and merge duplicate anchors before returning the result. A reference under `match` contributes those anchors as candidates; under `unless` it excludes candidates with the same anchors. It never removes the whole surrounding phrase or changes any input annotation. Reuse contributes only to the calling rule's result; feature counts are still evaluated separately, without adding dependency counts to the caller.

Anchor choice is part of the referenced rule's behaviour. In *She had left*, the contextual perfect rule anchors on *left*, so the past-tense rule can exclude that participle while retaining *had*. Another perfect rule anchored on HAVE would not be an interchangeable exclusion. References cannot override anchors or select another rule as a fallback.

References can nest and may point to rules declared later in the catalogue, including other rules in the same feature. They must resolve uniquely. Circular references are invalid, including self-references and cycles through exclusions. `use` references a complete rule; it is not text substitution inside a CQL or Semgrex pattern and cannot be quantified.

Each rule declares its own nondefault tagsets. Its defaults are those in section 5.1, independent of its caller. Rules require compatible annotation schemes for all their direct patterns and all referenced rules, including exclusions. Conflicting requirements or an explicit caller declaration that contradicts a referenced rule's requirement are invalid; callers cannot reinterpret another rule's tags.

Feature definitions, counting conventions and examples remain independent of their detection methods. A reused rule is evaluated against its own feature's examples as well as contributing to its callers. Provenance remains attached to each rule: referencing a reconstruction does not automatically make the caller a reconstruction of the same source. All rules must be valid, including ones not referenced elsewhere.

## 6. Lexicons

Keep small grammatical inventories, such as `have|has|had|having` and personal-pronoun paradigms, and alternatives specific to one pattern inline. Put named lexical inventories in lexicon files, especially when they are long or reused. Biber's adverbial lists, MAT's indefinite-pronoun list and MFTE's stative-verb and hedge lists are examples.

A lexicon is a plain-text file with one entry per line:

```
# title: Verb forms that MFTE’s v_stative list treats as stative
# from: mfte
# match: form
appear
appears
```

Comment lines of the form `# key: value` before the first entry are metadata. `title` says what the list is, `from` gives the citation key of its source, and `match` says which attribute the entries are (`form` or `lemma`). Entries are literal strings, never regular expressions. A standalone `$origin/name` reference compares the whole attribute exactly, or ignoring case with `%c`. Inside a quoted CQL regular expression, `${origin/name}` supplies escaped literal alternatives; the surrounding expression determines where they can match.

A list taken from a publication or tool lives at `lexicons/<origin>/<name>.txt`, where the origin is the source's citation key, and is referred to as `$origin/name`.

## 7. examples.txt

Examples show what the feature is. They are its test cases, the guidance for annotators, and the evidence for how well each rule works.

```
The teacher [looked] at the class and [smiled].
He has written three letters today.
    "written" is a past participle (VBN), not a past-tense form.
You {had} better go.
    HAD BETTER is treated as a modal (see Conventions).
I[?'d] read it.
    HAD or WOULD? Unresolved without more context.

@from le_foll_2024
It [fell] and [broke].
```

| Syntax | Meaning |
|---|---|
| `[…]` | one **occurrence** of the feature, represented by one contiguous piece |
| `[…]₁ … […]₁` | separate pieces of the same occurrence |
| `[?…]` | an **unresolved** case: neither required nor forbidden |
| `{…}` | a **distractor**: it looks like the feature but isn’t |
| no `[…]` or `[?…]` annotations on a line | a **negative** example, with no occurrences; it may contain distractors |
| an indented line | a **note** on the example above |
| `# …` at the start of a line | a comment |
| `@from key` | the examples below, up to the next blank line, come from the work `key` |

An unlabelled pair of square brackets marks one occurrence. To mark separate pieces of the same occurrence, put the same positive integer, written in subscript, immediately after each closing bracket. Labels apply only within one example line. For perfect aspect:

```
She [has been working].
She [has]₁, as {expected}, [left]₁.
[Has]₁ she [been working]₁?
She [has left], and he [has stayed].
```

The first three examples each contain one occurrence; the fourth contains two. A label may also group unresolved pieces (`[?…]₁ … [?…]₁`) or distractor pieces (`{…}₁ … {…}₁`). All pieces sharing a label must have the same status: definite, unresolved or distractor. Unlabelled annotations each stand alone.

Mark the parts of the construction on which a correct detection may be anchored. Different rules may identify the same occurrence through different pieces. Leave intervening context outside the marked pieces: in the examples above, neither *as expected* nor the subject *she* is part of the perfect occurrence. Each feature’s conventions explain which parts may be marked.

To recover the text passed to a rule, remove the annotation brackets, the `?` markers introducing unresolved pieces, and the subscript labels. Preserve the enclosed text and all other characters, including whitespace and punctuation. For example, `She['s left].` becomes `She's left.`. The marked pieces retain their character positions in this underlying text.

Evaluate each rule separately, after exclusions and the merging of candidates with the same anchor described in section 4. A detection can match an annotated occurrence when its anchor token overlaps at least one of that occurrence’s marked pieces in character positions. Its surrounding span plays no part in scoring.

1. Pair detections with definite annotated occurrences, matching as many occurrences as possible. Each detection and each occurrence may be paired only once. Each pair is a true positive. Among equally large pairings, maximise the number of paired detections whose anchors do not overlap unresolved pieces.
2. Each unpaired definite occurrence is a false negative.
3. An unpaired detection whose anchor overlaps an unresolved piece is not scored.
4. Every other unpaired detection is a false positive. If its anchor overlaps a distractor piece, it is a known false positive.

Finding several pieces of one occurrence does not earn several true positives. For example, separate detections anchored on *has* and *left* in the second example give one true positive and one false positive. A detection anchored on *left* is not penalised merely because its surrounding span includes the distractor *expected*.

Examples describe the **feature**, not a particular rule. When a rule fails an example, the failure is evidence of where that rule falls short. Notes say why an example is tricky, not what the feature is.

## 8. references.bib

A BibTeX file. Every citation key used anywhere in the catalogue (`[@key]` in Markdown, `from:` in rules, `@from` in examples) must be defined here. Fields that are not known are left out rather than guessed.
