# jarvis

`jarvis` 是一个面向单一用户的个人 Agent OS 设计项目。它的目标不是做一个聊天机器人，而是作为统一智能中枢，协调生活管理、投资研究、通用情报获取、AI 研究、知识沉淀、编码执行和内容创作。

当前仓库处于规范与架构定义阶段，主要内容是系统规则、工作区规范、Agent 规划与 GUI 设计文档，还没有落地的运行时代码或自动化脚手架。

## 这个仓库包含什么

- [`jarvis-Constitution.md`](./jarvis-Constitution.md)：系统宪章，定义核心规则、架构边界和 Agent 职责
- [`jarvis-12条铁律.md`](./jarvis-12%E6%9D%A1%E9%93%81%E5%BE%8B.md)：最核心的 12 条约束，可作为高层原则速览
- [`jarvis-工作区目录与Metadata规范.md`](./jarvis-%E5%B7%A5%E4%BD%9C%E5%8C%BA%E7%9B%AE%E5%BD%95%E4%B8%8EMetadata%E8%A7%84%E8%8C%83.md)：文件落盘、目录结构、命名与 metadata 规范
- [`jarvis-个人Agent规划.md`](./jarvis-%E4%B8%AA%E4%BA%BAAgent%E8%A7%84%E5%88%92.md)：核心 Agent 角色划分、能力域与协作方式
- [`jarvis-Workspace-GUI规划.md`](./jarvis-Workspace-GUI%E8%A7%84%E5%88%92.md)：资料工作台与可视化界面规划
- [`AGENTS.md`](./AGENTS.md)：本仓库贡献说明

## 推荐阅读顺序

如果你是第一次进入这个仓库，建议按下面顺序阅读：

1. [`jarvis-12条铁律.md`](./jarvis-12%E6%9D%A1%E9%93%81%E5%BE%8B.md)：先快速理解系统最硬的约束
2. [`jarvis-Constitution.md`](./jarvis-Constitution.md)：再建立整体结构和角色边界
3. [`jarvis-工作区目录与Metadata规范.md`](./jarvis-%E5%B7%A5%E4%BD%9C%E5%8C%BA%E7%9B%AE%E5%BD%95%E4%B8%8EMetadata%E8%A7%84%E8%8C%83.md)：明确文件如何落盘、命名和归档
4. [`jarvis-个人Agent规划.md`](./jarvis-%E4%B8%AA%E4%BA%BAAgent%E8%A7%84%E5%88%92.md)：理解各类 Agent 的职责和协作方式
5. [`jarvis-Workspace-GUI规划.md`](./jarvis-Workspace-GUI%E8%A7%84%E5%88%92.md)：最后看可视化工作台如何承接这些规范

## 核心设计原则

- 所有重要任务统一进入 `jarvis`
- 每个任务只能有一个主责 Agent
- 研究、执行、归档必须分离
- 长期资产必须落盘为文件，不能只存在聊天或隐藏存储中
- 工作区按领域组织，不按临时 Agent 实例组织
- 所有长期文档必须带稳定 metadata
- 发布、删除、外发、交易、关键配置修改都属于高风险动作，必须显式确认

## 稳定架构

jarvis 长期保持四层结构：

1. `Core`：负责路由、记忆、权限、审计与工作流协调
2. `Agents`：负责领域推理与任务主责
3. `Tools & Workflows`：负责执行动作与自动化流程
4. `Workspace`：负责文件、metadata、索引、备份与迁移

## 规划中的工作区模型

长期资料将进入稳定的领域目录，而不是散落在临时输出目录中。核心结构包括：

```text
00-system/   系统配置、注册表、日志、缓存
01-inbox/    临时接收与待整理输入
10-life/     生活资料
20-invest/   投资研究
30-intel/    通用情报
40-knowledge/ 知识归档
50-dev/      项目、脚本、工具、规格
60-content/  选题、草稿、发布内容
70-shared/   跨领域共享对象
90-archive/  快照、导出与废弃资料
```

更完整的目录职责、命名规则和 frontmatter 要求见 `jarvis-工作区目录与Metadata规范.md`。

## 当前状态

- 这是一个文档优先的设计仓库
- 尚未配置 `package.json`、测试框架或构建系统
- 当前重点是先把规则、边界、目录规范和 Agent 分工定义清楚
- 后续可在此基础上逐步补齐代码实现、工作流脚本和 GUI

## Roadmap

建议按以下顺序推进：

1. 固化规范：继续收敛宪章、规则、目录与 metadata 字段，减少重复定义
2. 初始化工作区：按规范创建基础目录、注册表、模板与示例文档
3. 落地最小工具链：补充脚本、配置文件和基本校验命令
4. 接入工作流：把常见输入、归档、摘要、整理动作做成可重复执行的流程
5. 实现 GUI：围绕文件浏览、资料预览、关系视图、快照与迁移能力逐步落地

更直接地说，当前阶段先把“规则说清楚”，下一阶段再把“目录搭起来”，最后才是“工具和界面真正跑起来”。

## 协作方式

提交新内容前，建议先阅读 `jarvis-Constitution.md` 和 `jarvis-工作区目录与Metadata规范.md`。新增长期文档时，请优先遵循以下要求：

- 使用 Markdown 或其他可迁移的纯文本格式
- 文件命名使用小写英文与连字符
- 日期统一采用 `YYYY-MM-DD`
- 避免 `final`、`v2`、`latest` 这类无语义命名
- 长期 Markdown 文档补齐 frontmatter metadata

如果你要扩展仓库结构、引入脚本或新增运行时代码，请同步更新 `README.md` 与 [`AGENTS.md`](./AGENTS.md)，避免规范与实现脱节。
