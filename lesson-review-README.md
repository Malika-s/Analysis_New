# Lesson Review — mistakes, outdated content & gaps

A single, self-contained `lesson-review.html` file that reviews one lesson's
worth of content — a transcript, a caption file, or a video — for mistakes,
outdated information, coverage gaps, and confusing explanations.

## Three ways to feed it content
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

## The two checks it runs
- **Pattern scan** (no API key needed): flags mentions of clearly deprecated
  tools/versions (Python 2, Internet Explorer, jQuery 1.x, etc.) and any
  year mentions at or before a threshold you set.
- **Claude's review** (needs your own Anthropic API key): reads the
  transcript and flags likely mistakes, outdated information, gaps in
  coverage, and unclear explanations, each with a short quote and
  explanation, and a timestamp when one's available.

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
Same as the other tools in this set: add the file to a repo (rename to
`index.html` if it should be the landing page) and turn on GitHub Pages in
Settings, or embed it in an internal page as raw HTML.
