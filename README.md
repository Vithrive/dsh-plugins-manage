# dsh-plugins-manage

管理我在 [DeepSeek Harness (DSH)](https://github.com/deepseek-ai/deepseek-harness) 中安装与使用的插件（plugin / bundle）。

本仓库记录我目前使用的**第三方插件**的 GitHub / npm 来源、简介与安装方式，分类方式参考 [awesome-dsh-plugin](https://github.com/awesome-dsh-plugin/awesome-dsh-plugin)。

## 我的Plugins管理规则

自研（自己生成）的插件统一按以下规范管理，避免目录散乱。

### 两个规范位置

| 位置 | 用途 |
|---|---|
| `~/.dsh/plugins/` | 开发 / 验证阶段；npm 上传失败或无法下载时的暂存区 |
| `~/.dsh/profiles/web/node_modules/` | 安装后的最终位置（统一管理） |

### 标准流程

1. 在 `~/.dsh/plugins/<插件名>/` 下生成并开发插件；
2. 本地验证通过；
3. 上传到 npm；
4. 安装：`dsh plugin --profile web add <npm包名>`；
5. 最终由 `~/.dsh/profiles/web/node_modules/` 统一管理。

### 异常情况

- **验证阶段**：暂存于 `~/.dsh/plugins/`，不安装；
- **npm 上传失败 / 无法下载**：继续留在 `~/.dsh/plugins/`，可临时用本地路径或 tarball 安装：
  ```bash
  dsh plugin --profile web add ~/.dsh/plugins/<插件名>
  dsh plugin --profile web add ~/.dsh/plugins/<插件名>/<name>-<ver>.tgz
  ```

> 除上述两个位置外，不要在其它地方散落插件源码（例如之前的 `~/.dsh/plugin-market/` 已合并进 `~/.dsh/plugins/`）。

### 自研插件清单

#### @vithrive/dsh-plugin-market（0.1.1）

插件市场标签页（Settings → Plugins），从 deepseek-harness-plugin.com 目录列出可安装的 dsh 插件，一键安装。

- 状态：已发布 npm（`@vithrive` scope）；原 `dsh-plugin-market` 名称被占用，故改名
- 安装来源：本地 tarball（`file:~/.dsh/plugins/dsh-plugin-market/vithrive-dsh-plugin-market-0.1.1.tgz`）

```bash
dsh plugin --profile web add @vithrive/dsh-plugin-market
```

#### dsh-about-settings-pinned（0.1.0）

在设置侧边栏最底部固定一个「关于」页，显示当前 dsh 版本与安装路径。

| 项 | 值 |
|---|---|
| npm | https://www.npmjs.com/package/dsh-about-settings-pinned |
| 当前使用版本 | `0.1.0` |

```bash
dsh plugin --profile web add dsh-about-settings-pinned
```

#### dsh-third-party-plugins-manage（0.2.1）

第三方插件管理标签页（Settings → Plugins）：列出 profile 的 `node_modules` 下安装的插件，提供启/停用、更新检测与删除。

- 状态：已发布 npm（0.2.1）
- 安装来源：npm

```bash
dsh plugin --profile web add dsh-third-party-plugins-manage
```

#### dsh-drop-caret（0.2.1）

把文件/文件夹拖进对话输入框，在拖放点对应的精确光标位置插入文件引用（文件夹自动递归展开）。

| 项 | 值 |
|---|---|
| npm | https://www.npmjs.com/package/dsh-drop-caret |
| 当前使用版本 | `0.2.1` |

```bash
dsh plugin --profile web add dsh-drop-caret
```

#### dsh-open-links（0.1.1）

把对话中的外部 http/https 链接点击转发给外层宿主（如 VS Code Webview），由宿主在默认浏览器打开，避免 iframe 内部导航卡死。

| 项 | 值 |
|---|---|
| npm | https://www.npmjs.com/package/dsh-open-links |
| 当前使用版本 | `0.1.1` |

```bash
dsh plugin --profile web add dsh-open-links
```

#### dsh-vscode-selection（0.1.0）

接收 VS Code 扩展发送的代码选中内容，并插入到对话输入框。

| 项 | 值 |
|---|---|
| npm | https://www.npmjs.com/package/dsh-vscode-selection |
| 当前使用版本 | `0.1.0` |

```bash
dsh plugin --profile web add dsh-vscode-selection
```

---

## 通用安装方式

所有插件均安装到 `web` profile（即 `dsh web` 所使用的 profile）：

```bash
# 安装插件到 web profile
dsh plugin --profile web add <package>

# 重启 dsh web 使插件生效
dsh web
```

> 说明：`dsh plugin` 会把参数转发给 profile 目录（`~/.dsh/profiles/web`）下的 pnpm 完成安装；安装后需重启 `dsh web`，新的 client bundle 才会被加载。

---

## 插件清单（第三方插件）

### UI Enhancements（界面增强）

#### [@linxin666/dsh-web-ui-all](https://github.com/zhu1090093659/dsh-web-ui)（0.2.4）

DSH Web UI 全家桶聚合插件：一键安装 task-board / git-graph / pet / remote-web-ui / web-ui-settings / skin-center / community-plugins 等（含 dsh-better-sidebar）。内置子插件 `husky-dsh-pet` 已停用。

| 项 | 值 |
|---|---|
| GitHub | https://github.com/zhu1090093659/dsh-web-ui |
| npm | https://www.npmjs.com/package/@linxin666/dsh-web-ui-all |
| 当前使用版本 | `0.2.4`（npm latest `0.2.5`） |

```bash
dsh plugin --profile web add @linxin666/dsh-web-ui-all
```

#### [dsh-better-sidebar](https://github.com/omdsh-dev/DSH-better-sidebar)（0.14.0）

类 VS Code 的右侧边栏（资源管理器 / 编辑器 / 终端 / Git / 浏览器），按会话隔离；对外提供服务，供其他插件注册侧边栏标签页和文件查看器。

| 项 | 值 |
|---|---|
| GitHub | https://github.com/omdsh-dev/DSH-better-sidebar |
| npm | https://www.npmjs.com/package/dsh-better-sidebar |
| 当前使用版本 | `0.14.0` |

- 备注：不再作为独立依赖，由 `@linxin666/dsh-web-ui-all` 聚合包内置

```bash
dsh plugin --profile web add dsh-better-sidebar
```

### Workflow & Automation（工作流与自动化）

#### [@nanmicoder/dsh-agent-teams](https://github.com/NanmiCoder/dsh-agent-teams)（0.1.8）

AgentTeams 多智能体团队协作：队长 / 成员 / 带依赖的任务 / 消息，Web GUI 树状监控。

| 项 | 值 |
|---|---|
| GitHub | https://github.com/NanmiCoder/dsh-agent-teams |
| npm | https://www.npmjs.com/package/@nanmicoder/dsh-agent-teams |
| 当前使用版本 | `0.1.8` |

```bash
dsh plugin --profile web add @nanmicoder/dsh-agent-teams
```

### Memory（记忆）

#### [dsh-memory-evolve](https://github.com/csyangwen/dsh-memory-evolve)（0.1.0）

分层记忆（全局 / 用户 / 项目 / 分支 / 每日）+ 自我进化（经验沉淀 + 技能自动创建）+ 技能管理、待办管理、CLI 调度、临时便签，带 WebUI。

| 项 | 值 |
|---|---|
| GitHub | https://github.com/csyangwen/dsh-memory-evolve |
| 当前使用版本 | `0.1.0` |

```bash
dsh plugin --profile web add github:csyangwen/dsh-memory-evolve
```

### Just for Fun（趣味）

#### [dsh-answer-pet](https://github.com/Nanki-nn/dsh-answer-pet)（0.6.0）— 🔴 已停用

可扩展的回答状态宠物框架：支持宠物主题、多会话进度、模型轨迹和工具调用。

| 项 | 值 |
|---|---|
| GitHub | https://github.com/Nanki-nn/dsh-answer-pet |
| 当前使用版本 | `0.6.0` |
| 状态 | 🔴 已停用（disabled） |

```bash
dsh plugin --profile web add dsh-answer-pet
```

---

## 参考

- [awesome-dsh-plugin](https://github.com/awesome-dsh-plugin/awesome-dsh-plugin) — DSH 插件精选列表（分类方式参考）
- [deepseek-harness](https://github.com/deepseek-ai/deepseek-harness) — DSH 官方仓库
