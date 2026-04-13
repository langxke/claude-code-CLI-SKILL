# Claude Code CLI Skill

A universal skill for invoking Claude Code CLI in any AI agent environment.

## Overview

This skill provides a comprehensive guide for using the Claude Code command-line tool. It covers basic commands, common development workflows, and best practices that help AI agents effectively use Claude Code for various programming tasks.

## Features

- **Basic Commands**: Print mode, authentication
- **CLI Flags**: Common flags, permission flags, output flags, MCP flags
- **Common Workflows**: Code review, refactoring, debugging, test generation, Git operations, documentation
- **Best Practices**: Small and incremental tasks, context management, CLAUDE.md configuration

## Prerequisites

- Claude Code CLI installed: `npm install -g @anthropic-ai/claude-code`
- Anthropic account logged in: `claude auth login`

## Quick Start

```bash
# Print mode (required for agents/scripts)
claude -p "Your query here"
```

## Usage

### For AI Agents

Copy the `SKILL.md` file to your agent's skill directory. The agent will automatically load and use it when invoking Claude Code CLI commands.

### File Structure

```
claude-code-CLI-SKILL/
├── SKILL.md       # English version
├── SKILL_zh.md    # Chinese version
├── README.md      # This file
└── README_zh.md   # Chinese README
```

## Common Workflows

| Workflow | Command | Use Case |
|----------|---------|----------|
| Code Review | `claude -p "Review this code"` | Pre-merge checks |
| Refactoring | `claude -p "Refactor this function"` | Improve code structure |
| Debugging | `claude -p "Debug this error"` | Fix bugs |
| Test Generation | `claude -p "Write tests for this"` | Improve coverage |
| Git Operations | `claude -p "Write commit message"` | Standardize commits |

## Documentation Languages

- English: [SKILL.md](SKILL.md)
- 中文: [SKILL_zh.md](SKILL_zh.md)

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## Reference

- [Claude Code Official Documentation](https://code.claude.com/docs/en/overview)
