# 04 · 常见问题 FAQ

> 本文基于 dsh 0.1.x 编写，如有出入请提 Issue。

## 安装相关

### `dsh: command not found` / Windows 提示"不是内部或外部命令"

说明 `dsh` 没装好，或没在 PATH 里。

1. 运行 `npm list -g --depth=0`，确认 `@deepseek-ai/dsh` 在列表中。
2. 运行 `npm bin -g` 得到全局 bin 目录，确认这个目录在系统 PATH 中。
3. 改完 PATH 后**重新打开终端**再试。

### 提示 Node 版本过低

`dsh` 需要 **Node 22.19+ 或 24**。运行 `node -v` 确认。若版本低，按 [01 · 安装第 1 步](01-installation.md) 升级，并重开终端。

### `npm install -g` 报权限错误（macOS / Linux）

全局安装需要权限。两种办法：

```bash
# 办法 A：用 sudo（不推荐，可能有副作用）
sudo npm install -g @deepseek-ai/dsh

# 办法 B：用 nvm 管理 Node，避免全局权限问题（推荐）
```

## API Key / 认证相关

### 提示 "认证失败" / "invalid api key"

- 确认 Key 拼写正确、`sk-` 开头完整。
- 确认用环境变量方式时，`dsh` 和 `export` 在**同一个终端会话**里。
- 确认账户有余额（DeepSeek 按量计费，余额为 0 会失败）。

### 三种配置方式到底用哪个？

| 场景 | 建议 |
|---|---|
| 只想快速试试 | 环境变量（临时，关终端即失效） |
| 固定在一台电脑长期用 | `~/.dsh/.credentials.yaml` |
| 单个项目里用、想跟着项目走 | 项目目录下的 `.env` |

三者优先级：**环境变量 > `.credentials.yaml` > `.env`**。已配置但没生效时，检查是否被更高优先级的方式覆盖了。

### 数据都存在哪？

默认在 `$DSH_HOME`，即 `~/.dsh`。里面有配置（`settings.yaml`）、凭据（`.credentials.yaml`）、会话（`sessions/`）、附件等。想换位置可设置 `DSH_HOME` 环境变量。

## 运行相关

### 打开 `127.0.0.1:3080` 打不开

- 确认终端里 `dsh web` 还在运行（那个窗口不能关）。
- 确认访问的是 `127.0.0.1` 而不是 `localhost`（极少数系统代理会拦截 localhost）。
- 如果端口被占，换端口启动。

### `EADDRINUSE ... :3080`（端口被占用）

3080 端口被别的程序占了。关掉占用程序，或换一个端口（进阶内容见配置章节）。

### headless 没有任何输出

`headless` 只在 stdout 打印**最后一条非空助手文本**。如果任务失败或没有文本结果，可能确实没输出。用退出码判断：

```bash
echo $?            # macOS / Linux / Git Bash
$LASTEXITCODE       # Windows PowerShell
```

### 想让它中途问我、需要人工审批的操作

`headless` 是"无人值守"模式，需要审批的操作会**默认拒绝**，不会弹窗问你。这类交互式场景请用 `web` 界面，或社区 TUI 插件。

## Windows 特有

### PowerShell 执行策略报错

如果安装或运行 `dsh` 时遇到 "execution policy" 相关错误，可在当前会话临时放开：

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

### 终端里 `export` 不起作用

`export` 是 bash 语法。Windows PowerShell 请用：

```powershell
$env:DEEPSEEK_API_KEY = "sk-xxx"
```

cmd（命令提示符）请用：

```cmd
set DEEPSEEK_API_KEY=sk-xxx
```

## 还是没解决？

- 看 [CONTRIBUTING.md](../../CONTRIBUTING.md) 里的"提 Issue"一节。
- 用 "问题报告" 模板，附上 **Node 版本、操作系统、报错原文**，方便快速定位。
