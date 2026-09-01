# AI Assets Directory — Skills

A collection of Claude Code / agent skills maintained by AI Assets Directory. Each
skill lives in its own folder under `skills/` with a `SKILL.md` plus any supporting
files.

## Skills

| Skill | Description |
|-------|-------------|
| [create-skill](skills/create-skill) | Scaffold high-quality Claude Code skills and slash commands with correct frontmatter, conventions and worked examples. |

## Install a skill

Clone the repo and copy the skill folder into your skills directory (the folder name
must match the skill's `name`):

```bash
git clone https://github.com/lorenzomeolav32-png/ai-assets-directory-skills
cp -r ai-assets-directory-skills/skills/create-skill ~/.claude/skills/create-skill
```

For a project-scoped install, copy into `.claude/skills/<name>/` instead, then reload
skills.

## License

MIT — see [LICENSE](LICENSE). Applies to all skills in this repository.
