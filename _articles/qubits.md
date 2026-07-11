---
layout: post
title: "How to Think in Qubits"
math: true
---

<!-- MathJax Configuration for Jekyll/GitHub Pages -->
<script>
MathJax = {
  tex: {
    inlineMath: [['$', '$'], ['\\(', '\\)']],
    displayMath: [['$$', '$$'], ['\\[', '\\]']],
    tags: 'ams'
  },
  svg: { fontCache: 'global' }
};
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js" async></script>

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
.ckp-callout p:last-child { margin-bottom: 0; }

/* ─── Equation display ─────────────────────────────────────────── */
.ckp-eq {
  margin: 1.8rem 0;
  padding: 1.2rem 1.5rem;
  background: var(--surface);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  overflow-x: auto;
  font-size: 1.05rem;
  text-align: center;
}
.ckp-eq .eq-label {
  font-family: var(--font-mono);
  font-size: 0.65rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--text-muted);
  display: block;
  margin-bottom: 0.6rem;
  text-align: left;
}

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

/* ─── Hierarchy list ────────────────────────────────────────────── */
.ckp-hier {
  margin: 1.5rem 0;
  padding: 0;
  list-style: none;
}
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

/* ─── Comparison / Glossary table ─────────────────────────────── */
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
.ckp-table.wide { min-width: 700px; }
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
.ckp-table .bad  { color: var(--red); font-family: var(--font-mono); font-size: 0.78rem; }
.ckp-table .good { color: var(--green); font-family: var(--font-mono); font-size: 0.78rem; }
.ckp-table code {
  font-family: var(--font-mono);
  font-size: 0.78rem;
  color: var(--accent);
  background: var(--surface2);
  padding: 0.05rem 0.35rem;
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
.ckp-refs p { margin: 0 0 0.5rem; break-inside: avoid; line-height: 1.4; }
.ckp-refs .ref-num { color: var(--accent); font-family: var(--font-mono); font-size: 0.7rem; }

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
.ckp-hero    { animation: ckp-fade-in 0.6s ease both; }
.ckp-abstract { animation: ckp-fade-in 0.6s ease 0.15s both; }
@media (prefers-reduced-motion: reduce) {
  .ckp-hero, .ckp-abstract { animation: none; }
  #ckp-progress { transition: none; }
}

/* ─── Keywords strip ────────────────────────────────────────────── */
.ckp-keywords {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin: 1.5rem 0 2rem;
}
.ckp-kw {
  font-family: var(--font-mono);
  font-size: 0.68rem;
  letter-spacing: 0.08em;
  background: var(--surface2);
  border: 1px solid var(--border);
  color: var(--text-muted);
  padding: 0.25rem 0.7rem;
}

/* ═══════════════════════════════════════════════════════════════ */
/*  EXTENSIONS FOR THIS ARTICLE: circuits, code, exercises         */
/* ═══════════════════════════════════════════════════════════════ */

/* ─── Circuit figures ───────────────────────────────────────────── */
.ckp-circuit {
  background: var(--surface);
  border: 1px solid var(--border);
  border-left: 3px solid var(--blue);
  padding: 1.6rem 1.2rem 1.1rem;
  margin: 2rem 0;
  overflow-x: auto;
}
.ckp-circuit svg {
  display: block;
  margin: 0 auto;
  width: 100%;
  max-width: 660px;
  height: auto;
}
.ckp-circuit figcaption {
  font-family: var(--font-mono);
  font-size: 0.66rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--text-muted);
  margin-top: 1.1rem;
  padding-top: 0.7rem;
  border-top: 1px solid var(--border);
  line-height: 1.7;
}

/* SVG circuit primitives */
.qc-wire     { stroke: #6f6f7c; stroke-width: 1.6; fill: none; }
.qc-cwire    { stroke: #6f6f7c; stroke-width: 1.1; fill: none; }
.qc-box      { fill: var(--surface2); stroke: var(--accent); stroke-width: 1.6; }
.qc-box-alt  { fill: var(--surface2); stroke: var(--blue);   stroke-width: 1.6; }
.qc-ctrl     { fill: var(--accent); }
.qc-tgt      { fill: var(--surface); stroke: var(--accent); stroke-width: 1.6; }
.qc-link     { stroke: var(--accent); stroke-width: 1.6; fill: none; }
.qc-meter    { stroke: var(--blue); stroke-width: 1.5; fill: none; }
.qc-stage    { stroke: var(--border); stroke-width: 1; stroke-dasharray: 4 4; }
.qc-time     { stroke: var(--border); stroke-width: 1; }
.qc-timehead { fill: var(--border); }
.qc-ket {
  font-family: var(--font-mono); font-size: 15px; fill: var(--text);
  text-anchor: middle; dominant-baseline: central;
}
.qc-txt {
  font-family: var(--font-mono); font-size: 15px; font-weight: 600; fill: var(--accent);
  text-anchor: middle; dominant-baseline: central;
}
.qc-txt-alt {
  font-family: var(--font-mono); font-size: 15px; font-weight: 600; fill: var(--blue);
  text-anchor: middle; dominant-baseline: central;
}
.qc-lbl {
  font-family: var(--font-mono); font-size: 11px; fill: var(--text-muted);
  text-anchor: middle; dominant-baseline: central;
}
.qc-lbl-s  { text-anchor: start; }
.qc-col {
  font-family: var(--font-mono); font-size: 10px; letter-spacing: 0.14em;
  text-transform: uppercase; fill: var(--text-muted); text-anchor: middle;
}
.qc-out {
  font-family: var(--font-mono); font-size: 14px; fill: var(--accent);
  text-anchor: start; dominant-baseline: central;
}
.qc-mk    { fill: var(--accent-dim); stroke: var(--accent); stroke-width: 1.2; }
.qc-mknum {
  font-family: var(--font-mono); font-size: 11px; font-weight: 600; fill: var(--accent);
  text-anchor: middle; dominant-baseline: central;
}
/* interference path diagram */
.qc-node    { fill: var(--surface2); stroke: var(--accent); stroke-width: 1.6; }
.qc-nodetxt {
  font-family: var(--font-mono); font-size: 14px; fill: var(--text);
  text-anchor: middle; dominant-baseline: central;
}
.qc-edge     { stroke: #6f6f7c; stroke-width: 1.6; }
.qc-edge-neg { stroke: var(--red); stroke-width: 1.6; }
.qc-amp {
  font-family: var(--font-mono); font-size: 12px; fill: var(--text);
  text-anchor: middle; dominant-baseline: central;
  paint-order: stroke; stroke: var(--surface); stroke-width: 5px; stroke-linejoin: round;
}
.qc-neg { fill: var(--red); }
.qc-pos { fill: var(--green); }
.qc-res {
  font-family: var(--font-mono); font-size: 13px;
  text-anchor: start; dominant-baseline: central;
}
.qc-res-sub {
  font-family: var(--font-mono); font-size: 10px; letter-spacing: 0.1em;
  text-transform: uppercase; text-anchor: start; dominant-baseline: central; opacity: 0.85;
}
.qc-foot {
  font-family: var(--font-mono); font-size: 11px; fill: var(--text-muted); text-anchor: middle;
}

/* ─── Code blocks ───────────────────────────────────────────────── */
.ckp-code {
  background: #16161a;
  border: 1px solid var(--border);
  border-left: 3px solid var(--green);
  padding: 1.1rem 1.3rem;
  margin: 1.8rem 0;
  overflow-x: auto;
  font-family: var(--font-mono);
  font-size: 0.78rem;
  line-height: 1.7;
  color: #cfcfd6;
  white-space: pre;
  tab-size: 2;
}
.ckp-code .c { color: var(--text-muted); font-style: italic; }
.ckp-code .k { color: var(--accent); }
.ckp-code .f { color: var(--blue); }
.ckp-code .s { color: var(--green); }

/* ─── Exercises ─────────────────────────────────────────────────── */
.ckp-exercise {
  display: grid;
  grid-template-columns: 34px 1fr;
  gap: 1rem;
  padding: 1rem 1.2rem;
  border: 1px solid var(--border);
  border-left: 3px solid var(--green);
  background: var(--surface);
  margin-bottom: 1rem;
  font-size: 0.9rem;
}
.ckp-exercise .ex-num {
  font-family: var(--font-mono);
  font-size: 0.8rem;
  font-weight: 600;
  color: var(--green);
  padding-top: 0.2rem;
}
.ckp-exercise p { margin: 0 0 0.5rem; }
.ckp-exercise p:last-child { margin: 0; }
.ckp-exercise .ex-hint {
  font-size: 0.82rem;
  color: var(--text-muted);
  font-style: italic;
}
</style>

<div id="ckp-progress"></div>

<article class="ckp-article">

<!-- ═══════════════════ HERO ═══════════════════════════════════ -->
<div class="ckp-hero">
  <div class="ckp-kicker">Quantum Information · Qubits · Gates · Circuits</div>
  <h1>How to Think in <em>Qubits</em></h1>
  <p class="ckp-deck">A first-principles tutorial in quantum information for cryptographers and mathematicians — from the state space of a single qubit to universal gate sets, circuit construction, interference, and what a quantum attack actually costs.</p>
  <div class="ckp-meta">
    <span>Quantum Foundations Series</span>
    <span class="dot"></span>
    <span>PakCrypt Technical Articles · 2026</span>
    <span class="dot"></span>
    <span>~45 min read</span>
    <span class="dot"></span>
    <span>Prerequisites: linear algebra, basic probability</span>
  </div>
</div>

<!-- Keywords -->
<div class="ckp-keywords">
  <span class="ckp-kw">Qubit</span>
  <span class="ckp-kw">Hilbert Space</span>
  <span class="ckp-kw">Unitary Gates</span>
  <span class="ckp-kw">Quantum Circuits</span>
  <span class="ckp-kw">Interference</span>
  <span class="ckp-kw">Entanglement</span>
  <span class="ckp-kw">No-Cloning</span>
  <span class="ckp-kw">Clifford+T</span>
  <span class="ckp-kw">Universality</span>
</div>

<!-- Mobile TOC -->
<div class="ckp-mobile-toc" id="ckp-mob-toc-toggle">
  <span>Contents</span><span>▾</span>
</div>
<div class="ckp-mobile-toc-list" id="ckp-mob-toc-list">
  <a href="#abstract">Abstract</a>
  <a href="#sec-model">1. The Right Mental Model</a>
  <a href="#sec-qubit">2. What a Qubit Actually Is</a>
  <a href="#sec-measure">3. Measurement</a>
  <a href="#sec-multi">4. Many Qubits &amp; Entanglement</a>
  <a href="#sec-unitary">5. Gates Are Unitary Matrices</a>
  <a href="#sec-gates">6. The Gate Zoo</a>
  <a href="#sec-circuits">7. Constructing Circuits</a>
  <a href="#sec-deutsch">8. Interference at Work</a>
  <a href="#sec-universal">9. Universality &amp; What Is Hard</a>
  <a href="#sec-crypto">10. What This Means for Cryptography</a>
  <a href="#sec-think">11. How to Think Correctly</a>
  <a href="#sec-exercises">Exercises</a>
  <a href="#sec-glossary">Quick Reference Glossary</a>
  <a href="#references">References</a>
</div>

<!-- ═══════════════════ LAYOUT ════════════════════════════════ -->
<div class="ckp-layout">

<!-- ─── Main Body ─────────────────────────────────────────── -->
<div class="ckp-body">

<!-- ABSTRACT -->
<div class="ckp-abstract" id="abstract">
  <div class="ckp-abstract-label">Abstract</div>
  <p>This is a self-contained introduction to quantum information for readers who are comfortable with linear algebra and probability but have never worked with a qubit. We build the subject from one substitution — replace the 1-norm over the non-negative reals with the 2-norm over the complex numbers — and derive everything else from it: the Born rule, unitarity, reversibility, no-cloning, entanglement, and interference. We then construct quantum circuits explicitly, catalogue the standard gates with their matrices, prove universality of small gate sets, and explain why entanglement alone is <em>not</em> the source of quantum advantage. We close with what all of this actually implies for cryptography, including honest resource estimates for attacks on RSA and AES.</p>
</div>

<!-- STATS BAR -->
<div class="ckp-stat-row">
  <div class="ckp-stat"><span class="stat-num">$\mathbb{C}^2$</span><span class="stat-label">The entire state space of one qubit</span></div>
  <div class="ckp-stat"><span class="stat-num">$2^n$</span><span class="stat-label">Amplitudes in an $n$-qubit register</span></div>
  <div class="ckp-stat"><span class="stat-num">$n$</span><span class="stat-label">Classical bits you can extract (Holevo)</span></div>
  <div class="ckp-stat"><span class="stat-num">3</span><span class="stat-label">Gates suffice for universality: H, T, CNOT</span></div>
</div>

<!-- ─── SECTION 1 ─────────────────────────────────────────── -->
<section id="sec-model">
<h2>1. The Right Mental Model</h2>

<p class="drop-cap">Almost every serious misunderstanding of quantum computing comes from the same mistake: reaching for a physical picture before reaching for the linear algebra. A qubit is not a coin that has not yet landed. It is not a bit that is secretly both values at once. It is a unit vector in a two-dimensional complex vector space — and every correct intuition you will ever have about quantum information is, in the end, a statement about that vector space.</p>

<p>So we will not start with photons, spins, or cats. We will start with something you already know — a probabilistic computer — and change exactly one thing.</p>

<h3>Three Computers, One Difference</h3>

<p>Consider a machine with $N$ possible configurations, labelled $0, 1, \dots, N-1$. There are three ways to describe its state.</p>

<ul class="ckp-hier">
  <li><strong>Deterministic.</strong> The state is a single label $x$. Equivalently, the standard basis vector $e_x \in \mathbb{R}^N$. Evolution is a function on labels; if we insist on reversibility, a permutation matrix.</li>
  <li><strong>Probabilistic.</strong> The state is a vector $p \in \mathbb{R}^N$ with $p_i \geq 0$ and $\sum_i p_i = 1$. That is: the entries are non-negative and the <em>1-norm</em> is 1. Evolution is a stochastic matrix — one that maps probability vectors to probability vectors.</li>
  <li><strong>Quantum.</strong> The state is a vector $\psi \in \mathbb{C}^N$ with $\sum_i |\psi_i|^2 = 1$. That is: the entries are arbitrary complex numbers and the <em>2-norm</em> is 1. Evolution is a unitary matrix — one that maps unit vectors to unit vectors.</li>
</ul>

<p>That is the whole leap. Swap the 1-norm over $\mathbb{R}_{\geq 0}$ for the 2-norm over $\mathbb{C}$. Everything that follows — interference, entanglement, the impossibility of copying, the Born rule, the entire architecture of quantum algorithms — is downstream of that one substitution.</p>

<div class="ckp-callout key">
  <strong>Why the Norm Is the Whole Story</strong>
  <p>The norm you preserve determines the matrices you are allowed to use, and the matrices you are allowed to use determine what your computer can do.</p>
  <p>Preserve the 1-norm on non-negative vectors and you get <em>stochastic</em> matrices. Their entries lie in $[0,1]$. There is no way for two non-negative numbers to cancel. Probability mass can be shuffled and spread, but never destroyed by adding more of it.</p>
  <p>Preserve the 2-norm over $\mathbb{C}$ and you get <em>unitary</em> matrices. Their entries may be negative, or complex. Two computational paths that arrive at the same outcome may now arrive carrying amplitudes $+\tfrac{1}{2}$ and $-\tfrac{1}{2}$ — and annihilate.</p>
  <p><strong style="display:inline; text-transform:none; letter-spacing:normal; font-family:var(--font-serif); font-size:0.92rem; color:var(--text);">Probabilities can only accumulate. Amplitudes can cancel.</strong> That single asymmetry is the entire resource that quantum computation exploits.</p>
</div>

<h3>The Comparison That Should Live in Your Head</h3>

<div class="ckp-table-wrap">
<table class="ckp-table wide">
<thead>
  <tr>
    <th></th>
    <th>Deterministic</th>
    <th>Probabilistic</th>
    <th>Quantum</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><span class="term">State</span></td>
    <td>Label $x$, i.e. basis vector $e_x$</td>
    <td>Probability vector $p \in \mathbb{R}^N$</td>
    <td>Amplitude vector $\psi \in \mathbb{C}^N$</td>
  </tr>
  <tr>
    <td><span class="term">Constraint</span></td>
    <td>—</td>
    <td>$p_i \geq 0$, &nbsp; $\textstyle\sum_i p_i = 1$</td>
    <td>$\textstyle\sum_i |\psi_i|^2 = 1$</td>
  </tr>
  <tr>
    <td><span class="term">Norm preserved</span></td>
    <td>—</td>
    <td>$\ell^1$</td>
    <td>$\ell^2$</td>
  </tr>
  <tr>
    <td><span class="term">Evolution</span></td>
    <td>Permutation matrix</td>
    <td>Stochastic matrix</td>
    <td>Unitary matrix</td>
  </tr>
  <tr>
    <td><span class="term">Reversible?</span></td>
    <td>If we require it</td>
    <td>Generally no</td>
    <td><em>Always</em> — until you measure</td>
  </tr>
  <tr>
    <td><span class="term">Cancellation</span></td>
    <td>None</td>
    <td>None — entries are $\geq 0$</td>
    <td><strong>Yes</strong> — this is the resource</td>
  </tr>
  <tr>
    <td><span class="term">Composing systems</span></td>
    <td>Cartesian product</td>
    <td>Tensor product of $p$-vectors</td>
    <td>Tensor product of Hilbert spaces</td>
  </tr>
  <tr>
    <td><span class="term">Reading the state</span></td>
    <td>Free, complete</td>
    <td>Free, complete</td>
    <td>Destructive, partial (Born rule)</td>
  </tr>
</tbody>
</table>
</div>

<h3>The Fallacy You Must Kill Immediately</h3>

<p>You will read, in a hundred popular articles, that a quantum computer "tries all $2^n$ possibilities in parallel." This is the single most damaging sentence in the field, and you should scrub it from your vocabulary before reading further.</p>

<p>Here is why it is wrong. Yes, an $n$-qubit register carries $2^n$ complex amplitudes. But you never get to <em>read</em> those $2^n$ numbers. When you measure, you receive exactly one $n$-bit string, sampled according to the Born rule. If "parallelism" were the mechanism, a quantum computer would solve NP-complete problems instantly by checking every certificate at once — and it is not believed to do so [<a href="#ref-BBBV1997">BBBV1997</a>].</p>

<p>The correct sentence is this: a quantum computer manipulates one vector of $2^n$ amplitudes, and hands you a single sample from it. The <em>entire art</em> of quantum algorithm design is arranging for the amplitudes on the wrong answers to cancel, so that the one sample you are allowed is overwhelmingly likely to be the right one.</p>

<div class="ckp-pull">
  <p>Superposition is not the resource. Interference is. Superposition merely makes interference possible — and a computation that never interferes is a computation you could have run classically, at the same cost, with a coin.</p>
  <cite>— The organising principle of this tutorial</cite>
</div>
</section>

<div class="ckp-sep">The Qubit</div>

<!-- ─── SECTION 2 ─────────────────────────────────────────── -->
<section id="sec-qubit">
<h2>2. What a Qubit Actually Is</h2>

<p>Set $N = 2$. A single qubit is a unit vector in $\mathbb{C}^2$.</p>

<div class="ckp-eq">
  <span class="eq-label">The Qubit — Eq. (1)</span>
  $$|\psi\rangle = \alpha\,|0\rangle + \beta\,|1\rangle, \qquad \alpha,\beta \in \mathbb{C}, \qquad |\alpha|^2 + |\beta|^2 = 1 \tag{1}$$
</div>

<p>The two vectors $|0\rangle$ and $|1\rangle$ form the <em>computational basis</em>. Concretely:</p>

<div class="ckp-eq">
  <span class="eq-label">Computational Basis — Eq. (2)</span>
  $$|0\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \qquad |1\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix} \tag{2}$$
</div>

<p>That is the definition. There is nothing else. A qubit is a point on the unit sphere of $\mathbb{C}^2$, and the rest of this tutorial is bookkeeping.</p>

<h3>Dirac Notation Is Just Linear Algebra with Better Bookkeeping</h3>

<p>The angle brackets intimidate newcomers unnecessarily. They are a compact notation for objects you already know.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr>
    <th>Dirac</th>
    <th>Name</th>
    <th>What it is</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><span class="term">$|\psi\rangle$</span></td>
    <td>ket</td>
    <td>A column vector in $\mathbb{C}^2$ (or $\mathbb{C}^{2^n}$).</td>
  </tr>
  <tr>
    <td><span class="term">$\langle\psi|$</span></td>
    <td>bra</td>
    <td>Its conjugate transpose — a row vector, i.e. $|\psi\rangle^{\dagger}$.</td>
  </tr>
  <tr>
    <td><span class="term">$\langle\phi|\psi\rangle$</span></td>
    <td>braket</td>
    <td>The Hermitian inner product $\phi^{\dagger}\psi \in \mathbb{C}$. A number.</td>
  </tr>
  <tr>
    <td><span class="term">$|\psi\rangle\langle\phi|$</span></td>
    <td>ketbra</td>
    <td>The outer product $\psi\phi^{\dagger}$ — a matrix. A rank-1 operator.</td>
  </tr>
  <tr>
    <td><span class="term">$\langle\phi|A|\psi\rangle$</span></td>
    <td>matrix element</td>
    <td>$\phi^{\dagger} A \psi$. A number.</td>
  </tr>
  <tr>
    <td><span class="term">$|\psi\rangle \otimes |\phi\rangle$</span></td>
    <td>tensor / Kronecker</td>
    <td>Also written $|\psi\rangle|\phi\rangle$ or $|\psi\phi\rangle$.</td>
  </tr>
</tbody>
</table>
</div>

<p>The one habit worth acquiring immediately: <strong>$\langle 0|\psi\rangle = \alpha$</strong>. The bra $\langle 0|$ extracts the coefficient of $|0\rangle$. This is why the Born rule is written the way it is.</p>

<h3>The Born Rule</h3>

<p>Measuring $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$ in the computational basis returns the outcome $0$ with probability $|\alpha|^2$ and $1$ with probability $|\beta|^2$.</p>

<div class="ckp-eq">
  <span class="eq-label">Born Rule — Eq. (3)</span>
  $$\Pr[\,k\,] = \bigl|\langle k|\psi\rangle\bigr|^2, \qquad k \in \{0,1\} \tag{3}$$
</div>

<p>The normalisation condition $|\alpha|^2 + |\beta|^2 = 1$ is now exactly the statement that probabilities sum to one. It is not an extra postulate bolted on; it is the reason the state space is the unit sphere and not all of $\mathbb{C}^2$.</p>

<h3>Global Phase Is Nothing. Relative Phase Is Everything.</h3>

<p>This is the distinction beginners fumble most often, and the one that most reliably separates people who understand qubits from people who are reciting them.</p>

<p>Multiply the whole state by a unit complex number: $|\psi'\rangle = e^{i\gamma}|\psi\rangle$. Then for any measurement, and after any subsequent sequence of gates $U$, the outcome probabilities are unchanged, because $|e^{i\gamma}|^2 = 1$ and $U(e^{i\gamma}|\psi\rangle) = e^{i\gamma}(U|\psi\rangle)$. The factor rides along, unobservably, forever. <strong>A global phase has no physical meaning whatsoever.</strong></p>

<p>Now consider instead the <em>relative</em> phase between the two components:</p>

<div class="ckp-eq">
  <span class="eq-label">Two States with Identical Born Statistics — Eq. (4)</span>
  $$|+\rangle = \tfrac{1}{\sqrt{2}}\bigl(|0\rangle + |1\rangle\bigr), \qquad |-\rangle = \tfrac{1}{\sqrt{2}}\bigl(|0\rangle - |1\rangle\bigr) \tag{4}$$
</div>

<p>Measure either one in the computational basis and you get $0$ or $1$ with probability $\tfrac{1}{2}$ each. They are statistically indistinguishable — <em>in that basis</em>. But they are orthogonal states, $\langle +|-\rangle = 0$, and a single application of the Hadamard gate maps $|+\rangle \mapsto |0\rangle$ and $|-\rangle \mapsto |1\rangle$, distinguishing them with certainty. The minus sign is not a decoration. It is the whole difference between two perfectly distinguishable states.</p>

<div class="ckp-callout warn">
  <strong>The Rule of Thumb</strong>
  <p>If a phase multiplies the <em>entire</em> state vector, ignore it — you may freely add or drop it in any calculation. If a phase multiplies <em>one component relative to another</em>, it is physical, it is measurable, and it is very probably the thing your algorithm is about to exploit.</p>
</div>

<h3>The Bloch Sphere — and When to Stop Using It</h3>

<p>Since global phase is meaningless and the norm is fixed, the four real parameters in $(\alpha,\beta)$ collapse to two. Write:</p>

<div class="ckp-eq">
  <span class="eq-label">Bloch Parametrisation — Eq. (5)</span>
  $$|\psi\rangle = \cos\tfrac{\theta}{2}\,|0\rangle + e^{i\varphi}\sin\tfrac{\theta}{2}\,|1\rangle, \qquad \theta \in [0,\pi],\ \ \varphi \in [0,2\pi) \tag{5}$$
</div>

<p>The pair $(\theta,\varphi)$ are spherical polar coordinates. Every pure qubit state is a point on a sphere: $|0\rangle$ at the north pole, $|1\rangle$ at the south pole, $|\pm\rangle$ on the equator. For a mathematician there is an elegant way to say this: the state space of a qubit is the complex projective line $\mathbb{CP}^1$, and $\mathbb{CP}^1 \cong S^2$ is the Riemann sphere.</p>

<p>Note carefully that <em>orthogonal states sit at antipodal points, not at right angles</em>. $|0\rangle$ and $|1\rangle$ are orthogonal in $\mathbb{C}^2$ but $180°$ apart on the sphere. The Bloch angle is half the Hilbert-space angle. This trips up everyone once.</p>

<div class="ckp-callout warn">
  <strong>Do Not Over-Trust the Bloch Sphere</strong>
  <p>The Bloch sphere is a faithful picture of <em>one</em> qubit and a lethal trap for <em>two</em>. There is no "Bloch sphere for two qubits." A two-qubit pure state lives in $\mathbb{CP}^3$ — six real dimensions — and entanglement is precisely the phenomenon that cannot be drawn as two little arrows on two little spheres.</p>
  <p>Rule: use the Bloch sphere to reason about single-qubit gates. The moment entanglement enters, drop it and return to vectors and matrices.</p>
</div>

<h3>Superposition Is Basis-Relative</h3>

<p>Here is a fact that reorganises many people's thinking, so read it slowly.</p>

<p>"Being in superposition" is <strong>not an intrinsic property of a state</strong>. It is a statement about a state <em>relative to a chosen basis</em>. The state $|+\rangle$ is a superposition of $|0\rangle$ and $|1\rangle$ — but it is a basis state of the $X$ basis $\{|+\rangle, |-\rangle\}$, where it is not a superposition of anything. And conversely $|0\rangle = \tfrac{1}{\sqrt2}(|+\rangle + |-\rangle)$ is a superposition in the $X$ basis.</p>

<p>Every state is a superposition in <em>some</em> basis and a basis state in another. So "the qubit is in a superposition" carries no information until you say <em>with respect to what</em>. (Contrast this with entanglement, in Section 4, which <em>is</em> basis-independent — and that is exactly why entanglement, not superposition, is the structurally meaningful notion.)</p>

<h3>How Much Information Is in a Qubit?</h3>

<div class="ckp-callout key">
  <strong>Key Concept: The Holevo Bound</strong>
  <p>A qubit is specified by two continuous complex parameters. It is tempting — and wrong — to conclude that a qubit stores infinitely many bits.</p>
  <p>You cannot get them out. Holevo's theorem [<a href="#ref-Holevo1973">Holevo1973</a>] states that no measurement strategy whatsoever can extract more than $n$ classical bits of information from $n$ qubits. The continuum of $(\alpha,\beta)$ is real, but it is <em>inaccessible</em>: one measurement yields one bit, and the state is destroyed in the process.</p>
  <p>For cryptographers this is the right calibration. Quantum states are not magic compression. The exponential lives in how the state <em>evolves</em>, never in how much you can <em>read</em>.</p>
</div>

<h3>Bit versus Qubit</h3>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr>
    <th></th>
    <th>Classical bit</th>
    <th>Qubit</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><span class="term">State space</span></td>
    <td>$\{0, 1\}$ — two points</td>
    <td>Unit sphere of $\mathbb{C}^2$ — a continuum</td>
  </tr>
  <tr>
    <td><span class="term">Copyable?</span></td>
    <td>Yes, trivially</td>
    <td><strong>No</strong> — no-cloning theorem (Section 5)</td>
  </tr>
  <tr>
    <td><span class="term">Readable?</span></td>
    <td>Yes, non-destructively, exactly</td>
    <td>One sample, then the state collapses</td>
  </tr>
  <tr>
    <td><span class="term">Information carried</span></td>
    <td>1 bit</td>
    <td>At most 1 bit extractable (Holevo)</td>
  </tr>
  <tr>
    <td><span class="term">$n$ of them</span></td>
    <td>$n$ bits describe the state</td>
    <td>$2^n$ complex amplitudes describe the state</td>
  </tr>
</tbody>
</table>
</div>
</section>

<div class="ckp-sep">Measurement</div>

<!-- ─── SECTION 3 ─────────────────────────────────────────── -->
<section id="sec-measure">
<h2>3. Measurement: The Only Irreversible Thing</h2>

<p>Every gate in a quantum circuit is reversible. Measurement is not. It is the one place where information leaves the quantum world, and it is where all of your probability comes from.</p>

<h3>Measuring in Another Basis</h3>

<p>The Born rule as stated in Eq. (3) measures in the computational ($Z$) basis. But you may measure in <em>any</em> orthonormal basis $\{|b_0\rangle, |b_1\rangle\}$; the probability of outcome $k$ is $|\langle b_k|\psi\rangle|^2$ and the state collapses to $|b_k\rangle$.</p>

<p>In practice hardware only measures in the computational basis, so we perform a change of basis first. To measure in the $X$ basis $\{|+\rangle,|-\rangle\}$: apply $H$ (which maps $|+\rangle \mapsto |0\rangle$ and $|-\rangle \mapsto |1\rangle$), then measure in $Z$. Reading outcome $0$ means "the state was $|+\rangle$."</p>

<div class="ckp-definition">
  <div class="ckp-def-label">Change of Basis = Rotate, Then Measure</div>
  <p>Measuring in the basis $\{U^{\dagger}|0\rangle,\, U^{\dagger}|1\rangle\}$ is the same as applying $U$ and measuring in the computational basis. Every "exotic" measurement is a unitary followed by the only measurement you actually have.</p>
</div>

<h3>The Experiment That Kills the Coin Analogy</h3>

<p>Prepare $|0\rangle$. Apply $H$. Measure. You get $0$ or $1$ with probability $\tfrac12$ each. So far, this is a fair coin, and you might reasonably conclude that $H$ "randomises" the qubit.</p>

<p>Now do it again — but apply $H$ <em>twice</em> before measuring.</p>

<p>You get $0$. Always. With certainty. Every single run.</p>

<p>Flip a fair coin, then flip it again: still fair. Randomise a bit, then randomise it again: still random. Classical randomisation is a one-way street — you cannot un-randomise. But $H^2 = I$, and so the qubit after the first $H$ was <em>never random at all</em>. It was in the perfectly definite state $|+\rangle$, which the second $H$ maps deterministically back to $|0\rangle$.</p>

<p>Let us watch the cancellation happen. The two applications of $H$ create two computational <em>paths</em> from the input $|0\rangle$ to each output, and we sum the amplitudes along them:</p>

<figure class="ckp-circuit">
<svg viewBox="0 0 780 285" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Path diagram showing constructive and destructive interference in the H-H circuit">
  <text class="qc-col" x="90"  y="34">input</text>
  <text class="qc-col" x="320" y="34">after H</text>
  <text class="qc-col" x="550" y="34">after H · H</text>

  <line class="qc-edge" x1="90"  y1="95"  x2="320" y2="95"/>
  <line class="qc-edge" x1="90"  y1="95"  x2="320" y2="205"/>
  <line class="qc-edge" x1="320" y1="95"  x2="550" y2="95"/>
  <line class="qc-edge" x1="320" y1="95"  x2="550" y2="205"/>
  <line class="qc-edge" x1="320" y1="205" x2="550" y2="95"/>
  <line class="qc-edge-neg" x1="320" y1="205" x2="550" y2="205"/>

  <circle class="qc-node" cx="90"  cy="95"  r="24"/>
  <text class="qc-nodetxt" x="90"  y="95">|0⟩</text>
  <circle class="qc-node" cx="320" cy="95"  r="24"/>
  <text class="qc-nodetxt" x="320" y="95">|0⟩</text>
  <circle class="qc-node" cx="320" cy="205" r="24"/>
  <text class="qc-nodetxt" x="320" y="205">|1⟩</text>
  <circle class="qc-node" cx="550" cy="95"  r="24"/>
  <text class="qc-nodetxt" x="550" y="95">|0⟩</text>
  <circle class="qc-node" cx="550" cy="205" r="24"/>
  <text class="qc-nodetxt" x="550" y="205">|1⟩</text>

  <text class="qc-amp" x="205" y="78">+1/√2</text>
  <text class="qc-amp" x="196" y="163">+1/√2</text>
  <text class="qc-amp" x="435" y="78">+1/√2</text>
  <text class="qc-amp" x="368" y="130">+1/√2</text>
  <text class="qc-amp" x="372" y="170">+1/√2</text>
  <text class="qc-amp qc-neg" x="435" y="224">−1/√2</text>

  <text class="qc-res qc-pos"     x="592" y="86">+½ + ½ = 1</text>
  <text class="qc-res-sub qc-pos" x="592" y="106">constructive</text>
  <text class="qc-res qc-neg"     x="592" y="196">+½ − ½ = 0</text>
  <text class="qc-res-sub qc-neg" x="592" y="216">destructive</text>

  <text class="qc-foot" x="390" y="266">Pr[0] = |1|² = 1        Pr[1] = |0|² = 0</text>
</svg>
<figcaption>Interference in the $H \cdot H$ circuit. Two paths reach the output $|0\rangle$, both with amplitude $+\tfrac12$: they reinforce. Two paths reach $|1\rangle$, with amplitudes $+\tfrac12$ and $-\tfrac12$: they annihilate. The single negative entry of the Hadamard matrix is doing all the work.</figcaption>
</figure>

<p>Written out algebraically, with $H|0\rangle = \tfrac{1}{\sqrt2}(|0\rangle + |1\rangle)$ and $H|1\rangle = \tfrac{1}{\sqrt2}(|0\rangle - |1\rangle)$:</p>

<div class="ckp-eq">
  <span class="eq-label">Destructive Interference — Eq. (6)</span>
  $$H\bigl(H|0\rangle\bigr) = \tfrac{1}{\sqrt2}\Bigl[\tfrac{1}{\sqrt2}\bigl(|0\rangle + |1\rangle\bigr) + \tfrac{1}{\sqrt2}\bigl(|0\rangle - |1\rangle\bigr)\Bigr] = \tfrac{1}{2}\bigl(2|0\rangle + 0 \cdot |1\rangle\bigr) = |0\rangle \tag{6}$$
</div>

<p>The $|1\rangle$ terms carry coefficients $+\tfrac12$ and $-\tfrac12$ and vanish. <strong>That</strong> is a quantum computation. Everything else — Deutsch, Simon, Grover, Shor — is this trick, scaled up and made to do useful work.</p>

<h3>Superposition Is Not Ignorance</h3>

<p>The $H \cdot H$ experiment refutes a specific, tempting, and wrong belief: that after the first $H$ the qubit "is really" $0$ or $1$, and we merely do not know which. If that were true, no subsequent operation could restore $|0\rangle$ with certainty. The information was never lost, because it was never randomised — only <em>rotated</em>.</p>

<p>To make this airtight, it helps to introduce the density matrix, which is the correct tool for distinguishing "in superposition" from "in an unknown one of two states."</p>

<div class="ckp-eq">
  <span class="eq-label">Coherent Superposition vs. Classical Mixture — Eq. (7)</span>
  $$\rho_{+} = |+\rangle\langle +| = \frac{1}{2}\begin{pmatrix} 1 &amp; 1 \\ 1 &amp; 1 \end{pmatrix}
  \qquad\text{versus}\qquad
  \rho_{\text{mix}} = \tfrac12|0\rangle\langle 0| + \tfrac12|1\rangle\langle 1| = \frac{1}{2}\begin{pmatrix} 1 &amp; 0 \\ 0 &amp; 1 \end{pmatrix} \tag{7}$$
</div>

<p>Both matrices have the same diagonal, so both give $50/50$ statistics when measured in the computational basis. They are <em>not</em> the same state. The difference lives entirely in the off-diagonal entries, which are called <strong>coherences</strong>. Apply $H$ to each: the left one becomes $|0\rangle\langle 0|$ and yields the outcome $0$ with certainty. The right one is $\tfrac12 I$, which is invariant under every unitary, and stays $50/50$ forever.</p>

<div class="ckp-callout warn">
  <strong>What Decoherence Actually Is</strong>
  <p>Decoherence — the central enemy of every quantum engineer alive — is precisely the process that drives those off-diagonal entries toward zero. It converts the left matrix in Eq. (7) into the right one.</p>
  <p>When that happens, your qubit has not "become noisy" in some vague sense. It has become a classical random bit. Coherences are what interference consumes; destroy them and your quantum computer is an expensive random number generator.</p>
</div>

<h3>Projective Measurement, Stated Properly</h3>

<p>For completeness, the general rule. A projective measurement is a family of orthogonal projectors $\{P_m\}$ with $\sum_m P_m = I$. Outcome $m$ occurs with probability $\langle\psi|P_m|\psi\rangle$, and the post-measurement state is $P_m|\psi\rangle / \sqrt{\langle\psi|P_m|\psi\rangle}$.</p>

<p>For a single-qubit $Z$ measurement, $P_0 = |0\rangle\langle 0|$ and $P_1 = |1\rangle\langle 1|$, and this reduces to Eq. (3). The value of the general form is that it applies unchanged when you measure <em>one qubit out of many</em> — which is exactly what happens in every real circuit, and what produces entanglement's strangest behaviour.</p>
</section>

<div class="ckp-sep">Composition</div>

<!-- ─── SECTION 4 ─────────────────────────────────────────── -->
<section id="sec-multi">
<h2>4. Many Qubits, Tensor Products, and Entanglement</h2>

<p>One qubit is a warm-up. The exponential arrives when you put qubits together.</p>

<h3>The Tensor Product</h3>

<p>If system $A$ has state space $\mathcal{H}_A = \mathbb{C}^2$ and system $B$ has $\mathcal{H}_B = \mathbb{C}^2$, the joint system has state space $\mathcal{H}_A \otimes \mathcal{H}_B = \mathbb{C}^4$. Note: <em>tensor</em> product, not Cartesian product. Dimensions multiply; they do not add.</p>

<div class="ckp-eq">
  <span class="eq-label">Two-Qubit Basis — Eq. (8)</span>
  $$|00\rangle,\ |01\rangle,\ |10\rangle,\ |11\rangle \quad\longleftrightarrow\quad e_0,\ e_1,\ e_2,\ e_3 \in \mathbb{C}^4 \tag{8}$$
</div>

<p>Concretely, the Kronecker product does what you expect:</p>

<div class="ckp-eq">
  <span class="eq-label">Kronecker Product — Eq. (9)</span>
  $$\begin{pmatrix} a_0 \\ a_1 \end{pmatrix} \otimes \begin{pmatrix} b_0 \\ b_1 \end{pmatrix}
  = \begin{pmatrix} a_0 b_0 \\ a_0 b_1 \\ a_1 b_0 \\ a_1 b_1 \end{pmatrix} \tag{9}$$
</div>

<p>An $n$-qubit register therefore lives in $\mathbb{C}^{2^n}$ and is described by $2^n$ complex amplitudes:</p>

<div class="ckp-eq">
  <span class="eq-label">$n$-Qubit State — Eq. (10)</span>
  $$|\psi\rangle = \sum_{x \in \{0,1\}^n} \alpha_x\,|x\rangle, \qquad \sum_x |\alpha_x|^2 = 1 \tag{10}$$
</div>

<p>Fifty qubits carry $2^{50} \approx 10^{15}$ amplitudes; three hundred carry more amplitudes than there are atoms in the observable universe. This is the number everyone quotes. Keep Holevo in mind while you quote it: you may still only read $n$ bits out.</p>

<div class="ckp-callout warn">
  <strong>Practical Trap: Qubit Ordering Conventions</strong>
  <p>In this article, and in most textbooks, $|q_0 q_1 \dots q_{n-1}\rangle$ lists qubit $0$ leftmost (most significant), so the basis state $|10\rangle$ means $q_0 = 1,\ q_1 = 0$, and it is index $2$ of the vector.</p>
  <p><strong style="display:inline; text-transform:none; letter-spacing:normal; font-family:var(--font-serif); font-size:0.92rem; color:var(--text);">Qiskit reverses this.</strong> Qiskit is little-endian: it prints $|q_{n-1} \dots q_1 q_0\rangle$, so qubit $0$ is <em>rightmost</em>. Apply <code>qc.x(0)</code> to a two-qubit register in Qiskit and the state vector prints as $|01\rangle$, not $|10\rangle$.</p>
  <p>Neither convention is wrong; mixing them silently is. Every single person who works with quantum circuits loses an afternoon to this exactly once. Consider this your afternoon.</p>
</div>

<h3>Product States versus Entangled States</h3>

<p>Some two-qubit states factor:</p>

<div class="ckp-eq">
  <span class="eq-label">Product State — Eq. (11)</span>
  $$|\Psi\rangle = |\psi_A\rangle \otimes |\psi_B\rangle \tag{11}$$
</div>

<p>Such a state carries no correlation at all: measuring $A$ tells you nothing new about $B$. A state that <strong>cannot</strong> be written in this form is called <em>entangled</em>. The canonical example is the Bell state:</p>

<div class="ckp-eq">
  <span class="eq-label">Bell State $|\Phi^{+}\rangle$ — Eq. (12)</span>
  $$|\Phi^{+}\rangle = \tfrac{1}{\sqrt{2}}\bigl(|00\rangle + |11\rangle\bigr) \tag{12}$$
</div>

<p>That this does not factor is a two-line exercise, and worth doing once by hand.</p>

<div class="ckp-callout key">
  <strong>Proof: $|\Phi^{+}\rangle$ Is Not a Product State</strong>
  <p>Suppose it were. Then for some $a,b,c,d \in \mathbb{C}$,</p>
  <p style="text-align:center;">$\bigl(a|0\rangle + b|1\rangle\bigr) \otimes \bigl(c|0\rangle + d|1\rangle\bigr) = ac|00\rangle + ad|01\rangle + bc|10\rangle + bd|11\rangle = \tfrac{1}{\sqrt2}\bigl(|00\rangle + |11\rangle\bigr).$</p>
  <p>Comparing coefficients: $ad = 0$ and $bc = 0$, while $ac = bd = \tfrac{1}{\sqrt2} \neq 0$. From $ad = 0$, either $a = 0$ or $d = 0$. If $a = 0$ then $ac = 0$, a contradiction. If $d = 0$ then $bd = 0$, a contradiction. Hence no such factorisation exists. $\blacksquare$</p>
  <p>Notice what this proof is <em>not</em>: it is not about distance, particles, or physics. It is a statement about rank. A two-qubit state, written as a $2 \times 2$ coefficient matrix, is a product state precisely when that matrix has rank $1$. Entanglement is rank $\geq 2$. That is all it ever was.</p>
</div>

<h3>The Four Bell States</h3>

<p>They form an orthonormal basis of $\mathbb{C}^4$ — the <em>Bell basis</em> — and every one of them is maximally entangled.</p>

<div class="ckp-eq">
  <span class="eq-label">Bell Basis — Eq. (13)</span>
  $$|\Phi^{\pm}\rangle = \tfrac{1}{\sqrt2}\bigl(|00\rangle \pm |11\rangle\bigr), \qquad
    |\Psi^{\pm}\rangle = \tfrac{1}{\sqrt2}\bigl(|01\rangle \pm |10\rangle\bigr) \tag{13}$$
</div>

<p>The state $|\Psi^{-}\rangle$ is the <em>singlet</em>, the star of Bell-inequality experiments [<a href="#ref-Bell1964">Bell1964</a>] and of the companion article in this series.</p>

<h3>Why You Cannot Signal With Entanglement</h3>

<p>Alice holds qubit $A$ of $|\Phi^{+}\rangle$; Bob holds $B$, a galaxy away. If Alice measures and gets $0$, Bob's qubit "instantly becomes" $|0\rangle$. Does that transmit information?</p>

<p>No — and the density matrix says exactly why. Alice's <em>local</em> description of her own qubit is the reduced state, obtained by tracing out Bob:</p>

<div class="ckp-eq">
  <span class="eq-label">Reduced State of Half a Bell Pair — Eq. (14)</span>
  $$\rho_A = \operatorname{Tr}_B\bigl(|\Phi^{+}\rangle\langle\Phi^{+}|\bigr) = \tfrac12|0\rangle\langle 0| + \tfrac12|1\rangle\langle 1| = \tfrac{1}{2}\,I \tag{14}$$
</div>

<p>The maximally mixed state. A perfect coin. And crucially, $\rho_A$ <em>does not depend on anything Bob does</em> — not on whether he measures, nor on which basis he chooses. Every local statistic Alice can compute is a function of $\rho_A$ alone, so nothing Bob does can change what she sees. The correlations only become visible when the two of them compare notes over a classical channel, which travels at most at the speed of light.</p>

<div class="ckp-definition">
  <div class="ckp-def-label">The Hierarchy Worth Memorising</div>
  <p>Every product state is a joint state. Not every joint state is a product state — the ones that are not are <em>entangled</em>. Entanglement is a property of the joint state, not of either part; each part, taken alone, is simply mixed. Maximal entanglement means each part alone is <em>maximally</em> mixed, i.e. carries no information at all.</p>
</div>

<div class="ckp-callout key">
  <strong>Why Entanglement, Not Superposition, Is the Structural Notion</strong>
  <p>Recall from Section 2 that "being in superposition" is basis-relative — every state is a superposition in some basis. Entanglement is different: it is basis-<em>independent</em>. A state is either a product state or it is not, and no change of local basis can turn one into the other.</p>
  <p>This is why entanglement earns a place in the theory and "superposition" does not, quite. And it is why, in Section 9, the honest question turns out not to be "does this circuit entangle?" but something considerably sharper.</p>
</div>
</section>

<div class="ckp-sep">Gates</div>

<!-- ─── SECTION 5 ─────────────────────────────────────────── -->
<section id="sec-unitary">
<h2>5. Gates Are Unitary Matrices — and Why That Forces Everything</h2>

<p>A quantum gate on $n$ qubits is a unitary matrix $U \in \mathbb{C}^{2^n \times 2^n}$, meaning $U^{\dagger}U = U U^{\dagger} = I$. It acts on the state by ordinary matrix–vector multiplication: $|\psi\rangle \mapsto U|\psi\rangle$.</p>

<p>This is not an arbitrary design choice. It is forced.</p>

<h3>The Two-Line Derivation</h3>

<div class="ckp-callout key">
  <strong>Theorem: Norm-Preserving + Linear $\Rightarrow$ Unitary</strong>
  <p>Suppose $U$ is linear and $\|U\psi\| = \|\psi\|$ for every $\psi \in \mathbb{C}^N$ (it must be, or probabilities would stop summing to one). Then</p>
  <p style="text-align:center;">$\langle \psi | (U^{\dagger}U - I) | \psi\rangle = \|U\psi\|^2 - \|\psi\|^2 = 0 \quad\text{for all } \psi.$</p>
  <p>Over $\mathbb{C}$, an operator $M$ with $\langle\psi|M|\psi\rangle = 0$ for all $\psi$ is the zero operator (apply the polarisation identity). Hence $U^{\dagger}U = I$. $\blacksquare$</p>
  <p>Linearity is a postulate of quantum mechanics. Norm preservation is forced by the Born rule. Unitarity is the consequence — and everything below is, in turn, a consequence of unitarity.</p>
</div>

<h3>Consequence 1: Every Gate Is Reversible</h3>

<p>If $U$ is unitary, $U^{-1} = U^{\dagger}$ exists and is itself unitary. So <em>every</em> quantum gate can be undone, exactly, by another quantum gate. There is no quantum gate that "forgets" its input.</p>

<p>This has a sharp consequence for anyone coming from classical computing: <strong>there is no quantum AND gate</strong> in the naive sense. Classical AND maps two bits to one; it is not injective; it destroys information. A quantum circuit simply cannot do that. The only irreversible step available to you is measurement — and measurement ends the coherent computation.</p>

<h3>Consequence 2: Classical Functions Must Be Embedded Reversibly</h3>

<p>Suppose you want a quantum circuit to evaluate some classical function $f : \{0,1\}^n \to \{0,1\}^m$ — AES, SHA-256, a modular exponentiation, whatever. You cannot simply "run the code." You must build a reversible embedding, standardly:</p>

<div class="ckp-eq">
  <span class="eq-label">Standard Oracle Embedding — Eq. (15)</span>
  $$U_f\,|x\rangle \otimes |y\rangle = |x\rangle \otimes |y \oplus f(x)\rangle \tag{15}$$
</div>

<p>This is a permutation of the computational basis (apply it twice and you are back where you started, since $y \oplus f(x) \oplus f(x) = y$), hence unitary, hence legal. It is called the <em>oracle</em> for $f$, and it is how every quantum algorithm in the literature accesses a classical function.</p>

<div class="ckp-callout warn">
  <strong>What This Costs You — And Why Cryptographers Should Care</strong>
  <p>Reversibility is not free. Classical circuits discard intermediate values constantly; quantum circuits cannot. Every scratch bit becomes an <em>ancilla qubit</em> that must be carried along, and — critically — must be <em>uncomputed</em> before it can be reused or discarded, because leftover ancillas remain entangled with your register and destroy the interference you were trying to arrange.</p>
  <p>The upshot: a quantum circuit for AES is dramatically more expensive than an AES chip. When you read that "Grover halves the security of AES-128," the honest version is "Grover requires roughly $2^{64}$ <em>sequential</em> evaluations of a fully reversible, error-corrected AES circuit." Those are wildly different statements, and only the second one is a cost model.</p>
</div>

<h3>Consequence 3: The No-Cloning Theorem</h3>

<p>This is the result on which quantum cryptography is built, and it falls straight out of linearity.</p>

<div class="ckp-callout key">
  <strong>Theorem (Wootters–Zurek, Dieks, 1982): Quantum States Cannot Be Copied</strong>
  <p>Suppose a unitary $U$ existed with $U\bigl(|\psi\rangle \otimes |0\rangle\bigr) = |\psi\rangle \otimes |\psi\rangle$ for <em>every</em> state $|\psi\rangle$. Take any two states $|\psi\rangle, |\phi\rangle$. Unitaries preserve inner products, so comparing the inner product of the inputs with that of the outputs:</p>
  <p style="text-align:center;">$\langle\psi|\phi\rangle \cdot \underbrace{\langle 0|0\rangle}_{=\,1} \;=\; \langle\psi|\phi\rangle\langle\psi|\phi\rangle \;=\; \langle\psi|\phi\rangle^2.$</p>
  <p>So $z = z^2$ where $z = \langle\psi|\phi\rangle$, forcing $z \in \{0, 1\}$: the two states are either orthogonal or identical. A cloner can therefore work on a set of <em>mutually orthogonal</em> states — but no unitary clones an arbitrary unknown state. $\blacksquare$ [<a href="#ref-WZ1982">WZ1982</a>, <a href="#ref-Dieks1982">Dieks1982</a>]</p>
</div>

<p>Notice how little was needed: linearity, unitarity, and an inner product. No physics.</p>

<div class="ckp-callout">
  <strong>Why This Is the Foundation of Quantum Key Distribution</strong>
  <p>In BB84 [<a href="#ref-BB84">BB84</a>], Alice sends qubits encoded at random in either the $Z$ basis $\{|0\rangle,|1\rangle\}$ or the $X$ basis $\{|+\rangle,|-\rangle\}$. These four states are <em>not</em> mutually orthogonal — $|0\rangle$ and $|+\rangle$ overlap — so by the theorem above, no device can copy them all.</p>
  <p>An eavesdropper cannot grab a copy and decide later. She must measure, and to measure she must guess a basis. Guess wrong and she irreversibly disturbs the state, injecting detectable errors into Alice and Bob's key. Security comes from a theorem of linear algebra, not from an assumption that some problem is hard. This is what "information-theoretic security" means, and it is why QKD is qualitatively different from RSA.</p>
</div>
</section>

<div class="ckp-sep">The Gate Zoo</div>

<!-- ─── SECTION 6 ─────────────────────────────────────────── -->
<section id="sec-gates">
<h2>6. The Gate Zoo</h2>

<p>You will meet perhaps a dozen gates in practice. Here they are, with their matrices. Learn the matrices; the names are just labels.</p>

<h3>6.1 The Pauli Gates</h3>

<div class="ckp-eq">
  <span class="eq-label">Pauli Matrices — Eq. (16)</span>
  $$X = \begin{pmatrix} 0 &amp; 1 \\ 1 &amp; 0 \end{pmatrix}, \quad
    Y = \begin{pmatrix} 0 &amp; -i \\ i &amp; 0 \end{pmatrix}, \quad
    Z = \begin{pmatrix} 1 &amp; 0 \\ 0 &amp; -1 \end{pmatrix} \tag{16}$$
</div>

<p>$X$ is the quantum NOT: $X|0\rangle = |1\rangle$, $X|1\rangle = |0\rangle$. It is a <em>bit flip</em>.</p>

<p>$Z$ leaves $|0\rangle$ alone and sends $|1\rangle \mapsto -|1\rangle$. It is a <em>phase flip</em>. It does absolutely nothing observable to $|0\rangle$ or $|1\rangle$ — and yet it swaps $|+\rangle \leftrightarrow |-\rangle$, which are perfectly distinguishable. A gate that is invisible in one basis can be maximally violent in another. Internalise that.</p>

<p>$Y = iXZ$ does both at once. The three Paulis together with $I$ span all $2\times 2$ Hermitian matrices over $\mathbb{R}$, they each square to $I$, and they pairwise anticommute: $XY = -YX = iZ$, and cyclic permutations thereof.</p>

<h3>6.2 Hadamard: The Basis Changer</h3>

<div class="ckp-eq">
  <span class="eq-label">Hadamard — Eq. (17)</span>
  $$H = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 &amp; 1 \\ 1 &amp; -1 \end{pmatrix}
    = \frac{X + Z}{\sqrt{2}} \tag{17}$$
</div>

<p>$H|0\rangle = |+\rangle$, $H|1\rangle = |-\rangle$, and $H^2 = I$. It maps the $Z$ basis to the $X$ basis and back. Nearly every quantum algorithm opens with a layer of Hadamards — $H^{\otimes n}|0\rangle^{\otimes n}$ produces the uniform superposition over all $2^n$ strings — and closes with another layer, which is where the interference is cashed in.</p>

<p>Two identities you will use constantly:</p>

<div class="ckp-eq">
  <span class="eq-label">Hadamard Conjugation — Eq. (18)</span>
  $$H X H = Z, \qquad H Z H = X, \qquad H Y H = -Y \tag{18}$$
</div>

<p>In words: <em>Hadamard exchanges bit flips and phase flips.</em> This is the single most useful algebraic fact in elementary quantum computing, and it is a thirty-second matrix multiplication to verify.</p>

<h3>6.3 Phase Gates: $S$, $T$, and $P(\varphi)$</h3>

<div class="ckp-eq">
  <span class="eq-label">Phase Gates — Eq. (19)</span>
  $$P(\varphi) = \begin{pmatrix} 1 &amp; 0 \\ 0 &amp; e^{i\varphi} \end{pmatrix}, \qquad
    S = P(\tfrac{\pi}{2}) = \begin{pmatrix} 1 &amp; 0 \\ 0 &amp; i \end{pmatrix}, \qquad
    T = P(\tfrac{\pi}{4}) = \begin{pmatrix} 1 &amp; 0 \\ 0 &amp; e^{i\pi/4} \end{pmatrix} \tag{19}$$
</div>

<p>These apply a relative phase to the $|1\rangle$ component and nothing else. Note $T^2 = S$ and $S^2 = Z$, so $T$ is the "eighth root of the identity" in a precise sense: $T^8 = I$.</p>

<p>The $T$ gate looks like the most boring object on this page. It is, in fact, the most expensive gate in the entire subject, and Section 9 explains why.</p>

<h3>6.4 Rotations</h3>

<p>For any Pauli $P \in \{X,Y,Z\}$ (each satisfying $P^2 = I$), the exponential series splits cleanly:</p>

<div class="ckp-eq">
  <span class="eq-label">Pauli Rotations — Eq. (20)</span>
  $$R_P(\theta) = e^{-i\theta P/2} = \cos\tfrac{\theta}{2}\,I \;-\; i\sin\tfrac{\theta}{2}\,P \tag{20}$$
</div>

<p>which gives the three familiar matrices:</p>

<div class="ckp-eq">
  <span class="eq-label">Explicit Rotations — Eq. (21)</span>
  $$R_x(\theta) = \begin{pmatrix} \cos\tfrac{\theta}{2} &amp; -i\sin\tfrac{\theta}{2} \\[2pt] -i\sin\tfrac{\theta}{2} &amp; \cos\tfrac{\theta}{2} \end{pmatrix},\quad
    R_y(\theta) = \begin{pmatrix} \cos\tfrac{\theta}{2} &amp; -\sin\tfrac{\theta}{2} \\[2pt] \sin\tfrac{\theta}{2} &amp; \cos\tfrac{\theta}{2} \end{pmatrix},\quad
    R_z(\theta) = \begin{pmatrix} e^{-i\theta/2} &amp; 0 \\[2pt] 0 &amp; e^{i\theta/2} \end{pmatrix} \tag{21}$$
</div>

<p>These are literally rotations of the Bloch sphere about the $x$, $y$, and $z$ axes, by angle $\theta$. The factor of $\tfrac12$ in the exponent is the Bloch-angle-is-half-the-Hilbert-angle business again — a $2\pi$ rotation returns $-I$, not $I$, which is the famous spinor sign and is (being a global phase) physically invisible.</p>

<div class="ckp-definition">
  <div class="ckp-def-label">Z–Y–Z Decomposition</div>
  <p>Every single-qubit unitary can be written $U = e^{i\alpha}\,R_z(\beta)\,R_y(\gamma)\,R_z(\delta)$ for real $\alpha,\beta,\gamma,\delta$. Three rotations and a phase — that is the whole of $U(2)$. So a hardware vendor who gives you $R_z$ and $R_y$ (or in practice $R_z$ and $\sqrt{X}$) has given you every single-qubit gate there is.</p>
</div>

<h3>6.5 Two-Qubit Gates</h3>

<p>The workhorse is the controlled-NOT. In the basis $(|00\rangle, |01\rangle, |10\rangle, |11\rangle)$, with qubit $0$ as control:</p>

<div class="ckp-eq">
  <span class="eq-label">CNOT — Eq. (22)</span>
  $$\mathrm{CNOT} = \begin{pmatrix}
  1 &amp; 0 &amp; 0 &amp; 0 \\
  0 &amp; 1 &amp; 0 &amp; 0 \\
  0 &amp; 0 &amp; 0 &amp; 1 \\
  0 &amp; 0 &amp; 1 &amp; 0
  \end{pmatrix}, \qquad |a, b\rangle \;\mapsto\; |a,\ b \oplus a\rangle \tag{22}$$
</div>

<p>It flips the target iff the control is $|1\rangle$. On basis states it is exactly the classical XOR-into-target. On superpositions it is the gate that creates entanglement.</p>

<p>More generally, for any single-qubit unitary $U$, the controlled-$U$ gate is the block matrix</p>

<div class="ckp-eq">
  <span class="eq-label">Controlled-$U$ — Eq. (23)</span>
  $$\mathrm{C}U \;=\; |0\rangle\langle 0| \otimes I \;+\; |1\rangle\langle 1| \otimes U
  \;=\; \begin{pmatrix} I &amp; 0 \\ 0 &amp; U \end{pmatrix} \tag{23}$$
</div>

<p>Taking $U = Z$ gives the controlled-$Z$ gate, $\mathrm{CZ} = \operatorname{diag}(1,1,1,-1)$, which is <em>symmetric</em> in control and target — there is no way to tell which qubit is which. That surprises people, and it is a good sanity check on whether you are thinking in matrices or in metaphors.</p>

<p>And since $HZH = X$, conjugating the target of a CZ by Hadamards produces a CNOT:</p>

<div class="ckp-eq">
  <span class="eq-label">CNOT from CZ — Eq. (24)</span>
  $$\mathrm{CNOT} = (I \otimes H)\,\mathrm{CZ}\,(I \otimes H) \tag{24}$$
</div>

<p>This is not a curiosity. Superconducting hardware often implements CZ natively, and the compiler turns your CNOTs into Eq. (24) without telling you.</p>

<h3>6.6 Three-Qubit Gates</h3>

<p>The <strong>Toffoli</strong> gate (CCX) flips the target iff <em>both</em> controls are $|1\rangle$: $|a,b,c\rangle \mapsto |a,\,b,\,c \oplus (a \wedge b)\rangle$. It is the reversible AND, and it is universal for classical reversible computation — anything a classical circuit can do, a circuit of Toffolis can do reversibly. It is also the gate in which quantum resource estimates for cryptanalysis are usually denominated.</p>

<p>The <strong>Fredkin</strong> gate (CSWAP) swaps two targets iff the control is $|1\rangle$. It is also classically universal.</p>

<h3>6.7 The Reference Table</h3>

<div class="ckp-table-wrap">
<table class="ckp-table wide">
<thead>
  <tr>
    <th>Gate</th>
    <th>Matrix</th>
    <th>Action</th>
    <th>Notes</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><span class="term">$X$</span></td>
    <td>$\begin{pmatrix} 0 &amp; 1 \\ 1 &amp; 0\end{pmatrix}$</td>
    <td>Bit flip; $\pi$ rotation about $x$</td>
    <td>Quantum NOT. Clifford.</td>
  </tr>
  <tr>
    <td><span class="term">$Y$</span></td>
    <td>$\begin{pmatrix} 0 &amp; -i \\ i &amp; 0\end{pmatrix}$</td>
    <td>Bit + phase flip</td>
    <td>$Y = iXZ$. Clifford.</td>
  </tr>
  <tr>
    <td><span class="term">$Z$</span></td>
    <td>$\begin{pmatrix} 1 &amp; 0 \\ 0 &amp; -1\end{pmatrix}$</td>
    <td>Phase flip</td>
    <td>Invisible on $|0\rangle,|1\rangle$. Clifford.</td>
  </tr>
  <tr>
    <td><span class="term">$H$</span></td>
    <td>$\tfrac{1}{\sqrt2}\begin{pmatrix} 1 &amp; 1 \\ 1 &amp; -1\end{pmatrix}$</td>
    <td>$Z$ basis $\leftrightarrow$ $X$ basis</td>
    <td>Creates superposition. $H^2 = I$. Clifford.</td>
  </tr>
  <tr>
    <td><span class="term">$S$</span></td>
    <td>$\begin{pmatrix} 1 &amp; 0 \\ 0 &amp; i\end{pmatrix}$</td>
    <td>Quarter phase turn</td>
    <td>$S^2 = Z$. Clifford.</td>
  </tr>
  <tr>
    <td><span class="term">$T$</span></td>
    <td>$\begin{pmatrix} 1 &amp; 0 \\ 0 &amp; e^{i\pi/4}\end{pmatrix}$</td>
    <td>Eighth phase turn</td>
    <td><strong>Non-Clifford.</strong> $T^2 = S$. The expensive one.</td>
  </tr>
  <tr>
    <td><span class="term">$R_z(\theta)$</span></td>
    <td>$\operatorname{diag}\bigl(e^{-i\theta/2},\, e^{i\theta/2}\bigr)$</td>
    <td>Rotation about $z$</td>
    <td>Continuous family; $S,T,Z$ are special cases.</td>
  </tr>
  <tr>
    <td><span class="term">CNOT</span></td>
    <td>$\begin{pmatrix} I &amp; 0 \\ 0 &amp; X\end{pmatrix}$</td>
    <td>$|a,b\rangle \mapsto |a, b \oplus a\rangle$</td>
    <td>Entangling. Clifford.</td>
  </tr>
  <tr>
    <td><span class="term">CZ</span></td>
    <td>$\operatorname{diag}(1,1,1,-1)$</td>
    <td>Phase $-1$ on $|11\rangle$</td>
    <td>Symmetric in control/target. Clifford.</td>
  </tr>
  <tr>
    <td><span class="term">SWAP</span></td>
    <td>$\begin{pmatrix} 1 &amp; 0 &amp; 0 &amp; 0 \\ 0 &amp; 0 &amp; 1 &amp; 0 \\ 0 &amp; 1 &amp; 0 &amp; 0 \\ 0 &amp; 0 &amp; 0 &amp; 1\end{pmatrix}$</td>
    <td>$|a,b\rangle \mapsto |b,a\rangle$</td>
    <td>Equals three CNOTs. Not entangling.</td>
  </tr>
  <tr>
    <td><span class="term">Toffoli</span></td>
    <td>$8\times 8$ permutation</td>
    <td>$|a,b,c\rangle \mapsto |a,b,\,c \oplus ab\rangle$</td>
    <td>Reversible AND. Non-Clifford. Costed in attacks.</td>
  </tr>
</tbody>
</table>
</div>
</section>

<div class="ckp-sep">Circuits</div>

<!-- ─── SECTION 7 ─────────────────────────────────────────── -->
<section id="sec-circuits">
<h2>7. Constructing Circuits</h2>

<p>A quantum circuit is a picture of a matrix product. That is the whole idea, and if you hold onto it you will never be confused by a circuit diagram again.</p>

<h3>Anatomy</h3>

<figure class="ckp-circuit">
<svg viewBox="0 0 700 220" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Anatomy of a quantum circuit: wires, single-qubit gate, two-qubit gate, rotation, measurement, classical wire">
  <line class="qc-wire" x1="62" y1="80"  x2="640" y2="80"/>
  <line class="qc-wire" x1="62" y1="150" x2="640" y2="150"/>

  <text class="qc-ket" x="36" y="80">|0⟩</text>
  <text class="qc-ket" x="36" y="150">|0⟩</text>

  <rect class="qc-box" x="96" y="58" width="44" height="44" rx="2"/>
  <text class="qc-txt" x="118" y="80">H</text>
  <circle class="qc-mk" cx="118" cy="30" r="10"/>
  <text class="qc-mknum" x="118" y="30">1</text>

  <line class="qc-link" x1="205" y1="80"  x2="205" y2="150"/>
  <circle class="qc-ctrl" cx="205" cy="80" r="6"/>
  <circle class="qc-tgt"  cx="205" cy="150" r="13"/>
  <line class="qc-link" x1="192" y1="150" x2="218" y2="150"/>
  <line class="qc-link" x1="205" y1="137" x2="205" y2="163"/>
  <circle class="qc-mk" cx="205" cy="30" r="10"/>
  <text class="qc-mknum" x="205" y="30">2</text>

  <rect class="qc-box" x="270" y="128" width="62" height="44" rx="2"/>
  <text class="qc-txt" x="301" y="150">Rz(θ)</text>
  <circle class="qc-mk" cx="301" cy="200" r="10"/>
  <text class="qc-mknum" x="301" y="200">3</text>

  <rect class="qc-box-alt" x="392" y="58" width="52" height="44" rx="2"/>
  <path class="qc-meter" d="M 404 90 A 14 14 0 0 1 432 90"/>
  <line class="qc-meter" x1="418" y1="90" x2="430" y2="72"/>
  <circle class="qc-mk" cx="418" cy="30" r="10"/>
  <text class="qc-mknum" x="418" y="30">4</text>

  <line class="qc-cwire" x1="444" y1="77" x2="640" y2="77"/>
  <line class="qc-cwire" x1="444" y1="83" x2="640" y2="83"/>
  <circle class="qc-mk" cx="545" cy="45" r="10"/>
  <text class="qc-mknum" x="545" y="45">5</text>

  <line class="qc-time" x1="62" y1="206" x2="628" y2="206"/>
  <path class="qc-timehead" d="M 630 206 L 619 202 L 619 210 Z"/>
  <text class="qc-lbl qc-lbl-s" x="644" y="206">time</text>
</svg>
<figcaption>
① Single-qubit gate — a $2\times2$ unitary. &nbsp; ② Two-qubit gate: filled dot = control, ⊕ = target. &nbsp; ③ A parametrised rotation. &nbsp; ④ Measurement — the only irreversible element. &nbsp; ⑤ Double line = classical bit. Time runs left to right; each horizontal wire is one qubit persisting through time, <em>not</em> a physical path.
</figcaption>
</figure>

<div class="ckp-callout warn">
  <strong>The Ordering Trap Everyone Falls Into Once</strong>
  <p>Circuits read <em>left to right</em>. Matrix products compose <em>right to left</em>. So the circuit "first $A$, then $B$, then $C$" corresponds to the operator</p>
  <p style="text-align:center;">$U = C \cdot B \cdot A$ &nbsp;&nbsp;— <em>not</em> $A \cdot B \cdot C$.</p>
  <p>The order is reversed, because $C(B(A|\psi\rangle))$ applies $A$ first. Write it out once, slowly, and then never think about it again.</p>
</div>

<h3>Gates in Parallel Are Tensor Products</h3>

<p>Two gates acting on different qubits at the same moment combine with $\otimes$. If you apply $H$ to qubit $0$ of a two-qubit register and nothing to qubit $1$, the operator on the full space is <strong>not</strong> $H$ — it is</p>

<div class="ckp-eq">
  <span class="eq-label">Identity Padding — Eq. (25)</span>
  $$H \otimes I = \frac{1}{\sqrt2}\begin{pmatrix}
  1 &amp; 0 &amp; 1 &amp; 0 \\
  0 &amp; 1 &amp; 0 &amp; 1 \\
  1 &amp; 0 &amp; -1 &amp; 0 \\
  0 &amp; 1 &amp; 0 &amp; -1
  \end{pmatrix} \tag{25}$$
</div>

<p>"Doing nothing" to a qubit is an operation — the identity — and it must appear explicitly in the tensor product. Every gate in an $n$-qubit circuit is secretly a $2^n \times 2^n$ matrix, padded with identities on the wires it does not touch.</p>

<h3>Worked Example: Building a Bell Pair</h3>

<p>Two gates. Watch every amplitude.</p>

<figure class="ckp-circuit">
<svg viewBox="0 0 660 230" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Bell pair circuit: Hadamard on qubit zero followed by CNOT">
  <line class="qc-stage" x1="88"  y1="32" x2="88"  y2="178"/>
  <line class="qc-stage" x1="188" y1="32" x2="188" y2="178"/>
  <line class="qc-stage" x1="330" y1="32" x2="330" y2="178"/>

  <line class="qc-wire" x1="66" y1="75"  x2="400" y2="75"/>
  <line class="qc-wire" x1="66" y1="145" x2="400" y2="145"/>

  <text class="qc-ket" x="40" y="75">|0⟩</text>
  <text class="qc-ket" x="40" y="145">|0⟩</text>

  <rect class="qc-box" x="110" y="53" width="44" height="44" rx="2"/>
  <text class="qc-txt" x="132" y="75">H</text>

  <line class="qc-link" x1="250" y1="75" x2="250" y2="145"/>
  <circle class="qc-ctrl" cx="250" cy="75" r="6"/>
  <circle class="qc-tgt"  cx="250" cy="145" r="13"/>
  <line class="qc-link" x1="237" y1="145" x2="263" y2="145"/>
  <line class="qc-link" x1="250" y1="132" x2="250" y2="158"/>

  <text class="qc-out" x="418" y="110">(|00⟩ + |11⟩)/√2</text>

  <text class="qc-lbl" x="88"  y="198">|ψ₀⟩</text>
  <text class="qc-lbl" x="188" y="198">|ψ₁⟩</text>
  <text class="qc-lbl" x="330" y="198">|ψ₂⟩</text>
</svg>
<figcaption>The Bell-pair circuit. A Hadamard on the control, then a CNOT. Two gates, and the output cannot be written as any product of two single-qubit states.</figcaption>
</figure>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr>
    <th>Stage</th>
    <th>Operator applied</th>
    <th>State</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><span class="term">$|\psi_0\rangle$</span></td>
    <td>—</td>
    <td>$|00\rangle$</td>
  </tr>
  <tr>
    <td><span class="term">$|\psi_1\rangle$</span></td>
    <td>$H \otimes I$</td>
    <td>$\tfrac{1}{\sqrt2}\bigl(|0\rangle + |1\rangle\bigr) \otimes |0\rangle \;=\; \tfrac{1}{\sqrt2}\bigl(|00\rangle + |10\rangle\bigr)$</td>
  </tr>
  <tr>
    <td><span class="term">$|\psi_2\rangle$</span></td>
    <td>$\mathrm{CNOT}$</td>
    <td>$\tfrac{1}{\sqrt2}\bigl(|00\rangle + |11\rangle\bigr) \;=\; |\Phi^{+}\rangle$</td>
  </tr>
</tbody>
</table>
</div>

<p>The CNOT acted <em>linearly</em> on the superposition: it left $|00\rangle$ alone and mapped $|10\rangle \mapsto |11\rangle$. It did not "choose" a branch. It processed both terms, because it is a matrix, and matrices do not choose.</p>

<p>As a whole the circuit is the single unitary $U = \mathrm{CNOT} \cdot (H \otimes I)$ — note the reversed order. And here is a fact worth knowing: fed the four computational basis states, this one circuit outputs the four Bell states.</p>

<div class="ckp-eq">
  <span class="eq-label">The Circuit Is a Change of Basis — Eq. (26)</span>
  $$|00\rangle \mapsto |\Phi^{+}\rangle, \quad |01\rangle \mapsto |\Psi^{+}\rangle, \quad |10\rangle \mapsto |\Phi^{-}\rangle, \quad |11\rangle \mapsto |\Psi^{-}\rangle \tag{26}$$
</div>

<p>Run it backwards — CNOT, then $H$ — and you map the Bell basis onto the computational basis. That reversed circuit is the <em>Bell measurement</em>, and it is the engine of quantum teleportation and superdense coding. Both protocols are, at bottom, this three-gate circuit read in the two possible directions.</p>

<pre class="ckp-code"><span class="c"># Qiskit: the Bell pair, and the endianness trap</span>
<span class="k">from</span> qiskit <span class="k">import</span> QuantumCircuit
<span class="k">from</span> qiskit.quantum_info <span class="k">import</span> Statevector

qc = <span class="f">QuantumCircuit</span>(2)
qc.<span class="f">h</span>(0)          <span class="c"># qubit 0 -> |+></span>
qc.<span class="f">cx</span>(0, 1)      <span class="c"># CNOT: control 0, target 1</span>

<span class="f">print</span>(<span class="f">Statevector</span>(qc).data)
<span class="c"># [0.70710678+0.j, 0.+0.j, 0.+0.j, 0.70710678+0.j]   ->  (|00> + |11>)/sqrt(2)</span>

<span class="c"># Careful: Qiskit is little-endian. Try this and read the output twice:</span>
qc2 = <span class="f">QuantumCircuit</span>(2)
qc2.<span class="f">x</span>(0)
<span class="f">print</span>(<span class="f">Statevector</span>(qc2).<span class="f">draw</span>(<span class="s">'latex_source'</span>))   <span class="c"># |01>, not |10></span>
</pre>

<h3>Circuit Identities Are Just Matrix Algebra</h3>

<p>Because circuits are products of matrices, you can <em>prove</em> circuit equivalences rather than guess at them. Three you will use forever:</p>

<ul class="ckp-hier">
  <li><strong>$H X H = Z$.</strong> A bit flip sandwiched between Hadamards is a phase flip. Compilers use this constantly to move gates past each other.</li>
  <li><strong>$(H \otimes H)\,\mathrm{CNOT}_{0 \to 1}\,(H \otimes H) = \mathrm{CNOT}_{1 \to 0}$.</strong> Conjugating a CNOT by Hadamards on <em>both</em> qubits reverses control and target. If your hardware only offers CNOT in one direction, this is how you get the other.</li>
  <li><strong>$\mathrm{SWAP} = \mathrm{CNOT}_{0\to1}\,\mathrm{CNOT}_{1\to0}\,\mathrm{CNOT}_{0\to1}$.</strong> The classic three-XOR swap, now in superposition. On hardware with limited connectivity, chains of SWAPs are how distant qubits are brought together — and they are a major hidden cost.</li>
</ul>

<h3>Depth, Width, and the Real Cost Model</h3>

<p>Two numbers describe a circuit's size. <strong>Width</strong> is the number of qubits. <strong>Depth</strong> is the number of time steps — layers of gates that must happen in sequence. Depth, not gate count, is what races against your qubits' coherence time.</p>

<p>But for cryptographic resource estimation, neither is the headline figure. The number that matters is the <strong>T-count</strong> (or equivalently the Toffoli count), and Section 9 explains why a gate that looks like a diagonal $2\times2$ matrix ends up dominating the cost of breaking RSA.</p>

<div class="ckp-callout">
  <strong>The Deferred Measurement Principle</strong>
  <p>You will sometimes see circuits that measure a qubit mid-way and then apply a gate conditioned on the classical outcome. This is always avoidable: any such circuit can be rewritten with all measurements pushed to the very end, replacing each classically-controlled gate with a quantum-controlled one.</p>
  <p>Consequence: you may always <em>analyse</em> a circuit as "one big unitary, then measure everything." Real hardware often prefers mid-circuit measurement for practical reasons, but the mathematics never requires it.</p>
</div>
</section>

<div class="ckp-sep">Interference at Work</div>

<!-- ─── SECTION 8 ─────────────────────────────────────────── -->
<section id="sec-deutsch">
<h2>8. Interference at Work: Deutsch's Algorithm</h2>

<p>Time to see the whole machine run. Deutsch's algorithm [<a href="#ref-Deutsch1985">Deutsch1985</a>] is the smallest problem on which a quantum computer provably beats a classical one, and it exhibits every idea in this tutorial in about six gates.</p>

<h3>The Problem</h3>

<p>You are given an oracle for an unknown function $f : \{0,1\} \to \{0,1\}$. There are four such functions: two are <em>constant</em> ($f \equiv 0$ or $f \equiv 1$) and two are <em>balanced</em> ($f(x) = x$ or $f(x) = \bar{x}$). Determine which class $f$ belongs to.</p>

<p>Classically you must query the oracle twice: knowing $f(0)$ alone tells you nothing about the class. Quantum mechanically, <strong>one query suffices</strong>.</p>

<h3>The Trick: Phase Kickback</h3>

<p>Recall the standard oracle from Eq. (15): $U_f|x\rangle|y\rangle = |x\rangle|y \oplus f(x)\rangle$. Now feed the target register the state $|-\rangle$ instead of a basis state, and compute:</p>

<div class="ckp-eq">
  <span class="eq-label">Phase Kickback — Eq. (27)</span>
  $$U_f\,\bigl(|x\rangle \otimes |-\rangle\bigr) \;=\; |x\rangle \otimes \tfrac{1}{\sqrt2}\bigl(|0 \oplus f(x)\rangle - |1 \oplus f(x)\rangle\bigr) \;=\; (-1)^{f(x)}\,|x\rangle \otimes |-\rangle \tag{27}$$
</div>

<p>Check both cases. If $f(x) = 0$ the target is unchanged and the factor is $+1$. If $f(x) = 1$ the two terms swap, giving $\tfrac{1}{\sqrt2}(|1\rangle - |0\rangle) = -|-\rangle$, and the factor is $-1$.</p>

<p>Read Eq. (27) again, because it is the most important line in this article. The oracle was supposed to write $f(x)$ into the <em>target</em> register. Instead, the target came out completely unchanged — and the value of $f(x)$ appeared as a <strong>phase on the control register</strong>. The function's output has been converted from a bit into a sign.</p>

<p>And signs, unlike bits, can cancel.</p>

<div class="ckp-pull">
  <p>Phase kickback is the hinge on which quantum algorithms turn. It takes a value you cannot use — a bit sitting in a register you are not going to read — and converts it into a phase you can interfere with. Every quantum speedup in the literature does some version of this.</p>
  <cite>— Why Eq. (27) is worth memorising</cite>
</div>

<h3>The Circuit</h3>

<figure class="ckp-circuit">
<svg viewBox="0 0 700 230" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Deutsch algorithm circuit with two Hadamards, an oracle, a final Hadamard and a measurement">
  <line class="qc-stage" x1="88"  y1="32" x2="88"  y2="196"/>
  <line class="qc-stage" x1="180" y1="32" x2="180" y2="196"/>
  <line class="qc-stage" x1="350" y1="32" x2="350" y2="196"/>
  <line class="qc-stage" x1="448" y1="32" x2="448" y2="196"/>

  <line class="qc-wire" x1="72" y1="78"  x2="620" y2="78"/>
  <line class="qc-wire" x1="72" y1="152" x2="500" y2="152"/>

  <text class="qc-ket" x="46" y="78">|0⟩</text>
  <text class="qc-ket" x="46" y="152">|1⟩</text>

  <rect class="qc-box" x="104" y="56" width="44" height="44" rx="2"/>
  <text class="qc-txt" x="126" y="78">H</text>
  <rect class="qc-box" x="104" y="130" width="44" height="44" rx="2"/>
  <text class="qc-txt" x="126" y="152">H</text>

  <rect class="qc-box-alt" x="215" y="46" width="104" height="138" rx="2"/>
  <text class="qc-txt-alt" x="267" y="112">U<tspan font-size="11" dy="4">f</tspan></text>

  <rect class="qc-box" x="378" y="56" width="44" height="44" rx="2"/>
  <text class="qc-txt" x="400" y="78">H</text>

  <rect class="qc-box-alt" x="470" y="56" width="52" height="44" rx="2"/>
  <path class="qc-meter" d="M 482 88 A 14 14 0 0 1 510 88"/>
  <line class="qc-meter" x1="496" y1="88" x2="508" y2="70"/>

  <line class="qc-cwire" x1="522" y1="75" x2="614" y2="75"/>
  <line class="qc-cwire" x1="522" y1="81" x2="614" y2="81"/>
  <text class="qc-out" x="624" y="78">0 / 1</text>

  <text class="qc-lbl qc-lbl-s" x="512" y="152">|−⟩ unchanged</text>

  <text class="qc-lbl" x="88"  y="212">|ψ₀⟩</text>
  <text class="qc-lbl" x="180" y="212">|ψ₁⟩</text>
  <text class="qc-lbl" x="350" y="212">|ψ₂⟩</text>
  <text class="qc-lbl" x="448" y="212">|ψ₃⟩</text>
</svg>
<figcaption>Deutsch's algorithm. The ancilla enters as $|1\rangle$, is Hadamarded to $|-\rangle$, and leaves completely untouched — it exists solely to enable the phase kickback of Eq. (27). Outcome $0$ means $f$ is constant; outcome $1$ means $f$ is balanced.</figcaption>
</figure>

<h3>The Walkthrough</h3>

<div class="ckp-chain">

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">0</div>
    <div class="ckp-chain-content">
      <h4>Prepare</h4>
      <p>$|\psi_0\rangle = |0\rangle \otimes |1\rangle$. The ancilla starts in $|1\rangle$, not $|0\rangle$ — that is deliberate.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">1</div>
    <div class="ckp-chain-content">
      <h4>Hadamard Both</h4>
      <p>$|\psi_1\rangle = |+\rangle \otimes |-\rangle = \tfrac{1}{\sqrt2}\bigl(|0\rangle + |1\rangle\bigr) \otimes |-\rangle$. The control is now a uniform superposition over both inputs to $f$; the ancilla is primed for kickback.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">2</div>
    <div class="ckp-chain-content">
      <h4>Query the Oracle — Once</h4>
      <p>By Eq. (27), applied linearly to both terms: $|\psi_2\rangle = \tfrac{1}{\sqrt2}\bigl((-1)^{f(0)}|0\rangle + (-1)^{f(1)}|1\rangle\bigr) \otimes |-\rangle$. Factoring out the (unobservable) global phase $(-1)^{f(0)}$, the control register is $\tfrac{1}{\sqrt2}\bigl(|0\rangle + (-1)^{f(0) \oplus f(1)}|1\rangle\bigr)$.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">3</div>
    <div class="ckp-chain-content">
      <h4>Interfere</h4>
      <p>The control is $|+\rangle$ if $f(0) \oplus f(1) = 0$ and $|-\rangle$ if $f(0) \oplus f(1) = 1$. The final Hadamard maps $|+\rangle \mapsto |0\rangle$ and $|-\rangle \mapsto |1\rangle$, so $|\psi_3\rangle$ is a computational basis state — <em>with certainty</em>.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">4</div>
    <div class="ckp-chain-content">
      <h4>Measure</h4>
      <p>Outcome $0$ $\Rightarrow$ $f(0) = f(1)$, i.e. constant. Outcome $1$ $\Rightarrow$ $f(0) \neq f(1)$, i.e. balanced. No randomness, no repetition, one oracle call.</p>
    </div>
  </div>

</div>

<pre class="ckp-code"><span class="c"># Qiskit: Deutsch's algorithm end to end</span>
<span class="k">from</span> qiskit <span class="k">import</span> QuantumCircuit

<span class="k">def</span> <span class="f">deutsch</span>(oracle):
    qc = <span class="f">QuantumCircuit</span>(2, 1)
    qc.<span class="f">x</span>(1)                          <span class="c"># ancilla -> |1></span>
    qc.<span class="f">h</span>([0, 1])                     <span class="c"># -> |+> (x) |-></span>
    qc.<span class="f">compose</span>(oracle, inplace=<span class="k">True</span>)  <span class="c"># the single query</span>
    qc.<span class="f">h</span>(0)                          <span class="c"># interfere the two paths</span>
    qc.<span class="f">measure</span>(0, 0)                  <span class="c"># 0 = constant, 1 = balanced</span>
    <span class="k">return</span> qc

constant = <span class="f">QuantumCircuit</span>(2)          <span class="c"># f(x) = 0  -> empty circuit</span>
balanced = <span class="f">QuantumCircuit</span>(2)
balanced.<span class="f">cx</span>(0, 1)                     <span class="c"># f(x) = x  -> a single CNOT</span>
</pre>

<h3>What Actually Happened Here</h3>

<p>Notice what you did <em>not</em> learn. You never found out $f(0)$. You never found out $f(1)$. Those values are simply not recoverable from the output — and if you tried to extract them you would need a second query anyway.</p>

<p>What you learned was a <em>global property</em> of $f$: the single bit $f(0) \oplus f(1)$. The superposition let the oracle touch both inputs; the phase kickback turned the outputs into signs; the final Hadamard made those signs interfere so that the answer to the global question landed, deterministically, on one basis state.</p>

<div class="ckp-callout key">
  <strong>The Template for Every Quantum Algorithm</strong>
  <p>Look at the shape of what we just did. It generalises almost verbatim:</p>
  <p><strong style="display:inline; text-transform:none; letter-spacing:normal; font-family:var(--font-serif); font-size:0.92rem; color:var(--text);">Spread</strong> — Hadamards create a uniform superposition over the input space. &nbsp;<strong style="display:inline; text-transform:none; letter-spacing:normal; font-family:var(--font-serif); font-size:0.92rem; color:var(--text);">Mark</strong> — the oracle imprints information about $f$ into <em>phases</em>. &nbsp;<strong style="display:inline; text-transform:none; letter-spacing:normal; font-family:var(--font-serif); font-size:0.92rem; color:var(--text);">Interfere</strong> — a final transform makes wrong answers cancel and right answers reinforce. &nbsp;<strong style="display:inline; text-transform:none; letter-spacing:normal; font-family:var(--font-serif); font-size:0.92rem; color:var(--text);">Measure</strong> — sample once.</p>
  <p>Deutsch–Jozsa [<a href="#ref-DJ1992">DJ1992</a>] scales this to $n$ bits. Simon's algorithm [<a href="#ref-Simon1997">Simon1997</a>] uses the same skeleton to find a hidden XOR-mask exponentially faster than any classical method — and it was Simon's paper that directly inspired Shor. Shor [<a href="#ref-Shor1997">Shor1997</a>] replaces the final Hadamard with the quantum Fourier transform, so that the interference reveals the <em>period</em> of a function; the period of $a^x \bmod N$ is what factors $N$. Grover [<a href="#ref-Grover1996">Grover1996</a>] alternates "mark" and "reflect" steps to rotate amplitude gradually onto the marked item.</p>
  <p>Different transforms, same skeleton. Learn the skeleton.</p>
</div>
</section>

<div class="ckp-sep">Universality</div>

<!-- ─── SECTION 9 ─────────────────────────────────────────── -->
<section id="sec-universal">
<h2>9. Universality, and What Is Actually Hard</h2>

<p>Two questions now demand answers. Which gates do you need? And — the question almost nobody asks — <em>which gates are expensive?</em></p>

<h3>Universal Gate Sets</h3>

<p>A set of gates is <strong>universal</strong> if any unitary on any number of qubits can be approximated to arbitrary accuracy by circuits built from that set.</p>

<ul class="ckp-hier">
  <li><strong>CNOT + all single-qubit gates</strong> is universal. Any $n$-qubit unitary decomposes into these [<a href="#ref-Barenco1995">Barenco1995</a>]. This is a <em>continuous</em> set, which is awkward for fault tolerance.</li>
  <li><strong>$\{H,\, T,\, \mathrm{CNOT}\}$</strong> is universal — and finite. Three gates. This is the standard set for fault-tolerant architectures, and the one you should have in your head.</li>
  <li><strong>$\{H,\, \mathrm{Toffoli}\}$</strong> is also universal, which is a small marvel: two real-valued gates suffice, no complex numbers required anywhere.</li>
</ul>

<div class="ckp-definition">
  <div class="ckp-def-label">Solovay–Kitaev Theorem</div>
  <p>If a finite gate set generates a dense subgroup of $SU(2)$, then any single-qubit unitary can be approximated to within $\varepsilon$ using $O\bigl(\log^{c}(1/\varepsilon)\bigr)$ gates from that set, with a small constant $c$ [<a href="#ref-DN2005">DN2005</a>]. The cost of discreteness is merely <em>polylogarithmic</em> — which is why a finite gate set costs you essentially nothing.</p>
</div>

<h3>The Result That Should Change Your Mind</h3>

<p>Here is where most introductions stop, and where the interesting part begins.</p>

<p>Define the <strong>Clifford group</strong> as the set of unitaries generated by $\{H,\, S,\, \mathrm{CNOT}\}$. (Equivalently: the unitaries that map Pauli operators to Pauli operators under conjugation. Eq. (18), $HXH = Z$, is exactly an instance of that.) Clifford circuits can prepare Bell states. They can prepare GHZ states on a thousand qubits. They generate <em>maximal</em> entanglement, and they are the backbone of every quantum error-correcting code.</p>

<div class="ckp-callout key">
  <strong>Gottesman–Knill Theorem</strong>
  <p>Any circuit consisting only of Clifford gates, preparation of computational basis states, and measurement in the computational basis can be simulated <em>in polynomial time on a classical computer</em> [<a href="#ref-Gottesman1998">Gottesman1998</a>, <a href="#ref-AG2004">AG2004</a>].</p>
  <p>Read that again with Section 4 in mind. Clifford circuits produce vast amounts of entanglement — and your laptop can simulate them efficiently.</p>
</div>

<p>The conclusion is unavoidable, and it contradicts what nearly every popular account will tell you:</p>

<div class="ckp-pull">
  <p>Entanglement is necessary for quantum speedup, but it is nowhere near sufficient. A circuit can entangle a thousand qubits maximally and still be simulable on a laptop in polynomial time. If entanglement were the resource, Gottesman–Knill would be impossible.</p>
  <cite>— The correction that separates the informed from the enthusiastic</cite>
</div>

<p>To be precise about the "necessary" half: for pure-state quantum computation, an exponential speedup does require entanglement that grows without bound with the problem size [<a href="#ref-JL2003">JL2003</a>]. So entanglement is a genuine prerequisite. It is simply not the thing that makes the problem hard for a classical simulator.</p>

<h3>So What Is the Resource? Magic.</h3>

<p>Add a single $T$ gate to a Clifford circuit and the Gottesman–Knill machinery breaks. Classical simulation cost grows exponentially in the number of $T$ gates. The technical name for the property that $T$ supplies — and that Clifford gates cannot manufacture — is <strong>magic</strong>, or non-stabilizerness [<a href="#ref-BK2005">BK2005</a>].</p>

<p>This is not a naming curiosity. It reaches all the way down into hardware, and all the way out into your threat model.</p>

<div class="ckp-callout warn">
  <strong>Why the $T$ Gate Costs So Much More Than the Others</strong>
  <p>In the surface code — the leading approach to fault tolerance — Clifford gates are comparatively cheap: they can be implemented by moving and merging patches of qubits (lattice surgery) without ever leaving the protected code space.</p>
  <p>The $T$ gate cannot be done this way. It requires <em>magic state distillation</em>: a whole subroutine that consumes many noisy ancillas to produce one sufficiently clean $|T\rangle$ resource state. Historically, magic state factories have dominated the space–time cost of a fault-tolerant machine.</p>
  <p>This is why serious resource estimates for quantum attacks are quoted in <strong>T-counts and Toffoli counts</strong>, not in "number of gates." A cryptographer reading a paper claiming "$N$ qubits break RSA" and not asking about the Toffoli count is reading only half of the cost.</p>
</div>

<div class="ckp-definition">
  <div class="ckp-def-label">The Hierarchy Worth Carrying Away</div>
  <p>Superposition alone: classically simulable. Superposition plus entanglement (Clifford): still classically simulable, by Gottesman–Knill. Superposition plus entanglement plus magic: this is where quantum computation finally becomes something a classical computer cannot follow — and it is also where the engineering becomes brutally expensive.</p>
</div>
</section>

<div class="ckp-sep">Consequences for Cryptography</div>

<!-- ─── SECTION 10 ────────────────────────────────────────── -->
<section id="sec-crypto">
<h2>10. What This All Means for Cryptography</h2>

<p>Now we can state the cryptographic implications precisely, rather than dramatically.</p>

<h3>Shor: Public-Key Cryptography Is Structurally Broken</h3>

<p>Shor's algorithm [<a href="#ref-Shor1997">Shor1997</a>] finds the period of $x \mapsto a^x \bmod N$ using the quantum Fourier transform as its interference step, and period-finding yields the factorisation of $N$. The same machinery solves discrete logarithms. Therefore RSA, finite-field Diffie–Hellman, DSA, ECDH, and ECDSA all fall to a sufficiently large fault-tolerant quantum computer — not by brute force, but by a polynomial-time algorithm.</p>

<p>There is no parameter increase that saves them. Doubling the RSA modulus roughly cubes the work for Shor; it does not change the asymptotics. This is why <em>migration</em>, not <em>bigger keys</em>, is the answer.</p>

<h3>How Much Machine Would It Take?</h3>

<p>Here the abstractions of this article become numbers. In 2019, Gidney and Ekerå estimated that factoring a 2048-bit RSA modulus would need about 20 million noisy physical qubits running for roughly 8 hours [<a href="#ref-GE2019">GE2019</a>]. In 2025, Gidney sharply revised this: <strong>fewer than one million noisy qubits, in under a week</strong> [<a href="#ref-Gidney2025">Gidney2025</a>] — a twentyfold reduction in qubit count, achieved not by better hardware but by better <em>circuits</em>.</p>

<p>Look at where the improvement came from, because it validates everything in Section 9: approximate residue arithmetic, denser storage of idle logical qubits, and a cheaper way of producing magic states. The headline gain was a reduction of the <em>Toffoli count</em> by more than two orders of magnitude. The bottleneck was never "qubits." It was magic.</p>

<div class="ckp-stat-row">
  <div class="ckp-stat"><span class="stat-num">20M</span><span class="stat-label">Physical qubits for RSA-2048 (2019 estimate)</span></div>
  <div class="ckp-stat"><span class="stat-num">&lt;1M</span><span class="stat-label">Physical qubits for RSA-2048 (2025 estimate)</span></div>
  <div class="ckp-stat"><span class="stat-num">~100</span><span class="stat-label">Logical qubits demonstrated as of 2026</span></div>
  <div class="ckp-stat"><span class="stat-num">$\sim$10³</span><span class="stat-label">Logical qubits a real attack would need</span></div>
</div>

<h3>Grover: Symmetric Cryptography Is Bruised, Not Broken</h3>

<p>Grover's algorithm [<a href="#ref-Grover1996">Grover1996</a>] searches an unstructured space of size $N$ in $O(\sqrt{N})$ queries, and this is provably optimal [<a href="#ref-BBBV1997">BBBV1997</a>]. Applied to key search, it takes AES-128 from $2^{128}$ to about $2^{64}$ <em>iterations</em>. That sounds catastrophic. It is not, for three reasons that every cryptographer should be able to recite:</p>

<ul class="ckp-hier">
  <li><strong>Each iteration is expensive.</strong> One Grover iteration requires a full, reversible, error-corrected AES circuit — including all the ancilla management and uncomputation from Section 5. This is not one AES evaluation; it is an AES evaluation running inside a fault-tolerant machine, and the constant factor is enormous.</li>
  <li><strong>Grover barely parallelises.</strong> Running $M$ quantum machines in parallel gives you only a $\sqrt{M}$ speedup, not $M$. Classical brute force parallelises linearly. So you cannot buy your way out of the $2^{64}$ <em>sequential</em> depth — and that serial chain must maintain coherence throughout.</li>
  <li><strong>Doubling the key restores everything.</strong> AES-256 under Grover retains roughly $2^{128}$ security, which is out of reach for any physically plausible machine. This is why NIST's post-quantum security categories are anchored to AES and why the mitigation is a one-line configuration change, not a redesign.</li>
</ul>

<p>Hash functions are similar. Preimage search gets a square-root speedup; <em>collision</em> finding does not meaningfully improve over the classical birthday attack once the enormous quantum memory requirements of the known algorithms are costed honestly. SHA-256 remains, in practice, a 128-bit collision-resistant hash.</p>

<h3>The Migration Already Under Way</h3>

<p>NIST published its first post-quantum standards on 13 August 2024: <strong>FIPS 203</strong> (ML-KEM, from CRYSTALS-Kyber, for key encapsulation), <strong>FIPS 204</strong> (ML-DSA, from CRYSTALS-Dilithium, for signatures), and <strong>FIPS 205</strong> (SLH-DSA, from SPHINCS+, a hash-based signature backup) [<a href="#ref-NIST2024">NIST2024</a>]. In March 2025 NIST selected <strong>HQC</strong>, a code-based KEM, as a diversity backup for ML-KEM in case lattice assumptions are ever weakened. A FALCON-based signature standard (FN-DSA, FIPS 206) remains in development.</p>

<div class="ckp-callout warn">
  <strong>Harvest Now, Decrypt Later</strong>
  <p>The reason the migration cannot wait for the hardware is straightforward. An adversary can record encrypted traffic <em>today</em> and decrypt it whenever a cryptographically relevant quantum computer arrives. Any secret whose confidentiality must outlive the machine — state secrets, medical records, long-lived identity keys — is already exposed if it travels under RSA or ECDH.</p>
  <p>The quantum computer does not need to exist yet for the attack to be under way. It only needs to exist before the data stops mattering.</p>
</div>

<h3>An Honest Reality Check</h3>

<p>As of 2026, error-corrected quantum computing has crossed from theory into engineering — Google's Willow processor demonstrated that logical error rates fall <em>exponentially</em> as the surface-code distance grows [<a href="#ref-Google2025">Google2025</a>], which is the threshold result the whole field was waiting for. Several groups have now demonstrated on the order of a hundred logical qubits.</p>

<p>A cryptographically relevant machine needs on the order of a few thousand logical qubits, sustained for billions of sequential operations. The gap is large — several orders of magnitude — and it is an engineering gap, not a physics gap. That is precisely why the migration timelines are what they are: nobody credible claims RSA falls next year, and nobody credible claims it never falls.</p>

<div class="ckp-callout">
  <strong>The Other Direction: Cryptography <em>From</em> Quantum Mechanics</strong>
  <p>Quantum information does not only attack cryptography; it supplies primitives that classical physics cannot. No-cloning (Section 5) gives BB84 and quantum key distribution, whose security rests on physics rather than on computational hardness. Bell-inequality violation certifies randomness <em>device-independently</em> — you can prove your random number generator is unpredictable without trusting its manufacturer, which no classical construction can do. Both are direct consequences of the linear algebra in this article.</p>
</div>
</section>

<div class="ckp-sep">How to Think Correctly</div>

<!-- ─── SECTION 11 ────────────────────────────────────────── -->
<section id="sec-think">
<h2>11. How to Think Correctly: The Misconception Table</h2>

<p>Everything above, compressed into the errors it is designed to prevent. If you retain one section of this article, retain this one.</p>

<div class="ckp-table-wrap">
<table class="ckp-table wide">
<thead>
  <tr>
    <th>The Slogan</th>
    <th>Why It Misleads</th>
    <th>Think Instead</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><span class="bad">"A qubit is 0 and 1 at the same time."</span></td>
    <td>Suggests a qubit holds two classical values. It holds neither.</td>
    <td>A qubit is a unit vector in $\mathbb{C}^2$. "Superposition" is a statement about a <em>basis</em>, not about the state.</td>
  </tr>
  <tr>
    <td><span class="bad">"Quantum computers try all answers in parallel."</span></td>
    <td>If true, NP-complete problems would be easy. They are not believed to be.</td>
    <td>One state vector evolves; one sample comes out. The work is arranging <em>cancellation</em> on wrong answers.</td>
  </tr>
  <tr>
    <td><span class="bad">"Superposition is just ignorance about which value it has."</span></td>
    <td>Then $H \cdot H$ could not restore $|0\rangle$ with certainty. It does.</td>
    <td>Compare $\rho_{+}$ and $\rho_{\text{mix}}$ in Eq. (7). The <em>coherences</em> are the difference, and they are physical.</td>
  </tr>
  <tr>
    <td><span class="bad">"Measurement reveals the value that was already there."</span></td>
    <td>Bell's theorem experimentally rules out local pre-assigned values [<a href="#ref-Bell1964">Bell1964</a>].</td>
    <td>Measurement is a basis-dependent, state-destroying operation governed by the Born rule.</td>
  </tr>
  <tr>
    <td><span class="bad">"Entanglement transmits information instantly."</span></td>
    <td>Alice's reduced state is $\tfrac12 I$ regardless of what Bob does — Eq. (14).</td>
    <td>Entanglement creates correlation, never signalling. Correlations are only visible after a classical comparison.</td>
  </tr>
  <tr>
    <td><span class="bad">"A qubit stores infinite information."</span></td>
    <td>$\alpha,\beta$ are continuous but inaccessible.</td>
    <td>Holevo: $n$ qubits yield at most $n$ classical bits, and the state is destroyed on readout.</td>
  </tr>
  <tr>
    <td><span class="bad">"Entanglement is what makes quantum computers fast."</span></td>
    <td>Clifford circuits entangle maximally and are classically simulable (Gottesman–Knill).</td>
    <td>Entanglement is necessary, not sufficient. The scarce resource is <em>magic</em> — the $T$ gates.</td>
  </tr>
  <tr>
    <td><span class="bad">"Global phase can be ignored, so all phases can."</span></td>
    <td>Conflates the unobservable global phase with the load-bearing relative phase.</td>
    <td>$e^{i\gamma}|\psi\rangle \equiv |\psi\rangle$. But $|+\rangle$ and $|-\rangle$ are perfectly distinguishable states.</td>
  </tr>
  <tr>
    <td><span class="bad">"Draw the two qubits as two Bloch vectors."</span></td>
    <td>Entangled states have <em>no</em> individual Bloch vectors — each part is mixed.</td>
    <td>The Bloch sphere is for one qubit. Beyond that: vectors, matrices, tensor products.</td>
  </tr>
  <tr>
    <td><span class="bad">"Quantum computers will break all encryption."</span></td>
    <td>Ignores that only structured problems (factoring, DLP) fall.</td>
    <td>Public-key falls to Shor. Symmetric and hash survive with doubled parameters. Lattice/code/hash-based schemes are the replacements.</td>
  </tr>
</tbody>
</table>
</div>

<h3>The Whole Picture in One Chain</h3>

<div class="ckp-chain">

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">1</div>
    <div class="ckp-chain-content">
      <h4>Change the Norm</h4>
      <p>Replace the 1-norm over $\mathbb{R}_{\geq 0}$ with the 2-norm over $\mathbb{C}$. States become unit vectors in $\mathbb{C}^{2^n}$; amplitudes may now be negative or complex.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">2</div>
    <div class="ckp-chain-content">
      <h4>Unitarity Follows</h4>
      <p>Linearity plus norm preservation forces every gate to be unitary. Unitarity forces reversibility, which forces oracles and ancillas — and forbids cloning.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">3</div>
    <div class="ckp-chain-content">
      <h4>Amplitudes Cancel</h4>
      <p>Because amplitudes carry signs and phases, two paths to the same outcome can annihilate. This — not superposition, not parallelism — is the resource.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">4</div>
    <div class="ckp-chain-content">
      <h4>Algorithms Are Interference Patterns</h4>
      <p>Spread with Hadamards, mark with phase kickback, interfere with a final transform, measure once. Deutsch, Simon, Grover, and Shor are all this skeleton with different transforms.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">5</div>
    <div class="ckp-chain-content">
      <h4>Entanglement Is Not the Bottleneck</h4>
      <p>Clifford circuits entangle maximally yet simulate classically in polynomial time. The scarce, expensive resource is magic — supplied by $T$ gates, priced in magic-state distillation.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">6</div>
    <div class="ckp-chain-content">
      <h4>Therefore, Cryptography</h4>
      <p>Shor kills RSA and ECC in polynomial time. Grover only dents symmetric primitives. The real cost of an attack is measured in Toffolis and magic states — which is exactly why the 2025 RSA estimate improved twentyfold with no new hardware at all.</p>
    </div>
  </div>

</div>
</section>

<div class="ckp-sep">Practice</div>

<!-- ─── EXERCISES ─────────────────────────────────────────── -->
<section id="sec-exercises">
<h2>Exercises</h2>

<p>Quantum information is not a spectator sport, and none of these require a computer. Pen, paper, and $2 \times 2$ matrices will do. When you want to go deeper, Nielsen and Chuang [<a href="#ref-NC2010">NC2010</a>] is the standard reference and its first four chapters cover everything above at greater length.</p>

<div class="ckp-exercise">
  <div class="ex-num">01</div>
  <div>
    <p>Verify $H|+\rangle = |0\rangle$ and $H|-\rangle = |1\rangle$ by direct matrix multiplication. Conclude that "measure in the $X$ basis" is implemented as "apply $H$, then measure in the $Z$ basis."</p>
  </div>
</div>

<div class="ckp-exercise">
  <div class="ex-num">02</div>
  <div>
    <p>Prove $HXH = Z$ and $HZH = X$. Then explain, using the Bloch sphere, why $H$ is a $180°$ rotation about the axis $\tfrac{1}{\sqrt2}(\hat{x} + \hat{z})$ — and why that makes $H^2 = I$ obvious without any multiplication.</p>
  </div>
</div>

<div class="ckp-exercise">
  <div class="ex-num">03</div>
  <div>
    <p>The gate $Z$ acts trivially on $|0\rangle$ (up to nothing at all) and on $|1\rangle$ (up to a global phase). Yet $Z$ is not the identity. Exhibit a single-qubit state and a measurement that distinguish $Z|\psi\rangle$ from $|\psi\rangle$ with certainty.</p>
    <p class="ex-hint">Hint: you have already seen the state. It is on the equator.</p>
  </div>
</div>

<div class="ckp-exercise">
  <div class="ex-num">04</div>
  <div>
    <p>Verify $\mathrm{SWAP} = \mathrm{CNOT}_{0\to1}\,\mathrm{CNOT}_{1\to0}\,\mathrm{CNOT}_{0\to1}$ by tracking all four computational basis states through the three gates. Then explain why this identity means SWAP creates no entanglement, despite being built entirely from entangling gates.</p>
  </div>
</div>

<div class="ckp-exercise">
  <div class="ex-num">05</div>
  <div>
    <p>Prove that the singlet $|\Psi^{-}\rangle = \tfrac{1}{\sqrt2}(|01\rangle - |10\rangle)$ is not a product state. Then write its $2\times2$ coefficient matrix and confirm that it has rank $2$ — connecting the algebraic proof to the rank characterisation of entanglement.</p>
  </div>
</div>

<div class="ckp-exercise">
  <div class="ex-num">06</div>
  <div>
    <p>Derive the phase-kickback identity of Eq. (27) from scratch for a general $f : \{0,1\}^n \to \{0,1\}$: show that $U_f\bigl(|x\rangle \otimes |-\rangle\bigr) = (-1)^{f(x)}|x\rangle \otimes |-\rangle$, and hence that $U_f\bigl(H^{\otimes n}|0\rangle^{\otimes n} \otimes |-\rangle\bigr)$ places the entire truth table of $f$ into phases.</p>
  </div>
</div>

<div class="ckp-exercise">
  <div class="ex-num">07</div>
  <div>
    <p>Show that a unitary <em>can</em> perfectly clone the pair $\{|0\rangle, |1\rangle\}$, and that a (different) unitary can perfectly clone $\{|+\rangle, |-\rangle\}$ — but that no single unitary clones all four. Explain in one sentence why this is exactly the security argument of BB84.</p>
  </div>
</div>

<div class="ckp-exercise">
  <div class="ex-num">08</div>
  <div>
    <p>Compute $\rho_A = \operatorname{Tr}_B\bigl(|\Phi^{+}\rangle\langle\Phi^{+}|\bigr)$ explicitly and confirm Eq. (14). Then argue that $\rho_A$ is unchanged whether Bob measures in the $Z$ basis, the $X$ basis, or not at all — and that this <em>is</em> the no-signalling theorem.</p>
  </div>
</div>

<div class="ckp-exercise">
  <div class="ex-num">09</div>
  <div>
    <p>(Superdense coding.) Alice holds qubit $A$ of $|\Phi^{+}\rangle$. Show that applying $I$, $X$, $Z$, or $ZX$ to her qubit alone maps the pair onto the four Bell states of Eq. (13). Since those are orthogonal, Bob can distinguish them perfectly with a Bell measurement. Conclude: one qubit, plus one pre-shared entangled pair, carries <em>two</em> classical bits.</p>
  </div>
</div>

<div class="ckp-exercise">
  <div class="ex-num">10</div>
  <div>
    <p>The GHZ state $\tfrac{1}{\sqrt2}(|000\rangle + |111\rangle)$ is maximally entangled across three qubits, and is produced by one $H$ and two CNOTs. All three gates are Clifford. In light of Gottesman–Knill, what exactly does this tell you about the claim "entanglement is the source of quantum computational power"?</p>
    <p class="ex-hint">This is the most important exercise on the list. If you can answer it in two sentences, you have understood Section 9.</p>
  </div>
</div>
</section>

<div class="ckp-sep">Quick Reference</div>

<!-- ─── GLOSSARY ────────────────────────────────────────────── -->
<section id="sec-glossary">
<h2>Quick Reference Glossary</h2>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr>
    <th>Term</th>
    <th>Definition</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><span class="term">Qubit</span></td>
    <td>A unit vector in $\mathbb{C}^2$, defined up to global phase. Equivalently, a point of $\mathbb{CP}^1$ — the Bloch sphere.</td>
  </tr>
  <tr>
    <td><span class="term">Amplitude</span></td>
    <td>A complex coefficient $\alpha_x$ in $|\psi\rangle = \sum_x \alpha_x|x\rangle$. Unlike a probability, it can be negative or complex — and can therefore cancel.</td>
  </tr>
  <tr>
    <td><span class="term">Born Rule</span></td>
    <td>$\Pr[x] = |\alpha_x|^2$. The bridge from amplitudes to observable statistics, and the only source of randomness in the theory.</td>
  </tr>
  <tr>
    <td><span class="term">Global Phase</span></td>
    <td>A factor $e^{i\gamma}$ multiplying the whole state. Physically undetectable; discard it freely.</td>
  </tr>
  <tr>
    <td><span class="term">Relative Phase</span></td>
    <td>A phase between components of a superposition. Fully physical; $|+\rangle$ and $|-\rangle$ differ only by one and are perfectly distinguishable.</td>
  </tr>
  <tr>
    <td><span class="term">Interference</span></td>
    <td>Amplitudes from distinct computational paths adding constructively or destructively. The one resource a classical probabilistic computer does not have.</td>
  </tr>
  <tr>
    <td><span class="term">Coherence</span></td>
    <td>The off-diagonal entries of the density matrix. What interference consumes; what decoherence destroys.</td>
  </tr>
  <tr>
    <td><span class="term">Entanglement</span></td>
    <td>A joint state that admits no factorisation $|\psi_A\rangle \otimes |\psi_B\rangle$. Basis-independent, unlike superposition.</td>
  </tr>
  <tr>
    <td><span class="term">Unitary</span></td>
    <td>A matrix with $U^{\dagger}U = I$. Every quantum gate is one; hence every gate is reversible.</td>
  </tr>
  <tr>
    <td><span class="term">Oracle $U_f$</span></td>
    <td>$|x\rangle|y\rangle \mapsto |x\rangle|y \oplus f(x)\rangle$ — the standard reversible embedding of a classical function.</td>
  </tr>
  <tr>
    <td><span class="term">Phase Kickback</span></td>
    <td>$U_f(|x\rangle \otimes |-\rangle) = (-1)^{f(x)}|x\rangle \otimes |-\rangle$. Converts a function's output bit into a phase that can interfere.</td>
  </tr>
  <tr>
    <td><span class="term">Ancilla</span></td>
    <td>A workspace qubit. Must be <em>uncomputed</em> before reuse, or its residual entanglement destroys the interference you need.</td>
  </tr>
  <tr>
    <td><span class="term">Clifford Group</span></td>
    <td>Unitaries generated by $\{H, S, \mathrm{CNOT}\}$; equivalently, those that map Paulis to Paulis. Entangling — yet classically simulable.</td>
  </tr>
  <tr>
    <td><span class="term">Gottesman–Knill</span></td>
    <td>Clifford circuits with computational-basis input and measurement are simulable in classical polynomial time.</td>
  </tr>
  <tr>
    <td><span class="term">Magic</span></td>
    <td>Non-stabilizerness — the property supplied by $T$ gates that Clifford operations cannot manufacture. The true scarce resource.</td>
  </tr>
  <tr>
    <td><span class="term">T-count</span></td>
    <td>The number of $T$ (or Toffoli) gates in a circuit. The currency in which fault-tolerant cost — and therefore quantum attack cost — is actually denominated.</td>
  </tr>
  <tr>
    <td><span class="term">No-Cloning</span></td>
    <td>No unitary copies an arbitrary unknown state. A two-line consequence of linearity; the foundation of QKD.</td>
  </tr>
  <tr>
    <td><span class="term">Holevo Bound</span></td>
    <td>At most $n$ classical bits can be extracted from $n$ qubits, however cleverly you measure.</td>
  </tr>
  <tr>
    <td><span class="term">Circuit Depth</span></td>
    <td>The number of sequential gate layers. Races directly against coherence time.</td>
  </tr>
  <tr>
    <td><span class="term">CRQC</span></td>
    <td>Cryptographically Relevant Quantum Computer — one large enough to run Shor against deployed key sizes. Requires on the order of thousands of logical qubits.</td>
  </tr>
</tbody>
</table>
</div>
</section>

<!-- ─── REFERENCES ─────────────────────────────────────────── -->
<div class="ckp-refs" id="references">
<h2>References</h2>
<p id="ref-NC2010"><span class="ref-num">[NC2010]</span> Nielsen, M.A., Chuang, I.L.: <em>Quantum Computation and Quantum Information</em>, 10th Anniversary Edition. Cambridge University Press (2010). The standard reference; Chapters 1–4 cover this article in depth.</p>
<p id="ref-Deutsch1985"><span class="ref-num">[Deutsch1985]</span> Deutsch, D.: Quantum theory, the Church–Turing principle and the universal quantum computer. <em>Proc. R. Soc. Lond. A</em> <strong>400</strong>, 97–117 (1985). <a href="https://doi.org/10.1098/rspa.1985.0070">doi:10.1098/rspa.1985.0070</a></p>
<p id="ref-DJ1992"><span class="ref-num">[DJ1992]</span> Deutsch, D., Jozsa, R.: Rapid solution of problems by quantum computation. <em>Proc. R. Soc. Lond. A</em> <strong>439</strong>, 553–558 (1992). <a href="https://doi.org/10.1098/rspa.1992.0167">doi:10.1098/rspa.1992.0167</a></p>
<p id="ref-Simon1997"><span class="ref-num">[Simon1997]</span> Simon, D.R.: On the power of quantum computation. <em>SIAM J. Comput.</em> <strong>26</strong>(5), 1474–1483 (1997). The paper that inspired Shor.</p>
<p id="ref-Shor1997"><span class="ref-num">[Shor1997]</span> Shor, P.W.: Polynomial-time algorithms for prime factorization and discrete logarithms on a quantum computer. <em>SIAM J. Comput.</em> <strong>26</strong>(5), 1484–1509 (1997). <a href="https://doi.org/10.1137/S0097539795293172">doi:10.1137/S0097539795293172</a></p>
<p id="ref-Grover1996"><span class="ref-num">[Grover1996]</span> Grover, L.K.: A fast quantum mechanical algorithm for database search. <em>Proc. 28th ACM STOC</em>, 212–219 (1996). <a href="https://doi.org/10.1145/237814.237866">doi:10.1145/237814.237866</a></p>
<p id="ref-BBBV1997"><span class="ref-num">[BBBV1997]</span> Bennett, C.H., Bernstein, E., Brassard, G., Vazirani, U.: Strengths and weaknesses of quantum computing. <em>SIAM J. Comput.</em> <strong>26</strong>(5), 1510–1523 (1997). Proves Grover's $\sqrt{N}$ is optimal — and that quantum computers do not simply solve NP.</p>
<p id="ref-Barenco1995"><span class="ref-num">[Barenco1995]</span> Barenco, A., Bennett, C.H., Cleve, R., DiVincenzo, D.P., Margolus, N., Shor, P., Sleator, T., Smolin, J.A., Weinfurter, H.: Elementary gates for quantum computation. <em>Phys. Rev. A</em> <strong>52</strong>, 3457–3467 (1995). <a href="https://doi.org/10.1103/PhysRevA.52.3457">doi:10.1103/PhysRevA.52.3457</a></p>
<p id="ref-DN2005"><span class="ref-num">[DN2005]</span> Dawson, C.M., Nielsen, M.A.: The Solovay–Kitaev algorithm. <em>Quantum Inf. Comput.</em> <strong>6</strong>(1), 81–95 (2006). <a href="https://arxiv.org/abs/quant-ph/0505030">arXiv:quant-ph/0505030</a></p>
<p id="ref-Gottesman1998"><span class="ref-num">[Gottesman1998]</span> Gottesman, D.: The Heisenberg representation of quantum computers. <em>Proc. XXII Int. Colloquium on Group Theoretical Methods in Physics</em>, 32–43 (1999). <a href="https://arxiv.org/abs/quant-ph/9807006">arXiv:quant-ph/9807006</a></p>
<p id="ref-AG2004"><span class="ref-num">[AG2004]</span> Aaronson, S., Gottesman, D.: Improved simulation of stabilizer circuits. <em>Phys. Rev. A</em> <strong>70</strong>, 052328 (2004). <a href="https://doi.org/10.1103/PhysRevA.70.052328">doi:10.1103/PhysRevA.70.052328</a></p>
<p id="ref-JL2003"><span class="ref-num">[JL2003]</span> Jozsa, R., Linden, N.: On the role of entanglement in quantum computational speed-up. <em>Proc. R. Soc. Lond. A</em> <strong>459</strong>, 2011–2032 (2003). Establishes that entanglement is <em>necessary</em> — the other half of the Gottesman–Knill picture.</p>
<p id="ref-BK2005"><span class="ref-num">[BK2005]</span> Bravyi, S., Kitaev, A.: Universal quantum computation with ideal Clifford gates and noisy ancillas. <em>Phys. Rev. A</em> <strong>71</strong>, 022316 (2005). <a href="https://doi.org/10.1103/PhysRevA.71.022316">doi:10.1103/PhysRevA.71.022316</a> Introduces magic state distillation.</p>
<p id="ref-WZ1982"><span class="ref-num">[WZ1982]</span> Wootters, W.K., Zurek, W.H.: A single quantum cannot be cloned. <em>Nature</em> <strong>299</strong>, 802–803 (1982). <a href="https://doi.org/10.1038/299802a0">doi:10.1038/299802a0</a></p>
<p id="ref-Dieks1982"><span class="ref-num">[Dieks1982]</span> Dieks, D.: Communication by EPR devices. <em>Phys. Lett. A</em> <strong>92</strong>(6), 271–272 (1982).</p>
<p id="ref-Holevo1973"><span class="ref-num">[Holevo1973]</span> Holevo, A.S.: Bounds for the quantity of information transmitted by a quantum communication channel. <em>Problems of Information Transmission</em> <strong>9</strong>(3), 177–183 (1973).</p>
<p id="ref-BB84"><span class="ref-num">[BB84]</span> Bennett, C.H., Brassard, G.: Quantum cryptography: Public key distribution and coin tossing. <em>Proc. IEEE Int. Conf. on Computers, Systems and Signal Processing</em>, Bangalore, 175–179 (1984).</p>
<p id="ref-Bell1964"><span class="ref-num">[Bell1964]</span> Bell, J.S.: On the Einstein–Podolsky–Rosen paradox. <em>Physics</em> <strong>1</strong>(3), 195–200 (1964). See the companion article in this series for a full treatment.</p>
<p id="ref-GE2019"><span class="ref-num">[GE2019]</span> Gidney, C., Ekerå, M.: How to factor 2048 bit RSA integers in 8 hours using 20 million noisy qubits. <em>Quantum</em> <strong>5</strong>, 433 (2021). <a href="https://doi.org/10.22331/q-2021-04-15-433">doi:10.22331/q-2021-04-15-433</a></p>
<p id="ref-Gidney2025"><span class="ref-num">[Gidney2025]</span> Gidney, C.: How to factor 2048 bit RSA integers with less than a million noisy qubits. (2025). <a href="https://arxiv.org/abs/2505.15917">arXiv:2505.15917</a>. Reduces the Toffoli count by over 100× and the qubit requirement twentyfold, with no change in hardware assumptions.</p>
<p id="ref-Google2025"><span class="ref-num">[Google2025]</span> Google Quantum AI: Quantum error correction below the surface code threshold. <em>Nature</em> <strong>638</strong>, 920–926 (2025). <a href="https://doi.org/10.1038/s41586-024-08449-y">doi:10.1038/s41586-024-08449-y</a></p>
<p id="ref-NIST2024"><span class="ref-num">[NIST2024]</span> National Institute of Standards and Technology: FIPS 203 (ML-KEM), FIPS 204 (ML-DSA), FIPS 205 (SLH-DSA). Published 13 August 2024. <a href="https://csrc.nist.gov/projects/post-quantum-cryptography">csrc.nist.gov/projects/post-quantum-cryptography</a>. HQC selected as a backup KEM, 11 March 2025.</p>
</div>

</div><!-- end .ckp-body -->

<!-- ─── Sidebar TOC ─────────────────────────────────────────── -->
<aside class="ckp-sidebar">
  <div class="ckp-toc-label">Contents</div>
  <ul class="ckp-toc-list" id="ckp-toc">
    <li data-section="abstract"><a href="#abstract">Abstract</a></li>
    <li data-section="sec-model"><a href="#sec-model">1. The Right Mental Model</a></li>
    <li class="toc-sub" data-section="sec-model"><a href="#sec-model">Three Computers</a></li>
    <li class="toc-sub" data-section="sec-model"><a href="#sec-model">The Parallelism Fallacy</a></li>
    <li data-section="sec-qubit"><a href="#sec-qubit">2. What a Qubit Is</a></li>
    <li class="toc-sub" data-section="sec-qubit"><a href="#sec-qubit">Dirac Notation</a></li>
    <li class="toc-sub" data-section="sec-qubit"><a href="#sec-qubit">Global vs. Relative Phase</a></li>
    <li class="toc-sub" data-section="sec-qubit"><a href="#sec-qubit">The Bloch Sphere</a></li>
    <li data-section="sec-measure"><a href="#sec-measure">3. Measurement</a></li>
    <li class="toc-sub" data-section="sec-measure"><a href="#sec-measure">Superposition ≠ Ignorance</a></li>
    <li data-section="sec-multi"><a href="#sec-multi">4. Many Qubits</a></li>
    <li class="toc-sub" data-section="sec-multi"><a href="#sec-multi">Entanglement</a></li>
    <li data-section="sec-unitary"><a href="#sec-unitary">5. Gates Are Unitaries</a></li>
    <li class="toc-sub" data-section="sec-unitary"><a href="#sec-unitary">No-Cloning</a></li>
    <li data-section="sec-gates"><a href="#sec-gates">6. The Gate Zoo</a></li>
    <li class="toc-sub" data-section="sec-gates"><a href="#sec-gates">Reference Table</a></li>
    <li data-section="sec-circuits"><a href="#sec-circuits">7. Constructing Circuits</a></li>
    <li class="toc-sub" data-section="sec-circuits"><a href="#sec-circuits">Worked Example: Bell Pair</a></li>
    <li data-section="sec-deutsch"><a href="#sec-deutsch">8. Interference at Work</a></li>
    <li class="toc-sub" data-section="sec-deutsch"><a href="#sec-deutsch">Phase Kickback</a></li>
    <li data-section="sec-universal"><a href="#sec-universal">9. Universality</a></li>
    <li class="toc-sub" data-section="sec-universal"><a href="#sec-universal">Gottesman–Knill</a></li>
    <li data-section="sec-crypto"><a href="#sec-crypto">10. Cryptography</a></li>
    <li data-section="sec-think"><a href="#sec-think">11. How to Think Correctly</a></li>
    <li data-section="sec-exercises"><a href="#sec-exercises">Exercises</a></li>
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

  /* ── TOC active state ── */
  var sections = ['abstract','sec-model','sec-qubit','sec-measure','sec-multi','sec-unitary','sec-gates','sec-circuits','sec-deutsch','sec-universal','sec-crypto','sec-think','sec-exercises','sec-glossary','references'];
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
})();
</script>
