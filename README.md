<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="docs/logo/readme-generator-horizontal-dark.svg" />
    <source media="(prefers-color-scheme: light)" srcset="docs/logo/readme-generator-horizontal-light.svg" />
    <img alt="readme-generator" src="docs/logo/readme-generator-horizontal-light.svg" width="460" />
  </picture>
</p>

<p align="center">
  <a href="SKILL.md"><img src="https://img.shields.io/badge/standard-AgentSkill-00cc5c?style=flat-square&labelColor=0a0a0a" alt="standard: AgentSkill" /></a>
  <a href="CHANGELOG.md"><img src="https://img.shields.io/badge/version-1.0.0-00cc5c?style=flat-square&labelColor=0a0a0a" alt="version: 1.0.0" /></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-00cc5c?style=flat-square&labelColor=0a0a0a" alt="license: MIT" /></a>
</p>

# readme-generator

Cross-platform AgentSkill for generating and updating evidence-grounded `README.md` documentation across software repositories.

## Overview

`readme-generator` guides AI coding agents to inspect actual repository files first, resolve missing context or existing-file strategies in a single clarification turn, and produce direct technical documentation without hallucinated commands, marketing filler, or leaked internal configuration.

## Capabilities

- **Codebase-first discovery**: Extracts verified runtimes, dependencies, entrypoints, scripts, environment variable names, licenses, and local visual assets from real repository files.
- **Adaptive clarification gate**: Consolidates ambiguous choices (output language, repository visibility, missing critical metadata, or how to handle an existing `README.md`) into one concise question turn instead of overwriting custom docs or inventing defaults.
- **Flexible archetype composition**: Supports web/mobile/desktop applications, backend APIs, libraries/SDKs, CLI tools, monorepos, plugins/agent skills, and hybrid repositories without forcing fixed templates or line caps.
- **Anti-leakage guardrails**: Excludes live credentials, database security rules, raw internal schema dumps, CI/CD workflow internals, and private endpoints.
- **Bilingual output standards**: Supports technical English and natural Vietnamese with complete diacritics and anti-translationese rules.

## Compatibility

Designed for AgentSkills-compatible coding agents without IDE-locked tool constraints:

- Antigravity
- Claude Code
- Codex
- Gemini CLI

## Installation

Copy or clone this repository into your agent's global or project-level skills directory so the skill folder is named `readme-generator`.

```bash
# Project-level installation (shared via repository)
mkdir -p .agents/skills
cp -r path/to/readme-generator .agents/skills/readme-generator

# Global installation on Unix/macOS (shared cross-runtime path)
mkdir -p ~/.agents/skills
cp -r path/to/readme-generator ~/.agents/skills/readme-generator
```

On Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force -Path "$HOME\.agents\skills" | Out-Null
Copy-Item -Recurse -Force "path\to\readme-generator" "$HOME\.agents\skills\readme-generator"
```

## Usage

Ask your agent to document a repository or invoke `/readme-generator` when supported:

- `"Create a README.md for this repository"`
- `"Update README.md to match the current FastAPI endpoints and Docker setup"`
- `"Viết file README.md bằng tiếng Việt cho repo này"`

When a repository already contains a `README.md` or lacks key setup details (such as a `LICENSE`, production run command, or `.env.example`), the skill asks once how to proceed before modifying files.

## Repository Structure

```text
readme-generator/
├── SKILL.md                                     # Core skill metadata and 4-phase workflow
├── README.md                                    # Repository documentation
├── CHANGELOG.md                                 # Release history (Keep a Changelog)
├── LICENSE                                      # MIT license
├── docs/
│   └── logo/                                    # M.O.B Signal SVG masters and symbol PNG
├── references/
│   ├── archetypes-and-sections.md               # Archetype detection, section selection, existing README modes
│   ├── writing-and-style.md                     # English/Vietnamese style, Mermaid, badges, TOC, and media rules
│   └── anti-leakage-and-verification.md         # Security boundary exclusions and pre-delivery checks
├── assets/
│   └── blueprints/
│       ├── app-and-api.md                       # Composable blueprint for apps and backend services
│       ├── library-and-cli.md                   # Composable blueprint for libraries, SDKs, and CLIs
│       └── monorepo-and-plugin.md               # Composable blueprint for monorepos, plugins, and skills
└── evals/
    └── evals.json                               # Evaluation test prompts and assertions
```

## License

Distributed under the [MIT](LICENSE) license.
