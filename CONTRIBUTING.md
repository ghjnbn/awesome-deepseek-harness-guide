# 贡献指南

感谢你为 awesome-deepseek-harness-guide 做贡献！这份指南面向"完全新手"，因此**清楚、准确、可复制**比"全面"更重要。

## 写作规范

### 语言与命名

- **正文用中文**，代码、命令、文件路径、字段名用英文原文。
- **文件名用英文 kebab-case**（小写 + 连字符），例如 `01-installation.md`，不要用中文或空格。
- 文档内的**标题（H1）用中文**，方便阅读与检索。

### 面向小白的原则

每篇教程尽量遵循统一结构：

```text
这是什么 → 为什么需要 → 一步步做 → 验证结果 → 常见报错 → 下一步
```

- 步骤要**编号、可复制**，命令放在 ```bash 代码块里。
- 首次出现的术语，用一句大白话解释。
- 出现 "点击 XX""打开 XX" 时，同时给出 **Windows / macOS / Linux** 的差异（如果有）。

### 版本标注（重要）

DeepSeek Harness 是 **0.1.x 开发预览版，迭代很快**，命令和配置可能变动。因此：

- 每条安装/命令若依赖特定版本，请标注版本，例如 `npm install -g @deepseek-ai/dsh@0.1.0-rc.7`。
- 文档开头可加一句适用版本说明，例如：`> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue`。

### 不要提交的东西

- API Key、`~/.dsh/.credentials.yaml`、`.env` 等任何凭据（已写入 `.gitignore`）。
- 大体积截图/视频，请放到 `assets/` 并控制大小，或用外部图床。

## 目录约定

```text
docs/
  getting-started/   # 新手主线，编号顺序阅读
  configuration/     # 配置（规划中）
  plugins/           # 插件（规划中）
  mcp/               # MCP（规划中）
  workflows/         # Agent 工作流（规划中）
  troubleshooting/   # 故障排查（规划中）
community/           # 社区资源清单（awesome 部分）
examples/            # 可运行的最小示例
assets/              # 图片、架构图
```

- 教程正文放 `docs/`，社区资源清单放 `community/`，两者分离。
- 新增示例时，在 `examples/` 下建独立目录，并带一份自己的 `README.md`。

## 提交流程

1. Fork 仓库，从 `main` 切分支。
2. 提交前本地跑一遍文档检查（见下文）。
3. 提交 PR，描述清楚改了什么、为什么。

## 本地文档检查

仓库配置了 markdownlint 与链接检查（见 `.github/workflows/docs.yml`）。本地可运行：

```bash
npx markdownlint-cli2 "**/*.md"
```

## 提 Issue

- 文档错误 / 过时 → 用 "内容建议 / 勘误" 模板。
- 命令跑不通 → 用 "问题报告" 模板，尽量附上 Node 版本、操作系统、报错原文。
