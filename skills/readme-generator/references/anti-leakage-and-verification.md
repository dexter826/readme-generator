# Anti-Leakage Boundary and Pre-Delivery Verification

A README helps users and contributors adopt or run the codebase safely. Protecting internal boundaries and verifying every technical claim against real files prevents security leaks and broken onboarding steps.

## 1. Anti-Leakage Boundary (Strict Exclusions)

Never expose the following categories in a README, even if present in repository files:

1. **Secrets and live credentials**:
   - Never copy API keys, tokens, passwords, private certificates, webhook secrets, or real database connection strings from `.env`, `secrets.*`, `config.*`, or fixture configs.
   - Only document environment variable *names*, required status, safe defaults, and synthetic placeholder values (sourced from `.env.example` or config schema definitions).
2. **Database security rules and authorization policies**:
   - Never copy or summarize granular `firestore.rules`, Storage rules, PostgreSQL/Supabase RLS policies, IAM policy documents, or internal RBAC permission matrices into an application README.
3. **Raw internal schemas and migrations**:
   - Never paste full ORM schema definitions (`schema.prisma`, SQL DDL dumps, migration histories, internal column lists for user/billing/audit tables). Mention only the database engine, ORM tool, and public migration command if verified.
4. **CI/CD pipeline internals and private infrastructure**:
   - Never copy multi-step GitHub Actions/GitLab CI YAML logic, internal deployment scripts, bastion hostnames, private IP addresses, internal staging URLs, or internal bucket/project IDs.
5. **Private repository metadata**:
   - When a repository is marked private (`"private": true` in `package.json`, internal metadata, or user-confirmed private) and has no `LICENSE` file, do not invent an open-source license or public clone URLs. Omit the `License` section or state only what the user confirmed.

### Public Contract vs Internal Implementation

| Safe to Document | Keep Out of README |
| :--- | :--- |
| Public HTTP/RPC route groups & conceptual auth method (e.g., Bearer JWT) | Internal auth token signing logic, secret salt values, or DB access rules |
| Verified CLI commands, flags, and environment variable *names* | Real `.env` values, production service account details, private webhooks |
| High-level component flow (API -> Queue -> Worker -> Postgres) | Raw SQL/Prisma table columns, internal admin endpoints, CI deploy keys |
| Confirmed test/lint/build commands (`pytest`, `npm run build`) | Step-by-step CI runner YAML internals and deployment secrets |

## 2. Pre-Delivery Verification Protocol

Before delivering or writing `README.md`, audit every item below directly against the files you inspected:

- [ ] **Commands verified**: Every install, dev, build, test, lint, migration, and Docker command matches actual scripts in manifests, `Makefile`, `Dockerfile`, or CLI entrypoints.
- [ ] **Paths verified**: Every file path, directory tree item, relative link, and image reference resolves on disk.
- [ ] **Environment variables verified**: Every documented variable name matches `.env.example` or actual config parsing code, with zero real secret values exposed.
- [ ] **API / CLI surface verified**: Exported functions, parameters, types, route groups, and CLI flags/aliases match actual source code.
- [ ] **License & visibility verified**: `License` matches an existing `LICENSE` file or explicit user confirmation; private repos do not claim a fabricated license.
- [ ] **Anti-leakage passed**: Zero secrets, DB security rules, raw internal schemas, CI internals, or internal URLs leaked.
- [ ] **Style check passed**: Zero marketing buzzwords, zero translationese, language identifiers on every code fence, proper Vietnamese diacritics (when writing in Vietnamese), and clean formatting.
- [ ] **Honest accounting of gaps**: Any missing info that the user chose to omit (or that could not be verified) is omitted cleanly or flagged in your closing summary rather than filled with guesswork.
