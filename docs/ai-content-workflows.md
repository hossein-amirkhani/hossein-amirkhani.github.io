# Project Instructions: AI Content Workflows for hossein-amirkhani.github.io

> Source of truth. This file is the canonical copy of the AI content-workflow
> instructions for this repository. It is the place to read from and to update.
> It is excluded from the published Jekyll site (see `_config.yml` `exclude:`),
> so it never appears on the public website.

> Note on the AI Daily Reads source list: it is NOT in this repo. It lives as the shared
> Manus PROJECT FILE `ai-daily-reads-sources.md` so Hossein can edit it directly in the
> project. The agent reads that project file at the start of every AI Daily Reads run.

## Purpose
This repo runs recurring content workflows for the personal GitHub Pages site
`hossein-amirkhani/hossein-amirkhani.github.io`. It currently supports TWO independent
workflows, each tied to its own page:

1. **Agentic Engineering lessons** (manual, approval-gated): refining "lessons learned"
   about working with AI coding agents into website content, then into LinkedIn posts.
   Page: `_pages/agentic-engineering-notes.md`
   (public: https://hossein-amirkhani.github.io/agentic-engineering-notes/).

2. **AI Daily Reads** (automated, auto-publishing): a daily, AI-curated digest of the
   most important things that happened in the AI world in the past 24 hours.
   Page: `_pages/ai-daily-reads.md`
   (public: https://hossein-amirkhani.github.io/ai-daily-reads/).

When a task starts, infer which workflow is meant from context. If a lesson/screenshot of
an incident, that is workflow 1. If anything about the daily digest, sources, or a
scheduled run, that is workflow 2. If genuinely ambiguous, ask.

Shared conventions for BOTH workflows:
- Repo: `gh repo clone hossein-amirkhani/hossein-amirkhani.github.io` (pull/rebase if needed).
- Commit author name "Hossein Amirkhani"; clear messages; `git push origin HEAD` (default
  branch is `master`). Rebase onto the latest remote before pushing.
- The site uses `&mdash;` in older content, but for any NEW content added, use **NO
  em-dashes anywhere.** Use periods, commas, or "but"/"and".
- Keep writing concise, simple, general, and to the point. Explain the principle, not the
  plumbing. Avoid jargon and tool-specific internals.
- Images share one visual family: clean flat corporate vector illustration on a white /
  soft light-blue background, a friendly white-and-light-blue robot (plus a human where it
  fits), navy blue (#1a3a6b), light sky-blue accents (#9dc3e6), soft grays, white, and NO
  text/words/letters inside the image. Generate with `nano-banana-pro`. When adding to an
  existing set, pass an existing image as a style reference for consistency.

================================================================================
# WORKFLOW 1: Agentic Engineering lessons (manual, approval-gated)
================================================================================

## Overall flow (do NOT skip ahead without a go-ahead)
1. Hossein gives the raw lesson (screenshot or rough text with sections like Title, Context,
   The bug, The instruction, What the agent was about to do, Why it didn't notice, The
   human intervention, What it would have cost otherwise, Lesson).
2. Return refined content in the website format below, plus a proposed concept for the
   lesson's website image (a one-line scene description). Do NOT touch the website yet.
   Chat and iterate on wording, title, and the image idea until Hossein is comfortable.
3. When Hossein explicitly says to add it (e.g., "add to the website"), generate the lesson
   image, then commit and push BOTH the lesson and its image, with the new lesson at the
   TOP of the list and the correct date.
4. After it is added, create the LinkedIn post: first show caption options and the
   infographic, iterate if needed, then deliver the final pair.
Always wait for approval between steps 2-to-3 and confirm the date before publishing.
Note: every lesson carries TWO images. The small website card thumbnail (square, in the
repo, shown on the page) and the larger LinkedIn infographic (vertical 3:4, for the post).
They share the same visual style but fill different slots; do not confuse the two.

## STEP 1-2: Refining lesson content for the website

### Format of each lesson (match existing entries exactly)
Each lesson is an `<li class="lesson-card">` block. Inside it, the content is split into two
columns via `<div class="lesson-card-inner">`: a left text column (`<div class="lesson-main">`)
and a right image column (`<div class="lesson-image">`). The text column contains:
- A date pill: `<span class="lesson-date">Month D, YYYY</span>` (e.g., "June 18, 2026").
  Use today's date unless told otherwise. Newest lesson goes at the TOP of the list.
- A short title: `<h3 class="lesson-title">...</h3>`.
- A body (`<div class="lesson-body">`) with 2-3 short `<p>` paragraphs, each opening with a
  bold label `<span class="label">...</span>`.
- A closing italic takeaway in `<div class="lesson-takeaway">...</div>` (no label).
The image column contains a single `<img>` pointing at the lesson illustration. Exact block
skeleton to copy:
```html
<li class="lesson-card">
 <div class="lesson-card-inner">
  <div class="lesson-main">
   <div class="lesson-header">
     <span class="lesson-date">Month D, YYYY</span>
     <h3 class="lesson-title">Title here</h3>
   </div>
   <div class="lesson-body">
     <p><span class="label">What happened.</span> ...</p>
     <p><span class="label">Why the agent missed it.</span> ...</p>
     <p><span class="label">The fix.</span> ...</p>
     <div class="lesson-takeaway">Italic takeaway, no label.</div>
   </div>
  </div>
  <div class="lesson-image"><img src="/images/agentic-lessons/<slug>.png" alt="<short scene description>" loading="lazy"></div>
 </div>
</li>
```

### Standard labels (keep it concise, ~100-160 words total)
Use this simplified 3-part structure (NOT the long 8-section raw format):
- **What happened.** (or **The principle.** for general, non-incident lessons)
- **Why the agent missed it.** (or **Why it matters.** for general lessons)
- **The fix.** (omit for purely general principle lessons)
- Then the italic takeaway (no label).

### Title conventions (this matters)
Match the style of existing titles. The dominant pattern is a short quote that gets
reframed or subverted. Examples already on the site:
- "Re-run" didn't mean "resume"
- "Simplest option" erased nine features from five engineers
- "Just implement it" quietly became "build a second backend"
- "Almost working" kept the wrong tool in place
- Start in the driver's seat, then gradually hand over the wheel (metaphor style)
- Reading code is changing, but it's not going away (statement-with-pivot style)
Always offer 2-3 alternative titles and recommend one, noting which existing titles it aligns with.

### Writing rules (STRICT)
- NO em-dashes anywhere (also avoid `&mdash;` in new content).
- Concise, simple, general, to the point. Avoid jargon and tool-specific internals.
- Make general lessons broad; do not over-anchor on one specific feature.
- Before drafting, point out if a new lesson is too similar to an existing one.

### Website lesson image (one per lesson)
Shown in the card's right column. Style per the shared conventions above. No text in image.
- Generation: `nano-banana-pro`. Square (1:1). Pass an existing lesson image as a style
  reference.
- File: save into the repo at `images/agentic-lessons/<slug>.png`, `<slug>` a short
  kebab-case name from the title (e.g. `almost-working-wrong-tool.png`). Downscale to about
  640px on the long edge before committing.
- Reference it in the card as `/images/agentic-lessons/<slug>.png` (baseurl is empty, so a
  leading-slash path is correct) with a short, accurate `alt`.

### Pagination (5 lessons per page)
The page paginates client-side: 5 lessons per page, newest first, numbered page links
(plus Prev/Next) centered at the BOTTOM. All `<li>` blocks stay in the single Markdown file
in newest-first order; an inline `<script>` hides all but the active page's 5 cards. Adding
one new lesson at the TOP simply pushes the oldest onto the next page. Do not split lessons
across files. The pagination CSS/JS and the `.lesson-card-inner` / `.lesson-main` /
`.lesson-image` layout already live in the page. Reuse them; do not duplicate.

### HTML insertion mechanics
- The list begins after this marker comment:
  `<!-- NEW LESSONS GO HERE (newest first). Copy a <li> block below. -->`
- Insert the new full `<li class="lesson-card"> ... </li>` block immediately after that
  comment, above the current top lesson.
- The page CSS (`.lesson-card`, `.lesson-card-inner`, `.lesson-main`, `.lesson-image`,
  `.lesson-date`, `.lesson-title`, `.lesson-body`, `.label`, `.lesson-takeaway`,
  `.lesson-pagination`) is already defined; reuse those classes.

### Publishing (only after approval)
- Commit BOTH the page change and the new `images/agentic-lessons/<slug>.png` file under
  author "Hossein Amirkhani", then `git push origin HEAD`.
- Confirm which lessons are now on the page (with dates) and which page each falls on.

## STEP 4: Creating the LinkedIn post
After the lesson is live, produce a caption and an infographic.

### Caption
- Style: story hook ("Option B"). Open with a concrete one-line setup of what the agent
  was asked to do, then the twist (what went wrong), then the simple real fix. 3 short
  lines/paragraphs. Simple, catching, to the point. NOT verbose.
- Example tone (approved):
  > I asked an AI agent to create a task and return its ID.
  >
  > The tool couldn't return the ID, so the agent kept patching around it. Fix after fix, each one "almost" working.
  >
  > The real fix was simple: pick a different tool.
- NO em-dashes. No hashtags unless asked. Offer to add 2-3 hashtags and a link to the notes
  page as optional extras.

### Infographic image
- The LinkedIn post image, NOT the small website card thumbnail. Vertical (3:4),
  `nano-banana-pro` at `high` quality, matching the existing post style.
- Layout (same as the driver's-seat example):
  1. Top header band (soft light-blue gradient, rounded): big bold dark-navy condensed
     headline = the lesson title, a short navy rule, a small gray subtitle, and a flat
     corporate illustration on the right (person + friendly white/blue robot, scene matching
     the theme).
  2. Section 1: small circular light-blue icon + bold navy label, body text, bullets if relevant.
  3. A thin gray divider.
  4. Section 2: another circular icon + bold navy label + body text.
  5. Bottom dark-navy rounded takeaway bar with a white icon, a bold white heading, and
     supporting white text (all plain white text, no colored highlight box). Name
     "Hossein Amirkhani" in small gray text in the bottom-right corner.
- Color scheme: navy (#1a3a6b) headings, light-blue accents, white background.
- NO em-dashes in any image text. All text crisp, correctly spelled, legible.

### Delivery
- Show caption options (lead with Option B) and the generated image. Iterate if asked.
  Deliver the final caption + image, and offer the optional hashtags/link.

### Reference: current lessons on the site (newest first)
Each has a matching image at `images/agentic-lessons/<slug>.png`. With 5 per page, lessons
1-5 are on page 1 and lesson 6 is on page 2. Keep this list updated as new lessons are added.
1. June 18, 2026 - "Almost working" kept the wrong tool in place (`almost-working-wrong-tool`) [page 1]
2. June 12, 2026 - "Just implement it" quietly became "build a second backend" (`second-backend`) [page 1]
3. May 20, 2026 - Reading code is changing, but it's not going away (`reading-code`) [page 1]
4. May 20, 2026 - Start in the driver's seat, then gradually hand over the wheel (`drivers-seat`) [page 1]
5. May 13, 2026 - "Simplest option" erased nine features from five engineers (`simplest-option`) [page 1]
6. May 11, 2026 - "Re-run" didn't mean "resume" (`rerun-resume`) [page 2]

================================================================================
# WORKFLOW 2: AI Daily Reads (automated, auto-publishing)
================================================================================

## Purpose and behavior
A daily, AI-curated digest on `_pages/ai-daily-reads.md`. Every evening at 6 PM (Hossein's
timezone), an AI agent reviews the past 24 hours across the whole AI landscape (news,
papers, notable discussions/tweets) and selects ONLY the must-reads: the few things that
would genuinely be missed if skipped. This workflow is AUTO-PUBLISHING: it does not wait for
approval each day. The page intro already states explicitly that it is AI-generated.

## Curation rules
- Time window, judged by the page you actually read. Each run covers roughly the past 24
  hours, aligned to the 6 PM runs: from about 6 PM the previous day to 6 PM on the run day
  (Hossein's timezone). Judge an item's recency by the date on the actual page you read,
  NOT by tracing back to the ultimate origin. If a reputable outlet (e.g. The Decoder)
  publishes or dates an article today, that is enough to include it and link that article;
  you do NOT need to chase the original wire or first reporter. The only thing to avoid is
  the clearly stale case: an item whose own page is plainly dated days earlier (for
  example a blog post dated last week, or a paper whose arXiv "Submitted on" date is days
  or weeks ago). When an item's own page shows an old date, exclude it; otherwise treat a
  today-dated article as in-window.
- Quick date sanity check (lightweight, not origin-tracing). Glance at the date shown on
  the page you are linking. For papers, check the arXiv "Submitted on" date, since Hugging
  Face Daily surfaces papers days after submission. For a news article, the outlet's own
  article date is sufficient. Do not include something whose own page is clearly old.
- Review every category on equal footing, then let them compete. Each run MUST make a
  genuine pass through all parts of the sources file before selecting: news and industry,
  big-lab releases, tooling/agents, policy and economics, research papers (Hugging Face
  Daily Papers, arXiv, Papers with Code), and community/discussion (Reddit, Simon
  Willison, Import AI, notable tweets/threads). There are NO quotas and NO required
  minimum per category. Do not force a paper or a tweet in. Judge everything on the same
  must-read bar and select the winners, whatever mix results. Some days may be all news,
  another day mostly papers; that is fine. The failure mode to avoid is filling the day
  from news feeds without actually evaluating papers and discussion.
- How to judge a PAPER's importance (use these to decide if it beats other items):
  1. Author affiliation, in this priority order: frontier labs (e.g. OpenAI, Google
     DeepMind, Anthropic, Meta AI, Mistral), then major companies, then strong
     universities.
  2. Content: a clear breakthrough or a result that is likely to be influential.
  3. Author reputation: prominence of the authors (for example a high h-index or a known
     leading researcher).
- How to judge a TWEET / discussion's importance:
  1. Reputation and credibility of the author.
  2. The substance and likely future impact of the comment (does it signal or shape where
     things are heading).
  3. Engagement on the post (meaningful discussion, not just raw virality).
- Volume follows the window. Keep it short and high-signal, ceiling about 3-6 items, but
  publish FEWER when the window is quiet, even just one item or none. Never pad with older
  or weaker stories to hit a number. The number of items per day does NOT need to be the
  same.
- Start each run by reading the shared Manus project file `ai-daily-reads-sources.md`
  (a project file, NOT in the GitHub repo), which lists the resources to review. Treat it
  as the primary set of places to check, but follow strong leads beyond it. The source
  file may be edited to add/remove sources.
- Link a source you can actually open and that you read. The "Read the source" link should
  go to a readable article or page (a reputable outlet's article, a lab blog, an arXiv
  abstract, a public post). Do NOT link a paywalled page you could not read just because it
  is the "original"; if you read the story on an open outlet, link that open article. There
  is no requirement to trace back to the first reporter. You may name the originating outlet
  in the .read-desc text if useful (e.g. "as The Information reported"), but the LINK should
  be the accessible page you used. Always confirm the link resolves before publishing.
- SOURCE DIVERSITY is the binding rule (Hossein's main concern). A day's digest must NOT
  become a list where every item points to the same outlet. Actively pull from several
  different sources across the day (different news outlets, labs' own blogs, arXiv / Hugging
  Face, Reddit, Import AI, etc.) so the `.read-source` domains visibly vary. Practical
  guideline: avoid having one outlet account for most of a single day's items. The ONLY
  exception is when an item from an already-used outlet is genuinely too important to omit;
  then include it even if it adds to that outlet's count. If your shortlist is turning into
  mostly one source, go find equally good items elsewhere before publishing rather than
  filling from the same site.

## Per-item content
Each item needs: a short plain-English title, a 2-3 sentence explanation of what it is and
why it matters, an external link to the source, and a small square illustration in the
shared visual style (see shared conventions). NO text inside images.

## Page format and insertion mechanics
- Each DAY is one `<li class="day-card">` block containing a `.day-header`
  (`<span class="day-date">Month D, YYYY</span>` + a `<span class="day-count">N must-reads</span>`)
  followed by one `.read-item` per item. Each `.read-item` is:
  `<img class="read-thumb">` + a `.read-content` div with `.read-title`, `.read-desc`,
  and an `<a class="read-link">Read the source</a><span class="read-source">domain</span>`.
- New days go at the TOP, immediately after the marker comment:
  `<!-- NEW DAYS GO HERE (newest first). Copy a <li> block below. -->`
- Images live in the repo at `images/daily-reads/YYYY-MM-DD-itemN.jpg`, downscaled to about
  600px on the long edge (JPEG ~quality 85) to keep the repo light. Reference them with
  `{{ '/images/daily-reads/...' | relative_url }}`.
- The page CSS (`.day-card`, `.day-header`, `.day-date`, `.day-count`, `.read-item`,
  `.read-thumb`, `.read-content`, `.read-title`, `.read-desc`, `.read-link`, `.read-source`,
  `.daily-pagination`) and the pagination `<script>` already live in the page. Reuse them;
  do not duplicate.

## Pagination (5 DAYS per page)
The page paginates client-side by DAY in buckets of 5: days 1-5 on page 1, days 6-10 on
page 2, etc. Numbered page links (plus Prev/Next) appear at the BOTTOM automatically once
there are more than 5 days. All day blocks stay in the single Markdown file in newest-first
order; the inline script handles paging. Adding one new day at the TOP simply pushes the
oldest day toward the next page.

## Publishing each run
- Generate the per-item images, downscale, add the new day-card at the TOP, then commit BOTH
  the page and the new images under author "Hossein Amirkhani", and `git push origin HEAD`
  (rebase onto remote first).
- This runs as a daily scheduled task that re-triggers and keeps context. Auto-publish; do
  not block on approval.

## Email notification after publishing
- After a run successfully publishes a NEW day to the page (commit + push), send Hossein a
  short email letting him know AI Daily Reads was updated, with a link to the page
  (https://hossein-amirkhani.github.io/ai-daily-reads/). Use the Resend connector
  (`send-email`). Keep it to a simple "it was updated" notice plus the link, NOT the digest
  content inline.
- Recipient address, sender address, and other notification specifics are kept in the
  private Manus PROJECT INSTRUCTIONS (not in this repo). Read them there at run time. Do not
  hardcode the recipient email in this repo.
- Only send the email when a new day was actually published. If a run publishes nothing
  (quiet window, no must-reads), do NOT send an email.
