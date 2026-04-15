# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

`jarvis` is a personal Agent OS design project for a single user. It serves as a unified intelligent hub coordinating life management, investment research, general intelligence gathering, AI research, knowledge organization, coding execution, and content creation.

This repository is currently in the specification and architecture definition phase. It contains system rules, workspace specifications, agent planning, and GUI design documents, but does not yet have runtime code or automation scaffolding.

## Core Architecture Principles

### System Invariants

These rules must hold regardless of model, framework, UI, or tooling changes:

1. **Single Entry Point**: All important tasks enter through `jarvis`
2. **One Task, One Owner**: Every task has exactly one primary agent
3. **Separation of Concerns**: Research, execution, and archival must remain separate responsibilities
4. **Knowledge Layer as Final Sink**: Anything worth keeping must be archived through the Knowledge Agent or knowledge workflow
5. **Files as Truth Source**: Durable knowledge must live in files, not only in chats, hidden memory, or vendor storage
6. **High-Risk Actions Require Confirmation**: Publishing, deletion, external sending, trading, and critical config changes need explicit approval
7. **Portability First**: The system must remain portable across models, frameworks, and interfaces

### Four-Layer Architecture

The system maintains a stable four-layer structure:

1. **Core**: Routing, memory, permissions, workflows, and audit
2. **Agents**: Domain-specific reasoning and task ownership
3. **Tools & Workflows**: Action execution and structured automation
4. **Workspace**: Files, metadata, indexes, backups, and archives

## Agent System

### Core Agents

- **Life Agent**: Daily operations, schedule, reminders, routines
- **Investment Agent**: Investment tracking, reviews, risk synthesis (no automatic trading)
- **General Intelligence Agent**: Broad information gathering, feeds, topic scanning
- **AI Research Agent**: AI models, papers, products, tools, workflows, trend judgment
- **Knowledge Agent**: Normalization, tagging, entity structure, linking, archival consistency (final archive sink)
- **Coding Agent**: Scripts, tools, code changes, automation implementation
- **Content Agent**: Framing, outlines, drafts, rewrites, publication preparation

### Optional Agent

- **Relationship and Collaboration Agent**: Contacts, communication context, meeting follow-up, collaboration tracking (never sends sensitive external communication without confirmation)

### Agent Layering

- **Execution Layer**: Life Agent, Coding Agent, Content Agent
- **Research Layer**: General Intelligence Agent, AI Research Agent, Investment Agent
- **Knowledge Layer**: Knowledge Agent
- **Optional Relationship Layer**: Relationship and Collaboration Agent

### Default Routing Patterns

**Pattern A: Intelligence → Research → Archive**
- Use for: Trend tracking, thematic research, investment signal review
- Route: `General Intelligence Agent` → `AI Research Agent / Investment Agent` → `Knowledge Agent`

**Pattern B: Research → Creation → Archive**
- Use for: Articles, video scripts, public-facing analysis
- Route: `General Intelligence / AI Research Agent` → `Content Agent` → `Knowledge Agent`

**Pattern C: Research → Build → Archive**
- Use for: Tools, experiments, automation
- Route: `AI Research / Knowledge Agent` → `Coding Agent` → `Knowledge Agent`

**Pattern D: Meeting / Contact → Follow-up → Archive**
- Use for: Meeting outcomes, contact management, collaboration progress
- Route: `Life / Relationship Agent` → `Relationship Agent` → `Knowledge Agent`

### Conflict Resolution

When multiple agents seem suitable:
1. The agent closest to the final output owns the task
2. The agent executing high-risk actions must be the final execution owner
3. Archive ownership always belongs to the Knowledge Agent
4. Research agents do not publish or externally send by default

## Workspace Structure

### Directory Organization

```
WORKSPACE_ROOT/
  00-system/       # System config, registry, logs, cache
  01-inbox/        # Temporary intake and unsorted input
  10-life/         # Life materials
  20-invest/       # Investment research
  30-intel/        # General intelligence
  40-knowledge/    # Knowledge archive
  50-dev/          # Projects, scripts, tools, specs
  60-content/      # Ideas, drafts, published content
  70-shared/       # Cross-domain shared objects
  90-archive/      # Snapshots, exports, deprecated materials
```

### File Storage Rules

- Store materials by domain and type, not by temporary agent instance
- Investment research notes → `20-invest/research/`
- News summaries → `30-intel/digests/`
- Knowledge cards → `40-knowledge/notes/`
- Scripts and tools → `50-dev/scripts/` or `50-dev/tools/`
- Content drafts → `60-content/drafts/`

### File Naming Convention

Use lowercase English with hyphens:

```
<type>-<topic>-<date>-<seq>.<ext>
```

Examples:
- `research-nvidia-supply-chain-2026-04-13-001.md`
- `digest-ai-agents-weekly-2026-04-13-001.md`
- `script-rss-ingest-2026-04-13-001.py`

Date format: `YYYY-MM-DD`

Avoid: `final`, `new`, `v2`, `latest`, spaces, Chinese filenames

### Metadata Requirements

All long-term Markdown documents must include frontmatter with minimum fields:

```yaml
---
id: unique-document-id
title: Document Title
created_at: YYYY-MM-DD
updated_at: YYYY-MM-DD
domain: life|invest|intel|knowledge|dev|content|shared|system
type: document-type
status: inbox|draft|active|reviewed|published|archived|deprecated
tags: [tag1, tag2, tag3]
visibility: private|internal|public
---
```

Recommended additional fields:
- `agent`: Agent that generated or maintains the document
- `workflow`: Source workflow ID
- `source_type`: manual|web|email|meeting|market|agent-generated|workflow-generated|imported
- `source_url`: External source link
- `authors`: Author or organizer list
- `entities`: Related entity IDs
- `related`: Related document IDs
- `review_at`: Review date
- `language`: Language code
- `summary`: Brief summary

## Memory System

Memory is split into two types:

- **Fact Memory**: Stable long-term data (user preferences, long-term goals, project context, contacts, rules, investment watchlist)
- **Working Memory**: Short-term task context (current tasks, temporary plans, drafts, recent conversations, in-progress workflow state)

Working memory may expire. Fact memory must be explicitly managed.

## Tool and Workflow Rules

1. Tools are registered objects, not agents
2. Agents decide; tools execute
3. Tool access must be limited by domain, risk, workflow stage, or allowlist
4. Important tool behavior must be documented in schemas, not only prompts

## Approval Rules

**Low Risk** (usually no explicit confirmation needed):
- Read, summarize, classify, draft

**Medium Risk** (policy-based approval):
- Write internal files, change knowledge organization, run scripts, edit structured configs

**High Risk** (must have explicit confirmation):
- Publish, delete, send externally, financial actions, credential changes, critical system changes

## Working with This Repository

### Current State

- This is a documentation-first design repository
- No `package.json`, test framework, or build system configured yet
- Current focus: Define rules, boundaries, directory specifications, and agent division of labor
- Future work: Gradually add code implementation, workflow scripts, and GUI

### Recommended Reading Order

1. `jarvis-12条铁律.md` - Understand the hardest system constraints
2. `jarvis-Constitution.md` - Establish overall structure and role boundaries
3. `jarvis-工作区目录与Metadata规范.md` - Understand file storage, naming, and archival
4. `jarvis-个人Agent规划.md` - Understand agent responsibilities and collaboration
5. `jarvis-Workspace-GUI规划.md` - Understand visualization workspace design

### File Verification Commands

Since no automated testing exists yet, use these lightweight commands:

```bash
# View repository files
rg --files

# Find and update cross-document references
rg -n "pattern" *.md

# Check trailing whitespace and patch format
git diff --check

# Confirm change scope before commit
git status
```

### Contribution Guidelines

When adding new long-term documents:

- Use Markdown or other portable plain text formats
- Use lowercase English with hyphens for filenames
- Use `YYYY-MM-DD` for dates
- Avoid `final`, `v2`, `latest` in naming
- Add frontmatter metadata to long-term Markdown documents
- Use relative paths for internal references
- Ensure indexes and caches are rebuildable from files

When extending repository structure, introducing scripts, or adding runtime code, synchronously update `README.md` and `AGENTS.md` to avoid specification-implementation drift.

### Commit Style

Use concise imperative sentences:
- `docs: add workspace metadata examples`
- `spec: refine agent routing rules`

## System Failure Conditions

These are considered system failures:

- One agent silently doing research, execution, and archival at once
- Important knowledge existing only in chat history
- Multiple agents competing for task ownership
- Research agents directly doing high-risk external actions
- Durable assets existing only in unrecoverable indexes
- External communication happening without traceability

## Portability Requirements

The system must not depend on any single:
- Model provider
- Orchestration framework
- Vector database
- UI

Core logic must survive model replacement. The following must remain stable even if infrastructure changes:
- Workspace
- Files
- Metadata
- Agent roles
- Routing rules
- Approval rules

## Final Principle

`jarvis` is not a temporary prompt setup. Models may change, tools may change, interfaces may change. The rules, workspace, and durable knowledge must remain.
