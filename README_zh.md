# Claude Code CLI Skill

[English](./README.md) | [中文](./README_zh.md)

---

适用于任何 AI Agent 环境的通用 Claude Code CLI 调用技能。

## 概述

本技能提供 Claude Code 命令行工具的完整使用指南，帮助 AI 智能体有效地使用 Claude Code 完成编程任务。参考了 [Claude Code 官方文档](https://code.claude.com/docs/zh-CN/overview) 和 Claude Code 橙皮书。

## 功能特点

- **CLAUDE.md 指南**：完整的层级结构、内容指南、自动记忆及实用示例
- **基础命令**：打印模式、认证、常用 CLI 标志
- **高级功能**：结构化输出、JSON Schema、流式传输、自动批准工具、自定义系统提示
- **Plan 模式**：复杂任务的先规划后执行工作流
- **Git Worktrees**：隔离环境下的并行任务执行
- **最佳实践**：编写后测试、上下文管理

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
├── SKILL.md      # 英文版
├── SKILL_zh.md  # 中文版
├── README.md    # 英文说明
└── README_zh.md # 中文说明
```

## 文档版本

- English: [SKILL.md](SKILL.md)
- 中文: [SKILL_zh.md](SKILL_zh.md)

## 许可证

MIT

## 贡献

欢迎提交 Issue 或 Pull Request！

## 参考资料

- [Claude Code 官方文档](https://code.claude.com/docs/zh-CN/overview)
- [Claude Code CLI 参考](https://code.claude.com/docs/zh-CN/headless)
- [Claude Code 橙皮书](https://my.feishu.cn/wiki/JK1WwrRgJiYfRok7YxxceS5qn1J)