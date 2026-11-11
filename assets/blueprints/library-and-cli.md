# Blueprint: Libraries, SDKs, and CLI Tools

Composable section blueprint for reusable packages/SDKs and command-line tools. Keep readers focused on installation, minimal working usage, and verified public surfaces (API exports or CLI subcommands/flags).

## Suggested Section Flow

```markdown
# <Package or CLI Name>

<!-- Optional: verified registry/runtime/license badges -->

<1-2 declarative sentences stating what problem the library or CLI solves.>

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
```

## API Reference <!-- Libraries / SDKs -->

### `Client(timeout=5.0)`

Brief description of purpose and side effects.

- **Parameters**:
  - `timeout` (`float`, optional): Request timeout in seconds. Default: `5.0`.
- **Returns**: Configured `Client` instance.

## Usage <!-- CLI Tools -->

```bash
<cli-name> <command> [options] <target>
```

### Examples

```bash
# Default invocation
<cli-name> check ./src

# JSON output
<cli-name> check ./src --format json --output report.json
```

## Commands and Options <!-- CLI Tools: list verified flags/subcommands only -->

| Flag / Command | Alias | Default | Description |
| :--- | :---: | :---: | :--- |
| `--format` | `-f` | `text` | Output format (`text`, `json`) |
| `--output` | `-o` | `stdout` | Destination file path |
| `--help` | `-h` | - | Print command help |

## Development <!-- Include verified build/test steps for contributors -->

```bash
<verified test/build command>
```

## License <!-- Include only when verified LICENSE exists -->

Distributed under the [MIT](LICENSE) license.
```
