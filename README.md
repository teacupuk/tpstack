<p align="center">
  <span aria-hidden="true" style="font-size: 4rem">🏕️</span>
</p>

<h1 align="center">TP Agent Skills</h1>

<p align="center">
  <strong>A shared home for the skills you use with Claude Code and Codex.</strong><br>
  Write a skill once, keep it in Git, and link it into both tools.
</p>

<p align="center">
  <a href="#getting-started">Get started</a> ·
  <a href="#skill-reference">Skill reference</a> ·
  <a href="#writing-a-skill">Write a skill</a> ·
  <a href="#linking-to-claude-code-and-codex">Link the tools</a>
</p>

---

Agent skills are reusable instructions for a particular kind of work. This repository keeps each skill in its own folder under `skills/`, with a `SKILL.md` file as its entry point. Claude Code and Codex can both read that format, so one shared folder can serve both tools.

## Getting started

Clone this repository somewhere convenient on each computer. The examples below use `~/agent-skills` on macOS or Linux and `%USERPROFILE%\agent-skills` on Windows.

```sh
git clone https://github.com/teacupuk/tpstack.git ~/agent-skills
```

To bring your skills up to date later, run `git pull` from the cloned repository on that computer.

## Skill reference

User-invoked skills run when you explicitly request them. Model-invoked skills can also be selected automatically when the task matches their description. Invoke a skill by name with `$skill-name` in Codex or `/skill-name` in Claude Code.

### User-invoked

- **[repo-docs](skills/repo-docs/SKILL.md)**: Set up or reorganise a repository's README, developer guide and agent instructions. Use it when establishing documentation or reviewing how existing docs fit together.

### Model-invoked

- **[setup-agent-skills](skills/setup-agent-skills/SKILL.md)**: Link this repository's skills into Claude Code and Codex on the current computer, preserving existing skills and reporting conflicts.
- **[repo-workflow](skills/repo-workflow/SKILL.md)**: Apply the shared conventions for repository changes, commits, issues, PRs, merges and releases, while respecting each repository's own rules.
- **[writing-for-agents](skills/writing-for-agents/SKILL.md)**: Write skills, `AGENTS.md`, `CLAUDE.md` and supporting agent documentation with clear triggers, steps and completion criteria.
- **[unslop](skills/unslop/SKILL.md)**: Edit writing to remove AI tells while preserving its meaning and intended tone.

This reference layout takes inspiration from [Matt Pocock's skills repository](https://github.com/mattpocock/skills#reference).

## Where skills live

Keep skills in `skills/`, with one directory per skill:

```text
agent-skills/
└── skills/
    ├── example-skill/
    │   └── SKILL.md
    └── another-skill/
        └── SKILL.md
```

Each `SKILL.md` should explain when to use the skill and give the agent the instructions or workflow to follow. Keep any supporting files for that skill inside its own folder. Use a short, lowercase, hyphen-separated folder name.

## Linking to Claude Code and Codex

Both tools look for personal skills in these directories:

| Tool | Personal skills directory |
| --- | --- |
| Claude Code | `~/.claude/skills/` |
| Codex | `~/.agents/skills/` |

Link the repository's `skills` directory into both locations. This lets both tools read the same skill folders while Git keeps the source in one place.

### macOS and Linux

```sh
mkdir -p ~/.claude ~/.agents
ln -s ~/agent-skills/skills ~/.claude/skills
ln -s ~/agent-skills/skills ~/.agents/skills
```

These commands expect that neither `skills` path already exists. If one does, inspect it first with `ls -la ~/.claude/skills` or `ls -la ~/.agents/skills`. If it is a directory containing skills you want to keep, link individual skill folders instead, or move the directory aside and merge its contents before creating the link. Do not remove an existing path until you know what it contains.

If you cloned the repository somewhere other than `~/agent-skills`, use its full path as the link target.

### Windows

In Command Prompt, create the parent directories if needed, then create directory junctions. Update the target path if you cloned the repository elsewhere.

```bat
if not exist "%USERPROFILE%\.claude" mkdir "%USERPROFILE%\.claude"
if not exist "%USERPROFILE%\.agents" mkdir "%USERPROFILE%\.agents"
mklink /J "%USERPROFILE%\.claude\skills" "%USERPROFILE%\agent-skills\skills"
mklink /J "%USERPROFILE%\.agents\skills" "%USERPROFILE%\agent-skills\skills"
```

These commands expect that neither destination already exists. If a destination exists, inspect it before changing it; junctions usually avoid the symlink privilege requirement.

### Link individual skills

If you already use either personal skills directory for other skills, leave it in place and link only the folders from this repository. For example, on macOS or Linux:

```sh
mkdir -p ~/.claude/skills ~/.agents/skills
ln -s ~/agent-skills/skills/example-skill ~/.claude/skills/example-skill
ln -s ~/agent-skills/skills/example-skill ~/.agents/skills/example-skill
```

Repeat those two `ln -s` commands for each skill you want to share.

## Writing a skill

Create a directory under `skills/` and add a `SKILL.md`. A simple starting point:

```markdown
---
name: example-skill
description: Briefly say what this skill helps with and when to use it.
---

# Example skill

Describe the task this skill supports and the steps the agent should follow.
```

Keep the description specific so it is clear when the skill applies. Add reference material, scripts, or examples to the same skill directory when needed, and link to them from `SKILL.md`.

## Updating and troubleshooting

- Pull changes in the cloned repository on each computer to get skill updates.
- If a new skill does not appear, check that the link points to this repository's `skills/` directory and that each skill folder contains `SKILL.md`.
- Restart Claude Code or Codex if a newly added skill is not picked up.
- You can link selected skill folders individually when you do not want every skill available in both tools.

Tool-managed `skills/synced/` and `skills/.trash/` folders are local data and are ignored by Git.

## Security

Report vulnerabilities privately using the process in [SECURITY.md](SECURITY.md). Review a skill's instructions and supporting files before enabling it; skills can guide an agent to run commands or access external services under that agent's permissions.

## Licence

Original material is available under the [MIT licence](LICENSE). Imported material retains its upstream copyright and licence notices; see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md). The `writing-for-agents` skill is copied unchanged from Matt Pocock's repository.

---

<p align="center"><sub>One skills folder. Shared by Claude Code and Codex.</sub></p>
