---
layout: post
title: "The NIST Modes of Operation: A Field Guide"
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
  --orange:       #e0935c;
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

/* Inline code */
.ckp-body code {
  font-family: var(--font-mono);
  font-size: 0.8em;
  background: var(--surface2);
  border: 1px solid var(--border);
  padding: 0.08em 0.36em;
  color: var(--accent);
  white-space: nowrap;
}

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
  margin: 0 0 0.8rem;
  color: var(--text-muted);
  font-style: italic;
}
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
.ckp-callout.warn { border-left-color: var(--orange); }
.ckp-callout.key  { border-left-color: var(--green); }
.ckp-callout.dead { border-left-color: var(--red); }
.ckp-callout strong {
  font-family: var(--font-mono);
  font-size: 0.68rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--blue);
  display: block;
  margin-bottom: 0.5rem;
}
.ckp-callout.warn strong { color: var(--orange); }
.ckp-callout.key  strong { color: var(--green); }
.ckp-callout.dead strong { color: var(--red); }
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
.ckp-table .mono { font-family: var(--font-mono); font-size: 0.9em; }
.ckp-table .yes { color: var(--green); font-family: var(--font-mono); font-size: 0.9em; }
.ckp-table .no  { color: var(--red);   font-family: var(--font-mono); font-size: 0.9em; }
.ckp-table .mid { color: var(--orange);font-family: var(--font-mono); font-size: 0.9em; }

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
.ckp-refs a { color: var(--blue); text-decoration: none; }
.ckp-refs a:hover { text-decoration: underline; }

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
/* ─── CRYPTO EXTENSIONS ─────────────────────────────────────── */
/* ═══════════════════════════════════════════════════════════════ */

/* ─── Mode header: spec line + status badges ──────────────────── */
.ckp-badges {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
  margin: 0.4rem 0 1.4rem;
}
.badge {
  font-family: var(--font-mono);
  font-size: 0.62rem;
  letter-spacing: 0.09em;
  text-transform: uppercase;
  padding: 0.24rem 0.6rem;
  border: 1px solid var(--border);
  background: var(--surface2);
  color: var(--text-muted);
  white-space: nowrap;
}
.badge.spec { color: var(--accent); border-color: rgba(201,168,76,0.45); background: var(--accent-dim); }
.badge.ok   { color: var(--green);  border-color: rgba(109,207,148,0.40); }
.badge.warn { color: var(--orange); border-color: rgba(224,147,92,0.40); }
.badge.bad  { color: var(--red);    border-color: rgba(224,92,92,0.40); }

/* ─── Verdict panel: use it / don't use it ────────────────────── */
.ckp-verdict {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1px;
  background: var(--border);
  border: 1px solid var(--border);
  margin: 2rem 0;
}
@media (max-width: 700px) { .ckp-verdict { grid-template-columns: 1fr; } }
.ckp-verdict > div { background: var(--surface); padding: 1.1rem 1.4rem 1.2rem; }
.ckp-verdict .use   { border-top: 2px solid var(--green); }
.ckp-verdict .avoid { border-top: 2px solid var(--red); }
.ckp-verdict h5 {
  font-family: var(--font-mono);
  font-size: 0.66rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  margin: 0 0 0.8rem;
  font-weight: 600;
}
.ckp-verdict .use h5   { color: var(--green); }
.ckp-verdict .avoid h5 { color: var(--red); }
.ckp-verdict ul { margin: 0; padding-left: 1.1rem; font-size: 0.86rem; line-height: 1.55; color: var(--text); }
.ckp-verdict li { margin-bottom: 0.5rem; }
.ckp-verdict li:last-child { margin-bottom: 0; }

/* ─── The one-line verdict ────────────────────────────────────── */
.ckp-ruling {
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  background: var(--accent-glow);
  padding: 1rem 1.4rem;
  margin: 1.8rem 0;
  display: flex;
  gap: 1rem;
  align-items: baseline;
  flex-wrap: wrap;
}
.ckp-ruling .rl {
  font-family: var(--font-mono);
  font-size: 0.62rem;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--accent);
  flex-shrink: 0;
}
.ckp-ruling p {
  margin: 0;
  font-family: var(--font-display);
  font-size: 1.02rem;
  font-style: italic;
  color: #f0f0f0;
  line-height: 1.45;
  flex: 1;
  min-width: 240px;
}

/* ─── Code blocks ─────────────────────────────────────────────── */
.ckp-code {
  margin: 1.8rem 0;
  background: #161619;
  border: 1px solid var(--border);
  border-left: 3px solid var(--blue);
  overflow: hidden;
}
.ckp-code .code-label {
  font-family: var(--font-mono);
  font-size: 0.62rem;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--text-muted);
  padding: 0.6rem 1.2rem;
  border-bottom: 1px solid var(--border);
  background: var(--surface);
}
.ckp-code pre {
  margin: 0;
  padding: 1.1rem 1.2rem;
  overflow-x: auto;
  font-family: var(--font-mono);
  font-size: 0.76rem;
  line-height: 1.7;
  color: #d6d6da;
  white-space: pre;
  background: none;
  border: none;
}
.ckp-code .c  { color: #6f6f7c; font-style: italic; }
.ckp-code .k  { color: var(--accent); }
.ckp-code .g  { color: var(--green); }
.ckp-code .r  { color: var(--red); }
.ckp-code .b  { color: var(--blue); }

/* ─── SVG figure ──────────────────────────────────────────────── */
.ckp-fig {
  margin: 2.2rem 0;
  background: var(--surface);
  border: 1px solid var(--border);
  padding: 1.4rem 1.4rem 1.1rem;
  overflow-x: auto;
}
.ckp-fig svg { display: block; width: 100%; height: auto; min-width: 520px; }
.ckp-fig figcaption {
  font-family: var(--font-mono);
  font-size: 0.65rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--text-muted);
  margin-top: 1rem;
  line-height: 1.6;
}
/* SVG primitives */
.dg-box   { fill: var(--surface2); stroke: var(--border); stroke-width: 1; }
.dg-key   { fill: var(--accent-dim); stroke: var(--accent); stroke-width: 1; }
.dg-hash  { fill: rgba(107,181,214,0.12); stroke: var(--blue); stroke-width: 1; }
.dg-good  { fill: rgba(109,207,148,0.12); stroke: var(--green); stroke-width: 1; }
.dg-bad   { fill: rgba(224,92,92,0.12); stroke: var(--red); stroke-width: 1; }
.dg-t     { fill: #e2e2e4; font-family: var(--font-mono); font-size: 11px; }
.dg-tm    { fill: #9898a4; font-family: var(--font-mono); font-size: 9.5px; letter-spacing: 0.05em; }
.dg-ta    { fill: #c9a84c; font-family: var(--font-mono); font-size: 11px; }
.dg-tb    { fill: #6bb5d6; font-family: var(--font-mono); font-size: 10px; }
.dg-l     { stroke: #9898a4; stroke-width: 1.2; fill: none; }
.dg-la    { stroke: #c9a84c; stroke-width: 1.2; fill: none; }
.dg-lb    { stroke: #6bb5d6; stroke-width: 1.2; fill: none; }
.dg-dash  { stroke: #383840; stroke-width: 1; stroke-dasharray: 3 3; fill: none; }
.dg-xor   { fill: #1b1b1e; stroke: #c9a84c; stroke-width: 1.2; }
</style>

<div id="ckp-progress"></div>

<article class="ckp-article">

<!-- ═══════════════════ HERO ═══════════════════════════════════ -->
<div class="ckp-hero">
  <div class="ckp-kicker">Applied Cryptography · NIST SP 800-38 · Authenticated Encryption</div>
  <h1>The NIST Modes of Operation: A <em>Field Guide</em></h1>
  <p class="ckp-deck">Every mode NIST has standardized — how it is built, how it fails, and when a working engineer should reach for it. The block cipher is the easy part. The mode is where your system dies.</p>
  <div class="ckp-meta">
    <span>Applied Cryptography Series</span>
    <span class="dot"></span>
    <span>Revised July 2026</span>
    <span class="dot"></span>
    <span>~55 min read</span>
    <span class="dot"></span>
    <span><a href="https://csrc.nist.gov/Projects/block-cipher-techniques" target="_blank">NIST Block Cipher Techniques ↗</a></span>
  </div>
</div>

<!-- Keywords -->
<div class="ckp-keywords">
  <span class="ckp-kw">AES-GCM</span>
  <span class="ckp-kw">CBC</span>
  <span class="ckp-kw">CTR</span>
  <span class="ckp-kw">CCM</span>
  <span class="ckp-kw">XTS</span>
  <span class="ckp-kw">Key Wrapping</span>
  <span class="ckp-kw">Format-Preserving Encryption</span>
  <span class="ckp-kw">Ascon</span>
  <span class="ckp-kw">Nonce Misuse</span>
  <span class="ckp-kw">Key Commitment</span>
  <span class="ckp-kw">Birthday Bound</span>
</div>

<!-- Mobile TOC -->
<div class="ckp-mobile-toc" id="ckp-mob-toc-toggle">
  <span>Contents</span><span>▾</span>
</div>
<div class="ckp-mobile-toc-list" id="ckp-mob-toc-list">
  <a href="#abstract">Abstract</a>
  <a href="#sec-basics">1. What a Mode Actually Is</a>
  <a href="#sec-goals">2. The Goals You Are Buying</a>
  <a href="#sec-map">3. The Standards Map (2026)</a>
  <a href="#sec-38a">4. The Confidentiality-Only Modes</a>
  <a href="#sec-cmac">5. CMAC</a>
  <a href="#sec-composition">6. Generic Composition</a>
  <a href="#sec-ccm">7. CCM</a>
  <a href="#sec-gcm">8. GCM and GMAC</a>
  <a href="#sec-ascon">9. Ascon</a>
  <a href="#sec-xts">10. XTS-AES</a>
  <a href="#sec-kw">11. Key Wrapping</a>
  <a href="#sec-fpe">12. Format-Preserving Encryption</a>
  <a href="#sec-eng">13. The Engineering That Kills You</a>
  <a href="#sec-decide">14. How to Choose</a>
  <a href="#sec-future">15. What Is Coming</a>
  <a href="#sec-glossary">Quick Reference</a>
  <a href="#references">References</a>
</div>

<!-- ═══════════════════ LAYOUT ════════════════════════════════ -->
<div class="ckp-layout">

<!-- ─── Main Body ─────────────────────────────────────────── -->
<div class="ckp-body">

<!-- ABSTRACT -->
<div class="ckp-abstract" id="abstract">
  <div class="ckp-abstract-label">Abstract</div>
  <p>This is a working reference for engineers who ship cryptography. It covers every block cipher mode of operation that NIST has approved — the five confidentiality-only modes of SP 800-38A, the CMAC authentication mode, the two block-cipher AEAD modes (CCM and GCM), the XTS storage mode, the key-wrapping methods, format-preserving encryption, and the newly standardized Ascon family — together with the attacks that have broken each of them in the field.</p>
  <p>For each mode: the architecture, the proven security and its exact preconditions, the pitfalls that keep showing up in real code, and a blunt verdict on when to use it and when to walk away. The document reflects the standards landscape as of July 2026, including the ongoing revisions to SP 800-38A, 38B, 38C, 38D and 38E, and NIST's proposed successors: wGCM, Rijndael-256, and the cryptographic accordion.</p>
</div>

<!-- STATS BAR -->
<div class="ckp-stat-row">
  <div class="ckp-stat"><span class="stat-num">5</span><span class="stat-label">Confidentiality modes, none with integrity</span></div>
  <div class="ckp-stat"><span class="stat-num">2</span><span class="stat-label">Block-cipher AEAD modes: CCM, GCM</span></div>
  <div class="ckp-stat"><span class="stat-num">$2^{32}$</span><span class="stat-label">GCM messages per key with random IVs</span></div>
  <div class="ckp-stat"><span class="stat-num">1</span><span class="stat-label">Nonce reuse needed to destroy GCM</span></div>
</div>

<!-- ─── SECTION 1 ─────────────────────────────────────────── -->
<section id="sec-basics">
<h2>1. What a Mode Actually Is</h2>

<p class="drop-cap">A block cipher is not an encryption system. AES takes a 128-bit block and a key and produces another 128-bit block. That is all it does. It is a keyed permutation on a set of size $2^{128}$ — a very good one, unbroken after twenty-five years of the best cryptanalysis money can't buy. It is also, on its own, almost useless. Your data is not 128 bits long.</p>

<p>The mode of operation is the machinery that turns this fixed-width permutation into something that encrypts a message, a file, a packet, a disk, a database column. And here is the thing that should worry you: <em>essentially every real-world cryptographic failure of the last thirty years happened in that machinery, or in the glue around it — not in the cipher.</em></p>

<p>Nobody breaks AES. They break the padding. They break the initialization vector. They break the nonce counter after a virtual machine snapshot. They break the fact that you decrypted before you checked the tag. They break your CBC ciphertext with a chosen-plaintext oracle you didn't know you were exposing, and they walk out with the session cookie.</p>

<div class="ckp-pull">
  <p>The cipher is a component with a proof. The mode is a contract with preconditions. Attacks on ciphers make academic papers; violations of mode preconditions make CVEs.</p>
  <cite>— The central asymmetry of applied cryptography</cite>
</div>

<h3>The Three Questions</h3>

<p>Before you can choose a mode you have to know what you are buying. Every mode answers three questions, and you must be able to answer all three about your own system before you write a line of code.</p>

<ul class="ckp-hier">
  <li><strong>What does it hide?</strong> Every approved mode hides the content of your plaintext. None of them hides its length. Some of them do not hide repetition. Ask what your adversary learns from the ciphertext even when the mode works perfectly.</li>
  <li><strong>What does it prove?</strong> Confidentiality is not integrity. A CBC ciphertext can be modified into a <em>different valid ciphertext</em> that decrypts to a plaintext of the attacker's partial choosing. Unless the mode produces an authentication tag, it proves nothing.</li>
  <li><strong>What does it demand from you?</strong> This is the one people get wrong. Every mode has preconditions — unpredictable IVs, unique nonces, per-key data limits, tag verification before use. The proof is conditional on them. Break one and the proof evaporates, usually catastrophically and usually silently.</li>
</ul>

<h3>The Anatomy</h3>

<p>All the confidentiality modes are variations on two ideas. Either you feed the plaintext into the cipher (ECB, CBC), or you use the cipher to manufacture a keystream and XOR it with the plaintext (CFB, OFB, CTR). The second family turns a block cipher into a stream cipher, which is why the second family is so dangerous: a stream cipher that repeats its keystream is not a cipher at all, it is a rearrangement.</p>

<div class="ckp-eq">
  <span class="eq-label">The Two-Time Pad — Eq. (1)</span>
  $$C_1 \oplus C_2 = (P_1 \oplus S) \oplus (P_2 \oplus S) = P_1 \oplus P_2 \tag{1}$$
</div>

<p>Equation (1) is the reason nonce reuse is the deadliest bug in this document. If the same keystream $S$ is ever produced twice, the key cancels out and the attacker is left with the XOR of two plaintexts — from which natural-language text, structured protocol data, and anything with known headers falls out with an afternoon of work. This applies to CTR, OFB, CFB, GCM, CCM, ChaCha20, and every other stream construction ever built. There is no clever recovery. The data is gone.</p>

<div class="ckp-callout warn">
  <strong>The Precondition Is the Product</strong>
  <p>When a standard says "the IV shall be unpredictable" or "the nonce shall be unique for each invocation under a given key," that is not boilerplate. It is the load-bearing wall. NIST's own review of the SP 800-38 series, IR 8459 [<a href="#ref-IR8459">IR8459</a>], concludes that incorrectly generated IVs and counter blocks are the dominant source of practical vulnerabilities in these modes — not weaknesses in the modes themselves.</p>
</div>
</section>

<div class="ckp-sep">Security Goals</div>

<!-- ─── SECTION 2 ─────────────────────────────────────────── -->
<section id="sec-goals">
<h2>2. The Goals You Are Actually Buying</h2>

<p>Cryptographers argue about security definitions because the definitions are the specification. If you don't know which one your mode satisfies, you don't know what you have. Here are the only ones you need, in the order they will bite you.</p>

<h3>Confidentiality: IND-CPA</h3>

<p>Indistinguishability under chosen-plaintext attack. An adversary who can get any plaintext of his choosing encrypted still cannot tell which of two equal-length messages a challenge ciphertext contains. This is the bar the SP 800-38A modes are designed to clear — <em>and it is a low bar.</em> IND-CPA says nothing about an adversary who can <em>modify</em> ciphertexts. In the real world, adversaries can modify ciphertexts.</p>

<p>Note also what IND-CPA does not promise. ECB fails it outright. Every other mode achieves it only if the IV or counter discipline is honored.</p>

<h3>Integrity: INT-CTXT</h3>

<p>Integrity of ciphertexts. The adversary cannot produce any ciphertext that the receiver will accept and that the sender did not send. This is what an authentication tag buys you, and it is the property that turns a cipher into a channel you can trust.</p>

<div class="ckp-definition">
  <div class="ckp-def-label">The Theorem You Should Tattoo Somewhere</div>
  <p>IND-CPA + INT-CTXT $\Rightarrow$ IND-CCA. If your scheme is semantically secure against chosen plaintexts <em>and</em> unforgeable, you get chosen-ciphertext security for free. This is why authenticated encryption is not a luxury: it is the cheapest known route to the security property you actually need.</p>
</div>

<h3>AEAD: The Modern Default</h3>

<p>Authenticated Encryption with Associated Data. One primitive, one call, three inputs: key, nonce, plaintext — plus <em>associated data</em> that is authenticated but not encrypted. The AAD is for the parts of your message that must travel in the clear but must not be tampered with: packet headers, routing information, sequence numbers, key identifiers, algorithm identifiers, version numbers.</p>

<p>Use it. The AAD field is not decoration; it is how you cryptographically bind a ciphertext to its context. Almost every "attacker swapped one valid ciphertext for another valid ciphertext from a different context" bug in the wild is an unused AAD field.</p>

<h3>Nonce-Misuse Resistance</h3>

<p>An MRAE scheme (misuse-resistant AE) degrades gracefully when a nonce repeats: instead of catastrophe, the attacker learns only that two identical plaintexts were encrypted twice. The canonical construction is SIV [<a href="#ref-RS06">RS06</a>], and its practical incarnation is AES-GCM-SIV.</p>

<p>Note carefully: <strong>NIST has not approved a nonce-misuse-resistant AEAD mode.</strong> Not one. This is the single largest gap in the American standards portfolio, and NIST knows it — misuse resistance is explicitly on the requirements list for the accordion project (§15).</p>

<h3>Key Commitment</h3>

<p>A committing AEAD guarantees that a ciphertext decrypts successfully under <em>at most one</em> key. This sounds like a theoretical nicety. It is not. GCM, CCM, and ChaCha20-Poly1305 are all non-committing, and an attacker can construct a single ciphertext that decrypts to two different meaningful plaintexts under two different keys. That property has been weaponized twice: to defeat Facebook Messenger's encrypted-image abuse reporting [<a href="#ref-Salamanders">Salamanders</a>], and to recover user passwords from Shadowsocks proxies via a <em>partitioning oracle</em> [<a href="#ref-Partition">Partition</a>].</p>

<div class="ckp-callout dead">
  <strong>Where Key Commitment Matters</strong>
  <p>If your key is derived from a low-entropy secret (a password, a PIN), or if the receiver <em>selects among candidate keys by trial decryption</em>, or if a ciphertext is evidence in an abuse-reporting or moderation system — you need a committing AEAD and no NIST mode gives it to you natively. Fix it yourself: bind a key commitment into the AAD, or prepend a block of zeros to the plaintext and check it on decryption (the "padding fix"), or derive the encryption key with a KDF whose output includes a commitment value.</p>
</div>

<h3>The Birthday Bound: The Number That Decides Rekeying</h3>

<p>Every mode built on an $n$-bit block cipher leaks structure once you have processed about $2^{n/2}$ blocks under one key. For CBC, ciphertext blocks start to collide, and a collision reveals the XOR of two plaintext blocks. For CTR and its descendants, the keystream stops looking uniform. The bound is not an attack; it is where the security proof runs out — and NIST IR 8459 is blunt that the key must be changed <em>well before</em> $2^{n/2}$ blocks.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr><th>Block size</th><th>Birthday point</th><th>In bytes</th><th>Reality check</th></tr>
</thead>
<tbody>
  <tr>
    <td class="mono">64-bit (3DES, Blowfish)</td>
    <td class="mono">$2^{32}$ blocks</td>
    <td class="mono">32 GB</td>
    <td class="no">Broken in practice. This is Sweet32 [<a href="#ref-Sweet32">Sweet32</a>]: a long-lived HTTPS or OpenVPN connection reaches it in hours.</td>
  </tr>
  <tr>
    <td class="mono">128-bit (AES)</td>
    <td class="mono">$2^{64}$ blocks</td>
    <td class="mono">~295 exabytes</td>
    <td class="yes">Unreachable by data volume. At 100 Gb/s you need roughly 750 years.</td>
  </tr>
  <tr>
    <td class="mono">256-bit (Rijndael-256, proposed)</td>
    <td class="mono">$2^{128}$ blocks</td>
    <td class="mono">absurd</td>
    <td class="yes">The reason NIST is standardizing a wide block at all.</td>
  </tr>
</tbody>
</table>
</div>

<p>Now the trap. That 750-year figure makes engineers complacent, and complacency is exactly wrong, because <strong>the data limit is not the limit that kills you</strong>. Consider AES-GCM with random 96-bit IVs. The standard caps you at $2^{32}$ invocations per key — not because of bytes, but because random 96-bit nonces start colliding. At one million messages per second, a busy service burns through $2^{32}$ messages in <em>seventy-one minutes</em>.</p>

<div class="ckp-pull">
  <p>Seven hundred and fifty years of bytes. Seventy-one minutes of messages. Count your messages, not your gigabytes.</p>
  <cite>— On why the GCM invocation limit is the real limit</cite>
</div>
</section>

<div class="ckp-sep">The Standards Map</div>

<!-- ─── SECTION 3 ─────────────────────────────────────────── -->
<section id="sec-map">
<h2>3. The Standards Map, July 2026</h2>

<p>The SP 800-38 series is seven documents accumulated over fifteen years, plus an addendum, plus a new lightweight standard that lives outside the series entirely. It was not designed as a portfolio. It grew as one, which is why it has five ways to do the wrong thing and no way to do nonce-misuse resistance.</p>

<p>The critical fact for anyone making an architecture decision in 2026: <strong>most of this series is currently under revision.</strong> NIST's Crypto Publication Review Board has been working through it since 2021, and the results are landing now. If you are choosing a mode for a system with a ten-year life, choose with the revisions in view.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr>
    <th>Document</th>
    <th>Specifies</th>
    <th>Published</th>
    <th>Status — July 2026</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><span class="term">SP 800-38A</span></td>
    <td>ECB, CBC, CFB, OFB, CTR</td>
    <td class="mono">2001</td>
    <td class="mid"><strong>Revision decided.</strong> ECB approval to be restricted to specifically permitted uses; IV and counter-block requirements to be tightened; the ciphertext-stealing addendum folded in. NIST states it "will consider deprecating" these modes once an accordion is approved [<a href="#ref-Rev38A">Rev38A</a>].</td>
  </tr>
  <tr>
    <td><span class="term">SP 800-38A Add.</span></td>
    <td>CBC-CS1, CS2, CS3 (ciphertext stealing)</td>
    <td class="mono">2010</td>
    <td class="mid">To be merged into the 38A revision.</td>
  </tr>
  <tr>
    <td><span class="term">SP 800-38B</span></td>
    <td>CMAC</td>
    <td class="mono">2005</td>
    <td class="mid"><strong>Revision decided</strong> (April 2025).</td>
  </tr>
  <tr>
    <td><span class="term">SP 800-38C</span></td>
    <td>CCM</td>
    <td class="mono">2004</td>
    <td class="mid"><strong>Revision decided</strong> (April 2025).</td>
  </tr>
  <tr>
    <td><span class="term">SP 800-38D</span></td>
    <td>GCM, GMAC</td>
    <td class="mono">2007</td>
    <td class="no"><strong>Revision in progress — comment period closes 31 July 2026.</strong> Tags below 96 bits will be removed. TLS 1.3's IV construction will be explicitly approved. A wide variant, <strong>wGCM</strong>, is proposed [<a href="#ref-38Dr1">38Dr1</a>].</td>
  </tr>
  <tr>
    <td><span class="term">SP 800-38E</span></td>
    <td>XTS-AES (storage)</td>
    <td class="mono">2010</td>
    <td class="mid"><strong>Revision decided</strong> (February 2024).</td>
  </tr>
  <tr>
    <td><span class="term">SP 800-38F</span></td>
    <td>KW, KWP, TKW (key wrapping)</td>
    <td class="mono">2012</td>
    <td class="yes">Stable. TKW dies with 3DES.</td>
  </tr>
  <tr>
    <td><span class="term">SP 800-38G</span></td>
    <td>FF1 (and formerly FF3)</td>
    <td class="mono">2016</td>
    <td class="no"><strong>Rev. 1 in draft.</strong> The second public draft <em>deletes FF3 and FF3-1 entirely</em>. Only FF1 survives, with a hard minimum domain size of one million [<a href="#ref-38Gr1">38Gr1</a>].</td>
  </tr>
  <tr>
    <td><span class="term">SP 800-232</span></td>
    <td>Ascon-AEAD128, Ascon-Hash256, XOFs</td>
    <td class="mono">Aug 2025</td>
    <td class="yes"><strong>Final.</strong> The first NIST AEAD that is not a block cipher mode [<a href="#ref-Ascon">Ascon</a>].</td>
  </tr>
  <tr>
    <td><span class="term">SP 800-197x</span></td>
    <td>Cryptographic accordions (Acc128, Acc256, BBBAcc)</td>
    <td class="mono">—</td>
    <td class="mid">Pre-draft. HCTR2-based. This is the intended future of the whole portfolio [<a href="#ref-Acc">Acc</a>].</td>
  </tr>
  <tr>
    <td><span class="term">FIPS 197</span></td>
    <td>AES-128/192/256</td>
    <td class="mono">2001, upd. 2023</td>
    <td class="mid">Revision planned to add <strong>Rijndael-256</strong>, a 256-bit-block variant.</td>
  </tr>
</tbody>
</table>
</div>

<h3>Three Things This Table Is Telling You</h3>

<p><strong>First: the confidentiality-only modes are on notice.</strong> NIST has said in writing that if a suitable wide tweakable encryption technique gets approved, it will consider deprecating ECB, CBC, CFB, OFB, and CTR outright. Do not architect a new system around raw CBC in 2026 and expect it to age well.</p>

<p><strong>Second: GCM is being tightened while you read this.</strong> The short tags are going away. If you shipped AES-GCM with 64-bit or 32-bit tags because a constrained radio link made it seem reasonable, your configuration is about to fall out of the standard.</p>

<p><strong>Third: the gaps are being filled, slowly.</strong> Ascon closed the constrained-device gap in August 2025. The accordion project intends to close the misuse-resistance, key-commitment, and wide-block gaps simultaneously. Neither of those helps you today, but both should shape what you build for tomorrow.</p>

<div class="ckp-callout">
  <strong>A Note on TDEA</strong>
  <p>Three-key Triple DES is finished. Under SP 800-131A Rev. 2, TDEA encryption has been disallowed since the end of 2023; only legacy decryption remains. Its 64-bit block makes Sweet32 a routine engineering hazard rather than an exotic attack. Every mode in this document should be read as "instantiated with AES." If you have 3DES in production, the mode you choose is not your problem.</p>
</div>
</section>

<div class="ckp-sep">SP 800-38A · Confidentiality Only</div>

<!-- ─── SECTION 4 ─────────────────────────────────────────── -->
<section id="sec-38a">
<h2>4. The Confidentiality-Only Modes</h2>

<p>Five modes, published in 2001, designed against a threat model in which the adversary listens but does not write. That threat model has not existed since the invention of the network switch.</p>

<p>Read this section as history and as diagnosis. You will meet all five in legacy code, in hardware you cannot change, and in protocols you must interoperate with. You should deploy none of them naked in a new design.</p>

<div class="ckp-ruling">
  <span class="rl">Ruling</span>
  <p>None of these modes provides integrity. Every one of them is malleable. If you use one, you are also, personally, on the hook for a MAC — and for getting the composition right.</p>
</div>

<!-- ══════════════ ECB ══════════════ -->
<h3>4.1 ECB — Electronic Codebook</h3>

<div class="ckp-badges">
  <span class="badge spec">SP 800-38A §6.1</span>
  <span class="badge bad">Not IND-CPA</span>
  <span class="badge bad">No integrity</span>
  <span class="badge bad">Deterministic</span>
  <span class="badge warn">Approval being restricted</span>
</div>

<p><strong>Architecture.</strong> There isn't one. Split the plaintext into blocks; encrypt each block independently with the same key. No IV, no state, no chaining.</p>

<div class="ckp-eq">
  <span class="eq-label">ECB — Eq. (2)</span>
  $$C_i = E_K(P_i) \qquad\qquad P_i = D_K(C_i) \tag{2}$$
</div>

<p><strong>Security.</strong> ECB is a deterministic map from plaintext blocks to ciphertext blocks. Identical plaintext blocks produce identical ciphertext blocks. This is not a subtle leak; it is the entire structure of your data, published. The classic demonstration is the ECB-encrypted bitmap of a penguin, in which the penguin remains perfectly, insultingly visible. The formal statement is that a trivial distinguishing attack succeeds after encrypting exactly two blocks.</p>

<figure class="ckp-fig">
<svg viewBox="0 0 720 150" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="ECB pattern leakage: identical plaintext blocks map to identical ciphertext blocks">
  <defs>
    <marker id="ecbA" markerWidth="7" markerHeight="7" refX="6" refY="3" orient="auto">
      <path d="M0,0 L6,3 L0,6 Z" fill="#9898a4"/>
    </marker>
  </defs>
  <text x="0" y="14" class="dg-tm">PLAINTEXT BLOCKS</text>
  <rect x="0"   y="24" width="100" height="34" class="dg-box"/>
  <rect x="110" y="24" width="100" height="34" class="dg-bad"/>
  <rect x="220" y="24" width="100" height="34" class="dg-box"/>
  <rect x="330" y="24" width="100" height="34" class="dg-bad"/>
  <rect x="440" y="24" width="100" height="34" class="dg-box"/>
  <rect x="550" y="24" width="100" height="34" class="dg-bad"/>
  <text x="30"  y="46" class="dg-t">HDR</text>
  <text x="140" y="46" class="dg-t">0x00…</text>
  <text x="250" y="46" class="dg-t">NAME</text>
  <text x="360" y="46" class="dg-t">0x00…</text>
  <text x="470" y="46" class="dg-t">ADDR</text>
  <text x="580" y="46" class="dg-t">0x00…</text>

  <line x1="50"  y1="60" x2="50"  y2="84" class="dg-l" marker-end="url(#ecbA)"/>
  <line x1="160" y1="60" x2="160" y2="84" class="dg-l" marker-end="url(#ecbA)"/>
  <line x1="270" y1="60" x2="270" y2="84" class="dg-l" marker-end="url(#ecbA)"/>
  <line x1="380" y1="60" x2="380" y2="84" class="dg-l" marker-end="url(#ecbA)"/>
  <line x1="490" y1="60" x2="490" y2="84" class="dg-l" marker-end="url(#ecbA)"/>
  <line x1="600" y1="60" x2="600" y2="84" class="dg-l" marker-end="url(#ecbA)"/>
  <text x="660" y="78" class="dg-tm">AES-K</text>

  <text x="0" y="104" class="dg-tm">CIPHERTEXT BLOCKS</text>
  <rect x="0"   y="112" width="100" height="34" class="dg-box"/>
  <rect x="110" y="112" width="100" height="34" class="dg-bad"/>
  <rect x="220" y="112" width="100" height="34" class="dg-box"/>
  <rect x="330" y="112" width="100" height="34" class="dg-bad"/>
  <rect x="440" y="112" width="100" height="34" class="dg-box"/>
  <rect x="550" y="112" width="100" height="34" class="dg-bad"/>
  <text x="14"  y="134" class="dg-t">a4 f1 …</text>
  <text x="122" y="134" class="dg-t">9c 2e …</text>
  <text x="234" y="134" class="dg-t">77 b0 …</text>
  <text x="342" y="134" class="dg-t">9c 2e …</text>
  <text x="454" y="134" class="dg-t">1d 55 …</text>
  <text x="562" y="134" class="dg-t">9c 2e …</text>
</svg>
<figcaption>ECB. The three padding blocks are identical in the plaintext, so they are identical in the ciphertext. The adversary reads your record structure straight off the wire without touching the key.</figcaption>
</figure>

<p><strong>Pitfalls.</strong> Beyond the obvious: because blocks are independent, an attacker can <em>cut and paste</em> ciphertext blocks between messages, reorder them, delete them, and replay them. Combine ECB with a chosen-plaintext oracle — say, a cookie of the form <code>attacker_data || secret</code> — and you can recover the secret one byte at a time by aligning it against a block boundary. It is a first-week exercise in every crypto course, and it still appears in production.</p>

<div class="ckp-verdict">
  <div class="use">
    <h5>Use ECB when</h5>
    <ul>
      <li>Another NIST standard explicitly tells you to — for example, the challenge-response construction in SP 800-73-4. The forthcoming 38A revision will limit approval to exactly these cases.</li>
      <li>You are encrypting a single block of uniformly random data that will never repeat — key wrapping internals, some DRBG constructions. Here "ECB" is really just "one call to the block cipher."</li>
    </ul>
  </div>
  <div class="avoid">
    <h5>Never use ECB when</h5>
    <ul>
      <li>The data is longer than one block. Ever.</li>
      <li>The data has any structure, repetition, or low entropy — which is to say, whenever it is real data.</li>
      <li>You are tempted to say "but the blocks are all different in practice." They aren't, and you can't check.</li>
    </ul>
  </div>
</div>

<!-- ══════════════ CBC ══════════════ -->
<h3>4.2 CBC — Cipher Block Chaining</h3>

<div class="ckp-badges">
  <span class="badge spec">SP 800-38A §6.2</span>
  <span class="badge ok">IND-CPA (with correct IVs)</span>
  <span class="badge bad">No integrity</span>
  <span class="badge bad">Malleable</span>
  <span class="badge warn">Padding oracles</span>
  <span class="badge warn">Serial encryption</span>
</div>

<p><strong>Architecture.</strong> Chain each plaintext block with the previous ciphertext block before encrypting. The first block is chained with an initialization vector.</p>

<div class="ckp-eq">
  <span class="eq-label">CBC — Eq. (3)</span>
  $$C_i = E_K(P_i \oplus C_{i-1}), \quad C_0 = IV \qquad\qquad P_i = D_K(C_i) \oplus C_{i-1} \tag{3}$$
</div>

<figure class="ckp-fig">
<svg viewBox="0 0 720 240" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="CBC encryption: each plaintext block is XORed with the previous ciphertext block before encryption">
  <defs>
    <marker id="cbcA" markerWidth="7" markerHeight="7" refX="6" refY="3" orient="auto">
      <path d="M0,0 L6,3 L0,6 Z" fill="#9898a4"/>
    </marker>
  </defs>

  <rect x="145" y="14" width="90" height="32" class="dg-box"/>
  <rect x="335" y="14" width="90" height="32" class="dg-box"/>
  <rect x="525" y="14" width="90" height="32" class="dg-box"/>
  <text x="180" y="35" class="dg-t">P₁</text>
  <text x="370" y="35" class="dg-t">P₂</text>
  <text x="560" y="35" class="dg-t">P₃</text>

  <rect x="35" y="72" width="80" height="32" class="dg-key"/>
  <text x="60" y="93" class="dg-ta">IV</text>

  <circle cx="190" cy="88" r="11" class="dg-xor"/><text x="185" y="92" class="dg-ta">⊕</text>
  <circle cx="380" cy="88" r="11" class="dg-xor"/><text x="375" y="92" class="dg-ta">⊕</text>
  <circle cx="570" cy="88" r="11" class="dg-xor"/><text x="565" y="92" class="dg-ta">⊕</text>

  <line x1="190" y1="46" x2="190" y2="76" class="dg-l" marker-end="url(#cbcA)"/>
  <line x1="380" y1="46" x2="380" y2="76" class="dg-l" marker-end="url(#cbcA)"/>
  <line x1="570" y1="46" x2="570" y2="76" class="dg-l" marker-end="url(#cbcA)"/>
  <line x1="115" y1="88" x2="177" y2="88" class="dg-la" marker-end="url(#cbcA)"/>

  <rect x="145" y="124" width="90" height="36" class="dg-hash"/>
  <rect x="335" y="124" width="90" height="36" class="dg-hash"/>
  <rect x="525" y="124" width="90" height="36" class="dg-hash"/>
  <text x="166" y="147" class="dg-tb">AES-K</text>
  <text x="356" y="147" class="dg-tb">AES-K</text>
  <text x="546" y="147" class="dg-tb">AES-K</text>

  <line x1="190" y1="99" x2="190" y2="120" class="dg-l" marker-end="url(#cbcA)"/>
  <line x1="380" y1="99" x2="380" y2="120" class="dg-l" marker-end="url(#cbcA)"/>
  <line x1="570" y1="99" x2="570" y2="120" class="dg-l" marker-end="url(#cbcA)"/>

  <rect x="145" y="188" width="90" height="32" class="dg-box"/>
  <rect x="335" y="188" width="90" height="32" class="dg-box"/>
  <rect x="525" y="188" width="90" height="32" class="dg-box"/>
  <text x="180" y="209" class="dg-t">C₁</text>
  <text x="370" y="209" class="dg-t">C₂</text>
  <text x="560" y="209" class="dg-t">C₃</text>

  <line x1="190" y1="160" x2="190" y2="184" class="dg-l" marker-end="url(#cbcA)"/>
  <line x1="380" y1="160" x2="380" y2="184" class="dg-l" marker-end="url(#cbcA)"/>
  <line x1="570" y1="160" x2="570" y2="184" class="dg-l" marker-end="url(#cbcA)"/>

  <path d="M235,204 L285,204 L285,88 L367,88" class="dg-la" marker-end="url(#cbcA)"/>
  <path d="M425,204 L475,204 L475,88 L557,88" class="dg-la" marker-end="url(#cbcA)"/>

  <text x="640" y="92" class="dg-tm">SERIAL:</text>
  <text x="640" y="106" class="dg-tm">C₁ BEFORE</text>
  <text x="640" y="120" class="dg-tm">C₂ …</text>
</svg>
<figcaption>CBC encryption. The gold feedback path is the whole mode — and the reason encryption cannot be parallelized. Decryption, however, is fully parallel: each block needs only $C_i$ and $C_{i-1}$.</figcaption>
</figure>

<p><strong>The IV requirement is stronger than you think.</strong> SP 800-38A does not merely say the CBC IV must be unique. It says it must be <em>unpredictable</em>. Generate it with an approved RBG, or by encrypting a nonce under the same key. A unique-but-guessable IV — a counter, a timestamp, or the previous message's last ciphertext block — is not sufficient, and the reason is a chosen-plaintext attack.</p>

<div class="ckp-callout dead">
  <strong>BEAST: Why "Unique" Is Not "Unpredictable"</strong>
  <p>TLS 1.0 chained records: the IV of record $n+1$ was the last ciphertext block of record $n$. Unique — and completely predictable to anyone watching the wire. An attacker who can inject chosen plaintext into the same stream (via JavaScript in the victim's browser) can then <em>guess</em> a secret block $P$: submit the crafted block $P' = IV_{\text{next}} \oplus C_{j-1} \oplus G$ for a guess $G$. If the resulting ciphertext equals $C_j$, the guess was right. Byte-at-a-time, that recovers the session cookie. This is BEAST, CVE-2011-3389, and it is why the requirement says <em>unpredictable</em> [<a href="#ref-BEAST">BEAST</a>].</p>
</div>

<p><strong>Malleability.</strong> Flip a bit in $C_{i-1}$ and you flip exactly the same bit in $P_i$ — while turning $P_{i-1}$ into garbage. An attacker who knows or guesses the plaintext of block $i$ can therefore make it decrypt to <em>anything he wants</em>, at the price of destroying the preceding block. If block $i-1$ happens to be somewhere the application ignores — a comment field, a slack region, an unparsed header — the cost is zero. NIST's own revision proposal cites work showing this can be escalated to arbitrary code execution against CBC-encrypted binaries.</p>

<p><strong>Padding oracles.</strong> CBC needs the plaintext padded to a block multiple. If your system reveals — through an error message, a different response code, a distinguishable timing, or a TCP reset — whether the padding was valid after decryption, an attacker decrypts arbitrary ciphertext without the key, at roughly 128 queries per byte. Vaudenay published this in 2002 [<a href="#ref-Vaudenay">Vaudenay</a>]. It has since produced a parade of disasters:</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr><th>Attack</th><th>Year</th><th>Target</th><th>The oracle was…</th></tr>
</thead>
<tbody>
  <tr><td class="mono">Vaudenay</td><td class="mono">2002</td><td>SSL/IPsec/WTLS</td><td>a distinguishable padding error</td></tr>
  <tr><td class="mono">MS10-070</td><td class="mono">2010</td><td>ASP.NET</td><td>an HTTP error code difference</td></tr>
  <tr><td class="mono">Lucky 13</td><td class="mono">2013</td><td>TLS (MAC-then-Encrypt)</td><td>a few microseconds of HMAC timing</td></tr>
  <tr><td class="mono">POODLE</td><td class="mono">2014</td><td>SSL 3.0</td><td>unchecked padding bytes</td></tr>
  <tr><td class="mono">Efail</td><td class="mono">2018</td><td>S/MIME, OpenPGP</td><td>the mail client itself, exfiltrating via HTML</td></tr>
</tbody>
</table>
</div>

<p>Notice the pattern. Every single one of these is a <em>plumbing</em> failure. None of them touched AES. And notice Lucky 13 in particular: the "oracle" was a timing difference of microseconds, arising from the order in which TLS composed its MAC and its encryption. Which brings us to the real lesson of CBC: it is not that CBC is unusable, it is that using CBC correctly requires you to also get a MAC, the composition order, the padding check, and the constant-time comparison right. That is four chances to lose. AEAD gives you zero.</p>

<h4>Ciphertext Stealing: CBC-CS1, CS2, CS3</h4>

<p>The SP 800-38A Addendum specifies three ciphertext-stealing variants that let CBC encrypt any input at least one block long without expanding it. The padding bits are "stolen" from the penultimate ciphertext block. The three variants differ only in how the final two blocks are ordered on the wire — CS3 (the "Kerberos" ordering) unconditionally swaps them; CS2 swaps only when the last block is partial; CS1 does not swap.</p>

<p>Use ciphertext stealing when a length-preserving requirement forces your hand — legacy record formats, fixed-width fields. Understand that it eliminates <em>padding</em> oracles, not <em>malleability</em>, and that the three orderings are a gratuitous interoperability trap. Note which one you implemented. Your counterparty probably chose differently.</p>

<div class="ckp-verdict">
  <div class="use">
    <h5>Use CBC when</h5>
    <ul>
      <li>You must interoperate with an existing protocol that mandates it, and you can wrap it in Encrypt-then-MAC.</li>
      <li>You are in a constrained environment with only a hardware AES core and a hardware CMAC, and no AEAD.</li>
      <li>Decryption throughput matters more than encryption throughput — CBC decryption parallelizes; encryption does not.</li>
    </ul>
  </div>
  <div class="avoid">
    <h5>Avoid CBC when</h5>
    <ul>
      <li>You have any choice at all. Use an AEAD mode.</li>
      <li>The attacker can submit ciphertexts and observe <em>any</em> difference in how they are rejected. You have a padding oracle and you probably don't know it.</li>
      <li>Your IVs come from a counter, a timestamp, or the last ciphertext block.</li>
      <li>The block cipher has a 64-bit block. That's Sweet32.</li>
    </ul>
  </div>
</div>

<!-- ══════════════ CFB ══════════════ -->
<h3>4.3 CFB — Cipher Feedback</h3>

<div class="ckp-badges">
  <span class="badge spec">SP 800-38A §6.3</span>
  <span class="badge ok">IND-CPA (with correct IVs)</span>
  <span class="badge bad">No integrity</span>
  <span class="badge warn">Self-synchronizing</span>
  <span class="badge bad">CFB-8 is a performance disaster</span>
</div>

<p><strong>Architecture.</strong> CFB turns the block cipher into a self-synchronizing stream cipher with a segment size $s$, where $1 \le s \le b$. Encrypt the current shift register, take the top $s$ bits, XOR with the plaintext segment to produce the ciphertext segment, then shift the ciphertext segment into the register. The IV seeds the register.</p>

<div class="ckp-eq">
  <span class="eq-label">CFB, segment size $s$ — Eq. (4)</span>
  $$C_i = P_i \oplus \mathrm{MSB}_s\bigl(E_K(I_i)\bigr), \qquad I_{i+1} = \mathrm{LSB}_{b-s}(I_i) \,\|\, C_i \tag{4}$$
</div>

<p><strong>Security.</strong> Like CBC, the IV must be unpredictable. Like every keystream mode, IV reuse is fatal. The self-synchronizing property — the mode recovers automatically after $\lceil b/s \rceil$ segments of corruption — was valuable in 1980 on a noisy serial line. It is worthless today, because a modern protocol should be <em>rejecting</em> corrupted data, not gracefully resynchronizing with it.</p>

<p><strong>The performance trap.</strong> CFB-8 costs one full block cipher invocation per <em>byte</em>. That is sixteen times the work of CFB-128 for the same data. CFB-1 costs one AES call per bit. People still choose these settings because a spec somewhere said "CFB" without a segment size.</p>

<div class="ckp-callout dead">
  <strong>Zerologon: The Cost of a Zero IV</strong>
  <p>Microsoft's Netlogon protocol used AES-CFB8 with a fixed, all-zero IV (CVE-2020-1472). With CFB-8, if the plaintext byte and the top byte of $E_K(I)$ happen to be equal, the ciphertext byte is zero — and the register shifts in a zero, leaving the state unchanged. So if an attacker submits an all-zero client challenge, the entire ciphertext is all zeros with probability roughly $1/256$, <em>for any key</em>. Just retry: about 256 attempts, a few seconds, and you have authenticated as the domain controller. This is a complete Active Directory compromise caused by one hardcoded IV in one mode nobody should have picked [<a href="#ref-Zerologon">Zerologon</a>].</p>
</div>

<div class="ckp-verdict">
  <div class="use">
    <h5>Use CFB when</h5>
    <ul>
      <li>A legacy protocol demands it and you cannot change the protocol.</li>
      <li>You genuinely need byte-granular streaming with no expansion and cannot use CTR — a situation I have never actually encountered.</li>
    </ul>
  </div>
  <div class="avoid">
    <h5>Avoid CFB when</h5>
    <ul>
      <li>Always, in new designs. CTR does the same job faster, and AEAD does it safely.</li>
      <li>Anyone suggests a fixed IV. Anyone suggests CFB-8.</li>
    </ul>
  </div>
</div>

<!-- ══════════════ OFB ══════════════ -->
<h3>4.4 OFB — Output Feedback</h3>

<div class="ckp-badges">
  <span class="badge spec">SP 800-38A §6.4</span>
  <span class="badge ok">IND-CPA (with unique IVs)</span>
  <span class="badge bad">No integrity</span>
  <span class="badge bad">Catastrophic on IV reuse</span>
  <span class="badge warn">No parallelism</span>
</div>

<p><strong>Architecture.</strong> Iterate the cipher on its own output to make a keystream, independent of the plaintext. XOR to encrypt.</p>

<div class="ckp-eq">
  <span class="eq-label">OFB — Eq. (5)</span>
  $$O_i = E_K(O_{i-1}), \quad O_0 = IV \qquad\qquad C_i = P_i \oplus O_i \tag{5}$$
</div>

<p><strong>Security.</strong> The IV here must be a <em>nonce</em> — unique per key. It need not be unpredictable, but it must never, ever repeat, because the keystream depends on nothing else. Repeat the IV and you have re-derived Equation (1): the two-time pad.</p>

<p><strong>Why it exists and why it doesn't matter.</strong> OFB's one virtue is that bit errors in the ciphertext do not propagate — a corrupted bit corrupts exactly one plaintext bit. That mattered for analog voice links. Today, its keystream cannot be computed in parallel and cannot be seeked into, which makes it strictly worse than CTR at the only job it can do.</p>

<div class="ckp-ruling">
  <span class="rl">Ruling</span>
  <p>OFB is CTR mode with all the advantages removed. There is no scenario in 2026 in which OFB is the right answer to a question CTR cannot answer better.</p>
</div>

<!-- ══════════════ CTR ══════════════ -->
<h3>4.5 CTR — Counter Mode</h3>

<div class="ckp-badges">
  <span class="badge spec">SP 800-38A §6.5</span>
  <span class="badge ok">IND-CPA (with unique counters)</span>
  <span class="badge bad">No integrity</span>
  <span class="badge ok">Fully parallel</span>
  <span class="badge ok">Random access</span>
  <span class="badge ok">No padding</span>
  <span class="badge bad">Trivially malleable</span>
</div>

<p><strong>Architecture.</strong> Encrypt a sequence of counter blocks to make a keystream. XOR to encrypt. The plaintext never enters the cipher.</p>

<div class="ckp-eq">
  <span class="eq-label">CTR — Eq. (6)</span>
  $$C_i = P_i \oplus E_K(T_i), \qquad T_i = \text{Nonce} \,\|\, i \tag{6}$$
</div>

<figure class="ckp-fig">
<svg viewBox="0 0 720 200" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="CTR mode: counter blocks are encrypted independently to form a keystream">
  <defs>
    <marker id="ctrA" markerWidth="7" markerHeight="7" refX="6" refY="3" orient="auto">
      <path d="M0,0 L6,3 L0,6 Z" fill="#9898a4"/>
    </marker>
  </defs>

  <rect x="60"  y="14" width="120" height="32" class="dg-key"/>
  <rect x="270" y="14" width="120" height="32" class="dg-key"/>
  <rect x="480" y="14" width="120" height="32" class="dg-key"/>
  <text x="76"  y="35" class="dg-ta">N ‖ 0001</text>
  <text x="286" y="35" class="dg-ta">N ‖ 0002</text>
  <text x="496" y="35" class="dg-ta">N ‖ 0003</text>

  <line x1="120" y1="46" x2="120" y2="72" class="dg-l" marker-end="url(#ctrA)"/>
  <line x1="330" y1="46" x2="330" y2="72" class="dg-l" marker-end="url(#ctrA)"/>
  <line x1="540" y1="46" x2="540" y2="72" class="dg-l" marker-end="url(#ctrA)"/>

  <rect x="60"  y="76" width="120" height="36" class="dg-hash"/>
  <rect x="270" y="76" width="120" height="36" class="dg-hash"/>
  <rect x="480" y="76" width="120" height="36" class="dg-hash"/>
  <text x="97"  y="99" class="dg-tb">AES-K</text>
  <text x="307" y="99" class="dg-tb">AES-K</text>
  <text x="517" y="99" class="dg-tb">AES-K</text>

  <line x1="120" y1="112" x2="120" y2="134" class="dg-l" marker-end="url(#ctrA)"/>
  <line x1="330" y1="112" x2="330" y2="134" class="dg-l" marker-end="url(#ctrA)"/>
  <line x1="540" y1="112" x2="540" y2="134" class="dg-l" marker-end="url(#ctrA)"/>

  <circle cx="120" cy="148" r="11" class="dg-xor"/><text x="115" y="152" class="dg-ta">⊕</text>
  <circle cx="330" cy="148" r="11" class="dg-xor"/><text x="325" y="152" class="dg-ta">⊕</text>
  <circle cx="540" cy="148" r="11" class="dg-xor"/><text x="535" y="152" class="dg-ta">⊕</text>

  <text x="18" y="152" class="dg-t">P₁</text>
  <text x="228" y="152" class="dg-t">P₂</text>
  <text x="438" y="152" class="dg-t">P₃</text>
  <line x1="35"  y1="148" x2="107" y2="148" class="dg-l" marker-end="url(#ctrA)"/>
  <line x1="245" y1="148" x2="317" y2="148" class="dg-l" marker-end="url(#ctrA)"/>
  <line x1="455" y1="148" x2="527" y2="148" class="dg-l" marker-end="url(#ctrA)"/>

  <line x1="120" y1="159" x2="120" y2="180" class="dg-l" marker-end="url(#ctrA)"/>
  <line x1="330" y1="159" x2="330" y2="180" class="dg-l" marker-end="url(#ctrA)"/>
  <line x1="540" y1="159" x2="540" y2="180" class="dg-l" marker-end="url(#ctrA)"/>
  <text x="108" y="196" class="dg-t">C₁</text>
  <text x="318" y="196" class="dg-t">C₂</text>
  <text x="528" y="196" class="dg-t">C₃</text>

  <line x1="205" y1="94" x2="245" y2="94" class="dg-dash"/>
  <line x1="415" y1="94" x2="455" y2="94" class="dg-dash"/>
  <text x="622" y="90" class="dg-tm">NO CHAINING.</text>
  <text x="622" y="104" class="dg-tm">FULLY PARALLEL.</text>
</svg>
<figcaption>CTR mode. There is no feedback path at all — every block is independent, which is why CTR saturates modern pipelined AES-NI hardware and why it is the engine inside both GCM and CCM.</figcaption>
</figure>

<p><strong>Security.</strong> CTR is a clean, provably IND-CPA construction — and it is fast, parallel, seekable, needs no padding, and needs no inverse cipher. It is the best of the five by a wide margin, and it is the foundation of every AEAD mode NIST has standardized. It has exactly one requirement, and that requirement is absolute:</p>

<div class="ckp-callout warn">
  <strong>The Counter Block Must Be Globally Unique Per Key</strong>
  <p>Not unique per message. Unique across <em>every block of every message ever encrypted under that key</em>. The standard leaves you two constructions: increment the entire block, or split it into a nonce field and a counter field. The second is what everyone does, and the trap is arithmetic: if you give the counter field 32 bits, a message longer than $2^{32}$ blocks overflows into the next message's nonce, and now two messages share keystream. Size your fields so that the maximum message length cannot reach the next nonce. Then enforce that maximum in code.</p>
</div>

<p><strong>Malleability, and why CTR without a MAC is worse than CBC without a MAC.</strong> In CBC, flipping a ciphertext bit garbles a whole block. In CTR, flipping a ciphertext bit flips exactly the corresponding plaintext bit and nothing else. The attacker has surgical, bit-precise control over your plaintext. If you are transmitting <code>amount=100</code> and the attacker knows the offset, he sends <code>amount=900</code>. There is no integrity check, no corruption, no signal. Raw CTR mode over an active network is an authorization bypass with extra steps.</p>

<div class="ckp-verdict">
  <div class="use">
    <h5>Use CTR when</h5>
    <ul>
      <li>You are building an AEAD out of it, with a MAC, using Encrypt-then-MAC. (Or better: use GCM, which is exactly this, done for you.)</li>
      <li>You need random access into a large encrypted object and integrity is handled at a different layer.</li>
      <li>You need a keystream for a construction that provides its own integrity.</li>
    </ul>
  </div>
  <div class="avoid">
    <h5>Never use CTR when</h5>
    <ul>
      <li>There is no MAC. The malleability is total.</li>
      <li>You cannot prove your counter blocks are unique across every message under the key — including across process restarts, VM restores, and clustered instances.</li>
    </ul>
  </div>
</div>

<h3>4.6 Verdict Table: SP 800-38A</h3>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr>
    <th>Mode</th><th>IV/Counter rule</th><th>Parallel enc / dec</th><th>Padding</th><th>Effect of bit flip in $C_i$</th><th>2026 verdict</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="mono">ECB</td><td class="no">none — that's the problem</td><td class="yes">yes / yes</td><td>required</td><td>garbles $P_i$ only</td><td class="no">Do not use</td>
  </tr>
  <tr>
    <td class="mono">CBC</td><td class="mid"><strong>unpredictable</strong> IV</td><td class="mid">no / yes</td><td>required</td><td>garbles $P_i$; flips same bit in $P_{i+1}$</td><td class="mid">Legacy only, with EtM</td>
  </tr>
  <tr>
    <td class="mono">CFB</td><td class="mid"><strong>unpredictable</strong> IV</td><td class="mid">no / yes</td><td>none</td><td>flips bit in $P_i$; garbles next segments</td><td class="no">Do not use</td>
  </tr>
  <tr>
    <td class="mono">OFB</td><td class="mid"><strong>unique</strong> nonce</td><td class="no">no / no</td><td>none</td><td>flips exactly that bit in $P_i$</td><td class="no">Do not use</td>
  </tr>
  <tr>
    <td class="mono">CTR</td><td class="mid"><strong>unique</strong> counter block</td><td class="yes">yes / yes</td><td>none</td><td>flips exactly that bit in $P_i$</td><td class="mid">Only inside an AEAD</td>
  </tr>
</tbody>
</table>
</div>
</section>

<div class="ckp-sep">Authentication</div>

<!-- ─── SECTION 5 ─────────────────────────────────────────── -->
<section id="sec-cmac">
<h2>5. CMAC — The Authentication Mode</h2>

<div class="ckp-badges">
  <span class="badge spec">SP 800-38B</span>
  <span class="badge ok">Unforgeable (to birthday bound)</span>
  <span class="badge ok">No IV needed</span>
  <span class="badge warn">Serial</span>
  <span class="badge warn">Revision decided, April 2025</span>
</div>

<p>CMAC exists because the obvious thing — CBC-MAC — is broken, and the way it is broken is instructive.</p>

<h3>Why Raw CBC-MAC Fails</h3>

<p>CBC-MAC runs CBC with a zero IV and keeps only the last ciphertext block as the tag. For <em>fixed-length</em> messages this is provably secure. For variable-length messages it is trivially forgeable:</p>

<div class="ckp-code">
  <div class="code-label">Length-extension forgery on raw CBC-MAC</div>
<pre><span class="c">// Attacker knows two valid pairs:</span>
T1 = CBC-MAC(K, M1)
T2 = CBC-MAC(K, M2)

<span class="c">// Then this is a valid tag for a message he never saw authenticated:</span>
M3 = M1 ‖ (M2[0] ⊕ T1) ‖ M2[1..]
T3 = T2                       <span class="g">// forged, no key required</span></pre>
</div>

<p>The XOR with $T_1$ cancels the chaining value, so the second half of $M_3$ runs through exactly the same states as $M_2$. This is not an obscure edge case. It is the reason you must never build a MAC out of CBC by hand.</p>

<h3>Architecture</h3>

<p>CMAC (based on Iwata and Kurosawa's OMAC1) fixes this by deriving two subkeys from the block cipher itself and using one of them to mask the final block. The masking makes the last block unambiguous — the tag now depends on whether the message ended on a block boundary.</p>

<div class="ckp-eq">
  <span class="eq-label">CMAC subkey derivation — Eq. (7)</span>
  $$L = E_K(0^b), \qquad K_1 = L \cdot x, \qquad K_2 = L \cdot x^2 \quad \text{in } \mathrm{GF}(2^b) \tag{7}$$
</div>

<p>Multiplication by $x$ is a left shift with a conditional XOR of the field constant ($\texttt{0x87}$ for a 128-bit block). If the final message block is complete, XOR it with $K_1$; if it needed padding, pad with $\texttt{10}^*$ and XOR with $K_2$. Then run CBC and take the last block.</p>

<h3>Security and Pitfalls</h3>

<ul class="ckp-hier">
  <li><strong>Birthday-bounded, like everything else.</strong> Forgery probability grows with the square of the number of blocks MACed under one key, over $2^{128}$. Rekey before $2^{64}$ blocks. With a 64-bit block cipher, CMAC is as dead as everything else.</li>
  <li><strong>Truncation is allowed, but it costs you.</strong> A $t$-bit tag gives an attacker a $2^{-t}$ chance per forgery attempt. If the attacker can try often and cheaply — an unauthenticated network endpoint — a 32-bit tag is a matter of hours. SP 800-38B ties the acceptable tag length to the number of verification failures you will tolerate before you kill the key. Implement that counter. Almost nobody does.</li>
  <li><strong>CMAC is not a hash.</strong> The key is required. Do not use it as a checksum, a fingerprint, or a content identifier.</li>
  <li><strong>Don't reuse the key.</strong> A CMAC key and an encryption key must be different keys, derived separately. See §6.</li>
</ul>

<div class="ckp-callout key">
  <strong>CMAC vs. HMAC vs. KMAC vs. GMAC</strong>
  <p><strong>CMAC</strong> when you have a hardware AES engine and no hash engine — common in embedded and smartcard work. <strong>HMAC-SHA-256</strong> when you have a hash and want the most conservatively analyzed, most widely implemented option in existence; it is also the only one on this list that is not birthday-bounded in message length. <strong>KMAC</strong> (SP 800-185) when you are already using SHA-3. <strong>GMAC</strong> only when you are already doing GCM and can guarantee nonce uniqueness — it is fast but it inherits every nonce hazard in §8.</p>
</div>
</section>

<div class="ckp-sep">Composition</div>

<!-- ─── SECTION 6 ─────────────────────────────────────────── -->
<section id="sec-composition">
<h2>6. Generic Composition: The Decision That Sank TLS</h2>

<p>NIST does not standardize a "combine an encryption mode with a MAC" mode. It standardizes the pieces and leaves the assembly to you. That is a shame, because the assembly has exactly one correct answer and the industry spent fifteen years getting it wrong.</p>

<p>You have a confidentiality mode, a MAC, and two independent keys. There are three ways to put them together.</p>

<figure class="ckp-fig">
<svg viewBox="0 0 720 210" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Three generic composition orders: Encrypt-then-MAC, MAC-then-Encrypt, Encrypt-and-MAC">
  <defs>
    <marker id="cmpA" markerWidth="7" markerHeight="7" refX="6" refY="3" orient="auto">
      <path d="M0,0 L6,3 L0,6 Z" fill="#9898a4"/>
    </marker>
  </defs>

  <!-- EtM -->
  <text x="0" y="14" class="dg-tm">ENCRYPT-THEN-MAC — SECURE</text>
  <rect x="0" y="24" width="60" height="30" class="dg-box"/><text x="20" y="44" class="dg-t">P</text>
  <line x1="60" y1="39" x2="88" y2="39" class="dg-l" marker-end="url(#cmpA)"/>
  <rect x="92" y="24" width="70" height="30" class="dg-hash"/><text x="106" y="44" class="dg-tb">ENC</text>
  <line x1="162" y1="39" x2="190" y2="39" class="dg-l" marker-end="url(#cmpA)"/>
  <rect x="194" y="24" width="60" height="30" class="dg-box"/><text x="215" y="44" class="dg-t">C</text>
  <line x1="254" y1="39" x2="282" y2="39" class="dg-l" marker-end="url(#cmpA)"/>
  <rect x="286" y="24" width="70" height="30" class="dg-good"/><text x="302" y="44" class="dg-t">MAC</text>
  <line x1="356" y1="39" x2="384" y2="39" class="dg-l" marker-end="url(#cmpA)"/>
  <rect x="388" y="24" width="110" height="30" class="dg-good"/><text x="400" y="44" class="dg-t">C ‖ T</text>
  <text x="516" y="36" class="dg-tm">RECEIVER CHECKS T</text>
  <text x="516" y="49" class="dg-tm">BEFORE DECRYPTING.</text>

  <!-- MtE -->
  <text x="0" y="94" class="dg-tm">MAC-THEN-ENCRYPT — FRAGILE</text>
  <rect x="0" y="104" width="60" height="30" class="dg-box"/><text x="20" y="124" class="dg-t">P</text>
  <line x1="60" y1="119" x2="88" y2="119" class="dg-l" marker-end="url(#cmpA)"/>
  <rect x="92" y="104" width="70" height="30" class="dg-box"/><text x="108" y="124" class="dg-t">MAC</text>
  <line x1="162" y1="119" x2="190" y2="119" class="dg-l" marker-end="url(#cmpA)"/>
  <rect x="194" y="104" width="60" height="30" class="dg-box"/><text x="204" y="124" class="dg-t">P‖T</text>
  <line x1="254" y1="119" x2="282" y2="119" class="dg-l" marker-end="url(#cmpA)"/>
  <rect x="286" y="104" width="70" height="30" class="dg-bad"/><text x="300" y="124" class="dg-t">ENC</text>
  <line x1="356" y1="119" x2="384" y2="119" class="dg-l" marker-end="url(#cmpA)"/>
  <rect x="388" y="104" width="110" height="30" class="dg-bad"/><text x="404" y="124" class="dg-t">C</text>
  <text x="516" y="116" class="dg-tm">RECEIVER MUST DECRYPT</text>
  <text x="516" y="129" class="dg-tm">GARBAGE FIRST. ORACLE.</text>

  <!-- E&M -->
  <text x="0" y="174" class="dg-tm">ENCRYPT-AND-MAC — LEAKY</text>
  <rect x="0" y="184" width="60" height="26" class="dg-box"/><text x="20" y="202" class="dg-t">P</text>
  <line x1="60" y1="197" x2="88" y2="197" class="dg-l" marker-end="url(#cmpA)"/>
  <rect x="92" y="184" width="70" height="26" class="dg-box"/><text x="106" y="202" class="dg-t">ENC</text>
  <line x1="162" y1="197" x2="190" y2="197" class="dg-l" marker-end="url(#cmpA)"/>
  <rect x="194" y="184" width="60" height="26" class="dg-box"/><text x="215" y="202" class="dg-t">C</text>
  <line x1="254" y1="197" x2="282" y2="197" class="dg-l" marker-end="url(#cmpA)"/>
  <rect x="286" y="184" width="212" height="26" class="dg-bad"/><text x="300" y="202" class="dg-t">C ‖ MAC(P)</text>
  <text x="516" y="194" class="dg-tm">TAG OF THE PLAINTEXT</text>
  <text x="516" y="207" class="dg-tm">LEAKS PLAINTEXT EQUALITY.</text>
</svg>
<figcaption>The three compositions. Bellare and Namprempre proved in 2000 that only the first is generically secure; the other two are secure only for specific, fragile choices of components.</figcaption>
</figure>

<h3>Encrypt-then-MAC. That's It. That's the Answer.</h3>

<p>Encrypt the plaintext. Then MAC the <em>ciphertext</em>, including the IV or nonce, and including every byte of associated data. On receipt, recompute the tag and compare it in constant time <em>before you touch the decryption function</em>. If the tag is wrong, discard the whole thing and return one single, indistinguishable error.</p>

<p><strong>MAC-then-Encrypt</strong> forces the receiver to decrypt attacker-controlled data before it has any reason to trust it. Every byte of that decryption — the padding check, the length parse, the MAC comparison — is a potential oracle. This is precisely how Lucky 13 worked, and it is why TLS 1.3 abandoned the construction entirely in favor of AEAD.</p>

<p><strong>Encrypt-and-MAC</strong> ships a MAC of the plaintext, so identical plaintexts produce identical tags — a direct confidentiality leak, regardless of how good the cipher is.</p>

<div class="ckp-callout warn">
  <strong>If You Must Build It Yourself</strong>
  <p>Derive two independent keys from one master key with a KDF (SP 800-108); never use the same key for encryption and authentication. Encode lengths unambiguously before you MAC — if the MAC input is <code>IV ‖ C ‖ AAD</code> with no length framing, an attacker can shift bytes between the fields and produce the same tag. Compare tags with a constant-time function; a <code>memcmp</code> that returns early is a timing oracle. Verify first, decrypt second, and never expose which of the two failed.</p>
  <p>Then throw all of it away and use GCM, because you have just written four things you can get wrong and GCM has already gotten them right.</p>
</div>

<div class="ckp-pull">
  <p>Every hand-rolled Encrypt-then-MAC is a small, private cryptographic standard, written by one engineer, reviewed by nobody, and validated by no test vectors.</p>
  <cite>— On why AEAD modes exist</cite>
</div>
</section>

<div class="ckp-sep">Authenticated Encryption</div>

<!-- ─── SECTION 7 ─────────────────────────────────────────── -->
<section id="sec-ccm">
<h2>7. CCM — Counter with CBC-MAC</h2>

<div class="ckp-badges">
  <span class="badge spec">SP 800-38C</span>
  <span class="badge ok">AEAD</span>
  <span class="badge ok">Proven secure</span>
  <span class="badge ok">One key, one primitive</span>
  <span class="badge warn">Two passes</span>
  <span class="badge warn">Not online</span>
  <span class="badge bad">Nonce reuse is fatal</span>
  <span class="badge warn">Revision decided, 2025</span>
</div>

<p><strong>Architecture.</strong> CCM is CTR mode for confidentiality plus CBC-MAC for authenticity, using the same key for both, glued together with a careful encoding. It is nominally MAC-then-Encrypt — the combination that we just spent a section condemning — but it survives because Jonsson proved <em>this specific construction</em> secure. The proof depends on the exact formatting of the first block, which encodes the nonce, the flags, and the message length. Change the encoding and the proof is void. Do not change the encoding.</p>

<div class="ckp-code">
  <div class="code-label">CCM, structurally</div>
<pre><span class="c">// Pass 1 — authenticate</span>
B0  = flags ‖ N ‖ len(P)          <span class="c">// nonce and length are baked in</span>
T   = CBC-MAC(K, B0 ‖ encode(A) ‖ P)
T   = MSB_t(T)                     <span class="c">// t ∈ {4,6,8,10,12,14,16} bytes</span>

<span class="c">// Pass 2 — encrypt</span>
Ctr0 = flags ‖ N ‖ 0
C    = CTR(K, Ctr1..) ⊕ P
Tag  = T ⊕ MSB_t(AES-K(Ctr0))      <span class="c">// tag is masked with counter 0</span></pre>
</div>

<h3>The Nonce/Length Trade-off</h3>

<p>CCM's most distinctive feature is a design constraint you cannot escape: the nonce and the message-length field share one 15-byte budget. Pick a longer nonce and you can send shorter messages. This is a real interoperability trap, because two implementations that "both support AES-CCM" may be incompatible.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr><th>Length field $q$</th><th>Nonce size $15-q$</th><th>Max payload</th><th>Where you'll see it</th></tr>
</thead>
<tbody>
  <tr><td class="mono">2 bytes</td><td class="mono">13 bytes</td><td class="mono">65,535 B</td><td>IEEE 802.11 CCMP (Wi-Fi), 802.15.4</td></tr>
  <tr><td class="mono">3 bytes</td><td class="mono">12 bytes</td><td class="mono">16 MB</td><td>TLS/DTLS AES-CCM, IPsec</td></tr>
  <tr><td class="mono">4 bytes</td><td class="mono">11 bytes</td><td class="mono">4 GB</td><td>bulk storage protocols</td></tr>
  <tr><td class="mono">8 bytes</td><td class="mono">7 bytes</td><td class="mono">$2^{64}-1$ B</td><td>rarely — a 7-byte nonce is dangerously small</td></tr>
</tbody>
</table>
</div>

<h3>Security and Pitfalls</h3>

<ul class="ckp-hier">
  <li><strong>It is not online.</strong> $B_0$ contains the message length, so you must know how long the message is <em>before you start</em>. You cannot CCM-encrypt a stream of unknown length in a single pass. Implementations that buffer the whole message to work around this create memory-exhaustion denial-of-service in exactly the systems — sensors, radios — that chose CCM for its small footprint.</li>
  <li><strong>Two passes over the data.</strong> Roughly twice the block cipher work of a one-pass mode. On hardware with an AES accelerator and no GHASH accelerator, this is still often the fastest option — which is precisely why 802.11 and Bluetooth chose it.</li>
  <li><strong>Nonce reuse destroys everything.</strong> Reusing $(K, N)$ gives you keystream reuse (Equation 1) <em>and</em> lets the attacker begin forging. There is no partial failure.</li>
  <li><strong>Short tags are a standing invitation.</strong> The 4-byte tag option gives a $2^{-32}$ forgery probability per attempt. On a network endpoint an attacker can make millions of attempts. CCM-8 (an 8-byte tag) appears in TLS and IoT profiles; treat it as a deliberate, documented risk acceptance, not a default.</li>
  <li><strong>The AAD cannot be precomputed.</strong> Because the CBC-MAC chain starts at $B_0$, which contains the nonce, you cannot cache the authentication state for a static header the way you can in GCM. Every message pays the full AAD cost.</li>
  <li><strong>No key commitment.</strong> Same problem as GCM. See §13.3.</li>
</ul>

<div class="ckp-verdict">
  <div class="use">
    <h5>Use CCM when</h5>
    <ul>
      <li>You are on constrained hardware with an AES engine and no carry-less multiplier — CCM needs only the forward cipher, nothing else.</li>
      <li>You are implementing a protocol that mandates it: Wi-Fi (CCMP), Bluetooth LE, Zigbee, many IPsec and DTLS profiles.</li>
      <li>Code size matters more than throughput. CCM reuses one primitive for both jobs.</li>
      <li>Messages are short and their lengths are known in advance — packets, not streams.</li>
    </ul>
  </div>
  <div class="avoid">
    <h5>Avoid CCM when</h5>
    <ul>
      <li>You have hardware GHASH support (any modern x86 or ARM). GCM will be several times faster.</li>
      <li>You need to encrypt a stream whose length you do not know up front.</li>
      <li>You would be tempted to buffer unbounded input to satisfy the length requirement.</li>
    </ul>
  </div>
</div>
</section>

<div class="ckp-sep">The Workhorse</div>

<!-- ─── SECTION 8 ─────────────────────────────────────────── -->
<section id="sec-gcm">
<h2>8. GCM and GMAC — The Mode You Are Probably Using</h2>

<div class="ckp-badges">
  <span class="badge spec">SP 800-38D</span>
  <span class="badge ok">AEAD</span>
  <span class="badge ok">One pass, fully parallel</span>
  <span class="badge ok">Hardware-accelerated everywhere</span>
  <span class="badge bad">Nonce reuse = total break</span>
  <span class="badge bad">Not key-committing</span>
  <span class="badge warn">Revision open until 31 Jul 2026</span>
</div>

<p>AES-GCM protects the majority of the world's encrypted traffic. It is in TLS 1.2 and 1.3, in IPsec, in SSH, in QUIC, in MACsec, in every cloud provider's storage layer. It is fast — with AES-NI and PCLMULQDQ it runs at well under one cycle per byte — and it is one pass and fully parallelizable.</p>

<p>It is also the most dangerous mode in the standard, because its failure mode is not degradation. It is annihilation, triggered by a single mistake that leaves no trace in your logs.</p>

<h3>8.1 Architecture</h3>

<p>GCM is two machines bolted together. <strong>GCTR</strong> is counter mode. <strong>GHASH</strong> is a polynomial hash — a universal hash, not a cryptographic one — evaluated in $\mathrm{GF}(2^{128})$ with the reducing polynomial $x^{128}+x^7+x^2+x+1$. The hash key is $H = E_K(0^{128})$.</p>

<figure class="ckp-fig">
<svg viewBox="0 0 780 310" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="GCM: GCTR encryption path above, GHASH authentication chain below, tag masked by E_K(J0)">
  <defs>
    <marker id="gcmA" markerWidth="7" markerHeight="7" refX="6" refY="3" orient="auto">
      <path d="M0,0 L6,3 L0,6 Z" fill="#9898a4"/>
    </marker>
    <marker id="gcmG" markerWidth="7" markerHeight="7" refX="6" refY="3" orient="auto">
      <path d="M0,0 L6,3 L0,6 Z" fill="#c9a84c"/>
    </marker>
  </defs>

  <!-- ── BAND 1: GCTR ── -->
  <rect x="8"   y="12" width="76" height="28" class="dg-key"/>
  <rect x="108" y="12" width="64" height="28" class="dg-key"/>
  <rect x="230" y="12" width="64" height="28" class="dg-box"/>
  <rect x="350" y="12" width="64" height="28" class="dg-box"/>
  <text x="24"  y="31" class="dg-ta">IV</text>
  <text x="130" y="31" class="dg-ta">J₀</text>
  <text x="250" y="31" class="dg-t">CB₁</text>
  <text x="370" y="31" class="dg-t">CB₂</text>
  <text x="432" y="32" class="dg-tm">…</text>

  <line x1="84"  y1="26" x2="104" y2="26" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="172" y1="26" x2="226" y2="26" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="294" y1="26" x2="346" y2="26" class="dg-l" marker-end="url(#gcmA)"/>
  <text x="182" y="18" class="dg-tm">inc₃₂</text>
  <text x="302" y="18" class="dg-tm">inc₃₂</text>

  <rect x="108" y="66" width="64" height="32" class="dg-hash"/>
  <rect x="230" y="66" width="64" height="32" class="dg-hash"/>
  <rect x="350" y="66" width="64" height="32" class="dg-hash"/>
  <text x="116" y="87" class="dg-tb">AES-K</text>
  <text x="238" y="87" class="dg-tb">AES-K</text>
  <text x="358" y="87" class="dg-tb">AES-K</text>

  <line x1="140" y1="40" x2="140" y2="62" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="262" y1="40" x2="262" y2="62" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="382" y1="40" x2="382" y2="62" class="dg-l" marker-end="url(#gcmA)"/>

  <circle cx="262" cy="124" r="10" class="dg-xor"/><text x="257" y="128" class="dg-ta">⊕</text>
  <circle cx="382" cy="124" r="10" class="dg-xor"/><text x="377" y="128" class="dg-ta">⊕</text>
  <line x1="262" y1="98" x2="262" y2="114" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="382" y1="98" x2="382" y2="114" class="dg-l" marker-end="url(#gcmA)"/>
  <text x="196" y="128" class="dg-t">P₁</text>
  <text x="316" y="128" class="dg-t">P₂</text>
  <line x1="214" y1="124" x2="250" y2="124" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="334" y1="124" x2="370" y2="124" class="dg-l" marker-end="url(#gcmA)"/>

  <rect x="230" y="152" width="64" height="28" class="dg-box"/>
  <rect x="350" y="152" width="64" height="28" class="dg-box"/>
  <text x="252" y="171" class="dg-t">C₁</text>
  <text x="372" y="171" class="dg-t">C₂</text>
  <line x1="262" y1="134" x2="262" y2="148" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="382" y1="134" x2="382" y2="148" class="dg-l" marker-end="url(#gcmA)"/>

  <text x="470" y="80" class="dg-tm">96-BIT IV:</text>
  <text x="470" y="94" class="dg-tm">J₀ = IV ‖ 0³¹ ‖ 1</text>
  <text x="470" y="112" class="dg-tm">ANY OTHER LENGTH:</text>
  <text x="470" y="126" class="dg-tm">J₀ = GHASH(IV) ← SLOW</text>
  <text x="470" y="140" class="dg-tm">AND COLLISION-PRONE</text>

  <!-- E_K(J0) long wire -->
  <path d="M140,98 L140,204 L622,204 L622,214" class="dg-la" marker-end="url(#gcmG)"/>
  <text x="150" y="200" class="dg-ta">E_K(J₀)</text>

  <!-- ── BAND 2: GHASH ── -->
  <text x="8" y="206" class="dg-tm">GHASH_H</text>
  <text x="8" y="219" class="dg-tm">H = AES-K(0¹²⁸)</text>

  <text x="96" y="232" class="dg-t">0¹²⁸</text>
  <circle cx="142" cy="228" r="10" class="dg-xor"/><text x="137" y="232" class="dg-ta">⊕</text>
  <line x1="126" y1="228" x2="132" y2="228" class="dg-l"/>
  <rect x="180" y="214" width="44" height="28" class="dg-hash"/><text x="190" y="233" class="dg-tb">×H</text>
  <circle cx="262" cy="228" r="10" class="dg-xor"/><text x="257" y="232" class="dg-ta">⊕</text>
  <rect x="300" y="214" width="44" height="28" class="dg-hash"/><text x="310" y="233" class="dg-tb">×H</text>
  <circle cx="382" cy="228" r="10" class="dg-xor"/><text x="377" y="232" class="dg-ta">⊕</text>
  <rect x="420" y="214" width="44" height="28" class="dg-hash"/><text x="430" y="233" class="dg-tb">×H</text>
  <circle cx="502" cy="228" r="10" class="dg-xor"/><text x="497" y="232" class="dg-ta">⊕</text>
  <rect x="540" y="214" width="44" height="28" class="dg-hash"/><text x="550" y="233" class="dg-tb">×H</text>
  <circle cx="622" cy="228" r="10" class="dg-xor"/><text x="617" y="232" class="dg-ta">⊕</text>
  <rect x="656" y="214" width="60" height="28" class="dg-good"/><text x="676" y="233" class="dg-t">T</text>

  <line x1="152" y1="228" x2="176" y2="228" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="224" y1="228" x2="252" y2="228" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="272" y1="228" x2="296" y2="228" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="344" y1="228" x2="372" y2="228" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="392" y1="228" x2="416" y2="228" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="464" y1="228" x2="492" y2="228" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="512" y1="228" x2="536" y2="228" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="584" y1="228" x2="612" y2="228" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="632" y1="228" x2="652" y2="228" class="dg-l" marker-end="url(#gcmA)"/>

  <!-- inputs -->
  <rect x="110" y="262" width="64" height="26" class="dg-box"/><text x="136" y="280" class="dg-t">A</text>
  <line x1="142" y1="262" x2="142" y2="242" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="262" y1="180" x2="262" y2="214" class="dg-l" marker-end="url(#gcmA)"/>
  <line x1="382" y1="180" x2="382" y2="214" class="dg-l" marker-end="url(#gcmA)"/>
  <rect x="452" y="262" width="100" height="26" class="dg-box"/><text x="460" y="280" class="dg-t">len(A)‖len(C)</text>
  <line x1="502" y1="262" x2="502" y2="242" class="dg-l" marker-end="url(#gcmA)"/>
</svg>
<figcaption>GCM. The gold wire is the tag mask $E_K(J_0)$ — the only thing standing between the attacker and the authentication key. Repeat an IV and the mask cancels, GHASH becomes a polynomial the attacker can solve, and $H$ falls out.</figcaption>
</figure>

<div class="ckp-eq">
  <span class="eq-label">GCM tag — Eq. (8)</span>
  $$T = \mathrm{MSB}_t\Bigl(\mathrm{GHASH}_H\bigl(A, C\bigr) \oplus E_K(J_0)\Bigr) \tag{8}$$
</div>

<p>Two structural details matter enormously in practice.</p>

<p><strong>The 96-bit IV is a special case, and it is the only case you should use.</strong> If the IV is exactly 96 bits, $J_0$ is formed by simple concatenation. If it is any other length, $J_0$ is computed by running GHASH over the IV — which is slower, and, more importantly, means <em>different IVs can collide into the same $J_0$</em>. You have taken a nonce-uniqueness requirement and added a hash collision to it, for no benefit. Use 96-bit IVs. The 2026 revision is asking the community whether variable-length IVs are needed at all; the honest answer is no.</p>

<p><strong>GHASH is not a cryptographic hash.</strong> It is a polynomial evaluation. Its unforgeability comes entirely from the secrecy of $H$ and the one-time mask $E_K(J_0)$. Take away either and it offers no resistance whatsoever. This is not a flaw — it is what makes GCM fast — but it means the mode's security is far more brittle than the words "authenticated encryption" suggest.</p>

<h3>8.2 The Forbidden Attack</h3>

<div class="ckp-callout dead">
  <strong>One Repeated Nonce Ends the Key</strong>
  <p>Encrypt two messages with the same $(K, IV)$. The tag mask $E_K(J_0)$ is identical in both. XOR the two tags and the mask cancels, leaving a polynomial equation in the single unknown $H$ — with coefficients the attacker already knows, because they are the ciphertexts. Factor the polynomial over $\mathrm{GF}(2^{128})$, recover $H$, and you can now <em>forge a valid tag for any message you like</em> under that nonce. Joux described this in 2006; it is known as the <em>forbidden attack</em>.</p>
  <p>In 2016, Böck, Zauner, Devlin, Somorovsky and Jovanovic scanned the public internet and found HTTPS servers — including hardware load balancers from major vendors — repeating GCM nonces in production. They demonstrated full content injection against real, live sites [<a href="#ref-Nonce">Nonce</a>].</p>
</div>

<p>Understand what this means operationally. A nonce collision does not corrupt one message. It burns the key. Every message ever encrypted under that key becomes forgeable. And your monitoring will show nothing: no error, no failed decryption, no anomaly. The system works perfectly right up until someone else is also making valid ciphertexts.</p>

<h3>8.3 The Limits, and How to Not Exceed Them</h3>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr><th>Limit</th><th>Value</th><th>Why</th></tr>
</thead>
<tbody>
  <tr>
    <td>Plaintext per invocation</td>
    <td class="mono">$2^{39}-256$ bits (~64 GiB)</td>
    <td>The GCTR counter field is only 32 bits. Overflow it and the keystream repeats <em>within one message</em>.</td>
  </tr>
  <tr>
    <td>AAD per invocation</td>
    <td class="mono">$2^{64}-1$ bits</td>
    <td>Encoding limit in the final GHASH length block.</td>
  </tr>
  <tr>
    <td>Invocations per key, <strong>random IV</strong></td>
    <td class="mono">$2^{32}$</td>
    <td>Birthday collisions among random 96-bit nonces. This bounds collision probability at $2^{-32}$.</td>
  </tr>
  <tr>
    <td>Invocations per key, <strong>deterministic IV</strong></td>
    <td class="mono">size of the invocation field</td>
    <td>Uniqueness is structural, not probabilistic. This is the better construction.</td>
  </tr>
  <tr>
    <td>Total blocks per key (practice)</td>
    <td class="mono">$\approx 2^{59}$</td>
    <td>Not in SP 800-38D, but ANSSI requires rekeying here, and TLS 1.3 sets much tighter per-connection record limits. Respect the stricter of the two.</td>
  </tr>
</tbody>
</table>
</div>

<h4>Constructing the IV: Two Choices, and One Is Better</h4>

<p><strong>Deterministic (recommended).</strong> Split the 96-bit IV into a <em>fixed field</em> that identifies the encrypting device, context, or connection, and an <em>invocation field</em> that is a strict counter. Uniqueness becomes a structural property you can reason about, audit, and test. This is what TLS 1.3 does — it XORs the record sequence number into a per-connection static IV — and the forthcoming revision will explicitly bless that construction.</p>

<p><strong>Random.</strong> Draw 96 bits from an approved RBG per message. Simple, stateless, and capped at $2^{32}$ messages per key — which, as we established, is seventy-one minutes at a million messages a second. If you choose this, you <em>must</em> implement the message counter and the rekey. Nobody implements the message counter.</p>

<div class="ckp-callout warn">
  <strong>The Nonce Killers</strong>
  <p>Counters are only unique if your state survives. These are the situations that reset a counter or replay an RNG, and every one of them has caused a real-world nonce collision:</p>
  <p><strong>Virtual machine snapshot and restore.</strong> Fork the VM after the key is loaded and both children continue from the same counter — and the same RNG state. <strong>Container image with a baked-in seed.</strong> <strong>Process restart</strong> where the counter lives in memory and the key lives on disk. <strong>Horizontal scaling</strong>, where three replicas share a key from the secrets manager and each starts its counter at zero. <strong>Backup restore</strong> of a stateful encryptor. <strong>Embedded devices</strong> with no entropy source at first boot.</p>
  <p>If two things can hold the same key, they must not be able to hold the same counter. Partition the fixed field by instance. This is an architecture decision, not a coding decision.</p>
</div>

<h3>8.4 Tag Length: The Rule Is Changing</h3>

<p>SP 800-38D currently approves tags of 128, 120, 112, 104, and 96 bits for general use, plus 64 and 32 bits for specific constrained applications hedged with restrictions in its Appendix C. Those restrictions exist because of Ferguson's 2005 observation: with a short tag and a long message, an attacker's forgery probability is <em>far higher</em> than the naive $2^{-t}$, and a successful forgery leaks information about $H$, making subsequent forgeries easier.</p>

<div class="ckp-ruling">
  <span class="rl">Live change</span>
  <p>The SP 800-38D revision <strong>removes all tag lengths below 96 bits</strong>. If you ship GCM with a 64-bit tag today, you are shipping a configuration that is being deleted from the standard. Use 128 bits. There is no meaningful cost.</p>
</div>

<h3>8.5 GCM Has No Key Commitment</h3>

<p>Given two keys $K_1$ and $K_2$, an attacker can construct a single ciphertext that decrypts <em>validly</em> — tag and all — under both, to two entirely different plaintexts. GCM's tag binds the ciphertext to the key only in the sense that a random key won't verify; it does not bind it to <em>one</em> key.</p>

<p>Two consequences, both realized in the field:</p>

<ul class="ckp-hier">
  <li><strong>Invisible Salamanders.</strong> Facebook Messenger's abuse-reporting scheme let a sender "frank" an encrypted image so a reported message could be attributed. Because GCM is non-committing, an attacker could craft an image that decrypted to something innocuous under the reporting key and something abusive under the recipient's — defeating the moderation system entirely [<a href="#ref-Salamanders">Salamanders</a>].</li>
  <li><strong>Partitioning oracles.</strong> When a key is derived from a password, an attacker who can submit a ciphertext and learn whether it decrypted successfully can craft one ciphertext that is valid under <em>thousands</em> of candidate passwords at once. Each query eliminates a huge slice of the password space. Len, Grubbs and Ristenpart used this to recover Shadowsocks passwords in a few hundred queries [<a href="#ref-Partition">Partition</a>].</li>
</ul>

<p><strong>The fix, since NIST won't give you one:</strong> put a commitment in the AAD. Concretely, derive $(K_{enc}, K_{commit})$ from your master secret with a KDF, transmit $K_{commit}$ alongside the ciphertext, and have the receiver check it. Or use the "padding fix": prepend a block of zeros to the plaintext before encryption and require it to be zero on decryption. Either turns GCM into a committing AEAD at trivial cost. Do this whenever keys are low-entropy or attacker-influenced.</p>

<h3>8.6 Implementation Hazards</h3>

<ul class="ckp-hier">
  <li><strong>Table-driven GHASH is a cache-timing side channel.</strong> The classic software implementation uses precomputed multiplication tables indexed by secret-dependent data. Use the carry-less multiply instruction (<code>PCLMULQDQ</code> on x86, <code>PMULL</code> on ARM) or a bitsliced implementation. If you are on a platform with neither, seriously consider CCM instead.</li>
  <li><strong>Never release unverified plaintext.</strong> GCM decryption produces plaintext <em>before</em> the tag is checked, because it's just CTR mode. Streaming APIs that hand out that plaintext as it becomes available have re-created a decryption oracle. The API must not emit a single byte until the tag verifies.</li>
  <li><strong>Compare tags in constant time.</strong> An early-exit comparison is a byte-at-a-time forgery oracle.</li>
  <li><strong>Enforce a verification-failure budget.</strong> A GCM implementation that will accept unlimited forgery attempts against a truncated tag is a different security proposition from one that kills the key after ten. The standard says to bound this. Bound it.</li>
</ul>

<h3>8.7 GMAC</h3>

<p>GMAC is GCM with an empty plaintext: authentication only, no encryption. It is fast and it is fine — <em>and it inherits every single nonce requirement of GCM</em>. A repeated nonce in GMAC recovers $H$ just as surely as in GCM. Engineers reach for GMAC as "just a MAC" and forget that, unlike CMAC or HMAC, it is stateful and fragile. If you need a MAC and you are not already running GCM, use HMAC or CMAC and sleep better.</p>

<div class="ckp-verdict">
  <div class="use">
    <h5>Use GCM when</h5>
    <ul>
      <li>You are encrypting network traffic and you have hardware AES and GHASH — which is to say, on any server, phone, or laptop made in the last decade.</li>
      <li>You can guarantee nonce uniqueness structurally, with a counter in a fixed-field-partitioned IV.</li>
      <li>You need one-pass, parallel, high-throughput AEAD with authenticated headers.</li>
      <li>Use a 128-bit tag, a 96-bit IV, and put your context in the AAD.</li>
    </ul>
  </div>
  <div class="avoid">
    <h5>Avoid GCM when</h5>
    <ul>
      <li>You cannot prove nonce uniqueness. If your architecture involves shared keys across replicas, snapshots, or restarts, and you have not partitioned the nonce space — you will collide, and the failure is total. Use AES-GCM-SIV (RFC 8452) even though it is not NIST-approved, or restructure until you can prove it.</li>
      <li>Keys come from passwords, or a receiver trial-decrypts among candidate keys. Add a commitment first.</li>
      <li>You are encrypting data at rest with long-lived keys and no rekeying story.</li>
      <li>Your platform has no constant-time $\mathrm{GF}(2^{128})$ multiply.</li>
    </ul>
  </div>
</div>

<div class="ckp-pull">
  <p>GCM is a race car with no seat belts. Driven correctly it is the fastest thing on the road. The engineering discipline it demands is not optional equipment — it is the mode.</p>
  <cite>— On the operational cost of AES-GCM</cite>
</div>
</section>

<div class="ckp-sep">Lightweight AEAD</div>

<!-- ─── SECTION 9 ─────────────────────────────────────────── -->
<section id="sec-ascon">
<h2>9. Ascon — The New One</h2>

<div class="ckp-badges">
  <span class="badge spec">SP 800-232 · Final, Aug 2025</span>
  <span class="badge ok">AEAD</span>
  <span class="badge ok">Single pass, online</span>
  <span class="badge ok">Tiny in hardware</span>
  <span class="badge ok">Masks cheaply</span>
  <span class="badge bad">Nonce reuse is fatal</span>
  <span class="badge warn">Not a block cipher mode</span>
</div>

<p>In August 2025 NIST finalized SP 800-232, standardizing the Ascon family after a decade-long lightweight cryptography competition. It is the first NIST-approved AEAD that is <em>not</em> a mode of AES. It is a permutation, used as a duplex sponge.</p>

<p><strong>Architecture.</strong> A 320-bit state. Load the key and nonce, stir with twelve rounds of the permutation $p$, absorb associated data, then absorb plaintext and squeeze ciphertext in the same operation, then finalize with the key and twelve more rounds to produce the tag. The key, nonce, and tag are 128 bits each.</p>

<figure class="ckp-fig">
<svg viewBox="0 0 780 200" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Ascon-AEAD128 duplex sponge: initialization, associated data absorption, plaintext duplexing, finalization">
  <defs>
    <marker id="ascA" markerWidth="7" markerHeight="7" refX="6" refY="3" orient="auto">
      <path d="M0,0 L6,3 L0,6 Z" fill="#9898a4"/>
    </marker>
  </defs>

  <rect x="6"   y="84" width="72" height="34" class="dg-key"/>
  <text x="16"  y="106" class="dg-ta">IV‖K‖N</text>
  <rect x="96"  y="80" width="48" height="42" class="dg-hash"/>
  <text x="106" y="106" class="dg-tb">p¹²</text>
  <rect x="240" y="80" width="44" height="42" class="dg-hash"/>
  <text x="248" y="106" class="dg-tb">p⁸</text>
  <rect x="384" y="80" width="44" height="42" class="dg-hash"/>
  <text x="392" y="106" class="dg-tb">p⁸</text>
  <rect x="534" y="80" width="48" height="42" class="dg-hash"/>
  <text x="544" y="106" class="dg-tb">p¹²</text>
  <rect x="634" y="84" width="60" height="34" class="dg-good"/>
  <text x="656" y="106" class="dg-t">T</text>

  <circle cx="166" cy="101" r="10" class="dg-xor"/><text x="161" y="105" class="dg-ta">⊕</text>
  <circle cx="212" cy="101" r="10" class="dg-xor"/><text x="207" y="105" class="dg-ta">⊕</text>
  <circle cx="310" cy="101" r="10" class="dg-xor"/><text x="305" y="105" class="dg-ta">⊕</text>
  <circle cx="356" cy="101" r="10" class="dg-xor"/><text x="351" y="105" class="dg-ta">⊕</text>
  <circle cx="456" cy="101" r="10" class="dg-xor"/><text x="451" y="105" class="dg-ta">⊕</text>
  <circle cx="506" cy="101" r="10" class="dg-xor"/><text x="501" y="105" class="dg-ta">⊕</text>
  <circle cx="606" cy="101" r="10" class="dg-xor"/><text x="601" y="105" class="dg-ta">⊕</text>

  <line x1="78"  y1="101" x2="92"  y2="101" class="dg-l" marker-end="url(#ascA)"/>
  <line x1="144" y1="101" x2="156" y2="101" class="dg-l" marker-end="url(#ascA)"/>
  <line x1="176" y1="101" x2="202" y2="101" class="dg-l" marker-end="url(#ascA)"/>
  <line x1="222" y1="101" x2="236" y2="101" class="dg-l" marker-end="url(#ascA)"/>
  <line x1="284" y1="101" x2="300" y2="101" class="dg-l" marker-end="url(#ascA)"/>
  <line x1="320" y1="101" x2="346" y2="101" class="dg-l" marker-end="url(#ascA)"/>
  <line x1="366" y1="101" x2="380" y2="101" class="dg-l" marker-end="url(#ascA)"/>
  <line x1="428" y1="101" x2="446" y2="101" class="dg-l" marker-end="url(#ascA)"/>
  <line x1="466" y1="101" x2="496" y2="101" class="dg-l" marker-end="url(#ascA)"/>
  <line x1="516" y1="101" x2="530" y2="101" class="dg-l" marker-end="url(#ascA)"/>
  <line x1="582" y1="101" x2="596" y2="101" class="dg-l" marker-end="url(#ascA)"/>
  <line x1="616" y1="101" x2="630" y2="101" class="dg-l" marker-end="url(#ascA)"/>

  <text x="158" y="146" class="dg-tm">K</text>
  <line x1="166" y1="136" x2="166" y2="113" class="dg-l" marker-end="url(#ascA)"/>
  <text x="204" y="60" class="dg-t">A₁</text>
  <line x1="212" y1="66" x2="212" y2="89" class="dg-l" marker-end="url(#ascA)"/>
  <text x="298" y="146" class="dg-tm">1 (SEP)</text>
  <line x1="310" y1="136" x2="310" y2="113" class="dg-l" marker-end="url(#ascA)"/>
  <text x="348" y="60" class="dg-t">P₁</text>
  <line x1="356" y1="66" x2="356" y2="89" class="dg-l" marker-end="url(#ascA)"/>
  <text x="348" y="152" class="dg-t">C₁</text>
  <line x1="356" y1="113" x2="356" y2="138" class="dg-l" marker-end="url(#ascA)"/>
  <text x="448" y="60" class="dg-t">P₂</text>
  <line x1="456" y1="66" x2="456" y2="89" class="dg-l" marker-end="url(#ascA)"/>
  <text x="448" y="152" class="dg-t">C₂</text>
  <line x1="456" y1="113" x2="456" y2="138" class="dg-l" marker-end="url(#ascA)"/>
  <text x="498" y="146" class="dg-tm">K</text>
  <line x1="506" y1="136" x2="506" y2="113" class="dg-l" marker-end="url(#ascA)"/>
  <text x="598" y="146" class="dg-tm">K</text>
  <line x1="606" y1="136" x2="606" y2="113" class="dg-l" marker-end="url(#ascA)"/>

  <text x="6" y="24" class="dg-tm">INITIALIZE</text>
  <text x="196" y="24" class="dg-tm">ABSORB AAD</text>
  <text x="340" y="24" class="dg-tm">DUPLEX PLAINTEXT → CIPHERTEXT</text>
  <text x="534" y="24" class="dg-tm">FINALIZE</text>
  <line x1="6" y1="32" x2="186" y2="32" class="dg-dash"/>
  <line x1="196" y1="32" x2="330" y2="32" class="dg-dash"/>
  <line x1="340" y1="32" x2="524" y2="32" class="dg-dash"/>
  <line x1="534" y1="32" x2="700" y2="32" class="dg-dash"/>
</svg>
<figcaption>Ascon-AEAD128. One 320-bit state, one permutation, no block cipher, no field arithmetic, no separate MAC. The plaintext XOR simultaneously produces ciphertext and updates the state — this is what "duplex" means.</figcaption>
</figure>

<h3>Why It Exists</h3>

<p>AES-GCM is superb on a CPU with AES-NI. On a thirty-cent microcontroller with no crypto instructions, GCM is miserable: the $\mathrm{GF}(2^{128})$ multiply is expensive in software, the tables are large, and the tables leak through cache and power. Ascon needs one small permutation, a few hundred bytes of state, and it masks cheaply against power analysis — which matters enormously for a smart meter or a medical implant sitting in an attacker's hands.</p>

<h3>Pitfalls</h3>

<ul class="ckp-hier">
  <li><strong>It is still nonce-based.</strong> Ascon is not misuse-resistant. Repeating a nonce under the same key is as fatal here as in GCM. The constrained devices most likely to use Ascon are also the ones most likely to have bad entropy at boot and no persistent counter. Solve that problem before you ship.</li>
  <li><strong>Per-key data limits.</strong> SP 800-232 specifies explicit limits on data processed under a single key. On a sensor you will never approach them; if you find yourself using Ascon for bulk data, you are using the wrong tool.</li>
  <li><strong>Ecosystem lag.</strong> FIPS 140-3 module validation, library support, and hardware IP for Ascon are all younger than for AES. Check that your certification path exists before you commit.</li>
</ul>

<div class="ckp-verdict">
  <div class="use">
    <h5>Use Ascon when</h5>
    <ul>
      <li>The target is constrained: IoT sensors, RFID, medical implants, low-power radios, secure elements.</li>
      <li>There is no AES hardware, or side-channel resistance under masking is a design requirement.</li>
      <li>You want AEAD, hashing, and an XOF from a single 320-bit permutation, to save gates and code.</li>
    </ul>
  </div>
  <div class="avoid">
    <h5>Avoid Ascon when</h5>
    <ul>
      <li>You have AES-NI. GCM will be far faster and is more widely validated.</li>
      <li>Your compliance regime does not yet recognize it in your module.</li>
      <li>You need misuse resistance. Ascon does not provide it either.</li>
    </ul>
  </div>
</div>
</section>

<div class="ckp-sep">Storage</div>

<!-- ─── SECTION 10 ────────────────────────────────────────── -->
<section id="sec-xts">
<h2>10. XTS-AES — Encryption for Disks</h2>

<div class="ckp-badges">
  <span class="badge spec">SP 800-38E</span>
  <span class="badge ok">Length-preserving</span>
  <span class="badge ok">Random access</span>
  <span class="badge bad">NO integrity</span>
  <span class="badge bad">No freshness</span>
  <span class="badge warn">Leaks equality per sector/offset</span>
  <span class="badge warn">Revision decided, 2024</span>
</div>

<p>Storage encryption has a brutal constraint: the ciphertext must be exactly as long as the plaintext, because a 512-byte sector has 512 bytes and there is nowhere to put a nonce or a tag. Every desirable property of AEAD is therefore off the table. XTS is what remains once you accept that.</p>

<p><strong>Architecture.</strong> XTS is a <em>tweakable</em> block cipher — the XEX construction with ciphertext stealing. Two keys: $K_1$ encrypts the data, $K_2$ derives the tweak. The tweak for data unit $i$ is $E_{K_2}(i)$, and the tweak for block $j$ within that unit is that value multiplied by $\alpha^j$ in $\mathrm{GF}(2^{128})$. The tweak is XORed in before and after the cipher.</p>

<div class="ckp-eq">
  <span class="eq-label">XTS — Eq. (9)</span>
  $$T_j = E_{K_2}(i) \otimes \alpha^{\,j}, \qquad C_j = E_{K_1}\!\left(P_j \oplus T_j\right) \oplus T_j \tag{9}$$
</div>

<figure class="ckp-fig">
<svg viewBox="0 0 720 285" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="XTS-AES: tweak derived from the data unit number, multiplied by alpha per block, XORed before and after the cipher">
  <defs>
    <marker id="xtsA" markerWidth="7" markerHeight="7" refX="6" refY="3" orient="auto">
      <path d="M0,0 L6,3 L0,6 Z" fill="#9898a4"/>
    </marker>
    <marker id="xtsG" markerWidth="7" markerHeight="7" refX="6" refY="3" orient="auto">
      <path d="M0,0 L6,3 L0,6 Z" fill="#c9a84c"/>
    </marker>
  </defs>

  <rect x="8"   y="20" width="76" height="30" class="dg-box"/>
  <text x="16"  y="40" class="dg-t">unit i</text>
  <rect x="104" y="16" width="76" height="38" class="dg-hash"/>
  <text x="112" y="40" class="dg-tb">AES-K₂</text>
  <line x1="84" y1="35" x2="100" y2="35" class="dg-l" marker-end="url(#xtsA)"/>

  <path d="M180,35 L225,35 L225,104" class="dg-la" marker-end="url(#xtsG)"/>

  <rect x="195" y="108" width="60" height="26" class="dg-key"/>
  <text x="215" y="126" class="dg-ta">T₀</text>
  <rect x="395" y="108" width="60" height="26" class="dg-key"/>
  <text x="415" y="126" class="dg-ta">T₁</text>
  <line x1="255" y1="121" x2="391" y2="121" class="dg-la" marker-end="url(#xtsG)"/>
  <text x="300" y="114" class="dg-ta">⊗ α</text>
  <line x1="455" y1="121" x2="500" y2="121" class="dg-la" marker-end="url(#xtsG)"/>
  <text x="508" y="126" class="dg-tm">…</text>

  <!-- block 0 -->
  <rect x="275" y="58" width="90" height="26" class="dg-box"/>
  <text x="310" y="76" class="dg-t">P₀</text>
  <circle cx="320" cy="146" r="10" class="dg-xor"/><text x="315" y="150" class="dg-ta">⊕</text>
  <line x1="320" y1="84" x2="320" y2="136" class="dg-l" marker-end="url(#xtsA)"/>
  <path d="M255,121 L285,121 L285,146 L308,146" class="dg-la" marker-end="url(#xtsG)"/>
  <rect x="275" y="166" width="90" height="34" class="dg-hash"/>
  <text x="290" y="188" class="dg-tb">AES-K₁</text>
  <line x1="320" y1="156" x2="320" y2="162" class="dg-l" marker-end="url(#xtsA)"/>
  <circle cx="320" cy="222" r="10" class="dg-xor"/><text x="315" y="226" class="dg-ta">⊕</text>
  <line x1="320" y1="200" x2="320" y2="212" class="dg-l" marker-end="url(#xtsA)"/>
  <path d="M225,134 L225,222 L308,222" class="dg-la" marker-end="url(#xtsG)"/>
  <rect x="275" y="242" width="90" height="28" class="dg-box"/>
  <text x="310" y="261" class="dg-t">C₀</text>
  <line x1="320" y1="232" x2="320" y2="238" class="dg-l" marker-end="url(#xtsA)"/>

  <!-- block 1 -->
  <rect x="475" y="58" width="90" height="26" class="dg-box"/>
  <text x="510" y="76" class="dg-t">P₁</text>
  <circle cx="520" cy="146" r="10" class="dg-xor"/><text x="515" y="150" class="dg-ta">⊕</text>
  <line x1="520" y1="84" x2="520" y2="136" class="dg-l" marker-end="url(#xtsA)"/>
  <path d="M455,121 L485,121 L485,146 L508,146" class="dg-la" marker-end="url(#xtsG)"/>
  <rect x="475" y="166" width="90" height="34" class="dg-hash"/>
  <text x="490" y="188" class="dg-tb">AES-K₁</text>
  <line x1="520" y1="156" x2="520" y2="162" class="dg-l" marker-end="url(#xtsA)"/>
  <circle cx="520" cy="222" r="10" class="dg-xor"/><text x="515" y="226" class="dg-ta">⊕</text>
  <line x1="520" y1="200" x2="520" y2="212" class="dg-l" marker-end="url(#xtsA)"/>
  <path d="M425,134 L425,222 L508,222" class="dg-la" marker-end="url(#xtsG)"/>
  <rect x="475" y="242" width="90" height="28" class="dg-box"/>
  <text x="510" y="261" class="dg-t">C₁</text>
  <line x1="520" y1="232" x2="520" y2="238" class="dg-l" marker-end="url(#xtsA)"/>

  <text x="600" y="180" class="dg-tm">NO NONCE.</text>
  <text x="600" y="194" class="dg-tm">NO TAG.</text>
  <text x="600" y="208" class="dg-tm">NO ROOM.</text>
</svg>
<figcaption>XTS-AES. The tweak makes each block position within each sector a different permutation — so identical plaintext at different offsets encrypts differently. It does nothing about identical plaintext at the <em>same</em> offset in the <em>same</em> sector.</figcaption>
</figure>

<h3>What XTS Actually Protects Against</h3>

<p>Exactly one threat: <strong>an adversary who obtains the drive at rest, once.</strong> A stolen laptop. A decommissioned disk. A seized server. For that threat, XTS is appropriate and effective.</p>

<p>It protects against nothing else, and the list of "nothing else" is long enough to matter:</p>

<ul class="ckp-hier">
  <li><strong>No integrity.</strong> An attacker who can write to the disk can flip bits. He cannot choose the resulting plaintext — the 16-byte block becomes random garbage — but he can corrupt precisely the block he wants, deterministically, and random garbage in the right place is often exploitable. XTS gives you <em>randomized corruption</em>, not tamper detection.</li>
  <li><strong>No freshness.</strong> An attacker with two snapshots of the disk can roll a sector back to its earlier value. The system will accept it. Nothing in XTS binds a sector to a point in time.</li>
  <li><strong>Deterministic per position.</strong> Write the same block to the same offset of the same sector twice and you get the same ciphertext twice. An adversary who watches the drive over time learns which sectors changed and which reverted — a rich side channel against, say, a database.</li>
  <li><strong>Copy-and-paste within an offset.</strong> Two blocks at the same offset in the same sector index share a tweak. Ciphertext can be relocated between them.</li>
  <li><strong>Data unit size is capped.</strong> SP 800-38E limits a data unit to $2^{20}$ AES blocks (16 MiB). Do not encrypt a whole file as one "unit".</li>
  <li><strong>$K_1 \ne K_2$.</strong> FIPS implementations must check this. It is a real check, and it is skipped in real code.</li>
</ul>

<div class="ckp-callout warn">
  <strong>The Key-Length Confusion</strong>
  <p>"XTS-AES-256" means two 256-bit keys — a 512-bit key blob. It does not give you 512 bits of security. The security level is that of AES-256. Vendors and auditors get this wrong constantly, in both directions.</p>
</div>

<div class="ckp-verdict">
  <div class="use">
    <h5>Use XTS when</h5>
    <ul>
      <li>You are doing block-level full-disk or full-volume encryption and the ciphertext must be exactly as long as the plaintext. BitLocker, FileVault, LUKS/dm-crypt, and VeraCrypt all do this, correctly.</li>
      <li>The threat is device loss, not an active adversary with write access.</li>
    </ul>
  </div>
  <div class="avoid">
    <h5>Never use XTS when</h5>
    <ul>
      <li>You are encrypting anything that travels over a network. XTS is not a transport mode. It has no nonce and no authentication.</li>
      <li>You are encrypting individual files or database fields and you <em>could</em> have stored a nonce and a tag. If you have 32 spare bytes, use AEAD.</li>
      <li>The attacker may write to the storage. Then you need authenticated storage — dm-integrity underneath, or a filesystem with checksums, or an AEAD layer above.</li>
    </ul>
  </div>
</div>
</section>

<div class="ckp-sep">Key Wrapping</div>

<!-- ─── SECTION 11 ────────────────────────────────────────── -->
<section id="sec-kw">
<h2>11. KW, KWP, TKW — Wrapping Keys</h2>

<div class="ckp-badges">
  <span class="badge spec">SP 800-38F</span>
  <span class="badge ok">Deterministic AE</span>
  <span class="badge ok">No IV needed</span>
  <span class="badge warn">6 passes — slow</span>
  <span class="badge bad">No associated data</span>
  <span class="badge bad">TKW is dead with 3DES</span>
</div>

<p>Key wrapping is a special case with a special property: the plaintext is a cryptographic key, so it is already uniformly random. That means you do not need an IV to randomize it — the plaintext randomizes itself. This lets you build a <em>deterministic authenticated encryption</em> scheme, which is exactly what you want, because a key management system that has to track nonces is a key management system that will eventually reuse one.</p>

<p><strong>Architecture.</strong> AES-KW takes the key material as 64-bit semiblocks, prepends a fixed integrity check value (<code>A6A6A6A6A6A6A6A6</code>), and then shuffles: six passes over the array, each pass running AES over a pair of semiblocks and mixing in a counter. Integrity comes from the redundancy — unwrap, and if the ICV does not come back exactly, reject. KWP extends this to key material that is not a multiple of 8 bytes by encoding the true length into the ICV. TKW is the TDEA version and should be considered dead.</p>

<div class="ckp-code">
  <div class="code-label">Why AES-KW is slow — and why that is fine</div>
<pre><span class="c">// 6 passes over n semiblocks = 6n AES invocations</span>
<span class="c">// Wrapping a 256-bit key (4 semiblocks + ICV):  6 x 4 = 24 AES calls</span>
<span class="c">// vs. AES-GCM on 32 bytes:                       ~4 AES calls + GHASH</span>

<span class="c">// You wrap a key once per rotation. You encrypt data constantly.</span>
<span class="c">// Optimizing the wrong one is a classic mistake.</span></pre>
</div>

<h3>Pitfalls</h3>

<ul class="ckp-hier">
  <li><strong>There is no associated data field.</strong> This is the big one. You cannot bind a wrapped key to its identifier, its algorithm, its policy, or its expiry. If your protocol stores "key ID 7 → wrapped blob," an attacker with write access to the store can swap blob 7 for blob 9 and the unwrap will succeed perfectly. The KEK proves the blob is <em>a</em> key it wrapped; it does not prove it is <em>this</em> key. You must bind the context yourself, at a higher layer — or use an AEAD instead.</li>
  <li><strong>It is deterministic.</strong> Wrapping the same key under the same KEK twice produces identical output. Usually harmless; occasionally a leak.</li>
  <li><strong>Its provable-security story is thinner than you'd like.</strong> The design predates the modern formalization of the key-wrap problem, which Rogaway and Shrimpton gave in 2006 along with the SIV construction [<a href="#ref-RS06">RS06</a>]. SIV is cleaner, provably misuse-resistant, and supports associated data — and is <em>not</em> a NIST mode.</li>
  <li><strong>Do not use it for bulk data.</strong> Six passes, no streaming, no parallelism.</li>
</ul>

<div class="ckp-ruling">
  <span class="rl">Ruling</span>
  <p>SP 800-38F also approves the AEAD modes for key wrapping. Use <strong>AES-GCM with a unique nonce and the key's full context in the AAD</strong> unless a standard forces KW on you. You get binding, and you get it in one pass.</p>
</div>
</section>

<div class="ckp-sep">Format Preservation</div>

<!-- ─── SECTION 12 ────────────────────────────────────────── -->
<section id="sec-fpe">
<h2>12. FF1 — Format-Preserving Encryption</h2>

<div class="ckp-badges">
  <span class="badge spec">SP 800-38G / Rev. 1 (draft)</span>
  <span class="badge ok">Preserves format and length</span>
  <span class="badge bad">No integrity</span>
  <span class="badge bad">Deterministic</span>
  <span class="badge bad">Small domains are broken</span>
  <span class="badge warn">FF3 and FF3-1 deleted</span>
</div>

<p>FPE encrypts a nine-digit Social Security number into a nine-digit number. A sixteen-digit card number into sixteen digits. It exists for exactly one reason: you have a legacy database with a <code>CHAR(9)</code> column and you cannot change the schema, and someone has told you the column must be encrypted.</p>

<p>That is a compliance requirement, not a security requirement, and you should hold that distinction firmly in mind, because FPE is the weakest primitive in this document.</p>

<h3>Architecture</h3>

<p>FF1 is a ten-round Feistel network over strings of numerals in an arbitrary radix. The round function is built from AES — specifically, a CBC-MAC over an encoding of the round number, the tweak, and half the data. The <em>tweak</em> is a non-secret input that acts as a changeable part of the key.</p>

<h3>The Curse of Small Domains</h3>

<p>A block cipher on a $2^{128}$-element domain is safe partly because the attacker cannot enumerate the domain. A cipher on a domain of one million elements is a different animal: the attacker can plausibly compromise a <em>meaningful fraction of the entire domain</em>, and Feistel networks fall apart under that kind of pressure. A decade of cryptanalysis has been unkind:</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr><th>Year</th><th>Result</th><th>Consequence</th></tr>
</thead>
<tbody>
  <tr><td class="mono">2015</td><td>Dworkin &amp; Perlner: FF2 (VAES3) does not deliver 128-bit security</td><td class="no">FF2 removed before publication</td></tr>
  <tr><td class="mono">2016</td><td>Bellare, Hoang &amp; Tessaro: message recovery on Feistel-based FPE</td><td class="mid">domain-size warnings</td></tr>
  <tr><td class="mono">2017</td><td>Durak &amp; Vaudenay: FF3 broken over small domains</td><td class="mid">FF3 → FF3-1 (tweak cut to 56 bits)</td></tr>
  <tr><td class="mono">2018</td><td>Hoang, Tessaro &amp; Trieu: "The Curse of Small Domains"</td><td class="mid">minimum domain raised to $10^6$</td></tr>
  <tr><td class="mono">2019</td><td>Hoang, Miller &amp; Trieu: "Attacks Only Get Better" — FF3 on <em>large</em> domains</td><td class="mid">further pressure</td></tr>
  <tr><td class="mono">2021</td><td>Beyne: linear cryptanalysis of FF3-1 — a weakness in the tweak schedule</td><td class="no"><strong>FF3 and FF3-1 removed entirely</strong> in the Rev. 1 draft</td></tr>
</tbody>
</table>
</div>

<p>The survivor is FF1, alone, with a hard requirement that the domain size $\mathrm{radix}^{\,minlen}$ be at least <strong>one million</strong>. At that domain size NIST estimates the data complexity of a message-recovery attack at around $2^{77}$ — comfortably out of reach. Below it, you are in the zone where the papers above apply.</p>

<div class="ckp-callout dead">
  <strong>Floating Point Will Ruin Your Day</strong>
  <p>The original FF1 specification used a <code>LOG()</code> function to compute a byte length. Implemented with floating-point arithmetic, it silently returns the wrong value for certain inputs — a bug Bleichenbacher found in Bouncy Castle. Two implementations that disagree on that one value produce ciphertexts that will not decrypt. The Rev. 1 draft rewrites the step in terms of an exact integer <code>BITLEN()</code> and <em>forbids floating-point arithmetic outright</em>. If you maintain an FF1 implementation, go and look at this line right now.</p>
</div>

<h3>Use the Tweak. Seriously.</h3>

<p>FPE is deterministic: the same plaintext under the same key and tweak always gives the same ciphertext. In a database of a hundred million card numbers where only the middle six digits are encrypted, roughly a hundred records will share each of the million possible values — and with a constant tweak, they will all share the same ciphertext. Compromise one, compromise a hundred.</p>

<p>The fix is in the standard, and it is the whole point of the tweak: <strong>use the surrounding non-encrypted data as the tweak.</strong> The leading six and trailing four digits of the card, the row's primary key, the customer ID — anything stably associated with that specific record. Now the hundred colliding plaintexts produce a hundred different ciphertexts.</p>

<div class="ckp-verdict">
  <div class="use">
    <h5>Use FF1 when</h5>
    <ul>
      <li>A legacy system's schema physically cannot hold a nonce, a tag, or a longer field, and you have exhausted the alternatives.</li>
      <li>Your domain is at least a million values, and you can supply a distinct, record-specific tweak.</li>
    </ul>
  </div>
  <div class="avoid">
    <h5>Avoid FF1 when</h5>
    <ul>
      <li>You could use tokenization instead — a random token plus a lookup vault. It gives strictly better security with no cryptanalytic surface at all, and it is usually less work than you think.</li>
      <li>You need integrity, or non-determinism, or protection against an adversary with chosen-plaintext access to your encryption service.</li>
      <li>Anyone tells you FPE "makes the database safe." It makes the field unreadable. Re-identification from surrounding metadata remains entirely possible.</li>
    </ul>
  </div>
</div>
</section>

<div class="ckp-sep">Engineering</div>

<!-- ─── SECTION 13 ────────────────────────────────────────── -->
<section id="sec-eng">
<h2>13. The Engineering That Actually Kills You</h2>

<p>You have chosen a mode. You are now roughly ten percent of the way to a secure system. Everything below is where the bodies are buried, and none of it appears in the mode's name.</p>

<h3>13.1 Nonce Management Is an Architecture Problem</h3>

<p>Say it plainly: <strong>nonce reuse is the single most destructive bug in modern cryptography</strong>, and it is almost never a cryptographic error. It is a distributed-systems error. It is a deployment error. It is an infrastructure error that happens to have cryptographic consequences.</p>

<p>The question is never "did I write the counter increment correctly." The question is: <em>can two entities ever hold the same key and the same counter value at the same time?</em> Work through every path in your system that duplicates state.</p>

<div class="ckp-code">
  <div class="code-label">Nonce strategies, ranked</div>
<pre><span class="g">BEST  </span> Deterministic, structurally partitioned:
         IV = [ fixed field: instance/shard/epoch ] ‖ [ counter ]
         Uniqueness is a property of the architecture, not of luck.
         Requires: durable counter, unique instance IDs, an epoch bump on restore.

<span class="g">GOOD  </span> Key derived per message/session:
         K_msg = KDF(K_master, context)   <span class="c">// then any nonce is fine</span>
         Sidesteps the problem entirely. Costs one KDF call.

<span class="k">OK    </span> Random 96-bit from an approved RBG:
         Simple, stateless. Hard cap: 2^32 messages per key.
         <span class="k">You must implement the counter and the rekey. Really.</span>

<span class="r">FATAL </span> Timestamps. Sequence numbers reset on restart. Anything
         derived from data. Anything derived from the plaintext.
         Anything that survives a VM snapshot.</pre>
</div>

<p>If you cannot make one of the first two work, you should not be using a nonce-based AEAD. Use AES-GCM-SIV — accept that it is an IETF RFC and not a NIST mode, document the deviation, and take the degradation of "an attacker learns two plaintexts were identical" over the annihilation of "an attacker forges everything."</p>

<h3>13.2 Data Limits and Rekeying</h3>

<p>Every key has a budget. Spend it and you leave the region where the security proof holds.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr><th>Mode (AES)</th><th>Hard per-message limit</th><th>Per-key limit</th><th>What to do</th></tr>
</thead>
<tbody>
  <tr>
    <td class="mono">CBC / CFB / OFB / CTR</td>
    <td>none specified</td>
    <td class="mono">$\ll 2^{64}$ blocks</td>
    <td>Rekey by $2^{59}$ blocks at the latest. NIST IR 8459 says "well before" the birthday bound and means it.</td>
  </tr>
  <tr>
    <td class="mono">GCM</td>
    <td class="mono">$2^{39}-256$ bits</td>
    <td class="mono">$2^{32}$ msgs (random IV)</td>
    <td>Prefer deterministic IVs. Count messages. Rekey.</td>
  </tr>
  <tr>
    <td class="mono">CCM</td>
    <td>set by $q$ (see §7)</td>
    <td>bounded by nonce space</td>
    <td>Choose $q$ so the nonce is 12–13 bytes and enforce the payload cap.</td>
  </tr>
  <tr>
    <td class="mono">XTS</td>
    <td class="mono">$2^{20}$ blocks per data unit</td>
    <td>volume-lifetime</td>
    <td>Rekeying a disk means rewriting the disk. Plan for it or accept it.</td>
  </tr>
  <tr>
    <td class="mono">CMAC</td>
    <td>none</td>
    <td class="mono">$\ll 2^{64}$ blocks</td>
    <td>Same birthday budget as the ciphers.</td>
  </tr>
</tbody>
</table>
</div>

<p>The cheapest way to make all of this go away is a key hierarchy. Keep one long-lived key-encrypting key. Derive short-lived data keys from it with a KDF, keyed by connection, by file, by epoch, by hour. Every derived key gets a fresh budget, and the blast radius of a nonce collision shrinks from "everything" to "one file."</p>

<h3>13.3 Key Commitment: Bind the Key to the Ciphertext</h3>

<p>Covered in §8.5, but it generalizes: <strong>no NIST-approved AEAD mode is key-committing.</strong> Not GCM, not CCM, not Ascon. If any of the following is true of your system, you must add commitment yourself:</p>

<ul class="ckp-hier">
  <li>Keys are derived from passwords, PINs, or other low-entropy secrets.</li>
  <li>The receiver tries multiple candidate keys and uses "it decrypted" as the selection signal.</li>
  <li>Ciphertexts serve as evidence — abuse reports, audit logs, moderation systems, escrow.</li>
  <li>The same ciphertext is delivered to parties holding different keys.</li>
</ul>

<h3>13.4 Never Release Unverified Plaintext</h3>

<p>All the AEAD modes here decrypt <em>before</em> they verify — CTR-based decryption produces plaintext immediately, and the tag check comes at the end. If your API streams plaintext to the caller as it is produced, you have handed the attacker a decryption oracle and undone the entire point of authentication.</p>

<p>This is a genuine engineering tension: streaming decryption of a 10 GB file <em>needs</em> to emit data before the end. The correct answer is not to relax the rule. It is to <strong>chunk the file into independently authenticated segments</strong>, each with its own tag, each bound by its AAD to its position and to the file identity — so that an attacker can neither reorder, truncate, drop, nor splice segments. Frame it properly and the last chunk is marked final. Do not invent this yourself; the pattern is well-trodden.</p>

<h3>13.5 Side Channels and Constant Time</h3>

<ul class="ckp-hier">
  <li><strong>Tag comparison must be constant-time.</strong> Not <code>memcmp</code>. An early return is a forgery oracle.</li>
  <li><strong>Table-driven AES leaks through the cache.</strong> If you don't have AES-NI, use a bitsliced implementation.</li>
  <li><strong>Table-driven GHASH leaks through the cache.</strong> Use the carry-less multiply instruction.</li>
  <li><strong>Error messages must not distinguish failures.</strong> "Bad padding," "bad MAC," "bad length" — one error, one code path, one timing. Ideally the same amount of work.</li>
  <li><strong>Compilers are hostile.</strong> A "constant-time" comparison written in C can be optimized into a branch. Use your platform's provided primitive, or verify the assembly.</li>
</ul>

<h3>13.6 Validation, Compliance, and Quantum</h3>

<p>An algorithm being "approved" is not the same as your <em>implementation</em> being approved. FIPS 140-3 validation is about the module: the boundary, the self-tests, the key zeroization, the RBG. CAVP test vectors will tell you your GCM produces the right tag; they will not tell you your nonce counter resets on reboot.</p>

<p>On quantum: Grover's algorithm gives at most a quadratic speedup against a symmetric key search, and realistic accounting of the required circuit depth makes even that optimistic. AES-128 remains defensible; AES-256 is the conservative choice and is what CNSA 2.0 mandates for national-security systems. <strong>The modes themselves are not the problem.</strong> Nobody needs a post-quantum replacement for CBC. Use AES-256 for anything with a long confidentiality horizon and stop worrying about this particular thing.</p>

<h3>13.7 The Hall of Fame</h3>

<p>Every one of these was a production system, designed by competent people, using a NIST-approved mode. Not one of them involved breaking AES.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr><th>Failure</th><th>Year</th><th>Mode</th><th>Root cause</th></tr>
</thead>
<tbody>
  <tr><td>Vaudenay padding oracle</td><td class="mono">2002</td><td class="mono">CBC</td><td class="no">Distinguishable padding errors</td></tr>
  <tr><td>ASP.NET (MS10-070)</td><td class="mono">2010</td><td class="mono">CBC</td><td class="no">Padding oracle via HTTP status</td></tr>
  <tr><td>BEAST</td><td class="mono">2011</td><td class="mono">CBC</td><td class="no">Predictable (chained) IV</td></tr>
  <tr><td>Lucky 13</td><td class="mono">2013</td><td class="mono">CBC</td><td class="no">MAC-then-Encrypt timing</td></tr>
  <tr><td>POODLE</td><td class="mono">2014</td><td class="mono">CBC</td><td class="no">Unchecked padding bytes</td></tr>
  <tr><td>Sweet32</td><td class="mono">2016</td><td class="mono">CBC (64-bit block)</td><td class="no">Birthday bound reached in hours</td></tr>
  <tr><td>Nonce-Disrespecting Adversaries</td><td class="mono">2016</td><td class="mono">GCM</td><td class="no">Repeated IVs on live HTTPS servers</td></tr>
  <tr><td>Efail</td><td class="mono">2018</td><td class="mono">CBC / CFB</td><td class="no">Malleability + an exfiltration channel</td></tr>
  <tr><td>Invisible Salamanders</td><td class="mono">2018</td><td class="mono">GCM</td><td class="no">No key commitment</td></tr>
  <tr><td>Zerologon</td><td class="mono">2020</td><td class="mono">CFB-8</td><td class="no">Hardcoded all-zero IV</td></tr>
  <tr><td>Partitioning oracles</td><td class="mono">2021</td><td class="mono">GCM</td><td class="no">No key commitment + password-derived key</td></tr>
</tbody>
</table>
</div>

<div class="ckp-pull">
  <p>Look down that column. IV, IV, IV, composition, padding, block size, nonce, malleability, commitment, IV, commitment. The cipher never appears. It never does.</p>
  <cite>— On where cryptographic systems actually break</cite>
</div>
</section>

<div class="ckp-sep">How to Choose</div>

<!-- ─── SECTION 14 ────────────────────────────────────────── -->
<section id="sec-decide">
<h2>14. The Decision Procedure</h2>

<p>Here is the whole document, compressed into the order you should actually think in.</p>

<div class="ckp-chain">

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">1</div>
    <div class="ckp-chain-content">
      <h4>Default to AEAD. Always.</h4>
      <p>The question is never "encryption or authenticated encryption." It is authenticated encryption, and then you argue about which one. Confidentiality without integrity is a bug you have not found yet.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">2</div>
    <div class="ckp-chain-content">
      <h4>Can you guarantee nonce uniqueness — structurally, not hopefully?</h4>
      <p>If yes: AES-GCM, 96-bit IV, 128-bit tag, context in the AAD. If no: fix the architecture until you can, or use AES-GCM-SIV and document the deviation from the NIST portfolio. Do not use GCM and hope.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">3</div>
    <div class="ckp-chain-content">
      <h4>What hardware are you on?</h4>
      <p>AES-NI and PCLMULQDQ (any modern CPU) → GCM. AES engine but no field multiplier (many microcontrollers, Wi-Fi and Bluetooth silicon) → CCM. Neither, and you're counting gates → Ascon.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">4</div>
    <div class="ckp-chain-content">
      <h4>Is there room for a nonce and a tag?</h4>
      <p>If yes, you have no excuse: use AEAD. If the ciphertext must be exactly as long as the plaintext, you are in the length-preserving corner — XTS for block storage, FF1 for legacy formatted fields — and you must accept that you have no integrity and say so out loud in the design document.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">5</div>
    <div class="ckp-chain-content">
      <h4>Are the keys low-entropy or attacker-selected?</h4>
      <p>Then add key commitment, because no NIST mode gives it to you. A commitment value in the AAD, or the zero-block padding fix. This is five lines of code and it closes an entire attack class.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">6</div>
    <div class="ckp-chain-content">
      <h4>Write down the per-key budget and the rekey trigger.</h4>
      <p>Messages, not bytes. If your design document does not say how many messages a key may protect and what happens when it runs out, your design is not finished.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">7</div>
    <div class="ckp-chain-content">
      <h4>Use a library. Do not compose primitives.</h4>
      <p>libsodium, BoringSSL, Tink, your platform's validated module. Every mode in this document has been implemented correctly by someone who spent years on it. Your job is to pick the right one and feed it correctly — not to build it.</p>
    </div>
  </div>

</div>

<h3>The Lookup Table</h3>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr><th>I need to…</th><th>Use</th><th>Because</th></tr>
</thead>
<tbody>
  <tr>
    <td>Encrypt network traffic</td>
    <td class="yes">AES-GCM (128-bit tag, 96-bit deterministic IV)</td>
    <td>One pass, hardware-accelerated, authenticated headers via AAD.</td>
  </tr>
  <tr>
    <td>Encrypt network traffic, but I cannot manage nonces</td>
    <td class="mid">AES-GCM-SIV (RFC 8452, not NIST)</td>
    <td>Nonce misuse degrades gracefully instead of catastrophically.</td>
  </tr>
  <tr>
    <td>Encrypt on a microcontroller with an AES peripheral</td>
    <td class="yes">AES-CCM</td>
    <td>One primitive, small code, no field arithmetic.</td>
  </tr>
  <tr>
    <td>Encrypt on a device with no AES at all</td>
    <td class="yes">Ascon-AEAD128</td>
    <td>Tiny, maskable, purpose-built for this.</td>
  </tr>
  <tr>
    <td>Encrypt a whole disk or volume</td>
    <td class="mid">XTS-AES</td>
    <td>Only length-preserving option. Add integrity underneath if you can.</td>
  </tr>
  <tr>
    <td>Encrypt a file, a blob, a database row</td>
    <td class="yes">AES-GCM, chunked, with position bound into the AAD</td>
    <td>You have room for a nonce and a tag. Use them.</td>
  </tr>
  <tr>
    <td>Protect a key at rest or in transit</td>
    <td class="yes">AES-GCM with context in the AAD; or AES-KW if mandated</td>
    <td>KW has no AAD, so it cannot bind the key to its metadata.</td>
  </tr>
  <tr>
    <td>Authenticate without encrypting</td>
    <td class="yes">HMAC-SHA-256, or CMAC on AES-only hardware</td>
    <td>Stateless. Unlike GMAC, no nonce to get wrong.</td>
  </tr>
  <tr>
    <td>Fit ciphertext into a fixed-format legacy field</td>
    <td class="mid">FF1 — or, better, tokenization</td>
    <td>FPE is a compliance tool with real cryptanalytic limits.</td>
  </tr>
  <tr>
    <td>Interoperate with a spec that mandates CBC</td>
    <td class="mid">AES-CBC + HMAC, Encrypt-then-MAC, random IV</td>
    <td>And schedule its removal.</td>
  </tr>
  <tr>
    <td>Anything, using ECB</td>
    <td class="no">No</td>
    <td>No.</td>
  </tr>
</tbody>
</table>
</div>
</section>

<div class="ckp-sep">The Next Portfolio</div>

<!-- ─── SECTION 15 ────────────────────────────────────────── -->
<section id="sec-future">
<h2>15. What Is Coming</h2>

<p>NIST knows the portfolio is showing its age. IR 8459 — the review board's own survey of the SP 800-38 series — is a remarkably candid document about the limitations of the modes it standardized. Three efforts are now in flight, and together they represent the biggest change to symmetric cryptography standards since AES itself.</p>

<h3>Rijndael-256: A Wider Block</h3>

<p>Rijndael always supported a 256-bit block; NIST simply never standardized it. It is now proposing to, precisely because $2^{64}$ blocks is no longer the comfortable distance it was in 2001 when the largest disk you could buy held 40 GB. A 256-bit block pushes the birthday bound to $2^{128}$ and makes the whole class of birthday-bound anxieties disappear. FIPS 197 is slated for revision to include it.</p>

<h3>wGCM: GCM for the Wide Block</h3>

<p>Announced 1 June 2026, with the comment period closing on 31 July 2026 — <em>as this is published, the window is still open.</em> wGCM is GCM over a 256-bit block cipher. NIST's proposal: a 192-bit IV, a 64-bit block counter, $2^{64}$ invocations per key, and tags of 128, 192, or 256 bits. It is asking the community whether "wide-GHASH" (a proper degree-256 polynomial) or "concat-GHASH" (two independent 128-bit GHASHes concatenated) is the right trade — the latter is faster, the former is more provably sound.</p>

<p>If you have opinions about GCM's limits — and after reading §8, you should — this is the moment to send them to NIST.</p>

<h3>The Cryptographic Accordion</h3>

<p>This is the interesting one. An accordion is a <em>variable-input-length tweakable strong pseudorandom permutation</em>: a cipher that operates on inputs of any length, built as a mode of a block cipher. From one accordion you can derive, by input encoding alone, an AEAD mode, a storage mode, and a deterministic key-wrap mode — replacing GCM, XTS, and KW with three configurations of a single, well-analyzed core.</p>

<p>NIST proposes three, all based on the HCTR2 construction:</p>

<ul class="ckp-hier">
  <li><strong>Acc128</strong> — over AES-128, for typical use at the birthday bound.</li>
  <li><strong>Acc256</strong> — over Rijndael-256, for typical use with a wide block.</li>
  <li><strong>BBBAcc</strong> — beyond-birthday-bound security over AES, for the highest-throughput applications.</li>
</ul>

<p>And here is the part that should make you pay attention: NIST's requirements for the accordion explicitly include <strong>nonce-misuse resistance</strong> and <strong>key commitment</strong> — the two gaps this document has been complaining about for fifteen pages. The wide tweakable PRP structure gives them almost for free: change one bit of a ciphertext and the entire plaintext becomes random, which means integrity can be checked with redundancy rather than a bolted-on MAC.</p>

<div class="ckp-callout key">
  <strong>What This Means For Your Roadmap</strong>
  <p>None of this is deployable today. But NIST has said, in writing, that once a suitable wide tweakable technique is approved it will <em>consider deprecating the SP 800-38A modes entirely</em>. If you are designing a system with a long life, build in algorithm agility now: negotiate your AEAD, version your ciphertext format, and make sure you can add a mode without a wire-format flag day. You will need it.</p>
</div>

<div class="ckp-pull">
  <p>The standards are finally catching up to what cryptographers have known since 2006: the mode should make the safe thing the easy thing. Until then, the discipline has to come from you.</p>
  <cite>— On the state of the portfolio, July 2026</cite>
</div>
</section>

<div class="ckp-sep">Quick Reference</div>

<!-- ─── MASTER TABLE + GLOSSARY ─────────────────────────────── -->
<section id="sec-glossary">
<h2>Quick Reference</h2>

<h3>Every Approved Mode, Side by Side</h3>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr>
    <th>Mode</th>
    <th>Spec</th>
    <th>Conf.</th>
    <th>Integ.</th>
    <th>AAD</th>
    <th>IV / Nonce rule</th>
    <th>Passes</th>
    <th>Parallel</th>
    <th>Use it for</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><span class="term">ECB</span></td><td class="mono">38A</td>
    <td class="no">no</td><td class="no">no</td><td class="no">—</td>
    <td class="no">none</td><td class="mono">1</td><td class="yes">yes</td>
    <td class="no">Nothing.</td>
  </tr>
  <tr>
    <td><span class="term">CBC</span></td><td class="mono">38A</td>
    <td class="mid">yes*</td><td class="no">no</td><td class="no">—</td>
    <td class="mid">unpredictable</td><td class="mono">1</td><td class="mid">dec only</td>
    <td class="mid">Legacy interop, under a MAC.</td>
  </tr>
  <tr>
    <td><span class="term">CFB</span></td><td class="mono">38A</td>
    <td class="mid">yes*</td><td class="no">no</td><td class="no">—</td>
    <td class="mid">unpredictable</td><td class="mono">1</td><td class="mid">dec only</td>
    <td class="no">Nothing new.</td>
  </tr>
  <tr>
    <td><span class="term">OFB</span></td><td class="mono">38A</td>
    <td class="mid">yes*</td><td class="no">no</td><td class="no">—</td>
    <td class="mid">unique nonce</td><td class="mono">1</td><td class="no">no</td>
    <td class="no">Nothing new.</td>
  </tr>
  <tr>
    <td><span class="term">CTR</span></td><td class="mono">38A</td>
    <td class="mid">yes*</td><td class="no">no</td><td class="no">—</td>
    <td class="mid">unique ctr block</td><td class="mono">1</td><td class="yes">yes</td>
    <td class="mid">Keystream inside an AEAD.</td>
  </tr>
  <tr>
    <td><span class="term">CMAC</span></td><td class="mono">38B</td>
    <td class="no">—</td><td class="yes">yes</td><td class="no">—</td>
    <td class="yes">none needed</td><td class="mono">1</td><td class="no">no</td>
    <td class="yes">MAC on AES-only hardware.</td>
  </tr>
  <tr>
    <td><span class="term">CCM</span></td><td class="mono">38C</td>
    <td class="yes">yes</td><td class="yes">yes</td><td class="yes">yes</td>
    <td class="mid">unique nonce (7–13 B)</td><td class="mono">2</td><td class="mid">CTR half</td>
    <td class="yes">Constrained AEAD; Wi-Fi, BLE.</td>
  </tr>
  <tr>
    <td><span class="term">GCM</span></td><td class="mono">38D</td>
    <td class="yes">yes</td><td class="yes">yes</td><td class="yes">yes</td>
    <td class="mid">unique nonce (96-bit)</td><td class="mono">1</td><td class="yes">yes</td>
    <td class="yes">Default AEAD on real CPUs.</td>
  </tr>
  <tr>
    <td><span class="term">GMAC</span></td><td class="mono">38D</td>
    <td class="no">—</td><td class="yes">yes</td><td class="yes">yes</td>
    <td class="mid">unique nonce</td><td class="mono">1</td><td class="yes">yes</td>
    <td class="mid">Only if already running GCM.</td>
  </tr>
  <tr>
    <td><span class="term">XTS</span></td><td class="mono">38E</td>
    <td class="mid">yes†</td><td class="no">no</td><td class="no">—</td>
    <td class="mid">tweak = unit number</td><td class="mono">1</td><td class="yes">yes</td>
    <td class="mid">Block storage only.</td>
  </tr>
  <tr>
    <td><span class="term">KW / KWP</span></td><td class="mono">38F</td>
    <td class="yes">yes</td><td class="yes">yes</td><td class="no">no</td>
    <td class="yes">none needed</td><td class="mono">6</td><td class="no">no</td>
    <td class="mid">Key wrapping, when mandated.</td>
  </tr>
  <tr>
    <td><span class="term">FF1</span></td><td class="mono">38G</td>
    <td class="mid">yes‡</td><td class="no">no</td><td class="no">tweak</td>
    <td class="mid">tweak, not a nonce</td><td class="mono">10 rnd</td><td class="no">no</td>
    <td class="mid">Legacy fixed-format fields.</td>
  </tr>
  <tr>
    <td><span class="term">Ascon-AEAD128</span></td><td class="mono">800-232</td>
    <td class="yes">yes</td><td class="yes">yes</td><td class="yes">yes</td>
    <td class="mid">unique nonce (128-bit)</td><td class="mono">1</td><td class="no">no</td>
    <td class="yes">Constrained devices, no AES HW.</td>
  </tr>
</tbody>
</table>
</div>

<p style="font-size:0.82rem; color:var(--text-muted); font-family:var(--font-mono); line-height:1.7;">
* IND-CPA only, and only if the IV/counter rule is honored. † Confidentiality at rest only; leaks equality per (unit, offset). ‡ Only for domains of at least $10^6$; deterministic per (key, tweak).
</p>

<h3>Glossary</h3>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr><th>Term</th><th>Definition</th></tr>
</thead>
<tbody>
  <tr>
    <td><span class="term">AEAD</span></td>
    <td>Authenticated Encryption with Associated Data. Confidentiality for the plaintext, integrity for the plaintext <em>and</em> the associated data, in one primitive.</td>
  </tr>
  <tr>
    <td><span class="term">AAD</span></td>
    <td>Associated data: authenticated but not encrypted. Use it to bind a ciphertext to its context — headers, sequence numbers, key IDs, versions.</td>
  </tr>
  <tr>
    <td><span class="term">Birthday bound</span></td>
    <td>$2^{n/2}$ blocks for an $n$-bit block cipher. Where the security proof stops. $2^{32}$ blocks (32 GB) for 3DES; $2^{64}$ for AES.</td>
  </tr>
  <tr>
    <td><span class="term">Committing AEAD</span></td>
    <td>A ciphertext decrypts successfully under at most one key. No NIST mode has this property.</td>
  </tr>
  <tr>
    <td><span class="term">DAE</span></td>
    <td>Deterministic authenticated encryption. No nonce required, because the plaintext (a key) is already random. AES-KW is a DAE.</td>
  </tr>
  <tr>
    <td><span class="term">Forbidden attack</span></td>
    <td>GCM nonce reuse. XOR two tags to cancel the mask, solve the resulting polynomial for the hash key $H$, forge at will.</td>
  </tr>
  <tr>
    <td><span class="term">GHASH</span></td>
    <td>GCM's universal hash: polynomial evaluation in $\mathrm{GF}(2^{128})$. Fast, and worthless the moment its key leaks.</td>
  </tr>
  <tr>
    <td><span class="term">IND-CPA</span></td>
    <td>Indistinguishability under chosen-plaintext attack. The bar the SP 800-38A modes clear. Says nothing about an active attacker.</td>
  </tr>
  <tr>
    <td><span class="term">INT-CTXT</span></td>
    <td>Integrity of ciphertexts: the attacker cannot produce any ciphertext the receiver will accept. IND-CPA + INT-CTXT gives IND-CCA.</td>
  </tr>
  <tr>
    <td><span class="term">IV</span></td>
    <td>Initialization vector. In CBC and CFB it must be <em>unpredictable</em>; in OFB, CTR, GCM and CCM it must be <em>unique</em>. These are different requirements and confusing them is how BEAST happened.</td>
  </tr>
  <tr>
    <td><span class="term">Malleability</span></td>
    <td>The attacker can transform a ciphertext into another valid ciphertext whose plaintext relates predictably to the original. Every confidentiality-only mode is malleable.</td>
  </tr>
  <tr>
    <td><span class="term">MRAE</span></td>
    <td>Misuse-resistant AE. A repeated nonce leaks only plaintext equality, not the key. SIV and AES-GCM-SIV; nothing in the NIST portfolio.</td>
  </tr>
  <tr>
    <td><span class="term">Nonce</span></td>
    <td>Number used once. Not secret, not random — <em>unique</em>. Under one key, forever, across every machine that holds that key.</td>
  </tr>
  <tr>
    <td><span class="term">Padding oracle</span></td>
    <td>Any observable difference — error, timing, reset — that reveals whether decryption produced valid padding. Decrypts arbitrary CBC ciphertext at ~128 queries per byte.</td>
  </tr>
  <tr>
    <td><span class="term">RUP</span></td>
    <td>Release of unverified plaintext. Emitting decrypted bytes before the tag is checked. It is a decryption oracle with good intentions.</td>
  </tr>
  <tr>
    <td><span class="term">Tweak</span></td>
    <td>A non-secret, changeable input to a cipher that selects a different permutation. The sector number in XTS; the record context in FF1.</td>
  </tr>
  <tr>
    <td><span class="term">Two-time pad</span></td>
    <td>The same keystream used twice. $C_1 \oplus C_2 = P_1 \oplus P_2$. The key cancels and the plaintexts are recoverable. Unrecoverable as an incident.</td>
  </tr>
</tbody>
</table>
</div>
</section>

<!-- ─── REFERENCES ─────────────────────────────────────────── -->
<div class="ckp-refs" id="references">
<h2>References</h2>

<p id="ref-38A"><span class="ref-num">[38A]</span> Dworkin, M.: Recommendation for Block Cipher Modes of Operation: Methods and Techniques. NIST SP 800-38A (2001). <a href="https://doi.org/10.6028/NIST.SP.800-38A">doi:10.6028/NIST.SP.800-38A</a>. Addendum: Three Variants of Ciphertext Stealing for CBC Mode (2010).</p>

<p id="ref-38B"><span class="ref-num">[38B]</span> Dworkin, M.: The CMAC Mode for Authentication. NIST SP 800-38B (2005, updated 2016). <a href="https://doi.org/10.6028/NIST.SP.800-38B">doi:10.6028/NIST.SP.800-38B</a></p>

<p id="ref-38C"><span class="ref-num">[38C]</span> Dworkin, M.: The CCM Mode for Authentication and Confidentiality. NIST SP 800-38C (2004, updated 2007). <a href="https://doi.org/10.6028/NIST.SP.800-38C">doi:10.6028/NIST.SP.800-38C</a></p>

<p id="ref-38D"><span class="ref-num">[38D]</span> Dworkin, M.: Galois/Counter Mode (GCM) and GMAC. NIST SP 800-38D (2007). <a href="https://doi.org/10.6028/NIST.SP.800-38D">doi:10.6028/NIST.SP.800-38D</a></p>

<p id="ref-38Dr1"><span class="ref-num">[38Dr1]</span> NIST: Second Pre-Draft Call for Comments — GCM and GMAC Block Cipher Modes of Operation. SP 800-38D Rev. 1 (1 June 2026; comments due 31 July 2026). Proposes removal of sub-96-bit tags and the new wide variant <em>wGCM</em> over a 256-bit block. <a href="https://csrc.nist.gov/pubs/sp/800/38/d/r1/2prd">csrc.nist.gov/pubs/sp/800/38/d/r1/2prd</a></p>

<p id="ref-38E"><span class="ref-num">[38E]</span> Dworkin, M.: The XTS-AES Mode for Confidentiality on Storage Devices. NIST SP 800-38E (2010). <a href="https://doi.org/10.6028/NIST.SP.800-38E">doi:10.6028/NIST.SP.800-38E</a>. Revision decided, February 2024.</p>

<p id="ref-38F"><span class="ref-num">[38F]</span> Dworkin, M.: Methods for Key Wrapping. NIST SP 800-38F (2012). <a href="https://doi.org/10.6028/NIST.SP.800-38F">doi:10.6028/NIST.SP.800-38F</a></p>

<p id="ref-38Gr1"><span class="ref-num">[38Gr1]</span> Dworkin, M., Mouha, N.: Methods for Format-Preserving Encryption. NIST SP 800-38G Rev. 1, Second Public Draft (February 2025). Removes FF3; requires a minimum domain size of $10^6$ for FF1; forbids floating-point arithmetic. <a href="https://doi.org/10.6028/NIST.SP.800-38Gr1.2pd">doi:10.6028/NIST.SP.800-38Gr1.2pd</a></p>

<p id="ref-IR8459"><span class="ref-num">[IR8459]</span> Mouha, N., Dworkin, M.: Report on the Block Cipher Modes of Operation in the NIST SP 800-38 Series. NIST IR 8459 (September 2024). The review board's own catalogue of the portfolio's limitations. <a href="https://doi.org/10.6028/NIST.IR.8459">doi:10.6028/NIST.IR.8459</a></p>

<p id="ref-Rev38A"><span class="ref-num">[Rev38A]</span> NIST: Decision to Revise NIST SP 800-38A (28 April 2023). Restricts ECB approval; tightens IV and counter-block requirements; states NIST "will consider deprecating the modes in SP 800-38A" if a wide tweakable technique is approved. <a href="https://csrc.nist.gov/News/2023/decision-to-revise-nist-sp-800-38a">csrc.nist.gov/News/2023/decision-to-revise-nist-sp-800-38a</a></p>

<p id="ref-Ascon"><span class="ref-num">[Ascon]</span> Kang, J., Kelsey, J., et al.: Ascon-Based Lightweight Cryptography Standards for Constrained Devices. NIST SP 800-232 (August 2025). <a href="https://doi.org/10.6028/NIST.SP.800-232">doi:10.6028/NIST.SP.800-232</a></p>

<p id="ref-Acc"><span class="ref-num">[Acc]</span> NIST: Launch of the Development of Cryptographic Accordions. Pre-draft call for comments, SP 800-197A (June 2025). Proposes Acc128, Acc256 and BBBAcc, all HCTR2-based, with misuse resistance and key commitment among the requirements. <a href="https://csrc.nist.gov/pubs/sp/800/197/a/iprd">csrc.nist.gov/pubs/sp/800/197/a/iprd</a>. See also NIST IR 8537, the 2024 Accordion Workshop report.</p>

<p id="ref-FIPS197"><span class="ref-num">[FIPS197]</span> NIST: Advanced Encryption Standard (AES). FIPS 197 (2001, updated May 2023). <a href="https://doi.org/10.6028/NIST.FIPS.197-upd1">doi:10.6028/NIST.FIPS.197-upd1</a>. A revision to add Rijndael-256 is planned.</p>

<p id="ref-131A"><span class="ref-num">[131A]</span> Barker, E., Roginsky, A.: Transitioning the Use of Cryptographic Algorithms and Key Lengths. NIST SP 800-131A Rev. 2 (2019). Three-key TDEA encryption disallowed after 2023. <a href="https://doi.org/10.6028/NIST.SP.800-131Ar2">doi:10.6028/NIST.SP.800-131Ar2</a></p>

<p id="ref-BN00"><span class="ref-num">[BN00]</span> Bellare, M., Namprempre, C.: Authenticated Encryption: Relations among Notions and Analysis of the Generic Composition Paradigm. ASIACRYPT 2000. The paper that settled Encrypt-then-MAC.</p>

<p id="ref-RS06"><span class="ref-num">[RS06]</span> Rogaway, P., Shrimpton, T.: Deterministic Authenticated-Encryption: A Provable-Security Treatment of the Key-Wrap Problem. EUROCRYPT 2006. Formalizes key wrapping and introduces SIV. <a href="https://eprint.iacr.org/2006/221">eprint 2006/221</a></p>

<p id="ref-Vaudenay"><span class="ref-num">[Vaudenay]</span> Vaudenay, S.: Security Flaws Induced by CBC Padding — Applications to SSL, IPSEC, WTLS… EUROCRYPT 2002. The original padding-oracle attack.</p>

<p id="ref-BEAST"><span class="ref-num">[BEAST]</span> Duong, T., Rizzo, J.: Practical chosen-plaintext attack against TLS 1.0 CBC (2011). CVE-2011-3389. <a href="https://nvd.nist.gov/vuln/detail/CVE-2011-3389">nvd.nist.gov/vuln/detail/CVE-2011-3389</a></p>

<p id="ref-Lucky13"><span class="ref-num">[Lucky13]</span> AlFardan, N., Paterson, K.: Lucky Thirteen — Breaking the TLS and DTLS Record Protocols. IEEE S&amp;P 2013. CVE-2013-0169.</p>

<p id="ref-POODLE"><span class="ref-num">[POODLE]</span> Möller, B., Duong, T., Kotowicz, K.: This POODLE Bites — Exploiting the SSL 3.0 Fallback (2014). CVE-2014-3566.</p>

<p id="ref-Sweet32"><span class="ref-num">[Sweet32]</span> Bhargavan, K., Leurent, G.: On the Practical (In-)Security of 64-bit Block Ciphers — Collision Attacks on HTTP over TLS and OpenVPN. ACM CCS 2016. CVE-2016-2183. <a href="https://sweet32.info/">sweet32.info</a></p>

<p id="ref-Efail"><span class="ref-num">[Efail]</span> Poddebniak, D., et al.: Efail — Breaking S/MIME and OpenPGP Email Encryption using Exfiltration Channels. USENIX Security 2018. <a href="https://efail.de/">efail.de</a></p>

<p id="ref-Zerologon"><span class="ref-num">[Zerologon]</span> Tervoort, T. (Secura): Zerologon — Instantly Becoming Domain Admin by Subverting Netlogon Cryptography (2020). AES-CFB8 with an all-zero IV. CVE-2020-1472. <a href="https://nvd.nist.gov/vuln/detail/CVE-2020-1472">nvd.nist.gov/vuln/detail/CVE-2020-1472</a></p>

<p id="ref-Nonce"><span class="ref-num">[Nonce]</span> Böck, H., Zauner, A., Devlin, S., Somorovsky, J., Jovanovic, P.: Nonce-Disrespecting Adversaries — Practical Forgery Attacks on GCM in TLS. USENIX WOOT 2016. Found live HTTPS servers repeating GCM nonces.</p>

<p id="ref-Salamanders"><span class="ref-num">[Salamanders]</span> Dodis, Y., Grubbs, P., Ristenpart, T., Woodage, J.: Fast Message Franking — From Invisible Salamanders to Encryptment. CRYPTO 2018. Defeated Facebook Messenger's abuse reporting via GCM's lack of key commitment.</p>

<p id="ref-Partition"><span class="ref-num">[Partition]</span> Len, J., Grubbs, P., Ristenpart, T.: Partitioning Oracle Attacks. USENIX Security 2021. Password recovery against Shadowsocks using non-committing AEAD.</p>

<p id="ref-Ferguson"><span class="ref-num">[Ferguson]</span> Ferguson, N.: Authentication Weaknesses in GCM. Public comment to NIST (2005). The reason short GCM tags carry extra restrictions — and the reason they are now being removed.</p>

<p id="ref-Joux"><span class="ref-num">[Joux]</span> Joux, A.: Authentication Failures in NIST Version of GCM. Public comment to NIST (2006). The forbidden attack.</p>

<p id="ref-Beyne"><span class="ref-num">[Beyne]</span> Beyne, T.: Linear Cryptanalysis of FF3-1 and FEA. CRYPTO 2021. <a href="https://doi.org/10.1007/978-3-030-84242-0_3">doi:10.1007/978-3-030-84242-0_3</a>. The result that removed FF3 from the standard.</p>

<p id="ref-DV17"><span class="ref-num">[DV17]</span> Durak, F.B., Vaudenay, S.: Breaking the FF3 Format-Preserving Encryption Standard over Small Domains. CRYPTO 2017. <a href="https://doi.org/10.1007/978-3-319-63715-0_23">doi:10.1007/978-3-319-63715-0_23</a></p>

<p id="ref-HTT18"><span class="ref-num">[HTT18]</span> Hoang, V.T., Tessaro, S., Trieu, N.: The Curse of Small Domains — New Attacks on Format-Preserving Encryption. CRYPTO 2018. <a href="https://doi.org/10.1007/978-3-319-96884-1_8">doi:10.1007/978-3-319-96884-1_8</a></p>

<p id="ref-BHT16"><span class="ref-num">[BHT16]</span> Bellare, M., Hoang, V.T., Tessaro, S.: Message-Recovery Attacks on Feistel-Based Format-Preserving Encryption. ACM CCS 2016. <a href="https://doi.org/10.1145/2976749.2978390">doi:10.1145/2976749.2978390</a></p>

<p id="ref-GCMSIV"><span class="ref-num">[GCMSIV]</span> Gueron, S., Langley, A., Lindell, Y.: AES-GCM-SIV — Nonce Misuse-Resistant Authenticated Encryption. RFC 8452 (2019). Not NIST-approved. Use it anyway when you cannot guarantee nonces. <a href="https://www.rfc-editor.org/rfc/rfc8452">rfc-editor.org/rfc/rfc8452</a></p>

<p id="ref-TLS13"><span class="ref-num">[TLS13]</span> Rescorla, E.: The Transport Layer Security (TLS) Protocol Version 1.3. RFC 8446 (2018). AEAD only; the GCM IV construction the 38D revision will bless. <a href="https://www.rfc-editor.org/rfc/rfc8446">rfc-editor.org/rfc/rfc8446</a></p>
</div>

</div><!-- end .ckp-body -->

<!-- ─── Sidebar TOC ─────────────────────────────────────────── -->
<aside class="ckp-sidebar">
  <div class="ckp-toc-label">Contents</div>
  <ul class="ckp-toc-list" id="ckp-toc">
    <li data-section="abstract"><a href="#abstract">Abstract</a></li>
    <li data-section="sec-basics"><a href="#sec-basics">1. What a Mode Actually Is</a></li>
    <li data-section="sec-goals"><a href="#sec-goals">2. The Goals You Are Buying</a></li>
    <li class="toc-sub" data-section="sec-goals"><a href="#sec-goals">The Birthday Bound</a></li>
    <li data-section="sec-map"><a href="#sec-map">3. The Standards Map, 2026</a></li>
    <li data-section="sec-38a"><a href="#sec-38a">4. Confidentiality-Only Modes</a></li>
    <li class="toc-sub" data-section="sec-38a"><a href="#sec-38a">ECB · CBC · CFB · OFB · CTR</a></li>
    <li data-section="sec-cmac"><a href="#sec-cmac">5. CMAC</a></li>
    <li data-section="sec-composition"><a href="#sec-composition">6. Generic Composition</a></li>
    <li data-section="sec-ccm"><a href="#sec-ccm">7. CCM</a></li>
    <li data-section="sec-gcm"><a href="#sec-gcm">8. GCM and GMAC</a></li>
    <li class="toc-sub" data-section="sec-gcm"><a href="#sec-gcm">The Forbidden Attack</a></li>
    <li class="toc-sub" data-section="sec-gcm"><a href="#sec-gcm">Limits &amp; Key Commitment</a></li>
    <li data-section="sec-ascon"><a href="#sec-ascon">9. Ascon</a></li>
    <li data-section="sec-xts"><a href="#sec-xts">10. XTS-AES</a></li>
    <li data-section="sec-kw"><a href="#sec-kw">11. Key Wrapping</a></li>
    <li data-section="sec-fpe"><a href="#sec-fpe">12. Format-Preserving (FF1)</a></li>
    <li data-section="sec-eng"><a href="#sec-eng">13. The Engineering</a></li>
    <li class="toc-sub" data-section="sec-eng"><a href="#sec-eng">Nonces · Limits · RUP</a></li>
    <li data-section="sec-decide"><a href="#sec-decide">14. How to Choose</a></li>
    <li data-section="sec-future"><a href="#sec-future">15. What Is Coming</a></li>
    <li data-section="sec-glossary"><a href="#sec-glossary">Quick Reference</a></li>
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
  var sections = ['abstract','sec-basics','sec-goals','sec-map','sec-38a','sec-cmac','sec-composition','sec-ccm','sec-gcm','sec-ascon','sec-xts','sec-kw','sec-fpe','sec-eng','sec-decide','sec-future','sec-glossary','references'];
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
