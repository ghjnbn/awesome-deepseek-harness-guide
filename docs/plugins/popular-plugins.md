# 常用插件清单

> 本文基于 dsh 0.1.x 编写。社区插件迭代快，安装前请以各自仓库的最新 README 为准。

> ⚠️ 以下第三方插件多为社区维护，非官方支持。安装任何插件前请评估来源可信度。

## 终端界面（TUI）

官方 `dsh` 不默认带交互式终端，社区插件补上了"像 Claude Code 那样聊天"的体验：

| 插件 | 说明 |
|---|---|
| `@brianynwu/dsh-tui` | TUI 插件 bundle，支持流式 Markdown、工具卡片、审批、slash 命令、切换模型 |
| `@aruvelut_6/dsh-cli` | `dshcli`，Claude Code 风格 REPL，流式、多轮上下文、会话恢复 |
| `@dopejs/dsh-tui` | `dtui`，同进程终端界面，带 `--doctor` / `--resume` / `--print` |

## MCP 相关

| 插件 | 说明 |
|---|---|
| `dsh-mcp-ui` | 图形化 MCP server 配置界面，自动接官方 `dsh-mcp-client`（`dsh plugin --profile web add github:quan-v/dsh-mcp-ui`） |
| `dsh-plugin-mcp` | 通用 MCP 桥接，带 CLI（`dsh-mcp catalog/install/add/list`）、多级配置、权限与缓存 |
| `dsh-mcp-bridge` | 精选 MCP server 合集（demo、memory、filesystem、GitHub、Playwright 等） |
| `dsh-claude-compat` | 兼容 Claude 的 skill / rules 加载规则与 MCP 配置 |

## 兼容 / 生态

| 插件 | 说明 |
|---|---|
| `dsh-claude-compat` | 让 `dsh` 兼容 Claude 的 skill、rules 加载规则 |

## 怎么判断一个插件靠不靠谱？

1. 看仓库的 star、最近更新时间、README 是否清晰。
2. 看它请求了哪些权限（是否读写你的文件、联网）。
3. 优先选有 CI、有版本号、有明确作者的项目。
4. 不确定时，先在一个隔离环境 / 临时 profile 里试。

## 下一步

- 完整的社区资源索引（插件、教程、视频）见 [community/README.md](../../community/README.md)。
- MCP 到底是什么、怎么配，见 [MCP 章节](../mcp/what-is-mcp.md)。
