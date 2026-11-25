---
name: schedule-posts
description: Turn finished Mostly carousels, videos or images into scheduled TikTok, Instagram, YouTube, X, LinkedIn and Facebook posts - native captions, connected accounts, posting times - and manage the queue (reschedule, cancel, retry failed posts). Use when the user says "post this", "schedule these for next week", "make a posting plan", "what's scheduled", "move Tuesday's post", or a post failed.
---

# Schedule posts

Agents create **drafts**; the user approves them in Mostly under **Publish**, then they go out at the scheduled time. Say this every time, so nobody thinks a post is live when it isn't.

**Calling Mostly:** use the Mostly MCP tools if they're connected, otherwise `mostly tools call <tool> --args '<json>'`. Setup: the `mostly` skill.

## 1. Check the accounts

`list_integrations` shows the connected accounts and any that need reconnecting. Missing a platform → `get_connect_link` with `platform` (`TIKTOK`, `INSTAGRAM`, `YOUTUBE`, `TWITTER` for X, `LINKEDIN`, `FACEBOOK`) and give the user the link.

## 2. Make sure the media is ready

- Carousel: every slide rendered (`get_slide_deck`; CLI `mostly slides get <id>`).
- Video: a finished storyboard export (`get_storyboard_export` says `COMPLETED`).
- Anything else: the image or video URLs.

## 3. Write the caption

Native to each platform: hook in the first line; TikTok and Instagram 3-5 relevant hashtags; LinkedIn no hashtag wall, a clear point of view; X short. If the platforms need very different captions, make one draft per platform.

## 4. Create the draft

`create_post_draft` with:
- `content`: the caption
- `platforms`: e.g. `["TIKTOK", "INSTAGRAM"]`; every connected account on those platforms is targeted
- one source of media: `slideDeckId` (carousel, slides in order), `storyboardExportId` (video), or `mediaUrls`
- `scheduledFor`: ISO 8601 with the user's UTC offset (`2026-12-01T09:00:00+08:00`); null posts right after approval
- `title`: optional (TikTok photo posts show up to 90 characters)
- `tiktokPrivacyLevel`: only if the user said so

TikTok, Instagram and YouTube need media; YouTube needs exactly one video. Then tell the user the drafts are waiting in **Publish → Drafts** at mostly.so.

## 5. Plan a schedule

For a batch, spread posts out: about one a day per platform, at times the user's audience is awake, never two on one platform within a few hours. Show the plan as a table (date and time, platforms, post, caption's first line) before creating the drafts.

## Manage the queue

| Need | Call |
|---|---|
| What's drafted, scheduled, published or failed | `list_posts` (filter by status, platform or text) |
| One post's status and live links | `get_post` |
| Change caption, media, platforms or time | `update_post`; a new `scheduledFor` reschedules it |
| Unschedule | `cancel_post`; it goes back to drafts |
| A post failed | `get_post` for the error, fix it (often a reconnect), then `retry_post`; it posts only to the channels that failed |

Published posts can't be edited.
