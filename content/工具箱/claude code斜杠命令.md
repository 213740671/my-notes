# Claude Code 斜杠命令速查笔记

这是一份关于 **Claude Code** (Anthropic CLI) 所有斜杠命令的功能整理，方便在开发时快速检索。

---

## 1. 会话与上下文管理 (Context & Session)
| 命令 | 功能说明 |
| :--- | :--- |
| **`/init`** | 在当前目录初始化 `CLAUDE.md`，用于存储项目规范和背景。 |
| **`/add-dir`** | 将指定的外部目录添加到当前 Claude 会话的上下文中。 |
| **`/clear`** | 彻底清除当前对话历史，重置上下文。 |
| **`/compact`** | 压缩对话。删除冗长历史并生成摘要以节省 Token，同时保留关键信息。 |
| **`/context`** | **可视化工具**：以彩色网格形式展示当前 Token 的消耗分布。 |
| **`/rewind`** | 回溯功能。将代码或会话状态恢复到之前的某个时间点。 |
| **`/resume`** | 列出并恢复之前的历史会话。 |
| **`/rename`** | 为当前会话重命名，便于在历史记录中识别。 |

---

## 2. 开发、任务与记忆 (Development & Memory)
* **`/plan`**：查看或修改 Claude 针对当前任务生成的执行计划。
* **`/tasks`**：管理后台正在运行的异步任务。
* **`/todos`**：查看当前项目积压的待办事项列表。
* **`/skills`**：列出 Claude 当前已掌握并可调用的工具/能力。
* **`/memory`**：**核心功能**：编辑 Claude 的长期记忆文件，记录项目偏好或特定规则。
* **`/mcp`**：管理 Model Context Protocol 服务器，连接数据库、本地文件等外部数据源。

---

## 3. 代码审查与 GitHub 集成 (Review & Git)
* **`/review`**：对当前分支的修改进行代码审查。
* **`/security-review`**：针对安全漏洞对挂起的更改进行专项检查。
* **`/pr-comments`**：直接从 GitHub Pull Request 中拉取评论到终端。
* **`/release-notes`**：查看 Claude Code 的版本更新日志。
* **`/install-github-app`**：在当前仓库配置 Claude GitHub Actions。

---

## 4. 系统、账户与统计 (System & Stats)
| 命令 | 功能说明 |
| :--- | :--- |
| **`/status`** | 查看综合状态（版本、模型、API 连接、账户等）。 |
| **`/stats`** | 查看详细的使用统计数据和开发活动活跃度。 |
| **`/usage`** | 检查当前计费周期内的 Token 或 API 限额使用情况。 |
| **`/doctor`** | 故障排除工具：诊断安装环境、权限和配置问题。 |
| **`/login / /logout`** | 管理 Anthropic 账号的登录状态。 |
| **`/upgrade`** | 快速跳转至升级页面，以获取更高限额或 Opus 模型权限。 |

---

## 5. UI、偏好与编辑器设置 (UI & Preferences)
* **`/config`**：打开交互式配置面板。
* **`/theme`**：切换终端配色方案。
* **`/vim`**：开启/关闭 Vim 模式，习惯使用 HJKL 跳转的用户必开。
* **`/terminal-setup`**：配置终端快捷键（如 Shift+Enter 换行）。
* **`/output-style`**：在“简洁”和“详细”输出模式间切换。
* **`/mobile`**：通过二维码获取 Claude Mobile App 链接。
* **`/stickers`**：访问官方页面订购 Claude 主题贴纸。
* **`/exit`**：安全退出 REPL 环境。

---
> **提示**：直接在终端输入 `/help` 也可以随时查看这些命令的简要说明。