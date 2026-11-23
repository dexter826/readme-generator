# Writing, Language, and Formatting Standards

Write for readers scanning a repository to evaluate, install, configure, or contribute. Every sentence should communicate verifiable behavior with global technical clarity, scannable layout, zero marketing filler, and precise adaptation to the chosen Wording Lens.

## 1. English Prose & Readability Standards

### 1.1 Declarative Style & Anti-Fluff

- **Declarative and active**: State directly what the software does (`"FastAPI validates request payloads via Pydantic models"` rather than `"This project serves as a solution designed to effortlessly handle validation"`).
- **Specific verbs over empty adjectives**: Replace vague hype with observable facts (ports, protocols, supported formats, runtime constraints).
- **Banned AI-marketing fluff & filler**: Never use empty qualifiers and promotional clichés:
  - *Qualifiers:* `seamless`, `seamlessly`, `lightning-fast`, `blazingly fast`, `robust`, `powerful`, `cutting-edge`, `versatile`, `comprehensive`, `effortlessly`, `beautifully`, `flexible`, `game-changing`, `production-ready` (unless backed by verified test coverage/uptime), `scalable` (without metrics).
  - *Phrases:* `"in today's fast-paced world"`, `"look no further"`, `"dive into"`, `"a testament to"`, `"designed with care"`, `"serves as"`, `"acts as"`, `"empowers developers to"`.
  - *Filler:* `"It is important to note that"`, `"Notice that"`, `"Users can easily"`.

### 1.2 ESL & Global Audience Readability (Flesch-Kincaid $\le$ Grade 9)

Most developers and users reading software documentation are non-native English speakers. Write with structural clarity:

- **Target reading level**: Aim for a Flesch-Kincaid Grade level $\le$ 9. Short, well-constructed sentences communicate technical instructions faster than complex prose.
- **DO use active voice**: `"The CLI parses flags into a config struct"` (Active) instead of `"Flags are parsed into a config struct by the CLI"` (Passive).
- **DON'T stack modifiers before nouns**:
  - *Bad:* `"the recently refactored centralized authentication token verification middleware"`
  - *Good:* `"middleware that validates auth tokens"`
- **Limit embedded clauses**: Keep clauses to at most one level of nesting.
  - *Bad:* `"The worker, which starts when the queue, which receives messages from the gateway, is not empty, processes jobs."`
  - *Good:* `"The worker processes jobs from the queue. The queue receives messages from the gateway."`
- **One concept per sentence**: Break multi-part statements into distinct, digestible steps.
- **Explicit logical transitions**: Use explicit transition words (`because`, `therefore`, `however`, `instead`) rather than expecting readers to infer implicit relationships.
- **Simple conditionals**: Use standard `"if/then"` conditions. Avoid mixed or inverted conditionals (`"Had the port been occupied..."` $\rightarrow$ `"If the port is occupied..."`).
- **No idioms or cultural references**: Avoid colloquialisms, sports metaphors, or culture-specific idioms.

### 1.3 The WIIFM Formula (What's in It for Me)

Every project README must answer two questions in the first 1–2 sentences:
1. **What is it?** (Direct definition + core technology).
2. **What problem does it solve for the reader?** (Concrete benefit, workflow, or capability).

*Example:*
> `imgpack` is a command-line image optimization utility that compresses PNG and WebP assets by up to 70% without observable quality loss.

---

## 2. Vietnamese Prose Quality

When generating or updating a README in Vietnamese:

- **Proper diacritics**: Always write standard Vietnamese with complete, accurate diacritics (`có dấu đầy đủ`).
- **Preserve natural engineering terms**: Keep established technical terms in English when Vietnamese developers routinely use them in codebases (e.g., `endpoint`, `CLI`, `hook`, `middleware`, `monorepo`, `token`, `Docker`, `build`, `lint`, `webhook`) instead of forcing unnatural literal translations.
- **Eliminate translationese**: Never translate English filler word-for-word. Avoid phrases like:
  - `"đóng vai trò như một..."`, `"hoạt động như một..."` $\rightarrow$ write `"là..."` or state what it runs/exposes directly.
  - `"mang trong mình..."`, `"nhằm mục đích..."`, `"được thiết kế để..."` $\rightarrow$ state the capability directly.
  - `"một cách dễ dàng"`, `"một cách liền mạch"`, `"giúp người dùng có thể"` $\rightarrow$ drop filler and start with the action verb.
- **Eliminate Vietnamese marketing fluff**: Avoid `"mượt mà"`, `"cực nhanh"`, `"siêu tốc"`, `"mạnh mẽ"`, `"linh hoạt"`, `"toàn diện"`, `"chuẩn mực"`, `"hiện đại bậc nhất"`.
- **Feature bullet formula**: Start each capability bullet with a concrete action verb or technical noun phrase, followed by verifiable scope:
  - *Good:* `"Xác thực JWT qua middleware cho toàn bộ route /api/v1."`
  - *Good:* `"Xuất báo cáo định dạng JSON hoặc Markdown qua cờ --format."`
  - *Bad:* `"Hệ thống xác thực mạnh mẽ giúp bảo vệ ứng dụng một cách linh hoạt."`

---

## 3. Formatting, Visual Elements, and Automated Visual Conventions

Never ask the user how or where to format visual assets. The skill applies **Zero-Question Visual Conventions** based purely on real assets discovered across standard media locations (`assets/`, `docs/`, `.github/`, `media/`, `static/`, `public/`, or root):

### 3.1 Automated Header & Asset Placement

1. **No Visual Assets Found (Default for Core Libraries & Utilities)**:
   - When no logo, banner, or screenshots exist in the repository, use clean, left-aligned standard Markdown:
     ```markdown
     # project-name

     A declarative one-sentence description answering what problem the project solves.
     ```
   - Never inject empty HTML tags, placeholders, or forced centering when no visual assets exist.

2. **Logo Asset Found**:
   - **Responsive Dark/Light Pair**: When matching light and dark SVG logos exist (e.g. `logo-dark.svg` and `logo-light.svg`):
     ```html
     <p align="center">
       <picture>
         <source media="(prefers-color-scheme: dark)" srcset="<path-to-dark-logo>" />
         <source media="(prefers-color-scheme: light)" srcset="<path-to-light-logo>" />
         <img alt="Project Logo" src="<path-to-light-logo>" width="380" />
       </picture>
     </p>
     ```
   - **Single Logo / Icon**: When only one logo file exists:
     ```html
     <p align="center">
       <img src="<path-to-logo>" alt="Project Logo" width="120" />
     </p>
     ```
   - Constrain logo width reasonably (`80px` to `400px`) to prevent display distortion.

3. **Hero / Showcase Banner Found**:
   - When a dedicated banner or header image exists (`banner.*`, `hero.*`, `header.*`, `cover.*`):
     - Place as a responsive visual block immediately below the title or badge row.
     - Use `<img src="<path-to-banner>" alt="Project Banner" width="100%" />` to preserve responsive scaling.

4. **Rich Visual Walkthrough / Demo Media Found**:
   - Inspect the nature and format of the discovered visual media:
     - **Animated Media (GIF / WebP)**: Commonly used for terminal recordings or fast UI walkthroughs. Embed directly using standard Markdown `![Walkthrough](<path-to-media.gif>)`.
     - **Video Media (Hosted Video / MP4 / MOV)**: Commonly used for motion explainers or deep walkthroughs. Embed using GitHub asset video syntax or an interactive link card.
     - **Terminal Casts (Asciinema / SVG)**: Embed using standard SVG badges or asciinema player links.
     - **Static Screenshots**: UI application screen captures.
   - Title the containing section accurately based on the content role:
     - `## Demo` — For live CLI screencasts, terminal recordings, or interactive application walkthroughs.
     - `## How It Works` or `## Architecture Overview` — For visual pipeline diagrams, motion explainers, or architectural schematics.
     - `## Preview` or `## Screenshots` — For static UI or dashboard gallery captures.

5. **Quick Navigation Bar**:
   - When a Centered Hero Header is applied (branding exists), include a clean anchor navigation row separated by `•`:
     ```html
     <p align="center">
       <a href="#features">Features</a> •
       <a href="#quick-start">Quick Start</a> •
       <a href="#configuration">Configuration</a> •
       <a href="#contributing">Contributing</a> •
       <a href="#license">License</a>
     </p>
     ```

### 3.2 Badges Standardization

- **Style**: Standardize on `style=flat-square` or clean minimalist badges.
- **Alignment**: Place all badges in a single row immediately below the logo/title. Center only if the header is centered.
- **Evidence only**: Never invent build-passing, code-coverage, or live-deployment badges when no matching `.github/workflows/` or external integration exists in the repository.

### 3.3 GitHub Flavored Markdown (GFM) Admonitions

Use standard GFM alerts for technical caveats, tips, and security notes instead of random emojis:

```markdown
> [!NOTE]
> Explanatory context or runtime prerequisites.

> [!TIP]
> Useful optimization or developer productivity shortcut.

> [!IMPORTANT]
> Critical step required for setup or operation.

> [!WARNING]
> Breaking change, data migration note, or security boundary.
```

*Rules:*
- Never stack multiple admonitions back-to-back.
- Never use decorative emojis (`🔥`, `🚀`, `✨`, `⚡`, `🎉`) in section headings. Keep headings clean and professional.

### 3.4 Collapsible Sections (`<details><summary>`)

For secondary technical reference material that would otherwise bloat the README, wrap in `<details><summary>`:

```markdown
<details>
<summary><strong>Advanced CLI Flags & Options</strong></summary>

| Flag | Short | Default | Description |
| :--- | :---: | :---: | :--- |
| `--timeout` | `-t` | `30s` | Network timeout duration |
| `--verbose` | `-v` | `false` | Enable detailed debug logs |

</details>
```

*When to use:* Full CLI parameter matrices (>8 flags), advanced `.env` configuration tables, detailed OS-specific build troubleshooting, or migration matrices.

### 3.5 Headings, Code Fences, Tables, and Mermaid Diagrams

- **Heading Hierarchy**: `#` for title, `##` for top-level sections, `###` for subsections. Never skip heading levels.
- **Code Fences**: Always declare an explicit language identifier (`bash`, `sh`, `powershell`, `python`, `ts`, `go`, `json`, `yaml`, `text`, `mermaid`).
- **Markdown Tables**: Include explicit alignment indicators (`:---`, `:---:`, `---:`).
- **Mermaid Diagrams**: Include a diagram (`flowchart LR/TD` or `sequenceDiagram`) only when multi-service or multi-package flow benefits from visual representation. Keep diagrams between 4 and 12 nodes, with every node reflecting real directories or services.

---

## 4. The 4 Wording Lenses (Persona-Driven Voice)

Documentation perspective must adapt to the target audience without breaking canonical GitHub README section structure. The 4 Wording Lenses tune **vocabulary, tone, and value emphasis** across all standard sections:

### 4.1 Lens Definitions

| Wording Lens | Target Audience | Primary Focus | Vocabulary & Tone |
| :--- | :--- | :--- | :--- |
| **Developer Lens** *(Default)* | Engineers, SDK consumers, contributors | Technical mechanisms, architecture, type signatures, dev toolchains, APIs | Technical precision, explicit types, compiler flags, internal interfaces, unit test targets |
| **Product Lens** | Decision-makers, evaluators, buyers, users | Pain-point resolution, business ROI, WIIFM outcomes, key capabilities | Outcome-oriented, benefit verbs, problem $\rightarrow$ solution, zero internal implementation jargon |
| **End-User Lens** | Daily operators, CLI users, desktop/app users | Practical day-to-day command usage, output formats, task workflows | Task-oriented, step-by-step clarity, input $\rightarrow$ output, practical usage examples |
| **Ops / Admin Lens** | DevOps, SREs, platform engineers, sysadmins | Deployment, containerization, environment variables, security posture | Operational stability, health checks, ports, memory limits, TLS, audit logs |

### 4.2 Lens Comparison Matrix Across Standard Sections (Example: Background Job Scheduler)

| Section | Developer Lens | Product Lens | End-User Lens | Ops / Admin Lens |
| :--- | :--- | :--- | :--- | :--- |
| **Tagline (WIIFM)** | `"Distributed task queue written in Go with Raft consensus and zero external dependencies."` | `"Automated background job engine that eliminates server bottlenecks and cuts infrastructure costs by 40%."` | `"Command-line tool to schedule, monitor, and retry background jobs with a single command."` | `"Production-ready task daemon with Prometheus metrics, graceful drainage, and zero-downtime rolling upgrades."` |
| **Feature Bullets** | Focus on thread-safe memory pool, gRPC streaming API, sub-millisecond p99 latency, and typed client SDKs. | Focus on real-time execution visibility, automated failure recovery, predictable SLA, and eliminated data loss. | Focus on single-binary installation, human-readable terminal progress, automatic retries, and clean logging. | Focus on native Helm charts, non-root container security, configurable CPU/memory limits, and structured JSON audit trails. |
| **Quick Start** | `$ go test ./... -race`<br>`$ make build` *(How to build & verify)* | View live interactive playground or one-click sandbox setup link. | `$ taskmesh schedule --cron "0 * * * *" ./backup.sh`<br>*(Direct usage command)* | `$ helm install taskmesh ./charts/taskmesh -f values-prod.yaml`<br>*(Production deployment)* |
| **Configuration** | Internal interface overrides, worker pool concurrency flags, Raft election timeouts. | Feature tier toggles, notification webhook targets, SLA tier settings. | User CLI flags (`--verbose`, `--output`), config file path (`~/.config/app.yaml`). | Environment variables, TLS certificate paths, Prometheus scrape ports, healthcheck probe intervals. |
