# Blueprint: Libraries, SDKs, and CLI Tools

Composable section blueprint for reusable packages, SDKs, and command-line tools. Keep readers focused on installation, minimal working snippets, and verified public surfaces (exported functions or CLI subcommands/flags).

## Suggested Section Flow

### Option A: Centered Hero Header (CLI Tools or Branded Libraries)

```html
<div align="center">

<!-- Optional: logo or CLI icon if available in docs/ or assets/ -->
<img src="./docs/logo.svg" alt="Project Logo" width="120" />

# <CLI or Library Name>

**<1 declarative sentence answering what the tool does and what's in it for the developer (WIIFM).>**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](LICENSE)
[![NPM Version](https://img.shields.io/npm/v/<pkg-name>.svg?style=flat-square)](https://www.npmjs.com/package/<pkg-name>)
[![CI](https://img.shields.io/github/actions/workflow/status/owner/repo/ci.yml?branch=main&style=flat-square)](actions)

[Features](#features) • [Installation](#installation) • [Usage](#usage) • [API / Commands](#commands-and-options) • [Contributing](#contributing) • [License](#license)

</div>

---
```

### Option B: Left-Aligned Minimal Header (Pure Core Libraries / SDKs)

```markdown
# <library-name>

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-green.svg?style=flat-square)](releases)

<1-2 declarative sentences stating what problem the library solves and its core exported functionality.>
```

---

```markdown
## Features

- **<Key Feature>**: <Concrete action and verifiable scope>
- **<Key Feature>**: <Concrete action and verifiable scope>

## Installation

<!-- Match the project's actual package ecosystem; omit unused snippets -->

```bash
# Node.js
npm install <package-name>

# Python
pip install <package-name>

# Go
go install <module-path>@latest

# Rust
cargo add <crate-name>
```

## Quick Start <!-- Libraries / SDKs -->

```python
# Minimal runnable example using actual exported symbols
from my_lib import Client

client = Client(timeout=5.0)
result = client.parse("input.json")
print(result.status)
```

## Usage <!-- CLI Tools -->

```bash
<cli-name> <command> [options] <target>
```

### Examples

```bash
# Default execution
<cli-name> analyze ./src

# Export report in JSON format
<cli-name> analyze ./src --format json --output report.json
```

## Commands and Options <!-- CLI Tools -->

| Command / Flag | Alias | Default | Description |
| :--- | :---: | :---: | :--- |
| `analyze` | - | - | Run static analysis on target directory |
| `--format` | `-f` | `text` | Output format (`text`, `json`, `markdown`) |
| `--output` | `-o` | `stdout` | Destination report file path |
| `--help` | `-h` | - | Print command help |

<!-- For extensive flag matrices (>8 flags), wrap in <details> to keep README scannable -->
<details>
<summary><strong>Advanced Configuration Flags</strong></summary>

| Flag | Default | Description |
| :--- | :---: | :--- |
| `--concurrency` | `4` | Maximum parallel worker threads |
| `--ignore` | `node_modules` | Comma-separated glob patterns to ignore |

</details>

## API Reference <!-- Libraries / SDKs -->

### `Client(timeout=5.0)`

Initializes the API client with connection parameters.

- **Parameters**:
  - `timeout` (`float`, optional): Request timeout in seconds. Default: `5.0`.
- **Returns**: Configured `Client` instance.

> [!NOTE]
> Client instances are thread-safe and can be reused across multiple requests.

## Contributing

Contributions are welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for local development setup and submission guidelines.

## License <!-- Include only when verified LICENSE exists -->

Distributed under the [MIT](LICENSE) License.
```
