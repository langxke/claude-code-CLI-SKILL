# Claude Code CLI Skill

[English](./README.md) | [中文](./README_zh.md)

---

A universal skill for invoking Claude Code CLI in any AI agent environment.

## Overview

This skill provides a comprehensive guide for using Claude Code command-line tool, helping AI agents effectively use Claude Code for programming tasks. It references the [Claude Code Official Documentation](https://code.claude.com/docs/en/overview) and the Claude Code Orange Book.

## Features

- **CLAUDE.md Guide**: Complete guide with hierarchy structure, content guidelines, Auto Memory, and practical examples
- **Basic Commands**: Print mode, authentication, common CLI flags
- **Advanced Features**: Structured output, JSON Schema, streaming, auto-approve tools, custom system prompts
- **Plan Mode**: Plan-then-execute workflow for complex tasks
- **Git Worktrees**: Parallel task execution with isolated environments
- **Best Practices**: Testing after implementation, context management

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
├── SKILL_zh.md   # Chinese version
├── README.md     # English README
└── README_zh.md # Chinese README
```

## Documentation Languages

- English: [SKILL.md](SKILL.md)
- 中文: [SKILL_zh.md](SKILL_zh.md)

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## Reference

- [Claude Code Official Documentation](https://code.claude.com/docs/en/overview)
- [Claude Code CLI Reference](https://code.claude.com/docs/en/headless)
- [Claude Code Orange Book](https://my.feishu.cn/wiki/JK1WwrRgJiYfRok7YxxceS5qn1J)