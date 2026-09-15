# Course QA Tracker

A single, self-contained `course-qa-tracker.html` file that turns a full
course export into a QA tracker matching the "Module no. / Section Name /
Asset Name / Asset Type / Asset link / Issue(Yes/No) / Issue description /
Action to be taken / Jira Ticket Link" format — one row per real asset in
the course, not a single video at a time.

## This is different from the other two tools
- **`lesson-review.html`** reviews *one* lesson (a transcript, caption
  file, video, or a small zip/tar containing just that lesson's files).
- **`course-qa-tracker.html`** (this one) reviews the **entire course
  export** — every chapter, section, video, reading, lab, and quiz in one
  pass, producing one master tracker.

If you're not sure which asset got analyzed after uploading a full course
`.tar.gz` into the lesson tool, that's why — it was only designed to find
one lesson's worth of files inside an archive. Use this tool instead for
whole-course coverage.

## Upload
The full course export `.tar.gz` or `.zip` pulled from Studio's Export
tab (not a single lesson's folder). It's parsed entirely in your browser.

## What it does automatically (no API key)
Walks the whole course tree and, for every video, reading, lab, and quiz:
- Pulls its real title, its type (derived from the "Video:", "Reading:",
  "Lab:", "Practice Quiz:" style prefix in its name), and the section it
  lives in
- Builds a real deep link back to it on `learning.edx.org`, built from the
  course's org/course/run and that section's block ID — the same link
  format you'd get by right-clicking "copy link" on that section in the
  actual course
- For videos specifically, pulls the real English transcript text (or
  flags "No English transcript found" if the video doesn't have one)
- Runs a pattern scan for known-deprecated tech mentions across everything

This is instant and needs no setup — click "Scan every asset" and the
tracker populates immediately.

## Claude's review (optional, catches real mistakes/gaps)
The pattern scan only catches known deprecated-tech phrases — it can't
tell you a video's analogy is wrong or a quiz's feedback contradicts its
own answer. For that, assets are grouped into batches (to keep prompts a
reasonable size across a whole course) and reviewed by Claude either way:

- **No API key**: pick a batch, click "Copy prompt for this batch", paste
  it into claude.ai (free), then paste Claude's reply back into the page.
  Repeat per batch — a typical course export makes ~15-30 batches.
- **I have an API key**: paste your own Anthropic API key and click "Run
  Claude's review on all batches" to do the same thing automatically.
  This calls `api.anthropic.com` directly from your browser — the key is
  visible in the page's network requests, so only use this on a
  device/page you trust, and prefer a key with a low spending limit.

Either way, results merge into the same tracker rows. Re-running or
reloading a batch replaces that batch's results rather than stacking
duplicates on top.

## The tracker
Search, filter by type or issue status, and fill in "Action to be taken"
and "Jira Ticket Link" directly in the table (typed values are kept for
export). Export as CSV (always works) or XLSX (needs an internet
connection to load the export library; falls back to suggesting CSV if
it can't load).

## Embed it on GitHub
Add the file to a repo (rename to `index.html` if it should be the
landing page) and turn on GitHub Pages in Settings, or embed it in an
internal page as raw HTML.
