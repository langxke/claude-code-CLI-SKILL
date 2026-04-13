---
name: claude-code-CLI-SKILL
description: Claude Code CLI tool invocation guide - covering basic commands, common workflows, and best practices
metadata:
  {
    "version": "1.0",
    "requires": { "bins": ["claude"] }
  }
---

# Claude Code CLI Skill

This skill provides a guide for using the Claude Code command-line tool, helping agents understand how to use Claude Code for various development tasks.

## Table of Contents

- [Quick Start](#quick-start)
- [Basic Commands](#basic-commands)
- [CLI Flags](#cli-flags)
- [Common Workflows](#common-workflows)
- [Best Practices](#best-practices)
  - [3.1 Why CLAUDE.md Matters](#31-why-claudemd-matters)
  - [3.2 Hierarchy Structure](#32-hierarchy-structure)
  - [3.3 Content Guidelines](#33-content-guidelines)
  - [3.4 Auto Memory vs Manual CLAUDE.md](#34-auto-memory-vs-manual-claudemd)
  - [3.5 Iterative Flywheel](#35-iterative-flywheel)
  - [3.6 Example CLAUDE.md](#36-example-claudemd)
- [Advanced Features](#advanced-features)
  - [4.1 Structured Output](#41-structured-output)
  - [4.2 JSON Schema](#42-json-schema)
  - [4.3 Streaming](#43-streaming)
  - [4.4 Auto-Approve Tools](#44-auto-approve-tools)
  - [4.5 Custom System Prompts](#45-custom-system-prompts)
  - [4.6 Conversation Management](#46-conversation-management)
  - [4.7 Plan Mode Workflow](#47-plan-mode-workflow)
  - [4.8 Git Worktrees](#48-git-worktrees)

---

## Quick Start

Claude Code is Anthropic's official command-line AI coding assistant, supporting code editing, debugging, refactoring, and more.

### Prerequisites

- Install Claude Code CLI: `npm install -g @anthropic-ai/claude-code`
- Login: `claude auth login`

### Basic Invocation

```bash
# With query (print mode, suitable for scripts/agents)
claude -p "Explain this code"
```

---

## Basic Commands

### Print Mode

Print mode is designed for script/agent invocation, returning plain text results without interactive prompts.

```bash
# Simple query
claude -p "What does this function do?"

# Complex query
claude -p "Review this code for security issues"
```

### Authentication

```bash
# Login to Anthropic account
claude auth login

# Check login status
claude auth status
```

---

## CLI Flags

### Common Flags

| Flag | Description | Example |
|------|-------------|---------|
| `-p, --print` | Print mode, exit after returning result | `claude -p "query"` |
| `--model <model>` | Specify model | `claude --model opus "query"` |

### Permission Flags

| Flag | Description | Example |
|------|-------------|---------|
| `--permission-mode <mode>` | Set permission mode | `claude --permission-mode plan "query"` |
| `--dangerously-skip-permissions` | Skip all permission prompts (use with caution) | `claude --dangerously-skip-permissions "query"` |

### Output Flags

| Flag | Description | Example |
|------|-------------|---------|
| `--output-format <format>` | Output format | `claude --output-format json "query"` |
| `--debug` | Enable debug output | `claude --debug "query"` |

### MCP Flags

| Flag | Description | Example |
|------|-------------|---------|
| `--mcp-config <path>` | Specify MCP config file | `claude --mcp-config ./mcp.json` |

---

## Common Workflows

### 1. Code Review

```bash
# Review code changes
claude -p "Review the changes in the src directory"

# Review PR
claude -p "Review this PR: explain what changed and suggest improvements"

# Security review
claude -p "Check this code for security vulnerabilities"
```

**Use cases**: Pre-merge checks, discovering potential issues, learning codebase

### 2. Code Refactoring

```bash
# Rename and extract
claude -p "Rename the 'processData' function to 'handleUserData' and extract validation logic"

# Improve code structure
claude -p "Refactor this class to follow single responsibility principle"

# Type conversion
claude -p "Convert this JavaScript to TypeScript"
```

**Use cases**: Improve readability, extract duplicated code, migrate tech stack

### 3. Debugging and Troubleshooting

```bash
# Analyze error messages
claude -p "Explain this error and suggest fixes: [paste error]"

# Debug code
claude -p "Debug why this function returns undefined"

# Performance analysis
claude -p "Analyze this code for performance issues"
```

**Use cases**: Locate bugs, understand errors, fix crashes

### 4. Test Generation

```bash
# Generate unit tests
claude -p "Write unit tests for this function using Jest"

# Generate integration tests
claude -p "Create integration tests for this API endpoint"

# Test review
claude -p "Review existing tests and suggest improvements"
```

**Use cases**: Improve test coverage, verify edge cases

### 5. Git Operations

```bash
# Generate commit message
claude -p "Write a concise commit message for these changes"

# Analyze commit
claude -p "What does this commit do? git show <hash>"

# Resolve conflicts
claude -p "Help me resolve this merge conflict"
```

**Use cases**: Write standard commit messages, understand history

### 6. Code Explanation

```bash
# Explain function
claude -p "Explain what this function does in simple terms"

# Explain algorithm
claude -p "Explain the algorithm used in this code"

# Explain architecture
claude -p "Describe the architecture of this codebase"
```

**Use cases**: Learn new codebase, understand complex logic

### 7. Documentation Generation

```bash
# Generate README
claude -p "Generate README.md for this project"

# Generate API documentation
claude -p "Generate JSDoc comments for this module"

# Update documentation
claude -p "Update the documentation to reflect these changes"
```

**Use cases**: Project initialization, keep documentation in sync

---

## Best Practices

### 1. Small and Incremental

Let Claude Code complete one clear task at a time.

```
# ✅ Good approach
claude -p "Extract the validation logic into a separate function"

# ❌ Avoid this
claude -p "Rewrite this entire application with better architecture"
```

### 2. Always Test After Implementation

After writing any feature, always test it to ensure correctness before delivery.

```bash
# After implementation, run tests to verify
claude -p "Run tests to verify the implementation works correctly"

# If tests fail, fix before proceeding
claude -p "Fix the failing tests"
```

**Why this matters**:
- Ensures the code actually works before delivery
- Catches issues early when they're easy to fix
- Prevents broken code from reaching production

### 3. Provide Sufficient Context

Include relevant code, error messages, or file paths.

```
# ✅ Good approach
claude -p "Review src/utils/validator.js - it should validate email format"

# ❌ Lack of context
claude -p "Check this file"
```

### 3. Using CLAUDE.md Effectively

Claude Code automatically reads CLAUDE.md at the start of every session. This file is not a manual—it's a contract defining how you and AI work together.

#### 3.1 Why CLAUDE.md Matters

CLAUDE.md is the most important file in your project. When Claude starts a new session, it reads this file first to understand:
- Project structure and architecture
- Code style preferences
- Custom commands and scripts
- Common pitfalls to avoid

Without it, Claude is like a new teammate dropped into an unfamiliar codebase. With it, Claude knows the rules immediately.

Shrivu Shankar (AI Strategy VP at Abnormal Security) puts it simply:
> "The CLAUDE.md file is the 'constitution' for the agent—it determines the primary source of truth for how your specific codebase works."

#### 3.2 Hierarchy Structure

CLAUDE.md is not just one file—it's a hierarchy that Claude reads automatically:

| Level | Location | Purpose |
|-------|----------|---------|
| Global | `~/.claude/CLAUDE.md` | Personal preferences across all projects |
| Project | `./CLAUDE.md` | Project-specific rules, committed to git |
| Subdirectory | `./src/CLAUDE.md` | Module-specific rules for monorepos |

**Global level** (`~/.claude/CLAUDE.md`): Personal preferences like preferred languages, test frameworks, commit message format.

**Project level** (`./CLAUDE.md`): Project conventions, code style, architecture decisions, common pitfalls. Commit to git for team sharing.

**Subdirectory level** (`./src/CLAUDE.md`): Specific rules for monorepo modules (e.g., frontend vs backend rules).

#### 3.3 Content Guidelines

The key principle: **Write what Claude can't infer from code; don't write what Claude can read itself.**

| Write | Don't Write |
|-------|-----------|
| Custom commands (e.g., `pnpm db:generate`) | "This is a React project" (readable from package.json) |
| Code style preferences (e.g., "use Tailwind, not CSS files") | Standard syntax (Claude already knows) |
| Test framework preferences | Detailed API docs (Claude can search) |
| Architecture decisions and why | Frequently changing info |
| Common pitfalls and fixes | Vague rules like "write clean code" |

**Additional tips:**
- Don't @ reference large files—use paths instead (e.g., "see docs/troubleshooting.md")
- Always provide alternatives: don't just say "don't do X", say "use Y instead"
- Keep it under ~2500 tokens (Boris's team uses about this much)

#### 3.4 Auto Memory vs Manual CLAUDE.md

Claude has an automatic memory system that captures corrections during conversation:

| Aspect | Manual CLAUDE.md | Auto Memory |
|--------|----------------|-----------|
| Maintenance | You write manually | Claude auto-captures |
| Scope | Team-shared rules | Personal preferences |
| Storage | In git | Local (`~/.claude/projects/<id>/memory/`) |
| Organization | Structured | Incremental |

When you correct Claude (e.g., "always write commit messages in English"), it automatically saves this to memory. No need to manually update CLAUDE.md for personal preferences.

#### 3.5 Iterative Flywheel

The best CLAUDE.md starts empty and grows over time:

1. **Week 1**: Write only architecture and basic commands
2. **Week 2**: Add rules as Claude makes mistakes
3. **Month 1**: 20-30 rules from real mistakes—quality improves
4. **Ongoing**: Remove outdated rules, keep file lean

This is the "guardrails not manuals" approach: each rule comes from a real mistake.

#### 3.6 Example CLAUDE.md

```markdown
# My App

## Architecture
- Next.js 15 + TypeScript + Tailwind CSS
- Database: PostgreSQL + Drizzle ORM
- Auth: Better Auth
- State: Zustand (not Redux)

## Commands
- Dev: pnpm dev
- Test: pnpm test (Jest + React Testing Library)
- Typecheck: pnpm typecheck
- Lint: pnpm lint

## Code Style
- Use functional components, not class
- Use Tailwind for styling, no CSS files
- Use server components for data, not useEffect
- Use error.tsx boundaries, not try-catch

## Common Pitfalls
- After Drizzle migration: run `pnpm db:generate`
- Restart dev server after env changes
- Auth checks in middleware, not in page components

## Don't:
- Install dependencies without my approval
- Modify drizzle.config.ts
- Call database directly in client components
```

Every line comes from either a custom command or a real mistake. This is what an effective CLAUDE.md looks like.

### 4. Leverage Repeated Invocation

- Use `-p` flag for each invocation (stateless)
- Process complex tasks in batches with multiple calls
- Use file paths instead of pasting entire code

### 5. Manage Context Window

- Avoid inputting too much code at once
- Process large refactoring tasks in batches
- Use file paths instead of pasting entire code

### 6. Permission Mode Selection

| Mode | Description | Use Case |
|------|-------------|----------|
| `plan` | Read-only, no commands executed | Review, explanation |
| `bypassPermissions` | Auto-execute all operations | Automation scripts |
| `default` | Confirm before execution | Daily development |

---

## Advanced Features

### 4.1 Structured Output

Use `--output-format` to control the response format:

| Format | Description |
|--------|-------------|
| `text` (default) | Plain text output |
| `json` | Structured JSON with result, session_id, and metadata |
| `stream-json` | Streaming JSON (newline-separated) |

```bash
# Get JSON output
claude -p "Summarize this project" --output-format json

# Parse with jq
claude -p "Summarize this project" --output-format json | jq -r '.result'
```

### 4.2 JSON Schema

Use `--json-schema` to get responses in a specific schema format:

```bash
claude -p "Extract the main function names from auth.py" \
  --output-format json \
  --json-schema '{"type":"object","properties":{"functions":{"type":"array","items":{"type":"string"}}},"required":["functions"]}'
```

Parse the structured output:

```bash
claude -p "Extract function names" --output-format json --json-schema '...' | jq '.structured_output'
```

### 4.3 Streaming

Use `--output-format stream-json` with `--verbose` and `--include-partial-messages` to receive real-time tokens:

```bash
claude -p "Explain recursion" --output-format stream-json --verbose --include-partial-messages
```

Filter streaming text with jq:

```bash
claude -p "Write a poem" --output-format stream-json --verbose --include-partial-messages | \
  jq -rj 'select(.type == "stream_event" and .event.delta.type? == "text_delta") | .event.delta.text'
```

### 4.4 Auto-Approve Tools

Use `--allowedTools` to let Claude use certain tools without prompting:

```bash
# Run tests and fix failures without prompts
claude -p "Run the test suite and fix any failures" \
  --allowedTools "Bash,Read,Edit"

# Create a commit
claude -p "Create a commit" \
  --allowedTools "Bash(git diff *),Bash(git log *),Bash(git status *),Bash(git commit *)"
```

The `*` enables prefix matching: `Bash(git diff *)` allows any command starting with `git diff`. Space before `*` matters.

### 4.5 Custom System Prompts

Use `--append-system-prompt` to add instructions while preserving default behavior:

```bash
gh pr diff "$1" | claude -p \
  --append-system-prompt "You are a security engineer. Review for vulnerabilities." \
  --output-format json
```

Use `--system-prompt` to completely replace the default prompt.

### 4.6 Conversation Management

Use `--resume` with a session ID to continue a specific conversation. This is useful when running multiple Claude instances in parallel:

```bash
# Capture session ID from first call
session_id=$(claude -p "Start a review" --output-format json | jq -r '.session_id')

# Resume that specific conversation
claude -p "Continue that review" --resume "$session_id"
```

### 4.7 Plan Mode Workflow

For complex tasks, use a "plan then execute" workflow to ensure clean context:

1. **Generate plan**: Use `--permission-mode plan` to get plan without execution

```bash
claude -p "Implement user authentication feature" --permission-mode plan --output-format json
```

2. **Review plan**: Check the returned plan and confirm

3. **Execute**: Call with a NEW session (not resume) to execute

```bash
# Execute in a fresh session - do NOT use --resume
claude -p "Execute: [paste the confirmed plan here]"
```

**Important**: Always use a new session for execution, not `--resume`. This ensures:
- Clean context for execution
- No carryover from planning discussion
- Fresh state to start

**When to use Plan mode**:

| Use Plan Mode | Skip Plan |
|--------------|---------|
| Multiple files need changes | One-line fix |
| Unfamiliar code area | Simple typo fix |
| Refactoring / architecture | Add console.log |
| Need to discuss approach | Run tests |

### 4.8 Git Worktrees

Git worktree allows you to have multiple working directories from the same repository, each on a different branch with isolated filesystem. Claude Code has native support:

```bash
# Start a Claude session running in an isolated worktree
claude --worktree

# Start in a Tmux session (can run in background)
claude --worktree --tmux
```

Each `claude --worktree` creates a new worktree, switches to a new branch, and works in that isolated environment. This is ideal for parallel tasks:

- **Parallel work**: Run multiple Claude instances simultaneously, each in its own worktree
- **No interference**: Changes in one worktree don't affect others
- **Easy merge**: Merge branches back when done

**Boris's workflow**: He runs 5 Claude Code instances in parallel, each in different worktrees, plus 5-10 sessions on claude.ai/code—handling dozens of tasks simultaneously.

---

## Reference Links

- [Claude Code Official Documentation](https://code.claude.com/docs/en/overview)