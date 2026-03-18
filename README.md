# claude-skills

A collection of skills for Claude Code — reusable agent instructions that auto-activate in the right context.

## What are skills?

Skills are modular `.md` files that teach Claude Code how to handle specific workflows. Drop them into `~/.claude/skills/<skill-name>/skill.md` and Claude picks them up automatically.

Compatible with Claude Code, Cursor, Windsurf, and other agents that support the Agent Skills open standard.

## Skills in this repo

| Skill | Description | Install |
|---|---|---|
| [vercel-deploy.md](./vercel-deploy.md) | Deploy to Vercel — auth flow, first deploy, one-deploy rule, SSO removal, anti-patterns | `clawhub install vercel-deploy-pro` |

## Installation

**Via ClawHub (one command):**
```bash
clawhub install vercel-deploy-pro
```

**Manually:**
1. Copy [vercel-deploy.md](./vercel-deploy.md)
2. Save to `~/.claude/skills/vercel-deploy/skill.md`

## Contributing

PRs welcome. Keep skills universal — no personal tokens, IDs, or project-specific references.
