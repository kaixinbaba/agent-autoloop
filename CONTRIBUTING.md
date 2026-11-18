# 参与贡献

欢迎提交可复现的问题、文档修正、插件和通用能力改进，中文或英文都可以。

## 去哪里交流

- [本仓库 Issues](https://github.com/kaixinbaba/agent-autoloop/issues)：可以复现的故障、功能建议、使用问答与实践分享。本 fork 与[上游](https://github.com/KKKKhazix/agent-autoloop)分开维护，相关改动先在这里立项；能做的由维护者修复，修复提交会署上报告者。
- 本仓库尚未开启 Discussions，不把本 fork 的问题默认转给上游。
- 安全问题按 [安全说明](SECURITY.md) 联系维护者，不在公开讨论中披露利用细节。

## 贡献范围

新 Agent、事件插件和通道接在插件层；完整业务流程可以做成场景模板。先看 [插件开发说明](docs/plugins.md) 和 [现有场景](README.md#拿来即用的场景模板)，避免重复实现。

内核保持零运行时依赖，不连接外部产品。总览页、工作流画布和其他界面属于独立客户端，不放进这个仓库。改协议或核心流程前，先说明具体场景和兼容影响；维护约定见 [AGENTS.md](AGENTS.md)，协议见 [docs/protocol.md](docs/protocol.md)。

## 提交改动

1. 先开本仓库 Issue，写清计划，待本人确认后，从最新的远端 `main` 在独立 worktree 创建 `agent/issue-编号` 分支；主目录保留在 `main`。外部贡献者使用 Fork，同样先对齐 Issue 与计划。tag 只用于发布（`v1.2.3`）。
2. 使用 Node.js 24 或更新版本，运行 `npm ci`。一次 PR 解决一个问题，同步更新受影响的中英文说明、示例和配置。
3. 修 bug 先写能复现它的失败测试，测试文件开头说明防止什么失败。纯文档、模板或小范围可逆改动，不补照着实现抄的测试。
4. 提交前运行 `npm run test:quick`、`npm run typecheck`、`npm run format:check`。改了 `kernel/`、`protocol/`、`sim/` 时用 `npm test`，它多跑完整模拟和穷举。涉及日志、到期表或并发时，再运行 `npm run test:nightly`。Windows 原生检查用 `npm run test:windows`。各平台的 CI 与安装冒烟检查见 [检查范围](AGENTS.md#怎么改)。
5. 向 `main` 提交 draft PR，正文写 `Fixes #编号`（例如本次为 `Fixes #2`），说明问题、改后的行为、验证结果和兼容影响。计划确认只授权开发与原生只审查，不授权合并或上线；原生流程在当前提交审查通过后转正式，再核对同一提交最新的 Ubuntu、macOS 和 Windows 三项检查，等待本人在当前成果卡同意上线后由中台合并。不直接推送或本地合并 `main`，不开自动合并，不跳过闸门。维护者把独立审查和必要的真机验证记在 PR。外部 PR 请勾选“Allow edits by maintainers”，需调整时维护者通常直接在你的分支上改好；首次外部 PR 的 CI 可能需要维护者允许运行。

测试使用临时 `AGENT_AUTOLOOP_HOME`、随机端口、本地假 HTTP 和假通知命令。不要连接真实业务数据库、发送消息，或给已在线的飞书应用再开事件监听。真实交付脚本会创建和删除指定测试仓库，只在用户明确要求时运行。

不要提交密钥、带权限的卡片链接、完整配置、数据库、运行输出或同事资料。问题中的日志和截图也要先脱敏。代码按 [MIT 许可证](LICENSE) 提交。

本 fork 的安装与更新跟随 `release` 分支，不是 `main` 或上游标签，见 [INSTALL.md](INSTALL.md)。合并 `main` 与发布到 `release` 是两件事：目前没有核实过的自动晋级流程，文档合并不代表已升级引擎；推进 `release`、打 tag 和更新现有安装须另行授权。tag 版本规则仍见[协议](docs/protocol.md#版本与兼容)，不另设长期支持承诺。
