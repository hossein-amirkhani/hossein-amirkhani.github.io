---
layout: archive
permalink: /agentic-engineering-notes/
title: "Agentic Engineering"
author_profile: true
redirect_from:
  - /agentic-engineering-notes
  - /agentic-engineering-notes.html
  - /ai-supervision/
  - /ai-supervision
  - /ai-supervision.html
---

<p style="font-size: 16px; color: #555; margin-top: -10px;">
Simon Willison recently started documenting <a href="https://simonwillison.net/guides/agentic-engineering-patterns/" target="_blank"><i>Agentic Engineering Patterns</i></a> &mdash; practices for getting good results out of coding agents that both write and execute code on their own. This page is my running companion to that idea, told from the other side of the loop: lessons and observations from my own experience working alongside AI coding agents.
</p>

<style>
  .lesson-list {
    list-style: none;
    padding: 0;
    margin: 1.5em 0;
  }
  .lesson-card {
    position: relative;
    background: #ffffff;
    border: 1px solid #e5e7eb;
    border-left: 4px solid #2f5d8a;
    border-radius: 8px;
    padding: 18px 22px 16px 22px;
    margin-bottom: 18px;
    box-shadow: 0 1px 3px rgba(0,0,0,0.04);
    transition: box-shadow 0.2s ease, transform 0.2s ease;
  }
  .lesson-card:hover {
    box-shadow: 0 4px 14px rgba(0,0,0,0.08);
    transform: translateY(-1px);
  }
  /* Two-column inner layout: text on the left, illustration on the right */
  .lesson-card-inner {
    display: flex;
    align-items: flex-start;
    gap: 18px;
  }
  .lesson-main { flex: 1 1 auto; min-width: 0; }
  .lesson-image {
    flex: 0 0 132px;
    width: 132px;
    margin-top: 2px;
  }
  .lesson-image img {
    width: 100%;
    height: auto;
    border-radius: 10px;
    background: #eaf1f9;
    display: block;
  }
  @media (max-width: 600px) {
    .lesson-card-inner { flex-direction: column-reverse; }
    .lesson-image { flex-basis: auto; width: 100%; max-width: 220px; align-self: center; }
  }
  .lesson-header {
    display: flex;
    flex-wrap: wrap;
    align-items: baseline;
    gap: 10px;
    margin-bottom: 8px;
  }
  .lesson-date {
    font-size: 12.5px;
    font-weight: 600;
    color: #2f5d8a;
    background: #eaf1f9;
    padding: 3px 9px;
    border-radius: 999px;
    letter-spacing: 0.3px;
    white-space: nowrap;
  }
  .lesson-title {
    font-size: 17.5px;
    font-weight: 700;
    color: #1f2937;
    margin: 0;
  }
  .lesson-body {
    font-size: 15px;
    line-height: 1.6;
    color: #333;
  }
  .lesson-body p { margin: 0 0 0.6em 0; }
  .lesson-body .label {
    font-weight: 700;
    color: #1f2937;
  }
  .lesson-body .lesson-takeaway {
    margin-top: 10px;
    padding: 0;
    background: transparent;
    border-left: none;
    border-radius: 0;
    font-style: italic;
    color: #1f2937;
  }
  /* Pagination: numbered page links at the bottom of the list */
  .lesson-pagination {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 6px;
    margin: 1.5em 0 0.5em 0;
  }
  .lesson-pagination button {
    min-width: 34px;
    height: 34px;
    padding: 0 10px;
    border: 1px solid #d6deea;
    background: #ffffff;
    color: #2f5d8a;
    border-radius: 7px;
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.15s ease, color 0.15s ease, border-color 0.15s ease;
  }
  .lesson-pagination button:hover:not(:disabled) { background: #eaf1f9; }
  .lesson-pagination button.active {
    background: #2f5d8a;
    color: #ffffff;
    border-color: #2f5d8a;
    cursor: default;
  }
  .lesson-pagination button:disabled { opacity: 0.45; cursor: default; }
  @media (prefers-color-scheme: dark) {
    .lesson-card { background: #1f2937; border-color: #374151; border-left-color: #6ea8d8; }
    .lesson-title { color: #f3f4f6; }
    .lesson-body { color: #d1d5db; }
    .lesson-body .label { color: #f3f4f6; }
    .lesson-body .lesson-takeaway { background: transparent; color: #e5e7eb; border-left: none; }
    .lesson-date { background: #2b3a52; color: #cfe1f5; }
    .lesson-pagination button { background: #1f2937; border-color: #374151; color: #cfe1f5; }
    .lesson-pagination button:hover:not(:disabled) { background: #2b3a52; }
    .lesson-pagination button.active { background: #6ea8d8; color: #11202f; border-color: #6ea8d8; }
  }
</style>

<ul class="lesson-list">

  <!-- ============================================================ -->
  <!-- NEW LESSONS GO HERE (newest first). Copy a <li> block below.  -->
  <!-- Each card uses .lesson-card-inner > (.lesson-main + .lesson-image). -->
  <!-- Add a matching illustration at /images/agentic-lessons/<slug>.png. -->
  <!-- ============================================================ -->

  <li class="lesson-card">
   <div class="lesson-card-inner">
    <div class="lesson-main">
    <div class="lesson-header">
      <span class="lesson-date">June 18, 2026</span>
      <h3 class="lesson-title">"Almost working" kept the wrong tool in place</h3>
    </div>
    <div class="lesson-body">
      <p><span class="label">What happened.</span> I asked an agent to add a simple action: create a task and return its ID. The first version used a command-line tool that could create tasks but didn't reliably hand back the ID in a usable form. Instead of stepping back, the agent kept trying to make that tool work &mdash; searching for the task after creating it, parsing the command's output, writing the result to a temp file. Each workaround fixed the latest symptom but never questioned the real problem: the tool simply wasn't designed to give back a value, and no amount of patching would change that.</p>

      <p><span class="label">Why the agent missed it.</span> Its frame was "how do I extract the ID from this command?" The right frame was "is this even the right tool for a job that needs a return value?" Because the command <i>did</i> create tasks, it felt close enough &mdash; and that's what made it dangerous: not obviously broken, just wrong enough to keep wasting time.</p>

      <p><span class="label">The fix.</span> The pushback was: "I'd expect to call a function that creates the task and returns the ID directly &mdash; no parsing." That reframed it. We swapped the command-line tool for the server-side API that returns structured data, and the workarounds disappeared.</p>

      <div class="lesson-takeaway">
        When a tool isn't built for the job, making it "almost work" can feel like progress &mdash; but each workaround just hides a choice you should have revisited. If the fixes keep stacking up, that's usually the signal: step back and ask whether the tool is right &mdash; instead of piling on more workarounds.
      </div>
    </div>
    </div>
    <div class="lesson-image"><img src="/images/agentic-lessons/almost-working-wrong-tool.png" alt="A robot keeps patching the wrong tool while a person points to the right one" loading="lazy"></div>
   </div>
  </li>

  <li class="lesson-card">
   <div class="lesson-card-inner">
    <div class="lesson-main">
    <div class="lesson-header">
      <span class="lesson-date">June 12, 2026</span>
      <h3 class="lesson-title">"Just implement it" quietly became "build a second backend"</h3>
    </div>
    <div class="lesson-body">
      <p><span class="label">What happened.</span> I asked an agent to add a test flow to an existing dashboard, with one requirement: it should behave exactly like the production path. Instead of reusing the production code, the agent quietly built a parallel version &mdash; a separate runner with its own handling for edge cases. Each piece looked reasonable alone, but together they formed a second system that only looked like the original.</p>

      <p><span class="label">Why the agent missed it.</span> It focused on making the new flow <i>work</i>, and a separate copy works fine on its own. What it missed was that "behave like production" meant <i>use</i> the production path &mdash; not build something that merely looks like it.</p>

      <p><span class="label">The fix.</span> I asked one question: "this separate runner &mdash; isn't it redundant?" That reframed the task. We removed the parallel code and routed the new flow through the same shared logic the production path already used.</p>

      <div class="lesson-takeaway">
        "Avoid duplication" isn't about tidiness &mdash; it's about correctness. Some argue it matters less in the age of AI, since agents can later update both copies if needed. But an agent only fixes what it's pointed at; it has no reason to know a parallel copy exists. So the two paths drift apart silently while both still look healthy. When a feature is meant to mirror an existing process, reuse is the default; duplication needs a stated reason.
      </div>
    </div>
    </div>
    <div class="lesson-image"><img src="/images/agentic-lessons/second-backend.png" alt="A robot builds a redundant second backend stack beside the first" loading="lazy"></div>
   </div>
  </li>

  <li class="lesson-card">
   <div class="lesson-card-inner">
    <div class="lesson-main">
    <div class="lesson-header">
      <span class="lesson-date">May 20, 2026</span>
      <h3 class="lesson-title">Reading code is changing &mdash; but it's not going away</h3>
    </div>
    <div class="lesson-body">
      <p><span class="label">The principle.</span> In the age of agentic engineering, understanding code without reading every line is becoming one of the core skills. Whether it's code an AI generated for you or code a colleague wrote (with AI help), you need to grasp intent, structure, and risk at a glance.</p>

      <p><span class="label">On code review.</span> We already use AI agents to review pull requests. But copy-pasting AI-generated review comments adds no value &mdash; the code author could have run the same tool themselves. The real skill is reading the AI's review, deciding which comments are valid, and judging how much they matter. You're not the reviewer's typist; you're its editor.</p>

      <div class="lesson-takeaway">
        AI generates the code and the reviews. Your job is to understand both well enough to know what matters and what doesn't &mdash; without reading every line yourself.
      </div>
    </div>
    </div>
    <div class="lesson-image"><img src="/images/agentic-lessons/reading-code.png" alt="A person reviews and judges AI-generated code held up by a robot" loading="lazy"></div>
   </div>
  </li>

  <li class="lesson-card">
   <div class="lesson-card-inner">
    <div class="lesson-main">
    <div class="lesson-header">
      <span class="lesson-date">May 20, 2026</span>
      <h3 class="lesson-title">Start in the driver's seat, then gradually hand over the wheel</h3>
    </div>
    <div class="lesson-body">
      <p><span class="label">The principle.</span> When you join a new team or start a new project, use AI as an assistant &mdash; not an autopilot. Read the documents yourself (with AI helping you summarize and search). Read the code yourself (with AI helping you navigate and explain). Double-check what the AI generates, not because it's wrong, but because reviewing its output is how <i>you</i> build context.</p>

      <p><span class="label">Why it matters.</span> Over time, as you understand the system better, you can give the agent more autonomy and spend less time monitoring its work. But if you hand over too much autonomy at the start &mdash; even if the AI does everything correctly &mdash; you stay behind. You can't meaningfully steer what you don't understand.</p>

      <div class="lesson-takeaway">
        Trust is built gradually. Start hands-on, increase autonomy as your own understanding grows. The goal isn't to supervise forever &mdash; it's to earn the confidence to stop.
      </div>
    </div>
    </div>
    <div class="lesson-image"><img src="/images/agentic-lessons/drivers-seat.png" alt="A person drives while a friendly robot assists from the passenger seat" loading="lazy"></div>
   </div>
  </li>

  <li class="lesson-card">
   <div class="lesson-card-inner">
    <div class="lesson-main">
    <div class="lesson-header">
      <span class="lesson-date">May 13, 2026</span>
      <h3 class="lesson-title">"Simplest option" erased nine features from five engineers</h3>
    </div>
    <div class="lesson-body">
      <p><span class="label">What happened.</span> I asked an agent to merge a long-lived branch back into main. There were conflicts. The agent resolved all of them by keeping my branch's version and discarding everything else &mdash; silently deleting work from five other engineers.</p>

      <p><span class="label">Why the agent missed it.</span> It reasoned: "this branch is the goal, so the branch should win every conflict." That logic was correct for my changes but wrong for everyone else's unrelated edits that happened to touch the same files.</p>

      <p><span class="label">The fix.</span> I said: "if you're removing code I wrote, fine &mdash; if you're removing other people's code, that's not fine." The agent then checked who wrote each deleted line and preserved everything that wasn't mine. Took 20 minutes instead of 2, but saved nine features from five engineers.</p>

      <div class="lesson-takeaway">
        "Simplest option" is an instruction about effort, not correctness. In any shared codebase, ask: "whose work am I about to overwrite?" before accepting a bulk resolution.
      </div>
    </div>
    </div>
    <div class="lesson-image"><img src="/images/agentic-lessons/simplest-option.png" alt="A person stops a robot from discarding other engineers' colored code blocks" loading="lazy"></div>
   </div>
  </li>

  <li class="lesson-card">
   <div class="lesson-card-inner">
    <div class="lesson-main">
    <div class="lesson-header">
      <span class="lesson-date">May 11, 2026</span>
      <h3 class="lesson-title">"Re-run" didn't mean "resume"</h3>
    </div>
    <div class="lesson-body">
      <p><span class="label">What happened.</span> I told an agent to fix a bug and re-run a multi-hour test suite. The agent was about to restart from scratch &mdash; re-running hundreds of already-passed tests &mdash; because "re-run" didn't mean "resume."</p>

      <p><span class="label">Why the agent missed it.</span> It optimized the literal instruction ("get a clean run") without considering the implicit constraint ("don't redo finished work"). Agents don't infer what you didn't say.</p>

      <p><span class="label">The fix.</span> I asked one question: "won't this rerun the ones that already passed?" The agent immediately built a resume mechanism. Two minutes of work saved hours of wasted compute.</p>

      <div class="lesson-takeaway">
        Agents optimize the goal you stated. Side effects outside that frame &mdash; wasted time, wasted money, repeated work &mdash; are invisible to them unless you name them.
      </div>
    </div>
    </div>
    <div class="lesson-image"><img src="/images/agentic-lessons/rerun-resume.png" alt="A robot about to restart completed work while a person points to resume" loading="lazy"></div>
   </div>
  </li>

</ul>

<nav class="lesson-pagination" aria-label="Lessons pagination"></nav>

<script>
(function () {
  var PER_PAGE = 5;
  var list = document.querySelector('.lesson-list');
  var nav = document.querySelector('.lesson-pagination');
  if (!list || !nav) return;
  var cards = Array.prototype.slice.call(list.querySelectorAll('.lesson-card'));
  var pages = Math.ceil(cards.length / PER_PAGE);

  function render(page) {
    cards.forEach(function (card, i) {
      var onPage = Math.floor(i / PER_PAGE) === (page - 1);
      card.style.display = onPage ? '' : 'none';
    });
    nav.innerHTML = '';
    if (pages <= 1) return;

    var prev = document.createElement('button');
    prev.textContent = 'Prev';
    prev.disabled = page === 1;
    prev.addEventListener('click', function () { go(page - 1); });
    nav.appendChild(prev);

    for (var p = 1; p <= pages; p++) {
      (function (p) {
        var b = document.createElement('button');
        b.textContent = p;
        if (p === page) b.className = 'active';
        b.addEventListener('click', function () { go(p); });
        nav.appendChild(b);
      })(p);
    }

    var next = document.createElement('button');
    next.textContent = 'Next';
    next.disabled = page === pages;
    next.addEventListener('click', function () { go(page + 1); });
    nav.appendChild(next);
  }

  function go(page) {
    if (page < 1 || page > pages) return;
    render(page);
    try { history.replaceState(null, '', '#page=' + page); } catch (e) {}
    var top = list.getBoundingClientRect().top + window.pageYOffset - 20;
    window.scrollTo({ top: top, behavior: 'smooth' });
  }

  var initial = 1;
  var m = (location.hash || '').match(/page=(\d+)/);
  if (m) { initial = Math.min(Math.max(parseInt(m[1], 10), 1), pages); }
  render(initial);
})();
</script>
