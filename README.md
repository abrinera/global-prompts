# Global Prompts

Reusable prompts for AI coding agents that help standardize how repositories are analyzed, documented, and maintained.

This repo is intentionally small and focused: each prompt is designed to be copied into an AI coding agent to guide it through a specific kind of repository work.

## Repository contents

- `codebase-master-file-prompt.md`
- `multi-developer-codebase-documentation-prompt.md`

## Prompt 1: `codebase-master-file-prompt.md`

### What it does

This is the foundational documentation prompt.

It tells an AI agent to inspect an existing codebase and generate or update two root-level documents:

- `AGENTS.md` — concise operational guidance for future coding agents
- `MASTER.md` — a comprehensive, living engineering record of the codebase and how it works

### What the agent is expected to do

- Read repository instructions and any existing documentation
- Inspect the real source code, build files, configs, tests, CI, and tooling
- Identify the project type, architecture, entry points, dependencies, and subsystem boundaries
- Distinguish dependencies that are actually used from ones that are only declared or installed
- Distinguish real implementation from mocks, placeholders, generated content, and unused code
- Document the technology stack and build process
- Explain the repository's execution flow, major capabilities, and data flows
- Capture verification status honestly without inventing test results
- Update the docs in a way that reflects actual code, not assumptions
- Run a final validation pass (filenames, links, tree vs. actual files, consistency across sections, no invented or sensitive content)

### Safety boundaries

- **Documentation only** — it must not modify application source, configuration, dependencies, assets, or tests.
- **Reconciles, never blindly replaces** — existing `AGENTS.md` / `MASTER.md` are merged carefully and unrelated working-tree changes are preserved.
- **Source inspection by default** — it does not install dependencies, run builds or tests, start servers, or call external services unless you ask. Checks that were not run are marked as such.
- **No secrets** — credentials, tokens, keys, and environment values are never copied; only configuration names and purpose are documented.

### What `AGENTS.md` enforces

The generated `AGENTS.md` contains standing rules for every future agent, most importantly: **every change must reconcile the affected sections of `MASTER.md` in the same work item**, keep the repository tree and diagrams current, preserve history, and record only checks actually performed.

### What `MASTER.md` contains

- Purpose, document control (branch, HEAD, scope, coverage), and source-of-truth rules
- A status legend separating implementation status (Implemented / Partial / Deferred / Unknown) from verification status (Verified / Partially verified / Not verified)
- Current codebase snapshot and current change tracker
- Codebase analysis: tech stack, complete annotated directory tree, entry points, feature inventory, plus project-specific sections (APIs, auth, data, state, integrations, UI, jobs, config, CI/deployment)
- Test inventory, known issues, technical debt, deferred decisions
- Implementation progress, pending requests and handoff, and a change-impact table for future updates
- Append-only verification log and change log

### Best use case

Use this when you want a single, strong documentation baseline for a repository—especially for a smaller project, a single developer workflow, or an initial repo audit.

This prompt is focused on creating a maintainable master analysis that becomes the source of truth for future agent work.

## Prompt 2: `multi-developer-codebase-documentation-prompt.md`

### What it does

This is the advanced, team-scale documentation system prompt.

It goes beyond a single `MASTER.md` and creates a more structured documentation architecture for multi-developer and multi-agent environments. Crucially, `MASTER.md` becomes a **stable high-level reference that is not updated after routine changes**; per-task progress, verification, and change logs live in separate work-item files so contributors don't all edit the same document.

### Operating modes

- **Mode A — Initial setup / migration:** analyze the codebase, build the documentation structure, and migrate any existing single-file `MASTER.md` into it. Documentation only; no source changes.
- **Mode B — Ongoing development:** used on every later task. The agent reads only the relevant docs, inspects the affected source, implements, and updates its own work-item record plus any genuinely affected architecture docs. No full repo re-analysis.

### What the agent is expected to do

- Build a documentation system that supports parallel contributors with minimal unnecessary merge conflicts
- Maintain a root-level `AGENTS.md` and `MASTER.md`
- Add structured docs under `docs/` for:
  - codebase architecture and subsystem analysis
  - work-item records for specific tasks
  - historical or legacy documentation
- Keep documentation source-grounded and architecture-aware
- Support concurrent development and multi-agent workflows safely
- Record implementation progress and verification evidence per work item
- Reconcile architecture changes without forcing all contributors to edit the same central file
- Protect against overwriting another contributor's work or creating stale shared docs
- Keep documentation context-efficient: agents read only what is relevant to their task

### Documentation structure it establishes

```text
AGENTS.md                         # rules every agent follows
MASTER.md                         # stable, high-level architecture + navigation
docs/
├── codebase/                     # detailed per-subsystem analysis
│   ├── overview.md
│   ├── architecture.md
│   └── <subsystem>.md
├── work-items/
│   └── <TASK-ID>/
│       └── <UNIQUE-WORK-UNIT-ID>.md   # one record per independent work unit
└── history/                      # legacy records that can't be attributed to a work unit
```

Each work-unit record has one editor at a time, keeps its current state at the top, and carries its own progress table, verification log, change log, architecture-reconciliation notes, and handoff section. There is no shared index or change log that everyone must edit.

`MASTER.md` may only change when high-level architecture, major subsystems, cross-cutting decisions, or navigation change—not because a feature was completed, a test passed, or a file was added.

### Mandatory workflow

Every future agent follows: **READ → INSPECT → IMPLEMENT → RECONCILE → VERIFY → RECORD**.

### Concurrency and Git safety

The prompt covers four scenarios: a solo developer, multiple developers on separate branches, multiple developers on the **same** branch, and multiple AI agents running in parallel. Key rules:

- Unique work-unit IDs regardless of branch name; never edit another active work unit's record
- Fetch and integrate upstream before publishing; never force-push over others' work
- Stage and commit only files belonging to the current work unit
- Run parallel agents in isolated clones or Git worktrees, not one shared working tree
- When work units overlap on shared architecture, assign one reconciler and mark docs as pending until reconciled against the integrated source

It reduces documentation conflicts but explicitly does **not** guarantee conflict-free merges, especially for shared application code.

### Safety boundaries

Same as Prompt 1: no secrets, no invented history, test results, ownership, or Git metadata, and source inspection by default during initial setup.

### Best use case

Use this when:

- multiple developers are working on the same repo
- several AI agents may be contributing simultaneously
- the repo is large or complex
- you need a documentation system that minimizes shared-file churn and merge conflicts
- you want task-level records and architecture reconciliation instead of one giant documentation file

## Why both prompts exist

| | Prompt 1 — master file | Prompt 2 — multi-developer |
|---|---|---|
| Output | `AGENTS.md` + `MASTER.md` | `AGENTS.md` + `MASTER.md` + `docs/` tree |
| Where task logs live | Inside `MASTER.md` | Per work-unit file in `docs/work-items/` |
| Updating `MASTER.md` | On every change | Only on high-level architecture changes |
| Used for | One-time baseline (rules then guide future changes) | Initial setup **and** every later task (Mode A / B) |
| Concurrency / Git rules | Not covered | Detailed |
| Best for | Solo work, small repos, first-pass audits | Teams, parallel agents, large repos |

If you are documenting a single repository for a solo developer or a first-pass audit, start with the first prompt.

If you are documenting a repo that will have multiple contributors or AI agents, the second prompt is the better choice.

**Upgrade path:** you can start with Prompt 1 and later run Prompt 2 in Mode A. Prompt 2 migrates the existing `MASTER.md` content into `docs/codebase/`, `docs/work-items/`, and `docs/history/` without losing information.

## How to use these prompts

1. Copy the contents of one of the prompt files.
2. Replace `<CODEBASE_ROOT>` with the path to the repository.
3. Paste it into your coding agent.

Alternatively, if the agent can read this repo, point it at the file:

- “Analyze this repo at `<CODEBASE_ROOT>` and apply the instructions in `codebase-master-file-prompt.md`.”
- “Use the multi-developer workflow in `multi-developer-codebase-documentation-prompt.md` for this repo.”

If the agent has filesystem access, it writes the files and reports paths, coverage, checks performed, and limitations. If not, it outputs the complete file contents instead of claiming they were created.

The prompts are designed to be reusable, not repo-specific. They work by guiding the agent to inspect the actual source and generate documentation from evidence instead of assumptions.

## Summary

This repo provides reusable prompt templates for codebase understanding and documentation generation.

- The first prompt creates the standard master documentation baseline.
- The second prompt creates a more scalable documentation system for teams and multi-agent work.

Together they help AI agents produce documentation that is more accurate, more maintainable, and better aligned with how real repositories evolve.
