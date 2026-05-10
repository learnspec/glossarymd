# GlossaryMD — Format Specification v0.1

> Part of the **LearnSpec** suite  
> Status: Draft — May 10, 2026

---

## Core Principle

GlossaryMD is the **glossary format** of the LearnSpec suite. It centralises the definitions of key terms in a learning corpus, enabling other formats to resolve them automatically — term highlighting in text, tooltip definitions, navigation between related terms.

GlossaryMD is a **pure leaf format**: it imports and references no other LearnSpec format. It is always consumed via a `!ref` directive.

GlossaryMD is the format in the LearnSpec suite whose graceful degradation is the most natural: a Level 0 file is a perfectly readable glossary in any standard Markdown reader, with no specific syntax whatsoever.

| Principle | Description |
|---|---|
| **Markdown-first** | A `.glossary.md` Level 0 file is a pure Markdown glossary |
| **File-native** | All definitions live in the file — no database required |
| **Graceful degradation** | Headings + paragraphs — readable everywhere without tooling |
| **LaTeX from Level 0** | Mathematical formulas are available in definitions without frontmatter |
| **AI-native** | Generatable and consumable by an LLM without specific tooling |

---

## Format Levels

| Level | Mechanism | Purpose |
|---|---|---|
| 0 | `##` headings + paragraphs | Minimal glossary, readable everywhere |
| 1 | YAML frontmatter | File metadata, language |
| 2 | Optional `term` block per entry | Aliases, related terms, per-term tags |

Each level is a strict superset of the previous one.

---

## GlossaryMD File Structure

### Level 0 — Pure Markdown

Each term is a `##` heading. Its definition is the paragraph(s) immediately following that heading, before the next heading at the same level.

```markdown
# Cell Biology Glossary

## Photosynthesis

The process by which plants convert sunlight into **chemical energy**,
using $CO_2$ and $H_2O$.

$$6CO_2 + 6H_2O + \text{light} \rightarrow C_6H_{12}O_6 + 6O_2$$

## Mitosis

Cell division producing two daughter cells genetically identical to the parent cell.

*Phases: prophase → metaphase → anaphase → telophase.*

## Chloroplast

Organelle in plant cells where **photosynthesis** takes place. Contains chlorophyll,
the pigment responsible for absorbing light.
```

**Definition rules:**
- **Inline Markdown** is allowed: bold, italic, `code`, links, lists
- **Inline LaTeX** (`$...$`) and **block LaTeX** (`$$...$$`) are allowed
- **Fenced blocks are forbidden** in definitions (Mermaid, quiz, rich examples) — a definition that requires a diagram is a lesson, not a glossary entry
- Definitions may span multiple paragraphs

### Level 1 — YAML Frontmatter

```yaml
---
title: "Cell Biology Glossary"    # optional — inferred from first # H1
lang: en                           # REQUIRED — BCP-47 code
spec_version: "0.1"                # optional
author: Jane Smith                 # optional
tags: [biology, high-school]       # optional — file-level tags
created: 2026-05-10                # optional — ISO 8601
updated: 2026-05-10                # optional — ISO 8601
---
```

### Level 2 — Per-Entry `term` Block

An optional `term` block may be placed **immediately after the `##` heading**, before the definition text. It is empty — it carries only metadata attributes.

````markdown
## Photosynthesis

```term id:photosynthesis aliases:["Photosynthèse","photosynthesis"] related:["Chloroplast","Chlorophyll"] tags:[biology,botany]
```

The process by which plants convert sunlight into **chemical energy**.
````

| Attribute | Status | Description |
|---|---|---|
| `id` | Optional | Reference slug for the term. If absent, auto-generated from the heading (lowercase, no diacritics, spaces → hyphens). |
| `aliases` | Optional | Alternative names for the term — variants, abbreviations, names in other languages. The player may use them for detection in text. |
| `related` | Optional | Display names of related terms in this glossary or in other referenced GlossaryMD files. The player resolves the corresponding slugs. |
| `tags` | Optional | Term-specific tags. Added to the file-level tags from frontmatter. |

---

## Complete Example

````markdown
---
title: "Cell Biology Glossary"
lang: en
spec_version: "0.1"
tags: [biology, high-school]
---

# Cell Biology Glossary

## Photosynthesis

```term id:photosynthesis aliases:["Photosynthèse"] related:["Chloroplast","Chlorophyll","ATP"] tags:[botany,energy]
```

The process by which plants, algae, and some bacteria convert sunlight into **chemical energy**
stored as glucose.

$$6CO_2 + 6H_2O + \text{light} \rightarrow C_6H_{12}O_6 + 6O_2$$

## Mitosis

```term id:mitosis related:["Meiosis","Cell cycle"] tags:[cell-division]
```

Cell division producing two daughter cells genetically identical to the parent cell.
Occurs in four phases: **prophase**, **metaphase**, **anaphase**, **telophase**.

## Chloroplast

```term id:chloroplast related:["Photosynthesis","Chlorophyll"] tags:[organelle,botany]
```

Organelle in plant cells where **photosynthesis** takes place. Bounded by a double membrane
and containing thylakoids and stroma.

## ATP

```term id:atp aliases:["Adenosine triphosphate"] related:["Photosynthesis","Cellular respiration"]
```

The molecule $C_{10}H_{16}N_5O_{13}P_3$ — the primary energy currency of the cell.
Releases energy upon hydrolysis of a phosphate group: $ATP \rightarrow ADP + P_i$.
````

---

## Referencing from Another Format

### Declaration

A GlossaryMD is declared via the `!ref` directive at the top of the consuming document:

```markdown
!ref ./glossary-biology.glossary.md
!ref https://github.com/neuroneo/commons/blob/main/glossaries/en/biology.glossary.md
```

Multiple `!ref` directives may coexist. Terms from all referenced glossaries share the same namespace — term names must be unique across all GlossaryMD files referenced in a given document.

### Player Behaviour

A GlossaryMD-compatible player may:

- **Highlight** defined terms in the document text (and their aliases)
- **Display the definition** in a tooltip or side panel on hover or click
- **Link related terms** to enable navigation within the glossary
- **Generate a term index** at the end of the document

These behaviours are optional player features — the spec makes them possible, it does not mandate them.

---

## Automatic Slug Generation

In the absence of an `id` attribute in the `term` block, the parser generates a slug from the `##` heading text:

| Heading | Generated slug |
|---|---|
| `## Photosynthesis` | `photosynthesis` |
| `## Deoxyribonucleic acid` | `deoxyribonucleic-acid` |
| `## Ohm's Law` | `ohm-s-law` |
| `## DNA` | `dna` |

Slugification rules: lowercase, diacritics removed, spaces and apostrophes → hyphens, non-alphanumeric characters removed.

---

## Interoperability

| Mechanism | Support |
|---|---|
| Referenced via `!ref` by LearnMD | ✅ |
| Referenced via `!ref` by QuizMD | ✅ |
| Referenced via `!ref` by FlashMD | ✅ |
| Referenced via `!ref` by TrackMD | ✅ |
| `!import` of other formats | ❌ — leaf format |
| `!ref` of other formats | ❌ — leaf format |

---

## Validation

### Lenient Mode (default)

| Condition | Level |
|---|---|
| `lang` absent from frontmatter | Warning |
| No terms found (no `##` headings) | Warning |
| `term` block not immediately followed by a definition | Warning |
| `term` block without a preceding `##` heading | Error |
| Duplicate `id` within the file | Error |
| Fenced block within a definition | Error |
| Term name conflict across multiple GlossaryMD files referenced in the same document | Warning |
| Term in `related` matching no term in the glossary | Warning |

### Strict Mode (`--strict`)

All warnings are promoted to errors.

---

*Released under the MIT License. Copyright © 2024-present LearnSpec Contributors*
