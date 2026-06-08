# ClearML MCP Server

![ClearML MCP](https://raw.githubusercontent.com/prassanna-ravishankar/clearml-mcp/main/docs/clearml.png)

[![PyPI version](https://badge.fury.io/py/clearml-mcp.svg)](https://badge.fury.io/py/clearml-mcp)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A lightweight **Model Context Protocol (MCP) server** that enables AI assistants to interact with [ClearML](https://clear.ml) experiments, models, and projects. Get comprehensive ML experiment context and analysis directly in your AI conversations.

## ✨ Features

- **🔍 Experiment Discovery**: Find and analyze ML experiments across projects
- **📊 Performance Analysis**: Compare model metrics and training progress
- **📈 Real-time Metrics**: Access training scalars, validation curves, and convergence analysis
- **🏷️ Smart Search**: Filter tasks by name, tags, status, and custom queries
- **📦 Artifact Management**: Retrieve model files, datasets, and experiment outputs
- **🌐 Cross-platform**: Works with all major AI assistants and code editors

## 📋 Requirements

- **uv** ([installation guide](https://docs.astral.sh/uv/getting-started/installation/)) for `uvx` command
- **ClearML account** with valid API credentials in `~/clearml.conf`

## 🚀 Quick Start

### Prerequisites

You need a configured ClearML environment with your credentials in `~/clearml.conf`:

```conf
api {
  api_server = https://api.clear.ml
  web_server = https://app.clear.ml
  files_server = https://files.clear.ml
  credentials {
      "access_key": "your-access-key",
      "secret_key": "your-secret-key"
  }
  # Disable certificate verification if needed (e.g., Python SSL doesn't match
  # underscore subdomains with wildcard certs)
  # verify_certificate = false
}
```

Get your credentials from [ClearML Settings](https://app.clear.ml/settings).

### Installation

```bash
git clone https://github.com/ziadloo/clearml-mcp.git
cd clearml-mcp
uv tool install --force .
```

## 🔌 Integrations

<details>
<summary><strong>🤖 Claude Desktop</strong></summary>

Add to your Claude Desktop configuration:

**macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows**: `%APPDATA%/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "clearml": {
      "command": "uvx",
      "args": ["clearml-mcp"]
    }
  }
}
```

Alternative with pip installation:
```json
{
  "mcpServers": {
    "clearml": {
      "command": "python",
      "args": ["-m", "clearml_mcp.clearml_mcp"]
    }
  }
}
```
</details>

<details>
<summary><strong>⚡ Cursor</strong></summary>

Add to your Cursor settings (`Ctrl/Cmd + ,` → Search "MCP"):

```json
{
  "mcp.servers": {
    "clearml": {
      "command": "uvx",
      "args": ["clearml-mcp"]
    }
  }
}
```

Or add to `.cursorrules` in your project:
```
When analyzing ML experiments or asking about model performance, use the clearml MCP server to access experiment data, metrics, and artifacts.
```
</details>

<details>
<summary><strong>🔥 Continue</strong></summary>

Add to your Continue configuration (`~/.continue/config.json`):

```json
{
  "mcpServers": {
    "clearml": {
      "command": "uvx",
      "args": ["clearml-mcp"]
    }
  }
}
```
</details>

<details>
<summary><strong>🦾 Cody</strong></summary>

Add to your Cody settings:

```json
{
  "cody.experimental.mcp": {
    "servers": {
      "clearml": {
        "command": "uvx",
        "args": ["clearml-mcp"]
      }
    }
  }
}
```
</details>

<details>
<summary><strong>🧠 Other AI Assistants</strong></summary>

For any MCP-compatible AI assistant, use this configuration:

```json
{
  "mcpServers": {
    "clearml": {
      "command": "uvx",
      "args": ["clearml-mcp"]
    }
  }
}
```

**Compatible with:**
- Zed Editor
- OpenHands
- Roo-Cline
- Any MCP-enabled application
</details>

## 🛠️ Available Tools

The ClearML MCP server provides **36 comprehensive tools** for complete ML management, monitoring, and analysis:

### 📊 Task Read Operations
- `get_task_info` - Get detailed task information, parameters, and status
- `list_tasks` - List tasks with advanced filtering (project, status, tags, user)
- `get_task_parameters` - Retrieve hyperparameters and configuration
- `get_task_metrics` - Access training metrics, scalars, and plots
- `get_task_artifacts` - Get metadata for artifacts, model weights, and outputs

### ⚙️ Task Mutation Operations
- `create_task` - Create a new task/experiment with name, project, tags, and parameters
- `clone_task` - Clone an existing task or experiment
- `enqueue_task` - Enqueue a task to an execution queue
- `change_task_status` - Reset, start, fail, stop, or publish a task
- `update_task_tags` - Add or remove tags for a specific task
- `update_task_parameters` - Update hyperparameters of a task
- `upload_task_artifact` - Upload a local file or directory as a task artifact
- `download_task_artifact` - Download a task artifact to local storage

### 🤖 Model Operations
- `get_model_info` - Get input/output model metadata and configuration details
- `list_models` - Browse available registered models with filtering
- `get_model_artifacts` - Access model files and download URLs
- `upload_model` - Upload/register new model weights under a task
- `download_model` - Download registered model weights to local storage

### 📁 Dataset Operations
- `list_datasets` - List available ClearML datasets
- `get_dataset_info` - Get details and file list of a specific dataset version
- `create_dataset` - Create a new dataset version under a project
- `add_files_to_dataset` - Add local files or directories to an unfinalized dataset
- `finalize_dataset` - Finalize a dataset version (uploads files to fileserver)
- `download_dataset` - Download all files of a dataset version locally
- `list_dataset_files` - List and filter files within a dataset version

### 📂 Project Operations
- `list_projects` - Discover available ClearML projects
- `get_project_stats` - Get project statistics and task summaries
- `find_project_by_pattern` - Find projects matching name patterns
- `find_experiment_in_project` - Find specific experiments within projects

### 🚦 Queue & Agent Management
- `list_queues` - List execution queues and their current entry count
- `create_queue` - Create a new execution queue
- `delete_queue` - Delete an execution queue
- `remove_task_from_queue` - Remove a task entry from a queue
- `list_agents` - List active execution agents/workers and their status

### 🔍 Analysis Tools
- `compare_tasks` - Compare multiple tasks by specific metrics
- `search_tasks` - Advanced search by name, tags, comments, and more

## 💡 Usage Examples

### Demo

[![asciicast](https://asciinema.org/a/9Bf0hiIsEqGbf3zKnkdsNIbf0.svg)](https://asciinema.org/a/9Bf0hiIsEqGbf3zKnkdsNIbf0)

Once configured, you can ask your AI assistant questions like:

- *"Show me the latest experiments in the 'computer-vision' project"*
- *"Compare the accuracy metrics between tasks task-123 and task-456"*
- *"What are the hyperparameters for the best performing model?"*
- *"Find all failed experiments from last week"*
- *"Get the training curves for my latest BERT fine-tuning"*

## 🏗️ Development

### Setup

```bash
# Clone and setup with UV
git clone https://github.com/prassanna-ravishankar/clearml-mcp.git
cd clearml-mcp
uv sync

# Run locally
uv run python -m clearml_mcp.clearml_mcp
```

### Available Commands

```bash
# Run tests with coverage
uv run task coverage

# Lint and format
uv run task lint
uv run task format

# Type checking
uv run task type

# Run examples
uv run task consolidated-debug  # Full ML debugging demo
uv run task example-simple      # Basic integration
uv run task find-experiments    # Discover real experiments
```

### Testing with MCP Inspector

```bash
# Test the MCP server directly
npx @modelcontextprotocol/inspector uvx clearml-mcp
```

## 🚨 Troubleshooting

<details>
<summary><strong>Connection Issues</strong></summary>

**"No ClearML projects accessible"**
- Verify your `~/clearml.conf` credentials
- Test with: `python -c "from clearml import Task; print(Task.get_projects())"`
- Check network access to your ClearML server

**Module not found errors**
- Try `bunx clearml-mcp` instead of `uvx clearml-mcp`
- Or use direct Python: `python -m clearml_mcp.clearml_mcp`
</details>

<details>
<summary><strong>Performance Issues</strong></summary>

**Large dataset queries**
- Use filters in `list_tasks` to limit results
- Specify `project_name` to narrow scope
- Use `task_status` filters (`completed`, `running`, `failed`)

**Slow metric retrieval**
- Request specific metrics instead of all metrics
- Use `compare_tasks` with metric names for focused analysis
</details>

## 🤝 Contributing

Contributions welcome! This project uses:

- **UV** for dependency management
- **Ruff** for linting and formatting
- **Pytest** for testing with 69% coverage
- **GitHub Actions** for CI/CD

See our [testing philosophy](.cursor/rules/testing-philosophy.mdc) and [linting approach](.cursor/rules/linting-philosophy.mdc) for development guidelines.

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

## 🔗 Links

- **PyPI**: [clearml-mcp](https://pypi.org/project/clearml-mcp/)
- **ClearML**: [clear.ml](https://clear.ml)
- **Model Context Protocol**: [MCP Specification](https://modelcontextprotocol.io/)

---

**Created by [Prass, The Nomadic Coder](https://github.com/prassanna-ravishankar)**
