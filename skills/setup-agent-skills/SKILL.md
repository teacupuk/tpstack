---
name: setup-agent-skills
description: Set up shared skills on this computer. Use when installing this repository's skills, linking them into Claude Code or Codex, or troubleshooting those links.
---

# Set up shared agent skills

## Locate and inspect

1. Find the repository root from the working directory or this skill's location. Confirm its `skills/` directory and use the absolute path as the source. Work on the requested computer; if it is inaccessible, report the missing access before changing paths.
2. Discover immediate skill folders by their `SKILL.md` entry points. Exclude tool-managed folders such as `synced/` and `.trash/`.
3. Inspect both destination paths and their parents, including link targets and directory contents:
   - Claude Code: `~/.claude/skills/`
   - Codex: `~/.agents/skills/`

Continue when the source, skill inventory and state of each destination are known. Keep the tool configuration directories as real directories; link only their skills paths.

## Choose links

Handle each destination independently:

| Destination state | Action |
| --- | --- |
| Link to this repository's `skills/` | Leave it in place |
| Absent | Create the parent and link the whole `skills/` directory |
| Real directory | Preserve it and link each discovered skill folder into it |
| Link elsewhere | Preserve it and report its target; ask which setup is wanted if the session has not already specified it |
| File or unexpected item | Preserve it and report the conflict |

For individual skills, leave a link resolving to the intended source in place. Create a link only at an absent path; preserve and report any other name collision. Inspect dangling links as existing paths too.

If the user has explicitly requested replacing a destination, preserve the old item at a unique backup path outside the active skills directory, then create the requested link. Restore the backup if creation fails. Otherwise preserve existing user data in place.

## Create links for the current platform

Substitute the discovered source path in these examples. Run commands only for destinations already established as absent.

### macOS and Linux

Use symbolic links. For a whole-directory link:

```sh
mkdir -p "$HOME/.claude" "$HOME/.agents"
ln -s "/absolute/path/to/repository/skills" "$HOME/.claude/skills"
ln -s "/absolute/path/to/repository/skills" "$HOME/.agents/skills"
```

For an existing real skills directory, link each missing skill folder with the same `ln -s` pattern, using `skills/SKILL_NAME` as both the source suffix and destination suffix.

### Windows

Use directory junctions. In Command Prompt, for a whole-directory link:

```bat
if not exist "%USERPROFILE%\.claude" mkdir "%USERPROFILE%\.claude"
if not exist "%USERPROFILE%\.agents" mkdir "%USERPROFILE%\.agents"
mklink /J "%USERPROFILE%\.claude\skills" "C:\absolute\path\to\repository\skills"
mklink /J "%USERPROFILE%\.agents\skills" "C:\absolute\path\to\repository\skills"
```

For an existing real skills directory, create a junction for each missing skill folder, using `skills\SKILL_NAME` as both the source suffix and destination suffix.

## Verify and report

Resolve each whole-directory link or individual skill link and confirm every discovered skill's `SKILL.md` is readable through each tool's destination. Account for every skill and tool as linked, already correct or blocked by a named conflict.

Report the resulting paths, any backups and unresolved collisions. Suggest restarting the affected tool if it has not discovered the skills. A rerun with unchanged sources and destinations should make no changes.
