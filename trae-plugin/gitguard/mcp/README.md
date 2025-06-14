# GitGuard MCP - Secret Detection

This project provides a Minimal Command Platform (MCP) for detecting secrets in code using regex and optional LLM-based detection.

## Files Overview

- **create_mcp.py**: Defines the MCP server and exposes a `detect` tool for secret scanning.
- **detector.py**: Contains the logic for detecting secrets using regex patterns and, optionally, an LLM API.

## Requirements

- Python 3.12+
- Install dependencies:
  ```bash
  pip install -r requirements.txt
  ```
  or if you're using poetry, run:
  ```bash
  poetry install
  ```

  For LLM-based detection, set the following environment variables in a .env file:
- NOVITA_API_KEY (your Novita API key)
- NOVITA_API_URL (optional, defaults to https://api.novita.ai/v1/chat/completions )
- NOVITA_MODEL_NAME (optional, defaults to llama3.1)

## How to Run MCP
Start the MCP server:
If you dont have the claude desktop app, you can use the following command:
```bash
fastmcp dev gitguard/mcp/create_mcp.py
```
Click the connect button and try testing in the tool section.

```bash
fastmcp install gitguard/mcp/create_mcp.py
```
You will get the claude configuration file.

You can add on TraeAI IDE (custom MCP).
The result will be a JSON string listing any detected secrets.

## Demonstration

Here is the link to the demonstration of building GitGuardAI by using our own MCP Server in TraeIDE:
https://www.youtube.com/@user-fj8et6iw5y/playlists

## Secret Detection Patterns
- API Keys
- Private Keys
- Mnemonics
- Stripe API Keys
Detection uses regex patterns and, if configured, can leverage Novita LLM for advanced detection.

## Running with Docker

You can also run the MCP server using Docker:
```bash
docker pull yebhonelin102273442/gitguardai
docker run -it -v "Your Claude Root Path:/root/.config/Claude" yebhonelin102273442/gitguardai      
```