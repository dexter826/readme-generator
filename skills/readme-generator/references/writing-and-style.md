# Writing, Language, and Formatting Standards

Write for engineers scanning a repository to evaluate, install, configure, or contribute. Every sentence should communicate verifiable behavior without marketing filler or robotic translation phrasing.

## 1. Prose Quality (English)

- **Declarative and active**: State directly what the software does (`"FastAPI validates request payloads via Pydantic models"` rather than `"This project serves as a solution designed to effortlessly handle validation"`).
- **Specific verbs over empty adjectives**: Replace vague hype with observable facts (ports, protocols, supported formats, runtime constraints).
- **Banned AI-marketing fluff & filler**: Avoid empty qualifiers and promotional clichés that signal ungrounded writing:
  - Qualifiers: `seamless`, `seamlessly`, `lightning-fast`, `blazingly fast`, `robust`, `powerful`, `cutting-edge`, `versatile`, `comprehensive`, `effortlessly`, `beautifully`, `flexible`, `game-changing`, `production-ready` (unless backed by concrete evidence), `scalable` (without concrete architecture/metrics).
  - Phrases: `"in today's fast-paced world"`, `"look no further"`, `"dive into"`, `"a testament to"`, `"designed with care"`, `"serves as"`, `"acts as"`, `"empowers developers to"`.
  - Filler: `"It is important to note that"`, `"Notice that"`, `"Users can easily"`.

## 2. Prose Quality (Vietnamese)

When writing or updating a README in Vietnamese:

- **Proper diacritics**: Always write standard Vietnamese with complete, accurate diacritics (`có dấu đầy đủ`).
- **Preserve natural engineering terms**: Keep established technical terms in English when Vietnamese developers routinely use them in codebases (for example: `endpoint`, `CLI`, `hook`, `middleware`, `monorepo`, `token`, `Docker`, `build`, `lint`, `webhook`) instead of forcing unnatural literal translations.
- **Eliminate translationese**: Never translate English filler word-for-word. Avoid phrases like:
  - `"đóng vai trò như một..."`, `"hoạt động như một..."` -> write `"là..."` or state what it runs/exposes directly.
  - `"mang trong mình..."`, `"nhằm mục đích..."`, `"được thiết kế để..."` -> state the capability directly.
  - `"một cách dễ dàng"`, `"một cách liền mạch"`, `"giúp người dùng có thể"` -> drop the filler and start with the action.
- **Eliminate Vietnamese marketing fluff**: Avoid `"mượt mà"`, `"cực nhanh"`, `"siêu tốc"`, `"mạnh mẽ"`, `"linh hoạt"`, `"toàn diện"`, `"chuẩn mực"`, `"hiện đại bậc nhất"`, `"mọi lúc mọi nơi"`.
- **Feature bullet formula**: Start each capability bullet with a concrete action verb or technical noun phrase, followed by verifiable scope:
  - Good: `"Xác thực JWT qua middleware cho toàn bộ route /api/v1."`
  - Good: `"Xuất báo cáo định dạng JSON hoặc Markdown qua cờ --format."`
  - Bad: `"Hệ thống xác thực mạnh mẽ giúp bảo vệ ứng dụng một cách linh hoạt."`
- **Terminology consistency**: Follow any domain glossary (`GLOSSARY.md` or consistent naming in source code) rather than inventing synonyms across sections.

## 3. Formatting and Visual Elements

### Headings, Tables, and Code Blocks

- Use a single `#` H1 heading for the project title, `##` for top-level sections, and `###` for subsections.
- Declare a language identifier on every fenced code block (`bash`, `sh`, `powershell`, `python`, `ts`, `go`, `json`, `yaml`, `text`, `mermaid`).
- Align Markdown tables with explicit alignment markers (`:---`, `:---:`, `---:`) and keep cells concise.
- For directory trees inside `text` code blocks, standard ASCII (`|--`) or clean Unicode box-drawing (`├──`, `└──`) are both fine — use one style consistently per file.

### Badges

- Include badges only for facts verified in the repository (core runtime/framework, actual `LICENSE` type, or verified registry/CI workflow files present in `.github/workflows/`).
- Never invent build-passing, test-coverage, or live-deploy badges when no corresponding workflow or external integration exists.

### Mermaid Diagrams

- Use a Mermaid diagram (`flowchart LR/TD` or `sequenceDiagram`) only when the codebase has genuinely non-trivial interactions (multiple services, worker queues, gateway -> service -> DB pipelines, or monorepo package dependencies).
- Keep diagrams readable (roughly 4–12 nodes) and verify that every node name corresponds to an actual directory, service, or module in the repository.

### Screenshots and Local Visual Assets

- If valid images, GIFs, or SVGs exist in the repository (`docs/`, `assets/`, `.github/`), embed them using verified relative paths (`![Architecture overview](./docs/architecture.png)`) with descriptive alt text.
- Never insert broken external URLs or placeholder image paths.

### Table of Contents and Emojis

- Add a Table of Contents only when the document is long enough to need quick jumping (typically >120 lines or multi-package/extensive API docs).
- Default to clean, unadorned technical headings and bullets without decorative emojis. Only use restrained emojis if the user asks for them or an existing custom README already uses them consistently.
