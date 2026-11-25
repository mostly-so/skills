---
name: mostly
description: Set up Mostly and route requests to it. Mostly is a content team for product brands - live social research (outlier posts, comments and accounts on TikTok, Instagram and YouTube), carousels, product photos, AI images and video, UGC videos and scheduled posts. Use when the user mentions Mostly, wants to connect it, asks what it can do, hits a sign-in or credit error, or needs a Mostly tool that no other skill covers.
---

# Mostly

Mostly finds what is working on social, makes your version of it, and schedules it. Every skill in this pack calls Mostly in one of two ways. Both use the same account.

## Setup

**MCP (any MCP client).** Add the remote server; the first call opens the browser to sign in and pick a workspace.

```
https://mostly.so/api/mcp
```

```bash
claude mcp add --transport http --scope user mostly https://mostly.so/api/mcp
```

Other clients (Cursor, Codex, ChatGPT, Gemini CLI, VS Code, Windsurf): https://mostly.so/docs/mcp/setup

**CLI (any agent with a shell).**

```bash
npm i -g mostly
mostly auth login      # opens the browser; the user signs in themselves
mostly auth status
```

Never ask the user to paste an API key into the chat. If the browser login can't work (CI, a remote box), the user can create a key at mostly.so under **Settings → API & MCP** and run `mostly auth login --key …` themselves.

## Calling a tool

- **MCP connected:** call the tool by name (`search_social_posts`, `clone_creative`, …).
- **CLI:** `mostly tools call <tool> --args '<json>'`. `mostly tools list` shows every tool and `mostly tools get <tool>` its inputs.

Tool names and arguments are the same both ways.

## Brands

Most tools work for one brand: its voice, palette, products and connected accounts. List them with `list_brands`. Over MCP pass `brandId` on each call; on the CLI run `mostly brands use <id>` once (or add `--brand <id>`). Add a brand from its website with `create_brand` (`{"url":"https://…"}`); its analysis takes a few minutes, so wait until `list_brands` shows it `COMPLETED`.

## Credits

| Action | Cost |
|---|---|
| `search_social_posts`, `search_social_creators` | 1 credit per platform searched |
| `get_account_outliers` | 1 credit per account |
| `get_post_comments` | 1 credit per post |
| `search_reference_photos` | 1 credit per search |
| Any of the above repeated within 24 hours | Free |
| `import_creative` from a search result | Free |
| Breakdowns and blueprints | Credits the first time, cached after |
| Images, slides, videos, storyboard renders and exports | Depends on the model; price first |

Say what a step will cost before running anything large, and keep to what the user asked for. Storyboard renders, previews and exports return their price when called with `maxCredits: null`.

## Which skill

| The user wants | Skill |
|---|---|
| Find, copy and schedule what is working, end to end | `outliers-to-posts` |
| Posts beating their creator's usual numbers, on a topic or one account | `outlier-post-finder` |
| What viewers ask, love and roast under a post | `comment-mining` |
| Why one account works | `creator-teardown` |
| Several competitors compared | `competitor-research` |
| One post taken apart, with a reusable template | `viral-post-breakdown` |
| A carousel with the same look as a post | `clone-viral-carousel` |
| A proven post turned into an on-brand carousel | `remix-winning-post` |
| A carousel from a topic or outline | `carousel-generator` |
| Product photos and ad sets | `product-photoshoot` |
| Any image or video clip | `image-and-video-generation` |
| A talking-head UGC video, edited | `ugc-video` |
| Drafts and a posting schedule | `schedule-posts` |
| How the accounts are doing and what to post next | `content-performance-review` |

## Ground rules

- **Posting needs the user's approval.** Agents create drafts; the user approves them in Mostly under **Publish**.
- **Proof is real or absent.** Reviews, sales counts and ratings come from material the user gives you, never generated.
- **Public data only.** Research covers public TikTok, Instagram and YouTube posts and accounts.
- **Cite.** Give post links and the numbers a conclusion rests on.
