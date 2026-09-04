---
layout: single
permalink: /ai-slide-decks/
title: "AI Slide Decks"
author_profile: true
redirect_from:
  - /ai-slide-decks
  - /ai-slide-decks.html
slide_decks:
  - file: /slides/Agent_Frameworks.pdf
    title: "Agent Frameworks"
  - file: /slides/LLM01_Prompt_Injection.pdf
    title: "LLM01: Prompt Injection"
  - file: /slides/LLM06_Excessive_Agency.pdf
    title: "LLM06: Excessive Agency"
  - file: /slides/MCP_Basics.pdf
    title: "MCP Basics"
  - file: /slides/agent_runtime_infra.pdf
    title: "Agent Runtime Infrastructure"
---

<!--
  HOW TO ADD A DECK
  ------------------
  1. Drop the PDF into the /slides/ folder in this repo.
  2. Add one entry to the `slide_decks` list in this page's front matter:

     slide_decks:
       - file: /slides/My_New_Deck.pdf
         title: "My New Deck"

     file is the FULL site-relative path (starting with /slides/...).
     Order in the list = order shown on the page (newest usually added last,
     but feel free to reorder).
-->

<style>
.mpk-decks {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin: 1.5em 0 2.5em;
  padding: 0;
  list-style: none;
}

.mpk-decks__item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  padding: 14px 18px;
  border: 1px solid rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  text-decoration: none;
  transition: box-shadow 0.25s ease, transform 0.25s ease;
}

.mpk-decks__item:hover,
.mpk-decks__item:focus {
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.12);
  transform: translateY(-1px);
}

.mpk-decks__title {
  font-weight: 600;
  color: #3f4147;
}

.mpk-decks__arrow {
  color: #52adc8;
  font-size: 1.1em;
}
</style>

These are decks I've put together (with Claude doing the heavy lifting) on some AI topics.

<div class="mpk-decks">
  {% for deck in page.slide_decks %}
  <a class="mpk-decks__item" href="{{ deck.file | relative_url }}" target="_blank" rel="noopener">
    <span class="mpk-decks__title">{{ deck.title }}</span>
    <span class="mpk-decks__arrow">&rarr;</span>
  </a>
  {% endfor %}
</div>
