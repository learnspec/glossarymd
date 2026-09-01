# GlossaryMD

> **Status:** Draft (v0.1) — not yet stable. Part of the [LearnSpec](https://github.com/learnspec) suite.

**GlossaryMD** is an open, Markdown-based format for glossaries of key terms.

A `.glossary.md` file is valid Markdown — readable by humans, versionable in Git, and consumable by any compatible LearnSpec player. It centralises definitions of key terms in a learning corpus, enabling automatic highlighting and tooltips in compatible players.

## Specification

See [SPEC.md](./SPEC.md) for the full format specification. The shared design principles, universal frontmatter fields, and cross-format directives (`!import`, `!ref`, `!checkpoint`) are defined in the [LearnSpec Architecture Charter](https://learnspec.org/charter/).

## Related formats

| Format | Repo |
|---|---|
| LearnMD: instructional content | [learnspec/learnmd](https://github.com/learnspec/learnmd) |
| QuizMD: assessments | [learnspec/quizmd](https://github.com/learnspec/quizmd) |
| FlashMD: flashcards | [learnspec/flashmd](https://github.com/learnspec/flashmd) |
| NuggetMD: micro-learning | [learnspec/nuggetmd](https://github.com/learnspec/nuggetmd) |
| ExerciseMD: exercises with solutions | [learnspec/exercisemd](https://github.com/learnspec/exercisemd) |
| TrackMD: learning paths | [learnspec/trackmd](https://github.com/learnspec/trackmd) |
| CurriculumMD: reference frameworks | [learnspec/curriculummd](https://github.com/learnspec/curriculummd) |
| MediaMD: media catalogue | [learnspec/mediamd](https://github.com/learnspec/mediamd) |
| DiagramMD: diagram syntax | [learnspec/diagrammd](https://github.com/learnspec/diagrammd) |
| AnimMD: step-reveal animations | [learnspec/animmd](https://github.com/learnspec/animmd) |
| GlossaryMD: glossaries | [learnspec/glossarymd](https://github.com/learnspec/glossarymd) |
| BadgeMD: micro-credentials | [learnspec/badgemd](https://github.com/learnspec/badgemd) |
| CertMD: macro-credentials | [learnspec/certmd](https://github.com/learnspec/certmd) |
| ListenMD: speech-only episode scripts | [learnspec/listenmd](https://github.com/learnspec/listenmd) |

## Implementations

| Project | Type | Link |
|---------|------|------|
| neuroneo.md | Web player + API + MCP server | [neuroneo.md](https://www.neuroneo.md) |
| pylearnspec | Python parser & validator | learnspec/pylearnspec |

## License

[MIT](./LICENSE)
