# Claude Code + MiniMax 2.5 Setup Guide

This guide covers how to integrate MiniMax 2.5 as an alternative model in Claude Code CLI using the MCP (Model Context Protocol) infrastructure.

## Why MiniMax 2.5?

- **Cost-effective**: Significantly cheaper than Claude API ($1-2/M input tokens vs $15-18/M)
- **Fast inference**: Optimized for high throughput
- **MCP Integration**: Works seamlessly through the mcp-cli tool
- **Alternative model**: Good for tasks where Claude's strengths aren't required

## Prerequisites

1. Claude Code CLI installed: `npm install -g @anthropic-ai/claude-code`
2. MiniMax API key (get from https://platform.minimax.chat/)
3. mcp-cli installed (for MCP server management)

## Setup Steps

### 1. Get MiniMax API Key

1. Sign up at https://platform.minimax.chat/
2. Navigate to API Keys section
3. Create a new API key
4. Note your API key (starts with `sk-...`)

### 2. Configure mcp-cli for MiniMax

```bash
# Check current MCP servers
mcp-cli servers

# The MiniMax integration works through mcp-cli tools
# You'll use mcp-cli call minimax-* commands to interact with MiniMax
```

### 3. Environment Variables

Add to your shell profile (~/.zshrc or ~/.bashrc):

```bash
export MINIMAX_API_KEY="sk-your-api-key-here"
```

### 4. Usage with Claude Code

The integration works through MCP tools. You can:

- Use `mcp-cli call minimax-*` commands directly
- Invoke MiniMax for specific tasks through Claude Code's tool system
- Combine Claude Code's reasoning with MiniMax's cost-effectiveness

### 5. Verification

```bash
# Test MiniMax connection
mcp-cli call minimax/chat_completion '{"model": "MiniMax-M2.5", "messages": [{"role": "user", "content": "Hello"}]}'

# Or check health
mcp-cli call minimax/health_check '{}'
```

## Cost Comparison

| Model | Input $/1M tokens | Output $/1M tokens |
|-------|-------------------|-------------------|
| Claude 3.5 Sonnet | $15 | $75 |
| Claude 3.5 Sonnet (cached) | $1.50 | $1.50 |
| MiniMax 2.5 | ~$1-2 | ~$2-4 |

## Use Cases

- **High-volume tasks**: Batch processing, code generation for multiple files
- **Cost-sensitive projects**: Learning, experimentation, prototyping
- **Alternative perspective**: When you want a different model's approach

## Integration Points

### In Claude Code

You can call MiniMax through MCP tools:

```
Use mcp-cli call minimax/* tools within Claude Code sessions
```

### In Scripts

```bash
# Direct API call example
curl -X POST 'https://api.minimax.chat/v1/text/chatcompletion_pro' \
  -H 'Authorization: Bearer sk-...' \
  -H 'Content-Type: application/json' \
  -d '{
    "model": "MiniMax-M2.5",
    "messages": [{"role": "user", "content": "Your prompt here"}]
  }'
```

## Notes

- MiniMax 2.5 is a good complement to Claude Code, not a replacement
- Claude Code still provides the best CLI experience and tool orchestration
- Use MiniMax for cost optimization on suitable tasks

## Resources

- MiniMax Platform: https://platform.minimax.chat/
- MCP CLI Docs: https://github.com/anthropics/mcp-cli
- Claude Code Docs: https://docs.anthropic.com/claude/docs/claude-code
