# GlossaryMD

> **Status:** Draft (v0.1) — not yet stable. Part of the [LearnSpec](https://github.com/learnspec) suite.

**GlossaryMD** is an open, Markdown-based format for glossaries of key terms.

A `.glossary.md` file is valid Markdown — readable by humans, versionable in Git, and consumable by any compatible LearnSpec player. It centralises definitions of key terms in a learning corpus, enabling automatic highlighting and tooltips in compatible players.

## Specification

See [SPEC.md](./SPEC.md) for the full format specification. The shared design principles, universal frontmatter fields, and cross-format directives (`!import`, `!ref`, `!checkpoint`) are defined in the [LearnSpec Architecture Charter](https://github.com/learnspec/.github/blob/main/CHARTER.md).

## Related formats

| Format | Repo |
|---|---|
| LearnMD — instructional content | [learnspec/learnmd](https://github.com/learnspec/learnmd) |
| QuizMD — assessments | [learnspec/quizmd](https://github.com/learnspec/quizmd) |
| MediaMD — media catalogue | [learnspec/mediamd](https://github.com/learnspec/mediamd) |
| DiagramMD — diagram syntax | [learnspec/diagrammd](https://github.com/learnspec/diagrammd) |
| FlashMD — flashcards | [learnspec/flashmd](https://github.com/learnspec/flashmd) |
| GlossaryMD — glossaries | [learnspec/glossarymd](https://github.com/learnspec/glossarymd) |
| TrackMD — learning paths | [learnspec/trackmd](https://github.com/learnspec/trackmd) |
| BadgeMD — micro-credentials | [learnspec/badgemd](https://github.com/learnspec/badgemd) |
| CertMD — macro-credentials | [learnspec/certmd](https://github.com/learnspec/certmd) |

## Implementations

| Project | Type | Link |
|---------|------|------|
| neuroneo.md | Web player + API + MCP server | [neuroneo.md](https://www.neuroneo.md) |
| pylearnspec | Python parser & validator | learnspec/pylearnspec |

## License

[MIT](./LICENSE)
