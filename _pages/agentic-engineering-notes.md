---
layout: archive
permalink: /agentic-engineering-notes/
title: "Notes on Agentic Engineering: Where the Human Still Matters"
author_profile: true
redirect_from:
  - /agentic-engineering-notes
  - /agentic-engineering-notes.html
  - /ai-supervision/
  - /ai-supervision
  - /ai-supervision.html
---

<p style="font-size: 16px; color: #555; margin-top: -10px;">
Simon Willison recently started documenting <a href="https://simonwillison.net/guides/agentic-engineering-patterns/" target="_blank"><i>Agentic Engineering Patterns</i></a> &mdash; practices for getting good results out of coding agents like Claude Code and Codex, where the agent both writes and <i>executes</i> code, iterating largely on its own. This page is my running companion to that idea, told from the other side of the loop: short case studies from my own projects where a human in the loop still made the difference.
</p>

<p style="font-size: 16px; color: #555;">
Each entry describes what the agent did, where its frame of reasoning fell short, and what the intervention cost &mdash; or saved. Newest notes appear at the top.
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
    padding: 10px 14px;
    background: #f7faff;
    border-left: 3px solid #2f5d8a;
    border-radius: 4px;
    font-style: italic;
    color: #1f2937;
  }
  @media (prefers-color-scheme: dark) {
    .lesson-card { background: #1f2937; border-color: #374151; border-left-color: #6ea8d8; }
    .lesson-title { color: #f3f4f6; }
    .lesson-body { color: #d1d5db; }
    .lesson-body .label { color: #f3f4f6; }
    .lesson-body .lesson-takeaway { background: #111827; color: #e5e7eb; border-left-color: #6ea8d8; }
    .lesson-date { background: #2b3a52; color: #cfe1f5; }
  }
</style>

<ul class="lesson-list">

  <!-- ============================================================ -->
  <!-- NEW LESSONS GO HERE (newest first). Copy a <li> block below.  -->
  <!-- ============================================================ -->

  <li class="lesson-card">
    <div class="lesson-header">
      <span class="lesson-date">May 11, 2026</span>
      <h3 class="lesson-title">When "fix and re-run" silently means "re-run the whole thing"</h3>
    </div>
    <div class="lesson-body">
      <p><span class="label">Context.</span> I'm running a benchmark of <b>332 evaluation cases</b> against an LLM. Each case takes several minutes (the agent spins up a sandbox VM, the model has a conversation, then a grader scores it). The full run takes <b>multiple hours</b> end-to-end. I'm driving this with a Claude-based orchestrator agent.</p>

      <p><span class="label">The bug.</span> Partway through, the orchestrator detects an infrastructure bug &mdash; the LLM-judge isn't being called correctly, so every "criteria" assertion errors out. The agent does the right diagnostic work: identifies the file, applies a one-line fix, and prepares to relaunch.</p>

      <p><span class="label">The instruction.</span> I had told the agent: <i>"If a case fails due to an infra bug, fix the code and re-run until it's resolved."</i></p>

      <p><span class="label">What the agent was about to do.</span> Kill the controller, apply the fix, relaunch. The controller has no built-in resume &mdash; on restart it iterates the suite from case 0. So <b>every case that had already completed correctly would have been re-run</b>.</p>

      <p><span class="label">Why it didn't notice.</span> From the agent's perspective, it was doing exactly what I asked. Nothing in its local reasoning surfaced that "re-run" would silently include already-finished work. The agent wasn't tracking the implicit goal of <i>not wasting compute</i> &mdash; only the explicit goal of <i>getting a clean run</i>.</p>

      <p><span class="label">The human intervention.</span> I asked: <i>"are you sure it won't rerun the previously verified ones?"</i> The agent immediately understood the gap and built the missing piece &mdash; a sidecar file the watcher appends to as cases finish, plus a launcher wrapper that reads it and passes the IDs as <code>exclude_ids</code> on relaunch. Cost: ~2 minutes to design and implement.</p>

      <p><span class="label">What it would have cost otherwise.</span> Hours of duplicate compute &mdash; sandbox VMs, model inference quota, shared sampler time &mdash; to re-derive results that were already on disk.</p>

      <p><span class="label">Lesson.</span> AI coding agents are excellent at executing within the scope of the instruction they're given. Side effects <i>outside</i> that scope &mdash; wasted resources, repeated work, partial-state recovery &mdash; only get caught when a human pattern-matches against the broader system. The instruction "run until clean" implicitly assumes "and don't redo what's already done," but agents don't infer those implicit constraints. They optimize the explicit one.</p>

      <div class="lesson-takeaway">
        This is the case for keeping a human in the loop on long-running agentic workflows. Not because the agent is wrong &mdash; it's not &mdash; but because the agent's frame is narrower than the system's frame, and only the human sees the gap.
      </div>
    </div>
  </li>

</ul>

<p style="font-size: 13.5px; color: #777; margin-top: 2em;">
  More lessons will be added as I encounter them. If you've run into something similar, I'd love to hear about it.
</p>
