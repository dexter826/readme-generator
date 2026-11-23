---
name: readme-generator
description: >-
  Generate or update evidence-grounded, production-grade README.md files for any software repository (apps, backend APIs, libraries, CLIs, monorepos, plugins, or agent skills). Use this skill whenever the user asks to create, generate, write, update, refactor, or document a project's README, invokes /readme-generator, or asks in English or Vietnamese such as "create a readme", "update README.md", "document this project", "tạo README", "viết file readme", "cập nhật readme", or "viết tài liệu giới thiệu repo" — even if they do not name a template or project type.
license: MIT
metadata:
  author: "dexter826"
  version: "1.2.0"
---

# README Generator

Write and maintain accurate, scannable, and modern `README.md` documentation grounded strictly in repository evidence, adapted to persona wording lenses, and aligned collaboratively with project requirements.

## Core Principles

- **Evidence over assumptions**: Every command, file path, environment variable, API signature, CLI flag, dependency, and license reference must trace directly to inspected repository files or explicit user instructions. One broken Quick Start command destroys developer trust.
- **Collaborative scoping over unilateral guessing**: Never unilaterally decide documentation depth, audience lens, or overwrite custom docs without consulting the user. Discover facts silently first, audit drift, then align core intent decisions in a focused interactive turn.
- **Zero-question visual conventions**: Never burden the user with questions about format, banner placement, badge styling, or video embedding. Standardize 100% of visual presentation rules automatically based on detected assets (logos, banners, videos).
- **Integrity-first fact audit (No-Op on zero drift)**: When an existing README is already 100% accurate and synchronized with the codebase, report a clean health pass. Never nitpick or blindly rewrite healthy documentation; offer targeted wording or structural enhancements instead.
- **Persona wording lenses within standard structure**: Decouple document perspective from structural layout. Maintain standard GitHub section architecture while tuning vocabulary, tone, and emphasis across 4 Wording Lenses: **Developer**, **Product**, **End-User**, and **Ops/Admin**. Read [references/writing-and-style.md](./references/writing-and-style.md).
- **Global technical clarity (ESL & WIIFM)**: Value clarity over literary complexity. Aim for an accessible Flesch-Kincaid reading level ($\le$ Grade 9), active voice, short noun phrases (no modifier stacking), and open with a direct "What's in it for me" (WIIFM) statement.
- **Anti-duplication & public boundary**: Never duplicate dedicated standalone files (`CONTRIBUTING.md`, `CHANGELOG.md`, `LICENSE`, `SECURITY.md`) into bloated README sections — link to them concisely. Never leak real secrets, DB security rules, raw schemas, or CI/CD internals. Read [references/anti-leakage-and-verification.md](./references/anti-leakage-and-verification.md).

## Execution Workflow

### Phase 1: Silent Codebase Discovery & Fact Audit

Inspect the repository using file-reading and search tools before asking the user any factual questions you can answer yourself:

1. **Manifests and ecosystem**: Check manifests (`package.json`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `go.mod`, `pom.xml`, `composer.json`, `SKILL.md`, `plugin.json`) and workspace definitions (`pnpm-workspace.yaml`, `turbo.json`, `nx.json`, Cargo/Go workspaces).
2. **Entrypoints and architecture**: Locate main entrypoints, API routes/controllers, CLI bin definitions, exported library modules, and container configs (`Dockerfile`, `compose.yaml`).
3. **Runnable commands**: Extract verified scripts and task targets from manifests, `Makefile`, `justfile`, or container definitions.
4. **Configuration surface**: Inspect `.env.example`, `.env.template`, and config loaders for variable *names* and safe defaults. Never read or copy secret values from `.env` or credential files into documentation.
5. **Licensing, visibility, and visual assets**:
   - Check `LICENSE` files and private markers (`"private": true`).
   - Check `docs/`, `assets/`, or `.github/` for real screenshots, logos, banners, or video files.
6. **Existing README Fact Audit**:
   - If an existing `README.md` exists, audit its commands, environment variables, dependencies, and badges against codebase reality.
   - Categorize findings (see [references/archetypes-and-sections.md](./references/archetypes-and-sections.md#5-fact-audit-drift-matrix--zero-drift-handling) for the Fact Audit & Drift Matrix schema):
     - **Verified Facts** (matches current code/scripts).
     - **Stale Facts / Drift** (broken commands, deleted scripts, obsolete env vars).
     - **Missing Facts** (new endpoints, new CLI flags, newly added packages).

### Phase 2: Collaborative Discovery & Scoping Gate

Never proceed straight to writing without consulting the user. Pause and conduct a focused alignment turn:

1. **Discovery Briefing & Fact Audit Report**:
   - Summarize detected facts: Primary archetype, tech stack, verified runnable commands, configuration keys, and visual assets found.
   - **Fact Audit Verdict**:
     - *Zero Drift (100% In Sync)*: Explicitly confirm that existing commands, setup instructions, and paths match codebase reality.
     - *Drift Detected*: Present a concise comparison table: *Verified facts to preserve* vs *Stale commands/env vars to upgrade*.
2. **Interactive Scoping Turn**:
   - Present consolidated design decisions in **one focused turn** using `ask_question` (or short numbered choices with `➡️`).
   - **Apply Zero-Question Visuals**: Automatically resolve layout, banner placement, video player embedding, and badge styles. Do NOT ask the user how or where to format visual assets.
   - **Settle Core Intent Decisions**:
     - **If Zero Drift**: Ask what enhancement the user wants:
       1. *Tone & Wording Lens Tune*: Shift perspective (Developer $\leftrightarrow$ Product $\leftrightarrow$ End-User $\leftrightarrow$ Ops).
       2. *ESL Readability & Polish*: Refine prose, simplify sentence structures to Grade $\le$ 9, remove passive voice.
       3. *Add Specialized Section*: Add FAQ, Benchmarks, Troubleshooting, or Architecture diagram.
       4. *Keep As-Is*: Confirm audit pass and make no changes.
     - **If New README or Drift Detected**: Settle:
       1. *Target Wording Lens*:
          - `Developer` (Default): Technical mechanisms, architecture, build/test toolchains, internal APIs, developer setup.
          - `Product`: Value proposition, problem-solution statements, business ROI, user-facing capabilities.
          - `End-User`: Practical day-to-day command usage, task-oriented walkthrough, zero internal jargon.
          - `Ops / Admin`: Deployment, containerization flags, configuration parameters, reliability, observability.
       2. *Core Highlights to Spotlight*: Confirm 2–3 key capabilities or value propositions to emphasize at the top.

*Non-interactive bypass:* Proceed directly to Phase 3 without waiting ONLY when the user explicitly commands it in their initial prompt (e.g. `--non-interactive`, "viết luôn không cần hỏi", "generate directly without asking"), applying the safest non-destructive choices and reporting omissions. When zero drift is confirmed under non-interactive mode, report the 100% In Sync health pass and exit cleanly (Keep As-Is) without modifying `README.md`.

### Phase 3: Compose or Update `README.md`

1. Load [references/archetypes-and-sections.md](./references/archetypes-and-sections.md) to structure the document according to the chosen archetype, scope, and satellite file linking rules.
2. Load only the relevant blueprint file(s) from `assets/blueprints/` for compositional structure:
   - Applications and backend services: [assets/blueprints/app-and-api.md](./assets/blueprints/app-and-api.md)
   - Reusable libraries and CLIs: [assets/blueprints/library-and-cli.md](./assets/blueprints/library-and-cli.md)
   - Monorepos, plugins, and agent skills: [assets/blueprints/monorepo-and-plugin.md](./assets/blueprints/monorepo-and-plugin.md)
3. Follow [references/writing-and-style.md](./references/writing-and-style.md) for:
   - **Selected Wording Lens**: Apply the agreed persona vocabulary, tone, and emphasis consistently across all sections.
   - **Automated Visual Conventions**: Apply Centered Hero Header, responsive SVG `<picture>`, repository banner hero placement, GFM video embed block, badges, and quick links bar.
   - **ESL Technical Writing Standards**: Flesch-Kincaid Grade $\le$ 9, active voice, no modifier stacking, 1 concept per sentence, or natural Vietnamese with complete diacritics.
   - **GFM Admonitions & Collapsible Details**: Use `> [!NOTE]`, `> [!TIP]`, `> [!WARNING]` for callouts and `<details><summary>` for secondary reference tables.
   - **Anti-duplication**: Link to `CONTRIBUTING.md`, `CHANGELOG.md`, `LICENSE` concisely.
4. For **monorepos**, generate or update only the root `README.md` with package index links by default; touch sub-package READMEs only when requested.

### Phase 4: Pre-Delivery Verification

Before writing or finalizing `README.md`, audit your draft against [references/anti-leakage-and-verification.md](./references/anti-leakage-and-verification.md):

1. **Scoping & Decisions verified**: Confirm output strictly reflects the agreed Wording Lens, Scope, and Highlights.
2. **Commands & Paths verified**: Every command, script, path, and link resolves against real repository files.
3. **Anti-Leakage passed**: Zero secrets, DB security rules, raw internal schemas, CI internals, or private endpoints leaked.
4. **Formatting & Style passed**: Valid GFM syntax, properly closed HTML tags if `<div align="center">` or `<details>` is used, clean GFM callouts, zero visual clutter, and zero AI-marketing fluff.
5. Write `README.md` and present a concise summary covering update mode applied, key verified sections included, and any omitted items.
