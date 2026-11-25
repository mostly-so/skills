---
name: image-and-video-generation
description: |
  Generate images and videos with Mostly's image and video models.
  Use when: "generate an image", "make a video", "animate this photo",
  "image-to-video", "edit/restyle this image", "make variants", "which models
  does Mostly have", or the user wants a visual for their brand.
  Brand products are first-class: pass a product id and its photos and facts
  are applied automatically.
  NOT for: product photography sets (use product-photoshoot),
  carousels / slide decks and posting them (use carousel-generator).
---

# Image and video generation

**Calling Mostly:** the commands below use the `mostly` CLI. If the Mostly MCP tools are connected instead, call the same tool names directly (`mostly tools call X --args '{…}'` is the MCP tool `X` with those arguments). Setup, brands and credits: the `mostly` skill.

Generate images and videos through the `mostly` CLI. One command covers both: the model id decides whether it's an image or a video.

## Step 0 — Bootstrap (CLI only; skip with MCP)

1. If `mostly` is not on `$PATH`: `npm i -g mostly`.
2. Run `mostly auth status`. If it says "Not logged in", ask the user to run `mostly auth login` themselves (it opens the browser to sign in) and wait. Never ask the user to paste an API key into chat.
3. If the workspace has several brands and the request is about one of them, run `mostly brands list` and pass `--brand <id>` (or `mostly brands use <id>` once). If the user's brand isn't there yet, add it from its website with `mostly tools call create_brand --args '{"url":"https://…"}'`; analysis takes a few minutes, so re-run `mostly brands list` until its status is `COMPLETED`.

## UX rules

1. Be concise. Deliver result URLs, not JSON or ids.
2. Don't narrate polling. Use `--wait`; it blocks and prints URLs.
3. Pick a sensible default and go. Ask at most one question, only if the subject is genuinely missing.
4. Generation spends the user's credits. Don't run more than the user asked for, and confirm before anything large (4K, long video, many variants).

## Pick a model

Don't rely on memory: models change. Start with the defaults, and check `mostly models list` when the user wants something else (cheaper, faster, a named model).

- **Images:** the default image model (marked `(default)` in `mostly models list`). Use `gpt-image-2-5-*` for on-image text, UI, and typography-heavy graphics.
- **Video:** the default video model. Use `seedance-2-mini` or `veo-3.1-lite` when the user asks for cheap or fast.
- Before passing non-default options, run `mostly models get <id>` and use only the aspect ratios, resolutions and durations it lists.

## Commands

```bash
# Image
mostly generate <imageModel> --prompt "…" [--aspect-ratio 4:5] [--resolution 2K] [--count 1-4] --wait

# Image from a reference (local files are uploaded automatically; URLs pass through)
mostly generate <imageModel> --prompt "same product, on a marble counter" --image ./product.png --wait

# Video: text-to-video
mostly generate <videoModel> --prompt "…" --aspect-ratio 9:16 --duration 5 --wait

# Video: animate an image (first frame), optionally to an end frame
mostly generate <videoModel> --prompt "slow push-in, steam rising" --start-image ./still.png [--end-image ./end.png] --duration 5 --wait

# Feature a brand product (its photos become references, its facts go into the prompt)
mostly tools call list_brand_products
mostly generate <model> --prompt "…" --product <productId> --wait
```

Other flags: `--audio` / `--no-audio` (video models with native audio), `--no-enhance` (skip Mostly's prompt director for images; use when the user wrote an exact prompt), `--wait-timeout 15m` for long videos, `--json` for machine-readable output.

Prompt from a file or a heredoc: `cat prompt.txt | mostly generate <model> --wait`.

## Writing prompts

- **Image:** subject → setting → lighting → camera/lens → mood → style. Mostly's prompt director expands short prompts, so a clear one-sentence brief is enough. Write the full detail yourself only when the user gave a precise art direction (and then pass `--no-enhance`).
- **Video:** describe motion and camera, not just the scene: "slow dolly-in", "handheld pan left", "steam rising, light shifting". With `--start-image`, describe what *changes*; the image already sets the scene.
- **Variants:** `--count 3` gives three takes on one prompt. For genuinely different shots, run separate commands with different prompts.

## Delivering

- Print the result URLs as a short list with a one-line summary (model, aspect ratio, duration for video).
- URLs are signed and expire after about a day. To get fresh ones later: `mostly generations get <id>`.
- If a job fails, say so in one line and offer a retry (maybe a different model).

## Anything else

Every Mostly tool is reachable: `mostly tools list`, then `mostly tools get <name>` for its inputs and `mostly tools call <name> --args '{…}'`. For example brand memory (`search_brand_memory`), reference photos to make images look real (`search_reference_photos`), and social research (`search_social_posts`, `get_account_outliers`; see the `outlier-post-finder` skill).
