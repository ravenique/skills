# RAVENiQUE Skills

Reusable Agent Skills for AI coding agents. Each skill provides a focused workflow, engineering guidance, and supporting reference material that can be installed directly from this repository.

## Available skills

| Skill | What it does | Use it when |
| --- | --- | --- |
| [`mindful-feature-engineer`](./mindful-feature-engineer/) | Understands a repository's architecture, governance, conventions, dependencies, contracts, and tests before changing code. Guides feature implementation, modification, and safe removal with deliberate design and verification. | Building, changing, or safely removing a feature in an existing codebase. |
| [`repo-performance-refactor`](./repo-performance-refactor/) | Audits and prioritizes performance bottlenecks, creates an evidence-based refactoring plan, and guides user-approved implementation and validation. | Investigating performance, analyzing hot paths, optimizing resource usage, or planning performance-focused refactoring. |

## Installation

The Skills CLI can install skills from this GitHub repository. Use either `bunx` (Bun) or `npx` (Node.js).

### Install both skills for Antigravity in the current project

Project installation is the default. These commands install the skills into the current workspace for Antigravity:

```bash
bunx skills add ravenique/skills \
  --skill mindful-feature-engineer \
  --agent antigravity

bunx skills add ravenique/skills \
  --skill repo-performance-refactor \
  --agent antigravity
```

You can also install both in one command:

```bash
bunx skills add ravenique/skills \
  --skill mindful-feature-engineer \
  --skill repo-performance-refactor \
  --agent antigravity
```

### Install one skill

```bash
bunx skills add ravenique/skills \
  --skill mindful-feature-engineer \
  --agent antigravity
```

Replace `mindful-feature-engineer` with `repo-performance-refactor` to install the performance workflow instead.

### Install globally

Global installation makes the selected skills available across projects for the selected agent:

```bash
bunx skills add ravenique/skills \
  --skill mindful-feature-engineer \
  --skill repo-performance-refactor \
  --agent antigravity \
  --global
```

To install for another supported agent, replace `antigravity` with its Skills CLI agent identifier. Omit `--agent` to let the CLI guide agent selection interactively.

> **Project or global?** Project installation is useful when a repository should declare the skills it uses and share that setup with the team. Global installation is useful for personal workflows that should be available across your projects.

### Install all skills for all supported agents

```bash
bunx skills add ravenique/skills --all
```

## Updating

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

## Project lockfile

When skills are installed at project scope, the Skills CLI creates or updates `skills-lock.json`. Commit this file with the project so the selected skill sources, paths, and content hashes are recorded for the team.

The lockfile records installation metadata; it does not replace the installed skill directories. Keep `skills-lock.json` under version control alongside the project files.

The CLI also provides an experimental restore command for recreating skills from a lockfile:

```bash
bunx skills experimental_install
```

This command is marked experimental by the Skills CLI, so check the current CLI help and test it in your team's workflow before relying on it in automation.

## Repository structure

Each skill is self-contained. Its `SKILL.md` contains the required metadata and main instructions. Supporting catalogs and reference documents live inside the same skill directory so relative links continue to work after installation.

```text
.
├── mindful-feature-engineer/
│   ├── SKILL.md
│   ├── design-pattern-catalog.md
│   └── references/
├── repo-performance-refactor/
│   ├── SKILL.md
│   ├── refactoring-catalog.md
│   └── references/
└── README.md
```

## Contributing a skill

1. Create a directory with a lowercase `kebab-case` name.
2. Add a `SKILL.md` with YAML frontmatter containing `name` and `description`.
3. Make the frontmatter `name` match the skill directory name.
4. Keep supporting files inside that skill's directory and reference them using relative paths.
5. Validate the skill and verify that every referenced file exists before submitting a change.

See the [Agent Skills specification](https://agentskills.io/specification) for the skill format and metadata requirements.

## Safety and licensing

- Skills are instructions and reference material. Review their contents before installing or using them in a sensitive codebase.
- This repository is public. Do not add secrets, credentials, private project data, or other confidential material.
- A `LICENSE` file has not yet been added to this repository. Reuse and redistribution terms have therefore not been explicitly granted; add an appropriate license before inviting external contributions or reuse.
