---
layout: archive
permalink: /ai-daily-reads/
title: "AI Daily Reads"
author_profile: true
redirect_from:
  - /ai-daily-reads
  - /ai-daily-reads.html
---

<p style="font-size: 16px; color: #555; margin-top: -10px;">
This page is generated automatically by an AI agent. Every evening it reviews the past 24 hours across the AI world (news, papers, and notable discussions), then selects only the must-reads: the few things you would actually miss if you skipped them. The agent also writes each short note and creates each illustration. Some days have more items, some have fewer. Every item links to its original source so you can read further.
</p>

<style>
  .daily-list {
    list-style: none;
    padding: 0;
    margin: 1.5em 0;
  }
  .day-card {
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
  .day-card:hover {
    box-shadow: 0 4px 14px rgba(0,0,0,0.08);
    transform: translateY(-1px);
  }
  .day-header {
    display: flex;
    flex-wrap: wrap;
    align-items: baseline;
    gap: 10px;
    margin-bottom: 14px;
  }
  .day-date {
    font-size: 12.5px;
    font-weight: 600;
    color: #2f5d8a;
    background: #eaf1f9;
    padding: 3px 9px;
    border-radius: 999px;
    letter-spacing: 0.3px;
    white-space: nowrap;
  }
  .day-count {
    font-size: 12.5px;
    color: #6b7280;
  }
  .read-item {
    display: flex;
    gap: 14px;
    align-items: flex-start;
    padding: 12px 0;
    border-top: 1px solid #f0f1f3;
  }
  .read-item:first-of-type { border-top: none; }
  .read-thumb {
    flex: 0 0 auto;
    width: 84px;
    height: 84px;
    border-radius: 8px;
    object-fit: cover;
    background: #f3f6fb;
    border: 1px solid #e5e7eb;
  }
  .read-content { flex: 1 1 auto; }
  .read-title {
    font-size: 15.5px;
    font-weight: 700;
    color: #1f2937;
    margin: 0 0 4px 0;
    line-height: 1.4;
  }
  .read-desc {
    font-size: 14.5px;
    line-height: 1.55;
    color: #374151;
    margin: 0 0 6px 0;
  }
  .read-link {
    font-size: 13px;
    font-weight: 600;
    color: #2f5d8a;
    text-decoration: none;
  }
  .read-link:hover { text-decoration: underline; }
  .read-source {
    font-size: 12.5px;
    color: #9ca3af;
    margin-left: 6px;
  }
  .daily-pagination {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    justify-content: center;
    margin: 22px 0 10px 0;
  }
  .daily-pagination button {
    min-width: 34px;
    height: 34px;
    padding: 0 10px;
    border: 1px solid #d8dee6;
    background: #ffffff;
    color: #2f5d8a;
    border-radius: 7px;
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.15s ease, color 0.15s ease;
  }
  .daily-pagination button:hover { background: #eaf1f9; }
  .daily-pagination button.active {
    background: #2f5d8a;
    color: #ffffff;
    border-color: #2f5d8a;
    cursor: default;
  }
  .daily-pagination button:disabled {
    color: #c2c8d0;
    cursor: not-allowed;
  }
  @media (max-width: 520px) {
    .read-thumb { width: 64px; height: 64px; }
  }
  @media (prefers-color-scheme: dark) {
    .day-card { background: #1f2937; border-color: #374151; border-left-color: #6ea8d8; }
    .day-date { background: #2b3a52; color: #cfe1f5; }
    .day-count { color: #9aa6b6; }
    .read-item { border-top-color: #2c3a4e; }
    .read-thumb { background: #243044; border-color: #374151; }
    .read-title { color: #f3f4f6; }
    .read-desc { color: #d1d5db; }
    .read-link { color: #6ea8d8; }
    .read-source { color: #7c8a9c; }
    .daily-pagination button { background: #1f2937; color: #6ea8d8; border-color: #374151; }
    .daily-pagination button:hover { background: #2b3a52; }
    .daily-pagination button.active { background: #6ea8d8; color: #0f172a; border-color: #6ea8d8; }
    .daily-pagination button:disabled { color: #4b5563; }
  }
</style>

<ul class="daily-list" id="daily-list">

  <!-- ============================================================ -->
  <!-- NEW DAYS GO HERE (newest first). Copy a <li> block below.    -->
  <!-- Each day is one <li class="day-card"> with a date + items.   -->
  <!-- ============================================================ -->


</ul>

<div class="daily-pagination" id="daily-pagination"></div>

<script>
  (function () {
    var DAYS_PER_PAGE = 5;
    var list = document.getElementById('daily-list');
    var pager = document.getElementById('daily-pagination');
    if (!list || !pager) return;
    var days = Array.prototype.filter.call(list.children, function (el) {
      return el.classList && el.classList.contains('day-card');
    });
    var totalPages = Math.ceil(days.length / DAYS_PER_PAGE);
    var current = 1;

    function render() {
      days.forEach(function (day, i) {
        var page = Math.floor(i / DAYS_PER_PAGE) + 1;
        day.style.display = (page === current) ? '' : 'none';
      });
      pager.innerHTML = '';
      if (totalPages <= 1) return;

      var prev = document.createElement('button');
      prev.textContent = 'Prev';
      prev.disabled = (current === 1);
      prev.addEventListener('click', function () { if (current > 1) { current--; render(); scrollTop(); } });
      pager.appendChild(prev);

      for (var p = 1; p <= totalPages; p++) {
        (function (p) {
          var b = document.createElement('button');
          b.textContent = p;
          if (p === current) b.classList.add('active');
          b.addEventListener('click', function () { current = p; render(); scrollTop(); });
          pager.appendChild(b);
        })(p);
      }

      var next = document.createElement('button');
      next.textContent = 'Next';
      next.disabled = (current === totalPages);
      next.addEventListener('click', function () { if (current < totalPages) { current++; render(); scrollTop(); } });
      pager.appendChild(next);
    }

    function scrollTop() {
      var top = list.getBoundingClientRect().top + window.pageYOffset - 90;
      window.scrollTo({ top: top, behavior: 'smooth' });
    }

    render();
  })();
</script>
