# Repository Investigation Protocol

Use this protocol when the task requires claims about an existing codebase. Its purpose is **complete architectural coverage with selective code depth**, not reading every byte in the repository.

## A. Instruction and scope discovery

1. Establish the current repository root, working directories, workspaces, and configured subprojects without altering state.
2. Locate root and nearest-path rules (`AGENTS.md`, `CLAUDE.md`, applicable editor/agent rules), README, contribution instructions, architecture/design docs, and configuration guidance. Follow host instruction precedence if documents conflict.
3. Identify the stated domain boundaries, allowed dependency directions, gateways, shared DTO/schema conventions, error-handling conventions, and existing testing/type-checking strategy.
4. Examine manifests and lockfiles to identify actual tools and versions, not just documentation claims.

## B. Repo-wide inventory before deep dive

Inventory the repository's tracked source structure, packages/workspaces, runtime entry points, router/API edges, client/server boundaries, shared contracts, generated source, and infrastructure integration points. Use read-only discovery commands when appropriate; do not dump large vendored directories or sensitive environment files.

Skip irrelevant dependency caches and generated assets unless the question specifically concerns them. Untracked code that is materially relevant should not be ignored merely because it is untracked.

A breadth-first view is required. Then concentrate reading on the relevant call graph and dependency paths. Trace the flow as needed:

`entry point -> caller -> API/gateway -> domain logic -> data layer -> response/consumer`

The actual graph may differ. Check interfaces, schemas, validators, types, error flows, async boundaries, authentication/authorization, cache invalidation, and feature flags where applicable.

## C. Architecture compatibility checks

- Does the recommendation preserve existing layers and dependency direction?
- Is there already a shared type/schema/DTO to reuse? If there is an established shared Zod convention, do not duplicate schema definitions in server and client.
- Are there gateway patterns that must remain the only public path into backend code?
- Are proposed libraries already installed? Are versions, framework integrations, or package boundaries incompatible?
- Does an existing utility, hook, service, component, or middleware already solve all or part of the problem?
- Are conventions actually enforced by tooling or merely described by stale documentation?
- Would a local change break downstream callers, public interfaces, persistence models, or serialization formats?

## D. Evidence trail

For each major repository-specific claim, record its source (`path`, symbol, and line range if tooling exposes one). Separate:

- **Observed:** directly read from tracked files, configuration, or command output.
- **Inferred:** reasoned from observed behavior, with assumptions stated.
- **Unknown:** uninspected, inaccessible, ambiguous, or unsupported by evidence.

A README alone is insufficient to assert runtime behavior. Source code alone does not supersede binding repository rules. When they conflict, explain the discrepancy and its consequence.

## E. Read-only command discipline

Prefer source inspection and benign inventory commands. Never run installation, migration, generators, deployment, formatting, mutation scripts, or commands whose side effects are unknown. Avoid reading or echoing secrets in `.env*`, credentials, token files, or production dumps.

For type checking specifically:

1. Identify the exact script and every nested executable, flags, and relevant configuration. Check for `pre*`/`post*` lifecycle hooks, generators, caches, incremental outputs, or emitted artifacts.
2. Run only a relevant type-check command confirmed to avoid mutations. For TypeScript, `--noEmit` by itself may **not** establish absence of incremental cache writes; inspect `incremental`, `composite`, `tsBuildInfoFile`, and the invocation mode.
3. Do not use package-manager commands that could auto-install missing dependencies. Skip if the tool is absent or execution cannot be shown safe.
4. Report exact scope and result. An existing baseline failure is not a defect introduced by the hypothetical solution. A baseline pass does not prove proposed code correctness.
5. Do not run tests without an explicit user request; even authorized tests must be screened for side effects.

## F. Completion criteria

The recommendation should be grounded in the relevant code paths, interfaces, existing abstractions, versions, and constraints. If access was partial, disclose which areas remain unexamined instead of claiming a full scan.
