---
name: creator-teardown
description: Take apart one TikTok, Instagram or YouTube account - creator or brand - to see why it works - its outlier posts, formats, hooks, pillars, cadence and what the audience says - and turn it into a playbook to copy. Use when the user asks "why is @handle doing so well", "break down this creator", "what can I learn from this account", "audit this brand's TikTok", or names one account to study.
---

# Creator teardown

One account, studied against its own baseline: which posts took off, what they share, and what to steal.

**Calling Mostly:** use the Mostly MCP tools if they're connected, otherwise `mostly tools call <tool> --args '<json>'`. Setup and credits: the `mostly` skill.

## 1. Get the account

The user gave a handle or link → use it. Only a niche or a description ("that matcha girl in London") → `search_social_creators` with `query` (words its name or bio would carry) and `platforms` (`TIKTOK`, `INSTAGRAM`), then confirm the account with the user.

## 2. Rank its posts

`get_account_outliers` with `account`, `platform` (1 credit). You get the account's median views, its outlier count, and its recent posts ranked by `multiplier` (views ÷ median). Read the whole list, not only the outliers: the flops show what doesn't work for this audience.

## 3. Study the top 2-3 outliers

For each: `import_creative` with its `searchResult` (free), then `video_breakdown` (videos) or `slides_breakdown` (carousels), and `get_creative_blueprint` for the recipe. `get_post_comments` on the single best post shows what the audience responded to.

## Output

1. **Snapshot**: handle, platform, followers, median views, posts read, outlier rate.
2. **Positioning**: who it is for and the promise, in one line.
3. **Content pillars**: 3-5 recurring topics, with each one's average multiplier.
4. **Formats**: talking head, carousel, tutorial, skit…; length or slide count; what wins vs what flops.
5. **Hook patterns**: the openings of the outliers, as reusable templates.
6. **Cadence**: posting frequency from `publishedAt`.
7. **Outlier table**: link, multiplier, views, format, hook.
8. **Playbook**: 5 things to copy, 2-3 to avoid, and 3 post ideas for the user's brand that use the account's patterns, not its content.

Offer the next step: make those ideas (`outliers-to-posts`) or compare with other accounts (`competitor-research`).
