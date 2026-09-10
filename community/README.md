# 社区资源索引

> DeepSeek Harness 是 0.1.x 预览版，社区生态迭代极快。本页收录的资源以各自最新 README 为准，欢迎提交 PR 补充。

> ⚠️ 以下均为**社区 / 第三方**资源，非官方支持。使用前请评估来源可信度。

## 官方入口

- [deepseek-ai/DeepSeek-Harness](https://github.com/deepseek-ai/DeepSeek-Harness) —— 官方仓库与文档
- [DeepSeek 开放平台](https://platform.deepseek.com/) —— API Key、模型、计费

## 终端界面（TUI）

| 项目 | 说明 |
|---|---|
| [@brianynwu/dsh-tui](https://www.npmjs.com/package/@brianynwu/dsh-tui) | TUI 插件 bundle，流式 Markdown、工具卡片、审批、slash 命令、切换模型 |
| [@aruvelut_6/dsh-cli](https://www.npmjs.com/package/@aruvelut_6/dsh-cli) | `dshcli`，Claude Code 风格 REPL |
| [@dopejs/dsh-tui](https://www.npmjs.com/package/@dopejs/dsh-tui) | `dtui`，同进程终端界面，带 `--doctor` / `--resume` |

## MCP 相关

| 项目 | 说明 |
|---|---|
| [quan-v/dsh-mcp-ui](https://github.com/quan-v/dsh-mcp-ui) | MCP server 图形化配置界面插件 |
| [dsh-plugin-mcp](https://www.npmjs.com/package/dsh-plugin-mcp) | 通用 MCP 桥接，带 CLI 与权限引擎 |
| [dsh-mcp-bridge](https://socket.dev/npm/package/dsh-mcp-bridge) | 精选 MCP server 合集（memory、filesystem、GitHub、Playwright 等） |
| [zhang-guo-wen/dsh-claude-compat](https://github.com/zhang-guo-wen/dsh-claude-compat) | 兼容 Claude 的 skill / rules 与 MCP 配置 |

## 教程与博客

- [DeepSeek Harness: What It Is, How to Run It（Modellix）](https://www.modellix.ai/blog/deepseek-harness/)
- [How to Install DeepSeek Harness: npx, Source & Headless（OrcaRouter）](https://www.orcarouter.ai/blog/how-to-install-deepseek-harness)
- [DeepSeek Harness on Windows（OrcaRouter）](https://www.orcarouter.ai/blog/deepseek-harness-windows-tui)

## 贡献方式

想补充资源？请按以下格式提交 PR：

```markdown
| [项目名](链接) | 一句话说明 |
```

并确保：

- 链接可访问、描述准确。
- 标注是否官方、是否需评估权限。
- 不放任何含凭据 / 盗版的内容。

## 相关文档

- 插件清单与选用建议：见 [plugins-catalog.md](plugins-catalog.md)。
- 教程内推荐的插件：见 [docs/plugins/popular-plugins.md](../docs/plugins/popular-plugins.md)。
