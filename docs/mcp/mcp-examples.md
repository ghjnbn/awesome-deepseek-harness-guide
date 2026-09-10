# MCP 示例

> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue。示例中的 server 包名仅作示意，请以各 server 官方 README 为准。

## 示例一：本地 filesystem server（stdio）

给 AI 一个能读写指定目录的 MCP server：

```yaml
- id: mcp-fs
  name: '@deepseek-ai/dsh-mcp-client'
  config:
    serverName: filesystem
    transport: stdio
    command: npx
    args: ['-y', '@modelcontextprotocol/server-filesystem', '/allowed/path']
```

配置后，模型会获得 `mcp__filesystem__read_file` 等工具，能操作 `/allowed/path` 下的文件。

> ⚠️ 注意权限范围：只放行你希望 AI 能访问的目录，别给 `/` 或整个家目录。

## 示例二：远程 server（streamable-http）

```yaml
- id: mcp-remote
  name: '@deepseek-ai/dsh-mcp-client'
  config:
    serverName: myremote
    transport: streamable-http
    url: https://my-mcp.example.com/mcp
    headers:
      Authorization: !!js 'Bearer ' + process.env.MY_TOKEN
```

启动前先 `export MY_TOKEN=xxx`。

## 示例三：带环境变量的 stdio server

有些 server 需要 token 才能用：

```yaml
- id: mcp-github
  name: '@deepseek-ai/dsh-mcp-client'
  config:
    serverName: github
    transport: stdio
    command: npx
    args: ['-y', 'some-github-mcp-server']
    env:
      GITHUB_TOKEN: !!js process.env.GITHUB_TOKEN
```

> `!!js process.env.GITHUB_TOKEN` 是 YAML 里的 JS 表达式语法，表示"取宿主环境变量 GITHUB_TOKEN 的值"，这样配置里就不会出现明文 token。

## 验证方法

1. 配置好、重启对应 profile。
2. 在 Web 界面里问一句能触发该工具的问题，例如接 filesystem 后问："看看 /allowed/path 下有哪些文件"。
3. 观察是否出现 `mcp__<serverName>__<toolName>` 的工具调用。

## 进阶：图形化管理和热同步

如果懒得手写 YAML，装 `dsh-mcp-ui` 后用界面管理，保存即热同步（无需重启）：

```bash
dsh plugin --profile web add github:quan-v/dsh-mcp-ui
```

## 下一步

- 手写配置的完整字段说明：见 [配置 MCP](configure-mcp.md)。
- 更多现成 server 合集：见 [community](../../community/README.md)。
