# MCP Client

A Python MCP (Model Context Protocol) client that connects to any MCP-compatible server and lets you interact with its tools through Claude via an interactive chat loop.

## How it works

The client connects to an MCP server (Python or Node.js), discovers its available tools, and routes your natural language queries through Claude. Claude decides which tools to call, the client executes them via the MCP protocol, and the results are fed back to Claude to generate a final response.

```
You → Query → Claude (claude-sonnet-4-5) → Tool call → MCP Server → Result → Claude → Response
```

## Prerequisites

- Python 3.10+
- [uv](https://docs.astral.sh/uv/) (for running Python MCP servers)
- Node.js (for running JavaScript MCP servers)
- An Anthropic API key

## Installation

1. Clone the repository:

```bash
git clone https://github.com/Minokainduwara/MCP-Client.git
cd MCP-Client
```

2. Install dependencies:

```bash
pip install anthropic mcp python-dotenv
```

3. Create a `.env` file in the project root:

```env
ANTHROPIC_API_KEY=your-api-key-here
```

> ⚠️ Never commit your `.env` file. Add it to `.gitignore`.

## Usage

Run the client by passing the path to any MCP server script:

```bash
# Connect to a Python MCP server
python client.py path/to/server.py

# Connect to a JavaScript MCP server
python client.py path/to/server.js
```

Once connected, you'll see the available tools listed and can start typing queries:

```
Connected to server with tools: ['search', 'read_file', 'write_file']

MCP Client Started!
Type your queries or 'quit' to exit.

Query: Search for the latest news about MCP
```

Type `quit` to exit.

## Project structure

```
MCP-Client/
├── client.py       # Main MCP client implementation
├── .env            # API key (not committed)
└── README.md
```

## Key classes and methods

**`MCPClient`**

| Method | Description |
|---|---|
| `connect_to_server(path)` | Connects to a `.py` or `.js` MCP server and lists available tools |
| `process_query(query)` | Sends a query to Claude, handles tool calls, returns final response |
| `chat_loop()` | Runs the interactive REPL |
| `cleanup()` | Closes the server connection and cleans up resources |

## Supported server types

| Type | Command used | Requirement |
|---|---|---|
| Python (`.py`) | `uv run` | `uv` installed |
| JavaScript (`.js`) | `node` | Node.js installed |

## Environment variables

| Variable | Description |
|---|---|
| `ANTHROPIC_API_KEY` | Your Anthropic API key (required) |

## License

MIT