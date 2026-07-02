# claude-skills

Vercel deploy skill for Claude Code and OpenClaw.

## Install

**Claude Code** — paste in terminal:
```bash
mkdir -p ~/.claude/skills/vercel-deploy && curl -sL https://raw.githubusercontent.com/ranlywood/claude-skills/main/vercel-deploy.md -o ~/.claude/skills/vercel-deploy/skill.md
```

**OpenClaw** — send this link to your bot:
```
https://clawhub.ai/ranlywood/vercel-deploy-pro
```

## What it does

After install, just say "deploy my landing" or "create a landing about X" — the agent handles the rest:
1. Checks Vercel auth (guides you through it if missing)
2. Creates HTML
3. Deploys
4. Returns the public URL

## Skills

| File | Description |
|---|---|
| [vercel-deploy.md](./vercel-deploy.md) | Vercel deploy — auth flow, first deploy, one-deploy rule, SSO removal |
| [miro-native-mindmap.md](./miro-native-mindmap.md) | Native Miro mind map via MCP + computer use — keyboard mechanics, known failure modes, API limits, verification |

## miro-native-mindmap

**Claude Code** — paste in terminal:
```bash
mkdir -p ~/.claude/skills/miro-native-mindmap && curl -sL https://raw.githubusercontent.com/ranlywood/claude-skills/main/miro-native-mindmap.md -o ~/.claude/skills/miro-native-mindmap/skill.md
```

Prereqs: Miro MCP (`claude mcp add --transport http miro https://mcp.miro.com -s user`, then `claude mcp login miro`), computer use MCP, Miro desktop app. Use a top-tier model with high reasoning effort — the build is ~30 UI batches with live coordinate correction.
