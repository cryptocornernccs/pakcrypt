---
layout: post
title: "Bought, Not Hacked"
---

<style>
/* ─── Google Fonts ─────────────────────────────────────────────── */
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;0,700;0,900;1,400;1,700&family=Source+Serif+4:ital,opsz,wght@0,8..60,300;0,8..60,400;0,8..60,600;1,8..60,300;1,8..60,400&family=JetBrains+Mono:wght@400;600&display=swap');

/* ─── Design tokens ────────────────────────────────────────────────
   Scoped to .ckp-article so the article never overwrites site-wide
   theme variables. Progress bar + back-to-top carry literal colours.
   ──────────────────────────────────────────────────────────────── */
.ckp-article {
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
  --amber:        #e0935c;
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
  background: linear-gradient(90deg, #c9a84c, #e8c96a);
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
.ckp-hero h1 em { font-style: italic; color: var(--accent); }
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
.ckp-toc-list { list-style: none; padding: 0; margin: 0; }
.ckp-toc-list li {
  margin: 0;
  border-left: 2px solid transparent;
  transition: border-color 0.2s;
}
.ckp-toc-list li.active { border-color: var(--accent); }
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
.ckp-body a { color: var(--accent); text-decoration: none; border-bottom: 1px solid rgba(201,168,76,0.3); }
.ckp-body a:hover { border-bottom-color: var(--accent); }

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
.ckp-abstract p { margin: 0 0 0.9rem; color: var(--text-muted); font-style: italic; }
.ckp-abstract p:last-child { margin-bottom: 0; }

/* ─── Callout boxes ─────────────────────────────────────────────── */
.ckp-callout {
  background: var(--surface);
  border: 1px solid var(--border);
  border-left: 3px solid var(--blue);
  padding: 1.2rem 1.5rem;
  margin: 2rem 0;
  font-size: 0.92rem;
}
.ckp-callout.warn { border-left-color: var(--amber); }
.ckp-callout.key  { border-left-color: var(--green); }
.ckp-callout.bad  { border-left-color: var(--red); }
.ckp-callout p:last-child { margin-bottom: 0; }
.ckp-callout strong:first-child {
  font-family: var(--font-mono);
  font-size: 0.68rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--blue);
  display: block;
  margin-bottom: 0.5rem;
}
.ckp-callout.warn strong:first-child { color: var(--amber); }
.ckp-callout.key  strong:first-child { color: var(--green); }
.ckp-callout.bad  strong:first-child { color: var(--red); }

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
.ckp-definition p { margin: 0; font-style: italic; font-size: 0.95rem; color: var(--text); }

/* ─── Hierarchy list ────────────────────────────────────────────── */
.ckp-hier { margin: 1.5rem 0; padding: 0; list-style: none; }
.ckp-hier li {
  display: flex;
  gap: 1rem;
  align-items: flex-start;
  padding: 0.75rem 1rem;
  border-bottom: 1px solid var(--border);
  font-size: 0.92rem;
}
.ckp-hier li:first-child { border-top: 1px solid var(--border); }
.ckp-hier li::before {
  content: '▸';
  color: var(--accent);
  font-size: 0.75rem;
  margin-top: 0.3rem;
  flex-shrink: 0;
}

/* ─── Stats bar ────────────────────────────────────────────────── */
.ckp-stat-row {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
  gap: 1px;
  background: var(--border);
  border: 1px solid var(--border);
  margin: 2rem 0;
}
.ckp-stat { background: var(--surface); padding: 1.2rem 1.4rem; text-align: center; }
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
  line-height: 1.4;
}

/* ─── Chain / Ordered steps ─────────────────────────────────────── */
.ckp-chain { counter-reset: chain; margin: 2rem 0; }
.ckp-chain-item {
  display: grid;
  grid-template-columns: 44px 1fr;
  gap: 1rem;
  margin-bottom: 1.5rem;
  align-items: start;
}
.ckp-chain-num {
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
.ckp-chain-content h4 {
  font-family: var(--font-display);
  font-size: 1rem;
  font-weight: 700;
  color: #f0f0f0;
  margin: 0.45rem 0 0.4rem;
  text-transform: none;
  letter-spacing: normal;
}
.ckp-chain-content p { margin: 0; font-size: 0.88rem; color: var(--text-muted); }

/* ─── Tables ──────────────────────────────────────────────────── */
.ckp-table-wrap {
  overflow-x: auto;
  margin: 2rem -0.5rem;
  -webkit-overflow-scrolling: touch;
}
.ckp-table {
  width: 100%;
  min-width: 560px;
  border-collapse: collapse;
  font-size: 0.82rem;
}
.ckp-table thead tr { background: var(--surface2); }
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
.ckp-table .term { font-family: var(--font-display); font-weight: 700; color: #f0f0f0; }
.ckp-table code {
  font-family: var(--font-mono);
  font-size: 0.9em;
  color: var(--blue);
  background: none;
  padding: 0;
}
/* group rows inside long tables */
.ckp-table tr.group td {
  background: var(--surface2);
  font-family: var(--font-mono);
  font-size: 0.66rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--accent);
  padding: 0.6rem 1rem;
  border-bottom: 1px solid var(--accent);
}
.ckp-table tr.group:hover td { background: var(--surface2); }

/* ─── NEW: status pills ───────────────────────────────────────── */
.ckp-pill {
  font-family: var(--font-mono);
  font-size: 0.6rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  padding: 0.18rem 0.5rem;
  border: 1px solid;
  white-space: nowrap;
  display: inline-block;
  line-height: 1.4;
}
.ckp-pill.ok      { color: var(--green); border-color: rgba(109,207,148,0.45); background: rgba(109,207,148,0.08); }
.ckp-pill.partial { color: var(--amber); border-color: rgba(224,147,92,0.45);  background: rgba(224,147,92,0.08); }
.ckp-pill.no      { color: var(--red);   border-color: rgba(224,92,92,0.45);   background: rgba(224,92,92,0.08); }
.ckp-pill.info    { color: var(--blue);  border-color: rgba(107,181,214,0.45); background: rgba(107,181,214,0.08); }

/* ─── NEW: monospace diagram / code block ─────────────────────── */
.ckp-diagram {
  margin: 2rem 0;
  background: var(--surface);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  position: relative;
}
.ckp-diagram-head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  padding: 0.6rem 1rem;
  border-bottom: 1px solid var(--border);
  background: var(--surface2);
}
.ckp-diagram-label {
  font-family: var(--font-mono);
  font-size: 0.62rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--text-muted);
}
.ckp-copy {
  font-family: var(--font-mono);
  font-size: 0.6rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--text-muted);
  background: none;
  border: 1px solid var(--border);
  padding: 0.2rem 0.55rem;
  cursor: pointer;
  transition: color 0.2s, border-color 0.2s;
}
.ckp-copy:hover { color: var(--accent); border-color: var(--accent); }
.ckp-diagram pre {
  margin: 0;
  padding: 1.1rem 1.2rem;
  line-height: 1.28;
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
  background: none;
  border: none;
}
.ckp-diagram code {
  font-family: var(--font-mono);
  font-size: 0.72rem;
  line-height: 1.25;
  color: var(--text);
  white-space: pre;
  background: none;
  padding: 0;
}
@media (max-width: 600px) { .ckp-diagram code { font-size: 0.62rem; } }

/* inline code in prose */
.ckp-body p code, .ckp-body li code, .ckp-callout code {
  font-family: var(--font-mono);
  font-size: 0.86em;
  color: var(--blue);
  background: var(--surface2);
  padding: 0.08em 0.35em;
  border: 1px solid var(--border);
}

/* ─── NEW: findings grid ──────────────────────────────────────── */
.ckp-findings {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
  margin: 2rem 0;
}
.ckp-finding {
  background: var(--surface);
  border: 1px solid var(--border);
  border-top: 2px solid var(--accent);
  padding: 1.1rem 1.3rem;
  transition: background 0.2s, border-color 0.2s;
}
.ckp-finding:hover { background: var(--surface2); }
.ckp-finding .f-id {
  font-family: var(--font-mono);
  font-size: 0.62rem;
  letter-spacing: 0.14em;
  color: var(--accent);
  display: block;
  margin-bottom: 0.45rem;
}
.ckp-finding h4 {
  font-family: var(--font-display);
  font-size: 0.98rem;
  font-weight: 700;
  color: #f0f0f0;
  margin: 0 0 0.4rem;
  text-transform: none;
  letter-spacing: normal;
  line-height: 1.3;
}
.ckp-finding p { margin: 0; font-size: 0.82rem; color: var(--text-muted); line-height: 1.55; }

/* ─── NEW: claim vs claim ─────────────────────────────────────── */
.ckp-versus { margin: 2rem 0; border: 1px solid var(--border); }
.ckp-versus-head {
  display: grid;
  grid-template-columns: 1fr 1fr;
  background: var(--surface2);
  border-bottom: 2px solid var(--accent);
}
.ckp-versus-head div {
  padding: 0.7rem 1.1rem;
  font-family: var(--font-mono);
  font-size: 0.63rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
}
.ckp-versus-head .vs-bad  { color: var(--red); }
.ckp-versus-head .vs-good { color: var(--green); border-left: 1px solid var(--border); }
.ckp-versus-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  border-bottom: 1px solid var(--border);
  font-size: 0.85rem;
}
.ckp-versus-row:last-child { border-bottom: none; }
.ckp-versus-row > div { padding: 0.9rem 1.1rem; line-height: 1.5; }
.ckp-versus-row .vs-good { border-left: 1px solid var(--border); background: var(--surface); }
.ckp-versus-row .vs-bad  { color: var(--text-muted); font-style: italic; }
@media (max-width: 640px) {
  .ckp-versus-head { display: none; }
  .ckp-versus-row { grid-template-columns: 1fr; }
  .ckp-versus-row .vs-good { border-left: none; border-top: 1px solid var(--border); }
  .ckp-versus-row .vs-bad::before {
    content: 'Do not claim';
    display: block;
    font-family: var(--font-mono);
    font-size: 0.58rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--red);
    margin-bottom: 0.3rem;
    font-style: normal;
  }
  .ckp-versus-row .vs-good::before {
    content: 'Claim instead';
    display: block;
    font-family: var(--font-mono);
    font-size: 0.58rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--green);
    margin-bottom: 0.3rem;
  }
}

/* ─── Separator ─────────────────────────────────────────────────── */
.ckp-sep {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin: 3rem 0;
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

/* ─── References ────────────────────────────────────────────────── */
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
.ckp-refs h2 { column-span: all; font-size: 1rem; margin-bottom: 1rem; }
.ckp-refs p { margin: 0 0 0.6rem; break-inside: avoid; line-height: 1.45; }
.ckp-refs .ref-num { color: var(--accent); font-family: var(--font-mono); font-size: 0.7rem; }
.ckp-refs a { color: var(--text-muted); border-bottom: 1px dotted var(--border); text-decoration: none; word-break: break-word; }
.ckp-refs a:hover { color: var(--accent); }
.ckp-refs .v-tag {
  font-family: var(--font-mono);
  font-size: 0.55rem;
  letter-spacing: 0.08em;
  border: 1px solid var(--border);
  padding: 0.05rem 0.3rem;
  margin-right: 0.3rem;
}
.ckp-refs .v-tag.v { color: var(--green); }
.ckp-refs .v-tag.s { color: var(--blue); }
.ckp-refs .v-tag.r { color: var(--amber); }

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
@media (max-width: 900px) { .ckp-mobile-toc { display: flex; } }

/* ─── NEW: back to top ────────────────────────────────────────── */
#ckp-top {
  position: fixed;
  right: 1.4rem; bottom: 1.4rem;
  width: 40px; height: 40px;
  border: 1px solid #383840;
  background: #242428;
  color: #c9a84c;
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.9rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.25s, border-color 0.2s;
  z-index: 9998;
}
#ckp-top.show { opacity: 1; pointer-events: auto; }
#ckp-top:hover { border-color: #c9a84c; }

/* ─── Keywords strip ────────────────────────────────────────────── */
.ckp-keywords { display: flex; flex-wrap: wrap; gap: 0.5rem; margin: 1.5rem 0 2rem; }
.ckp-kw {
  font-family: var(--font-mono);
  font-size: 0.68rem;
  letter-spacing: 0.08em;
  background: var(--surface2);
  border: 1px solid var(--border);
  color: var(--text-muted);
  padding: 0.25rem 0.7rem;
}

/* ─── Animations ─────────────────────────────────────────────── */
@keyframes ckp-fade-in {
  from { opacity: 0; transform: translateY(16px); }
  to   { opacity: 1; transform: translateY(0); }
}
.ckp-hero     { animation: ckp-fade-in 0.6s ease both; }
.ckp-abstract { animation: ckp-fade-in 0.6s ease 0.15s both; }
@media (prefers-reduced-motion: reduce) {
  .ckp-hero, .ckp-abstract { animation: none; }
  #ckp-progress { transition: none; }
}

/* ─── NEW: print stylesheet ───────────────────────────────────── */
@media print {
  #ckp-progress, #ckp-top, .ckp-sidebar, .ckp-mobile-toc,
  .ckp-mobile-toc-list, .ckp-copy { display: none !important; }
  .ckp-article { color: #000; font-size: 10pt; line-height: 1.45; }
  .ckp-layout { display: block; }
  .ckp-hero h1, .ckp-body h2, .ckp-body h3 { color: #000; }
  .ckp-abstract, .ckp-callout, .ckp-definition, .ckp-diagram,
  .ckp-finding, .ckp-stat { background: #fff !important; border-color: #999 !important; }
  .ckp-body h2 { page-break-after: avoid; }
  .ckp-diagram, .ckp-table, .ckp-callout, .ckp-pull { page-break-inside: avoid; }
  .ckp-table td, .ckp-table th { color: #000; }
}
</style>

<div id="ckp-progress"></div>
<button id="ckp-top" aria-label="Back to top">↑</button>

<article class="ckp-article">

<!-- ═══════════════════ HERO ═══════════════════════════════════ -->
<div class="ckp-hero">
  <div class="ckp-kicker">Mobile Security · Ad-Tech Telemetry · Operational Security</div>
  <h1>Bought, <em>Not Hacked</em></h1>
  <p class="ckp-deck">An adversary no longer needs to compromise a phone to follow the person carrying it. The advertising industry already collects the data, and it is for sale. This is a technical reference architecture for reducing, enforcing and evidencing that exposure on managed Android devices — and an honest account of what such an architecture cannot do.</p>
  <div class="ckp-meta">
    <span>Mobile Security Series</span>
    <span class="dot"></span>
    <span>Technical White Paper · 2026</span>
    <span class="dot"></span>
    <span>~40 min read</span>
    <span class="dot"></span>
    <span>Sara Malik &amp; Naveed A. Aun</span>
    <span class="dot"></span>
    <span><a href="mailto:smk@pakcrypt.org">smk@pakcrypt.org</a></span>
  </div>
</div>

<!-- Keywords -->
<div class="ckp-keywords">
  <span class="ckp-kw">Advertising Identifier</span>
  <span class="ckp-kw">Real-Time Bidding</span>
  <span class="ckp-kw">Data Brokers</span>
  <span class="ckp-kw">Pattern of Life</span>
  <span class="ckp-kw">Android Enterprise</span>
  <span class="ckp-kw">Protective DNS</span>
  <span class="ckp-kw">WireGuard</span>
  <span class="ckp-kw">Application Admission</span>
  <span class="ckp-kw">Ubiquitous Technical Surveillance</span>
</div>

<!-- Mobile TOC -->
<div class="ckp-mobile-toc" id="ckp-mob-toc-toggle">
  <span>Contents</span><span>▾</span>
</div>
<div class="ckp-mobile-toc-list" id="ckp-mob-toc-list">
  <a href="#abstract">Abstract</a>
  <a href="#sec-market">1. The Market That Does the Work</a>
  <a href="#sec-inside">2. What Actually Leaves the Phone</a>
  <a href="#sec-routes">3. Six Ways Out</a>
  <a href="#sec-maid">4. Why Killing the Ad ID Isn't Enough</a>
  <a href="#sec-controls">5. What Each Control Buys You</a>
  <a href="#sec-arch">6. The Architecture</a>
  <a href="#sec-backfire">7. Two Risks the Architecture Creates</a>
  <a href="#sec-claims">8. What You May Honestly Claim</a>
  <a href="#sec-verify">9. Proving It</a>
  <a href="#sec-glossary">Glossary</a>
  <a href="#references">References</a>
</div>

<!-- ═══════════════════ LAYOUT ════════════════════════════════ -->
<div class="ckp-layout">
<div class="ckp-body">

<!-- ABSTRACT -->
<div class="ckp-abstract" id="abstract">
  <div class="ckp-abstract-label">Abstract</div>
  <p>Ordinary smartphone applications generate commercially valuable telemetry — a device-linked identifier, coordinates, timestamps, network addresses, application activity — which aggregators join into a historical pattern of life. For a consumer this is a privacy problem. For personnel with duty stations, routines and deployment cycles it is an operational security problem, because the analytical output of the advertising ecosystem is the same product a hostile service would otherwise run a collection operation to obtain.</p>
  <p>This paper decomposes that ecosystem: what is collected and by what mechanism, the six distinct routes by which data leaves a handset, and the off-device pipeline that converts events into targeting material. It then evaluates each candidate control — protective DNS, always-on tunnelling, TLS interception, device management, application allowlisting, identifier suppression, operating-system customisation, sandboxing, DNSSEC — stating for each what it removes and what survives it. A layered reference architecture follows, together with the verification programme required before any assurance claim is made.</p>
  <p>Two conclusions are unusual enough to state at the outset. The architecture creates risks as well as removing them: concentrating a population onto uniform infrastructure conceals identity while making affiliation more legible, and the evidence trail such a system produces is itself the asset it exists to deny. And the defensible product claim is narrower than the market rewards — measured, enforced and evidenced exposure reduction, not untraceability.</p>
</div>

<!-- STATS BAR -->
<div class="ckp-stat-row">
  <div class="ckp-stat"><span class="stat-num">500M+</span><span class="stat-label">Advertising IDs paired with precise location in one broker action</span></div>
  <div class="ckp-stat"><span class="stat-num">6</span><span class="stat-label">Distinct egress routes off the handset</span></div>
  <div class="ckp-stat"><span class="stat-num">2</span><span class="stat-label">Routes no device-side filter can reach</span></div>
  <div class="ckp-stat"><span class="stat-num">2025</span><span class="stat-label">Privacy Sandbox on Android deprecated</span></div>
</div>

<!-- ─── SECTION 1 ─────────────────────────────────────────── -->
<section id="sec-market">
<h2>1. The Market That Does the Work</h2>

<p class="drop-cap">A modern smartphone emits a continuous stream of individually trivial observations. An application opened. A coordinate resolved. An advertisement requested. A connection made from a particular network address at a particular second. None of these is a secret, and none of them was stolen.</p>

<p>Aggregated across applications, across weeks and across a population, they resolve into something quite different: a reconstructable account of where a device sleeps, where it works, which other devices travel with it, and how that pattern changes over time. This is not a side effect of a security failure. It is the intended function of an industry that exists to buy and sell audience attention, operating through documented protocols, standardised schemas and lawful commercial contracts.</p>

<p>The same pipeline that lets a retailer measure whether an advertisement produced a store visit lets a purchaser ask which devices were present at a specific facility on a specific night.</p>

<div class="ckp-pull">
  <p>An adversary does not need to compromise a device, break cryptography, or subvert a carrier. It needs a budget, a corporate identity, and access to a market designed to sell exactly this data.</p>
  <cite>The structural asymmetry</cite>
</div>

<p>Defensive spending is therefore competing against a supply chain whose marginal cost of producing the targeting material is close to zero. That asymmetry, more than any individual technical detail, is what makes this problem different from the ones security teams are used to.</p>

<h3>What is actually at risk</h3>

<p>The asset under protection is not a file. It is a set of inferences an adversary wishes to construct.</p>

<ul class="ckp-hier">
  <li><strong>Residence</strong> — the location of repeated overnight presence, which extends the exposure to family members.</li>
  <li><strong>Duty station</strong> — the location of repeated weekday presence, and the facility it maps to.</li>
  <li><strong>Affiliation</strong> — association of a device with an organisation, unit, command or programme.</li>
  <li><strong>Co-travel graph</strong> — devices that repeatedly move together, revealing teams, protective details and hierarchies.</li>
  <li><strong>Tempo</strong> — rates of arrival, departure, concentration and dispersal, revealing readiness and operational cycles.</li>
  <li><strong>Facility discovery</strong> — previously unpublished locations inferred from anomalous device density.</li>
  <li><strong>Personal vulnerability</strong> — financial, medical, religious or relational indicators usable for coercion.</li>
</ul>

<div class="ckp-callout key">
  <strong>Identity is frequently unnecessary</strong>
  <p>An adversary rarely needs a legal name. "A persistent device associated with this command, which departed this airfield on this date" is operationally sufficient for surveillance, coercion targeting or physical action. Defences designed around preventing <em>identification</em>, while permitting stable pseudonymous linkage, address the wrong property.</p>
</div>

<h3>The documented record</h3>

<p>This threat is evidenced rather than hypothesised, and three strands of public record matter.</p>

<p>On 4 September 2026, correspondence released by members of the United States Congress confirmed that the Army, the Air Force, the Department of the Navy and United States Special Operations Command each disable the mobile advertising identifier on government-issued devices. The memoranda were dated between 8 July and 18 August 2026. Reporting accompanying the release recorded that advertising identifiers had been blocked on Army Windows computers since before 2021, but disabled by default on Army-managed Android and Apple mobile devices only since at least February 2026 [<a href="#ref-Reuters2026">Reuters2026</a>]. The measures followed reporting that commercially available location data had been used to surveil or target personnel in the Middle East. The same legislators asked the Department of Defense Office of Inspector General to assess whether existing controls are effective, and stated publicly that the measures taken had not neutralised the threat.</p>

<p>Three engineering conclusions follow, and they matter more than the headline.</p>

<div class="ckp-chain">
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">01</div>
    <div class="ckp-chain-content">
      <h4>Staggered implementation implies a historical corpus</h4>
      <p>Controls applied in 2026 do not retract data collected in preceding years. Any architecture must assume a baseline profile of the protected population already exists in commercial and adversary holdings, and that its value decays slowly.</p>
    </div>
  </div>
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">02</div>
    <div class="ckp-chain-content">
      <h4>The control chosen was the cheapest available one</h4>
      <p>Disabling an identifier is a configuration change. It was selected because it is deployable at fleet scale without touching applications — which is a legitimate reason, and also precisely why it is insufficient.</p>
    </div>
  </div>
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">03</div>
    <div class="ckp-chain-content">
      <h4>The declared residual concern was unmanaged devices</h4>
      <p>The public record identifies personal devices carried by personnel and their families into sensitive areas as a continuing exposure. No managed-device product solves this, and vendors should say so rather than obscure it.</p>
    </div>
  </div>
</div>

<h4>Regulatory findings</h4>

<p>Enforcement action in the United States has established, as findings in administrative proceedings rather than as advocacy, several facts a technical design must accommodate. Raw location data paired with a mobile advertising identifier is not anonymous and can be used to associate a device with the places its user visited. A firm participating in real-time bidding retained the data in bid requests <em>including for auctions it did not win</em>, accumulating in excess of 500 million unique advertising identifiers paired with precise location over roughly two and a half years [<a href="#ref-FTCMobilewalla">FTCMobilewalla</a>]. Audience products have been built on visits to sensitive locations, and orders have specifically enumerated military installations alongside health, religious and political sites.</p>

<p>In February 2026 the Federal Trade Commission issued warning letters to thirteen data brokers concerning the Protecting Americans' Data from Foreign Adversaries Act, which prohibits supplying personally identifiable sensitive data — expressly including geolocation — to designated foreign adversary countries. The published letter template states that the Commission identified instances of companies offering products involving an individual's status as a member of the armed forces [<a href="#ref-FTCPADFAA">FTCPADFAA</a>].</p>

<div class="ckp-callout warn">
  <strong>Do not treat regulation as a technical control</strong>
  <p>Statutory restriction reduces lawful availability through compliant brokers in one jurisdiction. It does not affect non-compliant suppliers, intermediaries in permissive jurisdictions, foreign-origin data, or unlawful acquisition — and it does not reach data already transferred. It changes the adversary's cost, not the handset's behaviour. A design that relies on it has no defence when it is circumvented.</p>
</div>

<h3>Where the boundary falls</h3>

<p>The path from an ordinary application to a targeting product has six stages, and only the first two lie within a handset-based product's reach.</p>

<div class="ckp-diagram">
  <div class="ckp-diagram-head">
    <span class="ckp-diagram-label">Fig. 1 — Commercial surveillance chain</span>
    <button class="ckp-copy">Copy</button>
  </div>
<pre><code>[1] GENERATION      Application + embedded SDK produce an event
                    identifier | timestamp | context | location
                              |
[2] EGRESS          Event leaves the handset over TLS          &lt;-- device-side
                    direct to vendor, or to publisher backend      control ends
                              |                                    here
=================== LIMIT OF DEVICE ENFORCEMENT ===================
                              |
[3] DISTRIBUTION    Mediation, attribution, supply-side platform,
                    exchange broadcast to many demand-side bidders
                              |
[4] AGGREGATION     Normalisation, identifier joins, identity
                    resolution, location enrichment
                              |
[5] PRODUCTISATION  Audience segments, mobility datasets, query
                    platforms, measurement services
                              |
[6] ACQUISITION     Purchase by commercial, governmental or
                    hostile end-user -&gt; pattern-of-life analysis</code></pre>
</div>

<p>A device-side product can determine which code executes, what that code may access, and where packets may go. It cannot determine what a lawfully contacted backend does with data it legitimately received. Stage 3 onward is addressable only by rejecting the application, obtaining a telemetry-suppressed build from the publisher, or binding the publisher contractually. Any architecture that does not say this plainly is concealing its principal limitation.</p>

<h3>In scope, partly in scope, out of scope</h3>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead><tr><th>Exposure</th><th>Status</th><th>Note</th></tr></thead>
<tbody>
<tr><td><span class="term">Third-party ad &amp; analytics SDKs</span></td><td><span class="ckp-pill ok">In scope</span></td><td>Primary target.</td></tr>
<tr><td><span class="term">Cross-app identifier linkage</span></td><td><span class="ckp-pill ok">In scope</span></td><td>Suppression plus egress control.</td></tr>
<tr><td><span class="term">Unapproved app installation</span></td><td><span class="ckp-pill ok">In scope</span></td><td>Allowlisting.</td></tr>
<tr><td><span class="term">Excess sensor &amp; location permissions</span></td><td><span class="ckp-pill ok">In scope</span></td><td>Permission policy.</td></tr>
<tr><td><span class="term">Direct-IP / alternate resolver evasion</span></td><td><span class="ckp-pill ok">In scope</span></td><td>Enforced at the gateway.</td></tr>
<tr><td><span class="term">First-party backend forwarding</span></td><td><span class="ckp-pill partial">Partial</span></td><td>Only via admission, publisher builds or contract.</td></tr>
<tr><td><span class="term">Authenticated account correlation</span></td><td><span class="ckp-pill partial">Partial</span></td><td>Reduced by account separation; not eliminable.</td></tr>
<tr><td><span class="term">Probabilistic fingerprinting</span></td><td><span class="ckp-pill partial">Partial</span></td><td>Reduced by fleet uniformity.</td></tr>
<tr><td><span class="term">Cellular network location</span></td><td><span class="ckp-pill no">Out</span></td><td>Inherent to network operation.</td></tr>
<tr><td><span class="term">Baseband / firmware compromise</span></td><td><span class="ckp-pill no">Out</span></td><td>Mitigated only by hardware choice and patch currency.</td></tr>
<tr><td><span class="term">OS vendor telemetry</span></td><td><span class="ckp-pill partial">Partial</span></td><td>Reducible; not eliminable with platform services present.</td></tr>
<tr><td><span class="term">Unmanaged personal devices</span></td><td><span class="ckp-pill no">Out</span></td><td>Operational policy problem.</td></tr>
<tr><td><span class="term">Physical and RF surveillance</span></td><td><span class="ckp-pill no">Out</span></td><td>Outside the device boundary entirely.</td></tr>
</tbody>
</table>
</div>
</section>

<div class="ckp-sep">Inside the Handset</div>

<!-- ─── SECTION 2 ─────────────────────────────────────────── -->
<section id="sec-inside">
<h2>2. What Actually Leaves the Phone</h2>

<p>Informal discussion uses "data" to mean four different things with different security properties. Engineering requires the distinction, because each demands a different control.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead><tr><th>Category</th><th>Definition</th><th>Controlled by</th></tr></thead>
<tbody>
<tr><td><span class="term">Observation</span></td><td>A raw measured value: a coordinate, an address, an event, a timestamp.</td><td>Permission &amp; application admission</td></tr>
<tr><td><span class="term">Identifier</span></td><td>A value whose purpose is to make observations joinable.</td><td>Suppression &amp; isolation</td></tr>
<tr><td><span class="term">Attribute</span></td><td>A descriptive property: model, screen geometry, locale, carrier.</td><td>Uniformity, <em>not</em> removal</td></tr>
<tr><td><span class="term">Inference</span></td><td>A derived conclusion: home, workplace, affiliation, intent.</td><td>Nothing on-device. This is the asset.</td></tr>
</tbody>
</table>
</div>

<h3>The SDK is inside the permission boundary</h3>

<p>An advertising or analytics SDK is a library compiled into a host application. Absent a platform-provided separation mechanism, it executes under the host application's Linux UID and inherits the host application's granted permissions. This single fact is the root of the problem: Android's permission model authorises <em>applications</em>, and the SDK is, to the platform, part of the application.</p>

<div class="ckp-diagram">
  <div class="ckp-diagram-head">
    <span class="ckp-diagram-label">Fig. 2 — The grant the SDK inherits</span>
    <button class="ckp-copy">Copy</button>
  </div>
<pre><code>+---------------------------------------------------+
|  Application package  (one Linux UID, one sandbox) |
|                                                    |
|   Host application code  ....... location granted  |
|   Advertising SDK        ....... location granted  |  &lt;-- same grant
|   Analytics SDK          ....... location granted  |
|   Attribution SDK        ....... location granted  |
|   Mediation adapters     ....... location granted  |
+---------------------------------------------------+

Android cannot express: "the mapping feature may use location,
but the embedded advertising library may not."</code></pre>
</div>

<p>Collection proceeds through five mechanisms, and two of them defeat any reasoning based purely on permissions.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead><tr><th>ID</th><th>Mechanism</th><th>Description</th></tr></thead>
<tbody>
<tr><td><span class="term">M1</span></td><td>Direct platform API calls</td><td>Values available without special permission: advertising identifier (subject to manifest declaration), model, OS version, locale, network state, display metrics.</td></tr>
<tr><td><span class="term">M2</span></td><td>Inherited runtime permissions</td><td>Location, Bluetooth scanning, microphone, camera, contacts, telephony — reachable only where the host holds the grant.</td></tr>
<tr><td><span class="term">M3</span></td><td>Publisher-supplied events</td><td>The host application calls the SDK's event interface with arbitrary names and parameters. Unbounded by design.</td></tr>
<tr><td><span class="term">M4</span></td><td>Network-layer observation</td><td>The receiving endpoint observes source address, TLS metadata and timing without the SDK reading anything.</td></tr>
<tr><td><span class="term">M5</span></td><td>Derived computation</td><td>Fingerprints, session identifiers, fraud scores, behavioural classifications computed from the preceding four.</td></tr>
</tbody>
</table>
</div>

<div class="ckp-callout">
  <strong>M3 and M4 defeat permission-centric reasoning</strong>
  <p>A design that reasons only about permissions concludes that an application with no location permission cannot contribute to location tracking. It can: the publisher may pass a user-selected city or delivery address as an event attribute (M3), and the receiving server always observes a network address that resolves to a region, carrier or enterprise (M4).</p>
</div>

<h3>The signal taxonomy</h3>

<p>There is no complete enumeration of what "every advertising SDK collects" — behaviour varies by SDK version, host configuration, granted permissions, mediation partners, remote configuration and jurisdiction. What follows is a taxonomy of what is <em>technically reachable</em> under stated conditions. Platform restrictions are stated alongside, because overstating collection is an audit liability.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead><tr><th>Signal</th><th>M</th><th>Linkage value &amp; platform restriction</th></tr></thead>
<tbody>
<tr class="group"><td colspan="3">A. Identifiers</td></tr>
<tr><td><span class="term">Advertising ID</span></td><td>M1</td><td>Resettable device-and-user scoped join key usable across unrelated applications. Applications targeting Android 13+ must declare the <code>AD_ID</code> permission; absent that declaration the value returned is zeroed, as it is when the user deletes the identifier [<a href="#ref-Android13">Android13</a>].</td></tr>
<tr><td><span class="term">App Set ID</span></td><td>M1</td><td>Scoped to one developer's applications on one device. <strong>Deleting the advertising ID does not remove this developer-scoped linkage.</strong></td></tr>
<tr><td><span class="term">App-instance ID</span></td><td>M1</td><td>Generated locally on first run, stored in private storage, sent with every event. Survives advertising-ID reset entirely.</td></tr>
<tr><td><span class="term">Account / user ID</span></td><td>M3</td><td>Deterministic linkage across devices, reinstalls and channels. <strong>More persistent and more identifying than the advertising ID.</strong></td></tr>
<tr><td><span class="term">Hashed email or phone</span></td><td>M3</td><td>Identity resolution against advertiser and broker records. Hashing is not anonymisation when the input space is enumerable.</td></tr>
<tr><td><span class="term">Vendor SDK identifiers</span></td><td>M1</td><td>Each SDK may maintain its own installation and session identifiers. One application can carry several independent linkage keys.</td></tr>
<tr><td><span class="term">IMEI, IMSI, SIM serial</span></td><td>M2</td><td>Highly persistent. <strong>Heavily restricted on modern Android</strong>; requires privileged, carrier or default-handler status. Its presence in analysis output is a finding in itself.</td></tr>
<tr><td><span class="term">Hardware MAC address</span></td><td>M1</td><td><strong>Not available to ordinary applications</strong>; interface addresses are randomised per network. Frequently and incorrectly listed as routinely collected.</td></tr>
<tr><td><span class="term">Push token</span></td><td>M1</td><td>Durable reachability handle for one application installation.</td></tr>
<tr><td><span class="term">Attribution / click IDs</span></td><td>M3</td><td>Connect an impression or click to an install, registration or purchase.</td></tr>

<tr class="group"><td colspan="3">B. Network and transport</td></tr>
<tr><td><span class="term">Public IP address</span></td><td>M4</td><td>Observed by every receiving server irrespective of SDK behaviour. Yields approximate geography, carrier or enterprise identification, household correlation and short-term cross-app linkage. A tunnel changes which address is visible; it does not remove the signal.</td></tr>
<tr><td><span class="term">Carrier, MCC/MNC, connection type</span></td><td>M1/M4</td><td>Market classification and fraud scoring; carried as structured fields in bid requests.</td></tr>
<tr><td><span class="term">VPN / proxy indication</span></td><td>M4</td><td>Inferred server-side. Does not reveal the origin address — but marks the traffic as tunnelled, which is itself an attribute. See §7.</td></tr>
<tr><td><span class="term">Wi-Fi network information</span></td><td>M2</td><td>SSID, BSSID and scan results are gated behind location or nearby-device permissions. Where available, supports precise indoor positioning.</td></tr>

<tr class="group"><td colspan="3">C. Location</td></tr>
<tr><td><span class="term">Precise / fused location</span></td><td>M2</td><td>Latitude, longitude, accuracy, altitude, speed, bearing, timestamp. The highest-value signal in the catalogue.</td></tr>
<tr><td><span class="term">Approximate location</span></td><td>M2</td><td>Sufficient for regional analytics; insufficient alone for facility-level targeting, but joins with stronger signals.</td></tr>
<tr><td><span class="term">IP-derived location</span></td><td>M4</td><td>Country, region, city, sometimes network operator. Weak alone; corroborative in aggregate.</td></tr>
<tr><td><span class="term">Bluetooth beacon proximity</span></td><td>M2</td><td>Indoor position, visitation, and device-to-device proximity — directly relevant to co-travel analysis.</td></tr>
<tr><td><span class="term">Application-supplied place</span></td><td>M3</td><td>A branch, delivery address or map selection passed as an event attribute. <strong>Produces location targeting with no location permission.</strong></td></tr>

<tr class="group"><td colspan="3">D. Device attributes</td></tr>
<tr><td><span class="term">Make, model, hardware class</span></td><td>M1</td><td>Creative compatibility and purchasing-power inference; a standard bid-request field.</td></tr>
<tr><td><span class="term">OS version and build</span></td><td>M1</td><td>Compatibility, vulnerability scoring, segmentation.</td></tr>
<tr><td><span class="term">Screen geometry &amp; density</span></td><td>M1</td><td>Format selection; meaningful fingerprint entropy.</td></tr>
<tr><td><span class="term">Battery and charging state</span></td><td>M1</td><td>Rendering decisions, diagnostics, automation detection.</td></tr>
<tr><td><span class="term">Integrity &amp; tampering signals</span></td><td>M1/M5</td><td>Root and emulator detection, signature verification, platform attestation verdicts. Legitimate anti-fraud function — and a reliable detector of virtualised environments. See §5.</td></tr>
<tr><td><span class="term">Installed-application info</span></td><td>M1</td><td>Interest inference and competitor detection. <strong>Broad enumeration is restricted</strong> by package-visibility rules; targeted queries remain possible.</td></tr>

<tr class="group"><td colspan="3">E. Behavioural events</td></tr>
<tr><td><span class="term">Launch, session, duration</span></td><td>M1/M3</td><td>Establishes that a specific device used a specific application at a specific time. With address and timestamp this alone supports co-presence analysis.</td></tr>
<tr><td><span class="term">Search terms &amp; content viewed</span></td><td>M3</td><td><strong>Discloses health, religious, financial, political or affiliation characteristics without any location signal.</strong> Frequently underestimated.</td></tr>
<tr><td><span class="term">Commerce and conversion events</span></td><td>M3</td><td>Return-on-spend modelling and high-value audience construction.</td></tr>
<tr><td><span class="term">Custom events</span></td><td>M3</td><td>Arbitrary names and parameter dictionaries chosen by the publisher. <strong>The reason an exhaustive list is impossible.</strong></td></tr>

<tr class="group"><td colspan="3">F. Diagnostics and high-permission data</td></tr>
<tr><td><span class="term">Crash reports &amp; stack traces</span></td><td>M1</td><td>Developer-added metadata in traces can carry URLs, identifiers and application state unintentionally.</td></tr>
<tr><td><span class="term">Interaction cadence &amp; motion</span></td><td>M2/M5</td><td>Human-versus-automation discrimination. Anti-fraud vendors disclose little; treat claimed exhaustive lists sceptically.</td></tr>
<tr><td><span class="term">Contacts, calendar, SMS</span></td><td>M2</td><td>Identity resolution and social-graph construction. Heavily restricted; third-party SDK access should be a disqualifying finding.</td></tr>
<tr><td><span class="term">Microphone and camera</span></td><td>M2</td><td>Legitimate only in specific, visible formats with permission. <strong>Claims that mainstream ad SDKs continuously listen are not supported by primary evidence</strong> and are not needed to explain accurate targeting.</td></tr>
<tr><td><span class="term">Accessibility-derived content</span></td><td>M2</td><td>Characteristic of assistive technology or surveillance software, <strong>not</strong> of advertising libraries. Any ad component requesting it should be presumed hostile.</td></tr>
</tbody>
</table>
</div>

<div class="ckp-callout warn">
  <strong>Why the restrictions are stated</strong>
  <p>Several of these signals are routinely listed in industry commentary as freely collected. On a current, correctly configured Android device they are restricted or unavailable. Including unsupportable claims in a threat analysis invites an auditor to discount the supportable ones — and here, the supportable ones are more than sufficient to establish the risk.</p>
</div>
</section>

<div class="ckp-sep">Egress</div>

<!-- ─── SECTION 3 ─────────────────────────────────────────── -->
<section id="sec-routes">
<h2>3. Six Ways Out</h2>

<p>Data does not simply travel "from SDK to broker." It leaves by at least six distinct routes, and the device-side enforceability of each differs sharply. This table is the single most important input to any architecture, because it determines which problems network filtering can solve and which it structurally cannot.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead><tr><th>Route</th><th>Mechanism</th><th>Device-side enforceability</th></tr></thead>
<tbody>
<tr><td><span class="term">R1 Direct to vendor</span></td><td>SDK serialises events, queues them locally, posts over TLS to the vendor's collector.</td><td><span class="ckp-pill ok">High</span> Distinct destination; blockable by domain or destination policy.</td></tr>
<tr><td><span class="term">R2 Publisher relay</span></td><td>SDK reports to the application's own backend; the publisher forwards server-to-server afterwards.</td><td><span class="ckp-pill no">None</span> The handset never contacts the recipient. <em>The defining limitation of all network filtering.</em></td></tr>
<tr><td><span class="term">R3 Attribution partner</span></td><td>A measurement partner receives clicks from networks and installs from the application, then matches them.</td><td><span class="ckp-pill partial">Partial</span> Device leg blockable; matching occurs off-device.</td></tr>
<tr><td><span class="term">R4 Mediation</span></td><td>One monetisation SDK invokes multiple networks and remotely configured adapters.</td><td><span class="ckp-pill partial">Partial</span> Auditing only the primary SDK is insufficient; the recipient set is configurable after deployment.</td></tr>
<tr><td><span class="term">R5 Real-time bidding</span></td><td>A bid request describing the impression, device, geography and identifiers is broadcast to many buyers.</td><td><span class="ckp-pill partial">Partial</span> The initial request is blockable; the broadcast fan-out is entirely off-device.</td></tr>
<tr><td><span class="term">R6 Broker aggregation</span></td><td>A broker purchases feeds from publishers, SDK operators, exchanges and other brokers.</td><td><span class="ckp-pill no">None</span> No code on the handset.</td></tr>
</tbody>
</table>
</div>

<h3>The bidstream is a broadcast channel</h3>

<p>Real-time bidding deserves separate treatment because it inverts the usual assumption that data flows to a party the device chose to contact. The supply-side platform constructs a request describing the impression and broadcasts it to many demand-side bidders. Every recipient sees the device context; exactly one wins. The regulatory record establishes that at least one firm retained bid-request contents from auctions it lost, at a scale exceeding 500 million unique advertising identifiers paired with precise location [<a href="#ref-FTCRTB">FTCRTB</a>].</p>

<div class="ckp-pull">
  <p>One advertisement request can disclose device context to dozens of independent commercial entities in milliseconds, with no technical mechanism preventing non-winning recipients from retaining it.</p>
  <cite>Why defence-tier catalogues exclude ad-funded apps entirely</cite>
</div>

<p>Any application that serves programmatic advertising should therefore be treated as a broadcast channel for device context. This — not the presence of a named "bad SDK" — is the reason a high-assurance application catalogue excludes advertising-supported applications as a class rather than case by case.</p>

<h3>What happens after the handset</h3>

<p>Raw events acquire value through a six-stage pipeline operating entirely beyond the device's reach. Understanding it is necessary to understand which device-side controls actually degrade the output.</p>

<ul class="ckp-hier">
  <li><strong>S1 Normalisation</strong> — heterogeneous supplier schemas converted to a common record, malformed rows dropped, confidence scores assigned.</li>
  <li><strong>S2 Identifier joins</strong> — records grouped by advertising ID, app set ID, instance ID, account ID, hashed contact details, or address-plus-time-window heuristics. Where no direct identifier exists, <em>identity bridging</em> substitutes inferred linkage; industry specifications now carry provenance fields describing who performed such a substitution, which is an admission that it happens.</li>
  <li><strong>S3 Identity resolution</strong> — the pseudonymous device connected to a household, a second device, a browser, an account or a postal address, deterministically or probabilistically.</li>
  <li><strong>S4 Location enrichment</strong> — coordinates mapped to building polygons and point-of-interest categories. Overnight presence suggests residence; weekday presence suggests employment.</li>
  <li><strong>S5 Profile construction</strong> — events become categorical labels: frequent traveller, likely resident, visitor to a given facility, member of an organisation. These are inferences and can be wrong, stale or contaminated by shared family devices.</li>
  <li><strong>S6 Segment and model production</strong> — matching devices become an audience; models extend it to similar devices.</li>
</ul>

<div class="ckp-callout key">
  <strong>Where device-side control actually bites</strong>
  <p>Controls that remove identifiers degrade S2. Controls that remove location degrade S4. Controls that reduce the number of participating applications degrade S1 by starving the pipeline of input. <strong>No device-side control degrades S3</strong> — identity resolution operates on whatever reaches the aggregator by any route, including R2 and R6. This asymmetry is why application admission, which decides who receives anything at all, outperforms filtering.</p>
</div>

<h3>How it is sold</h3>

<p>"Selling data" rarely means transferring a file, and the commercial form determines the intelligence risk. A raw event feed lets the buyer perform its own joins. An audience segment is a list of identifiers activated through an advertising platform. A clean room returns matches without releasing the underlying data. A measurement service sells an answer rather than records.</p>

<p>The form most directly convertible into a targeting product is the <strong>query platform</strong>: a dashboard or API permitting geofence drawing, device enumeration within an area and movement analysis. It answers "which devices were within this polygon during this interval, and where else have they been?" without the purchaser holding or processing any raw dataset at all.</p>

<p>The supply chain does not distinguish between buyers. The same audience-segment mechanism that identifies likely vehicle purchasers identifies likely visitors to a military installation. The difference is the query, not the infrastructure.</p>
</section>

<div class="ckp-sep">The Obvious Control</div>

<!-- ─── SECTION 4 ─────────────────────────────────────────── -->
<section id="sec-maid">
<h2>4. Why Killing the Advertising ID Isn't Enough</h2>

<p>Suppressing the advertising identifier is the control most organisations reach for first, and they are right to. It destroys the cheapest, most standardised cross-application join key in the ecosystem. It is also, on its own, close to the smallest meaningful intervention available.</p>

<p>Consider a managed device on which the advertising identifier has been deleted or zeroed, and follow what survives.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead><tr><th>Linkage mechanism</th><th>State after suppression</th></tr></thead>
<tbody>
<tr><td><span class="term">App Set ID</span></td><td><span class="ckp-pill no">Intact</span> Links applications from the same developer.</td></tr>
<tr><td><span class="term">App-instance IDs</span></td><td><span class="ckp-pill no">Intact</span> One per SDK per installation, indefinitely stable.</td></tr>
<tr><td><span class="term">Account identity</span></td><td><span class="ckp-pill no">Intact</span> Stronger than the identifier removed — it spans devices and reinstalls.</td></tr>
<tr><td><span class="term">Push tokens</span></td><td><span class="ckp-pill no">Intact</span> Durable per-installation handle.</td></tr>
<tr><td><span class="term">Source address correlation</span></td><td><span class="ckp-pill no">Intact</span> Joins any applications active from the same address in the same window.</td></tr>
<tr><td><span class="term">Publisher event attributes</span></td><td><span class="ckp-pill no">Intact</span> Including application-supplied place data.</td></tr>
<tr><td><span class="term">Attribute fingerprint</span></td><td><span class="ckp-pill no">Intact</span> Model, OS build, display geometry, locale, time zone.</td></tr>
<tr><td><span class="term">Server-side identity graph</span></td><td><span class="ckp-pill no">Intact</span> Specifically designed to survive identifier resets.</td></tr>
<tr><td><span class="term">Historical profile</span></td><td><span class="ckp-pill no">Intact</span> Prior linkage is not retroactively broken.</td></tr>
</tbody>
</table>
</div>

<div class="ckp-callout warn">
  <strong>A necessary control with a bounded effect</strong>
  <p>Advertising-identifier suppression removes one edge from a graph that has many, and leaves at least eight other linkage mechanisms operational — several more persistent than the one removed. It should be deployed, it should be enforced by policy rather than left to the user, and it should never be presented as the control that solves the problem.</p>
</div>

<h3>The 2026 platform position</h3>

<p>Guidance written before 2025 is materially out of date, and one change in particular reshapes the design space.</p>

<div class="ckp-definition">
  <div class="ckp-def-label">Platform status, September 2026</div>
  <p>As of 17 October 2025 the Privacy Sandbox on Android programme — including the SDK Runtime, Topics, Protected Audience and Android attribution reporting — is deprecated, alongside the equivalent web APIs. Any architecture predicated on advertising SDKs migrating into a platform-provided isolated runtime, or on identifier-based targeting being superseded by on-device topic inference, is obsolete. The identifier-and-bidstream model described here is the operative model, not a legacy one.</p>
</div>

<p>Two further points of platform hygiene matter for design. Advertising-identifier access is declaration-gated: applications targeting Android 13 or later must declare the Play services <code>AD_ID</code> permission or receive zeros. This gives both a control surface and a reliable static signal for an admission pipeline — including when the declaration arrives by library manifest merge rather than by the developer's own hand. And store-facing data-safety declarations are developer assertions, covering the application and its embedded third-party components; the publisher holds information the store cannot independently determine. Treat every declaration as an input to analysis and never as a substitute for it.</p>

<h3>The right engineering primitive</h3>

<p>The preceding analysis implies a specific data model. Rather than maintaining a list of "advertising companies," the platform should represent every outbound transmission as a structured, answerable object.</p>

<div class="ckp-diagram">
  <div class="ckp-diagram-head">
    <span class="ckp-diagram-label">Fig. 3 — The outbound event as the unit of analysis</span>
    <button class="ckp-copy">Copy</button>
  </div>
<pre><code>OUTBOUND EVENT
--------------------------------------------------------------
device            pseudonymous identity, assurance tier
application       package name, version, signing certificate
component         SDK or library attributed, where determinable
permissions       grants held by the application at the time
identifiers       which linkage keys were reachable
destination       hostname, resolved address, owning legal entity
route             R1..R6 classification
necessity         required | optional | unjustified
decision          allowed | blocked | monitored, with reason code
policy            policy version and rule provenance
--------------------------------------------------------------</code></pre>
</div>

<p>This model survives the case where one hostname carries operational traffic, diagnostics and advertising telemetry simultaneously. It survives endpoint rotation, because the question is about a relationship rather than a name. And it produces a statement an assurance function can actually test: <em>this application version attempted to send this class of data to this destination under these permissions; policy allowed or blocked it for this reason; this is the residual exposure that remains.</em></p>

<p>"We block advertising domains, therefore the user cannot be tracked" is not a testable statement, and asserting it in front of a technical evaluation board is a commercial risk.</p>
</section>

<div class="ckp-sep">Control Analysis</div>

<!-- ─── SECTION 5 ─────────────────────────────────────────── -->
<section id="sec-controls">
<h2>5. What Each Control Buys You</h2>

<p>The common framing — "should we use protective DNS, or device management, or a custom operating system?" — is a category error. These operate at different layers and fail in different ways, and a serious design uses several precisely because each one's failure mode is another one's strength. The productive question is: <em>what does each layer measurably remove, what remains after it, and what assurance level does the residue support?</em></p>

<h3>Protective DNS: useful, and structurally shallow</h3>

<p>Android's Private DNS encrypts resolution between handset and resolver. Protective DNS adds the policy layer — a resolver that can allow, block, redirect, sinkhole and record decisions, as characterised in joint NSA and CISA guidance which explicitly distinguishes protective DNS from both encrypted DNS and DNSSEC [<a href="#ref-PDNS">NSAPDNS</a>]. Against dedicated, separately hosted tracking infrastructure it works well and it is cheap.</p>

<p>It has seven distinct bypass classes. These are not implementation defects; they are consequences of what DNS is.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead><tr><th>Class</th><th>Bypass</th></tr></thead>
<tbody>
<tr><td><span class="term">L1 Granularity</span></td><td>DNS decides whether a host resolves. It cannot determine whether the subsequent request carries a session token, a map tile request or a coordinate. Where one hostname carries both essential function and telemetry, the decision is binary. <strong>This has no DNS-layer solution.</strong></td></tr>
<tr><td><span class="term">L2 First-party relay</span></td><td>Route R2. The handset never queries the recipient's domain. No device-side blocklist can observe it.</td></tr>
<tr><td><span class="term">L3 Hard-coded addresses</span></td><td>An application may connect to a literal address without resolving anything.</td></tr>
<tr><td><span class="term">L4 Embedded resolvers</span></td><td>An application may implement DNS over HTTPS internally or tunnel resolution through an ordinary API call. System Private DNS does not intercept every application-defined mechanism.</td></tr>
<tr><td><span class="term">L5 Shared infrastructure</span></td><td>Trackers behind major clouds, CDNs or rotating hostnames cannot be blocked at the apex without collateral damage.</td></tr>
<tr><td><span class="term">L6 Reactivity</span></td><td>A denylist must already know the destination. It misses newly registered domains, per-customer collectors, obfuscated names and behaviour activated by remote configuration after deployment.</td></tr>
<tr><td><span class="term">L7 Encryption ≠ concealment</span></td><td>Encrypted resolution protects one hop. It does not hide the source address from the destination, nor prevent the configured resolver from processing every query.</td></tr>
</tbody>
</table>
</div>

<div class="ckp-callout warn">
  <strong>Assessment</strong>
  <p>Protective DNS is high value for consumer advertisement reduction, moderate for enterprise telemetry reduction, near zero against first-party forwarding, and low against a deliberately evasive application. A product marketed as preventing commercial tracking of defence personnel cannot rest primarily on domain denylists — and a competent evaluator will establish this in under an hour. Deploy it as one layer; do not build the product on it.</p>
</div>

<p>One policy point belongs here rather than in implementation, because it is a design decision. <strong>Public advertisement-blocking lists must not be ingested directly into production.</strong> They carry no provenance, no expiry, no confidence rating and no false-positive rollback path. In an enterprise deployment a false positive is an outage; in a fail-closed defence deployment it is a device that cannot communicate. Public lists are intelligence input to an analyst-curated, signed, versioned and expiring policy set.</p>

<h3>Network egress: strictly stronger, with four ways to void it</h3>

<p>An always-on tunnel with lockdown forces device traffic through a controlled enforcement point and blocks connections that do not traverse it. Android supports this directly, and the Android Management API exposes it through the <code>alwaysOnVpnPackage</code> policy used together with <code>vpnConfigDisabled</code> to prevent user modification [<a href="#ref-AMAPI">AMAPI</a>]. This changes the enforcement primitive from "a name did not resolve" to "no packet left this device by an unauthorised route," defeating L3, L4 and much of L5.</p>

<p>It does not reveal the contents of correctly implemented TLS. A tunnel is a routing and metadata control, not a content control. Four failure modes void the assurance claim entirely:</p>

<ul class="ckp-hier">
  <li><strong>Split tunnelling</strong> — any excluded application or destination is an unobserved egress path. Undocumented exemptions invalidate the claim.</li>
  <li><strong>IPv6 leakage</strong> — the classic failure: IPv4 routed through the tunnel while native IPv6 escapes on the physical interface.</li>
  <li><strong>Pre-tunnel traffic</strong> — connections made after boot but before the tunnel establishes, or during reconnection after a network transition.</li>
  <li><strong>Encrypted DNS indistinguishable from HTTPS</strong> — resolution over TCP 443 or QUIC to an application's own first-party server cannot be separated from an ordinary API call without decryption.</li>
</ul>

<div class="ckp-callout key">
  <strong>The layers are interdependent by design</strong>
  <p>DNS decides whether a name should resolve. The tunnel decides whether any packet may leave by an unauthorised route. Application admission decides whether an approved destination can be trusted with what the application will send it. The final defence against L4 is not a protocol signature — it is that approved applications may contact only approved destinations. None is sufficient alone; the composition is the control.</p>
</div>

<h3>TLS interception: the wrong control for production</h3>

<p>The temptation is obvious. If payload visibility would resolve L1, intercept the payload. The recommendation is nonetheless unambiguous.</p>

<p>It does not reliably work: applications may decline to trust user-installed certificate authorities, pin to specific certificates or public keys, and use native networking stacks that ignore platform trust entirely. Coverage is partial and unpredictable — the worst property an assurance control can have. It breaks things unpredictably: pinned applications fail, certificate rotation causes fleet-wide outages, and in a defence deployment the failure lands on a user who needs the device to work. And it concentrates catastrophic risk: a working interception point holds the organisation's decrypted credentials, messages, documents and location in one place. That asset is more valuable to an adversary than the advertising telemetry the programme set out to prevent.</p>

<p>Interception belongs in the isolated analysis laboratory, under explicit authorisation, with test accounts, for the purpose of characterising an application before admission. The findings then drive production controls that require no interception at all.</p>

<h3>Device management: necessary, and not an anti-tracking engine</h3>

<p>A fully managed, company-owned Android Enterprise device gives an administrator the broadest policy surface Android offers: always-on VPN and lockdown, forced installation and package blocking, explicit permission grant and denial, accessibility and input-method allowlists, untrusted-application and developer-settings policy, administrator-controlled private DNS, location and sensor modes, USB, tethering and Wi-Fi configuration, minimum API level, update policy, and network and security event reporting.</p>

<div class="ckp-callout">
  <strong>A control worth noticing</strong>
  <p>The <code>deviceRadioState</code> policy includes control of 2G cellular. Disabling 2G removes a downgrade path exploited by cell-site simulators. It is not an advertising-telemetry control, but it belongs in the same defence-tier policy and costs nothing to enable where coverage permits.</p>
</div>

<p>What management cannot do is determine what an approved application transmits. It can prevent installation of an application. It cannot determine that this payload, sent by an approved one, is a problem:</p>

<div class="ckp-diagram">
  <div class="ckp-diagram-head">
    <span class="ckp-diagram-label">Fig. 4 — Invisible to configuration policy</span>
    <button class="ckp-copy">Copy</button>
  </div>
<pre><code>{ "installation_id": "8f3a...persistent",
  "lat": 33.61, "lon": 73.05,
  "event": "session_start",
  "account": "u-40213" }</code></pre>
</div>

<p>Nor can it establish whether an approved application generates its own persistent identifier, correlates users after an advertising-ID reset, activates a new endpoint by remote configuration, or forwards server-to-server after collection. Managed application configuration only reaches settings the developer chose to expose — and many expose none. Management applies a policy; it does not create that policy and cannot verify that approved applications obey it. Any proposal presenting "deploy a management product" as the complete answer is a commercial position rather than a technical one.</p>

<h3>Application allowlisting: strong foundation, common mistake</h3>

<p>Allowlisting is materially stronger than domain denylisting because it reduces the number of code suppliers permitted to execute at all — attacking S1 of the aggregation pipeline rather than filtering its output. A tightly managed device should carry no general consumer store, no sideloading, no unapproved browser, no advertising-funded applications, no arbitrary keyboards, no unapproved VPN or DNS applications, no personal cloud accounts and no unaudited accessibility services.</p>

<div class="ckp-callout warn">
  <strong>"Approved" does not mean "clean"</strong>
  <p>An allowlisted application may still embed analytics, crash reporting, attribution and engagement SDKs; may authenticate a stable account identity; and may operate a backend that shares onward. Allowlisting by package name alone achieves far less than it appears to. The allowlist must bind to an analysed artefact — package, version <em>and</em> signing certificate.</p>
</div>

<p>The browser is a particularly dangerous exception: one approved package that executes code from millions of origins. If unrestricted web access is permitted, the software environment is not closed and the allowlist is substantially weakened.</p>

<h3>Fleet uniformity, not identifier randomisation</h3>

<p>A recurring proposal is to defeat probabilistic fingerprinting by randomising device attributes — rotating models, spoofing screen geometry, perturbing locale. This is counterproductive and should be rejected. The reasoning is standard anti-fingerprinting theory, and worth stating explicitly because the intuition runs the other way.</p>

<p>A fingerprint's power derives from entropy: how many devices share the observed attribute vector. Randomisation does not reduce entropy; it usually increases it. Improbable combinations are distinctive — a flagship model reporting an implausible display density occupies a <em>smaller</em> equivalence class than an unmodified device. Instability is itself a signal: an attribute vector that changes between sessions while the instance identifier and address remain constant announces that anti-fingerprinting is in use. And attributes are mutually constrained, so violations are detectable without special effort.</p>

<div class="ckp-pull">
  <p>The objective is not to be unpredictable. It is to be indistinguishable — to maximise the anonymity set by making every managed device present an identical, unremarkable and internally consistent configuration.</p>
  <cite>Uniformity over randomisation</cite>
</div>

<p>Same hardware family, same platform version, same patch level, same locale policy where operationally acceptable, same application set, same agent version. Within the fleet, devices become mutually indistinguishable on attributes alone. This trade is usually correct — but it <em>is</em> a trade, and §7 examines what it costs.</p>

<h3>Forking Android: the strongest control, and the wrong first move</h3>

<p>A controlled build genuinely enables things no enterprise API can: removal of selected platform services, elimination of advertising-identifier support at the platform level, per-application network allowlists enforced below application space, and — the only real answer to the structural problem in §2 — denying a library access to an API independently of the host application's grant.</p>

<p>The case for these capabilities is real. The case against doing it first is stronger. A custom build creates a permanent commitment: monthly platform patches, kernel and firmware vulnerabilities, baseband and vendor driver updates, verified-boot integration, compatibility testing, emergency patch capability, secure update infrastructure, rollback protection, and long-term hardware vendor support — for the life of every deployed device.</p>

<div class="ckp-callout bad">
  <strong>The decisive argument</strong>
  <p>A privacy-improved build that is three months behind on exploitable vulnerabilities provides better advertising privacy and worse overall security. For defence users — precisely the population an adversary is most motivated to exploit directly — that is an unacceptable trade. The commercial-tracking problem does not justify increasing exposure to direct compromise.</p>
</div>

<p>There is a second, less obvious cost. An operating system that removes the vendor's platform services also removes the management plane that depends on them. The Android Management API and its on-device policy component are unavailable in that configuration, so an organisation choosing this route must budget for replacing the entire management, application distribution, update and attestation stack — not merely for maintaining a kernel.</p>

<p>Begin instead with a narrow controlled reference platform, measure which residual leakage genuinely cannot be controlled through supported mechanisms, and let that measurement justify platform modification — ideally through an OEM partnership rather than an independent fork.</p>

<h3>Sandboxing: three things that are not what they sound like</h3>

<p><strong>Android already sandboxes applications.</strong> Every application gets a distinct UID and process, with kernel, filesystem and mandatory access controls enforcing separation. This protects applications from each other. It does not protect the user from code embedded inside an application they installed, because that code shares the UID and the grants.</p>

<p><strong>Work profiles isolate less than advertised.</strong> A work profile creates a separate managed profile with its own application instances and data, and because it is a distinct Android user, profile-scoped values — including the advertising identifier — differ from the personal profile. That property is often presented as decisive. It is not. An application in the work profile still observes its own instance identifier, its authenticated account, the egress address, device model and platform version, display geometry, locale and time zone, its own events, publisher-supplied attributes, and any granted sensor. A work profile changes profile-scoped identifiers; it is not a synthetic-device layer and cannot present fabricated attributes to an embedded library. On a fully managed device it is largely redundant.</p>

<p><strong>A general compatibility sandbox is an operating system in disguise.</strong> Running arbitrary unmodified applications requires mediating package management, binder services, location, telephony, identifier providers, platform services, notifications, camera and microphone, Bluetooth and Wi-Fi, files and content providers, keystore, accounts, push messaging, purchase, integrity and attestation, the web view, native code, intents and background scheduling. Simultaneously, applications increasingly verify their environment: platform integrity services report whether an interaction originates from an unmodified application, a recognised installation source and a certified device. A virtualised or repackaged environment fails those checks — and failing them breaks exactly the financial, identity and messaging applications an organisation most needs to work.</p>

<p>Application rewriting has the same problem from the other direction: signatures invalidated, signature-level permissions broken, backend verification rejecting the artefact, every update requiring repeat work, native code bypassing managed-language hooks, and no vendor support for the result. Rewriting is a laboratory technique, not a production mechanism.</p>

<p>What <em>is</em> achievable is a set of bounded sandboxes for specific content classes: open untrusted links in a managed browser, render documents in a hardened viewer, display remote web content without persistent storage, proxy map services through an enterprise endpoint, supply a controlled keyboard. Each has a defined interface and a testable boundary. "Run every commercial Android application inside our privacy container" does not.</p>

<h3>DNSSEC: neither a privacy feature nor redundant</h3>

<p>DNSSEC attracts two opposite errors — marketing it as a privacy control, and dismissing it as redundant once encrypted transport is in place. The second is the more damaging, because it discards a cheap control on a false premise.</p>

<div class="ckp-diagram">
  <div class="ckp-diagram-head">
    <span class="ckp-diagram-label">Fig. 5 — Two different segments, two different guarantees</span>
    <button class="ckp-copy">Copy</button>
  </div>
<pre><code>handset ===[ WireGuard / DoT / DoH ]===&gt; RESOLVER ----&gt; authoritative
        \________________________/                \________________/

         protected by encryption:                  NOT protected by
         confidentiality + integrity               the tunnel at all.
         of this hop only                          DNSSEC protects data
                                                   authenticity here.</code></pre>
</div>

<p>The recursive resolver is the policy decision point. Its answers determine which addresses the egress gateway associates with an approved hostname. If that resolver can be fed forged data from the authoritative side — by cache poisoning or on-path tampering — then an approved hostname can be bound to an attacker-controlled address, and the tunnel will faithfully carry traffic there. Encrypting the handset-to-resolver hop does nothing about this, because the attack is on the other side of the resolver.</p>

<p>What DNSSEC does not do: it does not encrypt DNS; it does not indicate that a domain is safe (a tracking company can sign its zone correctly, and validation will then accurately confirm the tracker's answer is authentic — <em>secure</em> is not <em>benign</em>); it does not authenticate the server behind the address; and it does not cover unsigned zones.</p>

<div class="ckp-callout key">
  <strong>Verdict</strong>
  <p>Enable validation at the recursive resolver and sign your own externally published zones — enrolment, policy retrieval, gateway discovery, update metadata, certificate status. Treat it as resolver-integrity protection that makes the policy decision point harder to deceive, and never market it as an anti-tracking feature. The operational cost is mostly monitoring, principally accurate time: DNSSEC signatures have validity periods, and clock drift presents as unexplained outage.</p>
</div>

<h3>Summary</h3>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead><tr><th>Control</th><th>Removes</th><th>Principal residual</th></tr></thead>
<tbody>
<tr><td><span class="term">Protective DNS</span></td><td>Resolution of known dedicated tracking hosts.</td><td>No payload visibility; blind to first-party relay; reactive.</td></tr>
<tr><td><span class="term">Destination policy</span></td><td>Direct-address egress and unauthorised routes.</td><td>Shared infrastructure; endpoint rotation.</td></tr>
<tr><td><span class="term">Always-on lockdown tunnel</span></td><td>Unobserved egress paths; resolver bypass.</td><td>No payload visibility; exemptions void the claim.</td></tr>
<tr><td><span class="term">TLS interception</span></td><td>Some payload opacity.</td><td>Pinning defeats it; centralises catastrophic risk. Lab only.</td></tr>
<tr><td><span class="term">Device management</span></td><td>Configuration drift; user modification.</td><td>Does not determine backend behaviour.</td></tr>
<tr><td><span class="term">Application allowlisting</span></td><td>Untrusted code suppliers.</td><td>Approved applications still carry SDKs and accounts.</td></tr>
<tr><td><span class="term">Admission analysis</span></td><td>Unjustified SDKs and destinations, per version.</td><td>Onward transfer remains unprovable from the device.</td></tr>
<tr><td><span class="term">Permission policy</span></td><td>Direct sensor and location access.</td><td>Publisher-supplied and address-derived data survive.</td></tr>
<tr><td><span class="term">Identifier suppression</span></td><td>The standard cross-application join key.</td><td>Instance IDs, accounts, graphs, history survive.</td></tr>
<tr><td><span class="term">Fleet uniformity</span></td><td>Attribute distinctiveness within the fleet.</td><td>Makes the fleet as a class more recognisable.</td></tr>
<tr><td><span class="term">DNSSEC validation</span></td><td>Forged resolver answers for signed zones.</td><td>No privacy effect; unsigned zones unprotected.</td></tr>
<tr><td><span class="term">Custom operating system</span></td><td>Platform-level capability limits.</td><td>Patch, hardware and management-plane obligations.</td></tr>
<tr><td><span class="term">Personal-device prohibition</span></td><td>The largest single unmanaged source.</td><td>Requires physical and cultural enforcement.</td></tr>
</tbody>
</table>
</div>

<p>Protective DNS is useful but shallow. Device management is essential but not sufficient. Application allowlisting is a strong foundation that requires continuous auditing to mean anything. A custom operating system is the highest-control option and is only justified once an organisation can demonstrably maintain it more securely and more quickly than the original vendor. The defensible product is none of these individually — it is an anti-telemetry assurance system composed of all of them, whose principal output is evidence.</p>
</section>

<div class="ckp-sep">Architecture</div>

<!-- ─── SECTION 6 ─────────────────────────────────────────── -->
<section id="sec-arch">
<h2>6. The Architecture</h2>

<p>Seven principles govern the design, and each is testable.</p>

<div class="ckp-findings">
  <div class="ckp-finding">
    <span class="f-id">P1</span>
    <h4>Default deny at every layer that can express it</h4>
    <p>Applications, permissions, destinations and identifiers are permitted by exception. A denylist is a supplementary intelligence feed, never the enforcement model.</p>
  </div>
  <div class="ckp-finding">
    <span class="f-id">P2</span>
    <h4>Fail closed, with a defined restricted fallback</h4>
    <p>Loss of policy control places a device in a restricted state. It never silently resumes unmediated internet access.</p>
  </div>
  <div class="ckp-finding">
    <span class="f-id">P3</span>
    <h4>Bind approval to artefacts, not names</h4>
    <p>An approval refers to a package, a version and a signing certificate. Every update is a new artefact requiring reassessment.</p>
  </div>
  <div class="ckp-finding">
    <span class="f-id">P4</span>
    <h4>Evidence is the product</h4>
    <p>Every enforcement decision emits a signed, structured record sufficient for a third party to reconstruct what was permitted and why.</p>
  </div>
  <div class="ckp-finding">
    <span class="f-id">P5</span>
    <h4>Minimise what the platform itself collects</h4>
    <p>The system must not become the surveillance asset it exists to prevent. Data minimisation is a functional requirement with acceptance criteria.</p>
  </div>
  <div class="ckp-finding">
    <span class="f-id">P6</span>
    <h4>Prefer supported platform mechanisms</h4>
    <p>Every divergence from documented enterprise capability is a maintenance liability that must be justified by a measured, otherwise-uncontrollable leak.</p>
  </div>
  <div class="ckp-finding">
    <span class="f-id">P7</span>
    <h4>Uniformity over randomisation</h4>
    <p>Managed devices converge on an identical configuration; the anonymity set is the defence.</p>
  </div>
</div>

<h3>System overview</h3>

<div class="ckp-diagram">
  <div class="ckp-diagram-head">
    <span class="ckp-diagram-label">Fig. 6 — Reference architecture</span>
    <button class="ckp-copy">Copy</button>
  </div>
<pre><code>CUSTOMER CONTROL PLANE
+--------------------------+      +-------------------------------+
| Existing EMM / MDM       |&lt;----&gt;| Policy + Evidence Console     |
| (Android Enterprise)     |      | tenants, approvals, evidence  |
+------------+-------------+      +---------------+---------------+
             |  device policy                     |  signed policy
             v                                    v
+=======================================================================+
| MANAGED ANDROID DEVICE   (fully managed, work-only, locked boot)      |
|                                                                       |
|  Approved applications only ........ exact version + signing cert     |
|  Runtime permissions ............... explicit grant / deny            |
|  Advertising identifier ............ suppressed                       |
|  Enforcement agent ................. VpnService + WireGuard tunnel    |
|                                       signed local policy cache       |
|                                       health + fail-closed logic      |
|                                       UID / flow attribution          |
|  Always-on VPN + lockdown .......... no exclusions by default         |
+=======================================+===============================+
                                        |
                     mutually authenticated encrypted tunnel
                              (IPv4 and IPv6)
                                        v
+=======================================================================+
| POLICY ENFORCEMENT GATEWAY   (customer-hosted / sovereign / regional) |
|                                                                       |
|  tunnel termination -&gt; peer identity -&gt; tenant isolation              |
|  nftables destination policy   |   forced internal DNS                |
|  direct-IP denial              |   per-application allowlists         |
|  rate limits + anomaly         |   flow evidence emission             |
+------------------+------------------------------+-------------------+
                   |                              |
                   v                              v
     +------------------------+     +-----------------------------+
     |  PROTECTIVE DNS        |     |  INTERNET EGRESS            |
     |  dnsdist ingress       |     |  approved destinations only |
     |  Unbound recursion     |     |  tenant egress pool         |
     |  DNSSEC + RPZ policy   |     +-----------------------------+
     +------------------------+
                   |
                   v
     +--------------------------------------------------------+
     |  EVIDENCE PIPELINE -&gt; customer console / SIEM           |
     |  minimal fields, pseudonymous, signed, retention-bound  |
     +--------------------------------------------------------+

- - - - - - - - LIMIT OF DEVICE-SIDE ENFORCEMENT - - - - - - - -

+--------------------------------------------------------------+
|  APPLICATION ASSURANCE LABORATORY   (offline, isolated)       |
|  APK -&gt; static analysis -&gt; instrumented execution -&gt;          |
|  SDK inventory -&gt; destination inventory -&gt; risk decision -&gt;   |
|  version-bound approval + generated gateway policy            |
+--------------------------------------------------------------+</code></pre>
</div>

<h3>The device baseline</h3>

<p>One or two device families only. The selection criterion is a <em>contractually stated</em> security-support lifetime, not a marketing claim. Locked bootloader, verified boot, hardware-backed key storage, file-based encryption. Fleet-wide minimum platform version enforced by policy, with patch level monitored as a compliance condition rather than merely reported. Company-owned, fully managed, work-only enrolment with no personal profile in the higher tiers.</p>

<div class="ckp-callout warn">
  <strong>Hardware selection is a security decision, not a procurement one</strong>
  <p>The single largest determinant of resistance to direct compromise is how quickly the manufacturer ships firmware and baseband fixes, and for how many years. A device family with a long, contractual support window contributes more to protecting this population than any feature in this architecture. Narrowing the supported hardware list is therefore a feature, and resisting pressure to broaden it is a security control.</p>
</div>

<h3>Two enforcement sources, deliberately</h3>

<p>Platform network logging can record resolutions and connections attributed to an application — and the platform documentation itself warns that applications may bypass some system networking interfaces, recommending network-layer monitoring where complete visibility is required. That warning is the architectural justification for combining on-device attribution with independent gateway observation: the device supplies attribution the gateway cannot derive, and the gateway supplies ground truth the device can be deceived about.</p>

<h3>The enforcement agent</h3>

<p>The agent establishes and maintains a full IPv4 and IPv6 tunnel via <code>VpnService</code>, using the official WireGuard Android tunnel library rather than a reimplementation [<a href="#ref-WG">WireGuard</a>]. WireGuard is the engineering default for a deliberately small implementation surface, a fixed modern cryptographic suite with no negotiation, efficient roaming, low handshake cost and mature kernel support on the gateway side. IKEv2/IPsec via strongSwan is the interoperability option where a customer requires standards-based interoperation, EAP-TLS, RADIUS integration or smart-card keys — not the default, and not built in a first release unless a pilot demands it.</p>

<div class="ckp-callout">
  <strong>Do not implement the cryptography</strong>
  <p>Fork as little as possible. Pin exact upstream versions, carry a minimal patch set, maintain a documented synchronisation process against upstream advisories. The defensible proprietary value sits <em>above</em> the tunnel: enrolment, policy, gateway selection, attribution, evidence generation, failure behaviour and fleet observability. It does not sit in a hand-rolled handshake.</p>
</div>

<p>Beyond the tunnel the agent must continuously verify that it remains the always-on provider, that lockdown is active, that full default routes for both address families are installed, that the intended resolver is assigned, that no application is excluded, that the gateway is reachable, and that local policy is current and signed. It maintains the UID-to-package-and-certificate mapping that makes gateway flow records resolvable to an application. And it holds a signed, versioned policy snapshot so that approved traffic continues during short control-plane outages while unknown applications remain blocked and rollback is prevented.</p>

<h4>Three edge cases that need decisions, not discovery</h4>

<ul class="ckp-hier">
  <li><strong>IPv6</strong> — carry it end to end with per-device allocation and firewall equivalence, or install an explicit unreachable route and block native IPv6 entirely. Silence on this point is the most common cause of a failed escape test.</li>
  <li><strong>Captive portals</strong> — lockdown and captive portals conflict directly. Defence tiers do not support them and permit only preapproved enterprise Wi-Fi or cellular. Government tiers may allow a tightly constrained, time-boxed exception covering only portal detection and the portal endpoint. Enterprise tiers may permit user bypass, which is not an assurance configuration.</li>
  <li><strong>UDP-restricted networks</strong> — fail closed for defence. Any TCP or TLS-compatible fallback must be explicitly designed, documented and tested, not an opportunistic obfuscation layer, which adds attack surface, audit burden and a distinguishing signature.</li>
</ul>

<h3>The gateway</h3>

<div class="ckp-diagram">
  <div class="ckp-diagram-head">
    <span class="ckp-diagram-label">Fig. 7 — Gateway processing order</span>
    <button class="ckp-copy">Copy</button>
  </div>
<pre><code>tunnel ingress
  |
  +-- validate source tunnel address against authorised peer identity
  +-- resolve tenant; enforce tenant routing isolation
  +-- force DNS to internal resolver; deny all other resolution paths
  +-- deny private and reserved destinations unless authorised
  +-- apply application-to-destination policy (mode-dependent)
  +-- rate limit; detect anomaly; emit flow evidence
  +-- source NAT via tenant egress pool
  |
  v
approved internet destinations</code></pre>
</div>

<p>Three enforcement modes. <strong>Monitor</strong> permits and classifies, used during initial deployment to build the destination inventory — never an end state. <strong>Tracker blocking</strong> denies known advertising, attribution, analytics and location-broker destinations, appropriate for enterprise and bounded by every limitation in §5. <strong>Strict allowlist</strong> permits only approved application-to-destination relationships and is the default recommendation for government and defence: a destination being legitimate is not sufficient, and the question is whether <em>this application</em> has an approved reason to contact it.</p>

<p>Where an application sends both operational and telemetric data to the same first-party hostname, the gateway cannot separate them inside TLS. There are exactly four honest responses, and the platform must record which was chosen: approve the endpoint on the basis of a documented assessment and record the accepted residual; reject the application; require a telemetry-suppressed enterprise build; or bind the publisher contractually. There is no fifth option in which individual fields are stripped from opaque, pinned TLS, and a product should not imply one exists.</p>

<h3>Protective DNS stack</h3>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead><tr><th>Layer</th><th>Component</th><th>Why</th></tr></thead>
<tbody>
<tr><td><span class="term">Ingress</span></td><td>dnsdist</td><td>DNS-aware load balancing, access control, rate limiting, backend health checks, abuse controls, metrics, structured query telemetry.</td></tr>
<tr><td><span class="term">Recursion</span></td><td>Unbound</td><td>Validating recursive caching resolver with DNSSEC, response policy zones, per-tenant views, QNAME minimisation, permissive licence.</td></tr>
<tr><td><span class="term">Telemetry</span></td><td>dnstap</td><td>Structured resolver events without log scraping.</td></tr>
<tr><td><span class="term">Optional</span></td><td>CoreDNS</td><td>Internal service discovery or a bespoke policy plugin — <em>not</em> the principal recursive security resolver.</td></tr>
</tbody>
</table>
</div>

<div class="ckp-callout">
  <strong>Why not CoreDNS as the resolver</strong>
  <p>CoreDNS is an excellent plugin-oriented DNS server and the natural choice for cluster service discovery. It is not a validating recursive resolver in the sense required here. The enforcement point needs full recursion with native DNSSEC validation, RPZ application, per-tenant views and mature cache semantics. Choosing a general DNS toolkit as the security resolver means implementing resolver security properties as plugins — avoidable work in a component that must be audited.</p>
</div>

<p>Resolution stays inside the tunnel, reaching a resolver address reachable only through it. That is simpler and more enforceable than configuring the handset to send DNS over TLS independently to the public internet; the tunnel already provides confidentiality and integrity for that hop.</p>

<p>Policy evaluation must be deterministic and ordered: emergency global deny, customer explicit deny, application-specific deny, customer explicit allow, application-specific allow, high-confidence tracker rule, customer category rule, then default posture. And the resolver must evaluate <strong>CNAME chains</strong> in full — a publisher may present a first-party-looking hostname that delegates to a tracking provider, and logging only the initially queried name misses this class entirely.</p>

<h3>Application assurance: the actual differentiator</h3>

<p>Tunnels, resolvers and management consoles are commodities. Version-bound knowledge of what each approved application actually does is not.</p>

<p>Static analysis extracts and records, per artefact: package and version; signing certificate; declared permissions including the advertising-identifier permission whether declared directly or merged from a library manifest; services, receivers and providers; embedded SDKs and native libraries; location and nearby-device permissions; accessibility components; VPN or custom resolver functionality; hard-coded hostnames and literal addresses; pinning configuration; and dynamic-code-loading indicators.</p>

<p>Instrumented execution then runs the artefact on real devices under scripted scenarios — first launch, before and after consent, authenticated login, background operation, location change, advertising-identifier deletion, network transition, a representative business action, reboot, extended idle, and receipt of remote configuration — recording resolutions, destinations, TLS server names, permission use, identifier access, and the delta against the previously approved version.</p>

<div class="ckp-callout key">
  <strong>Test the blocked case explicitly</strong>
  <p>An application's behaviour when its telemetry endpoint is unreachable is a first-class finding. Applications that retry aggressively, fall back to a literal address, switch to an alternate resolver, or degrade core functionality must be identified before deployment, not after a fleet-wide outage. This test also surfaces evasion behaviour that no static analysis will reveal.</p>
</div>

<div class="ckp-diagram">
  <div class="ckp-diagram-head">
    <span class="ckp-diagram-label">Fig. 8 — Admission decision record</span>
    <button class="ckp-copy">Copy</button>
  </div>
<pre><code>application        Field Maps
version            5.4.2       signing cert: &lt;fingerprint&gt; (approved)
embedded SDKs      7           advertising: 0    analytics: 1
AD_ID permission   not declared   (merged libraries: none)
location           required while in use; background prohibited
destinations       9 observed  -&gt;  6 approved, 3 denied
shared endpoints   1 (operational + diagnostics, exception recorded)
risk rating        moderate
status             approved with restrictions
gateway policy     generated, signed, bound to version + certificate
reassessment       30 days, or on any new release</code></pre>
</div>

<p>Where an application is operationally necessary but commercially instrumented, the best obtainable result is a publisher-supplied enterprise build: advertising SDKs removed, analytics disabled, no advertising-identifier access, no unnecessary location access, a customer-controlled telemetry endpoint, documented retention and a contractual prohibition on onward sale. This is less technically interesting than a sandbox and substantially more reliable — and negotiating leverage for it is one of the real benefits of running a serious admission programme.</p>

<h3>Assurance tiers</h3>

<p>One architecture, three configurations. The controls are identical; strictness, catalogue breadth and failure behaviour differ.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead><tr><th>Control</th><th>Enterprise</th><th>Government</th><th>Defence</th></tr></thead>
<tbody>
<tr><td><span class="term">Hardware list</span></td><td>Broad</td><td>Narrow</td><td>Single family</td></tr>
<tr><td><span class="term">App catalogue</span></td><td>Approved list</td><td>Exact-version approval</td><td>Minimal, no ad-funded apps</td></tr>
<tr><td><span class="term">Destination policy</span></td><td>Tracker blocking</td><td>Per-app allowlist</td><td>Strict per-app allowlist</td></tr>
<tr><td><span class="term">Default permission posture</span></td><td>Prompt</td><td>Deny</td><td>Deny</td></tr>
<tr><td><span class="term">Background location</span></td><td>By exception</td><td>Prohibited</td><td>Prohibited</td></tr>
<tr><td><span class="term">Browser</span></td><td>Managed</td><td>Restricted destinations</td><td>None, or isolated only</td></tr>
<tr><td><span class="term">Captive portals</span></td><td>Permitted</td><td>Constrained exception</td><td>Not supported</td></tr>
<tr><td><span class="term">Failure behaviour</span></td><td>Restricted fail-safe</td><td>Restricted fail-safe</td><td>Fail closed</td></tr>
<tr><td><span class="term">Egress</span></td><td>Vendor regional</td><td>Sovereign</td><td>Customer-hosted</td></tr>
<tr><td><span class="term">Reassessment</span></td><td>Quarterly</td><td>Monthly or per release</td><td>Per release, mandatory</td></tr>
<tr><td><span class="term">Personal devices</span></td><td>Policy guidance</td><td>Policy prohibition</td><td>Physical prohibition</td></tr>
</tbody>
</table>
</div>

<div class="ckp-callout warn">
  <strong>Fail-closed has a safety dimension</strong>
  <p>A handset that refuses all networking when the tunnel is unavailable may be the device a user needs in an emergency. Define the restricted fail-safe state precisely — typically device management, time synchronisation, certificate status and defined recovery services only — and confirm that emergency calling, which does not traverse the tunnel, is unaffected and has been tested. This is a safety requirement with a named owner, not a configuration footnote.</p>
</div>

<h4>One implementation detail worth singling out</h4>

<p>A Bloom filter is sometimes proposed for in-path destination matching because it is compact and fast. It has <em>false positives by construction</em>. In a fail-closed architecture a false positive is a silently dropped connection to a legitimate destination, occurring non-deterministically, on some devices and not others, with no record of why. That is close to the worst possible failure mode for an assurance product. Use an exact structure for the decision — a longest-prefix-match radix trie for addresses, exact-match or suffix-trie for domains, compiled into gateway rule sets with atomic replacement. A probabilistic filter is acceptable only as a negative prefilter, where a positive result is always confirmed against the exact structure before any packet is affected.</p>
</section>

<div class="ckp-sep">What This Costs You</div>

<!-- ─── SECTION 7 ─────────────────────────────────────────── -->
<section id="sec-backfire">
<h2>7. Two Risks the Architecture Creates</h2>

<p>Most treatments of this subject stop at the architecture. That is an incomplete analysis, because the design introduces two exposures that did not exist before it. Omitting them would make every other claim here less credible.</p>

<h3>The uniform problem</h3>

<p>The design concentrates a defined population onto uniform hardware, a uniform application set, a distinctive tunnel protocol and a bounded set of egress addresses. Each choice is individually correct. Collectively they produce a recognisable class signature.</p>

<ul class="ckp-hier">
  <li><strong>Egress address space</strong> — traffic emerges from a limited pool of addresses with registration records, autonomous-system assignments, reverse DNS and observable behaviour. An adversary who enumerates them, which is inexpensive, can thereafter classify any session originating from them — and can also detect the pool's growth, geography and diurnal activity.</li>
  <li><strong>Protocol signature</strong> — WireGuard has a recognisable handshake structure. An observer at a network position sees that a device is tunnelling, and frequently which protocol.</li>
  <li><strong>Configuration uniformity</strong> — the property that defeats fingerprinting within the fleet makes the fleet distinguishable from the general population: an unusual application set, an unusual patch discipline, an unusual absence of consumer services.</li>
  <li><strong>Behavioural absence</strong> — a device that contacts no advertising infrastructure at all, in a population where essentially every device does, is itself anomalous.</li>
</ul>

<div class="ckp-pull">
  <p>It conceals identity while advertising affiliation. An adversary who cannot determine whose handset this is, but can reliably determine that it is a government one, has still acquired targeting-relevant information.</p>
  <cite>The uniform problem</cite>
</div>

<p>The adversary's question is not always "who is this?" Frequently it is "which of these devices is worth attention?" In a denied or contested environment, carrying a device that is <em>visibly</em> protected may be worse than carrying an unremarkable one.</p>

<p>The mitigations manage rather than eliminate the effect. Enlarge the egress pool and use address space that does not identify the customer in registration data or reverse DNS. Avoid organisation-identifying gateway hostnames, certificate subject fields and service banners. Prefer commodity hosting and common transport ports where doing so does not weaken enforcement. Treat operational-mode selection as doctrine — in the highest-threat environments the correct control is often not a better tunnel but no device, or a device with radios disabled. And state the effect explicitly to the customer: a buyer who understands it can select deployment patterns accordingly, whereas a buyer who discovers it during a red-team exercise will not renew.</p>

<div class="ckp-callout key">
  <strong>This is not a reason to abandon the architecture</strong>
  <p>The alternative — an unmanaged handset emitting identifiable telemetry into the commercial ecosystem — is materially worse, because it discloses both identity <em>and</em> affiliation. The point is that "protected" and "invisible" are different properties, that this architecture delivers the first, and that a vendor claiming the second is claiming something its own design contradicts.</p>
</div>

<h3>The evidence system is a surveillance system</h3>

<p>A platform that records which applications every managed device contacted, and when, has constructed a high-value mobility and behaviour dataset for a population of specific interest to hostile services. This is the same asset class the programme exists to deny an adversary, differing only in custody.</p>

<p>It must therefore be engineered under minimisation constraints tested like any other requirement. Analysts see device pseudonyms; person-to-device resolution requires a separate privileged role and dual authorisation, and every resolution is itself audited. Retention is asymmetric — permitted DNS measured in days, denied DNS and flow metadata in weeks, incidents case-based — with short defaults configurable upward only with justification. No payload collection in production. Per-tenant encryption keys, customer-held where the deployment model permits. Evidence-store queries logged as security events. An immutable, signed, independently verifiable audit trail. Customer-initiated deletion that is demonstrable. And no secondary use of customer telemetry for product analytics, enrichment or threat-intelligence resale — a contractual warranty, not a privacy-policy sentence.</p>

<div class="ckp-callout bad">
  <strong>An anti-tracking product that builds a tracking database has failed</strong>
  <p>"Retain everything indefinitely" is not a security feature; it is an unpriced liability and, for a defence customer, a procurement disqualifier. It also conflicts with management-platform permissible-use terms that prohibit solutions built for monitoring or fingerprinting. Minimisation is simultaneously an ethical requirement, a security requirement and a commercial prerequisite.</p>
</div>

<p>The same reasoning drives deployment model as a first-class product decision rather than a late accommodation. Vendor-hosted regional deployment is appropriate for enterprise, and the vendor holds fleet metadata — say so plainly. Sovereign deployment places the control plane and gateways in a specified jurisdiction with customer-held keys. Customer-hosted deployment, where the customer operates gateways, resolvers and evidence store, is the correct default for defence. Disconnected operation is required for air-gapped environments and is the hardest to support: scope it deliberately or exclude it.</p>
</section>

<div class="ckp-sep">Honesty as Engineering</div>

<!-- ─── SECTION 8 ─────────────────────────────────────────── -->
<section id="sec-claims">
<h2>8. What You May Honestly Claim</h2>

<p>Government and defence buyers run technical evaluations. An overclaim that fails in evaluation does not merely lose the feature — it transfers the burden of proof onto every other statement the vendor has made. The table below maps claims that will not survive testing onto the strongest defensible equivalent.</p>

<div class="ckp-versus">
  <div class="ckp-versus-head">
    <div class="vs-bad">Do not claim</div>
    <div class="vs-good">Claim instead</div>
  </div>
  <div class="ckp-versus-row">
    <div class="vs-bad">"Users cannot be tracked."</div>
    <div class="vs-good">"Managed devices are prevented from contacting unapproved destinations, and every enforcement decision is recorded and exportable."</div>
  </div>
  <div class="ckp-versus-row">
    <div class="vs-bad">"We remove all tracking identifiers."</div>
    <div class="vs-good">"Advertising identifiers are suppressed by policy; application-instance and account identifiers are inventoried per application and assessed at admission."</div>
  </div>
  <div class="ckp-versus-row">
    <div class="vs-bad">"Anonymous."</div>
    <div class="vs-good">"Pseudonymous within the platform; the device remains identifiable to the cellular network and to services the user authenticates to."</div>
  </div>
  <div class="ckp-versus-row">
    <div class="vs-bad">"We block all trackers."</div>
    <div class="vs-good">"Known tracking destinations are denied; in strict mode only approved application-to-destination relationships are permitted; first-party onward transfer is addressed by application admission, not network filtering."</div>
  </div>
  <div class="ckp-versus-row">
    <div class="vs-bad">"Our VPN hides your location."</div>
    <div class="vs-good">"The tunnel conceals traffic destinations from local networks and replaces the visible network address; it does not conceal position from the cellular network."</div>
  </div>
  <div class="ckp-versus-row">
    <div class="vs-bad">"Certified" or "compliant" before evaluation completes.</div>
    <div class="vs-good">"Designed against [scheme]; evaluation in progress" — or say nothing.</div>
  </div>
  <div class="ckp-versus-row">
    <div class="vs-bad">"AI-powered detection" with no published evaluation.</div>
    <div class="vs-good">State the method, the data, the evaluation and the error rates, or omit the claim.</div>
  </div>
  <div class="ckp-versus-row">
    <div class="vs-bad">"Zero telemetry."</div>
    <div class="vs-good">"The platform collects the enumerated minimal fields, retained for the stated periods, under the stated access controls."</div>
  </div>
</div>

<h3>What remains unmitigated</h3>

<p>After correct and complete implementation, the following survive. They should be carried as a register, reviewed and accepted explicitly rather than discovered.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead><tr><th>Risk</th><th>Why it survives</th><th>Available response</th></tr></thead>
<tbody>
<tr><td><span class="term">Cellular network location</span></td><td>The network must know which cells serve the device to deliver service.</td><td>Operational: radio discipline, device-free areas. No handset control.</td></tr>
<tr><td><span class="term">Baseband compromise</span></td><td>Executes below the OS, outside the agent's reach.</td><td>Narrow hardware list, contractual patch commitments, retirement policy.</td></tr>
<tr><td><span class="term">First-party onward transfer</span></td><td>Occurs after data has lawfully left by an approved route.</td><td>Admission, enterprise builds, contract, downstream audit. Not provable from the handset.</td></tr>
<tr><td><span class="term">Account correlation</span></td><td>A login identifies a user across devices and resets by design.</td><td>Account separation policy; not eliminable while the service is used.</td></tr>
<tr><td><span class="term">Historical data</span></td><td>Profiles accumulated before deployment are not retracted.</td><td>None technical. Assume a baseline profile exists.</td></tr>
<tr><td><span class="term">Probabilistic fingerprinting</span></td><td>Attribute vectors need no identifier and no permission.</td><td>Fleet uniformity reduces distinctiveness; does not remove the signal.</td></tr>
<tr><td><span class="term">Protected-class visibility</span></td><td>Created by uniformity, distinctive transport and bounded egress.</td><td>Egress pool design, naming hygiene, doctrine, explicit disclosure.</td></tr>
<tr><td><span class="term">Compromised approved app</span></td><td>An update may introduce new behaviour between assessments.</td><td>Version pinning, staged rollout, per-release reassessment, drift alerting.</td></tr>
<tr><td><span class="term">Unmanaged personal devices</span></td><td>Outside the boundary entirely.</td><td>Physical and policy prohibition. Organisational, not technical.</td></tr>
<tr><td><span class="term">Metadata concentration</span></td><td>The architecture funnels a population's metadata through common infrastructure.</td><td>Customer-hosted deployment, customer keys, minimisation, short retention.</td></tr>
<tr><td><span class="term">Vendor insider access</span></td><td>Personnel with production access could observe fleet activity.</td><td>Role separation, dual authorisation, search auditing, customer hosting.</td></tr>
<tr><td><span class="term">Supply-chain compromise</span></td><td>Of the agent, gateway images, or any dependency.</td><td>Reproducible builds, artefact signing, SBOM, independent review.</td></tr>
</tbody>
</table>
</div>

<h3>Open questions</h3>

<p>In the interest of an honest record, several things could not be resolved from primary sources and should be established independently by any adopting organisation. A paper claiming no open questions in this domain is not being candid.</p>

<ul class="ckp-hier">
  <li><strong>Contractual security-support lifetimes</strong> for specific candidate device families. Marketing statements about support duration are not contractual commitments, and this is the single most important input to hardware selection. Obtain it in writing.</li>
  <li><strong>Current eligibility and permissible-use terms</strong> for the managed Android management interfaces, which change and which materially constrain the evidence model.</li>
  <li><strong>Completeness of on-device network logging</strong> across the selected hardware and platform versions. Measure it on the actual fleet rather than assuming.</li>
  <li><strong>Effectiveness of protocol-level classification</strong> against a determined observer — the §7 exposure, which should be measured before any statement about how visible the protected class is.</li>
  <li><strong>Behaviour of specific commercial applications</strong> under blocked endpoints, which is application-specific and must be measured per artefact.</li>
  <li><strong>The practical reach of foreign-transfer restrictions</strong> on actual data availability. The legal position is documented; the effect on adversary acquisition is not publicly measurable and should not be assumed favourable.</li>
  <li><strong>Long-term direction of platform advertising interfaces</strong> following the 2025 deprecation. The programme was withdrawn; what replaces it is not established, and no design should assume a favourable successor.</li>
</ul>
</section>

<div class="ckp-sep">Verification</div>

<!-- ─── SECTION 9 ─────────────────────────────────────────── -->
<section id="sec-verify">
<h2>9. Proving It</h2>

<p>No assurance claim should be made before the corresponding test passes, and every claim in customer-facing material should map to a named test with a recorded result. The classes below are the minimum, and each corresponds to a failure that would silently void the central claim.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead><tr><th>ID</th><th>Test</th><th>Pass criterion</th></tr></thead>
<tbody>
<tr class="group"><td colspan="3">E — Tunnel escape · claim: no packet leaves by an unauthorised route</td></tr>
<tr><td><code>E-01/02</code></td><td>Direct IPv4 / IPv6 to a literal address</td><td>No packet observed outside the tunnel. <strong>E-02 is the most frequently failed test in this set.</strong></td></tr>
<tr><td><code>E-03</code></td><td>Cellular/Wi-Fi transition during transfer</td><td>No unmediated packet in the transition window.</td></tr>
<tr><td><code>E-04</code></td><td>Reboot, pre-unlock window</td><td>No unmediated packet before policy applies.</td></tr>
<tr><td><code>E-05</code></td><td>Agent process termination</td><td>Platform lockdown holds; no egress.</td></tr>
<tr><td><code>E-06/07</code></td><td>Gateway / control-plane outage</td><td>Failure policy engages within the stated interval; signed cache governs; unknown apps stay blocked.</td></tr>
<tr><td><code>E-08</code></td><td>Agent package upgrade</td><td>No unmediated window during replacement.</td></tr>
<tr><td><code>E-09/10</code></td><td>Secondary Android user; tethering</td><td>Policy applies; tethered clients cannot bypass.</td></tr>
<tr><td><code>E-11/12</code></td><td>Captive portal; UDP-blocked network</td><td>Tier behaviour as defined; no silent fallback.</td></tr>
<tr><td><code>E-13</code></td><td>Emergency calling under fail-closed</td><td>Unaffected and demonstrated.</td></tr>

<tr class="group"><td colspan="3">D — Resolution bypass · claim: all name resolution is subject to policy</td></tr>
<tr><td><code>D-01..04</code></td><td>UDP/53, TCP/53, external DoT, public DoH</td><td>Denied and recorded.</td></tr>
<tr><td><code>D-05</code></td><td>Application-private DoH</td><td><strong>Result recorded honestly.</strong> If not distinguishable, destination allowlisting is documented as the operative control.</td></tr>
<tr><td><code>D-06..09</code></td><td>Hard-coded resolver; QUIC; native resolver; IPv6 bypass</td><td>Denied and recorded.</td></tr>
<tr><td><code>D-10/11</code></td><td>Cache persistence; CNAME chain to a denied provider</td><td>Stale answers bounded; full chain evaluated and query denied.</td></tr>

<tr class="group"><td colspan="3">P — Policy correctness</td></tr>
<tr><td><code>P-01/02</code></td><td>Same domain, two applications; shared CDN address</td><td>Both outcomes correct.</td></tr>
<tr><td><code>P-03..06</code></td><td>Rapid DNS change; wildcard scope; IDN homographs; DNS rebinding</td><td>TTL-aware expiry; positive and negative cases correct; no evasion; internal ranges unreachable.</td></tr>
<tr><td><code>P-07/08</code></td><td>DNSSEC bogus response; policy rollback attempt</td><td>Rejected with an operational event; older policy version refused.</td></tr>
<tr><td><code>P-09/10</code></td><td>Emergency deny propagation; tenant separation</td><td>Fleet-wide effect within the stated interval; no cross-tenant reachability at any layer.</td></tr>
<tr><td><code>P-11</code></td><td>Device and gateway clock skew</td><td>Behaviour defined and failures diagnosable, given DNSSEC validity windows.</td></tr>

<tr class="group"><td colspan="3">V — Evidence system · minimisation is a tested requirement</td></tr>
<tr><td><code>V-01/02</code></td><td>No payload capture; retention expiry</td><td>Verified by storage inspection, not configuration review.</td></tr>
<tr><td><code>V-03/04</code></td><td>Pseudonymisation; search auditing</td><td>Identity resolution requires separate role and dual authorisation; queries generate audit events.</td></tr>
<tr><td><code>V-05/06</code></td><td>Independent export validation; customer deletion</td><td>Signed export verifies without vendor tooling; deletion effective and demonstrable.</td></tr>
<tr><td><code>V-07</code></td><td>Protected-class classification exercise</td><td>Given only network-position observation, determine how reliably a device is identifiable as fleet. Result recorded.</td></tr>
</tbody>
</table>
</div>

<div class="ckp-callout key">
  <strong>Publish the failures</strong>
  <p>An organisation that publishes its test matrix — including which tests do not pass and what the compensating control is — is more credible than one publishing only capabilities. Sophisticated buyers assume undisclosed limitations exist. Disclosing them converts an unknown risk into a priced one.</p>
</div>

<h3>Where this leaves things</h3>

<p>The commercial advertising ecosystem produces, as a routine by-product of its ordinary operation, a dataset functionally equivalent to a surveillance product. Access to it requires money rather than capability. For organisations whose personnel have duty stations, routines, associations and deployment cycles, this converts a consumer privacy issue into an operational security problem — and the public record establishes that the conversion has already occurred in practice.</p>

<p>No single control addresses it. What works is the composition, operated as a system and evidenced as a system: controlled hardware with contractual support, fully managed enrolment, version-bound application admission with instrumented testing, explicit permission and identifier policy, fail-closed application-aware network egress, protective DNS with validated resolution, and a minimised, signed evidence trail that lets an auditor reconstruct every decision.</p>

<div class="ckp-pull">
  <p>A managed Android device operated under this architecture is not untrackable. It is a device on which the set of parties receiving data has been deliberately chosen, technically enforced, continuously re-verified, and recorded in a form a third party can audit.</p>
  <cite>The defensible claim</cite>
</div>

<p>That is a substantial and measurable improvement over the status quo, it is the most that current platform mechanisms support, and — for the buyers who will actually test it — it is worth considerably more than a claim that does not survive evaluation.</p>
</section>

<!-- ─── GLOSSARY ─────────────────────────────────────────── -->
<section id="sec-glossary">
<h2>Quick Reference Glossary</h2>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead><tr><th>Term</th><th>Meaning</th></tr></thead>
<tbody>
<tr><td><span class="term">Advertising identifier</span></td><td>Resettable, user-deletable device-and-user scoped identifier used as a cross-application join key.</td></tr>
<tr><td><span class="term">App Set ID</span></td><td>Identifier scoped to one developer's applications on one device; survives advertising-ID deletion.</td></tr>
<tr><td><span class="term">Bidstream</span></td><td>The flow of bid requests broadcast from exchanges to demand-side bidders during real-time auctions.</td></tr>
<tr><td><span class="term">CNAME cloaking</span></td><td>Presenting a first-party-looking hostname that delegates by CNAME to a third-party tracking provider.</td></tr>
<tr><td><span class="term">Data broker</span></td><td>An entity that makes available data about individuals it did not collect directly from them.</td></tr>
<tr><td><span class="term">Device owner</span></td><td>Management mode granting device-wide policy control on a company-owned device.</td></tr>
<tr><td><span class="term">DNSSEC</span></td><td>Cryptographic authentication of DNS data relative to a chain of trust. Not encryption, and not a safety signal.</td></tr>
<tr><td><span class="term">Identity graph</span></td><td>A vendor dataset linking pseudonymous identifiers to persons, households and devices.</td></tr>
<tr><td><span class="term">Lockdown (VPN)</span></td><td>Platform behaviour blocking connections that do not traverse the always-on tunnel.</td></tr>
<tr><td><span class="term">Pattern of life</span></td><td>An inferred model of a subject's routine locations, movements, associations and tempo.</td></tr>
<tr><td><span class="term">Protective DNS</span></td><td>A policy-enforcing resolver that can allow, block, redirect, sinkhole and record decisions.</td></tr>
<tr><td><span class="term">QNAME minimisation</span></td><td>Sending only the portion of a name needed at each resolution stage.</td></tr>
<tr><td><span class="term">Real-time bidding</span></td><td>Per-impression auction in which device context is broadcast to many potential buyers.</td></tr>
<tr><td><span class="term">Response policy zone</span></td><td>A mechanism for expressing resolver policy as DNS zone data.</td></tr>
<tr><td><span class="term">Ubiquitous technical surveillance</span></td><td>Aggregate visibility arising from the routine digital exhaust of ordinary devices and services.</td></tr>
<tr><td><span class="term">Work profile</span></td><td>A separate managed Android profile with its own application instances, data and profile-scoped identifiers.</td></tr>
</tbody>
</table>
</div>
</section>

<!-- ─── REFERENCES ─────────────────────────────────────────── -->
<div class="ckp-refs" id="references">
<h2>References</h2>

<p style="column-span: all; margin-bottom: 1.2rem; font-style: italic;">Sources marked <span class="v-tag v">V</span> were retrieved and checked against the primary source during preparation in September 2026. <span class="v-tag s">S</span> marks standard technical or project documentation cited from working knowledge — confirm currency, as version-specific behaviour changes. <span class="v-tag r">R</span> marks reporting on events, cited for the event rather than for any technical mechanism.</p>

<p id="ref-Reuters2026"><span class="v-tag r">R</span><span class="ref-num">[Reuters2026]</span> Reuters: US military disables ad trackers on devices following reports of location data used to target troops (4–5 September 2026). Originating report on correspondence released by Sen. Ron Wyden and Rep. Pat Harrigan, including service memoranda dated 8 July – 18 August 2026 and an Inspector General request due 2 October 2026. Widely syndicated; accessible account at <a href="https://taskandpurpose.com/news/military-cybersecurity-ad-trackers-iran/">taskandpurpose.com</a>. <em>Primary letters should be obtained from Sen. Wyden's office.</em></p>

<p id="ref-FTCMobilewalla"><span class="v-tag v">V</span><span class="ref-num">[FTCMobilewalla]</span> Federal Trade Commission: <em>FTC Takes Action Against Mobilewalla for Collecting and Selling Sensitive Location Data</em> (3 December 2024). <a href="https://www.ftc.gov/news-events/news/press-releases/2024/12/ftc-takes-action-against-mobilewalla-collecting-selling-sensitive-location-data">ftc.gov</a>; complaint at <a href="https://www.ftc.gov/system/files/ftc_gov/pdf/Mobilewalla-Complaint.pdf">Mobilewalla-Complaint.pdf</a></p>

<p id="ref-FTCRTB"><span class="v-tag v">V</span><span class="ref-num">[FTCRTB]</span> Federal Trade Commission, Office of Technology: <em>Unpacking Real Time Bidding through FTC's case on Mobilewalla</em>. <a href="https://www.ftc.gov/policy/advocacy-research/tech-at-ftc/2024/12/unpacking-real-time-bidding-through-ftcs-case-mobilewalla">ftc.gov</a></p>

<p id="ref-FTCPADFAA"><span class="v-tag v">V</span><span class="ref-num">[FTCPADFAA]</span> Federal Trade Commission: <em>FTC Reminds Data Brokers of Their Obligations to Comply with PADFAA</em> (9 February 2026), and the published <a href="https://www.ftc.gov/legal-library/browse/warning-letters/protecting-americans-data-foreign-adversaries-act-padfaa-warning-letter-template">warning letter template</a> referencing armed-forces status products. <a href="https://www.ftc.gov/news-events/news/press-releases/2026/02/ftc-reminds-data-brokers-their-obligations-comply-padfaa">Press release</a></p>

<p id="ref-PrivacySandbox"><span class="v-tag v">V</span><span class="ref-num">[PrivacySandbox]</span> Google: <em>Privacy Sandbox on Android</em> — deprecation notice, 17 October 2025. <a href="https://developers.google.com/admob/android/privacy/sandbox">developers.google.com</a></p>

<p id="ref-Android13"><span class="v-tag v">V</span><span class="ref-num">[Android13]</span> Android Developers: <em>Behavior changes: Apps targeting Android 13 or higher</em> — <code>AD_ID</code> permission and identifier zeroing. <a href="https://developer.android.com/about/versions/13/behavior-changes-13">developer.android.com</a>. See also Play Console Help, <a href="https://support.google.com/googleplay/android-developer/answer/6048248">Advertising ID</a></p>

<p id="ref-AMAPI"><span class="v-tag v">V</span><span class="ref-num">[AMAPI]</span> Google: <em>Android Management API — Policy resource reference</em>. Source for the policy fields cited in §5. <a href="https://developers.google.com/android/management/reference/rest/v1/enterprises.policies">developers.google.com</a></p>

<p id="ref-ADP"><span class="v-tag v">V</span><span class="ref-num">[ADP]</span> Android Open Source Project: <em>Device management overview</em>. <a href="https://source.android.com/docs/devices/admin">source.android.com</a></p>

<p id="ref-PDNS"><span class="v-tag v">V</span><span class="ref-num">[NSAPDNS]</span> NSA &amp; CISA: <em>Selecting a Protective DNS Service</em>, Cybersecurity Information Sheet U/OO/117652-21 (originally 4 March 2021; later versions issued). Distinguishes protective DNS from encrypted DNS and DNSSEC. <a href="https://www.nsa.gov/Press-Room/News-Highlights/Article/Article/2523771/nsa-and-cisa-release-cybersecurity-information-on-protective-dns/">nsa.gov</a></p>

<p id="ref-WG"><span class="v-tag s">S</span><span class="ref-num">[WireGuard]</span> Donenfeld, J.A.: <em>WireGuard: Next Generation Kernel Network Tunnel</em>, NDSS 2017. <a href="https://www.wireguard.com/papers/wireguard.pdf">wireguard.com</a>. Android tunnel library: <a href="https://git.zx2c4.com/wireguard-android/about/">git.zx2c4.com</a></p>

<p id="ref-Unbound"><span class="v-tag s">S</span><span class="ref-num">[Unbound]</span> NLnet Labs: <em>Unbound</em> — validating, recursive, caching resolver. <a href="https://nlnetlabs.nl/projects/unbound/about/">nlnetlabs.nl</a>. PowerDNS: <a href="https://dnsdist.org/">dnsdist</a></p>

<p id="ref-RFC"><span class="v-tag s">S</span><span class="ref-num">[RFCs]</span> RFC 4033/4034/4035 (DNSSEC); RFC 9364 (DNSSEC BCP); RFC 7858 (DoT); RFC 8484 (DoH); RFC 9250 (DoQ); RFC 9156 (QNAME minimisation); RFC 7871 (EDNS Client Subnet).</p>

<p id="ref-Platform"><span class="v-tag s">S</span><span class="ref-num">[Platform]</span> Android Developers: <a href="https://developer.android.com/reference/android/net/VpnService">VpnService</a>; <a href="https://developer.android.com/work/dpc/vpn">Always-on VPN</a>; <a href="https://developer.android.com/work/dpc/logging">Network logging</a>; <a href="https://developer.android.com/privacy-and-security/security-config">Network security configuration</a>; <a href="https://developer.android.com/training/package-visibility">Package visibility</a>; <a href="https://developer.android.com/google/play/integrity">Play Integrity API</a>. AOSP: <a href="https://source.android.com/docs/security/app-sandbox">Application sandbox</a>; <a href="https://source.android.com/docs/core/virtualization">Android Virtualization Framework</a>.</p>

<p id="ref-OpenRTB"><span class="v-tag s">S</span><span class="ref-num">[OpenRTB]</span> IAB Tech Lab: <em>OpenRTB Specification</em> — device, geography, identifier and privacy-signal fields. <a href="https://iabtechlab.com/standards/openrtb/">iabtechlab.com</a></p>

<p style="column-span: all; margin-top: 1.5rem; padding-top: 1rem; border-top: 1px solid var(--border); font-style: italic;">The authors welcome technical correction. Where a claim here is shown to be wrong, a revision will be issued with the correction identified rather than silently amended. Correspondence to <a href="mailto:smk@pakcrypt.org">smk@pakcrypt.org</a>.</p>
</div>

</div><!-- end .ckp-body -->

<!-- ─── Sidebar TOC ─────────────────────────────────────────── -->
<aside class="ckp-sidebar">
  <div class="ckp-toc-label">Contents</div>
  <ul class="ckp-toc-list" id="ckp-toc">
    <li data-section="abstract"><a href="#abstract">Abstract</a></li>
    <li data-section="sec-market"><a href="#sec-market">1. The Market That Does the Work</a></li>
    <li class="toc-sub" data-section="sec-market"><a href="#sec-market">The Documented Record</a></li>
    <li class="toc-sub" data-section="sec-market"><a href="#sec-market">Where the Boundary Falls</a></li>
    <li data-section="sec-inside"><a href="#sec-inside">2. What Leaves the Phone</a></li>
    <li class="toc-sub" data-section="sec-inside"><a href="#sec-inside">The Permission Boundary</a></li>
    <li class="toc-sub" data-section="sec-inside"><a href="#sec-inside">Signal Taxonomy</a></li>
    <li data-section="sec-routes"><a href="#sec-routes">3. Six Ways Out</a></li>
    <li class="toc-sub" data-section="sec-routes"><a href="#sec-routes">The Bidstream</a></li>
    <li class="toc-sub" data-section="sec-routes"><a href="#sec-routes">After the Handset</a></li>
    <li data-section="sec-maid"><a href="#sec-maid">4. Killing the Ad ID</a></li>
    <li class="toc-sub" data-section="sec-maid"><a href="#sec-maid">2026 Platform Position</a></li>
    <li data-section="sec-controls"><a href="#sec-controls">5. What Each Control Buys</a></li>
    <li class="toc-sub" data-section="sec-controls"><a href="#sec-controls">Protective DNS</a></li>
    <li class="toc-sub" data-section="sec-controls"><a href="#sec-controls">Network Egress</a></li>
    <li class="toc-sub" data-section="sec-controls"><a href="#sec-controls">Uniformity vs Randomisation</a></li>
    <li class="toc-sub" data-section="sec-controls"><a href="#sec-controls">Forking Android</a></li>
    <li class="toc-sub" data-section="sec-controls"><a href="#sec-controls">Sandboxing &amp; DNSSEC</a></li>
    <li data-section="sec-arch"><a href="#sec-arch">6. The Architecture</a></li>
    <li class="toc-sub" data-section="sec-arch"><a href="#sec-arch">Agent &amp; Gateway</a></li>
    <li class="toc-sub" data-section="sec-arch"><a href="#sec-arch">Application Assurance</a></li>
    <li class="toc-sub" data-section="sec-arch"><a href="#sec-arch">Assurance Tiers</a></li>
    <li data-section="sec-backfire"><a href="#sec-backfire">7. Risks It Creates</a></li>
    <li class="toc-sub" data-section="sec-backfire"><a href="#sec-backfire">The Uniform Problem</a></li>
    <li data-section="sec-claims"><a href="#sec-claims">8. What You May Claim</a></li>
    <li class="toc-sub" data-section="sec-claims"><a href="#sec-claims">Open Questions</a></li>
    <li data-section="sec-verify"><a href="#sec-verify">9. Proving It</a></li>
    <li data-section="sec-glossary"><a href="#sec-glossary">Glossary</a></li>
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

  /* ── Back to top ── */
  var topBtn = document.getElementById('ckp-top');
  function updateTop() {
    if (!topBtn) return;
    topBtn.classList.toggle('show', (window.scrollY || window.pageYOffset) > 600);
  }
  if (topBtn) {
    topBtn.addEventListener('click', function() {
      window.scrollTo({ top: 0, behavior: 'smooth' });
    });
  }
  window.addEventListener('scroll', updateTop, { passive: true });
  updateTop();

  /* ── TOC active state ── */
  var sections = ['abstract','sec-market','sec-inside','sec-routes','sec-maid',
                  'sec-controls','sec-arch','sec-backfire','sec-claims',
                  'sec-verify','sec-glossary','references'];
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

  /* ── Copy buttons on diagrams ── */
  document.querySelectorAll('.ckp-diagram .ckp-copy').forEach(function(btn) {
    btn.addEventListener('click', function() {
      var block = btn.closest('.ckp-diagram').querySelector('code');
      if (!block) return;
      var text = block.innerText;
      var done = function() {
        var old = btn.textContent;
        btn.textContent = 'Copied';
        setTimeout(function() { btn.textContent = old; }, 1400);
      };
      if (navigator.clipboard && navigator.clipboard.writeText) {
        navigator.clipboard.writeText(text).then(done).catch(function(){});
      } else {
        var ta = document.createElement('textarea');
        ta.value = text;
        ta.style.position = 'fixed';
        ta.style.opacity = '0';
        document.body.appendChild(ta);
        ta.select();
        try { document.execCommand('copy'); done(); } catch (err) {}
        document.body.removeChild(ta);
      }
    });
  });
})();
</script>
