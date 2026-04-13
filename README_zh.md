# Claude Code CLI Skill

适用于任何 AI Agent 环境的通用 Claude Code CLI 调用技能。

## 概述

本技能提供 Claude Code 命令行工具的完整使用指南，涵盖基础命令、常用开发工作流和最佳实践，帮助 AI 智能体有效地使用 Claude Code 完成各种编程任务。

## 功能特点

- **基础命令**：打印模式、认证
- **CLI 标志**：常用标志、权限标志、输出标志、MCP 标志
- **常用工作流**：代码审查、重构、调试、测试生成、Git 操作、文档生成
- **最佳实践**：小步快跑、上下文管理、CLAUDE.md 配置

## 前置要求

- 安装 Claude Code CLI：`npm install -g @anthropic-ai/claude-code`
- 登录 Anthropic 账户：`claude auth login`

## 快速开始

```bash
# 打印模式（智能体/脚本必需）
claude -p "你的查询"
```

## 使用方法

### 集成到 AI Agent

将 `SKILL.md` 或 `SKILL_zh.md` 文件复制到你的 AI Agent 技能目录中。智能体会自动加载并在调用 Claude Code CLI 命令时使用它。

### 文件结构

```
claude-code-CLI-SKILL/
├── SKILL.md       # 英文版
├── SKILL_zh.md    # 中文版
├── README.md      # 英文说明
└── README_zh.md   # 中文说明
```

## 常用工作流

| 工作流 | 命令示例 | 使用场景 |
|--------|----------|----------|
| 代码审查 | `claude -p "Review this code"` | 合并前检查 |
| 代码重构 | `claude -p "Refactor this function"` | 改善代码结构 |
| 调试排查 | `claude -p "Debug this error"` | 修复 bug |
| 测试生成 | `claude -p "Write tests for this"` | 提高覆盖率 |
| Git 操作 | `claude -p "Write commit message"` | 规范化提交 |

## 文档版本

- English: [SKILL.md](SKILL.md)
- 中文: [SKILL_zh.md](SKILL_zh.md)

## 许可证

MIT

## 贡献

欢迎提交 Issue 或 Pull Request！

## 参考资料

- [Claude Code 官方文档](https://code.claude.com/docs/zh-CN/overview)
