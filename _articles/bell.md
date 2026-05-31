---
layout: post
title: "Understanding the Bell Inequality"
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
</style>

<div id="ckp-progress"></div>

<article class="ckp-article">

<!-- ═══════════════════ HERO ═══════════════════════════════════ -->
<div class="ckp-hero">
  <div class="ckp-kicker">Quantum Foundations · Bell Inequality · Certified Randomness</div>
  <h1>Understanding the <em>Bell Inequality</em></h1>
  <p class="ckp-deck">A self-contained guide to Bell's theorem, quantum entanglement, and device-independent randomness — from the CHSH algebraic bound to the 2026 ETH Zürich demonstration of certified perfect randomness.</p>
  <div class="ckp-meta">
    <span>Quantum Foundations Series</span>
    <span class="dot"></span>
    <span>University Whitepaper · 2026</span>
    <span class="dot"></span>
    <span>~20 min read</span>
    <span class="dot"></span>
    <span><a href="https://ethz.ch/en/news-and-events/eth-news/news/2026/05/perfect-randomness-realised-for-the-first-time.html" target="_blank">ETH Zürich News ↗</a></span>
  </div>
</div>

<!-- Keywords -->
<div class="ckp-keywords">
  <span class="ckp-kw">Bell Inequality</span>
  <span class="ckp-kw">CHSH Bound</span>
  <span class="ckp-kw">Quantum Entanglement</span>
  <span class="ckp-kw">Singlet State</span>
  <span class="ckp-kw">QRNG</span>
  <span class="ckp-kw">Randomness Amplification</span>
  <span class="ckp-kw">Device-Independent Cryptography</span>
</div>

<!-- Mobile TOC -->
<div class="ckp-mobile-toc" id="ckp-mob-toc-toggle">
  <span>Contents</span><span>▾</span>
</div>
<div class="ckp-mobile-toc-list" id="ckp-mob-toc-list">
  <a href="#abstract">Abstract</a>
  <a href="#sec-bell">1. What Bell's Inequality Is About</a>
  <a href="#sec-classical">2. Why the Classical Limit Is 2</a>
  <a href="#sec-qm">3. Why Quantum Mechanics Can Exceed 2</a>
  <a href="#sec-entanglement">4. What Entanglement Is Doing</a>
  <a href="#sec-singlet">5. Singlet State vs. Joint State</a>
  <a href="#sec-matter">6. Why Bell Violation Matters</a>
  <a href="#sec-qrng">7. Bell Inequality and QRNGs</a>
  <a href="#sec-chain">8. The Main Picture in One Chain</a>
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
  <p>This paper is a self-contained guide to Bell's theorem, quantum entanglement, and device-independent randomness, written for university students with a basic background in linear algebra and probability. We derive the CHSH bound algebraically, explain why quantum mechanics violates it, give a detailed treatment of entanglement, and discuss the landmark 2026 ETH Zürich demonstration of certified perfect randomness as a concrete application.</p>
</div>

<!-- STATS BAR -->
<div class="ckp-stat-row">
  <div class="ckp-stat"><span class="stat-num">2</span><span class="stat-label">Classical CHSH bound $|S| \leq 2$</span></div>
  <div class="ckp-stat"><span class="stat-num">2√2</span><span class="stat-label">Tsirelson quantum maximum ≈ 2.828</span></div>
  <div class="ckp-stat"><span class="stat-num">2026</span><span class="stat-label">ETH Zürich certified randomness</span></div>
  <div class="ckp-stat"><span class="stat-num">45M</span><span class="stat-label">Certified-random bits extracted</span></div>
</div>

<!-- ─── SECTION 1 ─────────────────────────────────────────── -->
<section id="sec-bell">
<h2>1. What Bell's Inequality Is About</h2>

<p class="drop-cap">Bell's inequality is a mathematical test for whether nature can be explained by <em>local realism</em> — a classical picture of reality built on two interlocking assumptions.</p>

<h3>The Two Pillars of Local Realism</h3>

<div class="ckp-callout">
  <strong>Realism</strong>
  <p>Measurement outcomes are already determined by hidden properties of the particles, even before any measurement is made. Each particle carries a secret "instruction card" written at the moment the pair was created.</p>
</div>

<div class="ckp-callout" style="border-left-color: var(--green);">
  <strong style="color: var(--green);">Locality</strong>
  <p>What happens at one location cannot instantly affect a distant location. No influence can travel faster than light. If Alice makes a measurement in her lab, it cannot change anything in Bob's lab across the room — let alone across the galaxy.</p>
</div>

<p>Bell showed that if both assumptions hold simultaneously, certain experimental correlations must obey a mathematical bound. In the most widely used form, the <strong>CHSH inequality</strong> [<a href="#ref-CHSH1969">CHSH1969</a>] (named after Clauser, Horne, Shimony, and Holt), that bound is:</p>

<div class="ckp-eq">
  <span class="eq-label">CHSH Bound — Eq. (1)</span>
  $$|S| \leq 2 \tag{1}$$
</div>

<p>where the CHSH correlator $S$ is defined as:</p>

<div class="ckp-eq">
  <span class="eq-label">CHSH Correlator — Eq. (2)</span>
  $$S = E(a,b) + E(a,b') + E(a',b) - E(a',b') \tag{2}$$
</div>

<p>Each $E(x,y)$ is a <em>correlation coefficient</em> between outcomes measured on the two particles when Alice uses detector setting $x$ and Bob uses detector setting $y$. Outcomes are labelled $+1$ or $-1$ (e.g. spin-up or spin-down). A correlation of $+1$ means the two detectors always agree; $-1$ means they always disagree; $0$ means no correlation at all.</p>

<h3>A Primer: Measurements, Spin, and Bases</h3>

<div class="ckp-callout">
  <strong>Key Concept: What Is a Measurement in Quantum Mechanics?</strong>
  <p>In classical physics, measuring a property simply reads out a pre-existing value. A ball's velocity is what it is, regardless of how you look at it.</p>
  <p>In quantum mechanics, measurement is an <em>active, irreversible</em> process. Before measurement, a quantum particle such as a photon or electron can be in a <em>superposition</em> of several possible outcomes. The act of measurement forces the system into one definite result — chosen at random with probabilities prescribed by the quantum state.</p>
  <p>Photon polarisation and electron spin are the most common properties used in Bell experiments. Both are two-valued: a measurement along any chosen axis yields either $+1$ or $-1$, never anything in between.</p>
  <p>The direction along which you choose to measure is called the <em>measurement basis</em>. If you rotate your detector, you are choosing a different basis. Crucially, a particle that was spin-up along the vertical axis has a well-defined probability of being measured spin-up along a tilted axis — and that probability depends on the <em>angle</em> between the two axes. No pre-written value can account for all possible angles simultaneously, as Bell's theorem proves.</p>
</div>

<p>For photons, polarisation is the relevant property. A photon can be horizontally polarised, vertically polarised, or — in a quantum superposition — both at once. A polariser (the detector) is oriented at some angle $\theta$; it transmits the photon with probability $\cos^2\!\theta$ relative to the photon's polarisation direction, and blocks it otherwise. The outcome is binary: pass ($+1$) or block ($-1$).</p>

<p>If you choose the wrong basis — for example, trying to detect a diagonally polarised photon with a horizontal/vertical polariser — the outcome is completely random with equal probability. The information about the original diagonal polarisation is irretrievably lost. This is not a deficiency in your equipment; it is a fundamental feature of quantum mechanics.</p>
</section>

<div class="ckp-sep">Classical Bound</div>

<!-- ─── SECTION 2 ─────────────────────────────────────────── -->
<section id="sec-classical">
<h2>2. Why the Classical Limit Is 2</h2>

<p>The bound $|S| \leq 2$ follows from a simple algebraic argument. Assume each particle carries predetermined answers for all four possible measurement settings: $a$, $a'$, $b$, $b'$. Call the hidden outcomes $A, A' \in \{-1,+1\}$ for Alice's settings and $B, B' \in \{-1,+1\}$ for Bob's settings.</p>

<h3>The Algebraic Core</h3>

<p>Consider the quantity:</p>

<div class="ckp-eq">
  <span class="eq-label">Single-Trial Quantity — Eq. (3)</span>
  $$S^{*} = AB + AB' + A'B - A'B' \tag{3}$$
</div>

<p>Factoring gives:</p>

<div class="ckp-eq">
  <span class="eq-label">Factored Form — Eq. (4)</span>
  $$S^{*} = A(B + B') + A'(B - B') \tag{4}$$
</div>

<p>Since $B$ and $B'$ each take values in $\{-1,+1\}$, exactly one of two cases holds:</p>

<ul class="ckp-hier">
  <li><strong>Case 1: $B = B'$.</strong> Then $B + B' = \pm 2$ and $B - B' = 0$, giving $S^{*} = \pm 2A$ and $|S^{*}| = 2$.</li>
  <li><strong>Case 2: $B = -B'$.</strong> Then $B + B' = 0$ and $B - B' = \pm 2$, giving $S^{*} = \pm 2A'$ and $|S^{*}| = 2$.</li>
</ul>

<p>In every possible case $|S^{*}| = 2$. Since the measured correlation $E(a,b)$ is the average of $AB$ over many trials, and the average of a quantity bounded by $2$ in magnitude is also bounded by $2$, we obtain $|S| \leq 2$ for any local hidden-variable theory.</p>

<div class="ckp-callout warn">
  <strong>Why Randomness Cannot Save Local Realism</strong>
  <p>One might think: what if the hidden variables are random? Does that create a loophole? No. The argument above holds for <em>every single trial</em>, whatever values the hidden variables take. Averaging over any distribution of hidden-variable values preserves $|S| \leq 2$. The bound is a structural consequence of pre-assignment plus locality, not an artefact of any particular distribution.</p>
</div>

<p>The limit of $2$ is therefore not about noise, imprecision, or incomplete knowledge. It is a ceiling written into any theory where results are both pre-assigned on the particle and locally independent of the distant detector's orientation.</p>
</section>

<div class="ckp-sep">Quantum Violation</div>

<!-- ─── SECTION 3 ─────────────────────────────────────────── -->
<section id="sec-qm">
<h2>3. Why Quantum Mechanics Can Exceed 2</h2>

<p>Quantum mechanics does not treat measurement outcomes as pre-written answers read off a hidden card. For entangled states, the correlation between results at two distant detectors is determined by the <em>relative angle</em> between those detectors — a continuous, geometric quantity that no fixed hidden card can reproduce for all angles at once.</p>

<h3>The Quantum Correlation Formula</h3>

<p>For the spin singlet state (see Section 5), the correlation between Alice's and Bob's outcomes is:</p>

<div class="ckp-eq">
  <span class="eq-label">Quantum Correlation — Eq. (5)</span>
  $$E(a,b) = -\cos\theta_{ab} \tag{5}$$
</div>

<p>where $\theta_{ab}$ is the angle between Alice's detector direction $a$ and Bob's detector direction $b$. This smooth cosine dependence is the fingerprint of quantum entanglement.</p>

<h3>The Optimal CHSH Violation</h3>

<p>Choosing the four detector angles $a = 0°$, $b = 45°$, $a' = 90°$, $b' = 135°$ (equivalently $a = 0°$, $a' = 45°$, $b = 22.5°$, $b' = 67.5°$), quantum mechanics gives:</p>

<div class="ckp-eq">
  <span class="eq-label">Tsirelson Bound — Eq. (6)</span>
  $$|S| = 2\sqrt{2} \approx 2.828 \tag{6}$$
</div>

<p>This is the <strong>Tsirelson bound</strong> — the maximum Bell violation quantum mechanics allows. It exceeds the classical limit of $2$ by a factor of $\sqrt{2}$.</p>

<div class="ckp-callout">
  <strong>Why Can't Local Realism Match the Cosine?</strong>
  <p>Imagine writing all four answers $A$, $A'$, $B$, $B'$ on a card before any measurement. The algebraic argument in Section 2 shows that any such card must give $|S^{*}| = 2$ exactly, not $2\sqrt{2}$.</p>
  <p>The cosine curve $-\cos\theta$ is not piecewise constant — it bends smoothly. A hidden-variable card must commit to discrete $\pm 1$ values for each angle. No matter how cleverly you arrange the $\pm 1$ values on the card, you cannot reproduce the smooth cosine correlation for <em>all</em> possible angle choices simultaneously. There is a fundamental mismatch between the continuous geometry of quantum correlations and the discrete combinatorics of pre-assigned outcomes.</p>
  <p>Experiments — most notably the loophole-free Bell tests of 2015 [<a href="#ref-Hensen2015">Hensen2015</a>, <a href="#ref-Giustina2015">Giustina2015</a>, <a href="#ref-Shalm2015">Shalm2015</a>] — have confirmed Bell violations reaching close to $2\sqrt{2}$, ruling out local hidden-variable theories at high statistical confidence.</p>
</div>
</section>

<div class="ckp-sep">Entanglement</div>

<!-- ─── SECTION 4 ─────────────────────────────────────────── -->
<section id="sec-entanglement">
<h2>4. What Entanglement Is Doing</h2>

<p>Entanglement is a property of the <em>joint</em> quantum state of two or more particles. It means the system cannot be fully described as two independent single-particle states.</p>

<h3>Product States vs. Entangled States</h3>

<p>A <em>product state</em> looks like:</p>

<div class="ckp-eq">
  <span class="eq-label">Product State — Eq. (7)</span>
  $$|\Psi\rangle = |\psi_1\rangle \otimes |\psi_2\rangle \tag{7}$$
</div>

<p>Here particle 1 is in state $|\psi_1\rangle$ and particle 2 is in state $|\psi_2\rangle$, entirely independently. Measuring particle 1 tells you nothing new about particle 2. A product state is a joint state, but not an entangled one.</p>

<p>An entangled state <em>cannot</em> be written this way. The two particles share a single, inseparable quantum description. The Bell singlet state is the canonical example:</p>

<div class="ckp-eq">
  <span class="eq-label">Bell Singlet State — Eq. (8)</span>
  $$|\Psi^{-}\rangle = \frac{1}{\sqrt{2}}\bigl(|\!\uparrow\downarrow\rangle - |\!\downarrow\uparrow\rangle\bigr) \tag{8}$$
</div>

<p>There is no way to factor this into a state for particle 1 times a state for particle 2. The pair is genuinely one system, despite its parts potentially being light-years apart.</p>

<h3>Why Entanglement Produces Stronger Correlations</h3>

<p>When Alice measures her particle along direction $a$ and gets $+1$, the joint state collapses to one where Bob's particle will give $-1$ if he measures along the same direction. But this does not allow faster-than-light signalling: Bob's outcomes still look completely random to him until he compares notes with Alice through a classical channel.</p>

<div class="ckp-callout">
  <strong>Why Can't We Simulate Entanglement Classically?</strong>
  <p>Suppose Alice and Bob meet beforehand, agree on a strategy (a hidden-variable model), and then travel to opposite ends of the lab. Can their pre-agreed strategy reproduce quantum correlations?</p>
  <p>Bell's theorem proves: <em>no</em>. No pre-agreed strategy — however clever, however randomised — can produce correlations that violate $|S| \leq 2$. The quantum world generates correlations that are simply outside the reach of any classical coordination scheme.</p>
  <p>Entanglement is not a hidden telephone line. It does not transmit signals. It creates a new kind of statistical dependency — one that is stronger than any classical correlation but still unable to carry information.</p>
</div>

<h3>How Is Entanglement Created?</h3>

<ul class="ckp-hier">
  <li><strong>Spontaneous Parametric Down-Conversion (SPDC).</strong> A laser photon passes through a nonlinear crystal and splits into two entangled photons of lower energy. This is the workhorse of photonic Bell experiments.</li>
  <li><strong>Beam-splitter interference.</strong> Two photons entering a beam splitter from opposite sides can emerge in an entangled superposition.</li>
  <li><strong>Controlled quantum gates.</strong> In superconducting or trapped-ion processors, a CNOT gate applied to two qubits produces entanglement from a product state.</li>
  <li><strong>Atomic emissions.</strong> Some atomic transitions emit two photons in a cascade, entangled in polarisation.</li>
</ul>

<h3>Is Entanglement Only for Photons?</h3>

<p>No. Entanglement is a general feature of quantum mechanics. It has been demonstrated in electrons (spin entanglement in solid-state devices), atoms and ions (trapped-ion quantum computers), molecules, mechanical oscillators visible under a microscope, and superconducting circuits — the platform used in the 2026 ETH Zürich experiment discussed in Section 7.</p>

<p>There is no theoretical upper limit on the mass of an entangled system, though <em>decoherence</em> — the loss of quantum properties due to interaction with the environment — makes entanglement increasingly fragile as systems grow larger and warmer.</p>

<h3>Why Are Spins Opposite in the Singlet State?</h3>

<p>The singlet state has total spin zero. Angular momentum is conserved when the pair is created, so the two spins must add to zero: if one is up, the other must be down. However — and this is the quantum twist — neither spin is up or down <em>until measured</em>. Both are in superposition. The correlation is not the result of pre-existing opposite spins; it is established at the moment of measurement, as prescribed by the joint quantum state. This is precisely what confounds classical intuition and what Bell's theorem quantifies.</p>
</section>

<div class="ckp-sep">Singlet vs. Joint State</div>

<!-- ─── SECTION 5 ─────────────────────────────────────────── -->
<section id="sec-singlet">
<h2>5. Singlet State versus Joint State</h2>

<p>These two terms are often confused. Let us be precise.</p>

<h3>The Joint State</h3>

<p>A <em>joint state</em> is any quantum state of a multi-particle system. It lives in the tensor-product Hilbert space $\mathcal{H}_1 \otimes \mathcal{H}_2$. Every two-particle quantum state — entangled or not — is a joint state.</p>

<h3>The Singlet State</h3>

<p>The singlet state (Eq. 8) is one specific joint state of two spin-$\tfrac{1}{2}$ particles. It is special for two reasons. First, the total spin is exactly zero, so the pair carries no net angular momentum. Second, it is <em>rotationally invariant</em>: no matter which direction you choose to measure, the statistics look the same. This symmetry yields the clean cosine correlation $E(a,b) = -\cos\theta$ and makes the singlet the ideal state for Bell experiments.</p>

<div class="ckp-definition">
  <div class="ckp-def-label">Hierarchy of State Types</div>
  <p>Every singlet state is a joint state. Not every joint state is a singlet. Not every joint state is entangled — a product state $|\!\uparrow\rangle|\!\downarrow\rangle$ is a joint state but not entangled.</p>
</div>

<div class="ckp-callout key">
  <strong>Can More Than Two Particles Be Entangled?</strong>
  <p>Yes. Multi-particle entanglement is well established and is crucial for quantum computing. <em>GHZ states</em> (Greenberger–Horne–Zeilinger) entangle three or more particles. <em>Cluster states</em> and <em>graph states</em> entangle many qubits in structured patterns that underpin measurement-based quantum computing. Quantum error-correcting codes use entanglement across dozens of physical qubits to protect one logical qubit.</p>
  <p>As of 2026, quantum processors with hundreds of entangled qubits have been demonstrated, though maintaining coherence across all of them simultaneously remains a major engineering challenge.</p>
</div>
</section>

<div class="ckp-sep">Physical Significance</div>

<!-- ─── SECTION 6 ─────────────────────────────────────────── -->
<section id="sec-matter">
<h2>6. Why Bell Violation Matters Physically</h2>

<p>Observing a Bell violation — experimentally measuring $|S| > 2$ — has a precise and profound implication: the world cannot be explained by a theory that combines pre-existing outcomes, locality, and classical hidden variables. At least one of these must be abandoned.</p>

<h3>What Bell Violation Does Not Mean</h3>

<ul class="ckp-hier">
  <li>It does <em>not</em> mean faster-than-light signalling is possible. Alice and Bob's individual outcomes are still locally random; no information is transmitted by the correlations alone.</li>
  <li>It does <em>not</em> pick a unique alternative theory. Quantum mechanics is the current best description, but other non-local or non-realist interpretations (Bohmian mechanics, many-worlds, relational QM) also reproduce the violations — they simply give up locality or realism in different ways.</li>
</ul>

<h3>What Bell Violation Does Mean</h3>

<div class="ckp-pull">
  <p>The classical picture of reality — particles with pre-written properties, no faster-than-light influences — is provably incomplete. Quantum correlations are real, verified, and stronger than any classical model can achieve.</p>
  <cite>— Consequence of loophole-free Bell tests, 2015–2026</cite>
</div>

<p>This has moved from philosophical speculation to engineering fact: Bell violations are now the foundation of device-independent cryptography and certified randomness generation.</p>

<h3>Quantum Computers: Superposition and Entanglement</h3>

<div class="ckp-callout">
  <strong>Is Quantum Computing Just Classical Computing Without Entanglement?</strong>
  <p>Essentially, yes. A quantum circuit with no entanglement can be efficiently simulated on a classical computer. The exponential advantage of quantum computing derives from the combination of superposition <em>and</em> entanglement.</p>
  <p>Superposition allows a qubit to represent $|0\rangle$ and $|1\rangle$ simultaneously. Entanglement correlates qubits in ways that cannot be decomposed qubit-by-qubit. Together, $n$ entangled qubits can represent $2^n$ amplitudes simultaneously — a Hilbert space that grows <em>exponentially</em> with $n$.</p>
  <p>Quantum algorithms such as Shor's factoring algorithm and Grover's search algorithm exploit this structure to solve certain problems exponentially or quadratically faster than the best known classical methods. Without entanglement, a quantum computer degrades to a probabilistic classical computer.</p>
</div>
</section>

<div class="ckp-sep">Device-Independent Randomness</div>

<!-- ─── SECTION 7 ─────────────────────────────────────────── -->
<section id="sec-qrng">
<h2>7. Bell Inequality and Quantum Random Number Generators</h2>

<p>Not every quantum random number generator (QRNG) needs Bell inequality violation. But for the strongest possible certification of randomness, Bell tests become indispensable.</p>

<h3>Types of QRNGs</h3>

<ul class="ckp-hier">
  <li><strong>Single-system QRNGs.</strong> A photon hitting a beam splitter takes one of two paths with equal probability. The randomness is quantum-mechanical but you must trust that the device works as specified. If the manufacturer has planted a bias, you cannot detect it from the outputs alone.</li>
  <li><strong>Semi-device-independent QRNGs.</strong> Some assumptions about the device are relaxed (e.g. the dimension of the Hilbert space), providing intermediate certification.</li>
  <li><strong>Device-independent QRNGs (DI-QRNGs).</strong> Bell violation is the certification tool. If $|S| > 2$ is observed, no local deterministic hidden-variable model can explain the outputs — randomness is certified without any trust in the internal device structure.</li>
</ul>

<h3>How Does Bell Violation Certify Randomness?</h3>

<p>Here is the key logical step. A Bell violation certifies that the measurement outcomes cannot be predicted by any local hidden variable — not even one known to the device manufacturer. If the outcomes were deterministic (pre-written on a hidden card), the CHSH value would satisfy $|S| \leq 2$. Observing $|S| > 2$ therefore implies the outcomes contain <em>irreducible, unpredictable randomness</em>. The device itself certifies its own unpredictability.</p>

<h3>Breakthrough: ETH Zürich and Certified Perfect Randomness (2026)</h3>

<div class="ckp-callout key">
  <strong>Case Study: Perfect Randomness Realised for the First Time [<a href="#ref-Kulikov2026">Kulikov2026</a>]</strong>
  <p>In May 2026, researchers at ETH Zürich led by Renato Renner and Andreas Wallraff published a landmark result in <em>Nature</em>: the first experimental demonstration of certified perfect randomness using a Bell test.</p>
  <p><strong>The setup.</strong> The experiment used two superconducting qubit chips cooled to temperatures near absolute zero, connected by a 30-metre cryogenically cooled tube through which microwave photons could travel, creating quantum entanglement between the two qubits. The 30-metre separation closed the locality loophole: no classical signal could travel between the chips during the measurement window.</p>
  <p><strong>Why was this hard?</strong> A Bell test requires three things simultaneously: high-quality entanglement (to produce CHSH values well above 2), high data rate (to accumulate enough statistics for rigorous certification), and space-like separation (to close the locality loophole). Achieving all three at once with superconducting qubits — which must be kept at millikelvin temperatures — was an exceptional engineering feat.</p>
  <p><strong>Randomness amplification.</strong> The key conceptual insight is <em>randomness amplification</em>: you do not need perfect randomness to start with. Even if your initial random seed is slightly biased (up to 0.75% bias in this experiment), a Bell test can amplify it into certified-perfect randomness. The team applied a <em>two-source extractor</em> — a classical algorithm that takes two independent weak random inputs and produces one strongly random output.</p>
</div>

<!-- Experiment stats -->
<div class="ckp-stat-row">
  <div class="ckp-stat"><span class="stat-num">2.271</span><span class="stat-label">Average CHSH value (classical bound: 2)</span></div>
  <div class="ckp-stat"><span class="stat-num">1.34B</span><span class="stat-label">Bell-test trials performed</span></div>
  <div class="ckp-stat"><span class="stat-num">9 hr</span><span class="stat-label">Total experiment duration</span></div>
  <div class="ckp-stat"><span class="stat-num">$10^{-12}$</span><span class="stat-label">Failure probability bound</span></div>
</div>

<p>The experiment ran at 50,000 trials per second, performing $1{,}342{,}177{,}280$ trials in total. The final output was a certified-random string of $45{,}025{,}658$ bits, extracted from roughly $5.4 \times 10^{9}$ low-quality input bits. As Renner described: the output is guaranteed to remain perfectly random for all time, regardless of what analytical methods are used to assess it. Possible applications include cryptographic key generation, public randomness services for lotteries and blockchains, and certified randomness beacons for digital security infrastructure.</p>
</section>

<div class="ckp-sep">The Full Chain</div>

<!-- ─── SECTION 8 ─────────────────────────────────────────── -->
<section id="sec-chain">
<h2>8. The Main Picture in One Chain</h2>

<p>Everything in this paper connects into a single logical chain:</p>

<div class="ckp-chain">

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">1</div>
    <div class="ckp-chain-content">
      <h4>Local Realism Makes a Prediction</h4>
      <p>If particles carry pre-written answers and no influence travels faster than light, then the CHSH correlator satisfies $|S| \leq 2$.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">2</div>
    <div class="ckp-chain-content">
      <h4>Entangled States Defy the Prediction</h4>
      <p>The quantum singlet state produces cosine correlations $E(a,b) = -\cos\theta$. With the right choice of angles, these give $|S| = 2\sqrt{2} \approx 2.83$.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">3</div>
    <div class="ckp-chain-content">
      <h4>Experiments Confirm the Violation</h4>
      <p>Loophole-free Bell tests [<a href="#ref-Hensen2015">Hensen2015</a>] and the ETH Zürich experiment [<a href="#ref-Kulikov2026">Kulikov2026</a>] consistently measure $|S| > 2$, ruling out local hidden-variable theories.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">4</div>
    <div class="ckp-chain-content">
      <h4>Conclusion About Reality</h4>
      <p>The world is not fully described by local pre-written answers. At least one of locality or realism must be abandoned.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">5</div>
    <div class="ckp-chain-content">
      <h4>Practical Payoff</h4>
      <p>Quantum randomness can be certified without trusting any device. Bell violation proves unpredictability from the outside.</p>
    </div>
  </div>

</div>

<h3>A Note on Interpretations</h3>

<p>Giving up local realism does not uniquely fix which alternative is correct. Different interpretations of quantum mechanics make different choices:</p>

<ul class="ckp-hier">
  <li><strong>Copenhagen.</strong> Measurement outcomes are genuinely not determined until the act of measurement (gives up realism).</li>
  <li><strong>Bohmian mechanics.</strong> Particles have definite positions at all times, guided by a non-local pilot wave (gives up locality).</li>
  <li><strong>Many-worlds.</strong> All outcomes occur in branching universes; the apparent randomness is observer-relative (gives up a single outcome per experiment).</li>
</ul>

<div class="ckp-pull">
  <p>What Bell's theorem guarantees is that the simple classical picture — local, realist, no hidden message between particles — is experimentally falsified. The deeper story of what replaces it remains one of the great open questions in the foundations of physics.</p>
  <cite>— On Bell's Theorem and the foundations of physics</cite>
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
    <td><span class="term">Local Realism</span></td>
    <td>Particles carry pre-written outcomes; no faster-than-light influence.</td>
  </tr>
  <tr>
    <td><span class="term">CHSH Bound</span></td>
    <td>$|S| \leq 2$ — the maximum correlation achievable by any local hidden-variable theory.</td>
  </tr>
  <tr>
    <td><span class="term">Tsirelson Bound</span></td>
    <td>$|S| = 2\sqrt{2} \approx 2.83$ — the quantum maximum, achieved by the singlet state at optimal angles.</td>
  </tr>
  <tr>
    <td><span class="term">Bell Violation</span></td>
    <td>Experimental observation of $|S| > 2$, ruling out local hidden-variable theories.</td>
  </tr>
  <tr>
    <td><span class="term">Entanglement</span></td>
    <td>Joint quantum state that cannot be factored into independent single-particle states.</td>
  </tr>
  <tr>
    <td><span class="term">Singlet State</span></td>
    <td>$|\Psi^{-}\rangle = \tfrac{1}{\sqrt{2}}(|\!\uparrow\downarrow\rangle - |\!\downarrow\uparrow\rangle)$ — total spin zero, rotationally invariant, maximally entangled.</td>
  </tr>
  <tr>
    <td><span class="term">DI-QRNG</span></td>
    <td>Device-independent QRNG — randomness certified by Bell violation alone, without trusting device internals.</td>
  </tr>
  <tr>
    <td><span class="term">Randomness Amplification</span></td>
    <td>Protocol converting weak (biased) randomness into certified-perfect randomness using a Bell test and a classical two-source extractor.</td>
  </tr>
  <tr>
    <td><span class="term">Superposition</span></td>
    <td>A quantum system existing in multiple states simultaneously until a measurement forces one definite outcome.</td>
  </tr>
  <tr>
    <td><span class="term">Decoherence</span></td>
    <td>The loss of quantum properties due to interaction with the environment; makes entanglement fragile in macroscopic systems.</td>
  </tr>
</tbody>
</table>
</div>
</section>

<!-- ─── REFERENCES ─────────────────────────────────────────── -->
<div class="ckp-refs" id="references">
<h2>References</h2>
<p id="ref-Bell1964"><span class="ref-num">[Bell1964]</span> Bell, J.S.: On the Einstein-Podolsky-Rosen paradox. <em>Physics</em> <strong>1</strong>(3), 195–200 (1964)</p>
<p id="ref-CHSH1969"><span class="ref-num">[CHSH1969]</span> Clauser, J.F., Horne, M.A., Shimony, A., Holt, R.A.: Proposed experiment to test local hidden-variable theories. <em>Phys. Rev. Lett.</em> <strong>23</strong>(15), 880–884 (1969). <a href="https://doi.org/10.1103/PhysRevLett.23.880">doi:10.1103/PhysRevLett.23.880</a></p>
<p id="ref-Hensen2015"><span class="ref-num">[Hensen2015]</span> Hensen, B., et al.: Loophole-free Bell inequality violation using electron spins separated by 1.3 kilometres. <em>Nature</em> <strong>526</strong>, 682–686 (2015). <a href="https://doi.org/10.1038/nature15759">doi:10.1038/nature15759</a></p>
<p id="ref-Giustina2015"><span class="ref-num">[Giustina2015]</span> Giustina, M., et al.: Significant-loophole-free test of Bell's theorem with entangled photons. <em>Phys. Rev. Lett.</em> <strong>115</strong>, 250401 (2015). <a href="https://doi.org/10.1103/PhysRevLett.115.250401">doi:10.1103/PhysRevLett.115.250401</a></p>
<p id="ref-Shalm2015"><span class="ref-num">[Shalm2015]</span> Shalm, L.K., et al.: Strong loophole-free test of local realism. <em>Phys. Rev. Lett.</em> <strong>115</strong>, 250402 (2015). <a href="https://doi.org/10.1103/PhysRevLett.115.250402">doi:10.1103/PhysRevLett.115.250402</a></p>
<p id="ref-Kulikov2026"><span class="ref-num">[Kulikov2026]</span> Kulikov, A., Storz, S., Schär, J.D., Sandfuchs, M., Wolf, R., Berterottière, F., Hellings, C., Wallraff, A., Renner, R.: Experimental randomness amplification. <em>Nature</em> (27 May 2026). <a href="https://doi.org/10.1038/s41586-026-10521-8">doi:10.1038/s41586-026-10521-8</a>. See also: <a href="https://ethz.ch/en/news-and-events/eth-news/news/2026/05/perfect-randomness-realised-for-the-first-time.html">ETH Zürich News</a></p>
</div>

</div><!-- end .ckp-body -->

<!-- ─── Sidebar TOC ─────────────────────────────────────────── -->
<aside class="ckp-sidebar">
  <div class="ckp-toc-label">Contents</div>
  <ul class="ckp-toc-list" id="ckp-toc">
    <li data-section="abstract"><a href="#abstract">Abstract</a></li>
    <li data-section="sec-bell"><a href="#sec-bell">1. What Bell's Inequality Is About</a></li>
    <li class="toc-sub" data-section="sec-bell"><a href="#sec-bell">Local Realism Pillars</a></li>
    <li class="toc-sub" data-section="sec-bell"><a href="#sec-bell">Measurement Primer</a></li>
    <li data-section="sec-classical"><a href="#sec-classical">2. Classical Limit of 2</a></li>
    <li class="toc-sub" data-section="sec-classical"><a href="#sec-classical">Algebraic Core</a></li>
    <li data-section="sec-qm"><a href="#sec-qm">3. Quantum Exceeds 2</a></li>
    <li class="toc-sub" data-section="sec-qm"><a href="#sec-qm">Quantum Correlation</a></li>
    <li class="toc-sub" data-section="sec-qm"><a href="#sec-qm">Tsirelson Bound</a></li>
    <li data-section="sec-entanglement"><a href="#sec-entanglement">4. Entanglement</a></li>
    <li class="toc-sub" data-section="sec-entanglement"><a href="#sec-entanglement">Product vs. Entangled</a></li>
    <li class="toc-sub" data-section="sec-entanglement"><a href="#sec-entanglement">How Entanglement Forms</a></li>
    <li data-section="sec-singlet"><a href="#sec-singlet">5. Singlet vs. Joint State</a></li>
    <li data-section="sec-matter"><a href="#sec-matter">6. Physical Significance</a></li>
    <li class="toc-sub" data-section="sec-matter"><a href="#sec-matter">Interpretations</a></li>
    <li data-section="sec-qrng"><a href="#sec-qrng">7. QRNGs & Randomness</a></li>
    <li class="toc-sub" data-section="sec-qrng"><a href="#sec-qrng">ETH Zürich 2026</a></li>
    <li data-section="sec-chain"><a href="#sec-chain">8. The Full Chain</a></li>
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
  var sections = ['abstract','sec-bell','sec-classical','sec-qm','sec-entanglement','sec-singlet','sec-matter','sec-qrng','sec-chain','sec-glossary','references'];
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