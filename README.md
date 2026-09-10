# awesome-deepseek-harness-guide

> DeepSeek Harness（`dsh`）新手终极指南：从零开始，学会安装、配置、插件、MCP 与 AI Agent 工作流。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![文档语言](https://img.shields.io/badge/文档-中文-ff69b4.svg)](.)
[![DeepSeek Harness](https://img.shields.io/badge/dsh-0.1.x--preview-blue.svg)](https://github.com/deepseek-ai)

**这份指南写给谁？** 完全新手。你不需要懂编程，只要会复制粘贴命令，就能跟着一步步跑通。

---

## 什么是 DeepSeek Harness？

DeepSeek Harness（命令行命令是 `dsh`）是 DeepSeek 官方开源的 **AI Agent 运行时**。它把一个大模型接到工具、文件、终端和互联网上，让 AI 从"只会聊天"变成"能动手干活"。

- 一句话理解：**它是跑 AI 智能体（Agent）的平台/壳**。
- 官方自带两种运行方式：**浏览器界面**（`web`）和 **命令行一次性任务**（`headless`）。
- 目前是 **开发预览版（0.1.x）**，MIT 开源，迭代很快。

想了解它到底能干什么、和 Claude Code / Codex 有什么区别？先读 [00 · 什么是 DeepSeek Harness](docs/getting-started/00-what-is-deepseek-harness.md)。

---

## 快速开始（最快 5 分钟跑通）

```bash
# 1. 检查 Node 版本（需要 22.19+ 或 24）
node -v

# 2. 安装 dsh
npm install -g @deepseek-ai/dsh

# 3. 设置 API Key（两种方式任选其一）
#    方式 A：环境变量
export DEEPSEEK_API_KEY=你的key        # macOS / Linux / Git Bash
$env:DEEPSEEK_API_KEY = "你的key"      # Windows PowerShell

# 4. 跑第一个任务
dsh --profile headless "用一句话介绍你自己"
```

> ⚠️ 第 3 步的 API Key 需要到 DeepSeek 开放平台申请。详细的申请和配置步骤见 [01 · 安装](docs/getting-started/01-installation.md) 与 [02 · 第一次运行](docs/getting-started/02-first-run-web.md)。

---

## 目录导航

### 🚀 新手主线（从这里开始，按顺序读）

| 文档 | 你会学到 |
|---|---|
| [00 · 什么是 DeepSeek Harness](docs/getting-started/00-what-is-deepseek-harness.md) | 它是什么、能干什么、和别的工具的区别 |
| [01 · 安装](docs/getting-started/01-installation.md) | 环境要求、安装、验证 `dsh` 命令 |
| [02 · 第一次运行（浏览器界面）](docs/getting-started/02-first-run-web.md) | 启动 `web`、打开界面、配置 API Key |
| [03 · 第一次运行（命令行）](docs/getting-started/03-first-run-headless.md) | 用 `headless` 跑第一个任务、看懂输出 |
| [04 · 常见问题 FAQ](docs/getting-started/04-faq.md) | 新手高频坑与解决办法 |

### ⚙️ 配置

| 文档 | 你会学到 |
|---|---|
| [配置 API Key](docs/configuration/api-keys.md) | 三种配置方式、凭据安全 |
| [模型配置](docs/configuration/models.md) | 默认模型、自定义 OpenAI 兼容 provider |
| [Profile 配置](docs/configuration/profiles.md) | web / headless / 自定义 profile、bundle |
| [settings.yaml 详解](docs/configuration/settings-yaml.md) | 核心字段、改配置的两种方式 |

### 🧩 插件

| 文档 | 你会学到 |
|---|---|
| [插件基础（Cordis）](docs/plugins/plugin-basics.md) | 为什么一切都是插件、patch 文件 |
| [安装插件](docs/plugins/install-plugins.md) | `dsh plugin add` 四种来源 |
| [常用插件](docs/plugins/popular-plugins.md) | TUI、MCP、兼容层清单 |

### 🔌 MCP

| 文档 | 你会学到 |
|---|---|
| [什么是 MCP](docs/mcp/what-is-mcp.md) | MCP 是什么、概念 |
| [配置 MCP](docs/mcp/configure-mcp.md) | 手写 `dsh-mcp-client` 配置 |
| [MCP 示例](docs/mcp/mcp-examples.md) | stdio / 远程 / 带 token 的示例 |

### 🤖 Agent 工作流

| 文档 | 你会学到 |
|---|---|
| [headless 自动化](docs/workflows/headless-automation.md) | 批量、定时任务 |
| [CI/CD](docs/workflows/ci-cd.md) | GitHub Actions 里跑 dsh |
| [Agent 用法模式](docs/workflows/agent-patterns.md) | 怎么写好任务描述 |

### 🛠 故障排查

- [常见错误排查](docs/troubleshooting/common-errors.md) —— 报错对照表与排查思路

### 🌍 社区资源

- [社区资源索引](community/README.md) —— 官方入口、教程、博客
- [第三方插件目录](community/plugins-catalog.md) —— 社区插件分类清单

### 🧪 示例

- [examples/hello-world](examples/hello-world) —— 一个最小可运行示例，一条命令跑通。

---

## 贡献

欢迎提交 PR、Issue 或勘误。请先阅读 [CONTRIBUTING.md](CONTRIBUTING.md) 了解写作规范与目录约定。

本项目遵循 [行为准则](CODE_OF_CONDUCT.md)。

## 许可证

[MIT](LICENSE)
