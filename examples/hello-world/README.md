# hello-world

最小可运行示例：一条命令，验证 DeepSeek Harness 安装和配置是否正确。

> 基于 dsh 0.1.x。运行前请先完成 [01 · 安装](../../docs/getting-started/01-installation.md)。

## 运行

### macOS / Linux / Git Bash

```bash
export DEEPSEEK_API_KEY=sk-你的key
dsh --profile headless "用一句话介绍你自己"
echo $?
```

### Windows PowerShell

```powershell
$env:DEEPSEEK_API_KEY = "sk-你的key"
dsh --profile headless "用一句话介绍你自己"
$LASTEXITCODE
```

## 预期结果

- 终端打印一句 DeepSeek 的自我介绍。
- 退出码为 `0`。

## 说明

这个示例只做一件事：用 `headless` 模式跑一个最简单的任务。它的作用是**快速验证环境**，而不是展示复杂功能。

想更进一步？看 [03 · 第一次运行（命令行）](../../docs/getting-started/03-first-run-headless.md) 里"真干活"的例子，让 Agent 帮你创建文件、读目录。
