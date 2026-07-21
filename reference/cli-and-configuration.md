# Reference · CLI 与配置速查

> **事实核验基线：2026-07-21**  
> 这是易版本漂移的 Reference，不应被当作永久不变的 CLI 全表。  
> 完整命令以官方 CLI Reference 为准。

## 1. 核心入口

```bash
hermes
hermes setup
hermes status
hermes doctor
hermes logs
```

## 2. Chat

单次 Query：

```bash
hermes chat -q "Hello"
```

选择 Profile：

```bash
hermes -p work chat -q "Hello"
```

恢复最近 Session：

```bash
hermes --continue
```

具体 Resume 参数：

```bash
hermes --resume <session>
```

## 3. Model

```bash
hermes model
```

优先使用交互式选择器，避免在长期文档写死具体 Model ID。

## 4. Auth / Credential Pool

```bash
hermes auth
hermes auth list
hermes auth add openrouter --api-key <KEY>
hermes auth add anthropic --type oauth
```

不要继续使用旧文档中的：

```text
hermes auth set
hermes auth login
```

除非当前安装版本的 Help 明确支持。

## 5. Gateway

```bash
hermes gateway setup
hermes gateway run                 # 前台
hermes gateway install             # 首次安装 systemd/launchd 服务
hermes gateway start
hermes gateway stop
hermes gateway restart
hermes gateway status
hermes gateway list
hermes gateway uninstall
```

日志使用独立入口：

```bash
hermes logs
```

## 6. Skills

用户 CLI：

```bash
hermes skills
```

常见管理能力包括：

```text
browse / search / install
inspect / list
check / update
audit / uninstall
```

Agent 内部 `skill_manage` Tool 与 Shell CLI 是不同 Surface。

## 7. Curator

```bash
hermes curator status
hermes curator run
hermes curator run --dry-run
hermes curator backup
hermes curator rollback
```

具体 Pin/Restore 等子命令以当前 `--help` 为准。

## 8. Profile

```bash
hermes profile list
hermes profile create work --clone
hermes profile use work
hermes profile show work
hermes profile export work -o work-backup.tar.gz
```

命名 Profile 可以获得命令 Alias，例如：

```bash
coder setup
coder chat
coder gateway start
```

## 9. Kanban

```bash
hermes kanban [--board <slug>] <action>
```

当前 Kanban 支持多个 Board：

```text
default board:  ~/.hermes/kanban.db
other boards:   ~/.hermes/kanban/boards/<slug>/kanban.db
active pointer: ~/.hermes/kanban/current
```

常见入口：

```bash
hermes kanban boards list
hermes kanban boards create <slug> --switch
hermes kanban create "Task title" --assignee <profile>
hermes kanban list
hermes kanban dispatch --dry-run
```

这是人类、脚本和 Cron 使用的 Surface；Agent Worker 使用 `kanban_*` Toolset，而不是 Shell 调用 CLI。

## 10. Security

```bash
hermes security audit
```

不要把一次审计结果理解成永久安全状态。

## 11. 配置

```bash
hermes config
hermes config get
hermes config set
```

配置 Schema 变化较快，修改前先：

```bash
hermes config --help
```

或查看官方 Configuration 页面。

## 12. 默认 Profile 与命名 Profile

稳定心智模型：

```text
default:
  $HERMES_HOME = ~/.hermes/

named profile:
  $HERMES_HOME = ~/.hermes/profiles/<name>/
```

每个 Profile 是自己的 `$HERMES_HOME`。

典型内容：

```text
config.yaml
.env
SOUL.md
memories/
sessions/
skills/
cron/
state DB
gateway state
```

## 13. Skills 路径

对任意 Profile，统一表达为：

```text
$HERMES_HOME/skills/
```

默认 Profile 通常解析为 `~/.hermes/skills/`；命名 Profile 通常解析为 `~/.hermes/profiles/<name>/skills/`。

不要把默认 Profile 的 `~/.hermes/skills/` 自动解释成“所有 Profile 的全局目录”。

需要跨 Profile 共享时，使用当前版本支持的显式机制，例如 External Skill Directories 或复制/分发策略。

## 14. Docker

交互：

```bash
docker run -it --rm \
  -v ~/.hermes:/opt/data \
  nousresearch/hermes-agent
```

Gateway：

```bash
docker run -d \
  --name hermes \
  --restart unless-stopped \
  -v ~/.hermes:/opt/data \
  -p 8642:8642 \
  nousresearch/hermes-agent gateway run
```

Dashboard 需要单独启用和暴露对应端口。

## 15. 如何验证文档里的命令

发布前对每个 Copy-paste Block：

```text
1. 在干净 Profile 运行
2. 检查 --help
3. 检查 exit code
4. 检查副作用
5. 记录测试版本或 commit
```

不要手工维护“CLI 全表”。

## 官方参考

- `https://hermes-agent.nousresearch.com/docs/reference/cli-commands`
- `https://hermes-agent.nousresearch.com/docs/user-guide/profiles`
- `https://hermes-agent.nousresearch.com/docs/user-guide/docker`
