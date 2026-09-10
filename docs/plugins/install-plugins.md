# 安装插件

> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue。

## 基本命令

```bash
dsh plugin --profile <profile名> add <来源>
```

- `<profile名>`：装到哪个 profile，比如 `web`。
- `<来源>`：可以是 **npm 包、GitHub 仓库、tarball、本地目录**。

装完后通常需要**重启对应的 `dsh` 进程**（关掉再 `dsh web`）让插件生效。

## 四种来源

### 1. npm 包

```bash
dsh plugin --profile web add some-dsh-plugin
```

### 2. GitHub 仓库

用 `github:作者/仓库` 格式：

```bash
dsh plugin --profile web add github:quan-v/dsh-mcp-ui
```

### 3. tarball（压缩包）

```bash
dsh plugin --profile web add https://example.com/plugin.tar.gz
```

### 4. 本地目录

```bash
dsh plugin --profile web add ./my-local-plugin
```

## 举例：给 web 加一个 MCP 配置界面

以社区插件 `dsh-mcp-ui` 为例：

```bash
dsh plugin --profile web add github:quan-v/dsh-mcp-ui
```

然后重启：

```bash
# 先 Ctrl + C 停掉旧的，再重新启动
dsh web
```

重启后在 **Settings → Plugins → Plugin Config → MCP Servers** 就能看到新界面。

## 验证是否装好

- 看 profile 目录下的 `package.json` / `cordis.patch.yml` 是否多了对应条目。
- 或启动后在界面/日志里找插件痕迹。

## 常见问题

| 现象 | 原因 | 解决 |
|---|---|---|
| 装完没反应 | 没重启进程 | 停掉 `dsh` 再重新启动 |
| 提示找不到来源 | 包名/地址写错，或仓库不存在 | 核对来源格式 |
| 版本冲突 | 插件依赖不兼容 | 看日志，换版本或提 Issue 给插件作者 |

## 下一步

- 装什么？看 [常用插件](popular-plugins.md) 清单。
- MCP 相关插件怎么用，见 [MCP 章节](../mcp/what-is-mcp.md)。
