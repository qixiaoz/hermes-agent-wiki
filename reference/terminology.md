# Reference · 术语与书写规范

> **适用范围**：本 Wiki 全部中文正文。代码标识符、CLI、文件名和官方产品功能名保持原样。  
> **事实核验基线**：2026-07-21。官方名称变化时，本页应优先更新。

## 1. 核心术语

| 统一写法 | 首次出现建议 | 不再使用/避免 |
|---|---|---|
| Hermes Agent | `Hermes Agent`，后文可简称 `Hermes` | HermesAgent、Hermes agent |
| Agent | `Agent（代理）`；讨论源码时保留 Agent | 智能体/代理随机混用 |
| Agent Runtime | `Agent Runtime（代理运行时）` | Agent OS（除非明确是比喻） |
| Agent Loop | `Agent Loop（代理循环）` | ReAct Loop（除非特指 ReAct） |
| Profile | `Profile（独立 $HERMES_HOME）` | 把 Profile 简化成身份、Workspace 或 Sandbox |
| Session | `Session（会话）` | Chat、Thread 与 Session 无区分 |
| Provider | `Provider（模型提供方）` | 把 Provider 与 Model 当同一概念 |
| Tool | `Tool（工具）` | 能力、插件、Skill 混用 |
| Toolset | `Toolset（工具集）` | Tool List（除非真的是列表） |
| Skill | `Skill（技能）` | Prompt、Tool 的同义词 |
| Memory | `Memory（持久记忆）` | 把完整 Session History 叫 Memory |
| Session Search | `Session Search（会话搜索）` | 长期语义记忆 |
| Subagent | 中文正文写“子代理（Subagent）”；官方英文拼写无连字符 | Sub-agent、Sub Agent |
| Worker | `Worker（工作进程）`；Kanban Worker 是完整 OS 进程 | 与 Subagent 混用 |
| Kanban | `Kanban（多代理协作看板）` | 把 Kanban 当作 Subagent 别名 |
| 多代理 | 中文叙述使用“多代理”；英文官方名或代码中保留 Multi-Agent | 多 Agent |
| Gateway | `Gateway（消息网关）` | Platform、Channel、Adapter 的同义词 |
| Platform Adapter | `Platform Adapter（平台适配器）` | Gateway Plugin（除非特指插件包装） |
| Surface | `Surface（交互面/入口）` | 把所有 Surface 都叫 Gateway |
| MCP | `MCP Client` / `MCP Server` | “MCP Tool”泛指整个 Server |
| ACP | `ACP（Agent Client Protocol）` | 与 MCP 混用 |

## 2. 路径与状态

- 环境变量、路径根统一写作 `$HERMES_HOME`。
- 默认 Profile：`$HERMES_HOME = ~/.hermes/`。
- 命名 Profile：通常为 `~/.hermes/profiles/<name>/`。
- Profile-local Skill：`$HERMES_HOME/skills/`。
- Profile-local Memory：`$HERMES_HOME/memories/`。
- Kanban Board 是机器级跨 Profile 状态，不跟随单个 Profile 的 `$HERMES_HOME`：默认 Board 为 `~/.hermes/kanban.db`。

## 3. CLI 与 Agent Tool

必须区分：

```text
Shell CLI:       hermes skills / hermes kanban / hermes memory
Agent Tool:      skill_manage / kanban_* / memory / session_search
Slash Command:   /model /kanban /curator
```

不得因为 Agent 有 `skill_manage(action="patch")`，就写成不存在的 `hermes skill patch` CLI。

## 4. 大小写

- 文件：`MEMORY.md`、`USER.md`、`SOUL.md`、`SKILL.md`、`AGENTS.md`。
- 代码 Symbol：`AIAgent`、`IterationBudget`、`delegate_task`。
- 协议：MCP、ACP。
- 英文功能名：Subagent、Kanban、Curator、Gateway。

## 5. 事实表达

推荐：

> 截至 2026-07-21，官方默认并发上限为……

避免：

> Hermes 永远只会……

易漂移内容必须携带日期、版本或 commit SHA。
