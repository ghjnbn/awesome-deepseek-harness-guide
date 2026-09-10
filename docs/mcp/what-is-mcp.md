# 什么是 MCP

> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue。

## 一句话解释

**MCP（Model Context Protocol，模型上下文协议）是一个开放标准，让 AI 能"外接"各种工具和数据源。**

打个比方：AI 模型是个很聪明但"关在房间里"的人，它懂很多，但看不到你的文件、查不了你的数据库。MCP 就是给这个房间**开一扇扇门**，每扇门后面是一个工具或数据源（本地文件、GitHub、数据库、浏览器……）。

## 为什么需要 MCP？

没有 MCP 时，想让 AI 访问新工具，往往要为每个工具写专门的对接代码。有了 MCP：

- 一套标准接口，**一次对接，到处复用**。
- AI 能调用 `mcp__<服务器名>__<工具名>` 这样的命名工具。
- 生态里有大量现成的 MCP server 可直接装。

## MCP 里有什么概念？

| 概念 | 说明 |
|---|---|
| MCP server | 提供工具/数据的一方（比如一个能操作 GitHub 的 server） |
| MCP client | 使用方，也就是 `dsh`，负责连 server、发现工具 |
| 工具（tool） | server 暴露给 AI 调用的具体能力 |
| 传输（transport） | 怎么连：`stdio`（本地进程）或 `streamable-http`（远程 URL）/ SSE |

## `dsh` 里的 MCP

`dsh` 官方提供 MCP client：`@deepseek-ai/dsh-mcp-client`。接好一个 server 后，它的工具会以 `mcp__<serverName>__<toolName>` 的形式出现在模型可用工具里。

你可以：

1. 直接手写配置（见 [配置 MCP](configure-mcp.md)）。
2. 或装图形化插件（如 `dsh-mcp-ui`）在 Web 界面里点点点配置。

## 下一步

- 动手配一个 MCP server：见 [配置 MCP](configure-mcp.md)。
- 看具体例子：见 [MCP 示例](mcp-examples.md)。
