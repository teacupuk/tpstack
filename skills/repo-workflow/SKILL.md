---
name: repo-workflow
description: Repository workflow for changes intended for version control. Use when preparing repository changes, committing, pushing branches or tags, creating or updating issues and pull requests, merging, or publishing releases.
---

# Repository workflow

Apply these shared conventions to the requested work. Read the repository's `AGENTS.md`, `CLAUDE.md`, developer guide and contribution instructions first; explicit repository conventions take precedence over these defaults. Derive commands, scopes, required checks and release triggers from the current checkout and hosting configuration.

## Establish the change

1. Inspect the repository root, remote, current branch, working tree and staged changes. Identify the intended base branch from repository guidance or the remote's default branch; DashyNMS desktop uses `master`, while several sibling repos use `main`.
2. Work on a topic branch with one issue or coherent outcome per PR. Preserve unrelated work and stage the intended paths or hunks explicitly. Use an existing issue when supplied; link or create issues within the user's requested scope rather than inventing issue numbers.
3. Find the owner of shared code before editing. Fix libraries in their source repository, then update the consumer's package or submodule reference. Keep UI/platform adapters outside shared logic. Read the current dependency configuration: historical docs may describe a retired sharing arrangement.

Proceed when the base, intended change and ownership are established, and unrelated work is accounted for.

## Prepare and validate

- Follow the repository's code style; use British spelling in user-facing text and explain non-obvious reasons in comments. DashyNMS .NET projects favour sealed classes and XML comments explaining why.
- Keep credentials and identifiable customer/network data out of committed files, logs, fixtures, screenshots and public discussion. Use synthetic names such as `example.net` and documentation address ranges.
- Update affected documentation alongside behaviour. Keep user-facing release notes distinct from implementation and PR notes.
- Run the build, tests and security checks relevant to the change, including repository-required checks. Use regression tests for changed behaviour; respect platform-specific test requirements. Report unavailable platform or credential-dependent checks as unverified.
- For a public API, schema or persisted-format change, identify affected consumers, migration and version implications. Apply the repository's version policy; breaking public contracts require the appropriate major version change.
- Preserve upstream licences and provenance when importing material. For generated artefacts, use pinned inputs and the repository's reproducibility checks. Apply CI permissions and publication rules from that repository rather than importing another project's release process.

Before committing or pushing, inspect the complete intended diff and staged diff, confirm the file set, check whitespace errors, and account for each applicable check as passed, failed or unavailable. Fix actionable failures; state any remaining limitation accurately.

## Titles and commits

Use the same format for branch commit subjects, PR titles and issue titles:

```text
type(scope): what changes, as the user would notice it
```

- Types: `feat` for new capability, `fix` for corrected behaviour, `perf` for performance, `refactor` for restructuring without behaviour changes, `docs`, `test`, `build` for packages/projects/versions, `ci`, `chore`, `revert`.
- Choose a lower-case area from the repository's scope list. Separate two scopes with a comma; omit the scope when there is no single area. Add a new scope to the repository's documented list in the same PR when that convention applies.
- Start the description in lower case, omit the final full stop, and aim for a complete subject under 72 characters. Describe the result rather than a method or class edited.
- Keep issue numbers out of titles. Mark a breaking change with `!`, such as `feat(api)!: …`, and explain the break and migration in the body.
- Word issue titles as the outcome the fixing PR delivers. Epics end with `(epic)`; use `(blocked upstream)` where the repository follows that convention. Labels carry other classifications.
- Commits, PRs and release notes carry no AI attribution or `Co-Authored-By` lines.

Examples:

```text
fix(alerts): acknowledging preserves the current filter
feat(settings): choose the default polling interval
docs: explain local development setup
```

## Pull requests and merges

1. Push the intended topic branch when authorised. Inspect the branch diff against the actual PR base, not just the latest commit.
2. Use the PR title as the eventual squash-commit subject. Start the description with `Closes #NN` when the change resolves an issue; qualify cross-repository references. For partial work, use a non-closing reference. Omit the closing line when there is no issue.
3. Briefly describe the resulting behaviour, why it matters and how it was checked. Include consumer actions, provenance or migration when relevant, and identify checks still pending. Keep the description aligned with the final scope after revisions.
4. Squash-merge by default when a merge is requested and required checks and reviews permit it. Use a repository's documented exception where applicable: DashyNMS MCP permits rebase merges for larger branches whose individual commits are worth retaining. Preserve protected-branch requirements and published history.
5. Treat release publication as a separate action. Inspect what a merge, tag or workflow dispatch will trigger before performing it. Follow the repository's release policy, preserve immutable published versions, and publish only within the user's authorised scope.

Finish with the commit or PR reference, a concise validation result, and any remaining checks or consumer steps. Distinguish pushed, merged and released states; report only states actually verified.

## Basis

Adapted from DashyNMS desktop's `CLAUDE.md` and `docs/DEVELOPMENT.md`, mobile's `CLAUDE.md` and `docs/DEVELOPING.md`, Core's `CLAUDE.md`, MCP's `CLAUDE.md` and `docs/DEVELOPMENT.md`, and sensor-definitions' corresponding guides. These are shared defaults; product architecture, scope lists, build commands and release machinery remain repository-owned.
