# jarvis 规则

## 1. 目的

本文档定义 `jarvis` 个人助理系统的稳定规则。

它的目标是让系统保持：

- 清晰
- 一致
- 易于扩展
- 易于迁移
- 不依赖任何单一 AI 模型、框架或厂商

本文是约束层，不是功能清单。

---

## 2. 核心定义

`jarvis` 是一个以单一用户为中心的个人 Agent OS。

它管理：

- 生活
- 投资
- 通用情报获取
- AI 研究
- 知识组织
- 编码与工具构建
- 内容创作

后续也可以扩展到：

- 关系与协作管理

---

## 3. 系统不变量

无论模型、框架、UI 或工具栈如何变化，以下规则都应保持成立。

### 3.1 单一入口

所有重要任务都应通过 `jarvis` 进入。

原因：

- 统一上下文
- 统一记忆
- 统一审计轨迹

### 3.2 一个中枢，多个领域 Agent

`jarvis Core` 是总控中枢。

领域 Agent 是专业执行者。

中枢负责路由工作，专业 Agent 不替代中枢。

### 3.3 一个任务，一个主责

每个任务必须且只能有一个 `primary agent`。

其他 Agent 可以协作，但不能争夺同一任务的控制权。

### 3.4 研究、执行、归档必须分离

不要让一个 Agent 同时完成以下所有事情：

- 收集信息
- 做战略判断
- 执行最终动作
- 定义最终归档结构

这些职责必须分离。

### 3.5 知识层是最终收口

任何值得长期保留的结果，最终都必须由 `Knowledge Agent` 或知识工作流进行标准化并归档。

### 3.6 文件是长期真相源

重要数据不能只存在于：

- 聊天记录
- 隐藏记忆存储
- 向量数据库
- 厂商私有后端

重要产出必须以文件形式保存在稳定工作区中。

### 3.7 高风险动作必须最终确认

以下动作不得静默执行：

- 发布
- 删除
- 对外发送
- 交易
- 修改关键配置

这些动作必须有显式确认，或受明确定义的权限规则约束。

---

## 4. 稳定架构

系统应始终被理解为四层结构：

### 4.1 Core 层

负责：

- 用户身份
- 偏好
- 记忆协调
- 路由
- 工作流协调
- 权限控制
- 审计

### 4.2 Agent 层

负责领域推理与任务处理。

### 4.3 Tool 与 Workflow 层

负责：

- 工具执行
- 自动化
- 工作流步骤
- 结构化输出

### 4.4 Workspace 层

负责：

- 文件存储
- 目录结构
- metadata
- 索引
- 备份
- 迁移

如果未来系统仍保留这四层，系统就仍然具备可迁移性。

---

## 5. 规范 Agent 集合

### 5.1 核心 Agent

当前规范集合包括：

- `Life Agent`
- `Investment Agent`
- `General Intelligence Agent`
- `AI Research Agent`
- `Knowledge Agent`
- `Coding Agent`
- `Content Agent`

### 5.2 可选扩展 Agent

- `Relationship and Collaboration Agent`

该 Agent 是可选项，只有当对外沟通和协作成为系统的重要负载时才应启用。

---

## 6. Agent 角色

### 6.1 Life Agent

负责：

- 日程
- 提醒
- 日常运营
- 个人例行事务

不负责：

- 深度研究
- 代码实现
- 投资判断

### 6.2 Investment Agent

负责：

- 观察列表
- 投资复盘
- 风险跟踪
- 面向市场的综合判断

不负责：

- 自动交易
- 以全网扫描作为主要职责
- 最终对外执行

### 6.3 General Intelligence Agent

负责：

- 广泛信息收集
- 订阅流
- 新闻摘要
- 主题扫描

不负责：

- AI 专题深度研究
- 最终归档决策
- 最终发布

### 6.4 AI Research Agent

负责：

- AI 模型
- AI 产品
- AI 论文
- AI 工具
- AI 工作流
- AI 趋势判断

不负责：

- 以泛化扫描作为最终职责
- 最终代码实现
- 最终发布
- 最终归档控制

### 6.5 Knowledge Agent

负责：

- 标准化
- 打标签
- 实体结构
- 链接关系
- 归档一致性

不负责：

- 原始战略判断
- 直接公开发布
- 代码实现

### 6.6 Coding Agent

负责：

- 脚本
- 工具
- 代码修改
- 自动化实现

不负责：

- 最终内容策略
- 长期知识治理
- 投资决策权

### 6.7 Content Agent

负责：

- 选题 framing
- 提纲
- 草稿
- 改写
- 发布准备

不负责：

- 长期归档结构
- 代码实现
- 战略型投资判断

### 6.8 Relationship and Collaboration Agent

负责：

- 联系人
- 沟通上下文
- 会后跟进
- 协作跟踪
- 关系记忆

不负责：

- 日常生活运营
- 投资判断
- 未经确认的敏感外发

---

## 7. Agent 分层

为了避免职责重叠，Agent 应被划分为稳定层级。

### 7.1 执行层

- `Life Agent`
- `Coding Agent`
- `Content Agent`

### 7.2 研究层

- `General Intelligence Agent`
- `AI Research Agent`
- `Investment Agent`

### 7.3 知识层

- `Knowledge Agent`

### 7.4 可选关系层

- `Relationship and Collaboration Agent`

这些层级的含义是：

- 执行层：现在应该做什么
- 研究层：什么重要，为什么重要
- 知识层：什么值得长期保留
- 关系层：谁重要，哪些事项需要跟进

---

## 8. 默认路由规则

### 8.1 路由原则

对于任何任务：

1. 选择主责 Agent
2. 选择协作 Agent
3. 选择归档路径
4. 定义审批节点

### 8.2 默认模式

#### 模式 A：情报 -> 研究 -> 归档

适用于：

- 趋势跟踪
- 专题研究
- 投资信号复核

路由：

`General Intelligence Agent` -> `AI Research Agent` 或 `Investment Agent` -> `Knowledge Agent`

#### 模式 B：研究 -> 创作 -> 归档

适用于：

- 文章
- 视频脚本
- 面向公开的分析内容

路由：

`General Intelligence Agent` 或 `AI Research Agent` -> `Content Agent` -> `Knowledge Agent`

#### 模式 C：研究 -> 构建 -> 归档

适用于：

- 工具
- 实验
- 自动化

路由：

`AI Research Agent` 或 `Knowledge Agent` -> `Coding Agent` -> `Knowledge Agent`

#### 模式 D：会议 / 联系人 -> 跟进 -> 归档

适用于：

- 会议结果
- 联系人管理
- 协作进展

路由：

`Life Agent` 或 `Relationship and Collaboration Agent` -> `Relationship and Collaboration Agent` -> `Knowledge Agent`

### 8.3 冲突解决

如果多个 Agent 看起来都适合：

1. 离最终产出最近的 Agent 拥有任务主责
2. 执行高风险动作的 Agent 必须是最终执行 owner
3. 归档 ownership 始终属于 `Knowledge Agent`
4. 研究型 Agent 默认不能直接发布或对外发送

---

## 9. 工作区规则

### 9.1 稳定工作区

所有可长期保留的输出都必须存在于稳定工作区中。

### 9.2 按领域存储

按领域和内容类型存储，而不是按临时 Agent 实例存储。

推荐的领域根目录：

- `life`
- `invest`
- `intel`
- `knowledge`
- `dev`
- `content`
- `shared`
- `archive`

### 9.3 文件优先存储

推荐的长期格式：

- `md`
- `json`
- `yaml`
- `csv`
- 源代码文件
- 标准媒体格式

### 9.4 必须具备 Metadata

任何长期文档都应包含稳定 metadata。

最低字段：

- `id`
- `title`
- `created_at`
- `updated_at`
- `domain`
- `type`
- `status`
- `tags`
- `visibility`

### 9.5 只使用相对引用

内部引用应使用：

- 相对路径
- 逻辑 ID

避免在可迁移数据中写死机器相关的绝对路径。

### 9.6 索引必须可重建

搜索索引、向量索引和缓存都必须可以从文件重建。

---

## 10. 记忆规则

记忆必须拆分为两类。

### 10.1 Fact Memory

稳定数据，例如：

- 用户偏好
- 长期目标
- 项目上下文
- 联系人
- 规则
- 投资观察列表

### 10.2 Working Memory

短期数据，例如：

- 当前任务上下文
- 临时计划
- 草稿
- 最近对话
- 进行中的工作流状态

规则：

working memory 可以过期；  
fact memory 应被显式管理。

---

## 11. 工具规则

### 11.1 工具必须是已注册对象

每个工具都应具备稳定 metadata：

- `id`
- `name`
- `description`
- `category`
- `input_schema`
- `output_schema`
- `permissions`
- `version`
- `status`

### 11.2 工具不是 Agent

Agent 负责判断。  
Tool 负责执行。

概念上绝不能混淆这两个角色。

### 11.3 工具访问必须受限

不是每个 Agent 都可以使用每个 Tool。

工具访问应受以下因素限制：

- 领域
- 风险等级
- 工作流阶段
- 明确 allowlist

---

## 12. 审批规则

### 12.1 低风险动作

通常无需显式确认：

- 读取
- 总结
- 分类
- 起草

### 12.2 中风险动作

可以基于策略决定是否需要审批：

- 写入内部文件
- 修改知识组织
- 运行脚本
- 编辑结构化配置

### 12.3 高风险动作

必须显式确认：

- 发布
- 删除
- 对外发送
- 金融动作
- 凭证变更
- 重大系统配置变更

---

## 13. 可迁移性规则

本规则文件必须能够跨不同 AI 系统保持有效。

因此：

### 13.1 核心逻辑不得锁定单一厂商

核心规则不能依赖：

- 单一模型家族
- 单一聊天 UI
- 单一向量数据库
- 单一编排框架

### 13.2 语义必须稳定

即使不同系统中的名称发生变化，下列语义必须稳定：

- core
- agent
- tool
- workflow
- memory
- workspace
- archive
- approval

### 13.3 优先使用纯文件和简单 schema

尽可能使用可迁移格式：

- Markdown
- JSON
- YAML
- CSV

### 13.4 Prompt 不能是唯一规格

重要逻辑必须存在于显式文档和 schema 中，不能只藏在隐藏 prompt 里。

### 13.5 系统必须能在模型替换后继续存活

如果底层模型发生变化，以下内容仍必须可用：

- workspace
- files
- metadata
- agent roles
- routing rules
- approval rules

---

## 14. 绝对不能发生的事情

以下情况属于系统失败：

- 一个 Agent 静默地同时完成研究、执行和归档
- 重要知识只存在于聊天记录中
- 文件结构依赖某个模型厂商
- 研究型 Agent 直接执行高风险外部动作
- 多个 Agent 争夺任务 owner
- 长期资产只保存在不可恢复的索引中
- 对外沟通无法追溯

---

## 15. 最小可迁移契约

任何未来的 jarvis 实现，只要至少保留以下内容，就可以被接受：

1. 一个 Core orchestrator
2. 清晰的领域 Agent
3. one-task-one-owner 路由
4. 知识层作为最终归档收口
5. 基于文件的长期工作区
6. 稳定 metadata
7. 高风险动作显式审批
8. 可重建的索引与缓存
9. 与模型无关的系统语义

---

## 16. 最终原则

`jarvis` 应被视为一个长期存在的个人系统，而不是一次性的 prompt 搭建。

模型会变化。  
工具会变化。  
界面会变化。

但规则、工作区和长期知识应保持不变。
