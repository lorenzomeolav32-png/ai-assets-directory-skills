# skill-creator

A Claude Code skill that helps you create other high-quality skills and slash
commands. It encodes the conventions for skill frontmatter, invocation control,
supporting files, shell injection and the common skill patterns (task, research,
knowledge, dynamic context) so new skills come out consistent and well structured.

The skill itself is named `create-skill` (that is the `/create-skill` command);
this repository is the distributable package for it.

## What it does

- Walks through skill type, scope and frontmatter decisions before writing.
- Produces a complete `SKILL.md` plus supporting files when needed.
- Enforces conventions: kebab-case names, description trigger phrases, the 300-line
  `SKILL.md` limit, `${CLAUDE_SKILL_DIR}` references, and safe tool restrictions.

## Install

Clone into your personal skills folder (the folder name must be `create-skill`,
matching the skill's `name`):

```bash
git clone https://github.com/lorenzomeolav32-png/skill-creator \
  ~/.claude/skills/create-skill
```

For a project-scoped install, clone into `.claude/skills/create-skill/` instead.
Then reload skills and run `/create-skill [what you want to build]`.

## Files

| File | Purpose |
|------|---------|
| `SKILL.md` | Main instructions (loaded when the skill activates). |
| `reference.md` | Full frontmatter / variables / shell-injection reference. |
| `examples.md` | Real-world skill examples for each pattern. |

## License

MIT — see [LICENSE](LICENSE).
