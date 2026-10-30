# DeepSeek Harness rc5 兼容性记录

日期：2026-10-30。目标宿主：官方 macOS DeepSeek Harness `0.2.1-rc.5`；插件版本：`qiaomu-rss-dsh@0.9.3-rc5.1`。

## 变更

上游 `0.9.2` 的 `engines.dsh` 和 DSH peer 范围只包含 `0.2.1-rc.2` / `0.2.1-rc.3`，因此 rc5 的插件安装会被宿主兼容性门禁拒绝。本 fork 将以下声明扩展为显式的三个预发布版本：

```text
0.2.1-rc.2 || 0.2.1-rc.3 || 0.2.1-rc.5
```

`engines.dsh` 存在时，DSH 以该声明作为兼容性判断，peer 声明用于保持包元数据一致。此次没有放开任意未来版本，也没有改变 RSS 数据协议或宿主 API 调用。

## 已验证

- `npm ci` 完成，依赖审计无漏洞。
- `NODE_PATH="$PWD/node_modules" npm run check` 通过：构建、全部测试和 package 文件校验均通过。
- `npm pack` 生成 `qiaomu-rss-dsh-0.9.3-rc5.1.tgz`，包校验通过。
- 在临时 `DSH_HOME=/tmp/qmr-rc5-dsh` 中执行 `dsh plugin --profile web add <tgz>` 成功，pnpm 安装结果为 `qiaomu-rss-dsh 0.9.3-rc5.1`。
- 在同一临时 profile 执行 `dsh --profile web --dump-config`，输出包含 `qiaomu-rss-dsh` bundle 和 `qiaomu-rss` patch。
- 在同一临时 profile 执行 `dsh --profile web --no-open --host 127.0.0.1 --port 0`，服务成功监听随机本地端口；进程由 12 秒超时停止，日志没有插件加载错误。

- 在隔离 Web 界面打开真实文章，确认中文改写正文显示；打开 AI 伴读后，当前文章标题、原生输入框、模型选择器和快捷提示词均正常挂载。未发送模型请求。
- 当前 macOS rc.5 自带的 `dsh-desktop-host/lib/cli.js` 通过 `runCli({ manageDesktopProfile: true })` 支持 desktop profile。已使用应用内置 CLI 完成真实 Desktop 安装（2.7 秒），官方兼容检查通过，bundle 自动启用，原有 RSS 数据保持不变。
- 本次桌面 GUI 安装进程曾停滞并报 `Failed to fetch`；经官方取消恢复原配置后，改用上述官方 CLI 成功。未调用版本豁免，也未手改 profile manifest。

- 真实 Desktop 通过 OPML 预览并导入 23 个文章订阅，5 个分组成功保留；已核对持久化订阅的 URL、名称和分组与导入文件一致。订阅文件与个人阅读数据不包含在仓库中。

## 验证边界

这证明 rc5 的安装、配置合成和宿主启动路径可用，但不等于所有真实 RSS 源、登录态、外部服务、模型调用和浏览器交互均已端到端验收。日常 profile 的订阅和阅读缓存不在仓库中，也未写入仓库。

