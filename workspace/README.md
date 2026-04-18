# workspace/

运行时数据目录，对应 `docs/workspace-metadata-spec.md` 中的 `WORKSPACE_ROOT`。

按"领域 + 类型"组织，**不要**按临时 agent 实例组织。

| 目录 | 用途 |
| --- | --- |
| `00-system/` | 系统配置、注册表、日志、缓存 |
| `01-inbox/` | 临时收件、未分类输入 |
| `10-life/` | 生活材料 |
| `20-invest/` | 投资研究 |
| `30-intel/` | 通用情报 |
| `40-knowledge/` | 知识归档（Knowledge Agent 最终落点） |
| `50-dev/` | 项目、脚本、工具、规范 |
| `60-content/` | 灵感、初稿、已发布 |
| `70-shared/` | 跨域共享对象 |
| `90-archive/` | 快照、导出、废弃材料 |

文件命名、frontmatter、归档规则见 `docs/workspace-metadata-spec.md`。
