# MCP Server Basic

A basic MCP (Model Context Protocol) server and AI chat client demo. It exposes a **weather tool** powered by the [US National Weather Service API](https://www.weather.gov/documentation/services-web-api), and connects to it via an interactive CLI chat agent backed by **Groq** and **LangChain**.

## Project Structure

```
mcp-server-basic/
├── server/
│   ├── weather.py      # MCP server — exposes weather tools & resources
│   ├── client.py       # Interactive chat client using mcp-use + Groq LLM
│   └── weather.json    # MCP server config (used by the client)
├── main.py             # Placeholder entry point
├── pyproject.toml
├── .env                # API keys (not committed)
└── .python-version
```

## Features

- **`get_alerts` tool** — fetches active weather alerts for any US state (two-letter code, e.g. `CA`, `NY`) from the NWS API
- **`echo` resource** — echoes a message back via an MCP resource URI (`echo://{message}`)
- **Interactive chat loop** — multi-turn conversation with memory, powered by `llama-3.3-70b-versatile` on Groq
- **Conversation controls** — type `clear` to reset history, `exit`/`quit` to stop

## Requirements

- Python >= 3.11
- [uv](https://docs.astral.sh/uv/) package manager
- A [Groq API key](https://console.groq.com)

## Setup

1. **Clone the repo**
   ```bash
   git clone <repo-url>
   cd mcp-server-basic
   ```

2. **Install dependencies**
   ```bash
   uv sync
   ```

3. **Configure environment**
   ```bash
   cp .env.example .env
   # Edit .env and add your GROQ_API_KEY
   ```

   `.env` format:
   ```
   GROQ_API_KEY=your_key_here
   ```

## Usage

### Run the interactive chat client

```bash
uv run server/client.py
```

The agent will automatically start the MCP weather server and connect to it. You can then ask questions like:

- *"Are there any weather alerts in Texas?"*
- *"What's the current alert status for CA?"*

### Run the MCP server standalone

```bash
uv run --with mcp[cli] mcp run server/weather.py
```

## Dependencies

| Package | Purpose |
|---|---|
| `mcp[cli]` | MCP server framework (FastMCP) |
| `mcp-use` | MCP client + agent orchestration |
| `langchain-groq` | Groq LLM integration for LangChain |
| `python-dotenv` | Load `.env` API keys |
