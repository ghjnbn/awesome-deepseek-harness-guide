# Profile 配置

> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue。

## 什么是 profile？

`dsh` 是 **profile 启动器**，不是"打开一个对话框"。一个 profile 就是一套打包好的插件组合，决定了你启动后得到什么界面/能力。

官方自带：

| Profile | 用途 | 启动命令 |
|---|---|---|
| `web` | 浏览器界面，默认 `http://127.0.0.1:3080` | `dsh web` |
| `headless` | 跑一个任务 → 输出 → 退出 | `dsh --profile headless "任务"` |

社区还会提供 `tui`（终端交互界面）等 profile。

## profile 长什么样？

每个 profile 是一个目录，核心文件是 `package.json` 和 Cordis 配置：

```
profiles/
  web/
    package.json        # 声明这个 profile 用哪些 bundle
    cordis.yml          # Cordis 插件树（通常是空列表 []）
    cordis.patch.yml    # 补丁式配置，改这里而不是改 cordis.yml
```

### `package.json`：声明用哪些 bundle

```json
{
  "name": "dsh-profile-web",
  "private": true,
  "dependencies": {
    "dshmarket": "^1.45.1"
  },
  "dsh": {
    "profile": {
      "bundles": [
        "@deepseek-ai/dsh-base",
        "@deepseek-ai/dsh-web-app",
        "dshmarket"
      ],
      "patchReload": "live"
    }
  }
}
```

- `dsh.profile.bundles`：这个 profile 由哪些插件包组成。`dsh-base` 是基础，`dsh-web-app` 提供 Web 界面，`dshmarket` 是插件市场。
- `patchReload: live`：改动 patch 文件后热重载。

### `cordis.yml` 与 `cordis.patch.yml`

`dsh` 基于 **Cordis 插件框架**，插件树以"补丁"方式组合：

- `cordis.yml`：树的基础，通常就是空列表 `[]`。
- `cordis.patch.yml`：你的**补丁**。**改配置请编辑 `cordis.patch.yml`，不要直接改 `cordis.yml`**（它会被 patch 覆盖）。

## 查看配置

不用启动就能看配置：

```bash
dsh --profile web --dump-config          # 看当前合并后的配置
dsh --profile web --dump-default-config  # 看默认配置
```

## 自定义 profile

想做一个自己的 profile，思路是：复制现有 profile 结构 → 改 `package.json` 里的 `bundles` → 用 `cordis.patch.yml` 加插件/配置。进阶示例见 [插件章节](../plugins/plugin-basics.md)。

## 下一步

- 理解插件怎么加进去：见 [插件基础](../plugins/plugin-basics.md)。
- 想改具体设置项：见 [settings.yaml 详解](settings-yaml.md)。
