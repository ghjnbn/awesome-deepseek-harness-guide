# 常见错误排查

> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue。

## 快速对照表

| 报错 / 现象 | 常见原因 | 解决办法 |
|---|---|---|
| `dsh: command not found` | 未全局安装 / 不在 PATH | `npm list -g --depth=0` 确认，检查 `npm bin -g` 是否在 PATH |
| Node 版本过低 | 需要 22.19+ 或 24 | `node -v` 确认，升级 Node 后重开终端 |
| `EADDRINUSE ... :3080` | 端口被占用 | 关掉占用程序或换端口 |
| `MISSING_CREDENTIAL` | 缺 API Key / 环境变量未设 | 存 Key 或 `export` 对应环境变量 |
| `UNKNOWN_MODEL` | 模型 id 不在 provider 的 `models` 列表 | 把准确模型 id 加进 `models` |
| `401` / `404` 拉取模型列表 | 接口不提供 `GET /models` | 忽略该按钮，手动填模型 id |
| 认证失败 / invalid api key | Key 错误或余额不足 | 核对 Key、检查账户余额 |
| headless 无输出 | 任务失败或无文本结果 | 用 `echo $?` / `$LASTEXITCODE` 看退出码 |
| 退出码 `1` | 任务未完成 / 运行器失败 | 检查任务描述、Key、网络 |
| 需要审批的操作被拒 | headless 无人值守 fail closed | 改在 `web` 界面跑，或重设计任务避开审批 |

## 排查思路（遇到没见过的错）

1. **读完整报错**：错误信息里通常直接写了原因。
2. **看版本**：`node -v`、`dsh --version`，确认在支持范围。
3. **看配置**：`dsh --profile web --dump-config` 看合并后的配置是否符合预期。
4. **最小复现**：用最简单的任务（如 `"用一句话介绍你自己"`）排除任务本身的问题。
5. **看日志/退出码**：headless 用退出码，web 看终端日志。

## 还解决不了？

按 [CONTRIBUTING.md](../../CONTRIBUTING.md) 提 Issue，附上：

- Node 版本（`node -v`）
- 操作系统
- dsh 版本（`dsh --version`）
- 报错原文
- 你执行的命令

## 相关文档

- 安装问题：[01 · 安装](../getting-started/01-installation.md)、[04 · FAQ](../getting-started/04-faq.md)
- 配置问题：[API Key](../configuration/api-keys.md)、[模型配置](../configuration/models.md)
