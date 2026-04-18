# &lt;Agent Name&gt;

新 agent 的脚手架模板。复制本目录到 `agents/<name>/` 后，按以下结构填写。

## 职责
一句话说明该 agent 的核心职责。

## 边界
- 不做什么
- 与其他 agent 的分工

## 路由位置
属于哪一层（执行 / 研究 / 知识 / 关系），常见上下游 agent。

## 输入 / 输出
- 输入：消息、文件、事件
- 输出：归档去向、产物形态

## 高风险动作
列出需要显式确认的动作（参见 `docs/constitution.md` 审批规则）。

## 目录约定
- `prompt.md` 系统 prompt / 角色定义
- `tools.md` 允许调用的工具清单
- `schemas/` 结构化输入输出 schema
- `src/` 代码实现
- `tests/` 测试
