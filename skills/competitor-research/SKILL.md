---
name: competitor-research
description: Compare several competitors' TikTok, Instagram or YouTube accounts - median views, outlier rate, winning formats, topics and hooks - and find the gaps a brand can own. Use when the user asks "what are my competitors posting", "compare these brands on TikTok", "competitor social analysis", "what's working for brands like mine", or lists several accounts.
---

# Competitor research

Several accounts, each judged against its own baseline, side by side. The output is a brief: what works across the category, who wins at what, and the openings nobody has taken.

**Calling Mostly:** use the Mostly MCP tools if they're connected, otherwise `mostly tools call <tool> --args '<json>'`. Setup and credits: the `mostly` skill.

## 1. Pick the accounts (3-6)

- The user named them → use those.
- Not yet → `search_social_creators` with the category or place ("clean skincare brand", "specialty coffee roaster Melbourne") and propose a shortlist, mixing direct competitors with one or two accounts doing the category best.
- Get the user's own brand with `get_brand_kit` if they have one in Mostly, so the gaps are relative to it.

Cost: 1 credit per account per platform. Say the total before running.

## 2. Read each account

`get_account_outliers` with `account` and `platform` for each. Note median views, the outlier count, and the top posts' formats, topics and hooks. For the two or three best outliers across all accounts, `import_creative` (with the `searchResult`) and `video_breakdown` / `slides_breakdown` to see the structure.

Optional: `get_post_comments` on one top post per leading account, to hear what their audience asks for.

## Output

1. **Comparison table**: account, platform, followers, median views, outliers / posts read, top format, top topic.
2. **What works across the category**: patterns that show up in several accounts' outliers, each with links.
3. **Who wins at what**: one line per account on its edge.
4. **Gaps**: topics, formats or audience questions nobody covers well, the user's opening.
5. **Recommendations**: 3-5 concrete plays for the user's brand, each tied to evidence.

Numbers are a snapshot of recent posts, not a full history; say so. Offer to make the recommended posts (`outliers-to-posts`).
