# AI Development Recommendations

**Real-world AI coding toolchain from production use at [WorldArchitect.AI](https://github.com/jleechanorg/worldarchitect.ai)**

> Based on 19,044 commits over 6 months, running a production AI-powered D&D platform

---

## 🎯 What This Is

This is **NOT** a "top 10 AI tools" listicle. This is a **battle-tested toolchain** extracted from actual production usage, backed by git commit evidence and real workflow patterns.

**Evidence-based recommendations:**
- ✅ Git commit frequency analysis (6 months, 19K+ commits)
- ✅ MCP server usage metrics (5,075 diff hits)
- ✅ Slash command invocation patterns (7,950+ /copilot refs)
- ✅ Active directory analysis (29,470 file touches)
- ✅ Binary access timestamps

**What makes this different:**
- **Proven at scale** - Production system serving real users
- **Multi-agent orchestration** - 4 AI agents (copilot, cursor, codex, claude) creating branches autonomously
- **High automation** - 80+ custom slash commands, 40+ skill files
- **Quality-first** - Pre/post-commit hooks, evidence-based testing
- **Cost-conscious** - ~$40-60/mo AI services for advanced capabilities

---

## 📊 Quick Stats

| Metric | Value |
|--------|-------|
| **Git commits analyzed** | 19,044 (last 6 months) |
| **Custom slash commands** | 80+ commands, 18 heavily used |
| **MCP servers active** | 9 of 17 installed |
| **AI assistants** | 5 (Claude Code, Cursor, Antigravity, Codex, Warp) |
| **Testing commits** | 3,308 (17.4% of all work) |
| **PR automation refs** | 7,950 /copilot invocations |
| **Multi-agent branches** | 4 agent prefixes (copilot/, cursor/, codex/, claude/) |
| **Monthly AI cost** | ~$40-60 |

---

## 🚀 The Stack

### Core Tools (Used Daily)

| Tool | Evidence | Purpose |
|------|----------|---------|
| **Claude Code CLI** | 6,110 file touches | Primary AI assistant, 80+ custom commands |
| **pytest** | 3,308 commits (17.4%) | Testing framework |
| **gh CLI** | Accessed daily | GitHub automation |
| **Gemini** | 1,114 commits + 1,440 MCP hits | Primary LLM backend |
| **beads (bd)** | 259 commits, daily access | MCP-based task tracking |
| **tmux** | 287 commits | Multi-agent orchestration |

### AI Assistants (5 Active)
- **Claude Code CLI** - Terminal-first AI (Sonnet 4.5, 200K context)
- **Cursor** - AI pair programming IDE
- **Antigravity** - Experimental AI IDE
- **Codex** - Alternative AI assistant
- **Warp Terminal** - AI-enhanced terminal

### MCP Servers (9 Active)
1. **gemini-cli-mcp** (1,440 hits) - Gemini API integration
2. **grok** (670 hits) - X.ai real-time intelligence
3. **perplexity-ask** (661 hits) - Research and search
4. **sequential-thinking** (649 hits) - Enhanced reasoning
5. **beads** (539 hits) - Task management
6. **chrome-superpower** (407 hits) - Browser automation
7. **context7** (341 hits) - Library documentation
8. **claude-in-chrome** - Chrome extension control
9. **mcp_mail** (28 hits) - Agent-to-agent messaging

### Most-Used Slash Commands (18)
1. **`/copilot`** (7,950 refs) - Autonomous PR processing
2. **`/execute`** (6,332 refs) - General task execution
3. **`/fixpr`** (5,124 refs) - PR fix automation
4. **`/cerebras`** (4,901 refs) - Fast code generation
5. **`/commentreply`** (4,007 refs) - Comment automation
6. **`/commentfetch`** (2,440 refs) - Fetch PR comments
7. **`/redgreen`** (2,262 refs) - TDD workflow
8. **`/research`** (2,213 refs) - Research patterns
9. **`/testllm`** (2,172 refs) - LLM testing
10. **`/think`** (1,743 refs) - Reasoning tool
11. **`/pr`** (1,821 refs) - PR creation
12. **`/plan`** (1,753 refs) - Planning
13. **`/orch`** (1,397 refs) - Orchestration
14. **`/commentcheck`** (1,269 refs) - Comment validation
15. **`/secondo`** (106 commits) - Multi-model validation
16. **`/generatetest`** (82 commits) - Test generation
17. **`/adde2e`** (18 commits) - E2E test creation
18. **`/sync`** (26 commits) - Branch sync

### Development Tools
- **Docker + Docker Compose** - Containerization
- **Playwright** - Browser testing (69 commits)
- **Chrome DevTools Protocol** - Via MCP
- **httpie** - API testing

### Cloud & Deployment
- **Google Cloud Platform** - gcloud CLI
- **Firebase** (136 commits) - Backend services
- **Cloud Run** (192 commits) - Serverless deployment

---

## 💡 Unique Innovations

### 1. Multi-Agent Orchestration
**Evidence:** 4 agent branch prefixes (copilot/, cursor/, codex/, claude/)
- tmux-based coordination
- MCP Mail for agent messaging
- Autonomous convergence workflows
- Real production usage (not aspirational)

### 2. `/copilot` - Autonomous PR Processing
**Evidence:** 7,950 references, 68 file commits
- 4-phase workflow: Critical scan → Categorization → Implementation → Verification
- Priority-based triage: CRITICAL → BLOCKING → IMPORTANT → ROUTINE
- Hybrid execution: direct + agent delegation
- Handles 100+ comment PRs autonomously

### 3. Evidence-Based Testing
**Pattern:** `/tmp/worldarchitect.ai/<branch>/<test>/iteration_XXX/`
- Full absolute paths (never abbreviated)
- Structured bundles: README, evidence.md, logs, screenshots
- Mandatory review before success reporting
- 3,308 testing commits (17.4% of all work)

### 4. beads Task Tracking
**Evidence:** 259 commits, binary accessed daily
- MCP-integrated task system
- Used MORE than traditional issue trackers
- Real-time AI interaction with tasks

### 5. Cost-Conscious Architecture
- $40-60/mo total AI services
- Heavy automation reduces manual work
- Local classification (<50ms) vs API calls (>1500ms)
- Multi-agent parallelization

---

## 📚 Documentation

### Guides
- **[TOOLCHAIN.md](TOOLCHAIN.md)** - Complete tool inventory with evidence
- **[SETUP_GUIDE.md](SETUP_GUIDE.md)** - Installation instructions for each tool
- **[WORKFLOWS.md](WORKFLOWS.md)** - Unique workflows and automation patterns

### Evidence
- **Git analysis:** 19,044 commits (6 months)
- **MCP usage:** 5,075 diff occurrences
- **Active development:** 29,470 file touches in `mvp_site/tests`

---

## 🎓 Who This Is For

**You should use this if:**
- ✅ Building production systems with AI assistance
- ✅ Want terminal-first workflows
- ✅ Need multi-agent orchestration
- ✅ Value automation over manual work
- ✅ Cost-conscious but want advanced capabilities
- ✅ Want evidence-based recommendations (not hype)

**This is NOT for you if:**
- ❌ You prefer GUI-only tools
- ❌ You want simple autocomplete-only AI
- ❌ You're unwilling to customize/configure
- ❌ You don't write tests
- ❌ You want "works out of the box" with zero setup

---

## 🚦 Getting Started

### Minimal Setup (1 hour)
```bash
# 1. Install Claude Code CLI
npm install -g @anthropic-ai/claude-code

# 2. Install gh CLI
brew install gh

# 3. Install basic tools
brew install tmux ripgrep jq

# 4. Set API keys
export ANTHROPIC_API_KEY="sk-ant-..."
export GITHUB_TOKEN="ghp_..."

# 5. Start using
claude
```

### Full Setup (4-8 hours)
See [SETUP_GUIDE.md](SETUP_GUIDE.md) for complete installation of all 30+ tools.

### Learning Path (4 weeks)
**Week 1:** Claude Code + basic commands
**Week 2:** Add 2-3 MCP servers
**Week 3:** Testing + quality automation
**Week 4:** Multi-agent orchestration

---

## 💰 Cost Breakdown

### Current Stack
- **Claude Code Paid:** $20/mo (200K context)
- **Cursor Pro:** $20/mo
- **Optional services:** $0-20/mo (Perplexity, etc.)
- **Total:** $40-60/mo

### Cost Comparison
| Tier | Monthly | What You Get |
|------|---------|--------------|
| **Free** | $0 | VS Code + Copilot free tier, Claude free tier, all CLI tools |
| **Recommended** | $40-60 | Claude Paid + Cursor Pro + optional services |
| **Power User** | $200-240 | Claude Enterprise (500K context) + premium services |

---

## 🤝 Contributing

This repo documents **one developer's production toolchain**. It's not meant to be prescriptive.

**Contributions welcome:**
- ✅ Bug fixes in documentation
- ✅ Setup instruction improvements
- ✅ Additional evidence/metrics
- ✅ Alternative tool comparisons

**Not accepted:**
- ❌ "You should use X instead" without evidence
- ❌ Tools I don't actually use
- ❌ Promotional content

---

## 📖 Background

This toolchain evolved over 2+ years building [WorldArchitect.AI](https://github.com/jleechanorg/worldarchitect.ai), an AI-powered D&D platform. It represents:

- **19,044 commits** of real work
- **3,308 testing commits** (quality-first approach)
- **80+ custom commands** refined through use
- **4 autonomous AI agents** working in parallel
- **$40-60/mo** AI services (cost-conscious)

**Not included in this repo:**
- Custom MCP servers (proprietary)
- Slash command implementations (project-specific)
- Workflow automation scripts (WorldArchitect.AI-specific)

See the main repo for those details.

---

## 📜 License

MIT License - See [LICENSE](LICENSE)

---

## 🔗 Links

- **Main Project:** [WorldArchitect.AI](https://github.com/jleechanorg/worldarchitect.ai)
- **Author:** [@jleechan](https://github.com/jleechan)
- **Evidence:** This repo's claims are backed by git analysis in TOOLCHAIN.md

---

**Last Updated:** 2026-02-12
**Based On:** 6 months of production usage (Aug 2025 - Feb 2026)
**Commit Analysis:** 19,044 commits across WorldArchitect.AI
