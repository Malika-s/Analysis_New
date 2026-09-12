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
**"Review this lesson"** needs no setup and no API key. It splits the
transcript into assets (time-ranged segments, or word-count chunks for
pasted text with no timestamps) and immediately scans every one of them for
mentions of clearly deprecated tools/versions (Python 2, Internet Explorer,
jQuery 1.x, etc.). You get results the instant you click it.

**"Run Claude's review"** is a separate, optional step underneath, for a
deeper pass. Add your own Anthropic API key and it reads each asset looking
for factual mistakes, outdated explanations, and gaps in coverage, then
folds its findings into the same table.

### "2 — What was checked"
This is the main results table, and it always answers three things:
- **How many assets were checked** — the total count, each named ("Asset 1",
  "Asset 2"...) with the time range or word count it covers
- **How many came back clean** vs. **how many were flagged** — from the
  pattern scan alone if you haven't run Claude's review, or from both
  checks combined once you have
- Per-asset detail: how many pattern matches, and how many issues Claude's
  review found (or "Not run" if you haven't added a key yet)

If a Claude's-review request fails partway through, the remaining assets
are marked "not checked — stopped early" rather than silently skipped, so
you always know exactly how much was actually reviewed.

### About the API key
This calls `api.anthropic.com` directly from the visitor's browser using
their own key — there's no backend. That means the key is visible in the
page's network requests, so:
- Only enter a key on a device/page you trust.
- Use a key with a low spending limit if possible.
- The key is never saved to disk or sent anywhere but Anthropic's API —
  it lives only in that browser tab for that session.

This is the same trade-off as any "bring your own API key" client-side
tool — fine for personal or internal use, not something to hand to the
public on a shared page.

## Embed it on GitHub
Add the file to a repo (rename to `index.html` if it should be the landing
page) and turn on GitHub Pages in Settings, or embed it in an internal page
as raw HTML.
