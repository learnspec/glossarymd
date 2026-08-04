# Changelog

All notable changes to the GlossaryMD specification are documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).
Versioning follows [Semantic Versioning](https://semver.org/).

---

## [0.2] — 2026-08-04

### Added
- Optional `wikidata` attribute on the per-entry `term` block: a Wikidata
  QID (`Q925`) aligning the term with a linked-data entity, or the literal
  `none` marker recording that a mapping was considered and rejected.
  Backward compatible — absent by default, ignorable by consumers that
  don't use linked data.

## [0.1] — 2026-05-10

### Added
- Initial draft of the GlossaryMD specification as part of the LearnSpec suite.
