# 配置 API Key

> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue。

## 为什么需要 API Key

`dsh` 调用模型要走 DeepSeek（或你配置的第三方）接口，接口靠 API Key 识别身份和计费。**没有 Key，就调不动模型。**

## 三种配置方式

优先级从高到低：**环境变量 > `~/.dsh/.credentials.yaml` > 项目 `.env`**。高优先级的会覆盖低优先级。

### 方式一：环境变量（临时、最省事）

```bash
# macOS / Linux / Git Bash
export DEEPSEEK_API_KEY=sk-xxx

# Windows PowerShell
$env:DEEPSEEK_API_KEY = "sk-xxx"

# Windows cmd
set DEEPSEEK_API_KEY=sk-xxx
```

- 优点：不落盘、用完即走，适合临时用或 CI。
- 缺点：关掉终端就失效；`dsh` 和 `export` 必须在**同一个终端会话**。

### 方式二：凭据文件（长期、固定机器）

真正的 Key 只存在 `$DSH_HOME/.credentials.yaml`（`$DSH_HOME` 默认 `~/.dsh`）。

- `settings.yaml` 里**只存引用**（如 `apiKeyEnv: DEEPSEEK_API_KEY`），不存明文 Key。
- 适合一台电脑长期使用，不用每次设置环境变量。

> ⚠️ 这个文件是你的"钱包"，**绝不能提交到 Git**（本仓库 `.gitignore` 已排除）。

### 方式三：项目 `.env`（单项目）

在项目根目录放一个 `.env` 文件：

```
DEEPSEEK_API_KEY=sk-xxx
```

适合 Key 跟着某个项目走、需要团队共享的场景。同样要加进 `.gitignore`。

## 用环境变量引用 Key（推荐模式）

在 `settings.yaml` 里，provider 通过 `apiKeyEnv` 字段指定"从哪个环境变量读 Key"，而不是直接写 Key：

```yaml
llm-pi-ai:
  providers:
    my-provider:
      api: openai-completions
      baseURL: https://api.deepseek.com/v1
      apiKeyEnv: DEEPSEEK_API_KEY   # 读环境变量，而不是写明文
      models:
        - id: deepseek-flash
```

这样 Key 与环境变量绑定，配置文件和代码里都不出现明文 Key。

## 常见问题

| 现象 | 原因 | 解决 |
|---|---|---|
| `MISSING_CREDENTIAL` | 没配 Key，或 `apiKeyEnv` 指的环境变量没设 | 存 Key，或 `export` 对应环境变量 |
| 配了但没生效 | 被更高优先级的方式覆盖 | 按优先级排查，去掉多余的配置 |
| 401 / 认证失败 | Key 错误或余额不足 | 核对 Key，检查账户余额 |

## 安全清单

- [ ] Key 从未写进 `.md` / 代码 / 已提交文件
- [ ] `.env`、`.credentials.yaml` 在 `.gitignore` 中
- [ ] 需要团队共享时，用环境变量或密钥管理服务，而不是把 Key 存进仓库

## 下一步

Key 配好了，接着看 [模型配置](models.md)，了解怎么选模型、接自定义 provider。
