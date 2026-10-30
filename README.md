# 乔木 RSS · qiaomu-rss-dsh

**中文** · [English](#english)

**让订阅变成真正读进去的内容。** 在 Harness 里发现值得关注的作者，读原文或中文版本，再带着当前文章向 AI 追问。

[下载安装](https://github.com/joeseesun/qiaomu-rss-dsh/releases/latest) · [反馈问题](https://github.com/joeseesun/qiaomu-rss-dsh/issues)

![实际文章阅读：频道列表、阅读版本与正文](docs/screenshots/reading.png)

> 真实截图：独立 Harness Web profile，公开文章与服务已有的改写版本；没有合成 AI 回答。[截图说明](docs/SCREENSHOTS.md)

- **少切几个窗口：** 订阅列表、文章正文、原生 AI 对话在同一工作区。
- **外文文章也能顺畅读：** 在已有原文、译文和改写之间切换；缺失版本可交给已配置的模型生成。
- **从“看过”走向“看懂”：** 让伴读带着文章上下文继续解释、比较与追问。
- **订阅由你决定：** 发现博客与播客、添加 RSS/Atom 地址，用 OPML 迁移订阅。

Read RSS inside DeepSeek Harness and discuss the current article in its native AI conversation.

这是公开源码的社区插件，并非 DeepSeek 官方维护或背书。预构建安装包见 [GitHub Releases](https://github.com/joeseesun/qiaomu-rss-dsh/releases)；目前不发布 npm 包。v0.9.2 已在 DeepSeek Harness 0.2.1-rc.3 的隔离 Web profile 中验证安装、阅读与原生伴读挂载。

## 能做什么

| 功能 | 使用方式 |
| --- | --- |
| 乔木精选与个人订阅 | 从左上角搜索并切换频道，自动加载该频道的新文章；在探索页添加 RSS/Atom 源，导入或导出 OPML |
| 读者社区 | 「乔木精选」之外的独立分组，收录读者提交的链接，可按 YouTube / B 站 / 公众号 / 文章筛选；站点隐藏该频道后同步消失 |
| 阅读文章 | 切换原文、译文和乔木改写；支持未读、收藏、搜索与媒体内容 |
| AI 伴读 | 点击文章工具栏的魔法棒，或选中正文，右侧直接打开 Harness 原生对话；默认工作区自动连接当前文章，选段引用内嵌在输入框内，可展开或移除；翻译、解释、概括默认只处理选段，文章作为参考上下文 |
| 海外播客原文 | 搜索节目、浏览单集并获取已有完整转写；导入后可阅读、翻译和伴读 |
| 链接收录与改写（实验室） | 在设置中启用并验证邀请码，粘贴链接或右键正文链接提交；在「申请收录」查看进度、重试失败申请，完成后打开中文改写与 AI 伴读 |
| 插件设置 | 调整阅读外观和乔木服务地址；用弹窗编辑订阅、重命名或取消分组，管理 OPML 与快捷提示词，并查看关于与打赏信息 |
| Agent 工具 | 提供频道、文章、搜索、订阅、刷新和阅读版本相关的八个 `rss_*` 工具 |

## 链接收录与改写

在「插件设置 → 实验室」启用链接收录，输入邀请码并点击「验证并保存」，随后打开「申请收录」。粘贴网页地址提交，或右键文章中的链接选择「申请收录改写」。完成的申请可直接打开阅读，失败的申请可重试。任务在 Host 保存；重启会恢复进度检查，完成或失败时在 RSS 面板通知。没有未完成任务时不持续查询服务器。

链接会发送到设置中的乔木服务，生成的改写公开收录。此功能是网页收录和 AI 改写，与「海外播客原文」提供的已有逐字稿不同。实验室默认关闭。邀请码与实例访问密钥保存在本机插件数据中，不返回通用设置，不提供 Agent 提交工具；管理员管理功能本版未迁移。

![Harness 实验室：验证邀请码、开启收录和查看申请](docs/screenshots/link-collection.png)

## 真实界面

<details>
<summary>查看已合并的桌面版 AI 伴读实拍</summary>

![真实 AI 伴读：文章与原生对话](docs/screenshots/ai-companion.jpg)

此前桌面构建实拍：打开 Planet Money 文章后，发送「概括要点」，右侧返回对应文章的概括。该截图由此前的 [PR #6](https://github.com/joeseesun/qiaomu-rss-dsh/pull/6) 合入；该截图为此前版本；v0.6.0 的选段翻译已在 Desktop 原生对话中验证；v0.7.0 新功能在隔离 Web profile 中验证。

</details>

切换频道时先显示已缓存文章，再自动拉取该频道的新内容；刷新按钮仍可手动强制更新。切换文章时，阅读区用轻量骨架显示加载状态。默认阅读版本为「乔木改写」，仅在当前文章有内容时生效，缺失时自动选择其他已有版本或原文；手动选择缺失版本仍可调用 Harness 生成。文章与伴读之间的分割线可拖动，也可用方向键微调、双击复位。打开伴读时文章列表保持可见，文章左上角也可打开频道列表。伴读输入框上方的快捷提示词可横向滚动点选并直接发送；末端的 + 可直达设置新增提示词。已有手写草稿时不会覆盖或误发。本机个人提示词保存在插件的浏览器存储中，可在设置中编辑。探索订阅包含来自原版乔木 RSS 目录的 73 个播客 RSS 源；订阅后可使用文章中的音频附件播放。插件不提供 Obsidian 式笔记、划线保存或日记写入。

## 找到下一篇想读的内容

![订阅发现：搜索作者、播客或 RSS 地址](docs/screenshots/discovery.png)

打开「探索订阅」，找到作者并订阅；也可以直接输入 RSS 地址。首次使用无需导入旧数据，乔木精选可直接阅读。AI 伴读与缺失版本生成需要宿主模型配置，普通阅读不需要模型密钥。

## 安装

上游 v0.9.2 的版本声明支持 DeepSeek Harness 0.2.1-rc.2 / 0.2.1-rc.3。本 [fork](https://github.com/cpp-wen/qiaomu-rss-dsh/tree/codex/rc5-compatibility) 的 `0.9.3-rc5.1` 精确增加 `0.2.1-rc.5`，不豁免版本检查。

在源码目录构建安装包：

```bash
npm ci
npm run check
npm pack
```

**Desktop rc.5：** 可以使用应用自带的官方 CLI 安装。macOS 的入口如下（普通 PATH 中的其他版本 `dsh` 未必支持桌面 profile）：

```bash
"/Applications/DeepSeek Harness.app/Contents/Resources/runtime/cli/bin/dsh" plugin --profile desktop add "$PWD/qiaomu-rss-dsh-0.9.3-rc5.1.tgz"
```

也可以在桌面应用的插件管理器中填写安装包的本机绝对路径。

**Web：** 使用官方 CLI 安装：

```bash
dsh plugin --profile web add "$PWD/qiaomu-rss-dsh-0.9.3-rc5.1.tgz"
```

安装后按宿主提示重载或重启，在侧边栏打开「乔木 RSS」。AI 伴读使用 Harness 已配置的模型与账号。已有阅读数据继续使用原来的插件存储。

rc.5 已验证隔离安装、启动、真实文章阅读与原生伴读面板挂载；未发送付费模型请求。完整验证范围见 [rc5 兼容性记录](docs/RC5-COMPATIBILITY.md)。

## 开发

需要 Node.js 22 或更高版本，以及已安装的 DeepSeek Harness。克隆后执行：

```bash
git clone https://github.com/joeseesun/qiaomu-rss-dsh.git
cd qiaomu-rss-dsh
npm ci
npm run check
npm pack
```

`src/` 是源码；`lib/` 是随 Git 仓库提交的宿主与客户端构建产物，供 DSH bundle 加载。修改源码后请重新构建，并一并提交更新后的 `lib/`。包名 `qiaomu-rss-dsh` 必须与 `cordis.patch.yml` 中的 `name` 保持一致。

此前版本已在本地 Desktop profile 验证读取、伴读和可调分割线，并通过隔离 Web profile 的安装、配置和启动检查；本轮已验证 Desktop 中选段引用内嵌、保留输入草稿、移除引用，并实际发送「翻译」确认只翻译选段。隔离 Web 的已有文章和订阅发现截图来自 v0.5.2。详见 [发布验证](docs/RELEASE-VALIDATION.md)。`private: true` 仅阻止误发 npm，不限制 GitHub 源码或 Release 下载。正式使用时请安装 Release 包；从 GitHub 源码构建适合参与开发。

升级时安装新版本包并重启同一 profile。暂时停用可在 Harness 插件管理中禁用 RSS；卸载前请通过 OPML 导出订阅，阅读状态需要另外备份。

## 数据与来源

- 订阅与阅读状态保存在 Harness home 的 `storages/qiaomu-rss/data.json`，不在本仓库。升级时不会清空旧数据。
- 乔木精选读取 [乔木 AI RSS](https://github.com/joeseesun/qiaomu-ai-rss) 的公开接口；个人订阅由插件抓取。
- 内置独立博客源清单来自 [chinese-independent-blogs](https://github.com/timqian/chinese-independent-blogs)，其 MIT 声明保留在 [`vendor/chinese-independent-blogs/LICENSE`](vendor/chinese-independent-blogs/LICENSE)。
- 播客 RSS 推荐地址来自 [乔木 AI RSS 的源目录](https://github.com/joeseesun/qiaomu-ai-rss/blob/main/src/data/tidings.json)；第三方源的可用性和全文/音频内容由各发布方决定。
- 「探索订阅 → 海外播客原文」可搜索 [乔木 Podscribe API](https://api.qiaomu.ai/podscribe/docs) 收录的海外节目，按节目浏览单集并获取完整原文转写。已获取的单集出现在「海外播客原文」频道，可继续翻译、改写或在 AI 伴读中引用。覆盖范围随上游公开目录变化；接口不可用或无转写时会显示错误，不会生成虚构原文。
- AI 伴读使用 DeepSeek Harness 当前可用的模型与原生会话；模型服务的配置与费用由 Harness 管理。

问题与改进建议请通过 [GitHub Issues](https://github.com/joeseesun/qiaomu-rss-dsh/issues) 提交。本项目采用 [GPL-3.0-only](LICENSE) 许可。

---

<a id="english"></a>

## English

The [live desktop screenshots](#真实界面) show a real feed, the rewritten reading view, subscription discovery, and an article-specific native AI response from a locally installed development build. [Download v0.9.2](https://github.com/joeseesun/qiaomu-rss-dsh/releases/tag/v0.9.2) or follow the install steps above.

Qiaomu RSS brings curated and personal RSS/Atom feeds into DeepSeek Harness. Read the original, translated, or rewritten article; manage unread items and favorites; import/export OPML; and open a native Harness AI conversation beside the article with its reading context attached. The companion opens directly in the default workspace. The article/chat divider is resizable.

This is an open-source community plugin, not maintained or endorsed by DeepSeek. The fork build `0.9.3-rc5.1` adds exactly DeepSeek Harness `0.2.1-rc.5` to the upstream rc.2/rc.3 compatibility range. Build with `npm ci`, `npm run check`, and `npm pack`. On Desktop rc.5, use the application's bundled CLI (`/Applications/DeepSeek Harness.app/Contents/Resources/runtime/cli/bin/dsh` on macOS) with `plugin --profile desktop add <absolute-tarball-path>`, or use the desktop plugin manager. The bundled CLI explicitly enables Desktop profile management; a different `dsh` on PATH may not. Web users can run `dsh plugin --profile web add /absolute/path/to/qiaomu-rss-dsh-0.9.3-rc5.1.tgz`. Isolated rc.5 installation, startup, real article reading and native AI-companion panel mounting were verified. No paid model request was sent. See [validation details](docs/RC5-COMPATIBILITY.md).

Reading data lives in the user's Harness home under `storages/qiaomu-rss/data.json`, outside this repository. The curated feed uses the public [Qiaomu AI RSS](https://github.com/joeseesun/qiaomu-ai-rss) API. AI conversations use the host's configured model and account. Obsidian note, highlight-saving, and daily-note features are intentionally absent. Source is licensed under [GPL-3.0-only](LICENSE); the bundled blog list retains its separate MIT notice.
