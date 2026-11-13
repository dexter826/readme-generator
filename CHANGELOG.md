# Changelog

All notable changes to `readme-generator` are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Plugin distribution manifests (`plugin.json`, `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`, `.agents/plugins/marketplace.json`, `.antigravity-plugin/plugin.json`) so the repository installs directly as a plugin on Claude Code, Codex, and Antigravity, with a matching install section in `README.md`.

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
