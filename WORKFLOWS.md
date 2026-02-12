# Workflows & Automation Patterns

**Unique workflows from production usage**

---

## Overview

These workflows emerged from 19,044 commits over 6 months. They're not theoretical - they're battle-tested in production.

---

## 🤖 Multi-Agent Orchestration

### Evidence
- **4 agent branch prefixes:** `copilot/`, `cursor/`, `codex/`, `claude/`
- **287 orchestration commits**
- **1,397 `/orch` command references**
- **28 mcp_mail hits** for agent communication

### How It Works

**1. tmux Session Management**
```bash
# Create orchestration session
tmux new -s orch-session

# Spawn agent windows
tmux new-window -n copilot
tmux new-window -n cursor
tmux new-window -n codex
```

**2. Agent-to-Agent Communication**
- Via **mcp_mail** MCP server
- Repo: https://github.com/jleechanorg/mcp_mail
- Agents send/receive messages
- Async coordination

**3. Task Distribution**
- `orchestration/task_dispatcher.py` (111KB file!)
- Distributes work to specialized agents
- Monitors agent health
- Handles failures and retries

**4. Branch Coordination**
- Each agent creates own branch
- Naming: `{agent_name}/task-description`
- Autonomous PR creation
- Review and merge coordination

### Example Workflow
```
User: /orch fix all PR comments

1. Orchestrator reads PR comments
2. Categorizes by type (CRITICAL, BLOCKING, IMPORTANT)
3. Spawns specialized agents:
   - copilot/ → Security issues
   - cursor/ → UI/UX fixes
   - codex/ → Logic bugs
   - claude/ → Documentation
4. Agents work in parallel
5. Each creates branch and commits
6. Orchestrator merges when all complete
```

### Key Files
- `orchestration/orchestrate_unified.py` - Main orchestrator
- `orchestration/agent_system.py` - Agent management
- `orchestration/a2a_integration.py` - Agent-to-agent messaging
- `orchestration/task_dispatcher.py` - Task distribution

---

## 🔄 `/copilot` - Autonomous PR Processing

### Evidence
- **7,950 diff references** (#1 command)
- **68 file commits** (actively refined)
- **626 commit mentions**

### 4-Phase Workflow

**Phase 0: Critical Bug Scan**
```
Priority: CRITICAL, SECURITY
Action: Immediate fix, no waiting
Output: Critical issues resolved or flagged
```

**Phase 1: Comment Categorization**
```
Categories:
- BLOCKING: Must fix before merge
- IMPORTANT: Should fix before merge
- ROUTINE: Nice to have

Triage: Based on keywords, severity, file impact
```

**Phase 2: Implementation**
```
Hybrid execution:
- Direct implementation: Simple fixes
- Agent delegation: Complex changes

Parallel work:
- Multiple agents on independent issues
- Sequential for dependent changes
```

**Phase 3: Verification**
```
- Run tests for each fix
- Verify no new failures
- Commit tracking
- Evidence generation
```

### Usage
```bash
/copilot

# Automatically:
1. Fetches all PR comments
2. Categorizes by priority
3. Implements fixes
4. Runs tests
5. Commits changes
6. Reports results
```

### Integration
- Uses `/commentfetch` (2,440 refs)
- Uses `/commentreply` (4,007 refs)
- Uses `/commentcheck` (1,269 refs)
- Uses `/fixpr` (5,124 refs) for complex fixes

---

## 🛠️ `/fixpr` - Intelligent PR Fixing

### Evidence
- **5,124 diff references** (#2 command)
- **1,299 commit mentions**
- **20 file commits**

### Workflow

**1. Analysis Phase**
```
- Read PR description
- Analyze failed checks
- Review reviewer comments
- Understand context
```

**2. Root Cause Identification**
```
- Find failing tests
- Identify error patterns
- Trace to source files
- Determine fix scope
```

**3. Implementation**
```
- Minimal code changes
- Fix root cause, not symptoms
- Update tests if needed
- Verify in isolation
```

**4. Validation**
```
- Run affected tests
- Check for regressions
- Verify CI passes
- Update PR description
```

### Usage
```bash
/fixpr

# Or with specific PR
/fixpr 123
```

---

## 🧪 `/redgreen` - Test-Driven Development

### Evidence
- **3,817 combined references** (/redgreen + /tdd)
- **162 commit mentions**
- **3,308 testing commits** (17.4% of all work)

### Red-Green Workflow

**Step 1: Red (Write Failing Test)**
```bash
# Create test that fails
pytest tests/test_new_feature.py

# Expected: FAIL
```

**Step 2: Confirm Failure**
```bash
# Verify test actually fails
# Not false positive
```

**Step 3: Green (Minimal Code)**
```bash
# Write MINIMAL code to pass
# No gold-plating
# No extra features
```

**Step 4: Verify Green**
```bash
# Test should now pass
pytest tests/test_new_feature.py

# Expected: PASS
```

**Step 5: Refactor**
```bash
# Clean up code
# Keep tests passing
# Improve design
```

**Step 6: Commit**
```bash
git add .
git commit -m "feat: Add feature X with TDD

Wrote failing test, confirmed red, implemented minimal code, verified green.

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
```

### Evidence-Based Testing

**Pattern:** `/tmp/worldarchitect.ai/<branch>/<test>/iteration_XXX/`

```
/tmp/worldarchitect.ai/fix/feature-x/my_test/iteration_001/
├── README.md (test description)
├── evidence.md (results)
├── test_output.log (raw output)
├── screenshots/ (if browser test)
└── network_traces/ (if API test)

# Symlink to latest
/tmp/worldarchitect.ai/fix/feature-x/my_test/latest -> iteration_001
```

**Rules:**
1. ALWAYS use full absolute paths (never abbreviate)
2. Create new iteration for each run
3. Review evidence before claiming success
4. Include in PR as proof

---

## 🔍 `/generatetest` - Test Generation

### Evidence
- **82 file commits** (most-modified command!)
- Active development

### Workflow

**1. Analyze Code**
```
- Read implementation
- Identify edge cases
- Find happy paths
- Spot error conditions
```

**2. Generate Tests**
```
- Unit tests for functions
- Integration tests for flows
- E2E tests for user journeys
- Property tests for invariants
```

**3. Evidence Bundle**
```
- Generate in /tmp/ structure
- Include test file
- Include sample runs
- Document coverage
```

### Usage
```bash
/generatetest path/to/code.py
```

---

## 🌐 Browser Testing

### Tools
- **Playwright** (69 commits)
- **Chrome DevTools Protocol** (407 MCP hits)
- **MCP servers:** chrome-superpower, claude-in-chrome, plugin_superpowers-chrome_chrome

### Pattern

**NOT using `/browser` command** (last commit Nov 2025)

**Instead: Direct MCP calls**
```bash
# Navigate
mcp-cli call chrome-superpower/navigate '{"url": "http://localhost:3000"}'

# Click
mcp-cli call claude-in-chrome/click '{"selector": "#login-button"}'

# Execute JS
mcp-cli call chrome-superpower/eval '{"code": "document.title"}'

# Screenshot
mcp-cli call claude-in-chrome/screenshot '{"path": "/tmp/screenshot.png"}'
```

### Why Direct MCP > Command
- Faster (no command overhead)
- More control (access all MCP features)
- Better for automation (scriptable)

---

## 🧠 Multi-Model Validation (`/secondo`)

### Evidence
- **106 commit mentions**
- **49 file commits**

### Workflow

**1. Primary Implementation**
```
Use primary AI (Claude Code) for implementation
```

**2. Second Opinion**
```bash
/secondo "Review this implementation for correctness"

# Queries multiple models:
- Gemini (via MCP)
- Grok (via MCP)
- Perplexity (via MCP)
```

**3. Comparison**
```
- Identify disagreements
- Investigate discrepancies
- Decide on consensus or best approach
```

**4. Refinement**
```
- Update implementation
- Document decision rationale
- Re-verify with models if needed
```

### Use Cases
- Security-critical code
- Complex algorithms
- Architectural decisions
- Unfamiliar domains

---

## 📦 PR Automation (`automation/`)

### Evidence
- **Directory:** `automation/` in main repo
- **2,323 file touches** in `automation/jleechanorg_pr_automation/`

### Key Components

**1. orchestrated_pr_runner.py**
- Batch PR processing
- Parallel execution
- Rate limiting
- Error handling

**2. simple_pr_batch.sh**
- Shell wrapper for PR batches
- Cron-compatible
- Logging and monitoring

**3. jleechanorg_pr_automation/**
- Python package for PR automation
- GitHub API integration
- Comment parsing
- Status tracking

### Workflow
```
1. Cron job triggers batch run
2. Fetch open PRs
3. For each PR:
   - Fetch comments
   - Categorize issues
   - Delegate to /copilot
   - Monitor progress
4. Aggregate results
5. Send summary notification
```

---

## 🎯 Comment Automation

### Commands
- **`/commentfetch`** (2,440 refs) - Fetch PR comments
- **`/commentreply`** (4,007 refs) - Reply to comments
- **`/commentcheck`** (1,269 refs) - Validate comments addressed

### Workflow

**1. Fetch**
```bash
/commentfetch 123

# Returns:
- All unresolved comments
- Categorized by file
- Priority scored
```

**2. Process**
```
- Group by file
- Identify dependencies
- Plan fix order
```

**3. Reply**
```bash
/commentreply "Fixed in commit abc123"

# Automatically:
- Marks comment as resolved
- Links to commit
- Notifies reviewer
```

**4. Verify**
```bash
/commentcheck

# Confirms:
- All comments addressed
- No new comments
- Ready for review
```

---

## 🚀 Fast Code Generation (`/cerebras`)

### Evidence
- **4,901 combined references** (/cerebras + /cereb)
- **246 commit mentions**

### Workflow

**Standard Mode**
```bash
/cerebras "Implement feature X"

# Structured output
# Design → Implementation → Tests
```

**Light Mode (Faster)**
```bash
/cerebras --light "Quick prototype of Y"

# Raw code generation
# No structure overhead
```

### Use Cases
- Large code scaffolding
- Repetitive patterns
- Documentation generation
- Test fixture creation

### Speed
- **1000+ tokens/second** (fastest inference available)
- Good for bulk generation
- Trade-off: less reasoning than Claude

---

## 🔄 Branch Management (`/sync`)

### Evidence
- **26 file commits**

### Workflow

**1. Fetch Latest Main**
```bash
git fetch origin main
```

**2. Identify Conflicts**
```
Compare current branch with main
Detect potential merge issues
```

**3. Safe Merge**
```
Option 1: Rebase (clean history)
Option 2: Merge (preserve history)
User choice based on context
```

**4. Conflict Resolution**
```
- Show conflicts
- Suggest resolutions
- Verify tests pass
```

### Usage
```bash
/sync

# Automatically:
1. Fetches main
2. Analyzes diff
3. Proposes merge strategy
4. Handles conflicts
5. Runs tests
6. Pushes if clean
```

---

## 📊 Testing Metrics

### Coverage
- **3,308 testing commits** (17.4% of all work)
- **7,670 file touches** in `mvp_site/tests/`

### Test Types
1. **Unit tests** - pytest
2. **Integration tests** - Multi-component
3. **E2E tests** - Full user flows
4. **LLM tests** - Via `/testllm` (2,172 refs)
5. **Browser tests** - Playwright (69 commits)

### Evidence Standard
- Full paths always
- Structured bundles
- Mandatory review
- Linked in PRs

---

## 🎛️ Custom Configuration

### Claude Code Settings
- **290 lines** of custom config
- **150+ pre-approved permissions**
- **12+ hooks** (PreToolUse, PostToolUse, UserPromptSubmit)

### Hooks
**PreToolUse:**
- Context validation
- Command optimization
- File creation blocking

**PostToolUse:**
- Fake code detection
- Output trimming
- Evidence validation

**UserPromptSubmit:**
- Command composition
- Slash command expansion

### Skill Files
- **40+ skill files** in `.claude/skills/`
- **Most-modified:** evidence-standards.md (68 commits)
- Procedural knowledge base
- Referenced by commands

---

## 💡 Key Patterns

### 1. Terminal-First
- CLI over GUI
- Scriptable workflows
- Composable tools

### 2. Evidence-Based
- Full paths always
- Structured artifacts
- Mandatory review

### 3. Multi-Agent
- Parallel execution
- Specialized agents
- Coordinated merges

### 4. Quality-First
- 17.4% of commits are tests
- Pre/post-commit hooks
- Automated validation

### 5. Cost-Conscious
- Local classification (<50ms)
- Strategic AI use
- Batch operations

---

**Last Updated:** 2026-02-12
**Based On:** 19,044 commits (Aug 2025 - Feb 2026)
