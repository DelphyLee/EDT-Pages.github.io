# EDT-Pages.github.io

本项目维护 EdgeTunnel 管理面板静态界面，由 GitHub Pages 发布。Worker 源码和部署 ZIP 在相邻的本地项目目录 EdgeTunnel-ExitProxy 中维护；两个项目独立版本控制、独立发布，不复制对方的源码。

## 配套 Worker

- Worker 项目：EdgeTunnel-ExitProxy
- 运行项目：Cloudflare Pages magictunnel
- 管理界面：Worker 从本项目的 Pages 地址读取 admin/index.html
- 配置和日志 API：在生产 Worker 域名下由 Worker 提供，配置保存在 Worker KV
- 上游基线：已同步至 `EDT-Pages/EDT-Pages.github.io` `upstream/main`（`aaab6db`，2026-11-10），保留并融合了本地 PROXYIP 池、预设域名下拉、获取更多 PROXYIP（含公司归属）及按域名出口规则。
- ALPN 与 XMUX 控件按 Worker /version 与配置字段决定是否显示。当前配套 Worker Version `2026-11-10 23:26:46`（`20261110232646`）同时满足 ALPN（`>= 20260904162413`）与 XMUX 连接复用（`>= 20261110232646`）门槛。
- 订阅转换 `EXPAND`（展开规则全文）开关已随上游合入面板，支持读取、保存与重置。

## 发布约定

- 只改面板时，更新本仓库并推送 main；GitHub Actions 发布后，在 Worker 域名下验证 /admin。
- 只改 Worker 时，在 EdgeTunnel-ExitProxy 打包并上传 Worker ZIP，不必推送本仓库。
- Worker API 或配置契约有变化时，先发布兼容的 Worker，再发布面板。
- 当前 Pages 工作流会发布整个仓库中的跟踪文件。不要提交生产配置、凭据或运行日志；配置和日志由 Worker API 返回。admin/config.json 与 admin/log.json 仅可作为脱敏本地样例，须保持未跟踪。

详细关系、兼容点和发布顺序见 docs/项目关联与发布.md。
