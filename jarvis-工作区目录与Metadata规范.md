# jarvis 工作区目录与 Metadata 规范

## 1. 目的

本规范用于定义 `jarvis` 的个人工作区组织方式，确保所有 Agent、工具、工作流产生的资料都满足以下要求：

- 可被本地文件系统直接管理
- 可被 `VSCode`、`Obsidian`、`jarvis GUI` 直接读取
- 可长期保管
- 可跨设备迁移
- 可建立统一索引和可视化视图

本规范是实现层规范，不是产品概念说明。

---

## 2. 设计原则

### 2.1 文件是真相源

所有核心资料必须优先落盘为文件，不能只存在内存、数据库或向量索引中。

### 2.2 目录结构稳定优先

资料按领域、类型和状态组织，不按临时 Agent 实例组织。

### 2.3 Metadata 统一优先

所有核心文档必须具备统一元数据，以支持检索、索引、关系分析和迁移。

### 2.4 相对路径优先

工作区内部引用必须使用相对路径或工作区逻辑 ID，避免写死设备路径。

### 2.5 索引可重建

索引、缓存、向量库、搜索库都必须可重建，原始文件不可替代。

---

## 3. 工作区根目录

建议工作区根目录固定为一个独立目录，例如：

```text
jarvis/
```

后续文档中用 `WORKSPACE_ROOT` 指代该根目录。

---

## 4. 标准目录结构

```text
WORKSPACE_ROOT/
  00-system/
    config/
    registry/
      agents/
      tools/
      workflows/
      schemas/
    prompts/
    templates/
    logs/
    cache/
    backups/

  01-inbox/
    capture/
    imports/
    unsorted/

  10-life/
    calendar/
    tasks/
    journal/
    finance-personal/
    travel/

  20-invest/
    watchlist/
    research/
    market-notes/
    thesis/
    reviews/
    data/

  30-intel/
    news/
    web-clips/
    digests/
    topics/
    feeds/

  40-knowledge/
    notes/
    projects/
    entities/
    references/
    maps/

  50-dev/
    projects/
    scripts/
    tools/
    specs/
    snippets/

  60-content/
    ideas/
    outlines/
    drafts/
    published/
    assets/
    campaigns/

  70-shared/
    contacts/
    companies/
    assets/
    datasets/

  90-archive/
    snapshots/
    exports/
    deprecated/
```

---

## 5. 目录职责

### 5.1 `00-system`

系统控制区，不存放用户主内容。

用途：

- 配置
- Agent 定义
- Tool 注册
- Workflow 定义
- Prompt 模板
- 日志
- 缓存
- 备份

约束：

- `cache/` 可清理
- `logs/` 可滚动归档
- `registry/` 应纳入版本管理

### 5.2 `01-inbox`

临时接收区。

用途：

- 快速捕获内容
- 导入的未归类文件
- 待整理输入

约束：

- 该目录不应成为长期存储位置
- 文件应定期流转到正式领域目录

### 5.3 `10-life` 到 `60-content`

领域资料区。

约束：

- 这里存放长期有效的正式资料
- Agent 输出应优先按领域落到这些目录

### 5.4 `70-shared`

跨领域共享对象区。

适用于：

- 联系人
- 公司实体
- 公共数据集
- 跨领域引用资产

### 5.5 `90-archive`

归档区。

用途：

- 历史快照
- 导出包
- 废弃资料

约束：

- 不应作为活跃写入目录

---

## 6. 资料落盘规则

### 6.1 基本规则

每个 Agent 产生的资料必须落入“稳定领域目录”，而不是写入随意的输出目录。

正确示例：

- 投资研究笔记 -> `20-invest/research/`
- 新闻摘要 -> `30-intel/digests/`
- 项目知识卡片 -> `40-knowledge/projects/`
- 自动生成脚本 -> `50-dev/scripts/`
- 创作草稿 -> `60-content/drafts/`

不推荐示例：

- `agents/invest-agent/output-1.md`
- `tmp/hermes-result-final-v2.md`
- `desktop/new-note.md`

### 6.2 Agent 与目录的映射建议

| Agent 类型 | 默认落盘目录 |
|---|---|
| life-agent | `10-life/` |
| invest-agent | `20-invest/` |
| intel-agent | `30-intel/` |
| knowledge-agent | `40-knowledge/` |
| dev-agent | `50-dev/` |
| content-agent | `60-content/` |

说明：

- Agent 只决定默认路径
- 最终路径仍应由资料的真实业务属性决定

### 6.3 工作流输出规则

如果一个 Workflow 跨多个阶段产生中间文件，应区分：

- `正式产出物`：进入领域目录
- `中间产物`：进入 `00-system/cache/` 或临时目录
- `审计记录`：进入 `00-system/logs/`

---

## 7. 文件命名规范

### 7.1 通用命名规则

统一使用：

- 小写英文
- 连字符 `-`
- 不使用空格
- 不使用中文文件名作为主规范
- 避免 `final`, `new`, `v2`, `latest` 这类无语义后缀

推荐格式：

```text
<type>-<topic>-<date>-<seq>.<ext>
```

示例：

```text
research-nvidia-supply-chain-2026-04-13-001.md
digest-ai-agents-weekly-2026-04-13-001.md
draft-xhs-productivity-2026-04-13-001.md
script-rss-ingest-2026-04-13-001.py
```

### 7.2 日期格式

统一使用：

```text
YYYY-MM-DD
```

### 7.3 序号规则

同一日、同一主题下需要多个文件时，使用三位序号：

```text
001
002
003
```

### 7.4 特殊文件命名

配置文件和注册文件建议使用稳定名：

```text
agent.invest.yaml
tool.web_search.yaml
workflow.daily_digest.yaml
metadata.schema.yaml
```

---

## 8. 文件类型规范

### 8.1 首选文件格式

文本资料优先使用：

- `md`
- `json`
- `yaml`
- `csv`
- `txt`

媒体与二进制资料可使用：

- `png`
- `jpg`
- `webp`
- `pdf`
- `mp3`
- `mp4`

代码资料使用对应源代码格式：

- `py`
- `ts`
- `js`
- `sh`
- `sql`

### 8.2 文本主文档规范

以下内容建议优先使用 Markdown：

- 笔记
- 研究记录
- 摘要
- 草稿
- 报告
- 主题卡片

---

## 9. Markdown Metadata 规范

### 9.1 适用范围

以下文件必须带 frontmatter：

- 所有长期保存的 Markdown 主文档
- 所有需要进入索引系统的内容
- 所有需要在 GUI 中展示详情页的内容

### 9.2 必填字段

为了降低实施难度，只保留真正必需的字段作为必填项：

```yaml
id:           # 全局唯一文档 ID，系统自动生成
created_at:   # 创建时间，系统自动生成
domain:       # 资料所属领域，必须明确指定
```

### 9.3 推荐字段

以下字段强烈推荐填写，系统可提供默认值或自动推断：

```yaml
title:        # 文档标题，可从内容首行推断
updated_at:   # 更新时间，默认等于 created_at
type:         # 资料类型，可有默认值（如 note）
status:       # 当前状态，默认为 draft
tags:         # 标签数组，可为空数组 []
visibility:   # 可见性，默认为 private
```

### 9.4 可选字段

以下字段按需填写，用于增强检索和关系管理：

```yaml
agent:        # 生成或维护该文档的 Agent
workflow:     # 来源 Workflow ID
source_type:  # 来源类型
source_url:   # 外部来源链接
authors:      # 作者或整理者
entities:     # 关联实体 ID
related:      # 相关文档 ID
review_at:    # 复查日期
language:     # 语言
summary:      # 简介摘要
```

### 9.5 字段定义

| 字段 | 类型 | 是否必填 | 默认值 | 说明 |
|---|---|---|---|---|
| `id` | string | 是 | 自动生成 | 全局唯一文档 ID，格式：`<type>-<topic>-<date>-<seq>` |
| `created_at` | date or datetime | 是 | 自动生成 | 创建时间，ISO 8601 格式 |
| `domain` | enum | 是 | 无 | 资料所属领域，见枚举值 |
| `title` | string | 推荐 | 从内容推断 | 文档标题 |
| `updated_at` | date or datetime | 推荐 | = created_at | 更新时间 |
| `type` | string | 推荐 | `note` | 资料类型，如 note, research, draft, script 等 |
| `status` | enum | 推荐 | `draft` | 当前状态，见枚举值 |
| `tags` | string[] | 推荐 | `[]` | 标签数组 |
| `visibility` | enum | 推荐 | `private` | 可见性，见枚举值 |
| `agent` | string | 可选 | 无 | 生成或维护该文档的 Agent |
| `workflow` | string | 可选 | 无 | 来源 Workflow ID |
| `source_type` | enum | 可选 | 无 | 来源类型，见枚举值 |
| `source_url` | string | 可选 | 无 | 外部来源链接 |
| `authors` | string[] | 可选 | 无 | 作者或整理者 |
| `entities` | string[] | 可选 | 无 | 关联实体 ID |
| `related` | string[] | 可选 | 无 | 相关文档 ID |
| `review_at` | date | 可选 | 无 | 复查日期 |
| `language` | string | 可选 | 无 | 语言代码，如 zh, en |
| `summary` | string | 可选 | 无 | 简介摘要 |

### 9.5 枚举建议

#### `domain`

允许值：

- `life`
- `invest`
- `intel`
- `knowledge`
- `dev`
- `content`
- `shared`
- `system`

#### `type`

常见类型建议（可扩展）：

- `note` - 笔记
- `research` - 研究报告
- `digest` - 摘要
- `draft` - 草稿
- `article` - 文章
- `script` - 脚本
- `tool` - 工具
- `spec` - 规格说明
- `meeting-note` - 会议记录
- `journal` - 日志
- `task` - 任务
- `contact` - 联系人
- `entity` - 实体

#### `status`

允许值：

- `inbox` - 待整理
- `draft` - 草稿
- `active` - 活跃
- `reviewed` - 已复核
- `published` - 已发布
- `archived` - 已归档
- `deprecated` - 已废弃

#### `visibility`

允许值：

- `private` - 私有
- `internal` - 内部
- `public` - 公开

#### `source_type`

允许值：

- `manual` - 手动创建
- `web` - 网页来源
- `email` - 邮件来源
- `meeting` - 会议来源
- `market` - 市场数据
- `agent-generated` - Agent 生成
- `workflow-generated` - 工作流生成
- `imported` - 导入

### 9.6 标准 frontmatter 示例

**最小示例（仅必填字段）：**

```md
---
id: research-nvidia-supply-chain-2026-04-13-001
created_at: 2026-04-13
domain: invest
---
```

**推荐示例（必填 + 推荐字段）：**

```md
---
id: research-nvidia-supply-chain-2026-04-13-001
created_at: 2026-04-13
domain: invest
title: Nvidia Supply Chain Notes
updated_at: 2026-04-13
type: research-note
status: draft
tags:
  - invest
  - semis
  - nvidia
visibility: private
---
```

**完整示例（包含可选字段）：**

```md
---
id: research-nvidia-supply-chain-2026-04-13-001
created_at: 2026-04-13
domain: invest
title: Nvidia Supply Chain Notes
updated_at: 2026-04-13
type: research-note
status: draft
tags:
  - invest
  - semis
  - nvidia
visibility: private
agent: invest-agent
workflow: wf-invest-daily-research
source_type: web
source_url: https://example.com/article
authors:
  - hermes
entities:
  - company.nvidia
related:
  - digest-semiconductor-weekly-2026-04-13-001
review_at: 2026-04-20
language: en
summary: Notes on current supply chain signals affecting Nvidia.
---
```

---

## 10. 非 Markdown 文件的 Metadata 规范

二进制或非 Markdown 文件不适合写 frontmatter 时，应采用伴随 metadata 文件。

示例：

```text
earnings-nvidia-q1-2026.pdf
earnings-nvidia-q1-2026.pdf.meta.json
```

建议 `.meta.json` 结构：

```json
{
  "id": "report-nvidia-q1-2026-001",
  "title": "Nvidia Q1 2026 Earnings Report",
  "created_at": "2026-04-13",
  "updated_at": "2026-04-13",
  "domain": "invest",
  "type": "report-pdf",
  "status": "active",
  "tags": ["invest", "earnings", "nvidia"],
  "visibility": "private",
  "agent": "invest-agent",
  "source_type": "web",
  "source_url": "https://example.com/report.pdf"
}
```

---

## 11. 文档 ID 规范

### 11.1 基本格式

建议统一格式：

```text
<type>-<topic>-<date>-<seq>
```

示例：

```text
research-nvidia-supply-chain-2026-04-13-001
digest-ai-agents-weekly-2026-04-13-001
draft-xhs-productivity-2026-04-13-001
```

### 11.2 全局唯一性

`id` 在整个工作区中必须唯一。

推荐做法：

- 文件名与 `id` 保持一致
- 或保证文件名至少可从 `id` 推导

---

## 12. 标签与实体规范

### 12.1 标签

标签用于轻量分类。

规则：

- 使用小写英文
- 使用连字符
- 不建议混合中英标签作为主规范

示例：

- `ai`
- `agents`
- `nvidia`
- `weekly-review`
- `xhs`

### 12.2 实体

实体用于可视化关系和知识图谱，不等同于普通标签。

建议实体 ID 规范：

```text
person.<slug>
company.<slug>
project.<slug>
asset.<slug>
topic.<slug>
```

示例：

- `company.nvidia`
- `project.hermes`
- `topic.ai-agents`

---

## 13. 索引规范

### 13.1 索引目标

索引层用于支持：

- 全文搜索
- GUI 列表展示
- 时间线
- 图谱关系
- 按 Agent / Workflow / Tag / Entity 检索

### 13.2 索引来源

索引应来自：

- 文件路径
- frontmatter
- `.meta.json`
- 文本正文
- 系统 registry

### 13.3 索引最小字段

索引系统至少应提取：

- `id`
- `title`
- `path`
- `domain`
- `type`
- `status`
- `tags`
- `agent`
- `workflow`
- `created_at`
- `updated_at`
- `source_url`

### 13.4 索引重建规则

索引丢失时，应能通过扫描工作区完整重建。

因此：

- 不允许只有索引没有原始文件
- GUI 不应依赖不可恢复的数据库主键

---

## 14. Registry 规范

### 14.1 位置

注册信息存放于：

```text
00-system/registry/
```

建议子目录：

- `agents/`
- `tools/`
- `workflows/`
- `schemas/`

### 14.2 Agent 注册文件

示例：

```text
00-system/registry/agents/agent.invest.yaml
```

建议字段：

- `id`
- `name`
- `domain`
- `description`
- `allowed_tools`
- `default_output_paths`
- `permission_level`
- `owner`
- `status`

### 14.3 Tool 注册文件

示例：

```text
00-system/registry/tools/tool.web_search.yaml
```

建议字段：

- `id`
- `name`
- `category`
- `description`
- `input_schema`
- `output_schema`
- `permissions`
- `version`
- `status`

### 14.4 Workflow 注册文件

示例：

```text
00-system/registry/workflows/workflow.daily-digest.yaml
```

建议字段：

- `id`
- `name`
- `description`
- `inputs`
- `steps`
- `outputs`
- `default_target_paths`
- `approval_policy`
- `status`

---

## 15. 迁移约束

为保证工作区可迁移，必须遵守以下约束：

### 15.1 路径约束

- 不在文档中写死本机绝对路径
- 工作区内部引用优先使用相对路径

### 15.2 配置约束

- 本机差异配置放 `00-system/config/`
- 不把设备私有配置混入主内容目录

### 15.3 资源约束

- 图片、PDF、附件等资源必须保存在工作区内或有明确外部来源
- 避免引用失效的临时下载路径

### 15.4 缓存约束

- 向量索引、搜索库、临时缓存应位于 `00-system/cache/`
- 迁移时可不作为核心资产

---

## 16. 版本管理建议

建议对以下内容使用 Git 管理：

- Markdown 主文档
- YAML 配置
- JSON metadata
- Prompt
- Workflow
- Tool registry

不建议直接纳入 Git 的内容：

- 大型媒体文件
- 高频缓存文件
- 可重建索引

可选方案：

- 大文件使用 Git LFS
- 快照包放入 `90-archive/snapshots/`

---

## 17. 最小落地要求

如果只先做 MVP，至少应满足以下要求：

1. 存在统一 `WORKSPACE_ROOT`
2. 目录结构按本规范分层
3. 所有长期保存 Markdown 带 frontmatter
4. 所有二进制核心文件带 `.meta.json`
5. 所有 Agent 都有默认输出目录
6. 所有 Tool / Workflow 都有 registry 文件
7. 索引系统可以通过扫描文件重建

---

## 18. 推荐实施顺序

### Phase 1

- 建立工作区目录
- 建立 frontmatter 规范
- 建立 Agent / Tool / Workflow registry
- 让新生成资料全部按规范落盘

### Phase 2

- 增加索引器
- 增加 `.meta.json` 伴随文件规则
- 增加标签和实体规范
- 增加 GUI Explorer

### Phase 3

- 增加迁移检查器
- 增加一致性校验器
- 增加自动归档策略
- 增加快照和恢复机制

---

## 19. 一句话结论

jarvis 的长期资产不应依赖某个 Agent、某个数据库或某个前端，而应建立在统一的本地工作区、稳定的目录结构和统一的 metadata 规范之上。
