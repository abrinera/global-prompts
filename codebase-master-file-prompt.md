Analyse the codebase at <CODEBASE_ROOT>, then create or update these two files at its root:

1. AGENTS.md — concise repository guidance for future coding agents.
2. MASTER.md — the comprehensive, living codebase analysis and implementation record.

Complete the analysis before drafting either file. Adapt both documents to the actual codebase, whether it is a frontend, backend, full-stack application, monorepo, library, CLI, mobile application, or another kind of project.

This is a documentation task. Do not modify application source, configuration, dependencies, assets, or tests. Preserve unrelated working-tree changes. If the files already exist, reconcile them carefully rather than blindly replacing them.

ANALYSIS PROCESS

Before writing:

- Read applicable repository instructions, including existing AGENTS.md files and their scope.
- Inspect existing documentation, implementation plans, manifests, lockfiles, build configuration, tests, CI workflows, deployment configuration, and relevant tooling.
- Inventory authored files, including relevant hidden configuration and tooling directories. Use rg or equivalent tools where available.
- Inspect actual source and trace entry points, module boundaries, important imports, routes or commands, data flow, storage, authentication, integrations, and representative end-to-end workflows.
- Distinguish dependencies declared or installed from dependencies actually used.
- Distinguish active functionality from mocks, placeholders, disabled features, unused code, and generated files.
- Inspect Git branch, HEAD, and working-tree status where available. Record unavailable metadata honestly.
- Compare existing documentation with the resulting source. Resolve contradictions in current-state descriptions while preserving historical records.
- Reference source paths supporting important architectural and behavioral claims.
- State analysis coverage and any areas that could not be inspected. Do not describe uninspected areas as confirmed.

Source and actual consumers define implemented behavior. Documentation and comments provide context but may be outdated.

Do not infer working integrations from an API client, installed SDK, interface, or environment variable alone. Trace actual callers and configuration.

Never print or copy credentials, tokens, private keys, personal data, or configured environment values. Document configuration names, purpose, requiredness, validation, and loading precedence without exposing values.

Prefer source inspection for this documentation task. Do not install dependencies, run builds or tests, start servers, or contact external services unless separately requested or required by applicable instructions. Inventory available verification commands and clearly mark checks that were not run.

AGENTS.md REQUIREMENTS

Keep this file concise, specific, and actionable. Link to MASTER.md using a relative Markdown link.

Include these standing rules:

1. Before changing code, configuration, dependencies, assets, tests, or documentation, read MASTER.md and inspect the affected source and applicable scoped instructions.

2. In the same work item as every change, reconcile all affected Codebase Analysis subsections in MASTER.md against the resulting source. Update or remove obsolete statements. A change-log entry alone is insufficient.

3. Keep the current snapshot, change tracker, implementation progress, and verification summary consistent with the latest evidence.

4. Keep the annotated repository tree complete and current. Update entries when files are added, removed, moved, or change responsibility. Update architecture and execution-flow diagrams when their structure changes.

5. If a change does not affect architecture or behavior, add a dated reconciliation note explaining that conclusion.

6. Preserve earlier verification and change-log entries as history. Historical behavior must not remain presented as current behavior.

7. Record only checks actually performed. Distinguish source inspection, compilation, automated tests, runtime checks, and real external integrations. Follow the user's current testing instructions.

8. Preserve unrelated user changes and protect sensitive information.

Add repository-specific guidance supported by existing instructions and observed conventions: module boundaries, styling ownership, generated-file handling, dependency management, migration practices, or relevant development commands.

Clearly distinguish explicit requirements from observed conventions and recommendations. Document legacy exceptions where necessary.

Do not impose technology-specific rules from another project. For example, do not prescribe Tailwind, React, or a global-only index.css convention unless this repository supports that guidance.

MASTER.md REQUIREMENTS

Write a substantial engineering record grounded in inspected source. Use clear prose, relative file links, tables, annotated trees, and compact diagrams where useful.

Use this structure:

# Codebase Analysis & Implementation Record

## Purpose
Explain the document's scope, its maintenance role, and its relationship to AGENTS.md. State that current source is authoritative.

## Document Control
Include:
- Repository and analysis scope.
- Project type and purpose.
- Branch, HEAD, and relevant working-tree state.
- Last reconciliation date and known timezone.
- Frameworks, languages, runtime, and package/build tools.
- Active work, if established by evidence.
- Analysis coverage and limitations.

Do not invent timestamps, Git metadata, ownership, or active work.

## Source of Truth and Update Rules
Explain how source, configuration, actual consumers, verification evidence, and historical documentation are reconciled.

Require updates in the same work item as changes, complete architecture inventories, preservation of history, and exclusion of sensitive values.

## Status Legend
Define:
- Implemented: supporting source exists and the described functionality is connected to its consumers.
- Partially implemented: meaningful parts exist, with specified missing pieces.
- Verified: a named check passed for a stated scope and date.
- Partially verified: some checks passed, with remaining checks identified.
- Not verified: no relevant execution evidence.
- Deferred: explicitly accepted work outside the current scope.
- Unknown: insufficient evidence.

Implementation and verification are separate dimensions. Identify inactive or disabled implementations explicitly.

## Current Codebase Snapshot
Provide a concise table covering the main subsystems, capabilities, data sources, integrations, persistence, tooling, and verification status.

Describe the latest known state. Do not repeat outdated baseline results as current results.

## Current Change Tracker
Record:
- Work item and objective.
- Scope and status.
- Affected files.
- Behavior or architecture changes.
- Checks actually performed.
- Remaining work and limitations.

If this task only establishes documentation, identify it as a documentation baseline. Do not invent an application implementation project.

# Codebase Analysis

Include these common subsections:

## Technology Stack and Build
Explain dependencies actually used, runtime requirements, configuration, scripts, and build behavior.

## Repository Directory Architecture
Provide a complete annotated tree of authored files within scope, with each file's responsibility.

Include relevant configuration, tests, tooling, CI, and documentation. Identify dependency, generated, build, cache, vendor, and local-only areas by role without enumerating their generated contents.

Treat locally maintained component or framework source as repository-owned code.

For large repositories, split the inventory into package or subsystem trees while maintaining coverage.

## Entry Points and Execution Architecture
Explain startup, composition, module boundaries, providers or middleware, and important execution paths.

## Feature and Capability Inventory
Describe implemented behavior, entry points, supporting files, state changes, errors, and limitations. Identify mocks, placeholders, inactive code, and unfinished functionality.

Add other subsections appropriate to the repository, including:
- Routes, navigation, public APIs, or CLI commands.
- Authentication, sessions, authorization, and trust boundaries.
- Domain models, schemas, and validation.
- Data sources, databases, migrations, caching, and persistence.
- Client state, server state, and ownership of state.
- External integrations and their actual callers.
- UI components, styling, responsive behavior, and accessibility.
- Jobs, queues, scheduled tasks, polling, and real-time behavior.
- File handling and asset processing.
- Configuration, environment loading, and feature switches.
- Error handling, logging, and observability.
- CI, deployment, infrastructure, and operational requirements.

Adapt names and detail to the project. Do not force frontend sections onto a backend or invent missing systems.

## Test Inventory and Verification Baseline
Map existing tests to their actual coverage. List supported verification commands discovered in repository configuration.

Separate historical results, checks performed during this task, source-only findings, and unverified behavior. Passing a build does not establish runtime correctness. Mock checks do not establish real integration correctness.

## Known Issues
List confirmed issues with evidence. Label suspected risks and unknowns separately. Do not present an unexecuted check as a known failure.

## Technical Debt
Describe concrete maintenance concerns grounded in source.

## Deferred Decisions
Record explicitly deferred work. Keep suggested improvements separate from accepted scope.

# Implementation Progress
Organize progress by actual subsystem or workstream.

Use checklists or tables showing implementation status, verification status, evidence, and remaining work. Do not invent an approved roadmap or treat every absent feature as a defect.

## Pending Requests and Handoff
Record established outstanding requests, dependencies, unresolved questions, and the next actionable steps. State when none are established.

## Future Update Workflow and Architecture Drift
Describe the required read → inspect → change → reconcile → verify → record workflow.

Include a change-impact table mapping common change types to the analysis sections that need review. Require checking indirect effects as well.

## Verification Log
Use an append-only table:
Date | Work item / scope | Command or inspection | Result | Limitations

Record only actual actions and results. Preserve imported historical results with their original attribution and scope.

## Change Log
Use an append-only table:
Date | Work item | Change | Affected files / areas | Verification

For initial generation, record the documentation work actually completed. Preserve existing history when updating.

FINAL VALIDATION

Before finishing:

- Check that both filenames are exactly AGENTS.md and MASTER.md.
- Check that AGENTS.md links to MASTER.md.
- Verify relative links, headings, tables, and code fences.
- Compare the annotated tree with the actual file inventory.
- Check consistency across the snapshot, tracker, analysis, progress, issues, and verification records.
- Remove stale current-state claims while preserving historical entries.
- Ensure important claims have identifiable source evidence.
- Ensure no invented history, test results, integrations, requirements, or sensitive values appear.
- Confirm only the requested documentation files were changed.

If filesystem access is available, write the files and report their paths, analysis coverage, checks performed, and material limitations.

If filesystem access is unavailable, provide the complete contents of both files, clearly labelled AGENTS.md and MASTER.md.