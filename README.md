# RAVENiQUE Skills

Reusable Agent Skills for AI coding agents. Each skill provides a focused workflow, engineering guidance, and supporting references that can be installed directly from this repository.

## Available Skills

| Skill | Purpose | Use it when |
| --- | --- | --- |
| [`mindful-feature-engineer`](./mindful-feature-engineer/) | Plans and delivers feature work by first understanding repository architecture, governance, conventions, dependencies, contracts, and tests. Uses pragmatic design, a deliberate “No Pattern” default, and risk-based approval gates. | Adding, changing, extending, or safely removing features in an existing codebase. |
| [`repo-performance-refactor`](./repo-performance-refactor/) | Audits runtime, memory, database, network/assets, and maintainability concerns; ranks evidence-backed bottlenecks; then guides a focused, behavior-preserving refactor with measurement and verification. | Investigating slow or resource-intensive code, profiling hot paths, optimizing queries/assets, or planning a performance-focused refactor. |
| [`bug-fixer`](./bug-fixer/) | Traces defects from symptoms through the causal chain to the root cause, separates verified facts from assumptions, and prepares a regression-safe fix plan for approval before editing. Includes correctness, performance, security, and compatibility checks. | Debugging crashes, errors, failing tests, timeouts, incorrect results, data inconsistencies, or production defects. |
| [`ux-architect`](./ux-architect/) | Connects cognitive UX principles with practical interface rules and repository-native implementation. Includes 30 Laws of UX and 100 RFC 2119 rules across eight UI/UX domains, with workflows for ideation, audits, and implementation. | Designing user flows or interfaces, reviewing screens/components, improving forms and interactions, or implementing accessible UI. |

## Choose the Right Skill

| Your task | Start with |
| --- | --- |
| Build or change a feature | `mindful-feature-engineer` |
| Diagnose and fix an existing defect | `bug-fixer` |
| Investigate or improve performance | `repo-performance-refactor` |
| Design, critique, or implement UI/UX | `ux-architect` |

The skills have distinct scopes and may refer work to one another when appropriate. For example, feature development belongs to `mindful-feature-engineer`; a defect discovered during that work can be handed to `bug-fixer`; and a dedicated performance campaign belongs to `repo-performance-refactor`.

## Install

The Skills CLI installs skills directly from this GitHub repository. Use `bunx` with Bun or `npx` with Node.js.

### Install all four skills for Antigravity

Project installation is the default. Run these commands from your project directory:

```bash
bunx skills add ravenique/skills --skill mindful-feature-engineer --agent antigravity
bunx skills add ravenique/skills --skill repo-performance-refactor --agent antigravity
bunx skills add ravenique/skills --skill bug-fixer --agent antigravity
bunx skills add ravenique/skills --skill ux-architect --agent antigravity
```

### Install one skill

```bash
bunx skills add ravenique/skills --skill bug-fixer --agent antigravity
```

Replace `bug-fixer` with any skill name in the catalog.

### Let the CLI guide agent selection

Omit `--agent` to use the CLI's agent selection workflow. Select Antigravity if it is offered:

```bash
bunx skills add ravenique/skills --skill ux-architect
```

### Install globally

Add `--global` to make each selected skill available across projects for the selected agent:

```bash
bunx skills add ravenique/skills --skill mindful-feature-engineer --agent antigravity --global
bunx skills add ravenique/skills --skill repo-performance-refactor --agent antigravity --global
bunx skills add ravenique/skills --skill bug-fixer --agent antigravity --global
bunx skills add ravenique/skills --skill ux-architect --agent antigravity --global
```

For Antigravity, project skills are installed under `.agents/skills/`; global skills are installed under `~/.gemini/config/skills/`.

### Install all skills for all supported agents

```bash
bunx skills add ravenique/skills --all
```

To use npm instead of Bun, replace `bunx` with `npx` in the commands above.

## Update Skills

Check installed skills for available updates:

```bash
bunx skills check
```

Update project-installed skills:

```bash
bunx skills update --project
```

Update globally installed skills:

```bash
bunx skills update --global
```

You can update selected skills by passing their names:

```bash
bunx skills update bug-fixer ux-architect
```

## Project Lockfile

When skills are installed at project scope, the Skills CLI creates or updates `skills-lock.json`. Commit this file with the project to record the selected skill sources, paths, and content hashes.

The lockfile records installation metadata; it does not replace the installed skill directories. Keep it under version control so teammates can inspect which skill revisions the project uses.

The CLI also has an experimental restore command for recreating installed skills from the lockfile:

```bash
bunx skills experimental_install
```

Because this command is marked experimental by the CLI, verify its current help and behavior before relying on it in team automation.

## What Each Skill Includes

### Mindful Feature Engineer

- Repository reconnaissance before making changes: governance rules, architecture, conventions, callers, contracts, and tests.
- A structured path from understanding requirements through design, approval, incremental implementation, and verification.
- Pragmatic SOLID/DRY/KISS/YAGNI guidance, with “No Pattern” as the default and a bundled GoF pattern catalog for cases where structure genuinely calls for one.
- Risk-based approval gates, including stricter approval for shared contracts, schemas, authentication, data, and high-impact changes.
- Guardrails against speculative abstractions, unrelated cleanup, and unverified test claims.

### Repo Performance Refactor

- Read-only discovery and evidence gathering before proposing code changes.
- Assessment across compute/runtime, memory/resources, database/data access, network/assets, and maintainability/scalability.
- Evidence-confidence labels and a priority matrix to distinguish confirmed issues from hypotheses.
- One highest-value bottleneck per execution cycle, unless issues are inseparable.
- A concrete refactoring plan with success metrics, behavior-preservation constraints, approval gate, validation, and rollback strategy.
- Audit-only mode when the request is analysis without implementation.

### Bug Fixer

- Root-cause investigation that follows the failing behavior through relevant input, validation, API, core logic, persistence/I/O, and output paths.
- Clear separation of verified facts and unconfirmed assumptions.
- A diagnosis framed around symptom and impact, root cause, target behavior, and proposed fix.
- Mandatory user approval before changing repository files.
- Focused regression tests plus correctness, performance, security, compatibility, and side-effect reviews.
- Strict scope control: unrelated refactoring, broad optimization, and feature work stay out of the bug-fix diff.

### UX Architect

- Three operating modes: brainstorm/user-flow/information-architecture design, UI/UX audit and critique, and UI implementation/refactoring.
- A cognitive UX reference covering 30 laws and heuristics, including cognitive load, Hick’s Law, Fitts’s Law, Jakob’s Law, working memory, and the Peak-End Rule.
- A 100-rule engineering rulebook organized into eight domains: forms, visuals, layout and alignment, typography, usability, icons, language and perception, and miscellaneous interactions/edge cases.
- RFC 2119 obligation levels (`MUST`, `SHOULD`, `MAY`, `AVOID`) and a priority order that puts accessibility and semantic correctness first, then usability/data integrity, project design-system consistency, and visual polish.
- Repository context discovery: inspect actual design tokens, UI primitives, styling stack/version, viewport needs, and locale/script requirements before writing UI code.
- Progressive disclosure: use the master rule index to consult only the rules and UX laws relevant to the current task.

## Repository Structure

Each skill is self-contained. Its `SKILL.md` contains the required metadata and primary instructions. Supporting catalogs and references stay inside that skill's directory so relative links continue to work after installation.

```text
.
├── bug-fixer/
│   └── SKILL.md
├── mindful-feature-engineer/
│   ├── SKILL.md
│   ├── design-pattern-catalog.md
│   └── references/
├── repo-performance-refactor/
│   ├── SKILL.md
│   ├── refactoring-catalog.md
│   └── references/
├── ux-architect/
│   ├── SKILL.md
│   ├── references/
│   │   └── laws-of-ux.md
│   └── rules/
│       ├── global.md
│       ├── index.md
│       ├── forms.md
│       ├── visuals.md
│       ├── layout-and-alignment.md
│       ├── typography.md
│       ├── usability.md
│       ├── icons.md
│       ├── language-and-perception.md
│       └── misc.md
└── README.md
```

## Adding a Skill

1. Create a directory with a lowercase `kebab-case` name.
2. Add a `SKILL.md` with YAML frontmatter containing `name` and `description`.
3. Make the frontmatter `name` match the skill directory name.
4. Keep supporting files inside that skill's directory and use relative paths for references.
5. Verify that every referenced file exists and that the skill can be discovered by the CLI.
6. Review the skill for accuracy, safety, portability, and confidential information before publishing.

See the [Agent Skills specification](https://agentskills.io/specification) for the skill format and metadata requirements.

## Safety and Licensing

- Skills are instructions and reference material. Review their contents before installing or using them in a sensitive codebase.
- This repository is public. Do not add secrets, credentials, private project data, or other confidential material.
- A `LICENSE` file has not yet been added to this repository, so reuse and redistribution terms are not explicitly granted. Add an appropriate license before inviting external contributions or granting broader reuse.

## Links

- [GitHub Repository](https://github.com/ravenique/skills)
- [Skills Directory](https://skills.sh/)
- [Skills CLI Documentation](https://github.com/vercel-labs/skills)
- [Agent Skills Specification](https://agentskills.io/specification)
