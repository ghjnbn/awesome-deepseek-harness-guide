# headless 自动化

> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue。

## 什么时候用 headless？

`headless` = 不交互、跑一个任务、输出结果、退出。适合写进脚本，做批量或定时任务。

回顾它的行为契约（见 [03 · 第一次运行（命令行）](../getting-started/03-first-run-headless.md)）：

- **stdout**：最后一条非空助手文本
- **stderr**：成功时为空
- **退出码**：`0` 完成、`1` 未完成/运行器失败、`130` 被 SIGINT 优雅中断
- **无人值守**：需要审批的操作默认**拒绝**（fail closed），不弹窗

## 单次任务

```bash
export DEEPSEEK_API_KEY=sk-xxx
dsh --profile headless "把当前目录的 .md 文件列出来，统计数量"
echo $?
```

## 批量任务：写个循环脚本

```bash
#!/usr/bin/env bash
export DEEPSEEK_API_KEY=sk-xxx

for f in *.md; do
  dsh --profile headless "总结文件 $f 的内容，输出三句话以内的摘要" >> summary.txt
done
```

（Windows 下可用 PowerShell 的 `foreach` 循环，思路相同。）

## 定时任务

- **Linux / macOS**：用 `cron` 定时执行上面的脚本。
- **Windows**：用「任务计划程序」定时运行 PowerShell 脚本。

## 注意事项

1. **任务要自包含**：headless 不会中途问你，把要求写完整（输入是什么、输出是什么、放哪）。
2. **设计时避开需审批的步骤**：否则会静默失败。
3. **善用退出码**：脚本里根据 `$?` / `$LASTEXITCODE` 判断成功与否，失败时记录日志。
4. **会话不复用**：每次运行是新会话；要延续上下文需 `--resume <session-id>`（进阶）。

## 下一步

- 把 headless 接进 CI：见 [CI/CD](ci-cd.md)。
- 常见 Agent 用法模式：见 [Agent 模式](agent-patterns.md)。
