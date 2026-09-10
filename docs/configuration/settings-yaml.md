# settings.yaml 详解

> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue。

## 位置

个人设置文件在：

```
~/.dsh/settings.yaml      # 即 $DSH_HOME/settings.yaml
```

（`$DSH_HOME` 默认是 `~/.dsh`，可设环境变量改位置。）

## 怎么改

两种方式，效果一样：

1. **直接编辑文件**：用文本编辑器打开 `~/.dsh/settings.yaml` 改。
2. **Web 界面**：启动 `dsh web` 后，进 **Settings → Models**，可以图形化加 provider、改模型。

> 改动在**下一次请求时生效**，无需重启。

## 核心字段

### `agent-default-model`：默认模型

```yaml
agent-default-model:
  provider: deepseek-official
  model: deepseek-flash
  reasoningEffort: high   # low | medium | high
```

新会话默认用这个模型。

### `llm-pi-ai`：模型路由 / provider

```yaml
llm-pi-ai:
  providers:
    <provider-id>:
      api: openai-completions
      baseURL: https://...
      apiKeyEnv: XXX_API_KEY
      models:
        - id: <model-id>
          name: <显示名>   # 可选
```

各字段含义见 [模型配置](models.md)。

### 其他常见配置

`dsh` 的完整字段较多，且随版本变动。最稳妥的做法是用命令看默认配置：

```bash
dsh --profile web --dump-default-config
```

对照默认配置，你就能知道当前版本支持哪些键、默认值是什么。

## 关于凭据分离

`settings.yaml` 里**不存明文 Key**，只存引用（如 `apiKeyEnv: DEEPSEEK_API_KEY`）。真正的 Key 在 `~/.dsh/.credentials.yaml`，或来自环境变量。详见 [配置 API Key](api-keys.md)。

## 修改示例：接一个自定义 provider

假设你要接一个 OpenAI 兼容的第三方服务：

1. 打开 `~/.dsh/settings.yaml`。
2. 在 `llm-pi-ai.providers` 下加一个条目：

```yaml
llm-pi-ai:
  providers:
    my-third-party:
      api: openai-completions
      baseURL: https://my.service.example.com/v1
      apiKeyEnv: MY_SERVICE_KEY
      models:
        - id: their-fast-model
```

3. 设好环境变量 `MY_SERVICE_KEY`。
4. 在 `agent-default-model` 里把 `provider` 改成 `my-third-party`、`model` 改成 `their-fast-model`。

下一次请求就会走这个新 provider。

## 常见坑

| 现象 | 原因 | 解决 |
|---|---|---|
| 改了没效果 | 改动在下一次请求才生效，或改错了文件 | 确认文件是 `~/.dsh/settings.yaml` |
| 报 `UNKNOWN_MODEL` | 模型 id 不在 `models` 列表 | 把准确 id 加进 `models` |
| YAML 缩进报错 | YAML 对缩进敏感 | 用空格（别用 Tab），对齐层级 |

## 下一步

- 模型字段细节：见 [模型配置](models.md)。
- profile 与插件树：见 [profiles 配置](profiles.md)、[插件基础](../plugins/plugin-basics.md)。
