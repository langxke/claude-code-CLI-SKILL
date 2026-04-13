---
name: claude-code-CLI-SKILL
description: Claude Code CLI 工具调用指南 - 包含基础命令、常用工作流和最佳实践
metadata:
  {
    "version": "1.0",
    "requires": { "bins": ["claude"] }
  }
---

# Claude Code CLI Skill

本 Skill 提供 Claude Code 命令行工具的调用指南，帮助智能体理解如何使用 Claude Code 完成各种开发任务。

## 目录

- [快速开始](#快速开始)
- [基础命令](#基础命令)
- [CLI 标志](#cli-标志)
- [常用工作流](#常用工作流)
- [最佳实践](#最佳实践)
  - [3.1 为什么 CLAUDE.md 最重要](#31-为什么-claudemd-最重要)
  - [3.2 层级结构](#32-层级结构)
  - [3.3 内容指南](#33-内容指南)
  - [3.4 手动 CLAUDE.md vs 自动记忆](#34-手动-claudemd-vs-自动记忆)
  - [3.5 迭代飞轮](#35-迭代飞轮)
  - [3.6 CLAUDE.md 示例](#36-claudemd-示例)
- [高级功能](#高级功能)
  - [4.1 结构化输出](#41-结构化输出)
  - [4.2 JSON Schema](#42-json-schema)
  - [4.3 流式传输](#43-流式传输)
  - [4.4 自动批准工具](#44-自动批准工具)
  - [4.5 自定义系统提示](#45-自定义系统提示)
  - [4.6 对话管理](#46-对话管理)
  - [4.7 Plan 模式工作流](#47-plan-模式工作流)
  - [4.8 Git Worktrees](#48-git-worktrees)

---

## 快速开始

Claude Code 是 Anthropic 官方推出的命令行 AI 编程助手，支持代码编辑、调试、重构等多种功能。

### 前置要求

- 安装 Claude Code CLI：`npm install -g @anthropic-ai/claude-code`
- 完成登录：`claude auth login`

### 基础调用方式

```bash
# 带查询调用（打印模式，适合脚本/智能体）
claude -p "Explain this code"
```

---

## 基础命令

### 打印模式（Print Mode）

打印模式专为脚本/智能体调用设计，返回纯文本结果，无需交互。

```bash
# 简单查询
claude -p "What does this function do?"

# 复杂查询
claude -p "Review this code for security issues"
```

### 认证

```bash
# 登录 Anthropic 账户
claude auth login

# 检查登录状态
claude auth status
```

---

## CLI 标志

### 常用标志

| 标志 | 说明 | 示例 |
|------|------|------|
| `-p, --print` | 打印模式，返回结果后退出 | `claude -p "query"` |
| `--model <model>` | 指定模型 | `claude --model opus "query"` |

### 权限相关标志

| 标志 | 说明 | 示例 |
|------|------|------|
| `--permission-mode <mode>` | 设置权限模式 | `claude --permission-mode plan "query"` |
| `--dangerously-skip-permissions` | 跳过所有权限确认（谨慎使用） | `claude --dangerously-skip-permissions "query"` |

### 输出相关标志

| 标志 | 说明 | 示例 |
|------|------|------|
| `--output-format <format>` | 输出格式 | `claude --output-format json "query"` |
| `--debug` | 启用调试输出 | `claude --debug "query"` |

### MCP 相关标志

| 标志 | 说明 | 示例 |
|------|------|------|
| `--mcp-config <path>` | 指定 MCP 配置文件 | `claude --mcp-config ./mcp.json` |

---

## 常用工作流

### 1. 代码审查

```bash
# 审查代码变更
claude -p "Review the changes in the src directory"

# 审查 PR
claude -p "Review this PR: explain what changed and suggest improvements"

# 安全审查
claude -p "Check this code for security vulnerabilities"
```

**适用场景**：代码合并前检查、发现潜在问题、学习代码库

### 2. 代码重构

```bash
# 重命名和提取
claude -p "Rename the 'processData' function to 'handleUserData' and extract validation logic"

# 改进代码结构
claude -p "Refactor this class to follow single responsibility principle"

# 类型转换
claude -p "Convert this JavaScript to TypeScript"
```

**适用场景**：改善代码可读性、提取重复代码、迁移技术栈

### 3. 调试和问题排查

```bash
# 分析错误信息
claude -p "Explain this error and suggest fixes: [paste error]"

# 调试代码
claude -p "Debug why this function returns undefined"

# 性能分析
claude -p "Analyze this code for performance issues"
```

**适用场景**：定位 bug、理解错误、修复崩溃

### 4. 测试生成

```bash
# 生成单元测试
claude -p "Write unit tests for this function using Jest"

# 生成集成测试
claude -p "Create integration tests for this API endpoint"

# 测试审查
claude -p "Review existing tests and suggest improvements"
```

**适用场景**：补充测试覆盖、验证边界条件

### 5. Git 操作

```bash
# 生成提交信息
claude -p "Write a concise commit message for these changes"

# 分析提交
claude -p "What does this commit do? git show <hash>"

# 解决冲突
claude -p "Help me resolve this merge conflict"
```

**适用场景**：写规范的提交信息、理解历史变更

### 6. 代码解释

```bash
# 解释函数
claude -p "Explain what this function does in simple terms"

# 解释算法
claude -p "Explain the algorithm used in this code"

# 解释架构
claude -p "Describe the architecture of this codebase"
```

**适用场景**：学习新代码库、理解复杂逻辑

### 7. 文档生成

```bash
# 生成 README
claude -p "Generate README.md for this project"

# 生成 API 文档
claude -p "Generate JSDoc comments for this module"

# 更新文档
claude -p "Update the documentation to reflect these changes"
```

**适用场景**：项目初始化、保持文档同步

---

## 最佳实践

### 1. 小步快跑

每次只让 Claude Code 完成一个明确的任务。

```
# ✅ 好的做法
claude -p "Extract the validation logic into a separate function"

# ❌ 避免的做法
claude -p "Rewrite this entire application with better architecture"
```

### 2. 编写后务必测试

编写任何功能后，始终测试以确保正确性后再交付。

```bash
# 编写后运行测试验证
claude -p "Run tests to verify the implementation works correctly"

# 如果测试失败，先修复再继续
claude -p "Fix the failing tests"
```

**重要性**：
- 确保代码在实际交付前能正确运行
- 尽早发现问题，修复成本最低
- 防止有问题的代码进入生产环境

### 3. 提供足够的上下文

包含相关代码、错误信息或文件路径。

```
# ✅ 好的做法
claude -p "Review src/utils/validator.js - it should validate email format"

# ❌ 缺乏上下文
claude -p "Check this file"
```

### 3. 有效使用 CLAUDE.md

Claude Code 在每次会话开始时自动读取 CLAUDE.md。这个文件不是说明书——它更像一份契约，定义你与 AI 之间如何工作的约定。

#### 3.1 为什么 CLAUDE.md 最重要

CLAUDE.md 是项目中最重要的文件。当 Claude 新建会话时，它首先读取这个文件来了解：
- 项目结构和架构
- 代码风格偏好
- 自定义命令和脚本
- 需要避免的常见陷阱

没有它，Claude 就像空降到陌生代码库的新同事。有了它，Claude 立刻知道规矩。

Shrivu Shankar（Abnormal Security 的 AI 战略副总裁）说得直白：
> "CLAUDE.md 文件是 agent 的「宪法」——它决定了你的特定代码库如何工作的主要真理来源。"

#### 3.2 层级结构

CLAUDE.md 不只是一个文件——它是一套层级系统，Claude 会自动按顺序读取：

| 层级 | 位置 | 用途 |
|------|------|------|
| 全局级 | `~/.claude/CLAUDE.md` | 所有项目共用的个人偏好 |
| 项目级 | `./CLAUDE.md` | 项目特有规则，纳入 git 管理 |
| 子目录级 | `./src/CLAUDE.md` | monorepo 中特定模块的规则 |

**全局级** (`~/.claude/CLAUDE.md`)：个人偏好，如喜欢的语言、测试框架、提交信息格式。

**项目级** (`./CLAUDE.md`)：项目规范、代码风格、架构决策、常见陷阱。纳入 git 与团队共享。

**子目录级** (`./src/CLAUDE.md`)：monorepo 中特定模块的规则（如前端 vs 后端规则）。

#### 3.3 内容指南

核心原则：**写 Claude 猜不到的，不写 Claude 能自己推断的。**

| 应该写 | 不该写 |
|--------|--------|
| 自定义命令（如 `pnpm db:generate`） | "这是 React 项目"（从 package.json 可读） |
| 代码风格偏好（如"用 Tailwind，不用 CSS"） | 标准语法（Claude 已掌握） |
| 测试框架偏好 | 详细 API 文档（Claude 可搜索） |
| 架构决策和原因 | 频繁变化的信息 |
| 常见陷阱和修复方式 | "写整洁代码"这类空话 |

**额外建议：**
- 不要用 @ 引用大文件——用路径代替（如"参阅 docs/troubleshooting.md"）
- 永远提供替代方案：不要说"不要做 X"，要说"用 Y 代替 X"
- 控制在 ~2500 tokens 以内（Boris 团队约用这么多）

#### 3.4 手动 CLAUDE.md vs 自动记忆

Claude 有自动记忆系统，会在对话中自动捕获纠正：

| 方面 | 手动 CLAUDE.md | 自动记忆 |
|------|-------------|---------|
| 维护方式 | 手动编写 | Claude 自动捕获 |
| 范围 | 团队共享规则 | 个人偏好 |
| 存储位置 | 纳入 git | 本地 (`~/.claude/projects/<id>/memory/`) |
| 组织方式 | 结构化 | 增量累积 |

当你在对话中纠正 Claude（如"提交信息永远用英文"），它会自动保存到记忆。不需要手动更新 CLAUDE.md 来记录个人偏好。

#### 3.5 迭代飞轮

最好的 CLAUDE.md 从空文件开始，随着时间增长：

1. **第一周**：只写架构和基本命令
2. **第二周**：随着 Claude 犯错添加规则
3. **第一个月**：20-30 条来自真实错误的规则——质量明显提升
4. **持续迭代**：删除过时规则，保持文件精简

这就是"从护栏开始"的方法：每条规则都对应一个真实的错误。

#### 3.6 CLAUDE.md 示例

```markdown
# My App

## 架构
- Next.js 15 + TypeScript + Tailwind CSS
- 数据库：PostgreSQL + Drizzle ORM
- 认证：Better Auth
- 状态管理：Zustand（不用 Redux）

## 命令
- 开发：pnpm dev
- 测试：pnpm test（Jest + React Testing Library）
- 类型检查：pnpm typecheck
- Lint：pnpm lint

## 代码风格
- 用函数式组件，不用 class
- 用 Tailwind 样式，不用 CSS 文件
- 用 server component 读取数据，不用 useEffect
- 用 error.tsx 边界不用 try-catch

## 常见陷阱
- Drizzle 迁移后必跑：pnpm db:generate
- 环境变量改完要重启 dev server
- 认证检查在 middleware 中，不要在页面组件里重复检查

## 不要：
- 未经我同意不要安装依赖
- 不要修改 drizzle.config.ts
- 不要在 client component 中直接调数据库
```

每一行都来自自定义命令或真实错误。这就是有效的 CLAUDE.md 的样子。

### 4. 利用重复调用

- 每次调用使用 `-p` 标志（无状态）
- 将复杂任务分批处理，多次调用
- 使用文件路径而非粘贴完整代码

### 5. 管理上下文窗口

- 避免一次输入过多代码
- 分批处理大型重构任务
- 使用文件路径而非粘贴完整代码

### 6. 权限模式选择

| 模式 | 说明 | 使用场景 |
|------|------|----------|
| `plan` | 只读，不执行任何命令 | 审查、解释 |
| `bypassPermissions` | 自动执行所有操作 | 自动化脚本 |
| `default` | 执行前确认 | 日常开发 |

---

## 高级功能

### 4.1 结构化输出

使用 `--output-format` 控制响应格式：

| 格式 | 说明 |
|------|------|
| `text`（默认） | 纯文本输出 |
| `json` | 结构化 JSON，包含 result、session_id 和元数据 |
| `stream-json` | 流式 JSON（换行符分隔） |

```bash
# 获取 JSON 输出
claude -p "Summarize this project" --output-format json

# 用 jq 解析
claude -p "Summarize this project" --output-format json | jq -r '.result'
```

### 4.2 JSON Schema

使用 `--json-schema` 获取特定格式的响应：

```bash
claude -p "Extract the main function names from auth.py" \
  --output-format json \
  --json-schema '{"type":"object","properties":{"functions":{"type":"array","items":{"type":"string"}}},"required":["functions"]}'
```

解析结构化输出：

```bash
claude -p "Extract function names" --output-format json --json-schema '...' | jq '.structured_output'
```

### 4.3 流式传输

使用 `--output-format stream-json` 配合 `--verbose` 和 `--include-partial-messages` 接收实时令牌：

```bash
claude -p "Explain recursion" --output-format stream-json --verbose --include-partial-messages
```

用 jq 过滤流式文本：

```bash
claude -p "Write a poem" --output-format stream-json --verbose --include-partial-messages | \
  jq -rj 'select(.type == "stream_event" and .event.delta.type? == "text_delta") | .event.delta.text'
```

### 4.4 自动批准工具

使用 `--allowedTools` 让 Claude 使用某些工具无需提示：

```bash
# 运行测试并修复失败，无需提示
claude -p "Run the test suite and fix any failures" \
  --allowedTools "Bash,Read,Edit"

# 创建提交
claude -p "Create a commit" \
  --allowedTools "Bash(git diff *),Bash(git log *),Bash(git status *),Bash(git commit *)"
```

`*` 启用前缀匹配：`Bash(git diff *)` 允许任何以 `git diff` 开头的命令。`*` 前的空格很重要。

### 4.5 自定义系统提示

使用 `--append-system-prompt` 添加指令同时保持默认行为：

```bash
gh pr diff "$1" | claude -p \
  --append-system-prompt "You are a security engineer. Review for vulnerabilities." \
  --output-format json
```

使用 `--system-prompt` 完全替换默认提示。

### 4.6 对话管理

使用 `--resume` 和会话 ID 继续特定对话。在并行运行多个 Claude 实例时特别有用：

```bash
# 从第一次调用获取会话 ID
session_id=$(claude -p "Start a review" --output-format json | jq -r '.session_id')

# 恢复该特定对话
claude -p "Continue that review" --resume "$session_id"
```

### 4.7 Plan 模式工作流

对于复杂任务，使用"先规划后执行"工作流确保上下文干净：

1. **生成计划**：使用 `--permission-mode plan` 获取计划但不执行

```bash
claude -p "Implement user authentication feature" --permission-mode plan --output-format json
```

2. **检查计划**：查看返回的计划并确认

3. **执行**：用新 session 执行（不是 resume）

```bash
# 在新 session 中执行 - 不要使用 --resume
claude -p "Execute: [paste the confirmed plan here]"
```

**重要**：执行时始终使用新 session，不要使用 `--resume`。这确保：

- 干净的执行上下文
- 不携带规划时的讨论内容
- 全新状态开始

**何时使用 Plan 模式**：

| 使用 Plan 模式 | 跳过 Plan |
|--------------|---------|
| 需要修改多个文件 | 单行修复 |
| 不熟悉的代码区域 | 简单 typo 修复 |
| 重构/架构变更 | 添加 console.log |
| 需要讨论方案 | 运行测试 |

### 4.8 Git Worktrees

Git worktree 允许你从同一个仓库创建多个工作目录，每个工作目录在不同分支上，文件系统完全隔离。Claude Code 原生支持：

```bash
# 启动在独立 worktree 中运行的 Claude session
claude --worktree

# 在 Tmux 会话中启动（可后台运行）
claude --worktree --tmux
```

每次 `claude --worktree` 会创建新 worktree，切到新分支，然后在隔离环境中工作。这非常适合并行任务：

- **并行工作**：同时运行多个 Claude 实例，每个在各自的 worktree 中
- **互不干扰**：一个 worktree 中的更改不影响其他分支
- **轻松合并**：完成后将分支合并回主分支

**Boris 的工作方式**：他并行运行 5 个 Claude Code 实例，每个在不同 worktree 中，加上 claude.ai/code 网页端的 5-10 个会话——同时推进十几个任务。

---

## 参考资料

- [Claude Code 官方文档](https://code.claude.com/docs/zh-CN/overview)
