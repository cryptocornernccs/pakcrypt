---
layout: post
title: "Governance of Common Knowledge"
---
<style>
/* ─── Google Fonts ─────────────────────────────────────────────── */
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;0,700;0,900;1,400;1,700&family=Source+Serif+4:ital,opsz,wght@0,8..60,300;0,8..60,400;0,8..60,600;1,8..60,300;1,8..60,400&family=JetBrains+Mono:wght@400;600&display=swap');

/* ─── CSS Variables (dark-theme aware) ─────────────────────────── */
:root {
  --bg:           #1b1b1e;
  --surface:      #242428;
  --surface2:     #2c2c31;
  --border:       #383840;
  --text:         #e2e2e4;
  --text-muted:   #9898a4;
  --accent:       #c9a84c;
  --accent-dim:   rgba(201,168,76,0.15);
  --accent-glow:  rgba(201,168,76,0.08);
  --red:          #e05c5c;
  --blue:         #6bb5d6;
  --green:        #6dcf94;
  --font-serif:   'Source Serif 4', Georgia, serif;
  --font-display: 'Playfair Display', Georgia, serif;
  --font-mono:    'JetBrains Mono', 'Courier New', monospace;
}

/* ─── Reset & Layout ───────────────────────────────────────────── */
.ckp-article * { box-sizing: border-box; }
.ckp-article {
  font-family: var(--font-serif);
  font-size: 1.08rem;
  line-height: 1.82;
  color: var(--text);
  max-width: 100%;
  position: relative;
}

/* ─── Progress Bar ─────────────────────────────────────────────── */
#ckp-progress {
  position: fixed;
  top: 0; left: 0;
  height: 3px;
  width: 0%;
  background: linear-gradient(90deg, var(--accent), #e8c96a);
  z-index: 9999;
  transition: width 0.1s linear;
  box-shadow: 0 0 10px rgba(201,168,76,0.5);
}

/* ─── Hero ─────────────────────────────────────────────────────── */
.ckp-hero {
  padding: 3.5rem 0 2rem;
  border-bottom: 1px solid var(--border);
  margin-bottom: 0;
}
.ckp-kicker {
  font-family: var(--font-mono);
  font-size: 0.72rem;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 1.2rem;
  display: flex;
  align-items: center;
  gap: 0.75rem;
}
.ckp-kicker::before {
  content: '';
  display: inline-block;
  width: 28px; height: 1px;
  background: var(--accent);
}
.ckp-hero h1 {
  font-family: var(--font-display);
  font-size: clamp(2rem, 4.5vw, 3.4rem);
  font-weight: 900;
  line-height: 1.12;
  color: #f0f0f0;
  margin: 0 0 1rem;
  letter-spacing: -0.01em;
}
.ckp-hero h1 em {
  font-style: italic;
  color: var(--accent);
}
.ckp-deck {
  font-family: var(--font-serif);
  font-size: clamp(1rem, 2vw, 1.2rem);
  font-weight: 300;
  color: var(--text-muted);
  line-height: 1.6;
  max-width: 700px;
  margin-bottom: 1.8rem;
  font-style: italic;
}
.ckp-meta {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 1.2rem;
  font-family: var(--font-mono);
  font-size: 0.72rem;
  color: var(--text-muted);
  letter-spacing: 0.06em;
}
.ckp-meta span { display: flex; align-items: center; gap: 0.4rem; }
.ckp-meta .dot {
  width: 3px; height: 3px;
  border-radius: 50%;
  background: var(--border);
  display: inline-block;
}
.ckp-meta a {
  color: var(--accent);
  text-decoration: none;
  border-bottom: 1px solid transparent;
  transition: border-color 0.2s;
}
.ckp-meta a:hover { border-color: var(--accent); }

/* ─── Two-column layout wrapper ───────────────────────────────── */
.ckp-layout {
  display: grid;
  grid-template-columns: 1fr 260px;
  gap: 3rem;
  align-items: start;
  margin-top: 2.5rem;
}
@media (max-width: 900px) {
  .ckp-layout { grid-template-columns: 1fr; }
  .ckp-sidebar { display: none; }
}

/* ─── Sidebar TOC ─────────────────────────────────────────────── */
.ckp-sidebar {
  position: sticky;
  top: 5rem;
  max-height: calc(100vh - 8rem);
  overflow-y: auto;
  scrollbar-width: thin;
  scrollbar-color: var(--border) transparent;
}
.ckp-toc-label {
  font-family: var(--font-mono);
  font-size: 0.65rem;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--text-muted);
  margin-bottom: 1rem;
  padding-bottom: 0.5rem;
  border-bottom: 1px solid var(--border);
}
.ckp-toc-list {
  list-style: none;
  padding: 0; margin: 0;
}
.ckp-toc-list li {
  margin: 0;
  border-left: 2px solid transparent;
  transition: border-color 0.2s;
}
.ckp-toc-list li.active {
  border-color: var(--accent);
}
.ckp-toc-list a {
  display: block;
  padding: 0.35rem 0.75rem;
  font-family: var(--font-serif);
  font-size: 0.8rem;
  color: var(--text-muted);
  text-decoration: none;
  transition: color 0.2s;
  line-height: 1.4;
}
.ckp-toc-list li.active a,
.ckp-toc-list a:hover { color: var(--accent); }
.ckp-toc-list .toc-sub a {
  padding-left: 1.5rem;
  font-size: 0.74rem;
  opacity: 0.8;
}

/* ─── Body prose ───────────────────────────────────────────────── */
.ckp-body { min-width: 0; }

.ckp-body section { margin-bottom: 3.5rem; }

.ckp-body h2 {
  font-family: var(--font-display);
  font-size: clamp(1.4rem, 2.8vw, 2rem);
  font-weight: 700;
  color: #f0f0f0;
  line-height: 1.2;
  margin: 3.5rem 0 1.2rem;
  padding-top: 1rem;
  border-top: 1px solid var(--border);
  scroll-margin-top: 5rem;
}
.ckp-body h3 {
  font-family: var(--font-display);
  font-size: 1.2rem;
  font-weight: 600;
  color: #dcdce0;
  margin: 2.5rem 0 0.8rem;
  scroll-margin-top: 5rem;
}
.ckp-body h4 {
  font-family: var(--font-mono);
  font-size: 0.75rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--accent);
  margin: 2rem 0 0.6rem;
}
.ckp-body p { margin: 0 0 1.3rem; }

/* Drop cap for first paragraph after hero */
.ckp-body .drop-cap::first-letter {
  font-family: var(--font-display);
  font-size: 4.4rem;
  font-weight: 900;
  float: left;
  line-height: 0.78;
  margin: 0.12em 0.12em -0.06em 0;
  color: var(--accent);
}

/* ─── Pull Quotes ─────────────────────────────────────────────── */
.ckp-pull {
  margin: 2.5rem -1.5rem;
  padding: 1.8rem 2.2rem 1.8rem 2.5rem;
  border-left: 3px solid var(--accent);
  background: var(--accent-glow);
  position: relative;
}
@media (max-width: 700px) { .ckp-pull { margin: 2rem 0; } }
.ckp-pull::before {
  content: '\201C';
  font-family: var(--font-display);
  font-size: 5rem;
  color: var(--accent);
  opacity: 0.25;
  position: absolute;
  top: -0.5rem; left: 0.5rem;
  line-height: 1;
}
.ckp-pull p {
  font-family: var(--font-display);
  font-size: clamp(1.1rem, 2vw, 1.3rem);
  font-style: italic;
  font-weight: 400;
  color: #f0f0f0;
  line-height: 1.5;
  margin: 0;
  position: relative;
}
.ckp-pull cite {
  display: block;
  margin-top: 0.7rem;
  font-family: var(--font-mono);
  font-size: 0.68rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--text-muted);
  font-style: normal;
}

/* ─── Abstract box ─────────────────────────────────────────────── */
.ckp-abstract {
  background: var(--surface);
  border: 1px solid var(--border);
  border-top: 3px solid var(--accent);
  padding: 1.8rem 2rem;
  margin-bottom: 2.5rem;
  font-size: 0.95rem;
}
.ckp-abstract-label {
  font-family: var(--font-mono);
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 0.8rem;
}
.ckp-abstract p {
  margin: 0;
  color: var(--text-muted);
  font-style: italic;
}

/* ─── Callout boxes ─────────────────────────────────────────────── */
.ckp-callout {
  background: var(--surface);
  border: 1px solid var(--border);
  border-left: 3px solid var(--blue);
  padding: 1.2rem 1.5rem;
  margin: 2rem 0;
  font-size: 0.92rem;
}
.ckp-callout.warn { border-left-color: #e0935c; }
.ckp-callout.key  { border-left-color: var(--green); }
.ckp-callout strong {
  font-family: var(--font-mono);
  font-size: 0.68rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--blue);
  display: block;
  margin-bottom: 0.5rem;
}
.ckp-callout.warn strong { color: #e0935c; }
.ckp-callout.key  strong { color: var(--green); }

/* ─── Layer model ─────────────────────────────────────────────── */
.ckp-layers {
  margin: 2rem 0;
  border: 1px solid var(--border);
  overflow: hidden;
}
.ckp-layer {
  display: grid;
  grid-template-columns: 56px 1fr;
  border-bottom: 1px solid var(--border);
  transition: background 0.2s;
}
.ckp-layer:last-child { border-bottom: none; }
.ckp-layer:hover { background: var(--surface); }
.ckp-layer-badge {
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--surface2);
  font-family: var(--font-mono);
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--accent);
  border-right: 1px solid var(--border);
  padding: 1rem;
}
.ckp-layer-body { padding: 1rem 1.2rem; }
.ckp-layer-body strong {
  font-family: var(--font-display);
  color: #f0f0f0;
  display: block;
  margin-bottom: 0.25rem;
  font-size: 0.95rem;
}
.ckp-layer-body p {
  margin: 0;
  font-size: 0.85rem;
  color: var(--text-muted);
  line-height: 1.55;
}

/* ─── Archetype cards ─────────────────────────────────────────── */
.ckp-archetypes { margin: 2rem 0; }
.ckp-archetype {
  border: 1px solid var(--border);
  margin-bottom: 1rem;
  overflow: hidden;
  transition: border-color 0.2s;
}
.ckp-archetype:hover { border-color: var(--accent); }

.ckp-arch-header {
  display: grid;
  grid-template-columns: 52px 1fr auto;
  align-items: center;
  gap: 1rem;
  padding: 1rem 1.2rem;
  cursor: pointer;
  background: var(--surface);
  user-select: none;
}
.ckp-arch-num {
  font-family: var(--font-mono);
  font-size: 1.4rem;
  font-weight: 600;
  color: var(--border);
  text-align: center;
  line-height: 1;
}
.ckp-archetype.open .ckp-arch-num { color: var(--accent); }
.ckp-arch-title {
  font-family: var(--font-display);
  font-size: 1.05rem;
  font-weight: 700;
  color: #f0f0f0;
}
.ckp-arch-subtitle {
  font-family: var(--font-mono);
  font-size: 0.68rem;
  color: var(--text-muted);
  margin-top: 0.15rem;
  letter-spacing: 0.08em;
}
.ckp-arch-toggle {
  font-size: 0.9rem;
  color: var(--text-muted);
  transition: transform 0.25s;
}
.ckp-archetype.open .ckp-arch-toggle { transform: rotate(180deg); }

.ckp-arch-body {
  display: none;
  padding: 1.3rem 1.5rem 1.5rem;
  border-top: 1px solid var(--border);
  background: var(--bg);
}
.ckp-archetype.open .ckp-arch-body { display: block; }

.ckp-arch-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  margin-bottom: 1rem;
}
@media (max-width: 600px) { .ckp-arch-grid { grid-template-columns: 1fr; } }
.ckp-arch-cell {
  background: var(--surface);
  padding: 0.9rem 1rem;
  font-size: 0.83rem;
}
.ckp-arch-cell .cell-label {
  font-family: var(--font-mono);
  font-size: 0.62rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--text-muted);
  margin-bottom: 0.4rem;
}
.ckp-arch-cell p { margin: 0; line-height: 1.5; }

.ckp-decay-tag {
  display: inline-block;
  background: rgba(224,92,92,0.15);
  border: 1px solid rgba(224,92,92,0.35);
  color: var(--red);
  font-family: var(--font-mono);
  font-size: 0.7rem;
  padding: 0.25rem 0.7rem;
  margin-top: 0.8rem;
  letter-spacing: 0.06em;
}
.ckp-correct-tag {
  display: inline-block;
  background: rgba(109,207,148,0.1);
  border: 1px solid rgba(109,207,148,0.3);
  color: var(--green);
  font-family: var(--font-mono);
  font-size: 0.7rem;
  padding: 0.25rem 0.7rem;
  margin-top: 0.5rem;
  margin-left: 0.5rem;
  letter-spacing: 0.06em;
}

/* ─── Decay Laws ──────────────────────────────────────────────── */
.ckp-decay-laws { counter-reset: laws; margin: 2rem 0; }
.ckp-decay-law {
  display: grid;
  grid-template-columns: 52px 1fr;
  gap: 0;
  border-bottom: 1px solid var(--border);
  padding: 1.4rem 0;
  position: relative;
}
.ckp-decay-law:first-child { border-top: 1px solid var(--border); }
.ckp-law-num {
  font-family: var(--font-mono);
  font-size: 2rem;
  font-weight: 600;
  color: var(--surface2);
  line-height: 1;
  padding-top: 0.15rem;
}
.ckp-law-content h4 {
  font-family: var(--font-display);
  font-size: 1rem;
  font-weight: 700;
  color: #f0f0f0;
  margin: 0 0 0.4rem;
  text-transform: none;
  letter-spacing: normal;
}
.ckp-law-content p { margin: 0; font-size: 0.88rem; color: var(--text-muted); }

/* ─── Comparison table ─────────────────────────────────────────── */
.ckp-table-wrap {
  overflow-x: auto;
  margin: 2rem -0.5rem;
  -webkit-overflow-scrolling: touch;
}
.ckp-table {
  width: 100%;
  min-width: 620px;
  border-collapse: collapse;
  font-size: 0.82rem;
}
.ckp-table thead tr {
  background: var(--surface2);
}
.ckp-table th {
  font-family: var(--font-mono);
  font-size: 0.65rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--text-muted);
  padding: 0.8rem 1rem;
  text-align: left;
  border-bottom: 2px solid var(--accent);
  white-space: nowrap;
}
.ckp-table td {
  padding: 0.75rem 1rem;
  border-bottom: 1px solid var(--border);
  vertical-align: top;
  color: var(--text);
  line-height: 1.45;
}
.ckp-table tr:hover td { background: var(--surface); }
.ckp-table .nc-bad   { color: var(--red); font-family: var(--font-mono); font-size: 0.75rem; }
.ckp-table .nc-ok    { color: #e0c05c; font-family: var(--font-mono); font-size: 0.75rem; }
.ckp-table .nc-na    { color: var(--text-muted); font-family: var(--font-mono); font-size: 0.75rem; }
.ckp-table .arch-name { font-family: var(--font-display); font-weight: 700; color: #f0f0f0; }

/* ─── Diagnostic steps ─────────────────────────────────────────── */
.ckp-steps { counter-reset: steps; margin: 2rem 0; }
.ckp-step {
  display: grid;
  grid-template-columns: 44px 1fr;
  gap: 1rem;
  margin-bottom: 1.5rem;
  align-items: start;
}
.ckp-step-num {
  width: 44px; height: 44px;
  border: 2px solid var(--accent);
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-mono);
  font-weight: 600;
  font-size: 0.85rem;
  color: var(--accent);
  flex-shrink: 0;
  background: var(--accent-dim);
}
.ckp-step-content h4 {
  font-family: var(--font-display);
  font-size: 1rem;
  font-weight: 700;
  color: #f0f0f0;
  margin: 0.45rem 0 0.4rem;
  text-transform: none;
  letter-spacing: normal;
}
.ckp-step-content p { margin: 0; font-size: 0.88rem; color: var(--text-muted); }

/* ─── Definition box ───────────────────────────────────────────── */
.ckp-definition {
  background: var(--surface);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  padding: 1.3rem 1.6rem;
  margin: 2rem 0;
}
.ckp-def-label {
  font-family: var(--font-mono);
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 0.6rem;
}
.ckp-definition p {
  margin: 0;
  font-style: italic;
  font-size: 0.95rem;
  color: var(--text);
}

/* ─── Footnotes / References ───────────────────────────────────── */
.ckp-refs {
  margin-top: 3rem;
  padding-top: 1.5rem;
  border-top: 1px solid var(--border);
  font-size: 0.8rem;
  color: var(--text-muted);
  columns: 2;
  column-gap: 2rem;
}
@media (max-width: 700px) { .ckp-refs { columns: 1; } }
.ckp-refs h2 { columns: span 2; font-size: 1rem; margin-bottom: 1rem; }
.ckp-refs p { margin: 0 0 0.5rem; break-inside: avoid; line-height: 1.4; }
.ckp-refs .ref-num { color: var(--accent); font-family: var(--font-mono); font-size: 0.7rem; }

/* ─── Stats bar ────────────────────────────────────────────────── */
.ckp-stat-row {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
  gap: 1px;
  background: var(--border);
  border: 1px solid var(--border);
  margin: 2rem 0;
}
.ckp-stat {
  background: var(--surface);
  padding: 1.2rem 1.4rem;
  text-align: center;
}
.ckp-stat .stat-num {
  font-family: var(--font-display);
  font-size: 1.9rem;
  font-weight: 700;
  color: var(--accent);
  line-height: 1;
  display: block;
}
.ckp-stat .stat-label {
  font-family: var(--font-mono);
  font-size: 0.63rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--text-muted);
  margin-top: 0.35rem;
  display: block;
}

/* ─── Separator ─────────────────────────────────────────────────── */
.ckp-sep {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin: 3rem 0;
  color: var(--border);
  font-family: var(--font-mono);
  font-size: 0.7rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--text-muted);
}
.ckp-sep::before, .ckp-sep::after {
  content: '';
  flex: 1;
  height: 1px;
  background: var(--border);
}

/* ─── Mobile TOC toggle ─────────────────────────────────────────── */
.ckp-mobile-toc {
  display: none;
  background: var(--surface);
  border: 1px solid var(--border);
  padding: 0.8rem 1.2rem;
  margin-bottom: 1.5rem;
  cursor: pointer;
  font-family: var(--font-mono);
  font-size: 0.72rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--text-muted);
  justify-content: space-between;
  align-items: center;
}
.ckp-mobile-toc-list {
  display: none;
  background: var(--surface);
  border: 1px solid var(--border);
  border-top: none;
  padding: 1rem 1.2rem;
  margin-bottom: 1.5rem;
  margin-top: -2px;
}
.ckp-mobile-toc-list a {
  display: block;
  padding: 0.3rem 0;
  font-size: 0.85rem;
  color: var(--text-muted);
  text-decoration: none;
}
.ckp-mobile-toc-list a:hover { color: var(--accent); }
@media (max-width: 900px) {
  .ckp-mobile-toc { display: flex; }
}

/* ─── Animations ─────────────────────────────────────────────── */
@keyframes ckp-fade-in {
  from { opacity: 0; transform: translateY(16px); }
  to   { opacity: 1; transform: translateY(0); }
}
.ckp-hero { animation: ckp-fade-in 0.6s ease both; }
.ckp-abstract { animation: ckp-fade-in 0.6s ease 0.15s both; }
</style>

<div id="ckp-progress"></div>

<article class="ckp-article">

<!-- ═══════════════════ HERO ═══════════════════════════════════ -->
<div class="ckp-hero">
  <div class="ckp-kicker">Cyber Governance · Political Philosophy · Distributed Systems</div>
  <h1>Governing <em>Common Knowledge</em><br>Over Time</h1>
  <p class="ckp-deck">An ontological framework drawn from 2,500 years of political philosophy for long-term governance of shared-record systems — from blockchains to national registries.</p>
  <div class="ckp-meta">
    <span>PakCrypt Research</span>
    <span class="dot"></span>
    <span>April 2026</span>
    <span class="dot"></span>
    <span>~28 min read</span>
    <span class="dot"></span>
    <span><a href="/assets/phi/CKP7787932.pdf">PDF version ↗</a></span>
  </div>
</div>

<!-- Mobile TOC -->
<div class="ckp-mobile-toc" id="ckp-mob-toc-toggle">
  <span>Contents</span><span>▾</span>
</div>
<div class="ckp-mobile-toc-list" id="ckp-mob-toc-list">
  <a href="#abstract">Abstract</a>
  <a href="#introduction">Introduction</a>
  <a href="#ckp-definition">The Common-Knowledge Problem</a>
  <a href="#layered-model">The Layered Ontological Model</a>
  <a href="#archetypes">Eight Governance Archetypes</a>
  <a href="#decay-laws">Cross-Cutting Decay Laws</a>
  <a href="#synthesis">Synthesis & Diagnostic Method</a>
  <a href="#discussion">Discussion & Limitations</a>
  <a href="#conclusion">Conclusion</a>
  <a href="#references">References</a>
</div>

<!-- ═══════════════════ LAYOUT ════════════════════════════════ -->
<div class="ckp-layout">

<!-- ─── Main Body ─────────────────────────────────────────── -->
<div class="ckp-body">

<!-- ABSTRACT -->
<div class="ckp-abstract" id="abstract">
  <div class="ckp-abstract-label">Abstract</div>
  <p>We address a persistent, under-theorised problem at the intersection of distributed systems and governance: how to maintain trustworthy, tamper-evident shared state across parties who may not fully trust one another — not merely at deployment, but across the full lifecycle of a long-lived sociotechnical system. We call this the <em>Common-Knowledge Problem</em> (CKP) and argue that its core difficulty is not cryptographic but <em>political</em>. We propose a layered ontological model that decomposes any CKP system into five analytically separable strata, maps eight canonical governance archetypes drawn from Hobbes, Plato, Aristotle, Polybius, Rousseau, Weber, Michels, and Schmitt onto that stack, and derives eight cross-cutting decay laws alongside a six-step diagnostic procedure for practitioners.</p>
</div>

<!-- STATS BAR -->
<div class="ckp-stat-row">
  <div class="ckp-stat"><span class="stat-num">2,500</span><span class="stat-label">Years of political philosophy applied</span></div>
  <div class="ckp-stat"><span class="stat-num">8</span><span class="stat-label">Governance archetypes analysed</span></div>
  <div class="ckp-stat"><span class="stat-num">8</span><span class="stat-label">Cross-cutting decay laws derived</span></div>
  <div class="ckp-stat"><span class="stat-num">6</span><span class="stat-label">Step diagnostic procedure</span></div>
</div>

<!-- ─── SECTION 1: INTRODUCTION ──────────────────────────── -->
<section id="introduction">
<h2>Introduction</h2>

<p class="drop-cap">Every system designed to maintain a shared, authoritative record — from a national land registry to a public blockchain — faces a governance problem that outlasts its technical design. Cryptographic primitives, consensus protocols, and access-control policies can be specified and verified at deployment. What cannot be specified once and left unattended is the <em>political life</em> of the system: who controls the rules, how those controllers are selected and held accountable, and how the system evolves when its environment changes or when powerful actors seek to bend it to their advantage.</p>

<p>We term the underlying epistemic objective the <strong>Common-Knowledge Problem</strong> (CKP). Drawing on Aumann's formal definition of common knowledge and the Halpern–Moses impossibility result, we establish that no real system can deliver strict common knowledge. Every system instead delivers a <em>bounded approximation</em> — verifiable shared state with an explicit finality rule — and governance is the management of two gaps: between the approximation and the ideal, and between the stated finality rule and the actors who can override it.</p>

<p>Our central thesis is that this governance problem is structurally isomorphic to the problems analysed by the canonical tradition of political philosophy. Both domains confront rational, self-interested actors, asymmetric information, long time horizons, and the possibility that the authority responsible for maintaining the record is itself the most dangerous adversary. Political philosophy is therefore not an analogy for, but a <em>primary empirical source</em> about, how governance structures succeed, fail, and decay.</p>

<div class="ckp-callout">
  <strong>Four Principal Contributions</strong>
  <p><strong>1.</strong> A layered ontological model separating technical and political strata of a CKP system. <strong>2.</strong> Eight governance archetypes grounded in canonical primary sources, calibrated against documented historical cases. <strong>3.</strong> Eight cross-cutting decay laws that act on every archetype. <strong>4.</strong> A six-step applied diagnostic procedure translating the ontology into a practical selection and monitoring method.</p>
</div>

<p>We take care throughout to identify where the political-philosophy analogy leaks — where the structural differences between territorial polities and digital protocols invalidate a direct transfer — so that practitioners do not import the metaphor's <em>ceremony</em> in place of its <em>content</em>.</p>
</section>

<!-- ─── SECTION 2: CKP DEFINITION ────────────────────────── -->
<section id="ckp-definition">
<h2>The Common-Knowledge Problem: Definition &amp; Scope</h2>

<h3>Formal Grounding</h3>

<p>Aumann (1976) defines an event E as <em>common knowledge</em> among a set of agents N if every agent knows E, every agent knows that every other agent knows E, and so on ad infinitum. Halpern and Moses (1990) proved, via the Coordinated Attack problem, that this infinite epistemic tower is <em>unattainable</em> between agents communicating over an unreliable channel: no finite exchange of messages can produce common knowledge of coordination.</p>

<p>This impossibility is not a minor technical caveat; it is constitutive. Any system claiming to "solve" CKP is either restricting the reliability assumption (trusted channels), restricting the agent set (closed membership), or claiming less than strict common knowledge under a different name.</p>

<div class="ckp-definition">
  <div class="ckp-def-label">Definition — Common-Knowledge Problem (CKP)</div>
  <p>The Common-Knowledge Problem is the challenge of maintaining knowledge that would be knowable in principle — if authorised by policy and enabled by availability of communication — where both the authorisation gate and the communication channel are governed by whichever entity or rule-based protocol the participating community has chosen to trust.</p>
</div>

<p>This definition carries three analytically distinct components: the <strong>epistemic ceiling</strong> (what is reachable beneath the Halpern–Moses wall), the <strong>policy gate</strong> (authorisation — who controls what may be known), and the <strong>physical gate</strong> (communication availability — acknowledging eclipse attacks, network partitions, and denial-of-service).</p>

<h3>The Trustless Illusion</h3>

<div class="ckp-pull">
  <p>A common claim in the blockchain literature is that distributed ledgers solve CKP 'without trust.' This claim is technically false; the honest formulation is <em>trust-minimised</em>.</p>
  <cite>— On residual trust in distributed systems</cite>
</div>

<p>Residual trust always remains in: the hardness of the underlying cryptographic assumptions; the honesty of a majority of the validator or miner set; the correctness of client software that almost every participant uses without independent verification; and — most consequentially — the social layer that resolves disputes about which fork represents the "canonical" chain. Naming and governing each trust residual is the first act of CKP governance.</p>

<h3>The Legitimacy Principle</h3>

<p>We adopt a responsibility-grounded account of governance legitimacy rather than a normative-ideal account: <strong>whoever bears the responsibility and liability for a system holds the right to govern it</strong>. A corporation's owner governs the corporate ledger; a ministry answerable to a legislature governs a national registry.</p>

<p>This right is bounded by one structural fact: where a system's records bind parties who bear the consequences but did not delegate the governing authority and cannot exit, the owner's governing right and the affected parties' stake diverge. That divergence is the precise trigger condition for trust-minimisation; where it is absent, centralised authority is not merely acceptable but <em>optimal</em>.</p>
</section>

<!-- ─── SECTION 3: LAYERED MODEL ─────────────────────────── -->
<section id="layered-model">
<h2>The Layered Ontological Model</h2>

<p>A persistent error in cyber-governance discourse is the conflation of the <em>consensus mechanism</em> with the <em>governance structure</em>. A proof-of-work chain controlled by three mining pools and a centralised database controlled by a three-member committee are governed <em>identically</em> — by an oligarchy — despite opposite consensus mechanisms. To dissolve this conflation, we propose a five-layer model in which each stratum is analytically separable, with its own trust assumptions, failure modes, and relevant governance instruments.</p>

<div class="ckp-layers">
  <div class="ckp-layer">
    <div class="ckp-layer-badge">L0</div>
    <div class="ckp-layer-body">
      <strong>Substrate</strong>
      <p>The cryptographic primitives, hardware, and network fabric on which all higher layers depend. Trust residuals include computational hardness assumptions, hardware supply-chain integrity, and network reachability. Eclipse attacks and BGP hijacking operate here.</p>
    </div>
  </div>
  <div class="ckp-layer">
    <div class="ckp-layer-badge">L1</div>
    <div class="ckp-layer-body">
      <strong>Consensus</strong>
      <p>The protocol by which distributed replicas agree on the ordering and validity of state transitions: Nakamoto proof-of-work, proof-of-stake, BFT variants (PBFT, Tendermint), or the single-writer authority of a traditional database.</p>
    </div>
  </div>
  <div class="ckp-layer">
    <div class="ckp-layer-badge">L2</div>
    <div class="ckp-layer-body">
      <strong>Ledger / State</strong>
      <p>The shared, tamper-evident record itself: the sequence of committed blocks, the current world-state, and the finality rule. Who is allowed to declare a state <em>final</em> is a governance question masquerading as a technical one.</p>
    </div>
  </div>
  <div class="ckp-layer">
    <div class="ckp-layer-badge">L3</div>
    <div class="ckp-layer-body">
      <strong>Rule-Governance ★</strong>
      <p>The procedures by which the rules themselves are changed: upgrade paths, key-management policy, emergency-response authority, and the amendment process. <strong>This is the stratum at which political governance primarily operates.</strong> The upgrade key, the emergency multisig, and the pause function are instruments of L3 power.</p>
    </div>
  </div>
  <div class="ckp-layer">
    <div class="ckp-layer-badge">L4</div>
    <div class="ckp-layer-body">
      <strong>Social / Legitimacy</strong>
      <p>The human community — developers, validators, users, regulators, courts — whose collective interpretation determines which fork is "real." The Ethereum community's July 2016 decision to hard-fork after the DAO hack is a pure L4 act: no L1 mechanism changed; the social layer declared a new canonical chain.</p>
    </div>
  </div>
</div>

<div class="ckp-callout warn">
  <strong>Critical Structural Observation</strong>
  <p>Decentralisation at L1 provides <em>no protection</em> against capture at L3. A protocol can exhibit a Nakamoto coefficient of twenty at the consensus layer while its upgrade process is controlled by a single maintainer organisation. The political analysis must therefore target L3 and L4 primarily.</p>
</div>

<h3>The Sybil-Resistance Constraint</h3>

<p>Douceur (2002) proved that without a logically centralised authority, Sybil attacks are always possible except under extreme assumptions of resource parity. Without a proof-of-personhood mechanism, "weight by head" is not merely unwise — it is <em>unrepresentable</em>: the system can only weight by resource (stake or hashpower), and any nominal "democracy" collapses into a resource-weighted plutocracy. This is a feasibility-determining capability, not a normative constraint.</p>
</section>

<div class="ckp-sep">Eight Archetypes</div>

<!-- ─── SECTION 4: ARCHETYPES ─────────────────────────────── -->
<section id="archetypes">
<h2>Eight Governance Archetypes</h2>

<p>Each archetype is a canonical point in the design space of L3 governance, characterised by its principle of legitimacy, primary political-philosophy sources, at least one historical case, at least one modern digital-governance case, a characteristic decay vector, and conditions under which it constitutes a correct engineering choice.</p>

<div class="ckp-archetypes" id="ckp-arch-list">

  <!-- I. AUTOCRACY -->
  <div class="ckp-archetype" data-arch="1">
    <div class="ckp-arch-header">
      <div class="ckp-arch-num">I</div>
      <div>
        <div class="ckp-arch-title">Autocracy</div>
        <div class="ckp-arch-subtitle">Single will · Hobbes · Leviathan</div>
      </div>
      <div class="ckp-arch-toggle">▾</div>
    </div>
    <div class="ckp-arch-body">
      <p><strong>Principle of Legitimacy:</strong> A single will, vested by necessity or capacity, is the only guarantor of order; responsibility is total, so the governing right is total. Grounded in Hobbes's <em>Leviathan</em> (1651) — sovereignty is indivisible and the social covenant transfers all coercive power to the sovereign in exchange for peace.</p>
      <div class="ckp-arch-grid">
        <div class="ckp-arch-cell">
          <div class="cell-label">Historical Case</div>
          <p><strong>Stalinist record falsification.</strong> Stalin's photographic falsification programme airbrushed fallen officials — Yezhov, Trotsky, Kamenev — from official photographs. Subscribers to the <em>Great Soviet Encyclopaedia</em> were mailed instructions in 1954 to excise pages about Beria "with scissors or blade" and replace them with entries on the Bering Sea. This is not corruption — it is the structural implication of a model in which a single authority controls both the record and the record of the record.</p>
        </div>
        <div class="ckp-arch-cell">
          <div class="cell-label">Modern Digital Case</div>
          <p><strong>Single-key blockchain control.</strong> The Axie Infinity Ronin Bridge hack (March 2022) exploited a validator set of nine keys, four of which were controlled by a single organisation, reducing the effective threshold to control over those four keys. The structural failure is identical to Stalin's: a single authority controlled both the record and the mechanism of its revision.</p>
        </div>
      </div>
      <div class="ckp-decay-tag">⚠ Decay: Binary failure — functions until the principal becomes an adversary, then fails completely and irreversibly</div>
      <div class="ckp-correct-tag">✓ Correct when: principal is not in the threat model, records bind only consenting parties with cheap exit</div>
    </div>
  </div>

  <!-- II. TECHNOCRACY -->
  <div class="ckp-archetype" data-arch="2">
    <div class="ckp-arch-header">
      <div class="ckp-arch-num">II</div>
      <div>
        <div class="ckp-arch-title">Technocracy / Epistocracy</div>
        <div class="ckp-arch-subtitle">Expert knowledge · Plato · Republic</div>
      </div>
      <div class="ckp-arch-toggle">▾</div>
    </div>
    <div class="ckp-arch-body">
      <p><strong>Principle of Legitimacy:</strong> Knowledge confers the right to govern; those who understand the domain most deeply will make decisions of highest quality. Grounded in Plato's <em>Republic</em> — only those who have apprehended the Form of the Good are qualified to rule. This immediately faces the <em>selection problem</em>: to identify the wisest requires wisdom the selector may not possess.</p>
      <div class="ckp-arch-grid">
        <div class="ckp-arch-cell">
          <div class="cell-label">Historical Case</div>
          <p><strong>Chinese imperial examination (<em>keju</em>, c. 605–1905 CE).</strong> The longest-running technocratic experiment in recorded history. Decayed in two parallel processes: exam content ossified into the Eight-Legged Essay (<em>bagu wen</em>), measuring calligraphic conformity rather than administrative capacity; and differential access to tutors converted nominal meritocracy into hereditary advantage. Credential-capture problem: whoever controls the definition of "knowledge" controls who governs.</p>
        </div>
        <div class="ckp-arch-cell">
          <div class="cell-label">Modern Digital Case</div>
          <p><strong>Bitcoin Core maintainers &amp; Certificate Authorities.</strong> Bitcoin Core's governance is a technocracy of ~5 individuals with commit rights. The CA/Browser Forum: when monitoring of Certificate Transparency logs revealed Symantec had issued 100+ test certificates for domains it did not control, Google Chrome engineers unilaterally distrust Symantec over three years. DigiNotar was distrusted within 72 hours of the discovery of 500+ rogue certificates in 2011.</p>
        </div>
      </div>
      <div class="ckp-decay-tag">⚠ Decay: Credential capture, burnout-induced concentration, laundering of value judgements as technical facts</div>
      <div class="ckp-correct-tag">✓ Correct when: domain is genuinely technical, experts are accountable through a meta-mechanism, governed community has cheap exit</div>
    </div>
  </div>

  <!-- III. MERITOCRACY -->
  <div class="ckp-archetype" data-arch="3">
    <div class="ckp-arch-header">
      <div class="ckp-arch-num">III</div>
      <div>
        <div class="ckp-arch-title">Meritocracy</div>
        <div class="ckp-arch-subtitle">Measurable merit · Young · Hayek</div>
      </div>
      <div class="ckp-arch-toggle">▾</div>
    </div>
    <div class="ckp-arch-body">
      <p><strong>Principle of Legitimacy:</strong> Power allocated by demonstrated merit on a continuous, measurable scale — productivity, hashpower, stake, reputation. A critical note: Michael Young coined "meritocracy" in his 1958 satirical dystopia as a <em>pejorative</em>. The narrative ends in popular revolt against a hardened meritocratic elite. Hayek further distinguishes merit (deserved by effort) from market value (determined by scarcity), warning against conflating them.</p>
      <div class="ckp-arch-grid">
        <div class="ckp-arch-cell">
          <div class="cell-label">Historical Case</div>
          <p><strong>The Venetian <em>Serrata</em> (1297).</strong> The Great Council of Venice, initially meritocratic, became closed hereditary aristocracy in a single legislative act. Membership restricted to those whose patrilineal ancestors had served; formalised in the <em>Libro d'Oro</em> by 1323. Any merit criterion that is heritable, purchasable, or path-dependent calcifies into aristocracy within a predictable time horizon.</p>
        </div>
        <div class="ckp-arch-cell">
          <div class="cell-label">Modern Digital Case</div>
          <p><strong>Proof-of-work and proof-of-stake as proof of capital.</strong> "Merit" is operationally identical to capital expenditure. Larger pools extract more fees, reinvest more capital, attract more delegated stake — a compounding dynamic with no natural ceiling. The Nakamoto coefficient for Bitcoin mining as of May 2026: ≈2 (Foundry USA: 34.2% of global hashrate; AntPool: 14.2%). Venice took 30 years to close its books; proof-of-resource networks reach equivalent concentration in 18–36 months.</p>
        </div>
      </div>
      <div class="ckp-decay-tag">⚠ Decay: Merit that is purchasable and compounding will concentrate — decay into oligarchy is the equilibrium, not a corruption</div>
      <div class="ckp-correct-tag">✓ Correct when: merit is non-purchasable, regularly re-administered, and a redistribution mechanism prevents compounding</div>
    </div>
  </div>

  <!-- IV. OLIGARCHY -->
  <div class="ckp-archetype" data-arch="4">
    <div class="ckp-arch-header">
      <div class="ckp-arch-num">IV</div>
      <div>
        <div class="ckp-arch-title">Oligarchy / Plutocracy</div>
        <div class="ckp-arch-subtitle">Stake proportion · Aristotle · Michels</div>
      </div>
      <div class="ckp-arch-toggle">▾</div>
    </div>
    <div class="ckp-arch-body">
      <p><strong>Principle of Legitimacy:</strong> Governance rights proportional to stake. The honest claim: stake-weighted governance aligns incentives with outcomes. Aristotle's <em>Politics</em> defines oligarchy not by number but by <em>wealth</em>. Michels (1911): "Who says organisation, says oligarchy" — leaders acquire information advantages, organisational interest diverges from member interest, the leadership class becomes self-perpetuating. Winters (2011) modernises: oligarchy is compatible with any nominal regime type.</p>
      <div class="ckp-arch-grid">
        <div class="ckp-arch-cell">
          <div class="cell-label">Historical Case</div>
          <p><strong>The late Roman Republic (133–27 BCE).</strong> The <em>optimates</em> — the senatorial aristocracy — converted procedural norms (intercessio, tribunician veto, senatus consultum ultimum) into instruments of wealth defence. Gracchan reforms were blocked and reformers killed. The Republic ended not through popular revolution but through the oligarchy's own internecine conflict, requiring a military arbiter — the precise Polybian transition to tyranny from above.</p>
        </div>
        <div class="ckp-arch-cell">
          <div class="cell-label">Modern Digital Case</div>
          <p><strong>DAO governance concentration.</strong> The top ten addresses control 57.9% and 44.7% of voting power in Compound and Uniswap respectively; proposals achieve majority with an average of 2.84 participating addresses. Lido Finance (≈24.7% of staked ETH) plus Coinbase (≈12.2%) combined exceeds the 33% threshold at which a single coordinated actor can block finality in Ethereum's current consensus design.</p>
        </div>
      </div>
      <div class="ckp-decay-tag">⚠ Decay: Cartelisation — small group coordinates to extract rents — and the 51% attack as its technical analogue</div>
      <div class="ckp-correct-tag">✓ Correct only when: stakeholders are fully identified, stakes are non-transferable, liability is genuinely bound to governance power, exit is costly</div>
    </div>
  </div>

  <!-- V. DIRECT DEMOCRACY -->
  <div class="ckp-archetype" data-arch="5">
    <div class="ckp-arch-header">
      <div class="ckp-arch-num">V</div>
      <div>
        <div class="ckp-arch-title">Direct Democracy</div>
        <div class="ckp-arch-subtitle">Head count · Rousseau · Madison</div>
      </div>
      <div class="ckp-arch-toggle">▾</div>
    </div>
    <div class="ckp-arch-body">
      <p><strong>Principle of Legitimacy:</strong> Self-rule: each affected party has an equal say because all are equally subject to the outcome. Rousseau's <em>general will</em> is not the sum of preferences but the common interest each rational agent would identify under conditions of impartiality. Madison (Federalist No. 10) articulated the classical objection: "pure democracies have ever been spectacles of turbulence and contention."</p>
      <div class="ckp-arch-grid">
        <div class="ckp-arch-cell">
          <div class="cell-label">Historical Case</div>
          <p><strong>Athenian direct democracy (508–322 BCE).</strong> Demagogues (Cleon, Alcibiades) exploited assembly susceptibility to manipulation. Ostracism was weaponised as a factional tool. The Sicilian Expedition (415–413 BCE), endorsed by the assembly against cautious counsel, ended in catastrophic defeat. The six victorious generals after Arginusae were collectively tried and executed by mob vote — the epistemically most extreme form of majority tyranny. Athenian "democracy" covered perhaps 30,000–40,000 of a population of 250,000–300,000.</p>
        </div>
        <div class="ckp-arch-cell">
          <div class="cell-label">Modern Digital Case</div>
          <p><strong>The Sybil barrier and the 51% attack.</strong> One-entity-one-vote is impossible in a permissionless network without a centralised identity authority. The Ethereum Classic 51% attack (January 2019) rewrote 3,693 blocks and executed double-spends worth ~$1.1M. Majority rule and the 51% attack are the same act: the protocol <em>defines</em> the majority's decision as the valid chain. Uniswap governance routinely records turnout below 3% of token supply.</p>
        </div>
      </div>
      <div class="ckp-decay-tag">⚠ Decay: Arithmetically equivalent to plutocracy absent Sybil-resistance; demagoguery and minority-tyranny otherwise</div>
      <div class="ckp-correct-tag">✓ Correct only with: robust proof-of-personhood, bounded decision stakes, community small enough for genuine deliberation</div>
    </div>
  </div>

  <!-- VI. CONSTITUTIONAL REPUBLIC -->
  <div class="ckp-archetype" data-arch="6">
    <div class="ckp-arch-header">
      <div class="ckp-arch-num">VI</div>
      <div>
        <div class="ckp-arch-title">Constitutional Republic</div>
        <div class="ckp-arch-subtitle">Bounded rules · Polybius · Schmitt</div>
      </div>
      <div class="ckp-arch-toggle">▾</div>
    </div>
    <div class="ckp-arch-body">
      <p><strong>Principle of Legitimacy:</strong> Rules bind all parties symmetrically, including the rule-makers. Polybius attributes Rome's exceptional stability to its mixed constitution: consuls (monarchic), Senate (aristocratic), and popular assemblies (democratic) each constrain the others. The most penetrating source for the CKP context is Carl Schmitt's <em>Politische Theologie</em>: <em>"Souverän ist, wer über den Ausnahmezustand entscheidet"</em> — Sovereign is he who decides on the exception. Whoever can suspend the rules is the <em>de facto</em> sovereign.</p>
      <div class="ckp-arch-grid">
        <div class="ckp-arch-cell">
          <div class="cell-label">Historical Case</div>
          <p><strong>Weimar Germany and constitutional erosion.</strong> Article 48 granted emergency decree power. Between 1930 and 1933, government governed primarily by decree, normalising the exceptional until the constitutional frame was indistinguishable from the exception. Hitler's appointment was formally constitutional; the <em>Enabling Act</em> of March 1933 was passed by a parliament technically in session. The lesson: strength resides in the amendment process and emergency clause — those are the targets of any determined captor.</p>
        </div>
        <div class="ckp-arch-cell">
          <div class="cell-label">Modern Digital Case</div>
          <p><strong>The emergency multisig as hidden sovereign.</strong> DeFi protocols implement two-layer governance: slow on-chain token vote (the "legislature") and fast emergency multisig with pause/upgrade authority. Compound's Pause Guardian can disable markets without a vote; Aave's Guardian holds similar prerogatives. Per Schmitt's analysis, <em>these multisigs are the true sovereigns of the protocols</em>, regardless of the token-voting framing. Multiple bridge exploits (2022–2024) validated this architecturally.</p>
        </div>
      </div>
      <div class="ckp-decay-tag">⚠ Decay: Normalisation of the exception (Schmittian pathology) and capture of the amendment process</div>
      <div class="ckp-correct-tag">✓ Correct for: systems binding non-consenting parties at scale, multi-year to multi-decade intended lifespan, heterogeneous trust</div>
    </div>
  </div>

  <!-- VII. ANARCHY -->
  <div class="ckp-archetype" data-arch="7">
    <div class="ckp-arch-header">
      <div class="ckp-arch-num">VII</div>
      <div>
        <div class="ckp-arch-title">Anarchy / Code Is Law</div>
        <div class="ckp-arch-subtitle">Code alone · Lessig · May</div>
      </div>
      <div class="ckp-arch-toggle">▾</div>
    </div>
    <div class="ckp-arch-body">
      <p><strong>Principle of Legitimacy:</strong> The code is the only legitimate authority; whatever the protocol permits is legitimate; immutability is the supreme value. Important: Lessig introduced "code is law" as a <em>warning</em>, not an endorsement — that code is a form of regulation and should be subject to constitutional scrutiny. The cypherpunk appropriation inverts his meaning. Hobbes supplies the baseline: absent any sovereign, the state of nature degrades into "the war of all against all." Anarchy generates demand for a sovereign — that demand is the seed of the next autocracy.</p>
      <div class="ckp-arch-grid">
        <div class="ckp-arch-cell">
          <div class="cell-label">Historical Case</div>
          <p><strong>Icelandic Commonwealth (930–1262 CE).</strong> The most sustained historical experiment in institutional anarchy — private law enforcement, clan-based arbitration, no central executive. Functioned for ~300 years. Decay via the <em>Sturlung Era</em> of civil war (1220–1264), culminating in Norwegian annexation: concentrated private power achieved de facto governance while the formal constitution had no mechanism to check it. Anarchy produced an autocracy by the time the social cost was intolerable.</p>
        </div>
        <div class="ckp-arch-cell">
          <div class="cell-label">Modern Digital Case</div>
          <p><strong>The DAO hack and the Ethereum fork (2016).</strong> On 17 June 2016, an attacker drained 3.6M ETH (~$70M) via a valid execution of deployed bytecode — under "code is law," the funds belonged to the attacker. The Ethereum community executed a hard fork at block 1,920,000, stranding the attacker's gains. This is the definitive empirical refutation of code-as-governance: immutability is not a property of the code but a <em>social choice not to fork</em>. Ethereum Classic, which refused to fork, suffered three documented 51% attacks (2019–2020).</p>
        </div>
      </div>
      <div class="ckp-decay-tag">⚠ Decay: Not a stable equilibrium — generates demand for a sovereign that fills the governance vacuum</div>
      <div class="ckp-correct-tag">✓ Acceptable as the default layer (baseline absent social-layer intervention) but never as the only layer</div>
    </div>
  </div>

  <!-- VIII. BUREAUCRACY -->
  <div class="ckp-archetype" data-arch="8">
    <div class="ckp-arch-header">
      <div class="ckp-arch-num">VIII</div>
      <div>
        <div class="ckp-arch-title">Bureaucratic Administration</div>
        <div class="ckp-arch-subtitle">Rational-legal · Weber · Merton</div>
      </div>
      <div class="ckp-arch-toggle">▾</div>
    </div>
    <div class="ckp-arch-body">
      <p><strong>Principle of Legitimacy:</strong> Rational-legal authority: rules applied impersonally and predictably by technically trained officials selected on objective criteria. The office, not the person, holds the power. Weber identified bureaucracy as the most technically efficient form of organisation ever developed — virtues of precision, speed, formal equality, continuity — at the cost of what he called the <em>stahlhartes Gehäuse</em>: the iron cage of procedural rationality. Merton documented bureaucratic ritualism; Niskanen modelled budget-maximisation by information-controlling agents.</p>
      <div class="ckp-arch-grid">
        <div class="ckp-arch-cell">
          <div class="cell-label">Historical Case</div>
          <p><strong>Qing-dynasty bureaucracy in decline.</strong> The eight-legged essay format had become entirely self-referential: examining calligraphic conformity to a canonical style rather than practically applicable knowledge. The bureaucracy's response to the Taiping Rebellion, the Opium Wars, and industrialising neighbours was procedurally conformant and substantively incompetent — a precise instantiation of Merton's goal displacement.</p>
        </div>
        <div class="ckp-arch-cell">
          <div class="cell-label">Modern Digital Case</div>
          <p><strong>Change-advisory boards and the CrowdStrike incident (19 July 2024).</strong> A content-configuration update crashed ~8.5 million Windows endpoints globally. Pure Merton: a change-management process that satisfied procedural requirements while failing the substantive purpose. In blockchain governance, the pull-request merge authority of core developers and the key-signing authority of multisig holders are the bureaucratic sovereign — typically undocumented and unaccountable despite holding real power.</p>
        </div>
      </div>
      <div class="ckp-decay-tag">⚠ Decay: Goal displacement (procedure becomes the goal) and administrative capture (a shadow sovereign)</div>
      <div class="ckp-correct-tag">✓ Unavoidable in any production system — governance task is to bind it with transparency, rotation, and ex-ante constraints</div>
    </div>
  </div>

</div><!-- end archetypes -->
</section>

<div class="ckp-sep">Decay Laws</div>

<!-- ─── SECTION 5: DECAY LAWS ─────────────────────────────── -->
<section id="decay-laws">
<h2>Cross-Cutting Decay Laws</h2>

<p>The following eight laws act on all archetypes simultaneously. They constitute the dynamic machinery through which any governance form is deformed over time — not causes of failure in one particular system, but universal forces that any CKP governance design must instrument against.</p>

<div class="ckp-decay-laws">

  <div class="ckp-decay-law">
    <div class="ckp-law-num">01</div>
    <div class="ckp-law-content">
      <h4>Anacyclosis <span style="font-family:var(--font-mono);font-size:0.7rem;color:var(--text-muted);font-weight:400;">— Polybius, c. 140 BCE</span></h4>
      <p>A six-stage constitutional cycle: kingship → tyranny → aristocracy → oligarchy → democracy → mob rule → strongman → kingship. The cycle's engine: each good form contains within itself the incentive structure that produces its corrupt twin. No governance archetype is stable indefinitely, and the design task is to <em>instrument against your archetype's known decay</em>, not to find a form that does not decay.</p>
    </div>
  </div>

  <div class="ckp-decay-law">
    <div class="ckp-law-num">02</div>
    <div class="ckp-law-content">
      <h4>The Iron Law of Oligarchy <span style="font-family:var(--font-mono);font-size:0.7rem;color:var(--text-muted);font-weight:400;">— Michels, 1911</span></h4>
      <p>Every organisation, however democratic in charter, tends toward oligarchy through the structural logic of delegation. Leaders acquire information and skill advantages; the mass of members lacks the time, expertise, or incentive to exercise continuous oversight. The Nakamoto coefficient will tend downward; the maintainer set will tend to concentrate. Decentralisation is not a state one reaches — it is a force one must continuously exert against this attractor.</p>
    </div>
  </div>

  <div class="ckp-decay-law">
    <div class="ckp-law-num">03</div>
    <div class="ckp-law-content">
      <h4>The Principal-Agent Problem <span style="font-family:var(--font-mono);font-size:0.7rem;color:var(--text-muted);font-weight:400;">— Jensen &amp; Meckling, 1976 / Juvenal</span></h4>
      <p><em>Quis custodiet ipsos custodes</em> — who watches the watchmen? Every governance delegation creates an agent with private information and potentially divergent incentives. In CKP governance: every multisig signer, validator, and core developer is an agent with a private key. The security model of the protocol depends on their not defecting. Optimal governance design minimises agency costs through alignment of incentives (slashing, reputation) and monitoring (transparency, audits).</p>
    </div>
  </div>

  <div class="ckp-decay-law">
    <div class="ckp-law-num">04</div>
    <div class="ckp-law-content">
      <h4>Regulatory Capture <span style="font-family:var(--font-mono);font-size:0.7rem;color:var(--text-muted);font-weight:400;">— Stigler, 1971</span></h4>
      <p>Regulated industries systematically capture their regulators: regulated parties are concentrated, informed, and persistently motivated; the public interest is diffuse, uninformed, and episodically motivated. In CKP governance: entities most active in protocol governance are those with the most to gain — large token-holders, mining pools, infrastructure providers — and they consistently outparticipate the diffuse mass of ordinary users. The CA/Browser Forum before Certificate Transparency is a clean case.</p>
    </div>
  </div>

  <div class="ckp-decay-law">
    <div class="ckp-law-num">05</div>
    <div class="ckp-law-content">
      <h4>The State of Exception <span style="font-family:var(--font-mono);font-size:0.7rem;color:var(--text-muted);font-weight:400;">— Schmitt, 1922</span></h4>
      <p>No rule-system specifies its own emergency response completely — the space of possible emergencies is unbounded. The gap is filled by whoever is authorised — formally or informally — to decide that an emergency exists and to act outside normal procedure. In a CKP system, this is the pause guardian, the emergency multisig, and the "we will hard-fork if needed" capability. <strong>Identifying the holder of exception authority is the most important single diagnostic act in CKP governance.</strong></p>
    </div>
  </div>

  <div class="ckp-decay-law">
    <div class="ckp-law-num">06</div>
    <div class="ckp-law-content">
      <h4>The Sybil Constraint <span style="font-family:var(--font-mono);font-size:0.7rem;color:var(--text-muted);font-weight:400;">— Douceur, 2002</span></h4>
      <p>Sybil attacks are always possible in a permissionless setting absent a centralised identity authority. The feasible set of L3 governance forms is contingent on whether identity is solved. Without proof of personhood, any "democratic" governance reduces to resource-weighted plutocracy in the limit. Current proof-of-personhood mechanisms (Worldcoin, BrightID, Proof of Humanity) have achieved limited coverage at global scale and face genuine tensions between privacy and Sybil-resistance.</p>
    </div>
  </div>

  <div class="ckp-decay-law">
    <div class="ckp-law-num">07</div>
    <div class="ckp-law-content">
      <h4>Concentration Economics <span style="font-family:var(--font-mono);font-size:0.7rem;color:var(--text-muted);font-weight:400;">— Nakamoto Coefficient</span></h4>
      <p>Economies of scale in mining, staking, and protocol operations push relentlessly toward centralisation. Every measured proof-of-work and proof-of-stake network exhibits a Nakamoto coefficient that decreases monotonically after the initial growth phase unless explicit counter-measures are taken. Bitcoin mining (NC ≈ 2, May 2026) and Ethereum staking (NC ≈ 3–4) are below the threshold of meaningful decentralisation by any reasonable standard. These figures must be monitored continuously and used to trigger governance redesign when they cross operational thresholds.</p>
    </div>
  </div>

  <div class="ckp-decay-law">
    <div class="ckp-law-num">08</div>
    <div class="ckp-law-content">
      <h4>Exit, Voice, and Loyalty <span style="font-family:var(--font-mono);font-size:0.7rem;color:var(--text-muted);font-weight:400;">— Hirschman, 1970</span></h4>
      <p>Members of a declining organisation can exit (leave), voice (protest internally), or remain in loyalty. The most consequential structural novelty of blockchain governance relative to territorial politics: <em>exit is cheap</em>. Cheap exit reduces the incentive for voice (disgruntled minorities leave rather than fight) but powerfully checks tyranny (a majority that becomes too oppressive will simply be forked around). Ethereum Classic's survival after 2016 is the empirical test case. This is the single most important structural asymmetry between territorial and digital governance.</p>
    </div>
  </div>

</div><!-- end decay laws -->
</section>

<div class="ckp-sep">Synthesis</div>

<!-- ─── SECTION 6: SYNTHESIS ──────────────────────────────── -->
<section id="synthesis">
<h2>Synthesis &amp; Applied Diagnostic Method</h2>

<h3>Thesis, Antithesis, and Synthesis</h3>

<p><strong>Thesis.</strong> Political philosophy is the primary empirical source for CKP governance because the problem is constitutively about human power, incentive alignment, and the long-run dynamics of authority. The cryptography is solved engineering; the governance is not.</p>

<p><strong>Antithesis.</strong> The analogy leaks in four documented directions. First, the cheap-exit property of forking restructures the exit/voice balance in ways with no clean territorial analogue. Second, the governed "citizens" of a protocol are often pseudonymous capital units rather than persons. Third, code's literalism creates failure modes (the DAO reentrancy bug; the Parity multisig freeze) with no analog in legal interpretation. Fourth, the absence of a Weberian monopoly on legitimate violence means a protocol's "sovereign" holds power only over actors who choose to run the software.</p>

<div class="ckp-pull">
  <p>Political philosophy should be used as a catalogue of failure modes and decay vectors, not as a normative menu of desirable regime types. The engineering question is not "which archetype is ideal?" but "given my threat model, which archetype's predicted decay is least likely to destroy the CKP guarantee within my intended operational lifespan?"</p>
  <cite>— Central synthesis of the CKP governance framework</cite>
</div>

<h3>Archetype Summary Table</h3>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr>
    <th>Archetype</th>
    <th>Legitimacy Source</th>
    <th>Decay Vector</th>
    <th>Modern Analogue</th>
    <th>NC Threat</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><span class="arch-name">Autocracy</span></td>
    <td>Single will</td>
    <td>Record falsification</td>
    <td>Single-key bridge</td>
    <td><span class="nc-bad">NC = 1</span></td>
  </tr>
  <tr>
    <td><span class="arch-name">Technocracy</span></td>
    <td>Expert knowledge</td>
    <td>Credential capture</td>
    <td>Core developers</td>
    <td><span class="nc-ok">NC ≈ 5</span></td>
  </tr>
  <tr>
    <td><span class="arch-name">Meritocracy</span></td>
    <td>Measurable merit</td>
    <td>Capital compounding</td>
    <td>PoW / PoS pools</td>
    <td><span class="nc-bad">NC → 2</span></td>
  </tr>
  <tr>
    <td><span class="arch-name">Oligarchy</span></td>
    <td>Stake proportion</td>
    <td>Cartelisation</td>
    <td>DAO top 10</td>
    <td><span class="nc-bad">NC ≈ 2–3</span></td>
  </tr>
  <tr>
    <td><span class="arch-name">Direct Democracy</span></td>
    <td>Head count</td>
    <td>Sybil / apathy</td>
    <td>Token voting</td>
    <td><span class="nc-ok">NC = voters</span></td>
  </tr>
  <tr>
    <td><span class="arch-name">Constitutional Republic</span></td>
    <td>Bounded rules</td>
    <td>Exception capture</td>
    <td>Multisig guardian</td>
    <td><span class="nc-ok">NC varies</span></td>
  </tr>
  <tr>
    <td><span class="arch-name">Anarchy</span></td>
    <td>Code alone</td>
    <td>Social-layer override</td>
    <td>"Code is law"</td>
    <td><span class="nc-na">N/A</span></td>
  </tr>
  <tr>
    <td><span class="arch-name">Bureaucracy</span></td>
    <td>Rational-legal</td>
    <td>Goal displacement</td>
    <td>Ops / CAB</td>
    <td><span class="nc-bad">NC = ops team</span></td>
  </tr>
</tbody>
</table>
</div>

<h3>The Six-Step Diagnostic Procedure</h3>

<div class="ckp-steps">

  <div class="ckp-step">
    <div class="ckp-step-num">1</div>
    <div class="ckp-step-content">
      <h4>Specify the Threat Model</h4>
      <p>Enumerate adversary classes in priority order: rational profit-seekers (manageable through incentive alignment), coercive state-level adversaries (manageable only through geographic distribution), and the principal itself (resolvable only through trust-minimisation at L3 and L4). Every downstream governance choice is a function of this specification. Where the principal is not in the threat set and records bind only consenting parties, centralised administration with strong audit logging is the correct choice.</p>
    </div>
  </div>

  <div class="ckp-step">
    <div class="ckp-step-num">2</div>
    <div class="ckp-step-content">
      <h4>Name the Sovereign</h4>
      <p>Locate the fastest path by which the system's history could be altered against a participant's will. Ask: who holds the upgrade key; who controls the emergency multisig; who can merge a critical pull request; who can partition the network at L0? That entity is the true sovereign at L3, regardless of what the governance documentation asserts. Publish this analysis. If it cannot be published honestly, the system is an autocracy in fact.</p>
    </div>
  </div>

  <div class="ckp-step">
    <div class="ckp-step-num">3</div>
    <div class="ckp-step-content">
      <h4>Map to an Archetype</h4>
      <p>Locate the current governance structure in the typology using the <em>actual</em> distribution of L3 power, not the <em>stated</em> distribution. Most systems will be found to be in Archetype IV (Oligarchy) or Archetype I (Autocracy) in fact, regardless of their stated archetype.</p>
    </div>
  </div>

  <div class="ckp-step">
    <div class="ckp-step-num">4</div>
    <div class="ckp-step-content">
      <h4>Read the Decay Row</h4>
      <p>Take the characteristic decay vector of the identified archetype as a prior prediction about how the system will fail. Identify the leading indicators: for oligarchy, the Nakamoto coefficient trend; for technocracy, the size and insularity of the maintainer set; for constitutional republic, the use frequency of the emergency exception.</p>
    </div>
  </div>

  <div class="ckp-step">
    <div class="ckp-step-num">5</div>
    <div class="ckp-step-content">
      <h4>Instrument Against the Predicted Decay</h4>
      <p>Deploy monitoring and structural countermeasures calibrated to the predicted decay. For oligarchy: publish and alert on the Nakamoto/Gini coefficient for all L3 power dimensions. For the Schmittian exception: impose automatic expiry on emergency powers; require on-chain ratification within a bounded window. For concentration economics: impose stake caps or graduated voting-power curves. For the Sybil constraint: integrate a proof-of-personhood mechanism before claiming any head-weighted governance form.</p>
    </div>
  </div>

  <div class="ckp-step">
    <div class="ckp-step-num">6</div>
    <div class="ckp-step-content">
      <h4>Schedule Re-Diagnosis</h4>
      <p>Per anacyclosis, governance is not a state one reaches but a process of continuous decay that requires continuous counter-pressure. Schedule a full governance audit annually for fast-evolving protocols, every three years for slower-moving institutional systems. Define triggering thresholds — Nakamoto coefficient below k, emergency power invoked more than n times per period, maintainer set reduced below m organisations — that force an unscheduled re-diagnosis.</p>
    </div>
  </div>

</div>
</section>

<!-- ─── SECTION 7: DISCUSSION ─────────────────────────────── -->
<section id="discussion">
<h2>Discussion: Limitations &amp; Open Problems</h2>

<h3>The Limits of the Analogy</h3>

<p>The cheap-exit asymmetry is the most dangerous gap: political intuitions about the futility or violence of secession systematically overestimate the cost of exit from a protocol, leading practitioners to over-invest in governance mechanisms appropriate for captive populations but unnecessary when users can fork. We recommend that practitioners explicitly budget for fork scenarios when evaluating governance investment — a practice with no equivalent in territorial political design.</p>

<h3>Identity as the Unsolved Foundation</h3>

<div class="ckp-callout key">
  <strong>The Open Problem</strong>
  <p>The Sybil constraint establishes that the entire space of head-weighted governance forms is contingent on solving identity. Current proof-of-personhood mechanisms have achieved limited coverage at global scale and face genuine tensions between privacy and Sybil-resistance. Until identity is solved at scale, practitioners face a choice between plutocracy (resource-weighted) and autocracy/technocracy (trust-based selection). This is not a failure of governance design — it is a constraint imposed by mathematics.</p>
</div>

<h3>The Temporal Problem</h3>

<p>A system designed optimally for its initial threat model will be suboptimal as the threat model evolves. Quantum computing threatens L0 cryptographic assumptions and will require protocol-level migration at a scale with no historical precedent. Regulatory environments shift governance feasibility across jurisdictions. The correct response is not to over-engineer for imagined future threats but to ensure that the amendment process itself remains healthy: a constitutional republic whose amendment process is captured is worse than an honest autocracy with a succession plan.</p>

<h3>Measurement and the Nakamoto Coefficient</h3>

<p>The Nakamoto coefficient is an imperfect instrument: pool membership is volatile, concentration figures vary across trackers and measurement windows, and the coefficient measures enumerable entities but not collusion probability. We recommend complementing it with incentive-alignment measures: what fraction of validator revenue would be at risk in a detected collusion event; what is the geographic and jurisdictional distribution of signers; what is the market-cap fraction held by the top ten addresses. No single metric suffices; governance health is multi-dimensional.</p>
</section>

<!-- ─── SECTION 8: CONCLUSION ─────────────────────────────── -->
<section id="conclusion">
<h2>Conclusion</h2>

<p>The framework proposed here yields three actionable conclusions.</p>

<p><strong>First,</strong> the selection of a governance archetype is an engineering decision against a threat model, not a normative aspiration. The correct archetype is the one whose predicted decay is least likely to destroy the CKP guarantee within the intended operational lifespan, given the specific adversary classes in the threat model.</p>

<p><strong>Second,</strong> the true sovereign of any CKP system is not the entity named in the governance documentation but the entity identified by the "Find the Sovereign" diagnostic: whoever can alter the record fastest against a participant's will. That entity must be named, published, constrained, and periodically rotated.</p>

<p><strong>Third,</strong> governance is not a state one reaches — it is a continuous counter-pressure against the decay forces described above. Designing a governance structure and not re-diagnosing it is equivalent to writing a security policy and not auditing it: the threat model will have moved before the policy is deployed.</p>

<div class="ckp-pull">
  <p>The right to fork — cheap exit — is the structural novelty that digital governance contributes to the tradition of political thought. It is both the most powerful anti-tyranny mechanism available and the reason that the Polybian cycle in digital systems does not run to completion.</p>
  <cite>— On the unique property of digital governance</cite>
</div>

<p>The open problems remain: the identity problem, the interaction between regulatory law and protocol governance, and the dynamics of multi-chain and cross-chain governance. What the present framework provides is a disciplined starting point: eight archetypes, eight decay laws, and a six-step procedure that converts 2,500 years of hard-won political wisdom into an engineering checklist.</p>
</section>

<!-- ─── REFERENCES ─────────────────────────────────────────── -->
<div class="ckp-refs" id="references">
<h2>References</h2>
<p><span class="ref-num">[1]</span> Aumann, R.J.: Agreeing to disagree. <em>The Annals of Statistics</em> 4(6), 1236–1239 (1976)</p>
<p><span class="ref-num">[2]</span> Halpern, J.Y., Moses, Y.: Knowledge and common knowledge in a distributed environment. <em>Journal of the ACM</em> 37(3), 549–587 (1990)</p>
<p><span class="ref-num">[3]</span> Hobbes, T.: <em>Leviathan</em>. Andrew Crooke, London (1651)</p>
<p><span class="ref-num">[4]</span> Plato: <em>The Republic</em>, c. 375 BCE</p>
<p><span class="ref-num">[5]</span> Aristotle: <em>Politics</em>, c. 350 BCE</p>
<p><span class="ref-num">[6]</span> Polybius: <em>The Histories</em>, Book VI, c. 140 BCE</p>
<p><span class="ref-num">[7]</span> Rousseau, J.-J.: <em>Du Contrat Social</em>. Amsterdam (1762)</p>
<p><span class="ref-num">[8]</span> Montesquieu, C.: <em>De l'esprit des lois</em>. Geneva (1748)</p>
<p><span class="ref-num">[9]</span> Madison, J.: Federalist No. 10 &amp; No. 51. In: <em>The Federalist Papers</em> (1788)</p>
<p><span class="ref-num">[10]</span> Schmitt, C.: <em>Politische Theologie</em>. Duncker &amp; Humblot (1922)</p>
<p><span class="ref-num">[11]</span> Weber, M.: <em>Economy and Society</em> [Wirtschaft und Gesellschaft]. Mohr (1922)</p>
<p><span class="ref-num">[12]</span> Michels, R.: <em>Political Parties</em>. Klinkhardt (1911)</p>
<p><span class="ref-num">[13]</span> Merton, R.K.: Bureaucratic structure and personality. <em>Social Forces</em> 18(4) (1940)</p>
<p><span class="ref-num">[14]</span> Young, M.: <em>The Rise of the Meritocracy</em>. Thames &amp; Hudson (1958)</p>
<p><span class="ref-num">[15]</span> Hayek, F.A.: <em>The Constitution of Liberty</em>. U. of Chicago Press (1960)</p>
<p><span class="ref-num">[16]</span> Winters, J.A.: <em>Oligarchy</em>. Cambridge U. Press (2011)</p>
<p><span class="ref-num">[17]</span> Jensen, M.C., Meckling, W.H.: Theory of the firm. <em>J. Financial Economics</em> 3(4) (1976)</p>
<p><span class="ref-num">[18]</span> Stigler, G.J.: The theory of economic regulation. <em>Bell Journal of Economics</em> 2(1) (1971)</p>
<p><span class="ref-num">[19]</span> Hirschman, A.O.: <em>Exit, Voice, and Loyalty</em>. Harvard U. Press (1970)</p>
<p><span class="ref-num">[20]</span> Douceur, J.R.: The Sybil attack. In: <em>Peer-to-Peer Systems</em>. LNCS vol. 2429 (2002)</p>
<p><span class="ref-num">[21]</span> Srinivasan, B.S., Lee, L.: Quantifying decentralization. Earn.com (2017)</p>
<p><span class="ref-num">[22]</span> Messias, J. et al.: Understanding blockchain governance. arXiv:2305.17655 (2023)</p>
<p><span class="ref-num">[23]</span> De Filippi, P., Wright, A.: <em>Blockchain and the Law</em>. Harvard U. Press (2018)</p>
<p><span class="ref-num">[24]</span> Mehar, M.I. et al.: Understanding the DAO attack. <em>J. Cases on IT</em> 21(1) (2019)</p>
<p><span class="ref-num">[25]</span> King, D.: <em>The Commissar Vanishes</em>. Henry Holt (1997)</p>
<p><span class="ref-num">[26]</span> Lane, F.C.: <em>Venice: A Maritime Republic</em>. Johns Hopkins U. Press (1973)</p>
<p><span class="ref-num">[27]</span> CoinDesk: Bitcoin mining pools, 75% hashrate. CoinDesk (11 May 2026)</p>
<p><span class="ref-num">[28]</span> Lido Finance: Tokenholder Update Q3 2025. blog.lido.fi (2025)</p>
<p><span class="ref-num">[29]</span> SSLMate: Timeline of Certificate Authority Failures. sslmate.com</p>
<p><span class="ref-num">[30]</span> Microsoft: Helping customers through the CrowdStrike outage (20 July 2024)</p>
<p><span class="ref-num">[31]</span> Lessig, L.: <em>Code and Other Laws of Cyberspace</em>. Basic Books (1999)</p>
<p><span class="ref-num">[32]</span> Zargham, M. et al.: State-space modeling of blockchain-enabled economic systems. IEEE CDC (2019)</p>
</div>

</div><!-- end .ckp-body -->

<!-- ─── Sidebar TOC ─────────────────────────────────────────── -->
<aside class="ckp-sidebar">
  <div class="ckp-toc-label">Contents</div>
  <ul class="ckp-toc-list" id="ckp-toc">
    <li data-section="abstract"><a href="#abstract">Abstract</a></li>
    <li data-section="introduction"><a href="#introduction">Introduction</a></li>
    <li data-section="ckp-definition"><a href="#ckp-definition">The CKP Defined</a></li>
    <li class="toc-sub" data-section="ckp-definition"><a href="#ckp-definition">Formal Grounding</a></li>
    <li class="toc-sub" data-section="ckp-definition"><a href="#ckp-definition">Trustless Illusion</a></li>
    <li data-section="layered-model"><a href="#layered-model">Layered Model</a></li>
    <li data-section="archetypes"><a href="#archetypes">Eight Archetypes</a></li>
    <li class="toc-sub" data-section="archetypes"><a href="#archetypes">I. Autocracy</a></li>
    <li class="toc-sub" data-section="archetypes"><a href="#archetypes">II. Technocracy</a></li>
    <li class="toc-sub" data-section="archetypes"><a href="#archetypes">III. Meritocracy</a></li>
    <li class="toc-sub" data-section="archetypes"><a href="#archetypes">IV. Oligarchy</a></li>
    <li class="toc-sub" data-section="archetypes"><a href="#archetypes">V. Democracy</a></li>
    <li class="toc-sub" data-section="archetypes"><a href="#archetypes">VI. Constitutional</a></li>
    <li class="toc-sub" data-section="archetypes"><a href="#archetypes">VII. Anarchy</a></li>
    <li class="toc-sub" data-section="archetypes"><a href="#archetypes">VIII. Bureaucracy</a></li>
    <li data-section="decay-laws"><a href="#decay-laws">Decay Laws</a></li>
    <li data-section="synthesis"><a href="#synthesis">Synthesis & Method</a></li>
    <li data-section="discussion"><a href="#discussion">Discussion</a></li>
    <li data-section="conclusion"><a href="#conclusion">Conclusion</a></li>
    <li data-section="references"><a href="#references">References</a></li>
  </ul>
</aside>

</div><!-- end .ckp-layout -->

</article>

<script>
(function() {
  /* ── Progress bar ── */
  var bar = document.getElementById('ckp-progress');
  function updateProgress() {
    var scrolled = window.scrollY || window.pageYOffset;
    var total = document.documentElement.scrollHeight - window.innerHeight;
    bar.style.width = total > 0 ? (scrolled / total * 100) + '%' : '0%';
  }
  window.addEventListener('scroll', updateProgress, { passive: true });
  updateProgress();

  /* ── TOC active state ── */
  var sections = ['abstract','introduction','ckp-definition','layered-model','archetypes','decay-laws','synthesis','discussion','conclusion','references'];
  var tocItems = document.querySelectorAll('#ckp-toc li[data-section]');
  function updateTOC() {
    var current = '';
    sections.forEach(function(id) {
      var el = document.getElementById(id);
      if (el) {
        var rect = el.getBoundingClientRect();
        if (rect.top <= 120) current = id;
      }
    });
    tocItems.forEach(function(li) {
      li.classList.toggle('active', li.dataset.section === current);
    });
  }
  window.addEventListener('scroll', updateTOC, { passive: true });
  updateTOC();

  /* ── Archetype accordion ── */
  document.querySelectorAll('.ckp-arch-header').forEach(function(hdr) {
    hdr.addEventListener('click', function() {
      var arch = this.closest('.ckp-archetype');
      var wasOpen = arch.classList.contains('open');
      document.querySelectorAll('.ckp-archetype.open').forEach(function(a) { a.classList.remove('open'); });
      if (!wasOpen) arch.classList.add('open');
    });
  });

  /* ── Mobile TOC toggle ── */
  var mobToggle = document.getElementById('ckp-mob-toc-toggle');
  var mobList   = document.getElementById('ckp-mob-toc-list');
  if (mobToggle && mobList) {
    mobToggle.addEventListener('click', function() {
      var open = mobList.style.display === 'block';
      mobList.style.display = open ? 'none' : 'block';
      mobToggle.querySelector('span:last-child').textContent = open ? '▾' : '▴';
    });
    mobList.querySelectorAll('a').forEach(function(a) {
      a.addEventListener('click', function() {
        mobList.style.display = 'none';
        mobToggle.querySelector('span:last-child').textContent = '▾';
      });
    });
  }

  /* ── Smooth scroll ── */
  document.querySelectorAll('.ckp-toc-list a, .ckp-mobile-toc-list a').forEach(function(a) {
    a.addEventListener('click', function(e) {
      var id = this.getAttribute('href').slice(1);
      var target = document.getElementById(id);
      if (target) {
        e.preventDefault();
        target.scrollIntoView({ behavior: 'smooth', block: 'start' });
      }
    });
  });
})();
</script>