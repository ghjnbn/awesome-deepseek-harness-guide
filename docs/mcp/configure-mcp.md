# 配置 MCP

> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue。

## 两种方式

| 方式 | 适合 | 做法 |
|---|---|---|
| 手写 `cordis.patch.yml` | 想精确控制、写脚本 | 直接加 `@deepseek-ai/dsh-mcp-client` 条目 |
| 图形化插件（如 `dsh-mcp-ui`） | 不想碰配置、喜欢点点点 | 装插件后在 Web 界面里配 |

下面重点讲**手写方式**，因为它最通用、可移植。

## 手写配置：在 `cordis.patch.yml` 里加 server

编辑 profile 目录下的 `cordis.patch.yml`，加入一个 `@deepseek-ai/dsh-mcp-client` 实例：

```yaml
- id: mcp-myserver
  name: '@deepseek-ai/dsh-mcp-client'
  config:
    serverName: myserver
    transport: stdio            # 或 streamable-http
    command: npx
    args: ['-y', 'your-mcp-server']
    env:
      YOUR_TOKEN: !!js process.env.YOUR_TOKEN
```

### 字段说明

| 字段 | 说明 |
|---|---|
| `id` | 这个插件实例的自定义 id |
| `name` | 固定写 `@deepseek-ai/dsh-mcp-client` |
| `serverName` | server 名字，决定工具前缀 `mcp__<serverName>__...` |
| `transport` | `stdio`（本地进程）或 `streamable-http`（远程 URL）/ SSE |
| `command` / `args` | `stdio` 时用：启动 server 的命令和参数 |
| `env` | 传给 server 的环境变量；`!!js process.env.XXX` 表示引用宿主环境变量 |

### 远程 server（streamable-http）

本地进程换成远程地址：

```yaml
- id: mcp-remote
  name: '@deepseek-ai/dsh-mcp-client'
  config:
    serverName: remote
    transport: streamable-http
    url: https://example.com/mcp
    headers:
      Authorization: !!js 'Bearer ' + process.env.YOUR_TOKEN
```

## 配置好后

工具会以 `mcp__<serverName>__<toolName>` 形式暴露给模型。重启对应 profile 后，模型就能调用这些工具了。

## 图形化方式（可选）

想用界面配置，可以装 `dsh-mcp-ui`：

```bash
dsh plugin --profile web add github:quan-v/dsh-mcp-ui
```

重启 `dsh web` 后，在 **Settings → Plugins → Plugin Config → MCP Servers** 里管理 server。它帮你把上面的配置写好，支持 stdio / streamable-http / SSE、超时、失败策略、自动重连等字段，并把 server 列表存到 `~/.dsh/settings.yaml`。

## 常见问题

| 现象 | 原因 | 解决 |
|---|---|---|
| 工具没出现 | 没重启，或 `name` 写错 | 确认 `name` 是 `@deepseek-ai/dsh-mcp-client`，重启 |
| server 起不来 | `command`/`args` 不对，或缺依赖 | 手动跑一下那条命令看报错 |
| 认证失败 | `env`/`headers` 里的 token 没设 | 先设好对应环境变量 |

## 下一步

- 看几个真实例子：见 [MCP 示例](mcp-examples.md)。
- 完整社区插件清单：见 [community](../../community/README.md)。
