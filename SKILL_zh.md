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
- [环境适配](#环境适配)

---

## 快速开始

Claude Code 是 Anthropic 官方推出的命令行 AI 编程助手，支持代码编辑、调试、重构等多种功能。

### 前置要求

- 安装 Claude Code CLI：`npm install -g @anthropic-ai/claude-code`
- 完成登录：`claude auth login`

### 基础调用方式

```bash
# 交互式对话
claude

# 带初始提示的对话
claude "帮我解释这段代码"

# 打印模式（无交互，适合脚本）
claude -p "Explain this code"
```

---

## 基础命令

### 交互式会话

```bash
# 启动交互式会话
claude

# 带初始提示
claude "Review the changes in this PR"

# 继续最近的对话
claude -c
```

### 打印模式（Print Mode）

打印模式适合脚本调用，返回纯文本结果，不进入交互式界面。

```bash
# 简单查询
claude -p "What does this function do?"

# 复杂查询
claude -p "Review this code for security issues"
```

### 会话管理

```bash
# 继续最近的会话
claude -c

# 恢复指定会话
claude -r <session-id> "Continue with this task"

# 查看会话列表
claude session list
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
| `-c, --continue` | 继续最近的对话 | `claude -c` |
| `-r, --resume <id>` | 恢复指定会话 | `claude -r abc123 "query"` |
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

### 2. 提供足够的上下文

包含相关代码、错误信息或文件路径。

```
# ✅ 好的做法
claude -p "Review src/utils/validator.js - it should validate email format"

# ❌ 缺乏上下文
claude -p "Check this file"
```

### 3. 使用 CLAUDE.md 配置项目

在项目根目录创建 CLAUDE.md 文件，定义项目规范：

```markdown
# 项目规范

## 代码风格
- 使用 TypeScript
- 使用 ESLint + Prettier

## 命令
- 开发：npm run dev
- 测试：npm test
- 构建：npm run build

## 注意事项
- 避免修改 core/ 目录
```

### 4. 利用会话管理

- 使用 `-c` 继续未完成的任务
- 使用 `-r` 恢复特定会话继续工作
- 使用 `claude session list` 查看所有会话

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

## 环境适配

### 在不同环境中调用

Claude Code 可以通过 shell 命令调用。以下是不同环境中的调用方式：

#### Bash / Zsh / Unix Shell

```bash
claude -p "你的查询"
```

#### Windows CMD

```cmd
claude -p "你的查询"
```

#### Windows PowerShell

```powershell
claude -p "你的查询"
```

#### Python 脚本

```python
import subprocess
result = subprocess.run(
    ["claude", "-p", "你的查询"],
    capture_output=True,
    text=True
)
print(result.stdout)
```

#### Node.js

```javascript
const { execSync } = require('child_process');
const result = execSync('claude -p "你的查询"', { encoding: 'utf-8' });
console.log(result);
```

### 注意事项

1. **打印模式优先**：建议使用 `-p` 标志，避免交互式会话
2. **超时设置**：复杂任务建议设置较长的 timeout
3. **输出格式**：可使用 `--output-format json` 获取结构化输出
4. **错误处理**：检查命令返回码和 stderr

### 推荐的调用模式

```bash
# 简单查询
claude -p "Explain this function"

# 复杂任务
claude -p "Refactor this module with TypeScript"

# 带输出的任务
claude -p "Generate comprehensive tests for this API"
