---
layout: page
title: deadlines
permalink: /deadlines/
description: Submission countdowns for top AI, NLP and computer vision conferences through the end of 2027.
nav: true
nav_order: 4
---

<!-- _pages/deadlines.md: cards are rendered from _data/ai_deadlines.yml -->

<style>
  .dl-intro {
    color: var(--global-text-color-light);
    font-size: 0.9rem;
  }
  .dl-filters {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin: 1rem 0 1.5rem;
  }
  .dl-chip {
    border: 1px solid var(--global-divider-color);
    background: transparent;
    color: var(--global-text-color);
    border-radius: 999px;
    padding: 0.25rem 0.9rem;
    font-size: 0.85rem;
    cursor: pointer;
  }
  .dl-chip:hover {
    border-color: var(--global-theme-color);
  }
  .dl-chip[aria-pressed="true"] {
    background: var(--global-theme-color);
    border-color: var(--global-theme-color);
    color: #fff;
  }
  .dl-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(270px, 1fr));
    gap: 1rem;
  }
  .dl-card {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
    padding: 1rem 1.1rem;
    border: 1px solid var(--global-divider-color);
    border-top: 4px solid var(--global-theme-color);
    border-radius: 0.5rem;
    background: var(--global-card-bg-color);
    color: var(--global-text-color);
  }
  .dl-page [hidden] {
    display: none !important;
  }
  .dl-card[data-urgency="soon"] {
    border-top-color: var(--global-warning-block);
  }
  .dl-card[data-urgency="urgent"] {
    border-top-color: var(--global-danger-block);
  }
  .dl-card[data-urgency="closed"] {
    opacity: 0.55;
    border-top-color: var(--global-divider-color);
  }
  .dl-head {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    gap: 0.5rem;
  }
  .dl-title {
    margin: 0;
    font-size: 1.25rem;
    font-weight: 700;
    color: var(--global-theme-color);
  }
  .dl-full {
    margin: 0.15rem 0 0;
    font-size: 0.8rem;
    line-height: 1.3;
    color: var(--global-text-color-light);
  }
  .dl-tags {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    gap: 0.25rem;
    flex-shrink: 0;
  }
  .dl-tag {
    font-size: 0.7rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.03em;
    padding: 0.1rem 0.45rem;
    border-radius: 0.25rem;
    border: 1px solid var(--global-divider-color);
    color: var(--global-text-color-light);
    white-space: nowrap;
  }
  .dl-status-confirmed {
    color: var(--global-tip-block);
    border-color: var(--global-tip-block);
  }
  .dl-status-estimated {
    color: var(--global-warning-block);
    border-color: var(--global-warning-block);
    border-style: dashed;
  }
  .dl-countdown {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 0.35rem;
    text-align: center;
  }
  .dl-unit {
    padding: 0.35rem 0;
    border-radius: 0.35rem;
    background: var(--global-code-bg-color);
  }
  .dl-num {
    display: block;
    font-size: 1.35rem;
    font-weight: 700;
    font-variant-numeric: tabular-nums;
    line-height: 1.2;
  }
  .dl-lbl {
    display: block;
    font-size: 0.65rem;
    text-transform: uppercase;
    color: var(--global-text-color-light);
  }
  .dl-card[data-urgency="soon"] .dl-num {
    color: var(--global-warning-block);
  }
  .dl-card[data-urgency="urgent"] .dl-num {
    color: var(--global-danger-block);
  }
  .dl-closed-label {
    grid-column: 1 / -1;
    padding: 0.6rem 0;
    border-radius: 0.35rem;
    background: var(--global-code-bg-color);
    font-weight: 700;
    text-transform: uppercase;
    color: var(--global-text-color-light);
  }
  .dl-meta {
    display: grid;
    grid-template-columns: auto 1fr;
    gap: 0.2rem 0.75rem;
    margin: 0;
    font-size: 0.85rem;
  }
  .dl-meta dt {
    font-weight: 600;
    color: var(--global-text-color-light);
  }
  .dl-meta dd {
    margin: 0;
  }
  .dl-local {
    display: block;
    font-size: 0.75rem;
    color: var(--global-text-color-light);
  }
  .dl-note {
    margin: 0;
    font-size: 0.75rem;
    font-style: italic;
    color: var(--global-text-color-light);
  }
  .dl-link {
    margin-top: auto;
    font-size: 0.85rem;
    font-weight: 600;
  }
  .dl-empty {
    color: var(--global-text-color-light);
    font-style: italic;
  }
  .dl-closed {
    margin-top: 2rem;
  }
  .dl-closed summary {
    cursor: pointer;
    font-weight: 600;
    margin-bottom: 1rem;
    color: var(--global-text-color-light);
  }
</style>

{% assign area_labels = "ml:ML / AI,nlp:NLP,cv:Vision" | split: "," %}
{% assign conferences = site.data.ai_deadlines | where_exp: "c", "c.deadline < '2028-01-01'" | sort: "deadline" %}

<div class="dl-page">
  <p class="dl-intro">
    Paper submission deadlines for top AI conferences through December 2027. Times are Anywhere on Earth (AoE, UTC-12), with your local time
    shown below. Cards marked <strong>Estimated</strong> are projected from the previous edition; always check the official call for papers.
  </p>

  <div class="dl-filters" role="group" aria-label="Filter conferences by area">
    <button type="button" class="dl-chip" data-filter="all" aria-pressed="true">All</button>
    <button type="button" class="dl-chip" data-filter="ml" aria-pressed="false">ML / AI</button>
    <button type="button" class="dl-chip" data-filter="nlp" aria-pressed="false">NLP</button>
    <button type="button" class="dl-chip" data-filter="cv" aria-pressed="false">Vision</button>
  </div>

  <div class="dl-grid" id="dl-open">
    {% for c in conferences %}
      {% assign area_label = c.area %}
      {% for pair in area_labels %}
        {% assign kv = pair | split: ":" %}
        {% if kv[0] == c.area %}{% assign area_label = kv[1] %}{% endif %}
      {% endfor %}
      <article class="dl-card" id="{{ c.id }}" data-area="{{ c.area }}" data-deadline="{{ c.deadline }}">
        <header class="dl-head">
          <div>
            <h3 class="dl-title">{{ c.name }} {{ c.year }}</h3>
            <p class="dl-full">{{ c.full_name }}</p>
          </div>
          <div class="dl-tags">
            <span class="dl-tag">{{ area_label }}</span>
            {% if c.status == 'confirmed' %}
              <span class="dl-tag dl-status-confirmed" title="Taken from the official call for papers">Confirmed</span>
            {% else %}
              <span class="dl-tag dl-status-estimated" title="Projected from the previous edition">Estimated</span>
            {% endif %}
          </div>
        </header>

        <div class="dl-countdown" aria-label="Time left until the paper deadline">
          <span class="dl-unit"><span class="dl-num" data-unit="d">--</span><span class="dl-lbl">days</span></span>
          <span class="dl-unit"><span class="dl-num" data-unit="h">--</span><span class="dl-lbl">hrs</span></span>
          <span class="dl-unit"><span class="dl-num" data-unit="m">--</span><span class="dl-lbl">min</span></span>
          <span class="dl-unit"><span class="dl-num" data-unit="s">--</span><span class="dl-lbl">sec</span></span>
        </div>

        <dl class="dl-meta">
          <dt>Paper</dt>
          <dd>
            <time class="dl-aoe" datetime="{{ c.deadline }}">{{ c.deadline | slice: 0, 10 }} AoE</time>
            <span class="dl-local"></span>
          </dd>
          {% if c.abstract_deadline %}
            <dt>Abstract</dt>
            <dd>
              <time class="dl-aoe" datetime="{{ c.abstract_deadline }}">{{ c.abstract_deadline | slice: 0, 10 }} AoE</time>
              <span class="dl-local"></span>
            </dd>
          {% endif %}
          <dt>Dates</dt>
          <dd>{{ c.conf_dates }}</dd>
          <dt>Where</dt>
          <dd>{{ c.location }}</dd>
        </dl>

        {% if c.note %}
          <p class="dl-note">{{ c.note }}</p>
        {% endif %}

        <a class="dl-link" href="{{ c.link }}" target="_blank" rel="noopener noreferrer">Call for papers &rarr;</a>
      </article>
    {% endfor %}

  </div>
  <p class="dl-empty" id="dl-open-empty" hidden>No upcoming deadlines in this area.</p>

  <details class="dl-closed" id="dl-closed-wrap" hidden>
    <summary>Closed deadlines (<span id="dl-closed-count">0</span>)</summary>
    <div class="dl-grid" id="dl-closed"></div>
  </details>
</div>

<script>
  (function () {
    var openGrid = document.getElementById("dl-open");
    var closedGrid = document.getElementById("dl-closed");
    var closedWrap = document.getElementById("dl-closed-wrap");
    var closedCount = document.getElementById("dl-closed-count");
    var openEmpty = document.getElementById("dl-open-empty");
    var chips = document.querySelectorAll(".dl-chip");
    var cards = Array.prototype.slice.call(document.querySelectorAll(".dl-card"));
    var activeFilter = "all";
    var DAY = 86400000;

    /* Etc/GMT+12 is the IANA name for UTC-12 (Anywhere on Earth). */
    var aoeFmt = new Intl.DateTimeFormat(undefined, {
      timeZone: "Etc/GMT+12",
      weekday: "short",
      year: "numeric",
      month: "short",
      day: "numeric",
      hour: "2-digit",
      minute: "2-digit",
    });
    var localFmt = new Intl.DateTimeFormat(undefined, {
      weekday: "short",
      year: "numeric",
      month: "short",
      day: "numeric",
      hour: "2-digit",
      minute: "2-digit",
      timeZoneName: "short",
    });

    document.querySelectorAll("time.dl-aoe").forEach(function (el) {
      var d = new Date(el.getAttribute("datetime"));
      if (isNaN(d)) return;
      el.textContent = aoeFmt.format(d) + " AoE";
      var local = el.parentNode.querySelector(".dl-local");
      if (local) local.textContent = localFmt.format(d) + " your time";
    });

    cards.forEach(function (card) {
      card._deadline = new Date(card.getAttribute("data-deadline")).getTime();
      card._nums = {};
      card.querySelectorAll(".dl-num").forEach(function (n) {
        card._nums[n.getAttribute("data-unit")] = n;
      });
    });

    function pad(n) {
      return n < 10 ? "0" + n : String(n);
    }

    function closeCard(card) {
      card.setAttribute("data-urgency", "closed");
      card.querySelector(".dl-countdown").innerHTML = '<span class="dl-closed-label">Closed</span>';
      closedGrid.appendChild(card);
    }

    function applyFilter() {
      var visibleOpen = 0;
      var closedTotal = 0;
      cards.forEach(function (card) {
        var match = activeFilter === "all" || card.getAttribute("data-area") === activeFilter;
        card.hidden = !match;
        if (card.getAttribute("data-urgency") === "closed") {
          if (match) closedTotal++;
        } else if (match) {
          visibleOpen++;
        }
      });
      openEmpty.hidden = visibleOpen > 0;
      closedWrap.hidden = closedTotal === 0;
      closedCount.textContent = closedTotal;
    }

    function tick() {
      var now = Date.now();
      var changed = false;
      cards.forEach(function (card) {
        if (card.getAttribute("data-urgency") === "closed") return;
        var left = card._deadline - now;
        if (isNaN(left)) return;
        if (left <= 0) {
          closeCard(card);
          changed = true;
          return;
        }
        var urgency = left < DAY ? "urgent" : left < 7 * DAY ? "soon" : "normal";
        if (card.getAttribute("data-urgency") !== urgency) card.setAttribute("data-urgency", urgency);
        var s = Math.floor(left / 1000);
        card._nums.d.textContent = Math.floor(s / 86400);
        card._nums.h.textContent = pad(Math.floor((s % 86400) / 3600));
        card._nums.m.textContent = pad(Math.floor((s % 3600) / 60));
        card._nums.s.textContent = pad(s % 60);
      });
      if (changed) applyFilter();
    }

    chips.forEach(function (chip) {
      chip.addEventListener("click", function () {
        activeFilter = chip.getAttribute("data-filter");
        chips.forEach(function (c) {
          c.setAttribute("aria-pressed", c === chip ? "true" : "false");
        });
        applyFilter();
      });
    });

    tick();
    applyFilter();
    setInterval(tick, 1000);
  })();
</script>
