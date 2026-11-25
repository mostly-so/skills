# Social Media Content Skills for AI Agents

**Find what's working on TikTok, Instagram and YouTube, make your brand's version, and schedule it.** Powered by [Mostly](https://mostly.so).

Most research tools stop at a spreadsheet of viral posts. These skills give your agent the whole loop: find posts that beat their creator's usual numbers, work out why they took off, then make on-brand carousels, product photos and UGC videos from them and line them up as scheduled posts.

```bash
npx skills add mostly-so/social-media-content-skills
```

Works with Claude Code, Cursor, OpenAI Codex, GitHub Copilot, Gemini CLI, Windsurf and any agent that supports the [Agent Skills](https://agentskills.io) format.

## Connect Mostly

The skills call Mostly. Pick one way in; both use the same account.

**MCP** (Claude, ChatGPT, Cursor, Codex, VS Code and other MCP clients). Add the URL; the first call opens the browser to sign in:

```
https://mostly.so/api/mcp
```

```bash
claude mcp add --transport http --scope user mostly https://mostly.so/api/mcp
```

**CLI** (any agent with a shell):

```bash
npm i -g mostly
mostly auth login
```

Setup for every client: [mostly.so/docs/mcp/setup](https://mostly.so/docs/mcp/setup)

## Skills

### Research: find what's working

| Skill | Use it when you want to… | You get |
|---|---|---|
| [`outlier-post-finder`](skills/outlier-post-finder/) | Find posts on a topic, or on one account, that beat their creator's usual views | Outlier table with multipliers, shared patterns, hooks to adapt |
| [`comment-mining`](skills/comment-mining/) | Hear what viewers ask, want, object to and roast | Voice-of-customer report with verbatim quotes, FAQs, content ideas |
| [`creator-teardown`](skills/creator-teardown/) | Understand why one creator or brand account works | Pillars, formats, hook patterns, cadence, a playbook to copy |
| [`competitor-research`](skills/competitor-research/) | Compare several competitors side by side | Comparison table, category patterns, gaps you can own |
| [`viral-post-breakdown`](skills/viral-post-breakdown/) | Take one post or Meta ad apart | Hook, shot-by-shot or slide-by-slide structure, transcript, a fill-in template |

### Make: your brand's version

| Skill | Use it when you want to… | You get |
|---|---|---|
| [`clone-viral-carousel`](skills/clone-viral-carousel/) | Make a carousel that looks like a specific post, with your content | A rendered carousel, slide for slide in the original's layout |
| [`remix-winning-post`](skills/remix-winning-post/) | Turn a proven post into an on-brand carousel | A rendered carousel in your brand's voice, palette and products |
| [`carousel-generator`](skills/carousel-generator/) | Make a carousel or slide deck from a topic or outline | A rendered deck you can edit slide by slide |
| [`product-photoshoot`](skills/product-photoshoot/) | Shoot packshots, lifestyle scenes and ad sets from a product photo | Studio-quality product images |
| [`ugc-video`](skills/ugc-video/) | Make a talking-head UGC video about your product | An edited MP4: avatar takes, jump cuts, captions, product overlays, music |
| [`image-and-video-generation`](skills/image-and-video-generation/) | Generate any image or video clip | Images and videos from current image and video models |

### Ship: post and learn

| Skill | Use it when you want to… | You get |
|---|---|---|
| [`schedule-posts`](skills/schedule-posts/) | Post to TikTok, Instagram, YouTube, X, LinkedIn and Facebook | Scheduled drafts with native captions, a posting plan, queue fixes |
| [`content-performance-review`](skills/content-performance-review/) | See how your accounts are doing and what to post next | Breakouts, underperformers, winning formats, next post ideas |

### The full loop

| Skill | Use it when you want to… | You get |
|---|---|---|
| [`outliers-to-posts`](skills/outliers-to-posts/) | Go from "what's working in my niche?" to scheduled posts in one run | Researched, made and scheduled posts, each traced to the post it learned from |
| [`mostly`](skills/mostly/) | Set up Mostly, check credits, or reach any Mostly tool | Setup, routing and costs |

## Example prompts

```text
Find the outlier carousels about home espresso on TikTok and Instagram from the last month.
```

```text
Which of @ritual's recent TikToks blew up, and what do they have in common?
```

```text
Read the comments on this reel and tell me what people keep asking: https://www.instagram.com/reel/…
```

```text
Compare Glossier, Rare Beauty and Summer Fridays on TikTok. Where's the gap for us?
```

```text
Clone this carousel's look for our brand, about 5 cold brew mistakes: https://www.tiktok.com/@…/photo/…
```

```text
Find what's working for skincare brands this week, make three carousels for us from it, and schedule them Monday to Wednesday at 9am.
```

## How the skills fit together

```text
   RESEARCH                     MAKE                         SHIP
 outlier-post-finder  ──►  clone-viral-carousel   ──►  schedule-posts
 comment-mining            remix-winning-post               │
 creator-teardown          carousel-generator               ▼
 competitor-research       ugc-video                 content-performance-review
 viral-post-breakdown      product-photoshoot               │
                           image-and-video-generation       │
        ▲                                                   │
        └──────────── what worked feeds the next search ────┘

            outliers-to-posts runs the whole loop
```

## Principles

1. **Baseline, not vanity metrics.** A post is judged against its own creator's median views, so a small account's breakout counts and a big account's average post doesn't.
2. **Cite everything.** Post links and numbers sit next to every conclusion.
3. **Exact words matter.** Hooks, captions and comments are kept verbatim.
4. **Borrow the pattern, not the post.** Remixes and clones take structure and style, never a creator's face, photos or copy.
5. **Spend in the open.** Research costs 1 credit per platform or account (repeats within 24 hours are free), and renders are priced before they run.
6. **You approve what goes live.** Agents create drafts; you approve them in Mostly.
7. **Public data only.** Research covers public TikTok, Instagram and YouTube posts and accounts, plus Meta Ad Library ads by link.

## Claude Code plugin

The same skills ship as a Claude Code plugin with the Mostly MCP server bundled:

```
/plugin marketplace add mostly-so/social-media-content-skills
/plugin install mostly@mostly
```

## Links

- [Mostly](https://mostly.so)
- [Docs](https://mostly.so/docs)
- [MCP setup](https://mostly.so/docs/mcp/setup)
- [`mostly` CLI on npm](https://www.npmjs.com/package/mostly)
- MCP Registry: `so.mostly/mcp`

## License

[MIT](LICENSE)
