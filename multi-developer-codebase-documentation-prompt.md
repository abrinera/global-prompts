# Multi-Developer & Multi-Agent Codebase Documentation System

Analyse the codebase at `<CODEBASE_ROOT>` and create or update a comprehensive, continuously maintained engineering documentation system that supports **individual developers, multiple developers, and parallel AI coding agents working on the same repository, whether on separate branches or a shared branch**.

The documentation must remain accurate, structured, easy for AI agents to understand, efficient to maintain, and resistant to Git merge conflicts.

Preserve the depth of the existing codebase analysis and implementation tracking while eliminating the requirement for every contributor to modify the same central documentation file.

**Primary objectives:**
- Maintain comprehensive, source-grounded codebase knowledge.
- Provide AI agents with accurate, task-relevant context.
- Track implementation progress, decisions, verification, and history.
- Support concurrent development without unnecessary shared-file modifications.
- Prevent documentation overwrites, stale architectural claims, and accidental loss of changes.
- Minimise repeated codebase analysis and unnecessary context consumption.
- Keep documentation consistent with the actual integrated source code.

---

# 1. Operating Modes

Determine which mode applies before proceeding.

### Mode A — Initial Documentation Setup

Use when establishing the documentation system or migrating an existing single-file documentation approach.

- Analyse the existing codebase thoroughly before writing documentation.
- Create or reconcile the required documentation structure.
- Preserve existing accurate documentation, historical records, and developer changes.
- Migrate existing MASTER.md information into appropriate documents without losing important knowledge.
- Create a documentation baseline based on inspected source.
- Do not modify application source, configurations, dependencies, tests, or assets.

### Mode B — Ongoing Development Documentation

Use automatically during future implementation work.

- Read the relevant documentation before modifying code.
- Inspect actual affected source and dependencies.
- Create or update only the current work unit's documentation and necessary affected architecture records.
- Reconcile documentation against resulting source changes.
- Record implementation progress and verification evidence.
- Avoid modifying unrelated or centrally shared documents.

Never repeat a full repository analysis when focused inspection and existing documentation are sufficient.

---

# 2. Documentation Architecture

Use the following structure, adapting subsystem names to the actual project:

```text
<CODEBASE_ROOT>/
│
├── AGENTS.md
├── MASTER.md
│
└── docs/
    │
    ├── codebase/
    │   ├── overview.md
    │   ├── architecture.md
    │   ├── <subsystem-a>.md
    │   ├── <subsystem-b>.md
    │   └── ...
    │
    ├── work-items/
    │   ├── <TASK-ID>/
    │   │   ├── <UNIQUE-WORK-UNIT-ID>.md
    │   │   └── ...
    │   └── ...
    │
    └── history/
        └── <legacy-records-if-needed>.md
```

Do not create unnecessary placeholder files or directories.

Organise subsystem documentation according to the repository's actual architecture and meaningful responsibility boundaries.

The architecture must support frontend, backend, full-stack, monorepo, mobile, library, CLI, and other project types.

---

# 3. AGENTS.md — Repository-Wide Instructions

Create or reconcile `AGENTS.md` as the entry point for future coding agents.

Keep it concise, stable, and actionable.

Include instructions requiring every agent to:

1. Read MASTER.md before starting development work.
2. Identify and read only the relevant subsystem documentation.
3. Read the assigned work-unit record, if one already exists.
4. Inspect the actual affected source before making changes.
5. Follow applicable scoped AGENTS.md instructions.
6. Preserve established architectural conventions and module boundaries.
7. Maintain its assigned work-unit record throughout implementation.
8. Reconcile documentation impacted by its changes.
9. Avoid modifying unrelated documentation or another contributor's work record.
10. Preserve unrelated working-tree changes and protect sensitive information.
11. Record only checks actually performed.
12. Follow the repository's concurrency and Git integration rules.

Link to MASTER.md using a relative Markdown link.

Include repository-specific guidance supported by inspected source, such as:
- Module boundaries and ownership.
- Coding conventions.
- State and data ownership.
- Dependency management.
- Generated-file handling.
- Migration practices.
- Testing expectations.
- Development and deployment commands.

Distinguish explicit requirements from observed conventions and recommendations.

Do not introduce technology-specific rules unsupported by the repository.

**Important:** AGENTS.md must not require every developer to update MASTER.md after every implementation change.

---

# 4. MASTER.md — Central Engineering Reference

MASTER.md must remain the central entry point for understanding the repository.

It must contain stable, high-value engineering context rather than frequently changing implementation logs.

Use the following structure:

## Purpose
Explain the repository's purpose, documentation system, and relationship to AGENTS.md.

## Document Control
Include:
- Repository and analysis scope.
- Project type and purpose.
- Frameworks, languages, runtime, and build tools.
- Baseline branch and commit, where available.
- Last source reconciliation revision and date, when verifiable.
- Analysis coverage and limitations.

Do not invent metadata.

## Source of Truth
Define the precedence of:
1. Actual source and configuration.
2. Connected consumers and real execution paths.
3. Relevant verification evidence.
4. Current subsystem documentation.
5. Historical implementation records.

Source code remains authoritative for implemented behaviour.

## High-Level Architecture
Document:
- Major applications, services, and packages.
- Their responsibilities and boundaries.
- Important execution and data flows.
- Cross-cutting architectural decisions.
- Authentication and authorization boundaries.
- Persistence and external integration overview.
- Important operational dependencies.

Include compact diagrams when useful.

## Technology Stack
Summarise technologies actually used by the application.

Distinguish installed or declared dependencies from those connected to real application functionality.

## Subsystem Documentation
Provide relative links to the detailed documents under docs/codebase/.

Explain which documents apply to which parts of the repository.

## Development Conventions
Record durable repository-wide conventions and constraints.

## Documentation Maintenance Rules
Explain:
- Document ownership.
- Task-level change tracking.
- Architecture reconciliation.
- Verification recording.
- Concurrent development safeguards.
- Historical record preservation.
- When MASTER.md itself may be modified.

## Known Architectural Limitations
Include only significant, source-supported, cross-cutting limitations.

Keep detailed issues and local technical debt in the appropriate subsystem or work-unit records.

### MASTER.md Modification Rules

MASTER.md may be updated only when:
- High-level architecture materially changes.
- A new major subsystem is introduced or removed.
- Cross-cutting architectural decisions change.
- Documentation navigation requires updating.
- Existing high-level information becomes incorrect.

Do not update MASTER.md merely because:
- A feature was completed.
- A developer committed code.
- A test passed.
- A file was added inside an existing subsystem.
- A task's implementation status changed.
- A developer needs to append a change-log entry.

Do not maintain frequently edited shared task trackers, implementation logs, verification logs, or developer-specific status tables in MASTER.md.

Use targeted modifications instead of rewriting the complete file.

---

# 5. docs/codebase/ — Comprehensive Codebase Analysis

Maintain detailed, source-grounded architecture and implementation analysis in separately maintained subsystem documents.

During initial setup, analyse:

- Applicable repository instructions.
- Existing documentation and plans.
- Repository structure and authored files.
- Hidden configuration and tooling directories.
- Manifests, lockfiles, frameworks, and build configuration.
- Application entry points.
- Module and package relationships.
- Routes, commands, and public APIs.
- Authentication, sessions, and authorization.
- Domain models, schemas, and validation.
- Data sources, databases, caching, and persistence.
- Client-side and server-side state ownership.
- External integrations and actual consumers.
- UI components, styling, responsiveness, and accessibility, where applicable.
- Jobs, queues, polling, and background processing.
- File handling and asset processing.
- Environment configuration and feature flags.
- Error handling, logging, and observability.
- Testing, CI/CD, deployment, and infrastructure.
- Existing issues, technical debt, and deferred decisions.

Trace actual functionality rather than assuming that installed packages, API clients, SDKs, or environment variables represent working integrations.

Clearly distinguish active functionality from mock implementations, placeholders, disabled code, unused code, and generated files.

## Required Subsystem Document Content

Each relevant subsystem document should contain:

### Overview
Purpose, responsibilities, and module boundaries.

### Technology and Dependencies
Technologies and dependencies actually used.

### Directory Architecture
A complete annotated inventory of authored files within the subsystem's defined scope.

Include relevant source, configuration, tests, tooling, and documentation.

Identify generated, dependency, cache, build, vendor, and local-only areas without enumerating their generated contents.

### Entry Points and Execution Flow
Explain module composition, important imports, execution paths, and data flow.

### Feature and Capability Inventory
Document:
- Implemented functionality.
- Partially implemented functionality.
- Mocks and placeholders.
- Disabled or inactive functionality.
- Relevant limitations.

### Interfaces and Contracts
Describe applicable routes, APIs, schemas, models, events, or commands.

### State and Persistence
Explain state ownership, database or storage access, caching, and relevant migrations.

### Integrations
Identify connected external integrations, actual callers, configuration requirements, and limitations.

### Error Handling and Observability
Describe error propagation, logging, monitoring, and relevant fallback behaviour.

### Verification Baseline
Document:
- Available tests.
- Their actual coverage.
- Relevant verification commands.
- Verified behaviour.
- Unverified behaviour.

### Known Issues and Technical Debt
Separate confirmed issues from suspected risks and unknowns.

### Deferred Decisions
Record accepted deferrals separately from unapproved improvements.

### Source Evidence and Coverage
Reference supporting source paths for important architectural and behavioural claims.

Record areas that could not be inspected.

Adapt headings to the subsystem rather than forcing irrelevant sections.

## Subsystem Documentation Rules

- Keep documentation divided by meaningful subsystem boundaries.
- Avoid one enormous shared architecture document.
- Maintain complete inventory coverage across the collection of subsystem documents.
- Do not duplicate mutable information unnecessarily.
- Update only the documentation affected by the change.
- Preserve valid historical information where appropriate.
- Do not present historical behaviour as current behaviour.
- Avoid unrelated formatting changes or section reordering.
- Reconcile indirect architectural impacts, not only directly modified files.

Where independently owned features frequently change the same subsystem document, split the document further when meaningful architectural boundaries permit.

Do not fragment documentation solely to avoid coordinating genuinely shared architectural changes.

---

# 6. docs/work-items/ — Independent Implementation Records

Each independent development work unit must have its own Markdown record.

Use:

`docs/work-items/<TASK-ID>/<UNIQUE-WORK-UNIT-ID>.md`

A work unit may represent:
- An entire independently assigned ticket.
- A subtask of a shared ticket.
- A separately assigned implementation component.
- An independent AI agent work assignment.

The identifier must be stable and collision-resistant across developers, agents, machines, and branches.

Use existing ticket or work identifiers when available. Supplement them with an independently assigned work-unit identifier where multiple contributors share the same ticket.

Never use a branch name, generic developer name, or timestamp alone as the unique identifier.

Check for existing records before choosing a new path.

Do not invent official ticket IDs.

## Required Work-Unit Structure

### 1. Work Item Information
- Task ID and unique work-unit ID.
- Objective.
- Assigned scope.
- Branch and relevant revision, when available.
- Dependencies.
- Related subsystem documentation.
- Implementation and verification status.

### 2. Current State
Keep this section at the beginning of the record.

Include:
- Latest completed work.
- Current work in progress.
- Immediate next steps.
- Blockers.
- Relevant unresolved questions.

Keep this section concise and up to date.

### 3. Scope and Affected Files
Record:
- Files added, modified, moved, or removed.
- Affected modules.
- Relevant interfaces and dependencies.
- Potential cross-subsystem impact.

### 4. Implementation Changes
Explain:
- Changes actually implemented.
- Behavioural changes.
- Architectural decisions.
- API or schema changes.
- Configuration changes.
- Important implementation limitations.

### 5. Implementation Progress
Use a checklist or table with:
- Work component.
- Implementation status.
- Verification status.
- Evidence.
- Remaining work.

### 6. Verification Summary
Distinguish:
- Source inspection.
- Compilation or type checking.
- Automated tests.
- Manual or runtime verification.
- Mock-based verification.
- Real external integration verification.

Never infer runtime correctness from a passing build.

### 7. Architecture Reconciliation
Record:
- Affected subsystem documentation.
- Descriptions reconciled.
- Source evidence checked.
- Indirect effects reviewed.
- Outstanding shared-document updates.

If a change does not affect architecture or behaviour, record a dated explanation of that conclusion.

### 8. Known Issues and Remaining Work
Include:
- Confirmed issues.
- Unverified areas.
- Accepted deferrals.
- Blockers and dependencies.
- Required follow-up actions.

### 9. Verification Log
Maintain an append-only table:

`Date | Scope | Command or inspection | Result | Limitations`

Record only checks actually performed.

### 10. Change Log
Maintain an append-only table:

`Date | Work item | Change | Affected files | Verification`

Preserve previous entries as history.

### 11. Handoff
Provide enough context for another developer or AI agent to continue without re-analysing the entire project.

Include the next actionable step and any unresolved integration or reconciliation requirements.

## Work-Unit Ownership Rules

- Each work-unit record has one designated editor at a time.
- Agents must not overwrite records owned by another active work unit.
- Multiple developers working on the same ticket must maintain separate records when their work is independently managed.
- A handoff may transfer ownership of an existing record.
- Do not create duplicate records for the same continuing work unit merely because another agent resumes it.
- Historical entries must not be deleted or silently rewritten.
- Do not create a shared mutable work-item index that every developer must update.

---

# 7. Concurrent Development and Git Safety

The documentation system must support the following scenarios.

## Scenario A — Individual Developer

One developer works on a repository.

Use the normal documentation workflow.

Update the assigned work-unit record and any genuinely affected architecture documents.

Do not unnecessarily modify MASTER.md.

## Scenario B — Multiple Developers on Separate Branches

Different developers work on independent branches.

Rules:
- Each work unit has its own documentation path.
- Contributors update only their assigned records and relevant architecture.
- Avoid unrelated shared-document edits.
- Preserve all independent records when branches merge.
- Reconcile overlapping architecture changes against the integrated source.

Independent task records must not require updates to a common change log or progress table.

## Scenario C — Multiple Developers on the Same Branch

Multiple developers work on the same Git branch, potentially from different computers or independent clones.

Rules:
1. Allocate unique work-unit records regardless of branch name.
2. Never assume a branch belongs to one developer.
3. Do not modify another active work unit's record.
4. Fetch and integrate upstream changes safely before publishing local commits.
5. Detect non-fast-forward updates rather than overwriting remote history.
6. Never force-push over another contributor's work.
7. Stage and commit only files belonging to the current work unit and explicitly coordinated shared changes.
8. Preserve unrelated local and remote modifications.
9. Coordinate overlapping source-code or architecture changes.
10. Do not resolve conflicts by choosing one contributor's changes without checking the integrated behaviour.

A separate documentation file prevents routine documentation conflicts but does not eliminate conflicts involving shared application code.

## Scenario D — Multiple AI Agents Working Concurrently

Parallel agents must have clearly defined work scopes.

Each agent must know:
- Its assigned work-unit ID.
- Its source-code scope.
- Its documentation record.
- Its dependencies.
- Which shared files may require coordination.

When agents run concurrently:
- Prefer isolated clones or Git worktrees.
- Do not let agents independently modify the same working tree without explicit file-level coordination.
- Avoid concurrent commits, checkouts, rebases, or other Git index operations in a shared working directory.
- Do not allow one agent to overwrite another agent's uncommitted changes.
- Use separate local branches or detached worktrees as appropriate when isolated worktrees are required; Git normally does not allow the same local branch to be checked out in multiple worktrees.
- Integrate concurrent changes through a controlled process.

Do not assume that different AI agent sessions provide filesystem isolation.

## Shared-File Conflict Handling

Before editing shared architecture or configuration files:

1. Inspect the latest available file and source state.
2. Check for overlapping active changes when that information is available.
3. Determine whether the change can be safely isolated.
4. Apply the smallest necessary modification.
5. Preserve unrelated contributions.
6. Validate the resulting integrated behaviour.

If concurrent modifications are incompatible or ownership is unclear:
- Record the conflict and proposed resolution in the current work-unit file.
- Avoid uncoordinated overwrites.
- Request integration coordination or explicit resolution before modifying conflicting shared content.

Do not invent a locking mechanism unless the repository actually supports it.

---

# 8. Architecture Reconciliation During Parallel Development

Architecture documentation must remain consistent with the integrated source code.

However, unrelated developers must not be forced to edit the same document simultaneously.

Use the following approach.

### Independent Changes

If a work unit modifies only its own subsystem:
- Update its work-unit record.
- Reconcile its owned subsystem documentation.
- Leave unrelated documentation unchanged.

### Shared Architecture Changes

If two or more work units affect the same subsystem or architectural contract:

1. Each work unit independently documents its changes and source evidence.
2. Identify overlaps in architecture, contracts, or assumptions.
3. Assign reconciliation ownership for the affected shared document.
4. The responsible contributor or integrator reconciles the documentation against the combined source.
5. Preserve relevant decisions and verification history in the individual work-unit records.
6. Resolve contradictory descriptions before declaring the shared architectural documentation current.

For a shared branch, perform reconciliation after the relevant concurrent changes have been integrated into a consistent revision. Do not assume that a separate branch merge will necessarily occur.

If reconciliation cannot yet be safely completed:
- Record the outstanding documentation impact in the work-unit record.
- Identify the affected subsystem and source revision.
- Do not falsely claim the shared document is current.
- Ensure agents validate the affected source rather than relying on potentially stale descriptions.
- Keep the work item explicitly pending reconciliation until resolved.

For significant changes, document the revision against which architecture was reconciled.

Never treat an outdated architectural document as authoritative merely because it exists.

---

# 9. Mandatory Development Workflow

All future coding agents must follow:

**READ → INSPECT → IMPLEMENT → RECONCILE → VERIFY → RECORD**

### READ
Read:
1. AGENTS.md.
2. MASTER.md.
3. Relevant subsystem documentation.
4. Applicable scoped instructions.
5. The assigned work-unit record.

Avoid loading the entire documentation collection when only a small part is relevant.

### INSPECT
Inspect the actual affected source, interfaces, consumers, dependencies, tests, and working-tree state.

Confirm that the documentation is still consistent with the relevant source.

Do not rely only on previous documentation.

### IMPLEMENT
Perform the assigned implementation.

Respect module boundaries, repository conventions, concurrent modifications, and current user instructions.

Do not overwrite unrelated changes.

### RECONCILE
Review affected codebase-analysis sections.

Update descriptions, inventories, architecture diagrams, execution flows, contracts, and capability statuses when required.

For shared architecture changes, follow the ownership and integration process.

Do not update MASTER.md unless its high-level information genuinely changes.

### VERIFY
Perform only the checks authorised or required for the current task.

Record:
- Commands executed.
- Results.
- Relevant scope.
- Failures.
- Limitations.
- Unverified areas.

Never fabricate successful tests or integrations.

### RECORD
Update the assigned work-unit record with:
- Implementation changes.
- Current progress.
- Verification evidence.
- Architectural impacts.
- Remaining work.
- Handoff context.

Do not duplicate routine logs in shared documentation.

---

# 10. Documentation Status Standards

Use the following definitions consistently.

| Status | Definition |
|---|---|
| Implemented | Supporting source exists and is connected to its actual consumers |
| Partially implemented | Meaningful functionality exists, but specified elements remain incomplete |
| Verified | A named check passed for a stated scope and revision/date |
| Partially verified | Some relevant checks passed; remaining checks are identified |
| Not verified | No relevant execution evidence is available |
| Deferred | Work was explicitly accepted outside the current scope |
| Unknown | Available evidence is insufficient |

Implementation and verification are separate dimensions.

Identify inactive implementations explicitly.

Historical verification results must retain their original scope and attribution.

Do not present older verification results as confirmation of newer code without supporting evidence.

---

# 11. Documentation Efficiency and Context Management

Optimise the documentation for both human developers and AI coding agents.

Follow these rules:

1. MASTER.md must provide high-level understanding and navigation, not exhaustive task history.
2. Detailed source analysis belongs in subsystem documentation.
3. Task-specific changes and logs belong in independent work-unit records.
4. Keep the current work state near the top of each work-unit record.
5. Avoid duplicating the same architectural facts across multiple documents.
6. Use concise tables, annotated trees, and diagrams where they improve clarity.
7. Maintain detailed source references for important claims.
8. Avoid unnecessary restructuring or formatting-only edits.
9. Read only documentation relevant to the current task after the initial baseline.
10. Reuse existing verified context, but validate potentially stale claims against source.
11. Keep historical logs append-only within their assigned records.
12. Do not force a complete codebase scan after every small change.

For large repositories, partition documentation by package or subsystem while preserving comprehensive coverage.

The documentation system must scale with repository size and team size without causing MASTER.md to grow indefinitely.

---

# 12. Initial Documentation Migration

If MASTER.md, AGENTS.md, or other engineering records already exist:

1. Read them fully before changing their structure.
2. Compare current-state claims against actual source.
3. Preserve accurate architectural information.
4. Move detailed subsystem analysis into docs/codebase/.
5. Move identifiable task history and verification records into appropriate work-unit records.
6. Preserve historical information that cannot reliably be attributed to an individual work unit in a clearly labelled legacy-history document.
7. Do not fabricate ownership, tickets, dates, or verification details.
8. Replace duplicated mutable records with references to their canonical locations.
9. Rebuild MASTER.md as the stable engineering reference.
10. Update AGENTS.md to enforce the new documentation workflow.
11. Check that no relevant information was lost during migration.

Do not blindly replace existing documentation.

Preserve unrelated working-tree changes.

---

# 13. Git and Documentation Integration Rules

Apply these rules to all documentation updates:

- Inspect Git status before editing.
- Record branch and revision information only when available.
- Never assume the working tree is clean.
- Do not overwrite unrelated uncommitted changes.
- Do not stage or commit another contributor's files without explicit coordination.
- Do not rewrite shared documents simply to append an implementation event.
- Prefer small, scoped changes.
- Avoid unnecessary reordering of existing documentation.
- Keep independent work-unit records independently maintainable.
- Preserve history across rebases and merges.
- Do not use force-push or conflict-resolution strategies that discard another contributor's work.
- Validate shared documentation after integration when affected source changes overlap.

Documentation reconciliation should be completed in the same work item whenever safely possible.

If shared changes cannot be reconciled immediately, explicitly track the outstanding reconciliation and ensure it is completed before claiming the affected documentation is current.

Do not claim merge-conflict prevention guarantees. The purpose is to minimise unnecessary conflicts and make legitimate conflicts safe to identify and resolve.

---

# 14. Security and Evidence Rules

Never expose or copy:
- Credentials.
- Access tokens.
- Private keys.
- Environment secret values.
- Personal or confidential data.

Document configuration names, purpose, requiredness, validation, and loading precedence without disclosing sensitive values.

Never invent:
- Source behaviour.
- Working integrations.
- Test results.
- Architectural decisions.
- Historical changes.
- Active tasks.
- Ownership.
- Git metadata.
- Requirements.

Clearly distinguish:
- Observed source facts.
- Verified execution evidence.
- Historical records.
- Assumptions.
- Unknowns.
- Recommendations.
- Accepted requirements.

For initial documentation setup, prefer source inspection. Do not install dependencies, run builds or tests, start servers, or contact external services unless separately requested or required by applicable instructions.

---

# 15. Final Validation

Before completing the initial documentation task or a later documentation reconciliation:

### Structure
- Confirm AGENTS.md and MASTER.md exist at the root.
- Confirm links between documentation files are valid.
- Confirm subsystem documentation reflects actual repository boundaries.
- Confirm work-unit documentation paths are unique.

### Accuracy
- Compare annotated directory inventories with the inspected files.
- Confirm architectural claims have identifiable source evidence.
- Confirm active behaviour is not confused with mocks or unused code.
- Confirm known issues are distinguished from suspected risks.
- Confirm historical behaviour is not presented as current behaviour.
- Confirm important architectural changes are reflected in affected documentation.

### Concurrency
- Confirm no other contributor's work-unit record was overwritten.
- Confirm unrelated shared documentation was not modified.
- Confirm overlapping architecture changes were reconciled or explicitly marked pending.
- Confirm changes from other contributors were preserved.
- Confirm no unsafe Git operation discarded concurrent work.

### Verification
- Confirm recorded tests and checks actually occurred.
- Confirm failed or unexecuted checks are not presented as passed.
- Confirm current verification status is supported by evidence.

### Scope
- During initial setup, confirm only the requested documentation files were created or modified.
- During development, confirm changes remain within the assigned scope and necessary affected documentation.
- Confirm no secrets or fabricated information were introduced.

---

# 16. Final Output Requirements

After completion, provide a concise report containing:

1. Documentation files created or modified.
2. Repository analysis coverage.
3. Main subsystems identified.
4. Existing documentation migrated or preserved.
5. Current work-unit record, if applicable.
6. Architecture documents reconciled.
7. Checks actually performed.
8. Material limitations or outstanding documentation gaps.
9. Any concurrency or integration conflicts requiring attention.

If filesystem access is available, create or update the documentation and report the exact paths.

If filesystem access is unavailable, provide the proposed structure and complete required initial file contents without claiming they were created.

**Final objective:**

Build a reliable, comprehensive, AI-readable documentation system where the codebase remains the source of truth, architectural knowledge stays current, individual implementation histories remain independent, and multiple developers or AI agents can work on the same repository—including the same shared branch—with minimal unnecessary documentation conflicts and controlled reconciliation of genuinely overlapping changes.