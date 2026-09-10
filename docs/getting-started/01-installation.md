# 01 · 安装

> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue。

## 本节目标

装好环境，让 `dsh` 命令能在你的终端里跑起来。

## 第 1 步：检查 / 安装 Node.js

`dsh` 需要 **Node.js 22.19 及以上，或 24**（新版 Node 自带 zstd，能处理压缩的会话日志）。

在终端里运行：

```bash
node -v
```

- 如果显示 `v22.19.0`、`v24.x.x` 等 **≥ 22.19** 的版本 → 直接跳到第 2 步。
- 如果显示更低版本、或提示 `node: command not found` → 需要安装/升级。

### 怎么装 Node.js

- **Windows**：去 [nodejs.org](https://nodejs.org/) 下载 LTS 版安装包（.msi），一路"下一步"即可。装完**重新打开终端**再验证。
- **macOS**：`brew install node@24`（或用官网 .pkg 安装包）。
- **Linux**：用 NodeSource 或系统包管理器安装 Node 22+，例如：

```bash
curl -fsSL https://deb.nodesource.com/setup_24.x | sudo -E bash - && sudo apt-get install -y nodejs
```

装完重新运行 `node -v` 确认版本达标。同时可运行 `npm -v` 确认 npm 也装好了。

## 第 2 步：安装 dsh

推荐全局安装，装完就能在任何目录用 `dsh`：

```bash
npm install -g @deepseek-ai/dsh
```

> 💡 不想全局装？也可以每次用 `npx @deepseek-ai/dsh <命令>` 直接运行。为了后面省事，本指南用全局安装。

### 验证安装

```bash
dsh --version
```

如果打印出类似 `0.1.0-rc.7` 的版本号，说明装好了。

如果提示 `dsh: command not found`（Windows 上是"不是内部或外部命令"）：

- 确认全局安装成功（运行 `npm list -g --depth=0` 看有没有 `@deepseek-ai/dsh`）。
- 确认 npm 全局 bin 目录在 `PATH` 里。可用 `npm bin -g` 查看路径，把这个路径加入系统 PATH 后**重开终端**。

## 第 3 步：准备 API Key

`dsh` 需要一个 DeepSeek API Key 才能调用模型。先到 DeepSeek 开放平台申请：

1. 打开 [platform.deepseek.com](https://platform.deepseek.com/)，注册/登录。
2. 进入「API Keys」页面，点「创建」，复制生成的 `sk-...` 开头的 Key（**只显示一次，请保存好**）。
3. 往账户里充值少量余额（DeepSeek 按量计费）。

拿到 Key 后，有三种方式告诉 `dsh`（任选其一即可，三种方式的优先级：环境变量 > `.credentials.yaml` > `.env`）：

| 方式 | 做法 | 适合 |
|---|---|---|
| 环境变量 | 终端里 `export DEEPSEEK_API_KEY=sk-xxx`（Windows PowerShell：`$env:DEEPSEEK_API_KEY="sk-xxx"`） | 临时使用、CI |
| 凭据文件 | 写到 `$DSH_HOME/.credentials.yaml`（`$DSH_HOME` 默认是 `~/.dsh`） | 长期、固定机器 |
| `.env` 文件 | 在项目目录放一个 `.env`，内容 `DEEPSEEK_API_KEY=sk-xxx` | 单个项目 |

> ⚠️ **安全提醒**：Key 等于你的钱包。任何方式都**不要提交到 Git**（本仓库 `.gitignore` 已排除 `.env` 和 `.credentials.yaml`）。

本指南后续示例统一用**环境变量**方式（最简单，不落盘）。

## 第 4 步：看一眼配置（可选）

`dsh` 的配置和会话数据都存在 `$DSH_HOME`（默认 `~/.dsh`）。装好后它会自动生成基础配置。

想看看默认配置长什么样，可以：

```bash
dsh --profile web --dump-default-config
```

（这一步只是"看一眼"，不需要改任何东西。）

## 验证清单

- [ ] `node -v` ≥ 22.19
- [ ] `dsh --version` 能打印版本号
- [ ] 已拿到 API Key

## 下一步

都准备好了？进入 [02 · 第一次运行（浏览器界面）](02-first-run-web.md)，启动图形界面。
