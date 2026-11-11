# Archetypes, Section Composition, and Existing READMEs

Determine repository roles from actual codebase signals instead of forcing projects into rigid single-stack templates. Hybrid repositories (for example, a backend API paired with a CLI or a monorepo containing both a library and an app) should combine the relevant sections cleanly without repetition.

## 1. Archetype Detection Signals

| Archetype | Typical Codebase Signals | Primary Reader Question |
| :--- | :--- | :--- |
| **Application** (Web / Mobile / Desktop) | UI framework (`next`, `react`, `vue`, `svelte`, `flutter`, `electron`, `tauri`), pages/routes, public assets, `.env.example` | What does this app do, and how do I configure and run it locally? |
| **Backend API / Service** | HTTP/gRPC/GraphQL server (`fastapi`, `express`, `nestjs`, `gin`, `axum`, `spring`), route handlers, `Dockerfile`, `compose.yaml`, migrations | What service does this expose, how do I run it (local or Docker), and how is it configured? |
| **Library / SDK** | Exported modules (`exports`, `main`, `lib.rs`, `__init__.py`), package metadata without standalone server entrypoint, API tests | How do I install it, import it, and call the public API? |
| **CLI Tool** | Executable entrypoints (`bin` in `package.json`, `[project.scripts]`, `cmd/`, `clap`/`cobra`/`commander`/`typer`), flags/subcommands | How do I install it and what commands/flags does it support? |
| **Monorepo / Workspace** | `pnpm-workspace.yaml`, `turbo.json`, `nx.json`, Cargo/Go/uv workspaces, `apps/` and `packages/` directories | How is the workspace organized, what lives in each package, and how do root commands run? |
| **Plugin / Agent Skill / Template** | `SKILL.md`, `plugin.json`, `.claude-plugin/`, extension manifests, `references/`, `assets/` | What capability does it add, which runtimes does it support, and how do I install or trigger it? |

## 2. Section Composition

Include only sections backed by real repository evidence. Keep the top of the README scannable so readers reach installation or usage quickly.

### Core Sections (Nearly All Projects)

1. **Title & Local Logo**: Single `# Project Name` matching the manifest or repo purpose. Include a local logo image only if an asset exists in the repository.
2. **Badges (Conditional)**: Place immediately below the title only when backed by verified facts (confirmed tech stack, verified license, or real package/CI workflow files). Never invent CI status, coverage, or deploy badges.
3. **Summary**: 1–2 direct sentences stating what the software does and who or what workflow it serves.
4. **Key Capabilities**: Concise bullets describing real, implemented functionality observed in the code.
5. **Table of Contents (Conditional)**: Add only for longer documents (roughly >120 lines or multi-package/API references) where navigation materially helps readers.
6. **Quick Start / Installation & Running**: Prerequisites (versions verified from manifests, `engines`, `.nvmrc`, `Dockerfile`, or `pyproject.toml`) followed by exact setup and run commands.
7. **License**: Reference the actual `LICENSE` file (`[MIT](LICENSE)`, `[Apache-2.0](LICENSE)`). Omit for private/internal repositories unless the user asks otherwise.

### Conditional Sections by Archetype

- **Applications & Backend Services**:
  - **Architecture Overview (Conditional)**: Add a short Mermaid diagram (`flowchart` or `sequenceDiagram`) only when multiple services, queues, databases, or modules interact in a way prose cannot capture cleanly. Every node must match real modules/services.
  - **Configuration / Environment Variables**: Document variable *names*, whether required, defaults, and safe descriptions sourced from `.env.example` or config parsers.
  - **API / Endpoints Overview (Backend APIs)**: Summarize high-level route groups, auth mechanism at a conceptual level, or OpenAPI/Swagger path (`/docs`) without leaking internal secrets or security rules.
  - **Available Scripts / Docker**: Table or snippet of verified root commands (`dev`, `build`, `test`, `lint`, `docker compose up`).
  - **Project Structure**: Compact top-level tree showing real source directories only when helpful for contributors.
- **Libraries & SDKs**:
  - **Installation**: Package manager install command matching the package registry/manifest.
  - **Quick Start**: Minimal runnable import-and-call snippet using real exported symbols and realistic arguments.
  - **API Reference**: Document primary public functions, classes, options, parameters, and return types verified in source code. Link to deeper `docs/` if the API surface is large.
- **CLI Tools**:
  - **Installation**: Global install, `npx`/`uvx`, or binary build instructions matching the manifest.
  - **Usage & Examples**: Synopsis (`<tool> <command> [options]`) plus 2–3 realistic command examples verified against the CLI parser.
  - **Commands & Options**: Clean Markdown table of actual subcommands, flags, aliases, and defaults.
- **Monorepos**:
  - **Workspace Overview & Architecture**: Explain how apps and shared packages fit together (optional Mermaid dependency diagram when non-trivial).
  - **Packages / Apps Index**: Markdown table linking directly to each workspace directory (`[packages/core](./packages/core)`) with a one-line role summary.
  - **Workspace Commands**: Root-level dev, build, test, and lint commands.
  - Generate or update **only the root `README.md`** by default; touch sub-package READMEs only when explicitly asked.
- **Plugins, Extensions, & Agent Skills**:
  - **Compatibility / Supported Runtimes**: Runtimes or hosts verified from manifests/frontmatter.
  - **Installation**: Exact copy/clone/package manager/plugin install steps.
  - **Usage / Triggers**: Realistic prompts, commands, or hook lifecycle overview.
  - **Repository Structure**: Brief overview of skill/plugin files if helpful for maintainers or contributors.

## 3. Handling Existing `README.md` Files

Always inspect an existing `README.md` before proposing an update mode in Phase 2:

| Existing State | Indicators | Recommended Mode to Propose |
| :--- | :--- | :--- |
| **Missing or empty** | No `README.md`, or empty/stub file (<10 lines with title only) | **Create / Replace cleanly** (no gate needed if language/facts are clear) |
| **Framework boilerplate** | Unmodified starter text from `create-next-app`, `vite`, `cargo init`, `cookiecutter`, etc. | **Replace cleanly** (keep any user-added local images if present) |
| **Custom documentation** | Project-specific sections, custom screenshots/GIFs, architecture notes, contributor docs, or manual badges | **Preserve-and-upgrade** (keep valid custom sections and verified media; fix stale commands/paths/env vars and remove fluff), or **Surgical update** if only small parts drifted |

Never discard valid custom screenshots, diagrams, deployment notes, or external links without confirming with the user first.
