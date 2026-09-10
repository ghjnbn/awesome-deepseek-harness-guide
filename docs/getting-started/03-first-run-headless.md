# 03 · 第一次运行（命令行 headless）

> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue。

## 本节目标

用 `headless` profile 在命令行里跑一个任务，看懂它的输出，为后面的自动化打基础。

## 什么是 headless？

`headless`（无头模式）= 不打开任何界面，**跑一个任务 → 输出结果 → 退出**。

它特别适合：

- 写进脚本、定时任务、CI 流水线
- 批量处理
- 不想开浏览器、只想快速拿到一个结果

## 第 1 步：设置 API Key

同样先设置环境变量：

```bash
# macOS / Linux / Git Bash
export DEEPSEEK_API_KEY=sk-xxx
```

```powershell
# Windows PowerShell
$env:DEEPSEEK_API_KEY = "sk-xxx"
```

## 第 2 步：跑第一个任务

```bash
dsh --profile headless "用一句话介绍你自己"
```

它会：

1. 新建一个持久化的会话
2. 执行你给的任务
3. 在 **stdout（标准输出）** 打印最后一条非空的助手回复
4. 退出

正常情况下，你会直接在终端看到那一句回答。

## 第 3 步：看懂退出码

`headless` 用退出码告诉你任务成没成，脚本里常用它判断：

| 退出码 | 含义 |
|---|---|
| `0` | 任务完成 |
| `1` | 未完成 / 运行器失败 |
| `130` | 被 `SIGINT`（如 `Ctrl + C`）优雅中断 |

在 Linux / macOS / Git Bash 里可以用 `echo $?` 查看上一条命令的退出码：

```bash
dsh --profile headless "用一句话介绍你自己"
echo $?   # 输出 0 表示成功
```

在 Windows PowerShell 里用 `$LASTEXITCODE`：

```powershell
dsh --profile headless "用一句话介绍你自己"
$LASTEXITCODE
```

## 第 4 步：跑一个"真干活"的任务

试试让它读文件、写结果，体验 Agent 能力：

```bash
dsh --profile headless "在当前目录创建 hello.txt，内容为 Hello DeepSeek，然后告诉我文件创建成功了"
```

任务结束后，`ls`（Windows 是 `dir`）看看当前目录，会发现 `hello.txt` 真的被创建了——这就是 Agent 在帮你动手。

## headless 的几个要点

- **不交互**：它不会中途停下来问你问题。在无人值守场景下，需要审批的操作会**默认拒绝**（fail closed），所以设计任务时要避免需要人工确认的步骤。
- **不开端口**：不像 `web` 那样监听 3080 端口。
- **每次一个会话**：每次运行是新会话；要接着上一次的上下文，需配合 `--resume` 和会话 ID（进阶内容）。

## 验证清单

- [ ] `dsh --profile headless "..."` 能打印回复
- [ ] 退出码是 `0`
- [ ] 成功执行了一个会改动文件的任务

## 常见报错

| 报错 | 原因 | 解决 |
|---|---|---|
| 没有输出、直接退出 | 任务无文本结果或失败 | 用 `echo $?` / `$LASTEXITCODE` 看退出码 |
| 退出码 1 | 任务没跑成 | 检查任务描述、API Key、网络 |
| 提示认证失败 | Key 没配或余额不足 | 重新配置，检查账户余额 |

## 下一步

基础已经跑通。遇到问题先看 [04 · 常见问题 FAQ](04-faq.md)；没问题的可以看看 [examples/hello-world](../../examples/hello-world) 里的最小示例。
