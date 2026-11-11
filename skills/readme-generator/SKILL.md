---
name: readme-generator
description: >-
  Generate or update evidence-grounded, production-grade README.md files for any software repository (apps, backend APIs, libraries, CLIs, monorepos, plugins, or agent skills). Use this skill whenever the user asks to create, generate, write, update, refactor, or document a project's README, invokes /readme-generator, or asks in English or Vietnamese such as "create a readme", "update README.md", "document this project", "tạo README", "viết file readme", "cập nhật readme", or "viết tài liệu giới thiệu repo" — even if they do not name a template or project type.
license: MIT
metadata:
  author: "dexter826"
  version: "1.0.1"
---

# README Generator

Write and maintain accurate, readable `README.md` documentation grounded strictly in repository evidence.

## Core Principles

- **Evidence over assumptions**: Every command, file path, environment variable, API signature, CLI flag, dependency, and license reference must trace directly to inspected repository files or explicit user answers. One broken Quick Start command destroys developer trust faster than a missing section.
- **Public boundary (anti-leakage)**: A README is a public-facing entrypoint, not an internal operations manual. Never copy real secret values, database security rules, raw internal schema dumps, CI/CD pipeline internals, or private infrastructure endpoints. Read [references/anti-leakage-and-verification.md](./references/anti-leakage-and-verification.md).
- **Direct technical prose (anti-fluff)**: Avoid promotional hype, vague qualifiers, and AI translationese in both English and Vietnamese. Readers scan a README to answer "what is this?", "does it fit my problem?", and "how do I run or install it?". Read [references/writing-and-style.md](./references/writing-and-style.md).
- **Adaptive scope**: Match sections, structure, and length to the repository's actual role and complexity (including hybrid repositories) instead of forcing every codebase into a rigid template or fixed line count. Read [references/archetypes-and-sections.md](./references/archetypes-and-sections.md).
- **Ask instead of guessing**: Never silently overwrite existing custom documentation or silently invent missing critical facts (such as a license, undocumented environment variables, or unverified production commands). Clarify gaps in one focused turn before editing.

## Execution Workflow

### Phase 1: Silent Codebase Discovery

Inspect the repository using your available file-reading and search tools before asking the user any factual questions you can answer yourself:

1. **Manifests and ecosystem**: Check root and package manifests (`package.json`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `go.mod`, `pom.xml`, `composer.json`, `SKILL.md`, `plugin.json`) and workspace definitions (`pnpm-workspace.yaml`, `turbo.json`, `nx.json`, Cargo/Go workspaces).
2. **Entrypoints and architecture**: Locate main entrypoints, API routes/controllers, CLI bin definitions, exported library modules, and container configs (`Dockerfile`, `compose.yaml` / `docker-compose.yml`).
3. **Runnable commands**: Extract verified scripts and task targets from manifests, `Makefile`, `justfile`, or container definitions.
4. **Configuration surface**: Inspect `.env.example`, `.env.template`, and config loaders to collect variable *names* and safe defaults. Never read or copy secret values from `.env` or credential files into documentation.
5. **Licensing, visibility, assets, and existing docs**:
   - Check `LICENSE` files and private markers (`"private": true`, internal registry settings).
   - Check CI workflow files only to confirm whether verified status badges/checks exist, never to copy workflow implementation details.
   - Check `docs/`, `assets/`, or `.github/` for real screenshots, logos, or diagrams.
   - Inspect any existing `README.md` to classify whether it is missing/empty, framework boilerplate, or custom documentation.

### Phase 2: Single Consolidated Clarification Gate

Before creating or modifying `README.md`, check whether any user decision or missing fact remains unresolved:

1. **Existing `README.md` present** (including framework boilerplate such as default Next.js, Vite, or Cargo starter READMEs): Summarize what currently exists (custom sections, local screenshots/badges, or boilerplate) and ask the user how to proceed:
   - **Replace cleanly**: Build a fresh structure from current repo facts (preserving valid local media paths when still relevant).
   - **Preserve-and-upgrade**: Keep valid custom sections, badges, and media while updating stale commands/paths and tightening prose.
   - **Surgical update**: Modify only specific outdated or broken sections.
2. **Ambiguous framing**: Output language (English vs Vietnamese) or repository visibility (open-source vs private/internal) is unclear from the prompt and manifests.
3. **Missing critical facts**: Essential details cannot be verified from the codebase — such as missing `LICENSE`, absent `.env.example` for environment variables referenced in code, unclear production/deploy commands, or unverified external demo/docs links. Present the verified facts you found, then ask the user to supply the missing items or confirm omitting them.

**How to ask:** Consolidate every open question into **one concise turn**. If your environment offers an interactive multiple-choice question tool, use it with a recommended default per item; otherwise present short numbered questions with recommended defaults so the user can confirm quickly.

**Fast path:** Skip Phase 2 and proceed directly to Phase 3 when **all** of the following hold:
- No `README.md` exists yet (or the user explicitly instructed how to handle the existing file, e.g., overwrite/replace or keep sections).
- Output language and repository visibility are unambiguous.
- No critical setup or usage facts are missing from the codebase.

*Note for non-interactive runs:* If you are explicitly instructed to proceed without waiting for user input, apply the safest non-destructive choice, omit unverified claims rather than inventing them, and explicitly report all unresolved gaps in your final summary.

### Phase 3: Compose or Update `README.md`

1. Load [references/archetypes-and-sections.md](./references/archetypes-and-sections.md) to identify the repository's primary (and any secondary) archetype and select the matching structural sections.
2. Load only the relevant blueprint file(s) from `assets/blueprints/` as compositional inspiration (never copy example ecosystems or assumptions blindly):
   - Applications and backend services: [assets/blueprints/app-and-api.md](./assets/blueprints/app-and-api.md)
   - Reusable libraries and CLIs: [assets/blueprints/library-and-cli.md](./assets/blueprints/library-and-cli.md)
   - Monorepos, plugins, and agent skills: [assets/blueprints/monorepo-and-plugin.md](./assets/blueprints/monorepo-and-plugin.md)
3. Follow [references/writing-and-style.md](./references/writing-and-style.md) for prose tone (English or natural Vietnamese with diacritics), code fences, conditional Mermaid diagrams, badges, local media, and Table of Contents rules.
4. For **monorepos**, generate or update the root `README.md` with a workspace overview and package index links by default; generate per-package READMEs only when requested.

### Phase 4: Pre-Delivery Verification

Before writing or finalizing `README.md`, audit your draft against [references/anti-leakage-and-verification.md](./references/anti-leakage-and-verification.md):

1. Cross-check every shell command, script name, file path, directory tree entry, environment variable name, CLI flag, and exported symbol against actual repo files.
2. Confirm no secrets, database security rules, raw internal schemas, CI internals, or private URLs appear anywhere in the draft.
3. Confirm relative links and image paths resolve inside the repository and that any Mermaid block uses valid syntax matching real modules.
4. Write `README.md` and present a concise final summary covering:
   - Update mode applied (`created`, `replaced`, `preserve-and-upgrade`, or `surgical update`).
   - Key verified facts reflected in the README (archetype, commands, configuration, license).
   - Any sections intentionally omitted or awaiting user input due to missing repo data or privacy boundaries.
