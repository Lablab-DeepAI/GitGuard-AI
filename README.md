# GitGuardAI

## Overview

GitGuard is a Python package for secret detection in code, supporting both regex-based and LLM-based detection. It is organized as a single package (`gitguard`) containing API, MCP, and utility modules. The project integrates with Trae AI and vector databases for advanced pattern matching.

## Project Structure

```
├── gitguard/
│   ├── api/                # FastAPI server for secret detection
│   ├── mcp/                # Minimal Command Platform (MCP) for secret detection
│   └── utils/              # Utility methods (regex & LLM detection)
├── tests/                  # Additional scripts for Novita and Zilliz
├── requirements.txt        # Python dependencies
├── pyproject.toml          # Poetry project config
├── README.md               # Project documentation
```

## Pre-requisites

- Python 3.12+
- [Poetry](https://python-poetry.org/) (recommended) or pip
- For LLM-based detection: Novita API key (and optionally, API URL and model name)

## API Module

The API module provides a FastAPI server for secret detection.

**How to run:**

1. Install dependencies:
   ```bash
   poetry install
   # or
   pip install -r requirements.txt
   ```
2. Set up environment variables:
   - Copy `.env.example` to `.env` and fill in required values.
3. Run the API server:
   ```bash
   cd gitguard/api
   uvicorn main:app --reload
   ```

## MCP Module

The MCP module provides a Minimal Command Platform for secret detection in code using regex and optional LLM-based detection.

**How to run:**

1. Install dependencies (if not already done):
   ```bash
   poetry install
   # or
   pip install -r requirements.txt
   ```
2. Set environment variables for LLM-based detection (if needed):
   - `NOVITA_API_KEY` (your Novita API key)
   - `NOVITA_API_URL` (optional, defaults to https://api.novita.ai/v1/chat/completions)
   - `NOVITA_MODEL_NAME` (optional, defaults to llama3.1)
3. Start the MCP server:
   ```bash
   fastmcp dev gitguard/mcp/create_mcp.py
   ```
   Click the connect button and test in the tool section.
4. To install MCP for Claude desktop app:
   ```bash
   fastmcp install gitguard/mcp/create_mcp.py
   ```
   You will get the Claude configuration file, which can be added to TraeAI IDE (custom MCP).

The result will be a JSON string listing any detected secrets.

## Importing GitGuard Modules

After installing the package, you can import modules as follows:

```python
from gitguard.api import detector
from gitguard.mcp import create_mcp
from gitguard.utils import regex_detector, llm_detect
```

## MCP (Minimal Command Platform) Details

### Key Files

- `create_mcp.py`: Defines the MCP server and exposes a `detect` tool for secret scanning.
- `secret_detection_script.py`: Contains logic for detecting secrets using regex and, optionally, an LLM API.

### Requirements

- Python 3.12+
- Install dependencies:
  ```bash
  pip install -r requirements.txt
  ```
  or with Poetry:
  ```bash
  poetry install
  ```
- For LLM-based detection, set environment variables in a `.env` file:
  - `NOVITA_API_KEY` (your Novita API key)
  - `NOVITA_API_URL` (optional, defaults to https://api.novita.ai/v1/chat/completions)
  - `NOVITA_MODEL_NAME` (optional, defaults to llama3.1)

### How to Run MCP

Start the MCP server:

```bash
fastmcp dev gitguard/mcp/create_mcp.py
```

Click the connect button and test in the tool section.

To install MCP for Claude desktop app:

```bash
fastmcp install gitguard/mcp/create_mcp.py
```

You will get the Claude configuration file, which can be added to TraeAI IDE (custom MCP).

The result will be a JSON string listing any detected secrets.

### Secret Detection Patterns

- API Keys
- Private Keys
- Mnemonics
- Stripe API Keys
  Detection uses regex patterns and, if configured, can leverage Novita LLM for advanced detection.

## License

[MIT](./LICENSE)
