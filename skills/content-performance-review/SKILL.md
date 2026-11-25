---
name: content-performance-review
description: Review how a brand's TikTok, Instagram, YouTube and Facebook accounts are performing - totals vs the previous period, breakout posts, underperformers, which remixed formats worked - and decide what to post next. Use when the user asks "how are my posts doing", "what's working for us", "weekly content report", "which format should we do more of", or wants a performance recap before planning.
---

# Content performance review

Judge every post against the account's own usual numbers, then turn the result into the next posts.

**Calling Mostly:** use the Mostly MCP tools if they're connected, otherwise `mostly tools call <tool> --args '<json>'`. Setup: the `mostly` skill.

## 1. Pull the numbers

- `get_analytics` with `days` (default 30, up to 365); `allBrands: true` for the whole workspace. It covers every post on the brand's connected Instagram, TikTok, YouTube and Facebook accounts, not only ones posted through Mostly: totals vs the previous period, per platform and per account, top posts, breakouts (2× the account's usual views or more), underperformers (half or less), and views gained per day. X and LinkedIn have no analytics.
- `get_remix_results`: posts published through Mostly, matched to the viral post or format each one remixed, with a per-format summary.
- `list_posts` with a status filter for what is scheduled next and anything that failed.

## 2. Read it

- Compare breakouts with underperformers: format, hook, length, topic, posting time. What do the winners share that the losers lack?
- Remixed formats with a high median multiplier are worth repeating; formats that flopped twice are not.
- Note anything broken: failed posts, accounts that need reconnecting (`list_integrations`).

## Output

1. **Headline**: views and engagement vs the previous period, in one or two lines.
2. **Breakouts**: link, platform, multiplier, why it likely worked.
3. **Underperformers**: what they have in common.
4. **Formats**: what to do more of and what to drop, from `get_remix_results`.
5. **Next posts**: 3-5 concrete ideas built on the winners. For fresh ideas from outside the account, run `outlier-post-finder` on the winning topics.

Offer to make and schedule them (`outliers-to-posts`, `schedule-posts`).
