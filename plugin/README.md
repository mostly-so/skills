# Mostly skills

Skills that let coding agents (Claude Code, Cursor, Codex, …) use Mostly through the [`mostly` CLI](https://www.npmjs.com/package/mostly).

| Skill | What it does |
|---|---|
| `mostly-generate` | Images and videos from any Mostly model, with reference images, start/end frames and brand products |
| `mostly-product-photoshoot` | Studio, lifestyle, close-up, conceptual and banner product shots; coordinated ad sets |
| `mostly-slides` | Plan and render carousels, edit single slides, and create post drafts for TikTok / Instagram / LinkedIn / X / Facebook |

## Install

Claude Code:

```
/plugin marketplace add mostly-so/skills
/plugin install mostly@mostly
```

Other agents: copy `skills/*` into the agent's skills folder (e.g. `.claude/skills/`, `.cursor/skills/`).

Then install and log in to the CLI:

```bash
npm i -g mostly
mostly auth login
```
