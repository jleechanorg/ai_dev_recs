# Claude Code + MiniMax 2.5 Integration

Use MiniMax 2.5 directly within Claude Code CLI via the MiniMax MCP server.

## Quick Setup

The MiniMax MCP server is already connected in your stack:

```bash
# Verify connection
mcp-cli servers | grep MiniMax

# List available tools
mcp-cli tools MiniMax
```

## Available Tools

### Web Search
```bash
mcp-cli call MiniMax/web_search '{"query": "your search query"}'
```

### Image Understanding
```bash
mcp-cli call MiniMax/understand_image '{"image_url": "https://...", "prompt": "What do you see?"}'
```

## Usage in Claude Code

Within Claude Code sessions, you can call these MCP tools directly:
- Use `MiniMax/web_search` for real-time web information
- Use `MiniMax/understand_image` for analyzing images

## Cost

- MCP tools: Included with your MiniMax API key
- API key: Get from https://platform.minimax.io

## Links

- MiniMax Platform: https://platform.minimax.io
- Claude Code: https://docs.anthropic.com/claude/docs/claude-code
