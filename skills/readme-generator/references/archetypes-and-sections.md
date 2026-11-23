# Archetypes, Section Composition, and Existing READMEs

Determine repository roles from actual codebase signals instead of forcing projects into rigid single-stack templates. Hybrid repositories (for example, a backend API paired with a CLI or a monorepo containing both a library and an app) should combine relevant sections cleanly without repetition.

## 1. Archetype Detection Signals

| Archetype | Typical Codebase Signals | Default Wording Lens | Primary Reader Question |
| :--- | :--- | :--- | :--- |
| **Application** (Web / Mobile / Desktop) | UI framework (`next`, `react`, `vue`, `svelte`, `flutter`, `electron`, `tauri`), pages/routes, public assets, `.env.example` | **Product** / **End-User** | What does this app do, and how do I configure and run it locally? |
| **Backend API / Service** | HTTP/gRPC/GraphQL server (`fastapi`, `express`, `nestjs`, `gin`, `axum`, `spring`), route handlers, `Dockerfile`, `compose.yaml`, migrations | **Developer** / **Ops** | What service does this expose, how do I run it (local or Docker), and how is it configured? |
| **Library / SDK** | Exported modules (`exports`, `main`, `lib.rs`, `__init__.py`), package metadata without standalone server entrypoint, API tests | **Developer** | How do I install it, import it, and call the public API? |
| **CLI Tool** | Executable entrypoints (`bin` in `package.json`, `[project.scripts]`, `cmd/`, `clap`/`cobra`/`commander`/`typer`), flags/subcommands | **End-User** / **Developer** | How do I install it and what commands/flags does it support? |
| **Monorepo / Workspace** | `pnpm-workspace.yaml`, `turbo.json`, `nx.json`, Cargo/Go/uv workspaces, `apps/` and `packages/` directories | **Developer** | How is the workspace organized, what lives in each package, and how do root commands run? |
| **Plugin / Agent Skill / Template** | `SKILL.md`, `plugin.json`, `.claude-plugin/`, extension manifests, `references/`, `assets/` | **Developer** / **End-User** | What capability does it add, which runtimes does it support, and how do I install or trigger it? |

---

## 2. Anti-Duplication Rule for Dedicated Satellite Files

A README is an index and overview, not an archive. When dedicated root files exist in the repository, **never copy or summarize their full text into the README**. Always provide a concise, single-line reference:

| Standalone File | What to Avoid in README | Correct README Reference |
| :--- | :--- | :--- |
| `LICENSE` | Full legal text, copyright disclaimers, warranty exclusions | `Distributed under the [MIT](LICENSE) License.` |
| `CONTRIBUTING.md` | Detailed Git branching rules, PR templates, commit guidelines | `Contributions are welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for local setup and submission guidelines.` |
| `CHANGELOG.md` | Version-by-version release notes, historic diff logs | `See [CHANGELOG.md](CHANGELOG.md) for release history and migration notes.` |
| `SECURITY.md` | Vulnerability disclosure policy details | `To report a security vulnerability, please follow our [Security Policy](SECURITY.md).` |
| `CODE_OF_CONDUCT.md` | Full community code of conduct text | `Please review our [Code of Conduct](CODE_OF_CONDUCT.md) before participating.` |

---

## 3. Directory Glossary (GNU Standards)

When a repository contains unusual top-level directories, specialized automation folders, or domain-specific layouts that new contributors would not immediately recognize, include a compact Directory Glossary:

```markdown
## Repository Structure

```text
.
├── apps/               # User-facing applications (Next.js web and Electron desktop)
├── packages/           # Shared libraries (core engine, UI tokens, API client)
├── .agents/            # Agent skill definitions and automation workflows
└── scripts/            # Build, packaging, and benchmark automation scripts
```
```

*Rule:* Only explain top-level directories that warrant explanation. Never list standard self-explanatory folders (like `node_modules/` or `dist/`).

---

## 4. Section Composition by Archetype

### Core Sections (Universal across all Archetypes & Wording Lenses)

1. **Header Block**: Centered Hero Header (with Logo, Tagline, Badges, Quick Links bar) or Left-aligned standard H1 per automated visual conventions.
2. **Summary (WIIFM)**: 1–2 direct sentences stating what the software is and the concrete problem it solves, tuned to the chosen Wording Lens.
3. **Key Capabilities**: Concise bullets describing real, implemented functionality observed in code.
4. **Quick Start / Installation & Running**: Exact verified prerequisites and setup/run commands.
5. **Configuration**: Environment variables (`.env.example`) or config parameters with types and defaults.
6. **License & Contributing**: Single-line links to `LICENSE` and `CONTRIBUTING.md`.

### Conditional Sections by Archetype

- **Applications & Backend Services**:
  - **Architecture Overview**: Mermaid diagram (`flowchart LR/TD`) when multiple services, queues, or databases interact.
  - **API / Endpoints Overview**: High-level route groups and Swagger/OpenAPI path (`/docs`), without leaking internal secrets.
  - **Available Scripts / Docker**: Table of verified commands (`dev`, `build`, `test`, `docker compose up`).
- **Libraries & SDKs**:
  - **Quick Start**: Minimal runnable import-and-call snippet using real exported symbols.
  - **API Reference**: Markdown table or concise signatures of primary public functions, parameters, and return types.
- **CLI Tools**:
  - **Synopsis & Examples**: `<tool> <command> [options]` plus 2–3 realistic command examples verified against parser.
  - **Commands & Flags**: Markdown table of subcommands and flags. For extensive flag lists (>8 flags), wrap in `<details><summary>`.
- **Monorepos**:
  - **Workspace Index**: Table linking directly to `[packages/core](./packages/core)` with one-line roles.
  - **Workspace Commands**: Root-level dev, build, test, and lint commands.
- **Plugins & Agent Skills**:
  - **Compatibility**: Verified host runtimes.
  - **Installation & Triggers**: Exact install commands and realistic prompt triggers.

---

## 5. Fact Audit, Drift Matrix & Zero-Drift Handling

When an existing `README.md` is detected in Phase 1, the skill audits the existing text against codebase reality:

### 5.1 Case A: Zero Drift (100% In Sync)

When all commands, environment variables, dependencies, and file links in the existing README match current repository files:
- **Do NOT force a rewrite or nitpick healthy text.**
- Output a clear **Fact Audit Verdict**:
  ```markdown
  ### Fact Audit: 100% In Sync
  All commands, scripts, dependencies, and configuration variables in README.md match the codebase.
  ```
- Ask the user in Phase 2 if they want targeted enhancements:
  1. **Tune Wording Lens**: Shift perspective (e.g. from Developer to Product or End-User lens).
  2. **Prose & ESL Polish**: Simplify sentence structures to Grade $\le$ 9, remove passive voice, tighten WIIFM.
  3. **Add Specialized Section**: Add FAQ, Benchmarks, Troubleshooting, or an Architecture diagram.
  4. **Keep As-Is**: Confirm healthy state and exit without changes.

### 5.2 Case B: Drift Detected (Stale Facts or New Features)

When commands fail, scripts are missing, or new packages/env vars exist:
- Compile a concise **Fact Audit & Drift Matrix**:

```markdown
### Existing README.md Audit & Drift Report

| Section / Asset | Codebase Verification | Recommendation |
| :--- | :--- | :--- |
| Architecture diagram (`docs/arch.svg`) | File exists and matches current modules | **Preserve** |
| Quick Start commands (`npm start`) | `package.json` now uses `pnpm dev` | **Upgrade command** |
| Custom FAQ / Deployment notes | Valid operational context written by user | **Preserve** |
| Deprecated env var `OLD_API_KEY` | Removed from `.env.example` & codebase | **Remove** |
| New CLI flag `--format` | Implemented in `src/cli.ts` but missing in doc | **Add to flags table** |
```

- Propose update strategies:
  1. **Preserve-and-upgrade (Recommended for custom docs)**: Keep valid custom sections, diagrams, and domain notes while updating stale commands, broken paths, and aligning formatting/ESL prose.
  2. **Surgical update**: Modify only specific broken commands or outdated tables without touching surrounding text.
  3. **Replace cleanly**: Rebuild fresh documentation from current codebase facts (preserving local media paths if still relevant). Best for boilerplate or severely drifted READMEs.
