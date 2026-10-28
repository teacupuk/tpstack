---
name: repo-docs
description: Set up or reorganise a repository's user, developer and agent documentation.
disable-model-invocation: true
---

# Repository documentation

Run only when the user invokes this skill. Create or reorganise documentation in the target repository, using its current code and configuration as evidence. Apply `writing-for-agents` when writing agent instructions. This task prepares documentation; commit, push, PR and publication actions follow the user's requested scope.

## Inspect the repository

Read the existing README, agent instructions, developer and contribution guides, manifests, CI workflows and release configuration. Inspect the entry points and modules needed to establish the architecture. Identify:

- Who uses the project, what they receive and how they install or start it.
- How a developer builds, tests and runs it, including platform and credential prerequisites.
- Which repository owns shared code, how dependencies are consumed, and where platform boundaries sit.
- How changes, releases, support and security reports are handled.

Resolve contradictory documentation against current code and configuration. Ask for product, licensing or contribution-policy decisions that the repository cannot establish; mark unresolved facts explicitly rather than guessing. Continue when each proposed document has an audience and an evidence-backed purpose.

## Give each fact one home

Use the following division, preserving existing useful paths such as `docs/DEVELOPING.md` rather than creating a competing guide:

| Document | Owns |
| --- | --- |
| `README.md` | What the project does, who it is for, supported platforms, installation or a minimal quick start, and links to further help |
| `docs/DEVELOPMENT.md` | Developer prerequisites, build/run/test steps, architecture boundaries, shared dependencies, local configuration/storage, and release or deployment procedures |
| `AGENTS.md` / `CLAUDE.md` | A short agent entry point: orientation, high-impact invariants and conditional pointers to the developer or contribution guide |
| Existing contribution guide, or a section in the developer guide | Branch/PR/issue conventions, scope list, checks and merge policy |
| Release notes / What's New | User-visible changes for a release, separate from PR implementation notes |

Create security, privacy, licence, support or release documents only when the project's actual needs justify them. Preserve established policy and licence text. Keep roadmaps in the repository's existing issue/milestone system and link there rather than duplicating a changing feature inventory.

## Write and connect

1. Keep the README focused on users. Put build internals, source layout and developer release mechanics in the developer guide; link between them.
2. Write runnable developer instructions from the current scripts and workflows. Explain prerequisites, placeholders, expected outcomes and non-obvious platform limitations. Link to authoritative configuration instead of copying complete dependency versions, workflow schedules or directory trees that are cheap to inspect.
3. Document architectural reasons, ownership boundaries and compatibility traps that code alone does not explain. Distinguish local development builds, CI artefacts, previews and stable releases, including which actions actually publish.
4. Keep agent instructions short. Inline invariants needed on every change; point to detailed material with the condition for reading it. For example: “Before changing shared API contracts, read the compatibility section in the developer guide.” Ensure each pointer names a real file or section.
5. For both Codex and Claude support, prefer one canonical `AGENTS.md` with a thin `CLAUDE.md` that explicitly directs Claude to read it. Preserve an established working arrangement if it already provides a single source of truth. Put repository-specific rules here; leave general workflow conventions in `repo-workflow`, and make the repository's essential instructions usable by contributors who do not have that personal skill installed.
6. Put the full commit/PR/issue standard in one repository-owned location and link to it from agent instructions. Use the `repo-workflow` conventions as defaults while preserving explicit repository policy, the actual default branch and relevant scopes.

Use British spelling and synthetic examples. Explain credential names and permissions without including values. Update links when consolidating material and preserve externally used paths or provide an appropriate redirect. Keep user-visible release notes separate from technical review notes.

## Verify and hand back

- Every new factual statement is supported by inspected code, configuration, existing policy or a user decision; remaining uncertainties are explicit.
- Every relative file link and heading anchor resolves, and the README, developer guide and agent entry points connect to their intended targets.
- Build/test examples match current entry points. Run safe relevant examples or existing documentation checks where available; report examples requiring missing platforms, credentials or publication as unverified.
- Facts have one authoritative home; agent pointers state when their target should be read. Remove obsolete instructions and duplicated sections as part of the same edit.
- Inspect the final diff for accidental policy changes, customer data, credentials and unrelated edits. Report the documents changed and any unresolved decisions.

## Basis

Uses DashyNMS's separation of user-facing READMEs, technical development guides and concise `CLAUDE.md` entry points. Product-specific build, storage, signing and release details belong in the target repository rather than this reusable skill.
