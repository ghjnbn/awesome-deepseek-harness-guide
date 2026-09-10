# 在 CI/CD 里跑 dsh

> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue。

## 思路

把 `headless` 接进 CI（如 GitHub Actions），让流水线里跑一个 AI 任务——比如自动生成变更说明、审查代码、跑一个质检任务。

核心步骤：

1. 装 Node（22.19+ 或 24）。
2. 装 `@deepseek-ai/dsh`。
3. 用 **Secret** 提供 API Key（绝不写进仓库）。
4. 跑 `dsh --profile headless "任务"`。

## GitHub Actions 示例

```yaml
name: AI Task

on:
  workflow_dispatch:          # 手动触发；也可改成 push / pull_request

jobs:
  run-dsh:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: 24

      - name: 安装 dsh
        run: npm install -g @deepseek-ai/dsh

      - name: 跑 headless 任务
        env:
          DEEPSEEK_API_KEY: ${{ secrets.DEEPSEEK_API_KEY }}
        run: |
          dsh --profile headless "读取仓库里的 CHANGELOG 建议，输出 3 条改进点"
```

### 关键点

- **Key 放 Secret**：在仓库 Settings → Secrets 里建 `DEEPSEEK_API_KEY`，用 `${{ secrets.DEEPSEEK_API_KEY }}` 引用。
- **版本锁定**：为可复现，可把安装写成 `npm install -g @deepseek-ai/dsh@0.1.0-rc.7`（锁定具体版本）。
- **退出码**：headless 失败会返回非 0，CI 自动判失败。

## 无人值守的注意点

- headless 在无人值守下**需要审批的操作会失败**，任务要设计成不需要人工确认。
- 任务输出要可校验：让 headless 把结果写到文件，供后续步骤检查或归档。

## 下一步

- headless 行为细节：见 [headless 自动化](headless-automation.md)。
- 常见用法模式：见 [Agent 模式](agent-patterns.md)。
