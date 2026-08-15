# dsh-plugins-manage

管理我在 [DeepSeek Harness (DSH)](https://github.com/deepseek-ai/deepseek-harness) 中安装与使用的插件（plugin / bundle）。

本仓库记录我目前使用的**第三方插件**的 GitHub / npm 来源、简介与安装方式，分类方式参考 [awesome-dsh-plugin](https://github.com/awesome-dsh-plugin/awesome-dsh-plugin)。

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

## 插件清单

### UI Enhancements（界面增强）

#### [dsh-better-sidebar](https://github.com/omdsh-dev/DSH-better-sidebar)

类 VS Code 的右侧边栏（资源管理器 / 编辑器 / 终端 / Git / 浏览器），按会话隔离；对外提供服务，供其他插件注册侧边栏标签页和文件查看器。

| 项 | 值 |
|---|---|
| GitHub | https://github.com/omdsh-dev/DSH-better-sidebar |
| npm | https://www.npmjs.com/package/dsh-better-sidebar |
| 当前使用版本 | `0.12.2` |

```bash
dsh plugin --profile web add dsh-better-sidebar
```

---

### Tools & Capabilities（工具与能力）

#### [@anionex/dsh-vision-toolkit](https://github.com/Anionex/dsh-vision-toolkit)

DeepSeek Harness 原生集成的视觉工具包（[agent-vision-toolkit](https://github.com/Anionex/agent-vision-toolkit) 的 DSH 版本）：图像问答、OCR、grounding、UI 还原、像素差异对比、Artifacts 与 Web UI，让纯文本模型也能处理视觉任务。

| 项 | 值 |
|---|---|
| GitHub | https://github.com/Anionex/dsh-vision-toolkit |
| npm | https://www.npmjs.com/package/@anionex/dsh-vision-toolkit |
| 主页 | https://agent-vision.anionex.me |
| 当前使用版本 | `0.1.7` |

```bash
dsh plugin --profile web add @anionex/dsh-vision-toolkit
```

---

### 自有 / 本地插件（备注，非第三方）

以下为本地自建、暂无公开 GitHub 仓库的插件，一并记录以备参考：

#### dsh-plugin-market（本地 0.1.0）

插件市场标签页（Settings → Plugins），从 npm registry 列出可安装的 dsh 插件，并把精选插件置顶。

- 安装来源：本地 tarball（`file:~/.dsh/plugin-market/dsh-plugin-market-0.1.0.tgz`）
- 备注：npm 上同名包 `dsh-plugin-market`（1.3.0）是另一个项目，请勿混淆

```bash
dsh plugin --profile web add C:/Users/admin/.dsh/plugin-market
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

---

## 参考

- [awesome-dsh-plugin](https://github.com/awesome-dsh-plugin/awesome-dsh-plugin) — DSH 插件精选列表（分类方式参考）
- [deepseek-harness](https://github.com/deepseek-ai/deepseek-harness) — DSH 官方仓库
