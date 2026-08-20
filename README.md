# DSH 已安装插件备份（第三方插件·来源清单）

> 本仓库记录本机 [DeepSeek Harness (DSH)](https://github.com/deepseek-ai/deepseek-harness) 所安装的**第三方插件/组件的来源信息**，方便日后在新机器上重新安装。
> DSH 内置插件（`@deepseek-ai/dsh-base`、`@deepseek-ai/dsh-web-app` 等 200+ 官方 bundle）不在收录范围。
> 按需求只记录**来源**，不备份源码。

## 插件来源清单

| # | 名称 | 版本 | 来源 | 类型 | 安装位置 |
|---|------|------|------|------|----------|
| 1 | `dsh-better-sidebar` | 0.14.0 | [github:omdsh-dev/DSH-better-sidebar](https://github.com/omdsh-dev/DSH-better-sidebar) · commit `6c89151` | DSH 桌面版插件 | `~/.dsh/profiles/desktop` |
| 2 | `archify` | 2.15.0 | [github:tt-a1i/archify](https://github.com/tt-a1i/archify) · commit `82e63c9` | DSH 网页版插件（Agent Skill，架构图渲染） | `~/.local/share/ai.deepseek.harness.desk/harness/profiles/web` |
| 3 | `dsh-plugin-desktop`（DSH Desktop 桌面应用本体） | 2.0.1 | [github:anywhere-labs/deepseek-harness-desktop](https://github.com/anywhere-labs/deepseek-harness-desktop) · 安装包 `DSH-Desktop-2.0.1-amd64.deb` | Electron 桌面壳（Cordis 插件形态） | `~/.local/opt/DSH Desktop`（deb 安装） |
| 4 | `@deepseek-ai/dsh`（dsh CLI） | 0.1.0-rc.7 | npm: `@deepseek-ai/dsh` | dsh 命令行工具 | `~/.local/lib/node_modules/@deepseek-ai/dsh`（npm 全局） |

## 各插件简介

- **dsh-better-sidebar** — VSCode 风格的右侧边栏工作台：文件管理 / CodeMirror 编辑器 / 内嵌浏览器 / 真实终端（xterm.js + node-pty）/ Git 面板 / 后台任务页，并对外暴露 `ctx.betterSidebar` 服务供其他插件注册侧边栏 Tab 与文件预览器。MIT License。
- **archify** — Agent Skill：把代码库或系统描述变成可交互的系统架构图（architecture / workflow / sequence / dataflow / lifecycle 五种图型），输出自包含 HTML + PNG/SVG/WebM。含 DeepSeek Harness 集成（`integrations/deepseek-harness`，以 `archify-skill-filesystem` Skill 形式接入）。MIT License。
- **dsh-plugin-desktop (DSH Desktop)** — DSH 的 Electron 桌面应用，本身即一个 Cordis 插件。通过官方 deb 包安装。MIT License。
- **dsh CLI** — 官方命令行工具，负责 profile 启动与插件管理（`dsh plugin add ...`）。

## 本机环境快照

本机存在**两个 harness 主目录**（home）：

1. `~/.dsh` — dsh CLI 默认 home
   - `desktop` profile：安装了 `dsh-better-sidebar`（即上表 #1）
   - `web` profile：无第三方插件
2. `~/.local/share/ai.deepseek.harness.desk/harness` — DSH Desktop 桌面应用使用的 home（当前 GUI 正在使用）
   - `web` profile：安装了 `archify` + `dsh-better-sidebar`（即上表 #2，及 #1 的另一份拷贝）
   - `desktop` profile：无第三方插件

> 注意：`archify` 只安装在 DSH Desktop 的 web profile 里；如果你在 CLI 的 `~/.dsh` 里也想要它，需要再执行一次安装命令。

## 如何在新机器上恢复

```bash
# 1. dsh CLI（官方 npm 包）
npm install -g @deepseek-ai/dsh

# 2. DSH Desktop 桌面应用（官方 deb 包，版本 2.0.1）
#    从 https://github.com/anywhere-labs/deepseek-harness-desktop/releases 下载 DSH-Desktop-2.0.1-amd64.deb
sudo dpkg -i DSH-Desktop-2.0.1-amd64.deb

# 3. dsh-better-sidebar 插件（装进 desktop profile）
dsh plugin --profile desktop add github:omdsh-dev/DSH-better-sidebar

# 4. archify 插件（装进 DSH Desktop 的 web profile）
dsh plugin --profile web add github:tt-a1i/archify
# 若要装进 DSH Desktop 使用的 home，先设置：
# export DSH_HOME=~/.local/share/ai.deepseek.harness.desk/harness

# 5.（可选）恢复侧边栏浏览器 tab 设置 —— 在 DSH 设置里开启，或写入 settings.yaml：
# dsh-better-sidebar:
#   tabsEnabled:
#     browser: true
```

## 版权说明

以上插件均为开源项目（MIT License），版权归原作者所有：
- dsh-better-sidebar © [omdsh-dev](https://github.com/omdsh-dev)
- archify © [tt-a1i](https://github.com/tt-a1i)
- deepseek-harness-desktop © [anywhere-labs](https://github.com/anywhere-labs)
- dsh / DeepSeek Harness © [deepseek-ai](https://github.com/deepseek-ai)

本仓库仅记录来源信息用于个人备份，不含任何源码。
