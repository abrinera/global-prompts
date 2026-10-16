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
- `MASTER.md` — a comprehensive engineering record of the codebase and how it works

### What the agent is expected to do

- Read repository instructions and any existing documentation
- Inspect the real source code, build files, configs, tests, and tooling
- Identify the project type, architecture, entry points, dependencies, and subsystem boundaries
- Distinguish real implementation from mocks, placeholders, generated content, and unused code
- Document the technology stack and build process
- Explain the repository's execution flow, major capabilities, and data flows
- Capture verification status honestly without inventing test results
- Update the docs in a way that reflects actual code, not assumptions

### Best use case

Use this when you want a single, strong documentation baseline for a repository—especially for a smaller project, a single developer workflow, or an initial repo audit.

This prompt is focused on creating a maintainable master analysis that becomes the source of truth for future agent work.

## Prompt 2: `multi-developer-codebase-documentation-prompt.md`

### What it does

This is the advanced, team-scale documentation system prompt.

It goes beyond a single `MASTER.md` and creates a more structured documentation architecture for multi-developer and multi-agent environments.

### What the agent is expected to do

- Build a documentation system that supports parallel contributors without constant merge conflicts
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

### Documentation structure it establishes

The prompt defines a model like this:

- `AGENTS.md`
- `MASTER.md`
- `docs/codebase/`
- `docs/work-items/`
- `docs/history/`

This is designed to keep documentation maintainable at scale while preserving history and avoiding unnecessary shared-file edits.

### Best use case

Use this when:

- multiple developers are working on the same repo
- several AI agents may be contributing simultaneously
- the repo is large or complex
- you need a documentation system that avoids shared-file churn and merge conflicts
- you want task-level records and architecture reconciliation instead of one giant documentation file

## Why both prompts exist

The two prompts solve slightly different problems:

- `codebase-master-file-prompt.md` is the simpler, more direct “analyze repo and produce AGENTS.md + MASTER.md” workflow.
- `multi-developer-codebase-documentation-prompt.md` is the stronger operational system for scale, concurrency, and team collaboration.

If you are documenting a single repository for a solo developer or a first-pass audit, start with the first prompt.

If you are documenting a repo that will have multiple contributors or AI agents, the second prompt is the better choice.

## How to use these prompts

Paste the contents of one of the prompt files into a coding agent and provide the repository root or codebase path.

Example:

- “Analyze this repo at `<CODEBASE_ROOT>` and apply the instructions in `codebase-master-file-prompt.md`.”
- “Use the multi-developer workflow in `multi-developer-codebase-documentation-prompt.md` for this repo.”

The prompts are designed to be reusable, not repo-specific. They work by guiding the agent to inspect the actual source and generate documentation from evidence instead of assumptions.

## Summary

This repo provides reusable prompt templates for codebase understanding and documentation generation.

- The first prompt creates the standard master documentation baseline.
- The second prompt creates a more scalable documentation system for teams and multi-agent work.

Together they help AI agents produce documentation that is more accurate, more maintainable, and better aligned with how real repositories evolve.
