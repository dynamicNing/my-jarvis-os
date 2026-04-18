# core/

跨 agent 的系统能力，对应 `docs/constitution.md` 四层架构里的 **Core**。

| 子目录 | 职能 |
| --- | --- |
| `routing/` | 任务分派、agent 选择、冲突仲裁 |
| `memory/` | Fact memory（长期）与 Working memory（短期） |
| `permissions/` | 风险分级、审批策略、白名单 |
| `workflows/` | 默认路由模式 A/B/C/D 的编排 |
| `audit/` | 审计日志、可追溯性 |

实现可以是脚本、配置、schema —— 但任何"决策性"的规则必须落到 schema/配置文件，而不是只藏在 prompt 里。
