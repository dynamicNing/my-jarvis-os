# jarvis Rule

## 1. Purpose

This document defines the stable rules of the `jarvis` personal assistant system.

Its purpose is to keep the system:

- clear
- consistent
- easy to extend
- easy to migrate
- independent from any single AI model, framework, or vendor

This file is a constraint layer, not a feature list.

---

## 2. Core Definition

`jarvis` is a personal Agent OS centered on one user.

It manages:

- life
- investing
- general intelligence gathering
- AI research
- knowledge organization
- coding and tool building
- content creation

It may later expand to:

- relationship and collaboration management

---

## 3. System Invariants

The following rules should remain true even if the model, framework, UI, or tool stack changes.

### 3.1 Single Entry

All important tasks should enter through `jarvis`.

Reason:

- unified context
- unified memory
- unified audit trail

### 3.2 One Core, Multiple Domain Agents

`jarvis Core` is the orchestrator.

Domain Agents are specialists.

The core routes work. Specialists do not replace the core.

### 3.3 One Task, One Owner

Every task must have exactly one `primary agent`.

Other agents may assist, but must not compete for control of the same task.

### 3.4 Research, Execution, and Archiving Must Be Separated

Do not let one agent do all of the following at the same time:

- gather information
- make strategic judgments
- perform final execution
- define final archival structure

These should remain separate responsibilities.

### 3.5 Knowledge Is the Final Sink

Any output worth keeping must eventually be normalized and archived by the `Knowledge Agent` or a knowledge workflow.

### 3.6 Files Are the Long-Term Source of Truth

Important data must not live only inside:

- chat history
- hidden memory stores
- vector databases
- vendor-specific backends

Important outputs must be stored as files in a stable workspace.

### 3.7 High-Risk Actions Require Final Confirmation

The following actions must not run silently:

- publish
- delete
- send externally
- trade
- change critical configuration

These require explicit approval or a clearly defined permission rule.

---

## 4. Stable Architecture

The system should always be understood as four layers:

### 4.1 Core Layer

Responsible for:

- user identity
- preferences
- memory coordination
- routing
- workflow coordination
- permission control
- audit

### 4.2 Agent Layer

Responsible for domain-specific reasoning and task handling.

### 4.3 Tool and Workflow Layer

Responsible for:

- tool execution
- automation
- workflow steps
- structured outputs

### 4.4 Workspace Layer

Responsible for:

- file storage
- directory structure
- metadata
- indexing
- backup
- migration

If a future system keeps these four layers, the system remains portable.

---

## 5. Canonical Agent Set

### 5.1 Core Agents

The current canonical set is:

- `Life Agent`
- `Investment Agent`
- `General Intelligence Agent`
- `AI Research Agent`
- `Knowledge Agent`
- `Coding Agent`
- `Content Agent`

### 5.2 Optional Expansion Agent

- `Relationship and Collaboration Agent`

This agent is optional and should only be enabled when external communication and collaboration become a meaningful part of the workload.

---

## 6. Agent Roles

### 6.1 Life Agent

Owns:

- schedule
- reminders
- daily operations
- personal routines

Does not own:

- deep research
- code implementation
- investment judgment

### 6.2 Investment Agent

Owns:

- watchlists
- investment review
- risk tracking
- market-oriented synthesis

Does not own:

- automatic trading
- broad web scanning as its main role
- final external execution

### 6.3 General Intelligence Agent

Owns:

- broad information gathering
- feeds
- news summaries
- topic scanning

Does not own:

- deep AI-specialized research
- final archival decisions
- final publication

### 6.4 AI Research Agent

Owns:

- AI models
- AI products
- AI papers
- AI tools
- AI workflows
- AI trend judgment

Does not own:

- broad generic scanning as its final role
- final coding implementation
- final publication
- final archival control

### 6.5 Knowledge Agent

Owns:

- normalization
- tagging
- entity structure
- linking
- archival consistency

Does not own:

- original strategic judgment
- direct public publishing
- code implementation

### 6.6 Coding Agent

Owns:

- scripts
- tools
- code changes
- automation implementation

Does not own:

- final content strategy
- long-term knowledge governance
- investment decision authority

### 6.7 Content Agent

Owns:

- topic framing
- outlines
- drafts
- rewrites
- publication preparation

Does not own:

- long-term archival structure
- code implementation
- strategic investment judgment

### 6.8 Relationship and Collaboration Agent

Owns:

- contacts
- communication context
- meeting follow-up
- collaboration tracking
- relationship memory

Does not own:

- daily life operations
- investment judgment
- direct sensitive sending without confirmation

---

## 7. Agent Layering

To avoid overlap, agents should be grouped into stable layers.

### 7.1 Execution Layer

- `Life Agent`
- `Coding Agent`
- `Content Agent`

### 7.2 Research Layer

- `General Intelligence Agent`
- `AI Research Agent`
- `Investment Agent`

### 7.3 Knowledge Layer

- `Knowledge Agent`

### 7.4 Optional Relationship Layer

- `Relationship and Collaboration Agent`

The meaning of the layers is:

- execution layer: what should be done now
- research layer: what matters and why
- knowledge layer: what should be retained
- relationship layer: who matters and what needs follow-up

---

## 8. Default Routing Rules

### 8.1 Routing Principle

For any task:

1. choose the primary agent
2. choose supporting agents
3. choose the archive path
4. define approval points

### 8.2 Default Patterns

#### Pattern A: Intelligence -> Research -> Archive

Use for:

- trend tracking
- topical research
- investment signal review

Route:

`General Intelligence Agent` -> `AI Research Agent` or `Investment Agent` -> `Knowledge Agent`

#### Pattern B: Research -> Create -> Archive

Use for:

- articles
- scripts for videos
- public-facing analysis

Route:

`General Intelligence Agent` or `AI Research Agent` -> `Content Agent` -> `Knowledge Agent`

#### Pattern C: Research -> Build -> Archive

Use for:

- tools
- experiments
- automations

Route:

`AI Research Agent` or `Knowledge Agent` -> `Coding Agent` -> `Knowledge Agent`

#### Pattern D: Meeting / Contact -> Follow-Up -> Archive

Use for:

- meeting outcomes
- contact management
- collaboration progress

Route:

`Life Agent` or `Relationship and Collaboration Agent` -> `Relationship and Collaboration Agent` -> `Knowledge Agent`

### 8.3 Conflict Resolution

If more than one agent appears suitable:

1. the agent closest to the final output owns the task
2. the agent performing the high-risk action must be the final execution owner
3. archival ownership always belongs to the `Knowledge Agent`
4. research agents do not directly publish or externally send by default

---

## 9. Workspace Rules

### 9.1 Stable Workspace

All durable outputs must live in a stable workspace.

### 9.2 Domain-Based Storage

Store by domain and content type, not by temporary agent instance.

Preferred domain roots:

- `life`
- `invest`
- `intel`
- `knowledge`
- `dev`
- `content`
- `shared`
- `archive`

### 9.3 File-First Storage

Preferred durable formats:

- `md`
- `json`
- `yaml`
- `csv`
- source code files
- standard media formats

### 9.4 Metadata Is Required

Any durable document should include stable metadata.

Minimum metadata:

- `id`
- `title`
- `created_at`
- `updated_at`
- `domain`
- `type`
- `status`
- `tags`
- `visibility`

### 9.5 Relative References Only

Internal references should use:

- relative paths
- logical IDs

Avoid hardcoded machine-specific absolute paths inside portable data.

### 9.6 Rebuildable Indexes

Search indexes, vector indexes, and caches must be rebuildable from files.

---

## 10. Memory Rules

Memory must be split into two categories.

### 10.1 Fact Memory

Stable data such as:

- user preferences
- long-term goals
- project context
- contacts
- rules
- investment watchlists

### 10.2 Working Memory

Short-term data such as:

- current task context
- temporary plans
- drafts
- recent conversations
- in-progress workflow state

Rule:

working memory may expire;
fact memory should be explicitly managed.

---

## 11. Tool Rules

### 11.1 Tools Are Registered Objects

Every tool should have stable metadata:

- `id`
- `name`
- `description`
- `category`
- `input_schema`
- `output_schema`
- `permissions`
- `version`
- `status`

### 11.2 Tools Are Not Agents

Agents decide.
Tools execute.

Never mix these roles conceptually.

### 11.3 Tool Access Must Be Restricted

Not every agent may use every tool.

Tool access should be limited by:

- domain
- risk
- workflow stage
- explicit allowlists

---

## 12. Approval Rules

### 12.1 Low-Risk Actions

Usually safe without explicit confirmation:

- reading
- summarizing
- classifying
- drafting

### 12.2 Medium-Risk Actions

May require policy-based approval:

- writing internal files
- changing knowledge organization
- running scripts
- editing structured configs

### 12.3 High-Risk Actions

Require explicit confirmation:

- publishing
- deleting
- external sending
- financial actions
- credential changes
- major system configuration changes

---

## 13. Portability Rules

This rule file must remain valid across different AI systems.

Therefore:

### 13.1 No Vendor Lock-In in Core Logic

Core rules must not depend on:

- one model family
- one chat UI
- one vector database
- one orchestration framework

### 13.2 Keep Semantics Stable

Even if names change across systems, the following meanings must stay stable:

- core
- agent
- tool
- workflow
- memory
- workspace
- archive
- approval

### 13.3 Prefer Plain Files and Plain Schemas

Use portable formats wherever possible:

- Markdown
- JSON
- YAML
- CSV

### 13.4 Prompts Must Not Be the Only Specification

Important logic must exist in explicit documents and schemas, not only inside hidden prompts.

### 13.5 The System Must Survive Model Replacement

If the underlying model changes, the following should still remain usable:

- workspace
- files
- metadata
- agent roles
- routing rules
- approval rules

---

## 14. What Must Never Happen

The following are system failures:

- one agent silently doing research, execution, and archival all at once
- important knowledge existing only in chat history
- file structure depending on one model provider
- research agents directly executing high-risk external actions
- multiple agents competing as task owner
- durable assets stored only in unrecoverable indexes
- external communication happening without traceability

---

## 15. Minimal Portable Contract

Any future jarvis implementation is acceptable if it preserves at least:

1. one core orchestrator
2. clear domain agents
3. one-task-one-owner routing
4. knowledge as final archive sink
5. file-based durable workspace
6. stable metadata
7. explicit approval for high-risk actions
8. rebuildable indexes and caches
9. model-agnostic system semantics

---

## 16. Final Principle

`jarvis` should be treated as a long-lived personal system, not a temporary prompt setup.

Models may change.
Tools may change.
Interfaces may change.

The rules, workspace, and durable knowledge should remain.
