# Authoritative Source Verification

Use this reference when external APIs, ecosystems, migrations, framework integrations, or version-sensitive best practices affect the answer.

## 1. Determine the installed reality

Read manifests, lockfiles, framework config, integration code, and relevant vendor SDK versions. Distinguish installed from desired/target versions. Do not implicitly upgrade to the latest release or recommend examples written for a different major version.

## 2. Discover sources in this order of work

1. **Repository obligations and actual code:** rules establish constraints; source/config verifies existing behavior.
2. **Installed skills, if discoverable:** follow relevant skill workflows, but verify claims against the current technology and repository; an installed skill can be stale or broader than this project.
3. **Official vendor/framework documentation:** API references, integration guidance, best practices, supported versions, security guidance.
4. **Official changelogs, migration guides, release notes:** breaking changes, removal, deprecation, feature availability.
5. **Maintainer discussions and community examples:** only for nuance and corroboration, not as the primary proof of an API's current validity.

This is a **workflow**, not a rigid truth ranking. Local source is authoritative for *what the current repo does*; vendor docs are authoritative for *documented API semantics*. Explain conflicts and weigh them explicitly.

## 3. Cross-check claims

For each API/pattern likely to be used:

- Is it supported by the installed version, runtime, build target, and framework integration?
- Is it deprecated, unstable, superseded, or affected by a migration requirement?
- Is the pattern platform-specific (server/client, SSR, edge, browser, Node, mobile)?
- What are the security, performance, correctness, and maintenance considerations?
- Do the docs actually demonstrate the recommended usage, or merely a similar API?

Use publication/update dates and documentation version selectors where available. Do not call a source "latest" simply because it was the top search result. Do not copy unknown-age GitHub snippets and infer compatibility.

## 4. Provenance and uncertainty

When presenting significant external recommendations, supply the official source URL and the confirmed product/library version. Use precise phrases such as:

- "Verified in the installed version ..." only after checking both the installed baseline and suitable docs.
- "Official docs describe ..." only after accessing those docs.
- "Could not verify current guidance because ..." when browsing or a skill is unavailable.
- "Proposed departure from repository convention ..." with rationale and migration impact.

If reliable sources disagree, identify the disagreement, version/date differences, and a conservative approach. Never fabricate citations, source access, version checks, or current support status.

## 5. Suggested sources (not mandatory dependencies)

The primary references are the relevant project's official docs and release notes. For the **skill format itself**, see:

- https://agentskills.io/specification
- https://agentskills.io/skill-creation/best-practices
- https://agentskills.io/skill-creation/optimizing-descriptions
- https://agentskills.io/skill-creation/evaluating-skills

Do not use these skill-creation links as substitutes for framework/SDK documentation needed by a concrete question.
