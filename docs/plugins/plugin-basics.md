# 插件基础（Cordis）

> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue。

## 为什么 `dsh` 一切都是插件？

`dsh` 基于 **Cordis 插件框架**。这意味着：模型、工具、会话、甚至 Web 界面本身，都是"插件"。官方把 Harness 做成一个"壳"，功能靠插件堆上去。

好处：

- **灵活**：想加什么能力，装个插件就行，不用改核心。
- **可组合**：多个插件叠在一起，拼出你自己的工作台。
- **社区友好**：第三方能贡献插件（TUI、MCP 界面、兼容层等）。

## 插件怎么组织起来？

一个 profile 由一组 **bundle**（插件包）组成，声明在 `package.json` 的 `dsh.profile.bundles` 里（见 [profiles 配置](../configuration/profiles.md)）：

```json
"dsh": {
  "profile": {
    "bundles": [
      "@deepseek-ai/dsh-base",
      "@deepseek-ai/dsh-web-app",
      "dshmarket"
    ]
  }
}
```

- `@deepseek-ai/dsh-base`：基础能力
- `@deepseek-ai/dsh-web-app`：Web 界面
- `dshmarket`：插件市场

## 补丁文件：`cordis.patch.yml`

要往插件树里加/改东西，编辑 profile 目录下的 `cordis.patch.yml`（**不要改 `cordis.yml`**）。

一个典型的 patch 条目长这样：

```yaml
- id: my-plugin-instance      # 实例 id，自定义
  name: '@some/plugin-package' # 插件包名
  config:                      # 传给该插件的配置
    key: value
```

`dsh plugin add` 命令本质就是帮你把这类条目写进 patch 文件。

## 配置从哪来？

- **全局设置**：`~/.dsh/settings.yaml`（模型、provider 等，见 [settings.yaml 详解](../configuration/settings-yaml.md)）。
- **插件级配置**：`cordis.patch.yml` 里每个插件条目下的 `config`。

## 下一步

- 具体怎么装插件：见 [安装插件](install-plugins.md)。
- 有哪些好用的插件：见 [常用插件](popular-plugins.md)。
