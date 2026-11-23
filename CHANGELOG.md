# Changelog

All notable changes to `readme-generator` are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2026-11-24

### Added

- **Phase 2 Collaborative Discovery & Scoping Gate**: Replaced autonomous fast-path execution with an interactive scoping gate that pauses after silent discovery to present findings and align on Target Audience, Documentation Scope, Key Highlights, Visual Layout, and Existing README Update Strategy using interactive multiple-choice tools (`ask_question`).
- **ESL & Global Readability Standards**: Integrated international technical writing guidelines into `references/writing-and-style.md` (Flesch-Kincaid $\le$ Grade 9, active voice, short noun phrases without modifier stacking, 1 concept per sentence, explicit logical transitions, and direct "What's in it for me" WIIFM opening formula).
- **Modern GitHub Presentation & Centered Hero Header**: Added context-aware Centered Hero Header pattern (`<div align="center">`) with Logo, Title, WIIFM Tagline, Flat-Square Badges, and Quick Links navigation bar for applications, CLIs, plugins, and repositories with visual assets.
- **GFM Admonitions & Collapsible Details**: Standardized GitHub callouts (`> [!NOTE]`, `> [!TIP]`, `> [!WARNING]`) replacing decorative emojis, and introduced `<details><summary>` collapsible blocks for secondary technical references (CLI flag matrices, advanced configs).
- **Anti-Duplication Rule for Satellite Files**: Enforced strict single-line referencing for `CONTRIBUTING.md`, `CHANGELOG.md`, `LICENSE`, `SECURITY.md`, and `CODE_OF_CONDUCT.md` to prevent bloated, duplicate documentation.
- **Existing README Diff & Upgrade Report**: Mandated a comparative audit table (*Preserve* vs *Upgrade command/env* vs *Remove*) before proposing update modes on existing custom READMEs.
- **Directory Glossary (GNU Standards)**: Added guidance for concisely documenting non-standard top-level directories (`.agents/`, `scripts/`, etc.).

### Changed

- Bumped `metadata.version` in `skills/readme-generator/SKILL.md`, `plugin.json`, `.antigravity-plugin/plugin.json`, and `.claude-plugin/plugin.json` to `1.1.0`.
- Updated all composable blueprints (`app-and-api.md`, `library-and-cli.md`, `monorepo-and-plugin.md`) to reflect Centered Hero Headers, Quick Links, GFM Callouts, and anti-duplication references.
- Updated `evals/evals.json` test cases and expectations to verify the collaborative scoping gate, ESL readability, and modern formatting.

## [1.0.1] - 2026-11-11

### Changed

- Relocated the installable AgentSkill payload (`SKILL.md`, `references/`, and `assets/`) into `skills/readme-generator/` so `npx skills add` installs only skill files without root repository clutter.
- Updated `README.md` with execution modes, `languages: VI | EN` badge, `npx skills` CLI commands, isolated manual installation commands, updated badge links, and the `skills/readme-generator/` repository tree.
- Bumped `metadata.version` in `skills/readme-generator/SKILL.md` to `1.0.1`.

### Removed

- Removed redundant `docs/logo/README.md`.

## [1.0.0] - 2026-11-11

### Added

- Core AgentSkill definition in `SKILL.md` (`version: 1.0.0`, MIT license) with a 4-phase workflow: Silent Codebase Discovery, Adaptive Clarification Gate, Architecture-Driven Authoring, and Security Audit and Verification.
- Modular reference guides in `references/` covering repository archetype detection and existing README modes (`archetypes-and-sections.md`), bilingual English/Vietnamese style and formatting rules (`writing-and-style.md`), and anti-leakage verification guardrails (`anti-leakage-and-verification.md`).
- Composable repository blueprints in `assets/blueprints/` for apps/backend APIs (`app-and-api.md`), libraries/SDKs/CLIs (`library-and-cli.md`), and monorepos/plugins/agent skills (`monorepo-and-plugin.md`).
- Evaluation test suite in `evals/evals.json`.
- Lean M.O.B Signal logo suite (`Turned Codex`) in `docs/logo/` with light/dark horizontal and symbol SVGs, `512x512` symbol PNG fallback, usage notes, and responsive `<picture>` integration in `README.md`.
- Repository baseline files: `README.md`, `LICENSE` (MIT), `.gitignore`, `.gitattributes`, `.editorconfig`, and `CHANGELOG.md`.
