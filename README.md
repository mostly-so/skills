# Mostly for agents

[Mostly](https://mostly.so) is a content team for small product brands: carousels, product photos, short videos and scheduled posts for TikTok, Instagram, LinkedIn, X and Facebook, all on-brand.

This repo is how you use Mostly from Claude Code, Claude, ChatGPT, Codex, Cursor and other agents. There are three ways in, and they share one account and one backend.

## 1. MCP server (any MCP client)

```
https://mostly.so/api/mcp
```

Streamable HTTP with MCP sign-in (OAuth). Add the URL with no key; the first connect opens your browser to sign in and pick a workspace.

Claude Code:

```bash
claude mcp add --transport http --scope user mostly https://mostly.so/api/mcp
```

Then run `/mcp`, pick **mostly** and choose **Authenticate**.

Setup for Claude, ChatGPT, Codex, Cursor, VS Code, Gemini CLI, Windsurf and others: [mostly.so/docs/mcp/setup](https://mostly.so/docs/mcp/setup).

## 2. Claude Code plugin (skills)

Skills that teach your agent how to get good results out of Mostly: carousels that read well, product photoshoots, and image and video generation.

```
/plugin marketplace add mostly-so/skills
/plugin install mostly@mostly
```

Other agents: copy [`plugin/skills/*`](plugin/skills) into your agent's skills folder (`.claude/skills/`, `.cursor/skills/`, …). See [`plugin/README.md`](plugin/README.md).

## 3. CLI

The skills drive the [`mostly`](https://www.npmjs.com/package/mostly) CLI:

```bash
npm i -g mostly
mostly auth login
mostly slides generate --prompt "5 mistakes killing your cold brew" --aspect-ratio 4:5 --wait
```

`mostly --help` lists every command, and `mostly call <tool>` reaches any tool the MCP server has.

## Links

- Website: [mostly.so](https://mostly.so)
- Docs: [mostly.so/docs](https://mostly.so/docs)
- MCP Registry: `so.mostly/mcp`

## License

[MIT](LICENSE)
