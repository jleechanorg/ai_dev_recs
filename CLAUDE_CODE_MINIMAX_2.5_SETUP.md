# Claude Code + MiniMax 2.5 Setup Guide

This guide covers how to integrate MiniMax 2.5 as an alternative model in Claude Code. **Note:** MiniMax MCP currently only supports web search and image understanding - for chat completions, use the direct API.

## Why MiniMax 2.5?

- **Cost-effective**: $20/mo for 1M token context (vs $200/mo Claude Enterprise)
- **Large context**: 1M token context window
- **Web search**: Built-in MCP tool for real-time information

## Prerequisites

1. Claude Code CLI installed: `npm install -g @anthropic-ai/claude-code`
2. MiniMax API key (see setup below)
3. mcp-cli installed

## MiniMax MCP Tools (Available Now)

The MiniMax MCP server provides these tools:

```bash
# List MiniMax tools
mcp-cli tools MiniMax

# Web search
mcp-cli call MiniMax/web_search '{"query": "latest AI news 2025"}'

# Image understanding
mcp-cli call MiniMax/understand_image '{"image_url": "https://example.com/image.png", "prompt": "Describe this image"}'
```

## Using MiniMax for Chat (Direct API)

For chat completions, use the MiniMax API directly:

### 1. Get API Key

Sign up at https://platform.minimax.io and generate an API key.

### 2. Environment Setup

```bash
export MINIMAX_API_KEY="your-api-key-here"
```

### 3. API Call Example

```bash
# Use environment variable for security
curl -X POST 'https://api.minimax.chat/v1/text/chatcompletion_pro' \
  -H "Authorization: Bearer $MINIMAX_API_KEY" \
  -H 'Content-Type: application/json' \
  -d '{
    "model": "abab6.5s-chat",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```

### 4. In Claude Code

You can call MiniMax API from within Claude Code sessions using Bash tool or custom scripts.

## Cost Comparison

| Model | Context | Cost |
|-------|---------|------|
| Claude 3.5 Sonnet | 200K | $20/mo |
| Claude Enterprise | 500K | $200/mo |
| **MiniMax 2.5** | **1M** | **$20/mo** |

## Use Cases

- **Web search**: Use `MiniMax/web_search` MCP tool for real-time info
- **Image analysis**: Use `MiniMax/understand_image` MCP tool
- **High-context tasks**: Use direct API for large document processing
- **Cost optimization**: 1M context at $20/mo vs 500K at $200/mo

## Links

- MiniMax Platform: https://platform.minimax.io
- MCP CLI: https://github.com/anthropics/mcp-cli
- Claude Code: https://docs.anthropic.com/claude/docs/claude-code
