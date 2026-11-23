# Changelog

All notable changes to the `readme-generator` AgentSkill are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.2.0] - 2026-11-24

### Added

- **Zero-Question Visual Conventions**: The skill now autonomously detects and formats repository visual assets (responsive dark/light logo `<picture>` blocks, header banners, demo video sections, and badge bars) based entirely on codebase evidence. Eliminated all visual formatting and layout questions from the Scoping Gate.
- **Codebase Fact Audit & Zero-Drift Health Protocol**: Added codebase-versus-README fact auditing during Phase 1. When an existing README matches all verified commands, environment variables, dependencies, and file links (zero drift), the skill reports an integrity pass (`Fact Audit: 100% In Sync`) and presents targeted enhancement paths (Wording Lens tune, ESL clarity polish, specialized sections) rather than forcing arbitrary rewrites.
- **Zero-Drift Non-Interactive Handling**: In non-interactive mode (`--non-interactive`), confirmed zero-drift documentation exits cleanly with a health pass without modifying `README.md`.
- **4 Persona Wording Lenses**: Established 4 standardized Wording Lenses (**Developer**, **Product**, **End-User**, **Ops / Admin**) in `references/writing-and-style.md`. These lenses tune vocabulary, tone, and value proposition emphasis for target audiences while strictly preserving canonical GitHub README section architecture.

### Changed

- Streamlined Phase 2 Collaborative Scoping Gate to focus exclusively on essential intent decisions: Target Wording Lens and Key Highlights.
- Updated `references/archetypes-and-sections.md` with the Fact Audit & Drift Matrix schema and mapped archetypes to default Wording Lenses.
- Updated `references/anti-leakage-and-verification.md` with pre-delivery audit criteria for Wording Lens consistency, zero-question visuals, and zero-drift verification.
- Updated `evals/evals.json` with evaluation assertions for zero-question visual formatting, zero-drift integrity verification, and Product Wording Lens adaptation.

## [1.1.0] - 2026-11-24

### Added

- **Phase 2 Collaborative Discovery & Scoping Gate**: Replaced autonomous fast-path execution with an interactive scoping gate that pauses after silent discovery to present findings and align on Target Audience, Documentation Scope, Key Highlights, and Existing README Update Strategy using interactive multiple-choice tools (`ask_question`).
- **ESL & Global Readability Standards**: Integrated international technical writing guidelines into `references/writing-and-style.md` (Flesch-Kincaid $\le$ Grade 9, active voice, short noun phrases without modifier stacking, 1 concept per sentence, explicit logical transitions, and direct "What's in it for me" WIIFM opening formula).
- **Modern GitHub Presentation & Centered Hero Header**: Added context-aware Centered Hero Header pattern (`<div align="center">`) with Logo, Title, WIIFM Tagline, Flat-Square Badges, and Quick Links navigation bar for applications, CLIs, plugins, and repositories with visual assets.
- **GFM Admonitions & Collapsible Details**: Standardized GitHub callouts (`> [!NOTE]`, `> [!TIP]`, `> [!WARNING]`) replacing decorative emojis, and introduced `<details><summary>` collapsible blocks for secondary technical references (CLI flag matrices, advanced configs).
- **Anti-Duplication Rule for Satellite Files**: Enforced strict single-line referencing for `CONTRIBUTING.md`, `CHANGELOG.md`, `LICENSE`, `SECURITY.md`, and `CODE_OF_CONDUCT.md` to prevent bloated, duplicate documentation.
- **Existing README Diff & Upgrade Report**: Mandated a comparative audit table (*Preserve* vs *Upgrade command/env* vs *Remove*) before proposing update modes on existing custom READMEs.
- **Directory Glossary (GNU Standards)**: Added guidance for concisely documenting non-standard top-level directories (`.agents/`, `scripts/`, etc.).

### Changed

- Updated all composable blueprints (`app-and-api.md`, `library-and-cli.md`, `monorepo-and-plugin.md`) to reflect Centered Hero Headers, Quick Links, GFM Callouts, and anti-duplication references.
- Updated `evals/evals.json` test cases and expectations to verify the collaborative scoping gate, ESL readability, and modern formatting.

## [1.0.1] - 2026-11-11

### Changed

- Relocated the installable AgentSkill payload (`SKILL.md`, `references/`, and `assets/`) into `skills/readme-generator/` so `npx skills add` installs only skill files without root repository clutter.

## [1.0.0] - 2026-11-11

### Added

- Core AgentSkill definition in `SKILL.md` with a 4-phase workflow: Silent Codebase Discovery, Adaptive Scoping Gate, Architecture-Driven Authoring, and Security Audit & Verification.
- Modular reference guides in `references/` covering repository archetype detection and existing README modes (`archetypes-and-sections.md`), bilingual English/Vietnamese style and formatting rules (`writing-and-style.md`), and anti-leakage verification guardrails (`anti-leakage-and-verification.md`).
- Composable repository blueprints in `assets/blueprints/` for applications/backend APIs (`app-and-api.md`), libraries/SDKs/CLIs (`library-and-cli.md`), and monorepos/plugins/agent skills (`monorepo-and-plugin.md`).
- Evaluation test suite in `evals/evals.json`.
