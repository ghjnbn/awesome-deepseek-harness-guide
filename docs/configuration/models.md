# 模型配置

> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue。

## 默认模型：`agent-default-model`

`settings.yaml` 里的 `agent-default-model` 决定新会话默认用哪个模型：

```yaml
agent-default-model:
  provider: deepseek-official
  model: deepseek-flash
  reasoningEffort: high   # low | medium | high
```

| 字段 | 说明 |
|---|---|
| `provider` | 用哪个 provider（下文会讲） |
| `model` | 该 provider 下的模型 ID |
| `reasoningEffort` | 推理强度：`low` / `medium` / `high` |

> 💡 `deepseek-flash` 是 DeepSeek 官方 provider 下常见的默认模型。具体可用模型以 DeepSeek 官方文档为准，模型名可能随版本变动。

## 自定义 provider：接任意 OpenAI 兼容接口

`dsh` 的模型路由叫 `llm-pi-ai`。只要对方是 OpenAI 兼容接口，就能接进来：

```yaml
llm-pi-ai:
  providers:
    my-provider:                 # 自定义的 provider id
      api: openai-completions    # 走 OpenAI Chat Completions 协议
      baseURL: https://api.example.com/v1
      apiKeyEnv: EXAMPLE_API_KEY # 从环境变量读 Key
      models:
        - id: my-model-1
          name: 模型一号          # 可选，界面显示名
        - id: my-model-2
```

### 字段说明

| 字段 | 必填 | 说明 |
|---|---|---|
| `api` | 是 | 协议类型，OpenAI 兼容接口填 `openai-completions` |
| `baseURL` | 是 | 接口地址 |
| `apiKeyEnv` | 是 | 存 Key 的环境变量名（不写明文 Key） |
| `models` | 是 | 该路由的模型目录 |

### 重要：`models` 是"替换"不是"追加"

自定义 provider 里的 `models` 列表会**替换**（而非追加）该路由的模型目录。所以每个 `id` 必须是发送给接口的**精确模型 ID**。只写 `id` 一项也够用。

## 高级字段

- **图片输入**：手动加的模型默认只支持文本。要声明支持图片，给模型加 `input: [text, image]`，或在路由层设 `defaultInput: [text, image]`。
- **覆盖内置模型**：内置 provider 若没有 `models` 列表，可用 `modelOverrides`（按模型 id 为键）覆盖个别设置。

## 常见报错

| 报错 | 原因 | 解决 |
|---|---|---|
| `MISSING_CREDENTIAL` | 缺 Key 或 `apiKeyEnv` 环境变量未设 | 存 Key / 设环境变量 |
| `UNKNOWN_MODEL` | 模型不在该路由的 `models` 列表里 | 把准确的模型 id 加进 `models` |
| 拉取模型列表返回 401/404 | 很多 OpenAI 兼容接口不提供 `GET /models` | 忽略该按钮，手动填模型 id |

## 修改后生效时机

配置改动在**下一次请求时生效**，无需重启服务。

## 下一步

- 想改模型、加 provider 的界面操作，见 [settings.yaml 详解](settings-yaml.md)。
- 想了解 `web` / `headless` 怎么切换，见 [profiles 配置](profiles.md)。
