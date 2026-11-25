---
name: outlier-post-finder
description: Find TikTok, Instagram and YouTube posts that beat their creator's own baseline - on a topic or niche, or across one account's recent posts - and pull out the patterns and hooks worth reusing. Use when the user asks "what's working in my niche", "find viral posts about X", "which of @handle's posts blew up", "outliers", "top performing posts", or wants evidence before making content.
---

# Outlier post finder

Raw views mislead: a million views is normal for a big account and a fluke for a small one. Mostly ranks posts by how far each beat what is usual for its own creator.

**Calling Mostly:** use the Mostly MCP tools if they're connected, otherwise `mostly tools call <tool> --args '<json>'`. Setup and credits: the `mostly` skill.

## Pick the mode

**Topic or niche** → `search_social_posts`
- `query`: how people would caption it ("morning skincare routine", "things I wish I knew before Japan"). Two or three focused queries beat one broad one.
- `platforms`: `TIKTOK`, `INSTAGRAM`, `YOUTUBE` (default all three; 1 credit each).
- `mediaType`: `VIDEO` or `CAROUSEL` when only one matters.

**One account** → `get_account_outliers`
- `account`: handle (with or without @) or profile link; `platform`.
- `outliersOnly: true` keeps posts at 2.5× the account's median views or more.
- The response gives the account's median views and how many outliers it has.

**No accounts yet?** `search_social_creators` with a niche or place finds accounts, biggest first; then run `get_account_outliers` on the interesting ones.

Repeating a query or account within 24 hours is free.

## Read the numbers

- `signal.kind: "USUAL_VIEWS"`, `times: 6.2` → 6.2× the creator's median views. Strongest evidence.
- `signal.kind: "FOLLOWERS"`, `times: 1.4` → views per follower, when no median is known.
- `multiplier` (account mode) → views ÷ the account's median; `null` when the post shows no views (Instagram carousels), so judge those by likes and comments.
- Check `publishedAt`: a 2× post from yesterday is still climbing; a 2× post from last year is not news.

## Output

1. **Outlier table**: rank, link, account, views, multiplier or signal, format (video/carousel, length or slide count), posted date, the hook (first line of the caption).
2. **Patterns**: 3-5 things the outliers share (format, hook type, topic, length, on-screen text), each backed by the posts that show it.
3. **Hooks to adapt**: rewrite the strongest hooks as reusable patterns ("I tried {X} for {time} so you don't have to"), not copies.
4. **Next step**: offer to break the top ones down (`viral-post-breakdown`), mine their comments (`comment-mining`), or make versions for the user's brand (`outliers-to-posts`).

To save a result for later, `import_creative` with its `searchResult` object (free).
