# EDT-Pages.github.io

本项目维护 EdgeTunnel 管理面板静态界面，由 GitHub Pages 发布。Worker 源码和部署 ZIP 在相邻的本地项目目录 EdgeTunnel-ExitProxy 中维护；两个项目独立版本控制、独立发布，不复制对方的源码。

## 配套 Worker

- Worker 项目：EdgeTunnel-ExitProxy
- 运行项目：Cloudflare Pages magictunnel
- 管理界面：Worker 从本项目的 Pages 地址读取 admin/index.html
- 配置和日志 API：在生产 Worker 域名下由 Worker 提供，配置保存在 Worker KV
- ALPN 控件按 Worker /version 与配置字段决定是否显示。当前 Worker Version 2026-09-22 20:01:17 满足现有 ALPN 门槛。
- 当前面板没有订阅转换 EXPAND 开关；Worker 默认 EXPAND=true，因此 Worker-only 更新不要求发布面板。需要增加开关时，面板必须同时实现读取、保存和重置。

## 发布约定

- 只改面板时，更新本仓库并推送 main；GitHub Actions 发布后，在 Worker 域名下验证 /admin。
- 只改 Worker 时，在 EdgeTunnel-ExitProxy 打包并上传 Worker ZIP，不必推送本仓库。
- Worker API 或配置契约有变化时，先发布兼容的 Worker，再发布面板。
- 当前 Pages 工作流会发布整个仓库中的跟踪文件。不要提交生产配置、凭据或运行日志；配置和日志由 Worker API 返回。admin/config.json 与 admin/log.json 仅可作为脱敏本地样例，须保持未跟踪。

详细关系、兼容点和发布顺序见 docs/项目关联与发布.md。
