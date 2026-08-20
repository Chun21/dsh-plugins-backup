# DSH 已安装插件备份（第三方插件）

> 本仓库是本机 [DeepSeek Harness (DSH)](https://github.com/deepseek-ai/deepseek-harness) 所安装的**第三方插件**的整理备份。
> DSH 内置插件（`@deepseek-ai/dsh-base`、`@deepseek-ai/dsh-web-app` 等官方 bundle）不在收录范围内。

## 插件清单

| # | 插件名 | 版本 | 来源 | 安装位置（本机 profile） | 简介 |
|---|--------|------|------|--------------------------|------|
| 1 | `dsh-better-sidebar` | **0.14.0** | [github:omdsh-dev/DSH-better-sidebar](https://github.com/omdsh-dev/DSH-better-sidebar)（commit `6c89151`） | `~/.dsh/profiles/desktop` | VSCode 风格的右侧边栏工作台：文件管理 / CodeMirror 编辑器 / 内嵌浏览器 / 真实终端（xterm.js + node-pty）/ Git 面板 / 后台任务页，并对外暴露 `ctx.betterSidebar` 服务供其他插件注册侧边栏 Tab 与文件预览器 |

截至目前，本机通过 `dsh plugin add` 安装的第三方插件**共 1 个**（desktop profile）。web profile 未安装任何第三方插件。

## 目录结构

```
dsh-plugins-backup/
├── README.md                        # 本文件：插件清单与恢复方法
├── plugins.json                     # 机器可读的插件清单
└── dsh-better-sidebar/              # 插件完整快照（源码 src/ + 构建产物 lib/ + 配置）
    ├── package.json                 # 插件元数据（版本、依赖、dsh 配置）
    ├── cordis.patch.yml             # 插件的 cordis 补丁层
    ├── README.md / README_EN.md     # 官方说明文档（中/英）
    ├── LICENSE                      # MIT
    ├── src/                         # TypeScript 源码
    ├── lib/                         # 构建产物（含 6.7MB 的 mermaid 打包文件）
    └── scripts/                     # 安装脚本
```

## 安装信息快照（本机）

- DSH 配置根目录（harness home）：`~/.dsh`
- 已安装插件的 profile：`desktop`
- profile 中 `package.json` 的依赖声明：

  ```json
  {
    "dependencies": {
      "dsh-better-sidebar": "github:omdsh-dev/DSH-better-sidebar"
    },
    "dsh": {
      "profile": {
        "bundles": [
          "@deepseek-ai/dsh-base",
          "@deepseek-ai/dsh-web-app",
          "dsh-better-sidebar"
        ]
      }
    }
  }
  ```

- 锁定的安装来源（`pnpm-lock.yaml`）：
  `https://codeload.github.com/omdsh-dev/DSH-better-sidebar/tar.gz/6c891514b544b6e2da51fdab2eb3436cc02da246`（即上述 commit 的 tarball）
- 相关全局设置（`~/.dsh/settings.yaml`）：

  ```yaml
  dsh-better-sidebar:
    tabsEnabled:
      browser: true
  ```

## 如何恢复（在新机器上）

```bash
# 1. 安装 DSH 后，把本仓库克隆到任意位置
git clone https://github.com/Chun21/dsh-plugins-backup.git

# 2. 用 dsh CLI 重新安装插件（推荐，会拉取最新版）
dsh plugin --profile desktop add github:omdsh-dev/DSH-better-sidebar

# 3. 或者：直接使用本仓库中的快照（版本固定为 0.14.0 / commit 6c89151）
cp -r dsh-plugins-backup/dsh-better-sidebar ~/.dsh/profiles/desktop/node_modules/
# 然后在 ~/.dsh/profiles/desktop/package.json 的 dependencies 中加入：
#   "dsh-better-sidebar": "github:omdsh-dev/DSH-better-sidebar"
# 并把 "dsh-better-sidebar" 加进 dsh.profile.bundles 列表，重启 DSH Desktop。
```

## 版权说明

- `dsh-better-sidebar` 遵循其自带的 MIT License（见 `dsh-better-sidebar/LICENSE`），版权归原作者 [omdsh-dev](https://github.com/omdsh-dev) 所有。本仓库仅作个人备份。
