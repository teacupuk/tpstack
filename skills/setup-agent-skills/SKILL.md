---
name: setup-agent-skills
description: Set up Claude Code and Codex to use this shared skills repository. Use when asked to install, link, or troubleshoot the repository's skills on this computer.
disable-model-invocation: false
---

# Set up shared agent skills

Link this repository's `skills/` directory into the personal skills directories used by Claude Code and Codex. Work on the computer where the user asked for setup. Do not assume the repository is at `~/agent-skills`; find its actual path first.

## Find the repository

1. Identify the repository root from the current working directory or the current skill file's location.
2. Confirm that the root contains a `skills/` directory. Use its absolute path as the link target.
3. If the current environment cannot access the user's machine or the repository root is unclear, explain what path or environment is needed before making changes.

## Inspect before changing paths

The personal skill directories are:

- Claude Code: `~/.claude/skills/`
- Codex: `~/.agents/skills/`

Inspect both paths and their parent directories before creating links. Make the setup idempotent:

- If a destination is already a symlink or junction to this repository's `skills/` directory, leave it as is.
- If the destination does not exist, create a link to the repository's whole `skills/` directory.
- If the destination is a link to a different location, do not overwrite it. Report what it points to and ask which setup the user wants.
- If the destination is a real directory, preserve it. Link the repository's individual skill folders into it, skipping names that already exist. Report any name collisions rather than replacing their contents.
- If a destination is a regular file or another unexpected item, do not change it. Explain the conflict.

Do not delete, replace, or move existing user data. Do not run `ln -s` or junction creation against an existing destination without first inspecting it.

## macOS and Linux

Use symbolic links. Create the parent directories if needed. For an absent `skills/` destination, the command pattern is:

```sh
mkdir -p "$HOME/.claude" "$HOME/.agents"
ln -s "/absolute/path/to/agent-skills/skills" "$HOME/.claude/skills"
ln -s "/absolute/path/to/agent-skills/skills" "$HOME/.agents/skills"
```

Substitute the discovered absolute repository path. If either destination is a real directory, create links for each repository skill folder instead:

```sh
ln -s "/absolute/path/to/agent-skills/skills/SKILL_FOLDER" "$HOME/.claude/skills/SKILL_FOLDER"
ln -s "/absolute/path/to/agent-skills/skills/SKILL_FOLDER" "$HOME/.agents/skills/SKILL_FOLDER"
```

Run one pair for each skill after checking each destination name. Create a parent skills directory when it is missing.

## Windows

Use directory junctions from PowerShell or Command Prompt. A junction usually does not require symlink privileges. Create parent directories as needed. For an absent `skills` destination, the Command Prompt pattern is:

```bat
if not exist "%USERPROFILE%\.claude" mkdir "%USERPROFILE%\.claude"
if not exist "%USERPROFILE%\.agents" mkdir "%USERPROFILE%\.agents"
mklink /J "%USERPROFILE%\.claude\skills" "C:\absolute\path\agent-skills\skills"
mklink /J "%USERPROFILE%\.agents\skills" "C:\absolute\path\agent-skills\skills"
```

Substitute the discovered absolute repository path. If the destination is already a real directory, preserve it and create junctions for individual skill folders that do not already exist. Do not run `mklink` for an existing path.

## Verify and report

After setup, inspect the links and confirm that each points to the discovered repository path or that the individual skill links resolve into its `skills/` directory. Report which tool directories were linked and any conflicts left untouched. If a tool does not discover newly added skills, suggest restarting that tool.
