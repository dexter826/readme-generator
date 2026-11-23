---
name: readme-generator
description: >-
  Generate or update evidence-grounded, production-grade README.md files for any software repository (apps, backend APIs, libraries, CLIs, monorepos, plugins, or agent skills). Use this skill whenever the user asks to create, generate, write, update, refactor, or document a project's README, invokes /readme-generator, or asks in English or Vietnamese such as "create a readme", "update README.md", "document this project", "tạo README", "viết file readme", "cập nhật readme", or "viết tài liệu giới thiệu repo" — even if they do not name a template or project type.
license: MIT
metadata:
  author: "dexter826"
  version: "1.1.0"
---

# README Generator

Write and maintain accurate, scannable, and modern `README.md` documentation grounded strictly in repository evidence and aligned collaboratively with user decisions.

## Core Principles

- **Evidence over assumptions**: Every command, file path, environment variable, API signature, CLI flag, dependency, and license reference must trace directly to inspected repository files or explicit user answers. One broken Quick Start command destroys developer trust.
- **Collaborative scoping over unilateral guessing**: Never unilaterally decide documentation depth, audience, visual layout, or overwrite custom docs without consulting the user. Discover facts silently first, then align design decisions in a focused interactive turn.
- **Global technical clarity (ESL & WIIFM)**: Value clarity over literary complexity. Aim for an accessible Flesch-Kincaid reading level ($\le$ Grade 9), active voice, short noun phrases (no modifier stacking), and open with a direct "What's in it for me" (WIIFM) statement. Read [references/writing-and-style.md](./references/writing-and-style.md).
- **Modern GitHub visual presentation**: Support context-aware Centered Hero Headers (Logo, Title, Tagline, Badges, Quick Links bar) for user-facing apps, CLIs, and repos with visual branding, while keeping pure core libraries clean and left-aligned. Use GitHub Flavored Markdown (GFM) callouts (`> [!NOTE]`, `> [!TIP]`, `> [!WARNING]`) instead of decorative emojis.
- **Anti-duplication & public boundary**: Never duplicate dedicated standalone files (`CONTRIBUTING.md`, `CHANGELOG.md`, `LICENSE`, `SECURITY.md`) into bloated README sections — link to them concisely. Never leak real secrets, DB security rules, raw schemas, or CI/CD internals. Read [references/anti-leakage-and-verification.md](./references/anti-leakage-and-verification.md).

## Execution Workflow

### Phase 1: Silent Codebase Discovery

Inspect the repository using file-reading and search tools before asking the user any factual questions you can answer yourself:

1. **Manifests and ecosystem**: Check manifests (`package.json`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `go.mod`, `pom.xml`, `composer.json`, `SKILL.md`, `plugin.json`) and workspace definitions (`pnpm-workspace.yaml`, `turbo.json`, `nx.json`, Cargo/Go workspaces).
2. **Entrypoints and architecture**: Locate main entrypoints, API routes/controllers, CLI bin definitions, exported library modules, and container configs (`Dockerfile`, `compose.yaml`).
3. **Runnable commands**: Extract verified scripts and task targets from manifests, `Makefile`, `justfile`, or container definitions.
4. **Configuration surface**: Inspect `.env.example`, `.env.template`, and config loaders for variable *names* and safe defaults. Never read or copy secret values from `.env` or credential files into documentation.
5. **Licensing, visibility, assets, and existing docs**:
   - Check `LICENSE` files and private markers (`"private": true`).
   - Check `docs/`, `assets/`, or `.github/` for real screenshots, logos, banners, or diagrams.
   - Inspect any existing `README.md` to classify whether it is missing/empty, framework boilerplate, or custom documentation. Check for satellite files (`CONTRIBUTING.md`, `CHANGELOG.md`).

### Phase 2: Collaborative Discovery & Scoping Gate

Never proceed straight to writing without consulting the user. Pause and conduct a focused alignment turn:

1. **Discovery Briefing**:
   - Summarize detected facts: Primary archetype, detected tech stack, verified runnable commands, configuration keys, and visual assets found.
   - **Existing README Diff & Upgrade Report** (if custom `README.md` exists): Present a concise comparison table: *Valid custom sections & assets to preserve* vs *Outdated commands, broken links, or stale env vars to upgrade*.
2. **Interactive Scoping Turn**:
   - Present consolidated design decisions in **one focused turn**. If an interactive question tool (`ask_question`) is available, use it with a recommended default per question (`(Recommended)`); otherwise provide short numbered questions with clear recommended choices (`➡️`).
   - Settle the design frontier:
     - **Audience & Context**: Target reader (End-users, Open-source contributors, Internal team) and context (New repository, Post-refactor overhaul, Multi-repo standardization).
     - **Scope & Depth**: Minimal Quickstart (<80 lines, fast onboarding) vs Comprehensive Guide (full architecture, config tables, troubleshooting).
     - **Layout & Visuals**: Centered Hero Header (with Logo, Badges, Quick Links bar) vs Left-aligned standard GFM; include Mermaid architecture diagram or directory tree.
     - **Core Highlights**: Confirm 2–4 key capabilities/modules to spotlight at the top.
     - **Update Strategy** (if existing `README.md` present): *Replace cleanly*, *Preserve-and-upgrade*, or *Surgical update*.

*Non-interactive bypass:* Proceed directly to Phase 3 without waiting ONLY when the user explicitly commands it in their initial prompt (e.g. `--non-interactive`, "viết luôn không cần hỏi", "generate directly without asking"), applying the safest non-destructive choices and reporting omissions.

### Phase 3: Compose or Update `README.md`

1. Load [references/archetypes-and-sections.md](./references/archetypes-and-sections.md) to structure the document according to the chosen archetype, scope, and satellite file linking rules.
2. Load only the relevant blueprint file(s) from `assets/blueprints/` for compositional structure:
   - Applications and backend services: [assets/blueprints/app-and-api.md](./assets/blueprints/app-and-api.md)
   - Reusable libraries and CLIs: [assets/blueprints/library-and-cli.md](./assets/blueprints/library-and-cli.md)
   - Monorepos, plugins, and agent skills: [assets/blueprints/monorepo-and-plugin.md](./assets/blueprints/monorepo-and-plugin.md)
3. Follow [references/writing-and-style.md](./references/writing-and-style.md) for:
   - Centered Hero Header layout (Logo, Tagline, Badges, Quick Links bar) when selected.
   - ESL technical writing standards (Flesch-Kincaid $\le$ Grade 9, active voice, no modifier stacking, 1 idea/sentence) or natural Vietnamese with proper diacritics.
   - GFM Admonitions (`> [!NOTE]`, `> [!TIP]`, `> [!WARNING]`) for callouts and `<details><summary>` for secondary reference tables.
   - Anti-duplication: Link to `CONTRIBUTING.md`, `CHANGELOG.md`, `LICENSE` concisely.
4. For **monorepos**, generate or update only the root `README.md` with package index links by default; touch sub-package READMEs only when requested.

### Phase 4: Pre-Delivery Verification

Before writing or finalizing `README.md`, audit your draft against [references/anti-leakage-and-verification.md](./references/anti-leakage-and-verification.md):

1. **Scoping & Decisions verified**: Confirm output strictly reflects the Scope, Audience, and Highlights agreed in Phase 2.
2. **Commands & Paths verified**: Every command, script, path, and link resolves against real repository files.
3. **Anti-Leakage passed**: Zero secrets, DB security rules, raw internal schemas, CI internals, or private endpoints leaked.
4. **Formatting & Style passed**: Valid GFM syntax, properly closed HTML tags if `<div align="center">` or `<details>` is used, clean GFM callouts, and zero AI-marketing fluff.
5. Write `README.md` and present a concise summary covering update mode applied, key verified sections included, and any omitted items.
