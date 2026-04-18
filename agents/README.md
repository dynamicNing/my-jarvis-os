# agents/

每个子目录是一个 agent 的独立空间，承载职责说明、prompt、schema、代码与测试。

## 目录约定

```
agents/<name>/
├── README.md     # 职责、边界、路由位置、高风险动作
├── prompt.md     # 系统 prompt / 角色定义
├── tools.md      # 允许调用的工具清单
├── schemas/      # 结构化输入输出 schema
├── src/          # 代码实现
└── tests/
```

新增 agent：复制 `_template/` 为 `agents/<new-name>/`，按模板填写。

## 已登记 agent

| 目录 | 层级 | 职责概述 |
| --- | --- | --- |
| `life/` | 执行 | 日程、提醒、生活例行 |
| `investment/` | 研究 | 投资跟踪与复盘，不自动交易 |
| `general-intel/` | 研究 | 广域信息搜集 |
| `ai-research/` | 研究 | AI 模型/论文/产品研究 |
| `knowledge/` | 知识 | 归一化、标签、归档（最终落点） |
| `coding/` | 执行 | 脚本、工具、自动化 |
| `content/` | 执行 | 立意、初稿、出版准备 |
| `relationship/` | 关系（可选） | 联系人、协作跟进 |

层级定义与路由规则参见 `docs/constitution.md` 与 `docs/agent-plan.md`。
