# claude-skills

A collection of skills for Claude Code — reusable agent instructions that auto-activate in the right context.

## What are skills?

Skills are modular `.md` files that teach Claude Code how to handle specific workflows. Drop them into `~/.claude/skills/<skill-name>/skill.md` and Claude picks them up automatically.

Compatible with Claude Code, Cursor, Windsurf, and other agents that support the Agent Skills open standard.

## Skills in this repo

| Skill | Description |
|---|---|
| [vercel-deploy](./vercel-deploy/skill.md) | Deploy to Vercel — pre-deploy checklist, one-deploy rule, SSO removal, anti-patterns |

## Installation

```bash
# Clone the repo
git clone https://github.com/ranlywood/claude-skills.git

# Copy a skill to your Claude skills folder
cp -r claude-skills/vercel-deploy ~/.claude/skills/
```

Or just copy the `skill.md` file manually.

## Contributing

PRs welcome. Keep skills universal — no personal tokens, IDs, or project-specific references.
