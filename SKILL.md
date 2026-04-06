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
- [Environment Adaptation](#environment-adaptation)

---

## Quick Start

Claude Code is Anthropic's official command-line AI coding assistant, supporting code editing, debugging, refactoring, and more.

### Prerequisites

- Install Claude Code CLI: `npm install -g @anthropic-ai/claude-code`
- Login: `claude auth login`

### Basic Invocation

```bash
# Interactive session
claude

# With initial prompt
claude "Explain this code for me"

# Print mode (non-interactive, suitable for scripts)
claude -p "Explain this code"
```

---

## Basic Commands

### Interactive Session

```bash
# Start interactive session
claude

# With initial prompt
claude "Review the changes in this PR"

# Continue last conversation
claude -c
```

### Print Mode

Print mode is suitable for script invocation, returning plain text results without entering interactive mode.

```bash
# Simple query
claude -p "What does this function do?"

# Complex query
claude -p "Review this code for security issues"
```

### Session Management

```bash
# Continue last session
claude -c

# Resume specific session
claude -r <session-id> "Continue with this task"

# List sessions
claude session list
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
| `-c, --continue` | Continue last conversation | `claude -c` |
| `-r, --resume <id>` | Resume specific session | `claude -r abc123 "query"` |
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

### 2. Provide Sufficient Context

Include relevant code, error messages, or file paths.

```
# ✅ Good approach
claude -p "Review src/utils/validator.js - it should validate email format"

# ❌ Lack of context
claude -p "Check this file"
```

### 3. Use CLAUDE.md to Configure Project

Create a CLAUDE.md file in the project root to define project conventions:

```markdown
# Project Guidelines

## Code Style
- Use TypeScript
- Use ESLint + Prettier

## Commands
- Development: npm run dev
- Testing: npm test
- Build: npm run build

## Notes
- Avoid modifying the core/ directory
```

### 4. Leverage Session Management

- Use `-c` to continue unfinished tasks
- Use `-r` to resume specific sessions
- Use `claude session list` to view all sessions

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

## Environment Adaptation

### Invoking in Different Environments

Claude Code can be invoked via shell commands. Here are examples for different environments:

#### Bash / Zsh / Unix Shell

```bash
claude -p "Your query"
```

#### Windows CMD

```cmd
claude -p "Your query"
```

#### Windows PowerShell

```powershell
claude -p "Your query"
```

#### Python Script

```python
import subprocess
result = subprocess.run(
    ["claude", "-p", "Your query"],
    capture_output=True,
    text=True
)
print(result.stdout)
```

#### Node.js

```javascript
const { execSync } = require('child_process');
const result = execSync('claude -p "Your query"', { encoding: 'utf-8' });
console.log(result);
```

### Notes

1. **Prefer Print Mode**: Use `-p` flag to avoid interactive sessions
2. **Timeout Settings**: Set longer timeout for complex tasks
3. **Output Format**: Use `--output-format json` for structured output
4. **Error Handling**: Check return code and stderr

### Recommended Invocation Patterns

```bash
# Simple query
claude -p "Explain this function"

# Complex task
claude -p "Refactor this module with TypeScript"

# Task with output
claude -p "Generate comprehensive tests for this API"
```

### Error Handling

If command fails, check:
1. Claude Code installed: `claude --version`
2. Logged in: `claude auth status`
3. Model quota available

---

## Reference Links

- [Claude Code Official Documentation](https://code.claude.com/docs/en/overview)