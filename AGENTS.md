# Repository Guidelines

## 项目结构与模块组织

仓库已按 agent 设计分层：

- `docs/` — 设计规范（`constitution.md`、`iron-rules.md`、`agent-plan.md`、`workspace-metadata-spec.md`、`workspace-gui-plan.md`）
- `core/` — 跨 agent 的系统能力（routing/memory/permissions/workflows/audit）
- `agents/` — 每个 agent 一个子目录，含 README/prompt/tools/schemas/src/tests，`agents/_template/` 是新 agent 脚手架
- `tools/` — 共享工具注册表
- `workspace/` — 运行时数据，子目录遵循 `docs/workspace-metadata-spec.md`（`00-system/`、`01-inbox/`、`10-life/`、`20-invest/`、`30-intel/`、`40-knowledge/`、`50-dev/`、`60-content/`、`70-shared/`、`90-archive/`）

后续运行时内容必须落到对应领域目录，不要在根目录创建临时且无语义的散乱目录。

## 构建、测试与开发命令

当前仓库尚未配置构建系统、包管理清单或自动化测试。现阶段建议使用以下轻量命令完成检查：

- `rg --files`：快速查看仓库文件
- `rg -n "pattern" *.md`：查找并统一更新跨文档引用
- `git diff --check`：检查尾随空格和补丁格式问题
- `git status`：提交前确认变更范围

如果后续引入脚本、依赖或测试工具，请同步更新 `README.md` 和本文件。

## 编码风格与命名规范

文档统一使用简洁 Markdown，标题层级清晰，说明直接，不写空泛描述。仓库内部引用优先使用相对路径。

文件命名遵循现有规范：

- 使用小写英文和连字符，例如 `research-market-map-2026-04-13-001.md`
- 日期统一为 `YYYY-MM-DD`
- 避免 `final`、`new`、`v2`、`latest` 这类无语义后缀

需要长期保存的 Markdown 文档应包含 frontmatter，至少包括 `id`、`title`、`created_at`、`updated_at`、`domain`、`type`、`status`、`tags`、`visibility`。

## 测试要求

在自动化测试落地前，一致性检查就是当前测试标准。提交前请确认内部链接可用、metadata 字段完整、文件命名符合规范，并与宪章类文档保持一致。若后续加入可执行代码，建议将测试放在对应模块旁或单独的 `tests/` 目录，并在文档中写明运行命令。

## 提交与 Pull Request 规范

当前仓库还没有可参考的提交历史，先采用简洁的祈使句风格，例如 `docs: add workspace metadata examples` 或 `spec: refine agent routing rules`。

Pull Request 应包含：

- 变更摘要
- 修改动机或对应规则
- 影响的文件或目录
- 仅在未来涉及 UI 或可视化产物时附截图

保持 PR 小而聚焦。如果修改了规范性规则，应在同一分支内同步更新相关文档，避免规则漂移。
