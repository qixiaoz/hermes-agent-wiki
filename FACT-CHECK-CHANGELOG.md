# Fact Check Changelog · 2026-07-21

本轮以 Hermes Agent、Claude Code、OpenCode、OpenClaw 的官方文档为主要事实来源，对 Wiki v1 做了系统校准。

## 已修正的关键事实

### CLI 与安装

- 保留 `hermes chat -q`，确认 `-p / --profile` 用于选择 Profile。
- Credential Pool 统一使用 `hermes auth add/list/status/logout`。
- Gateway 后台服务流程改为 `hermes gateway install` → `start`；`run` 用于前台模式。
- Docker 首次配置改为 `nousresearch/hermes-agent setup`，持久数据挂载 `/opt/data`。
- 明确 8642 是 Gateway API/Health 端口，9119 是 Dashboard 端口。

### Profile 与路径

- Profile 统一定义为独立 `$HERMES_HOME`。
- Skills 与 Memory 路径统一写作 `$HERMES_HOME/skills/`、`$HERMES_HOME/memories/`。
- 删除“默认 Profile 的 `~/.hermes/skills` 自动全局共享给所有 Profile”的暗示。

### 子代理

- 官方拼写统一为 **Subagent**，不再使用 `Sub-agent`。
- 明确子代理不继承父会话历史，只接收 `goal` 与 `context`；只有最终摘要进入父上下文。

### Kanban

- 从“单个共享 kanban.db”升级为当前的 多 Board 模型。
- 默认 Board 保留 `~/.hermes/kanban.db`；其他 Board 位于 `~/.hermes/kanban/boards/<slug>/kanban.db`。
- 明确 Worker 是完整 OS 进程，并以分配给自己的 Profile 运行。
- 明确 Agent 使用 `kanban_*` Toolset，人类/脚本/Cron 使用 `hermes kanban` CLI、Slash Command 或 Dashboard。

### Curator

- 明确 Curator 主要管理后台 Self-improvement 标记为 agent-created 的 Skill。
- 手写、External Directory、前台按用户要求创建的 Skill 默认不受自动 Curator 管理。
- Hub-installed Skill 不被修改；Bundled Skill 只有受控归档路径。
- 加入 30 天 stale、90 天 archived 的当前默认值，并明确它们是带日期的版本事实。

### MCP 与竞品

- 明确 Claude Code 也支持 `claude mcp serve`；不再把 MCP Server 写成 Hermes 独有能力。
- Hermes 的差异改为：`hermes mcp serve` 暴露跨平台消息会话 Bridge。
- 加入 Claude Code Channels Research Preview，避免把 Claude Code 写成完全没有消息 Channel。
- 保留 Claude Code Agent Teams 为 Experimental 的状态说明。

## 术语统一

新增 [reference/terminology.md](./reference/terminology.md)，统一：

- Subagent / 子代理；
- Worker / 工作进程；
- Profile / `$HERMES_HOME`；
- Memory / Session Search / Skill；
- Gateway / Platform Adapter / Channel / Surface；
- MCP Client / MCP Server / ACP。

## 仍需定期复查

- Provider 与模型清单；
- Messaging Platform 数量；
- CLI 子命令和参数；
- Curator 默认阈值和管理范围；
- Kanban Dispatcher/Board 行为；
- Claude Code Channels、Agent Teams；
- OpenCode Server/ACP/Skills；
- OpenClaw Memory/Multi-agent/Gateway。

## 主要核验来源

- Hermes CLI Reference: https://hermes-agent.nousresearch.com/docs/reference/cli-commands
- Hermes Profiles: https://hermes-agent.nousresearch.com/docs/user-guide/profiles
- Hermes Memory: https://hermes-agent.nousresearch.com/docs/user-guide/features/memory
- Hermes Skills: https://hermes-agent.nousresearch.com/docs/user-guide/features/skills
- Hermes Curator: https://hermes-agent.nousresearch.com/docs/user-guide/features/curator
- Hermes Delegation: https://hermes-agent.nousresearch.com/docs/user-guide/features/delegation
- Hermes Kanban: https://hermes-agent.nousresearch.com/docs/user-guide/features/kanban
- Hermes Docker: https://hermes-agent.nousresearch.com/docs/user-guide/docker
- Hermes MCP: https://hermes-agent.nousresearch.com/docs/user-guide/features/mcp
- Claude Code MCP: https://code.claude.com/docs/en/mcp
- Claude Code Agent Teams: https://code.claude.com/docs/en/agent-teams
- Claude Code Channels: https://code.claude.com/docs/en/channels-reference
- OpenCode Docs: https://opencode.ai/docs/
- OpenClaw Docs: https://docs.openclaw.ai/
