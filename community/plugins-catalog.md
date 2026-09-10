# 第三方插件目录

> DeepSeek Harness 是 0.1.x 预览版，插件迭代快。本页按用途分类收录第三方插件，以各自最新 README 为准。

> ⚠️ 均为社区 / 第三方插件，非官方支持。安装前请评估来源可信度。

## 终端界面（TUI）

| 插件 | 命令/入口 | 说明 |
|---|---|---|
| `@brianynwu/dsh-tui` | TUI bundle | 流式 Markdown、工具卡片、审批、slash 命令、切换模型 |
| `@aruvelut_6/dsh-cli` | `dshcli` | Claude Code 风格 REPL，流式、多轮、会话恢复 |
| `@dopejs/dsh-tui` | `dtui` | 同进程终端界面，`--doctor` / `--resume` / `--print` |

## MCP 管理

| 插件 | 说明 |
|---|---|
| `dsh-mcp-ui` | 图形化 MCP server 配置界面，接官方 `dsh-mcp-client` |
| `dsh-plugin-mcp` | 通用 MCP 桥接，CLI + 多级配置 + 权限引擎 |
| `dsh-mcp-bridge` | 精选 MCP server 合集 |
| `dsh-manage-hub` | 增加 Skills 与 MCP 管理页，配置存 `mcp-servers.yaml` |
| `@anht3889/dsh-mcp-mgmt-bundle` | MCP 连接管理，含 OAuth、单工具开关、连接日志 |

## 兼容层

| 插件 | 说明 |
|---|---|
| `dsh-claude-compat` | 兼容 Claude 的 skill、rules 加载规则与 MCP 配置 |

## 怎么安装

通用命令（见 [安装插件](../docs/plugins/install-plugins.md)）：

```bash
dsh plugin --profile <profile名> add <npm包 | github:作者/仓库 | tarball | 本地目录>
```

示例：

```bash
dsh plugin --profile web add github:quan-v/dsh-mcp-ui
```

## 选用建议

1. **TUI**：想要终端交互，优先看 `@brianynwu/dsh-tui`（功能较全）。
2. **MCP 界面**：不想手写 YAML，选 `dsh-mcp-ui`。
3. **从 Claude 迁移**：看 `dsh-claude-compat`。
4. **隐私/安全敏感**：优先选源码公开、有 CI、权限说明清晰的项目。

## 贡献

发现新插件或信息过时？按 [community/README.md](README.md) 的格式提 PR。
