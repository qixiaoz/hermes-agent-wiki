# Contributing

感谢参与改进 Hermes Agent Wiki。

## 适合提交的内容

- 修正已经过时或不准确的 Hermes CLI、配置、架构和源码描述；
- 补充可复现的安装、部署、排错与安全实践；
- 改进 Mermaid 图、术语一致性和章节结构；
- 更新 Claude Code、OpenCode、OpenClaw 等竞品的官方事实基线。

## 事实要求

提交技术事实时，请优先提供以下来源之一：

1. Hermes 或相关项目的官方文档；
2. 官方仓库中的固定 commit SHA、模块路径和 Symbol；
3. 可复现的作者实测，并注明版本、日期和环境。

请区分：

- **官方事实**；
- **源码事实**；
- **作者实测**；
- **作者建议**。

避免使用没有版本边界的固定数量、源码行号和“唯一”“完全不支持”等绝对化表述。

## 修改检查

提交前请确认：

- Markdown 内部链接可解析；
- Mermaid 代码块语法完整；
- 命令示例来自当前 CLI，而不是 Agent 内部 Tool API；
- 中英文术语符合 [`reference/terminology.md`](./reference/terminology.md)；
- 易漂移事实已记录在 [`FACT-CHECK-CHANGELOG.md`](./FACT-CHECK-CHANGELOG.md)。
