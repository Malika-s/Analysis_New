# Lesson Review — mistakes, outdated content & gaps

A single, self-contained `lesson-review.html` file that reviews one lesson's
worth of content — a transcript, a caption file, a video, or a zipped/tarred
folder of either — and shows exactly what was checked, out of how many, and
how many came back clean vs. flagged.

## Four ways to feed it content
1. **Paste transcript** — just paste text in. No timestamps, so issues are
   located by quote instead of by time.
2. **Upload .srt / .vtt** — the reliable option if you have captions. Keeps
   timestamps, so every flagged issue can point back to a moment.
3. **Upload .mp4** — plays the video silently in the background and
   transcribes it live using your browser's built-in speech recognition.
   This only works in **Chrome or Edge**, needs the full video to play in
   real time, and accuracy varies with audio quality — treat it as a
   convenience for when you don't already have captions, not a reliable
   transcription tool. If it comes up empty, use the .srt tab or paste the
   transcript instead.
4. **Upload .zip / .tar / .tar.gz** — drop a zipped or tarred lesson folder
   and it looks inside for an .srt/.vtt file or an .mp4, extracts whichever
   it finds, and automatically switches to the matching tab above with it
   already loaded.

## How it's organized

**"Review this lesson"** needs no setup and no API key at all. It splits
the transcript into named assets (time-ranged segments, or word-count
chunks for pasted text with no timestamps) and immediately runs four
deterministic checks on every one of them:
- **Known-deprecated tech mentions** — Python 2, Internet Explorer,
  jQuery 1.x, and similar.
- **Overloaded technical acronyms** — terms like "EDA" that get defined
  one way in this video but commonly mean something else elsewhere in a
  tech/data curriculum (e.g. Exploratory Data Analysis vs. Enterprise
  Data Architecture). Not technically "wrong," but a real confusion risk
  worth a glance.
- **Repeated words** — "the the", "is is", the kind of thing that slips
  through a transcript unnoticed.
- **Possible learning-objective gaps** — when a video states an
  objective ("Describe X...") and X's key terms never seem to reappear
  anywhere later in the transcript.

This is instant, needs no setup, and is genuinely useful — but it's still
pattern-matching, not understanding. It can flag a confusing acronym
choice; it can't tell you a stated fact is wrong or an analogy is broken.
That takes actual judgment, which is what Claude's review (below) is for.

**"Run Claude's review"** is a separate, optional step for a deeper pass
that reads the actual content — factual mistakes, outdated explanations,
unclear wording, and coverage gaps a pattern can't catch. It works two
ways, both merging results into the same table:

- **No API key**: pick an asset from the dropdown, click "Copy prompt for
  this asset," paste it into [claude.ai](https://claude.ai) (free, no
  account cost beyond a normal login), then paste Claude's reply back
  into the page and click "Add these results."
- **I have an API key**: paste your own Anthropic API key and click "Run
  Claude's review" to do the same thing automatically, one asset at a
  time, with a progress bar.

There's no way around needing one of these two — some form of AI
judgment is required to catch a wrong fact, and every AI provider
requires a credential of some kind. The manual, no-key path exists
specifically so this still works without ever entering an API key
anywhere.

### "2 — What was checked"
This is the main results table, and it always answers three things:
- **How many assets were checked** — the total count, each named ("Asset 1",
  "Asset 2"...) with the time range or word count it covers
- **How many came back clean** vs. **how many were flagged** — from the
  deterministic checks alone if you haven't run Claude's review, or from
  both combined once you have
- Per-asset detail: how many pattern/structural hits, and how many issues
  Claude's review found (or "Not run" if you haven't done that step yet)

If a Claude's-review request fails partway through, the remaining assets
are marked "not checked — stopped early" rather than silently skipped, so
you always know exactly how much was actually reviewed. Re-running or
reloading an asset's results replaces that asset's issues instead of
stacking duplicates on top.

### About the API key (automatic path only)
This calls `api.anthropic.com` directly from the visitor's browser using
their own key — there's no backend. That means the key is visible in the
page's network requests, so:
- Only enter a key on a device/page you trust.
- Use a key with a low spending limit if possible.
- The key is never saved to disk or sent anywhere but Anthropic's API —
  it lives only in that browser tab for that session.

If you'd rather never enter a key anywhere, use the manual "No API key"
path instead — it gets the same Claude-quality review, just with a
copy/paste step instead of an automatic call.

## Embed it on GitHub
Add the file to a repo (rename to `index.html` if it should be the landing
page) and turn on GitHub Pages in Settings, or embed it in an internal page
as raw HTML.
