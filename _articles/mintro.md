---
layout: post
title: "No Entropy Without a Model"
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
  content: '\25B8';
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
  <div class="ckp-kicker">Cryptographic RNGs · Entropy Sources · Stochastic Models</div>
  <h1>No Entropy Without a <em>Model</em></h1>
  <p class="ckp-deck">A model-based discipline for entropy sources. Unpredictability is not a property of an output string — it is a property of an adversary's uncertainty, and a cryptographic argument must lower-bound that uncertainty.</p>
  <div class="ckp-meta">
    <span>Sara Malik &amp; Naveed A. Aun</span>
    <span class="dot"></span>
    <span>PakCrypt NPO</span>
    <span class="dot"></span>
    <span>~35 min read</span>
  </div>
</div>
<!-- Keywords -->
<div class="ckp-keywords">
  <span class="ckp-kw">True RNG</span>
  <span class="ckp-kw">Quantum RNG</span>
  <span class="ckp-kw">Min-Entropy</span>
  <span class="ckp-kw">Stochastic Model</span>
  <span class="ckp-kw">SP 800-90B</span>
  <span class="ckp-kw">AIS 31</span>
  <span class="ckp-kw">Health Tests</span>
  <span class="ckp-kw">Side-Channel Leakage</span>
  <span class="ckp-kw">Conditioning</span>
</div>
<!-- Mobile TOC -->
<div class="ckp-mobile-toc" id="ckp-mob-toc-toggle">
  <span>Contents</span><span>&#9662;</span>
</div>
<div class="ckp-mobile-toc-list" id="ckp-mob-toc-list">
  <a href="#abstract">Abstract</a>
  <a href="#sec-intro">1. Introduction</a>
  <a href="#sec-entropy">2. From Unpredictability to Conditional Min-Entropy</a>
  <a href="#sec-models">3. Analytical Output Models</a>
  <a href="#sec-measurement">4. Measurement, Estimation, and Health Tests</a>
  <a href="#sec-leakage">5. Leakage: Confidentiality of Unpredictability</a>
  <a href="#sec-conditioning">6. Conditioning and Entropy Accounting</a>
  <a href="#sec-quantum">7. The Quantum Case</a>
  <a href="#sec-conclusion">8. Conclusion</a>
  <a href="#sec-glossary">Quick Reference Glossary</a>
  <a href="#references">References</a>
</div>
<!-- ═══════════════════ LAYOUT ════════════════════════════════ -->
<div class="ckp-layout">
<!-- ─── Sidebar TOC ─────────────────────────────────────────── -->
<div class="ckp-sidebar">
  <div class="ckp-toc-label">Contents</div>
  <ul class="ckp-toc-list">
    <li class="active"><a href="#abstract">Abstract</a></li>
    <li><a href="#sec-intro">1. Introduction</a></li>
    <li class="toc-sub"><a href="#sec-intro-error">The Error We Address</a></li>
    <li class="toc-sub"><a href="#sec-intro-standards">Where the Standards Stand</a></li>
    <li class="toc-sub"><a href="#sec-intro-obligations">The Five Obligations</a></li>
    <li><a href="#sec-entropy">2. Unpredictability to Min-Entropy</a></li>
    <li class="toc-sub"><a href="#sec-min-entropy">Min-Entropy</a></li>
    <li class="toc-sub"><a href="#sec-conditional">Conditional Min-Entropy</a></li>
    <li class="toc-sub"><a href="#sec-lhl">Leftover Hash Lemma</a></li>
    <li class="toc-sub"><a href="#sec-model-necessary">Why a Model Is Necessary</a></li>
    <li><a href="#sec-models">3. Analytical Output Models</a></li>
    <li class="toc-sub"><a href="#sec-jitter">Oscillator Jitter</a></li>
    <li class="toc-sub"><a href="#sec-thermal">Amplified Thermal Noise</a></li>
    <li class="toc-sub"><a href="#sec-metastability">Metastability</a></li>
    <li class="toc-sub"><a href="#sec-photon">Single-Photon Which-Path</a></li>
    <li class="toc-sub"><a href="#sec-homodyne">Vacuum-Fluctuation Homodyne</a></li>
    <li><a href="#sec-measurement">4. Measurement &amp; Health Tests</a></li>
    <li><a href="#sec-leakage">5. Leakage Containment</a></li>
    <li><a href="#sec-conditioning">6. Conditioning &amp; Accounting</a></li>
    <li><a href="#sec-quantum">7. The Quantum Case</a></li>
    <li><a href="#sec-conclusion">8. Conclusion</a></li>
    <li><a href="#sec-glossary">Quick Reference</a></li>
    <li><a href="#references">References</a></li>
  </ul>
</div>
<!-- ─── Main Body ─────────────────────────────────────────── -->
<div class="ckp-body">
<!-- ABSTRACT -->
<div class="ckp-abstract" id="abstract">
  <div class="ckp-abstract-label">Abstract</div>
  <p>Hardware and quantum random number generators are routinely justified by an appeal to physical unpredictability followed by a clean pass through a statistical test battery. We argue that this justification is insufficient. Unpredictability is not a property of an output string; it is a property of an adversary's uncertainty, and a cryptographic argument must lower-bound that uncertainty. We treat three classical noise sources (oscillator jitter, amplified thermal noise, metastability) and two quantum sources (single-photon which-path and vacuum-fluctuation homodyne); for each we derive an analytical output model $p(x \mid \theta)$ from first principles together with an explicit falsification criterion. The recurring lesson is that a conditioner cannot manufacture entropy a model never proved.</p>
</div>
<!-- STATS BAR -->
<div class="ckp-stat-row">
  <div class="ckp-stat"><span class="stat-num">5</span><span class="stat-label">Source classes modelled from first principles</span></div>
  <div class="ckp-stat"><span class="stat-num">5</span><span class="stat-label">Linked obligations for certification</span></div>
  <div class="ckp-stat"><span class="stat-num">2</span><span class="stat-label">Governing standards: SP 800-90B &amp; AIS 31</span></div>
  <div class="ckp-stat"><span class="stat-num">$H_{\infty}$</span><span class="stat-label">Conditional min-entropy: the certifiable object</span></div>
</div>
<!-- ─── SECTION 1 ─────────────────────────────────────────── -->
<section id="sec-intro">
<h2>1. Introduction</h2>
<p class="drop-cap">A random number generator that merely <em>looks</em> unpredictable offers a cryptographer little assurance, because essentially every deterministic generator that was eventually broken also looked unpredictable beforehand. The clearest illustration is Dual_EC_DRBG. It was standardised in NIST SP 800-90, shipped by default in widely deployed libraries, and passes statistical test batteries without complaint; yet Shumow and Ferguson showed in 2007 that an adversary who knows a secret relation between two curve points can reconstruct the generator's internal state from a short run of output and predict everything that follows [<a href="#ref-shumow2007">Shumow2007</a>, <a href="#ref-bernstein2016">Bernstein2016</a>]. The output was indistinguishable from random to anyone without that side information and fully predictable to anyone with it.</p>
<p>A purely classical example makes the same point without malice: the Mersenne Twister passes most of Dieharder and TestU01, yet its entire future is determined once an observer has seen 624 consecutive outputs. <em>"Passes the tests"</em> and <em>"is unpredictable to the adversary"</em> are simply different properties.</p>
<div class="ckp-pull">
  <p>Randomness is not a visible feature of a bit string emerging from a black box. It is the gap between what the adversary knows and what the adversary would need to know to predict the next sample.</p>
  <cite>&mdash; The organising principle of this paper</cite>
</div>
<p>Randomness, then, is not a visible feature of a bit string emerging from a black box. It is the gap between what the adversary knows and what the adversary would need to know to predict the next sample. Building an entropy source is the discipline of bounding that gap from below, and of keeping it bounded while the device runs. Everything in this paper follows from taking that one sentence literally.</p>
<h3 id="sec-intro-error">The Error We Address</h3>
<p>A common informal argument runs as follows: the source is physically unpredictable; a hash or a von Neumann corrector compresses it; the compressed stream passes NIST STS and Dieharder; therefore the output has full entropy. Each step is either a non-sequitur or false. "Physically unpredictable" is unquantified until a model attaches a number to it. Compression preserves min-entropy at best and usually reduces it — it can never increase it, because a deterministic function of $X$ cannot have more min-entropy than $X$: any guessing strategy for the input induces at least as good a strategy for the output (formally, $H_{\infty}(f(X)) \leq H_{\infty}(X)$ for every deterministic $f$, the data-processing inequality for min-entropy). And a statistical battery detects gross structure while certifying nothing about entropy: a counter encrypted under AES passes every test in STS and Dieharder and has zero entropy given the key.</p>
<h3 id="sec-intro-standards">Where the Standards Stand</h3>
<p>Two evaluation traditions govern entropy sources, and they emphasise different things. <strong>NIST SP 800-90B</strong> [<a href="#ref-turan2018">Turan2018</a>] is estimator-centric: it requires a description of the noise source and then runs a battery of conservative min-entropy estimators on raw data, taking the minimum, with a lighter formal demand on a closed-form physical model. <strong>BSI AIS 31</strong> — in its 2024 revision, now Version 3.0 of the mathematical-technical reference by Peter and Schindler [<a href="#ref-peter2024">Peter2024</a>], superseding the 2011 Killmann–Schindler document [<a href="#ref-killmann2011">Killmann2011</a>] — is model-centric: for its higher class PTG.3 it requires an explicit stochastic model of the raw signal from which the entropy is derived and against which the online tests are justified. The two are converging: BSI and NIST have publicly described joint work comparing AIS 20/31 with the SP 800-90 series [<a href="#ref-schindler2023">Schindler2023</a>].</p>
<h3 id="sec-intro-obligations">The Five Obligations</h3>
<p>Our position is the practical intersection of the two traditions. An entropy claim is admissible if and only if it is the conclusion of the following linked obligations:</p>
<div class="ckp-chain">
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">1</div>
    <div class="ckp-chain-content">
      <h4>Stochastic Model</h4>
      <p>A model $p(x \mid \theta)$ of the raw source, derived from device physics, with parameter vector $\theta$ identified with measurable electrical or optical quantities.</p>
    </div>
  </div>
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">2</div>
    <div class="ckp-chain-content">
      <h4>Measured Entropy Bound</h4>
      <p>A measured lower confidence bound on the (possibly conditional) min-entropy per raw sample, obtained on raw, pre-conditioning data with the most conservative applicable estimator.</p>
    </div>
  </div>
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">3</div>
    <div class="ckp-chain-content">
      <h4>Model-Bound Health Tests</h4>
      <p>Online tests whose alarm thresholds are computed from the model's worst-case parameters and whose detection latency is proven, by fault injection, to fire before the min-entropy falls below the claim.</p>
    </div>
  </div>
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">4</div>
    <div class="ckp-chain-content">
      <h4>Conditioner Margin</h4>
      <p>A conditioner whose input-entropy margin is accounted for explicitly, so that the output entropy is a consequence of the measured bound, not an assumption.</p>
    </div>
  </div>
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">5</div>
    <div class="ckp-chain-content">
      <h4>Leakage Containment</h4>
      <p>An argument that the side information $E$ in the conditional bound is complete — that no physical side channel (power, EM, timing, acoustic, photonic) hands the adversary information the model omitted.</p>
    </div>
  </div>
</div>
<p>In one line: we replace <em>"unpredictable, compressed, and tested"</em> with <em>"modeled, measured, monitored, margined, and shielded."</em> Drop any one obligation and the others stop meaning anything.</p>
<div class="ckp-callout key">
  <strong>Contributions</strong>
  <p>This paper contributes: (i) a unifying argument that reduces "unpredictability" to a monitored lower bound on conditional min-entropy; (ii) first-principles output models $p(x \mid \theta)$ for five source classes, each with per-sample min-entropy and an explicit falsification criterion; (iii) a measurement-and-health-test protocol binding each online test to a specific model parameter; (iv) an explicit treatment of side-channel leakage as a first-class entropy obligation; and (v) a conditioning and entropy-pool discipline with end-to-end accounting.</p>
</div>
</section>
<div class="ckp-sep">Entropy Foundations</div>
<!-- ─── SECTION 2 ─────────────────────────────────────────── -->
<section id="sec-entropy">
<h2>2. From Unpredictability to Conditional Min-Entropy</h2>
<h3 id="sec-min-entropy">2.1 Min-Entropy</h3>
<p>For a source emitting a symbol $X$ with distribution $\{p_i\}$, Shannon entropy measures the average surprise. That is the wrong average for a key, which an adversary guesses once with their single best guess, not repeatedly. The relevant quantity is the worst case, the <strong>min-entropy</strong>:</p>
<div class="ckp-eq">
  <span class="eq-label">Min-Entropy — Eq. (1)</span>
  $$H_{\infty}(X) = -\log_2 \max_i p_i \tag{1}$$
</div>
<p>The two diverge precisely when one outcome is much more likely than the rest. Consider a source over 129 symbols that emits one fixed symbol with probability $\tfrac{1}{2}$ and spreads the remaining probability uniformly over the other 128. Its Shannon entropy is $\tfrac{1}{2} \cdot 1 + \tfrac{1}{2} \cdot (1 + \log_2 128) = 4.5$ bits, which sounds comfortable; its min-entropy is $-\log_2 \tfrac{1}{2} = 1$ bit, because an adversary who always guesses the fixed symbol is right half the time.</p>
<div class="ckp-callout warn">
  <strong>Why Shannon Entropy Is the Wrong Metric</strong>
  <p>A key drawn from a source with high Shannon entropy but low min-entropy is broken on the first guess with probability one-half. Shannon entropy is irrelevant to that fact; min-entropy reports it exactly. This is why cryptographic entropy accounting is always a worst-case, lower-bound discipline.</p>
</div>
<h3 id="sec-conditional">2.2 Conditional Min-Entropy</h3>
<p>Real sources are not isolated, and the adversary is not blind. Let $E$ denote all side information available to or controllable by the adversary: electronic noise, supply ripple, the classical excess noise of a homodyne detector, a temperature the attacker is allowed to drift. The correct object is the <strong>average conditional min-entropy</strong> of Dodis <em>et al.</em> [<a href="#ref-dodis2008">Dodis2008</a>]:</p>
<div class="ckp-eq">
  <span class="eq-label">Average Conditional Min-Entropy — Eq. (2)</span>
  $$\tilde{H}_{\infty}(X \mid E) = -\log_2 \mathbb{E}_{e \leftarrow E}\left[ \max_x \Pr(X = x \mid E = e) \right] \tag{2}$$
</div>
<p>The inner maximum is the adversary's best guess once they have seen the realisation $e$ of the side information; the outer expectation averages their success probability over the side information they will actually see; the negative logarithm turns that success probability into bits.</p>
<div class="ckp-callout">
  <strong>Worked Example: The Noisy Sensor</strong>
  <p>Suppose $X$ is a fair bit but a noisy sensor leaks $E = X \oplus N$, where $N = 0$ with probability $0.9$. Unconditionally $H_{\infty}(X) = 1$. But an adversary who reads $E$ and guesses $X = E$ is correct with probability $0.9$, so $\tilde{H}_{\infty}(X \mid E) = -\log_2 0.9 \approx 0.152$ bits. The bit "looks" fully random in isolation and is worth almost nothing against this adversary.</p>
</div>
<p>Equation (2) is exactly why a vacuum-fluctuation QRNG cannot quote the variance of its digitised quadrature as entropy: part of that variance is classical excess noise $E$, and the adversary is permitted to know it. The extractable randomness is what survives conditioning on $E$, never the total.</p>
<h3 id="sec-lhl">2.3 The Leftover Hash Lemma and the Price of Conditioning</h3>
<p>A conditioner cannot create min-entropy; the best it can do is concentrate existing min-entropy into a shorter, nearly uniform string, and even that costs something. The tool that prices it is the <strong>Leftover Hash Lemma</strong> [<a href="#ref-impagliazzo1989">Impagliazzo1989</a>, <a href="#ref-dodis2008">Dodis2008</a>]. A family $\mathcal{H} = \{h : \{0,1\}^n \to \{0,1\}^m\}$ is universal if for every pair of distinct inputs $x \neq x'$ a uniformly chosen $h$ collides with probability at most $2^{-m}$; standard low-cost constructions (multiplication in GF$(2^n)$, Toeplitz-matrix products) satisfy this.</p>
<p>Applied with a public uniform seed to a source of conditional min-entropy $k$, such a family yields output within statistical distance $\varepsilon$ of uniform (even given $E$ and the seed) provided:</p>
<div class="ckp-eq">
  <span class="eq-label">Leftover Hash Lemma — Eq. (3)</span>
  $$m \leq k - 2\log_2(1/\varepsilon) \tag{3}$$
</div>
<p>This is the whole truth about lossless post-processing, and it disposes of the amplification fantasy in one line: if $k$ is small, no choice of hash makes $m$ large. The $2\log_2(1/\varepsilon)$ term is the entropy gap one pays for near-uniformity; in cryptographically hardened form it reappears as the "+64" in the NIST conditioning rule of Section 6.</p>
<h3 id="sec-model-necessary">2.4 Why a Stochastic Model Is Necessary, Not Merely Nice</h3>
<p>It is tempting to ask: why is the model required at all? If one captures raw data, runs the SP 800-90B non-IID estimators, and obtains a healthy number, why is that not enough? Three concrete reasons follow.</p>
<p><strong>First,</strong> estimators bound the entropy of the observed distribution, but an entropy source must hold across an operating envelope — process, voltage, temperature, ageing — that no finite capture exhausts. The model is what extrapolates a bound measured at a few corners to the corners you did not test, because it says which parameter governs the entropy and how.</p>
<p><strong>Second,</strong> an estimator cannot separate intrinsic randomness from deterministic structure that merely looks complex. A weakly chaotic but deterministic circuit, or one injection-locked to an attacker's signal, can yield raw data on which the estimators report high entropy while the true conditional min-entropy against an informed adversary is near zero — this is precisely the Dual_EC_DRBG situation re-expressed at the physical layer.</p>
<p><strong>Third,</strong> the model is what makes the health test meaningful. A test threshold computed from a model parameter is a test of the entropy; a generic statistical test run on the output is a test of the conditioner. This is why AIS 31 PTG.3 elevates the stochastic model to a requirement rather than a recommendation.</p>
<div class="ckp-definition">
  <div class="ckp-def-label">Definition: Certifiable Entropy Source</div>
  <p>An entropy source is certifiable when there exist (i) a stochastic model $p(x \mid \theta)$, (ii) a measured lower bound $\hat{H}$ on $\tilde{H}_{\infty}(X \mid E)$ valid across the declared operating envelope, and (iii) an online test that rejects any trajectory on which the model's parameters leave the region in which $\tilde{H}_{\infty} \geq \hat{H}$ holds. Unpredictability that cannot be written in this form is an aesthetic judgement, not a security parameter.</p>
</div>
</section>
<div class="ckp-sep">Source Models</div>
<!-- ─── SECTION 3 ─────────────────────────────────────────── -->
<section id="sec-models">
<h2>3. Analytical Output Models</h2>
<p>We study five source classes chosen to span the field: free-running oscillator jitter, amplified thermal noise, and metastability on the classical side; single-photon which-path and vacuum-fluctuation homodyne on the quantum side. Each has at least two independent peer-reviewed silicon or optical realisations and a published stochastic model referenced by NIST or BSI material.</p>
<p>For each source we give a physics-grounded derivation of the output model $p(x \mid \theta)$, identify $\theta$ with measurable quantities, state the resulting per-sample min-entropy, and give the criterion under which we would declare the model false.</p>
<h3 id="sec-jitter">3.1 Oscillator Jitter</h3>
<p><strong>Physics.</strong> A free-running ring oscillator accumulates phase error because each gate delay is perturbed by thermal noise in the channel of its transistors; over time scales long compared with one period these independent perturbations sum into a random walk in phase. This is the standard Wiener-process model of phase diffusion [<a href="#ref-baudet2011">Baudet2011</a>, <a href="#ref-killmann2008">Killmann2008</a>]: the accumulated phase deviation over a sampling interval $\tau$ has variance growing linearly, $\sigma_{\text{acc}}^2(\tau) = \kappa\tau$, with diffusion coefficient $\kappa$ fixed by device thermal noise.</p>
<p><strong>Output.</strong> Sampling the oscillator with a reference edge reads the phase modulo the period $T_0$. Writing the normalised sampling phase $\psi = (\phi / T_0) \bmod 1$, the output bit is its most significant bit. Treating the accumulated jitter as Gaussian and expanding the bit probability in a Fourier series, every harmonic of order $k$ is suppressed by $\exp(-2\pi^2 k^2 Q)$ with the single governing parameter:</p>
<div class="ckp-eq">
  <span class="eq-label">Jitter Quality Factor — Eq. (4)</span>
  $$Q = \frac{\sigma_{\text{acc}}^2}{T_0^2} \tag{4}$$
</div>
<p>The bias is dominated by the first harmonic:</p>
<div class="ckp-eq">
  <span class="eq-label">Bit Bias Bound — Eq. (5)</span>
  $$\Bigl|\Pr(b=1) - \frac{1}{2}\Bigr| \leq \frac{C}{\pi} e^{-2\pi^2 Q} \tag{5}$$
</div>
<p>with a model-dependent constant $C$ of order unity [<a href="#ref-baudet2011">Baudet2011</a>], and the per-bit min-entropy follows:</p>
<div class="ckp-eq">
  <span class="eq-label">Per-Bit Min-Entropy — Eq. (6)</span>
  $$H_{\infty}(b) = -\log_2\left(\frac{1}{2} + \Bigl|\Pr(b=1) - \frac{1}{2}\Bigr|\right) \approx 1 - \frac{2C}{\pi \ln 2} e^{-2\pi^2 Q} \tag{6}$$
</div>
<div class="ckp-callout">
  <strong>Key Insight</strong>
  <p>Serial correlation between successive bits decays with the same exponential, so a measured $Q$ bounds bias and dependence simultaneously: the entropy claim reduces to measuring one jitter variance and one period. The SP 800-90B most-common-value (MCV) lower bound on $10^6$ simulated bits agrees with the exact wrapped-Gaussian bit probability to within its confidence interval (e.g. 0.768 versus 0.773 at $Q = 0.1$, 0.992 versus 0.996 at $Q \gtrsim 0.3$).</p>
</div>
<p><strong>Falsification.</strong> Collect raw bits across the PVT envelope; estimate $Q$ from a direct period/jitter measurement; predict bias and lag-1 correlation from Eq. (5); compare with measurement. If the measured bias exceeds the prediction beyond the confidence interval, or if its scaling with $\tau$ departs from $\exp(-2\pi^2 \kappa\tau / T_0^2)$, the Wiener-jitter model is rejected — typically a sign of injection locking or of flicker jitter dominating, either of which changes the scaling law.</p>
<h3 id="sec-thermal">3.2 Amplified Thermal Noise</h3>
<p><strong>Physics.</strong> The thermal agitation of charge carriers in a resistor produces a fluctuating voltage even with no applied signal: at the microscopic level the carriers are in constant random motion set by temperature, and the fluctuation–dissipation theorem ties the resulting open-circuit voltage to temperature and resistance. The Johnson–Nyquist law gives a Gaussian voltage of variance $\sigma_v^2 = 4k_B T R B$ across a resistor $R$ at temperature $T$ over bandwidth $B$ [<a href="#ref-petrie2000">Petrie2000</a>].</p>
<p><strong>Output.</strong> After gain $G$ and a comparator at threshold $V_{\text{th}}$ with input-referred offset $V_{\text{os}}$, the output bit is the sign of $(v - V_{\text{th}})$. With the threshold at the mean:</p>
<div class="ckp-eq">
  <span class="eq-label">Bit Probability — Eq. (7)</span>
  $$\Pr(b=1) = \Phi\left(\frac{-V_{\text{os}}}{G\sigma_v}\right) \approx \frac{1}{2} - \frac{V_{\text{os}}}{G\sigma_v \sqrt{2\pi}} \tag{7}$$
</div>
<p>so the bias is the offset measured in units of the amplified noise standard deviation. Successive samples are independent only if taken slower than the noise correlation time; for a one-pole front end of cutoff $f_c$, $\tau_c \approx 1/(2\pi f_c)$. Sampling at several $\tau_c$ yields a near-IID Bernoulli source of min-entropy $-\log_2 \max(p, 1-p)$. The synthetic source at $V_{\text{os}}/(G\sigma_v) = 0.15$ yields an MCV bound of 0.83 bit/sample, consistent with the closed form.</p>
<p><strong>Falsification.</strong> Verify the Gaussian shape of the pre-comparator distribution (Kolmogorov–Smirnov against $\mathcal{N}$), verify that $\sigma_v^2$ tracks $4k_B T R B$ as temperature is swept, and verify the exponential autocorrelation. Departure indicates amplifier saturation, $1/f$ contamination, or coupled deterministic interference — each of which the model explicitly forbids.</p>
<h3 id="sec-metastability">3.3 Metastability</h3>
<p><strong>Physics.</strong> A cross-coupled latch driven to its metastable point sits, in principle, on an unstable equilibrium between its two stable states; thermal noise breaks the tie. The differential voltage resolves as $\Delta V(t) = \Delta V_0 e^{t/\tau_{\text{reg}}}$, where $\tau_{\text{reg}}$ is the regeneration time constant and the initial imbalance $\Delta V_0 = V_{\text{off}} + n$ combines a deterministic offset and thermal noise $n \sim \mathcal{N}(0, \sigma_n^2)$ [<a href="#ref-tokunaga2008">Tokunaga2008</a>, <a href="#ref-vasyltsov2008">Vasyltsov2008</a>].</p>
<p>The offset $V_{\text{off}}$ is dominated by device mismatch from manufacturing variation, so this source is intrinsically process-dependent: nominally identical latches on the same die have different biases, and the offset drifts with voltage and temperature.</p>
<p><strong>Output.</strong> Reading the latch after a fixed window gives:</p>
<div class="ckp-eq">
  <span class="eq-label">Resolution Probability — Eq. (8)</span>
  $$\Pr(\text{out}=1) = \Phi\left(\frac{V_{\text{off}}}{\sigma_n}\right) \tag{8}$$
</div>
<p>maximised in entropy as $V_{\text{off}} \to 0$. Hysteresis and incomplete settling make the present output depend on the previous one, so the honest model is a two-state Markov chain rather than a Bernoulli source; the transition probabilities are the objects to estimate, and the SP 800-90B Markov estimator is the matched tool. A synthetic chain with $V_{\text{off}}/\sigma_n = 0.3$ and mild settling-induced correlation gives a Markov-estimator bound of 0.79 bit/sample, below the $\Phi(0.3)$ Bernoulli value — the dependence is real entropy loss the Bernoulli view would miss.</p>
<p><strong>Falsification.</strong> The model predicts that residual offset, hence bias, is cancellable by a calibration DAC, and that the unresolved-state rate falls as the window lengthens at rate $1/\tau_{\text{reg}}$. If bias persists after offset cancellation, or if the Markov dependence does not vanish as settling time grows, a deterministic coupling is present and the source is not yet an entropy source.</p>
<h3 id="sec-photon">3.4 Single-Photon Which-Path (Quantum)</h3>
<p><strong>Physics.</strong> A single photon at a balanced beam splitter is detected in one of two arms; the Born rule assigns probability $\tfrac{1}{2}$ to each and one bit of ideal entropy. Reality enters through unequal detection efficiencies $\eta_1 \neq \eta_2$, dark counts at rate $d$, dead time, and afterpulsing probability $a$. Commercial which-path QRNGs are built on exactly this principle; the ID Quantique Quantis family, for instance, has undergone certification under both AIS 31 and SP 800-90B, and such certifications rest on a vendor stochastic model of precisely these imperfections rather than on the ideal bit alone [<a href="#ref-idq">IDQ</a>].</p>
<p><strong>Output.</strong> Conditioned on a valid detection, the effective bias is, to first order:</p>
<div class="ckp-eq">
  <span class="eq-label">Effective Bias — Eq. (9)</span>
  $$\Pr(b=1) \approx \frac{\eta_1}{\eta_1 + \eta_2} + \text{(dark-count and afterpulsing corrections)} \tag{9}$$
</div>
<p>and inter-arrival times follow the Poisson statistics of the source rate $\mu$. The certifiable quantity is the conditional min-entropy of Eq. (2) with $E$ the classical imperfection parameters: a detector blinding or efficiency-mismatch attack is exactly an adversary exploiting $E$. The ideal bit is a ceiling; the floor is set by how tightly $\eta_1/\eta_2$, $d$ and $a$ are bounded and monitored.</p>
<p><strong>Falsification.</strong> Predict the bias from independently measured $\eta_1, \eta_2, d, a$; measure the realised bias; they must agree. Predict the exponential inter-arrival distribution; deviation signals afterpulsing or dead time outside the model.</p>
<h3 id="sec-homodyne">3.5 Vacuum-Fluctuation Homodyne (Quantum)</h3>
<p><strong>Physics.</strong> Homodyne detection of the vacuum quadrature against a strong local oscillator yields a measured value:</p>
<div class="ckp-eq">
  <span class="eq-label">Homodyne Measurement — Eq. (10)</span>
  $$M = Q_q + E_c, \quad Q_q \sim \mathcal{N}(0, \sigma_q^2), \quad E_c \sim \mathcal{N}(0, \sigma_e^2) \tag{10}$$
</div>
<p>where $\sigma_q^2$ is the shot-noise (vacuum) variance and $\sigma_e^2$ is classical electronic and excess noise [<a href="#ref-gabriel2010">Gabriel2010</a>, <a href="#ref-haw2015">Haw2015</a>].</p>
<p><strong>Output.</strong> After ADC discretisation with bin width $\delta$, the extractable randomness is the discretised conditional min-entropy $\tilde{H}_{\infty}(M_\delta \mid E_c)$, <em>not</em> the entropy of the total variance $\sigma_q^2 + \sigma_e^2$. Quoting the latter is the single most common over-statement in continuous-variable QRNG, because it credits the user with randomness the adversary controls through $E_c$.</p>
<div class="ckp-callout warn">
  <strong>The Homodyne Over-Statement</strong>
  <p>As the shot-noise clearance ratio $r = \sigma_q^2 / \sigma_e^2$ falls, the honest conditional min-entropy stays pinned near the value set by $\sigma_q$ (here $\approx 2.35$ bits/sample), while the naive total-variance figure inflates without bound — at $r = 1$ the over-statement is already about half a bit per sample, and at $r = \tfrac{1}{4}$ it exceeds a full bit. The clearance ratio is therefore not a performance number but a monitored security parameter.</p>
</div>
<p><strong>Falsification.</strong> Vary the local-oscillator power: $\sigma_q^2$ must scale linearly with it (shot noise) while $\sigma_e^2$ must not. If the "quantum" variance does not track the local oscillator, it is not quantum, and the conditional min-entropy claim collapses.</p>
</section>
<div class="ckp-sep">Measurement Discipline</div>
<!-- ─── SECTION 4 ─────────────────────────────────────────── -->
<section id="sec-measurement">
<h2>4. Measurement, Estimation, and Model-Bound Health Tests</h2>
<h3>4.1 Measure the Raw Source, Before Conditioning</h3>
<p>The cardinal rule is procedural: tap the digitiser output upstream of any hash or von Neumann corrector. A conditioner whitens everything, including failure, so measuring after it measures the conditioner, not the source. What you may not do is apply a von Neumann corrector, an XOR combiner, an LFSR, or a hash before estimating and then credit the cleaned-up statistics. Those are conditioning steps. They are permitted in the data path, but they live downstream of the measurement point, they cannot increase min-entropy ($H_{\infty}(f(X)) \leq H_{\infty}(X)$), and SP 800-90B caps the entropy creditable at the output of a non-vetted conditioner accordingly.</p>
<div class="ckp-callout key">
  <strong>Golden Rule</strong>
  <p>Debiasing is allowed, but it is never free and never measured as if it were the source. Log at least $10^6$ raw samples per operating corner (nominal, hot, cold, low-voltage, high-voltage), with timestamping for jitter sources and ADC capture at $\geq 10\times$ the noise bandwidth for thermal sources.</p>
</div>
<h3>4.2 Estimate Min-Entropy with the Non-IID Track</h3>
<p>Do not assume independence. Run the SP 800-90B IID permutation tests; if IID is not credibly established, take the non-IID route and report the minimum over the ten min-entropy estimators: most-common-value, collision, Markov, compression, t-tuple, longest repeated substring, and the MultiMCW / Lag / MultiMMC / LZ78Y predictors.</p>
<div class="ckp-callout">
  <strong>Reading the Dominating Estimator</strong>
  <p>Document which estimator dominates, because the dominating estimator names the structure the source is leaking. If the Markov estimator gives the minimum, the source has first-order serial dependence — the metastability latch with incomplete settling is the textbook case. If a predictor (LZ78Y, MultiMMC) dominates, the source has longer-range or periodic structure — injection locking on a jitter source shows up here. If the most-common-value estimator dominates, the source is essentially memoryless and merely biased.</p>
</div>
<h3>4.3 Tie Every Health Test to a Model Parameter</h3>
<p>The two SP 800-90B continuous tests are mandatory, and their thresholds are not free parameters: they are computed from the claimed min-entropy $\hat{H}$ and a false-alarm probability $\alpha$ (commonly $2^{-20}$):</p>
<div class="ckp-eq">
  <span class="eq-label">Repetition-Count Cutoff — Eq. (11)</span>
  $$C = 1 + \left\lceil \frac{-\log_2 \alpha}{\hat{H}} \right\rceil \tag{11}$$
</div>
<div class="ckp-eq">
  <span class="eq-label">Adaptive-Proportion Cutoff — Eq. (12)</span>
  $$\text{cutoff} = \min\left\{ c : \Pr[\text{Bin}(W, 2^{-\hat{H}}) \geq c] \leq \alpha \right\} \tag{12}$$
</div>
<p>with window $W \in \{512, 1024\}$. These catch catastrophic collapse — a stuck source, a totally biased one. They do not catch a source that has quietly drifted from 0.9 to 0.6 bits while still looking noisy, and that slow drift is the failure mode that actually occurs in the field as a device ages or warms.</p>
<p>The fix is to add, for each source, a direct online estimator of the very parameter $\theta$ that the model says governs entropy:</p>
<ul class="ckp-hier">
  <li><strong>Oscillator jitter:</strong> a sliding-window estimator of period variance, tracking $Q$; alarm when $Q$ falls below the value at which $H_{\infty}$ meets the claim. This also catches injection locking, which collapses $Q$ abruptly.</li>
  <li><strong>Amplified thermal:</strong> a DC-offset / bias-drift monitor and an amplifier-saturation detector — the two ways $\Pr(b=1)$ leaves its modelled band.</li>
  <li><strong>Metastability:</strong> the unresolved-state rate and the estimated Markov transition asymmetry.</li>
  <li><strong>Photon which-path:</strong> count-rate bounds, dead-time and afterpulsing monitors, and a continuous efficiency-mismatch check.</li>
  <li><strong>Vacuum homodyne:</strong> the shot-noise clearance ratio $\sigma_q^2 / \sigma_e^2$, alarmed against the value that keeps $\tilde{H}_{\infty}(M_\delta \mid E_c)$ above the claim.</li>
</ul>
<h3>4.4 Prove Effectiveness by Injecting the Failures You Fear</h3>
<p>A health test you have not tried to fool is decoration. The effectiveness obligation — explicit in AIS 31 — is met by adversarial fault injection: supply droop, electromagnetic injection, thermal shock, local-oscillator manipulation for the homodyne source, controlled illumination for the single-photon source.</p>
<div class="ckp-callout warn">
  <strong>Latency Bound</strong>
  <p>The acceptance criterion is a latency statement: for each fault, the relevant test must alarm before the measured min-entropy crosses below $\hat{H}$, and the number of below-claim outputs emitted between entropy collapse and alarm must be quantified and bounded. An entropy claim without a detection-latency bound is a statement about the past, not a guarantee about the next sample.</p>
</div>
</section>
<div class="ckp-sep">Side-Channel Defence</div>
<!-- ─── SECTION 5 ─────────────────────────────────────────── -->
<section id="sec-leakage">
<h2>5. Leakage: Unpredictability Must Also Be Confidential</h2>
<p>The conditional min-entropy $\tilde{H}_{\infty}(X \mid E)$ is only as honest as the side information $E$ it conditions on. If a physical side channel hands the adversary information the model omitted from $E$, the true conditional min-entropy is lower than the certified one, and every downstream guarantee silently fails. Leakage is therefore not a separate concern bolted onto entropy estimation; it is the question of whether the $E$ in the bound is complete.</p>
<div class="ckp-pull">
  <p>Leaking a key bit costs one bit; leaking the state of the noise source can collapse the entropy of every subsequent output, because the adversary who learns the oscillator phase, the comparator's instantaneous input, or the local-oscillator amplitude can predict samples rather than merely recover one secret.</p>
  <cite>&mdash; Why leakage is a first-class entropy obligation</cite>
</div>
<p>Power and electromagnetic emanations carry exactly these quantities: the switching of the sampling logic, the comparator decision, and the ADC conversion are all correlated with the raw sample, and modern EM probes and template attacks recover such correlations at fine spatial resolution. Worse, several of the injection faults of the previous section are also side channels run in reverse: frequency injection into a ring-oscillator TRNG can both reduce its entropy and synchronise it to the attacker's reference, and contactless electromagnetic injection has been demonstrated against oscillator-based sources [<a href="#ref-markettos2009">Markettos2009</a>, <a href="#ref-bayon2012">Bayon2012</a>].</p>
<div class="ckp-callout key">
  <strong>Leakage Containment Obligations</strong>
  <p>An entropy-source design that takes the fifth obligation seriously should: (i) place the noise source and its first amplifier inside the same shielding and power-conditioning boundary as the conditioner; (ii) treat the sampling-clock and conversion events as leakage sources and decorrelate or mask them; (iii) include, where the threat model warrants, a decoy or masking source whose emanations are indistinguishable from the live source; and (iv) extend the fault-injection campaign to emission measurement, verifying that the recoverable mutual information between an external probe and the raw sample is below a stated bound.</p>
</div>
<p>The leakage budget is then reported alongside the entropy budget, and the conditional min-entropy claim is annotated with the $E$ it assumed. <strong>A claim that does not state its $E$ is not yet a claim.</strong></p>
</section>
<div class="ckp-sep">Conditioning</div>
<!-- ─── SECTION 6 ─────────────────────────────────────────── -->
<section id="sec-conditioning">
<h2>6. Conditioning and Entropy Accounting</h2>
<h3>6.1 The Conditioner</h3>
<p>The Leftover Hash Lemma (Eq. 3) establishes, unconditionally, that a conditioner's output min-entropy is bounded by its input min-entropy minus a security margin — but only for the universal-hash-with-public-seed construction. The cryptographic standards substitute vetted conditioning components — hash derivation functions over SHA-2 or SHA-3, HMAC, AES in CMAC or CBC-MAC mode — whose entropy-preservation rests on a computational assumption rather than on LHL's proof.</p>
<p>For a vetted component producing $n_{\text{out}}$ bits of full entropy, SP 800-90B and SP 800-90C [<a href="#ref-barker2025">Barker2025</a>] require the input min-entropy to satisfy:</p>
<div class="ckp-eq">
  <span class="eq-label">NIST Conditioning Rule — Eq. (13)</span>
  $$h_{\text{in}} \geq n_{\text{out}} + 64 \tag{13}$$
</div>
<p>The $n_{\text{out}} + 64$ rule applies to the security strength being targeted, not to the conditioner's native output width: $n_{\text{out}}$ is the number of full-entropy bits the system actually needs. For a system that asks SHA-256 to deliver a full-entropy 256-bit block, $n_{\text{out}} = 256$ and $h_{\text{in}} \geq 320$ follows directly.</p>
<div class="ckp-callout">
  <strong>Arithmetic Note</strong>
  <p>Min-entropy bits are not raw bits. If the raw source delivers $\rho$ bits of min-entropy per raw bit, obtaining 320 min-entropy bits requires $\lceil 320 / \rho \rceil$ raw bits — e.g. 534 raw bits at $\rho = 0.6$, or 640 at $\rho = 0.5$.</p>
</div>
<h3>6.2 Worked Accounting</h3>
<div class="ckp-table-wrap">
  <table class="ckp-table">
    <thead>
      <tr>
        <th>Source (conservative $\rho$)</th>
        <th>$\rho$</th>
        <th>$n_{\text{out}}$</th>
        <th>Req. $h_{\text{in}}$</th>
        <th>Raw Bits</th>
        <th>Conditioner</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td class="term">Oscillator jitter</td>
        <td>0.50</td>
        <td>256</td>
        <td>320</td>
        <td>640</td>
        <td>SHA-256_df</td>
      </tr>
      <tr>
        <td class="term">Amplified thermal</td>
        <td>0.80</td>
        <td>256</td>
        <td>320</td>
        <td>400</td>
        <td>SHA-256_df</td>
      </tr>
      <tr>
        <td class="term">Metastability</td>
        <td>0.60</td>
        <td>256</td>
        <td>320</td>
        <td>534</td>
        <td>SHA-256_df</td>
      </tr>
      <tr>
        <td class="term">Vacuum homodyne</td>
        <td>0.95</td>
        <td>256</td>
        <td>320</td>
        <td>337</td>
        <td>SHA-256_df</td>
      </tr>
    </tbody>
  </table>
</div>
<p>The per-bit $\rho$ values shown are conservative design targets; the nominal-corner synthetic estimates of Section 3 (0.99 jitter, 0.83 thermal, 0.79 metastability, and a multi-bit homodyne sample) sit above them, which is the margin a real design should carry between its certified floor and its typical operating point.</p>
<h3>6.3 Stateful Entropy Pools</h3>
<p>A real generator does not consume raw bits at the rate applications request output. The standard resolution is a stateful pool sitting between them. Two regimes must be kept distinct.</p>
<p><strong>Information-theoretic regime</strong> — a pool that is itself the entropy reservoir, with no cryptographic generator after it — entropy is a conserved, additive quantity. The pool must accumulate at least $n_{\text{out}} + 64$ min-entropy bits before releasing any output, must debit the entropy it spends on each draw, and must block when its accounted entropy is insufficient.</p>
<p><strong>Computational regime</strong> — the SP 800-90C RBG2 and RBG3 constructions — the pool seeds a DRBG built from a vetted mechanism, and the security argument shifts from information-theoretic to computational. Here a single seeding with enough min-entropy ($\geq n_{\text{out}} + 64$) licenses the DRBG to produce many output blocks. What one must do is reseed before the DRBG's reseed interval and after any health-test alarm.</p>
<h3>6.4 Implementation Hygiene</h3>
<ul class="ckp-hier">
  <li><strong>Separate clock domains.</strong> Separate the entropy-source and conditioner clock domains, so the conditioner cannot lock to and launder a source artefact.</li>
  <li><strong>Zeroise intermediates.</strong> Zeroise intermediate buffers, so a fault does not leak partially-conditioned state.</li>
  <li><strong>Test the conditioner input.</strong> Run the continuous health tests on the conditioner input, not merely its output: testing the output tests the hash, which is precisely the component designed to hide the failure you are trying to catch.</li>
</ul>
</section>
<div class="ckp-sep">The Quantum Question</div>
<!-- ─── SECTION 7 ─────────────────────────────────────────── -->
<section id="sec-quantum">
<h2>7. The Quantum Case</h2>
<p>We single out the quantum case because it is where the word <em>quantum</em> does the most rhetorical work relative to its logical content, and because several distinct questions are routinely conflated. We separate them.</p>
<h3>Does a QRNG Carry a Real Advantage?</h3>
<p><strong>Yes.</strong> Its ideal model has a first-principles entropy that is a consequence of quantum measurement rather than an estimate of a complicated classical process. That advantage is genuine and worth paying for. But it is an advantage in the <em>ceiling</em>; the security parameter is the <em>floor</em>, and the floor is classical. The single-photon device leaks through detector imperfections; the homodyne device leaks through classical excess noise. In both, the certifiable output is the conditional min-entropy of Eq. (2), and a credible QRNG measures and monitors its classical side channel with the same rigour a classical TRNG applies to jitter or offset.</p>
<h3>Do Quantum Computers Threaten Hardware RNGs?</h3>
<p><strong>Not at the entropy-source layer.</strong> A quantum computer attacks the hard-problem assumptions behind public-key cryptography and, via Grover, halves the effective key length of symmetric primitives; it does not predict a well-characterised physical entropy source, whose security is information-theoretic at the raw layer and does not rest on a computational assumption. The post-quantum transition is a story about algorithms downstream of the RBG, not about the noise source. The one caveat is the conditioner: a hash or block cipher used for conditioning should retain adequate security under Grover, which the standard 256-bit choices already do.</p>
<h3>Do Quantum Sensors Make Sources More Predictable?</h3>
<p>This is the more interesting threat. Improved quantum-limited sensing lowers the cost of measuring the very classical quantities that constitute $E$ — the local-oscillator phase, a detector's afterpulsing, a faint emanation — and so can enlarge the adversary's side information against a source whose leakage budget was set against weaker instruments. This is a leakage question (Section 5), and it is an argument for stating the assumed measurement capability of the adversary in the model.</p>
<div class="ckp-pull">
  <p>The discriminating question to ask any QRNG vendor is not "is it quantum?" but "what is your conditional min-entropy given your own classical noise, which online test holds it, and what adversary measurement capability did your leakage budget assume?"</p>
  <cite>&mdash; The practical QRNG evaluation criterion</cite>
</div>
<p>A well-understood, transparently certified classical TRNG with a defended conditional min-entropy bound is preferable to an opaque QRNG that ships the ideal bit; an opaque QRNG is preferable to nothing only if one trusts the vendor's unstated model, which is exactly the trust this paper argues against extending. <strong>Transparency of the model is not a marketing nicety; under the definition of Section 2.4 it is what "certified" means.</strong></p>
</section>
<div class="ckp-sep">Conclusion</div>
<!-- ─── SECTION 8 ─────────────────────────────────────────── -->
<section id="sec-conclusion">
<h2>8. Conclusion</h2>
<p class="drop-cap">The community has the right standards and, sometimes, the wrong emphasis. The model, the health test, the leakage budget and the entropy accounting are routinely treated as compliance burden laid over a source that is "obviously random." The order of dependence is the reverse: those four are the only content the word <em>random</em> has in a cryptographic setting, and the source is nothing without them.</p>
<div class="ckp-pull">
  <p>Unpredictability is necessary, and — once written as a proven, monitored, leak-contained lower bound on conditional min-entropy — it is also sufficient, because at that point the Leftover Hash Lemma supplies the rest for free.</p>
  <cite>&mdash; The complete chain</cite>
</div>
<p>The error worth eradicating is the belief that the conditioner can rescue a source the model never characterised. It cannot: a hash function is an excellent way to hide that one does not know how much entropy one has, and a poor way to obtain any.</p>
</section>
<div class="ckp-sep">Reference</div>
<!-- ─── GLOSSARY ─────────────────────────────────────────── -->
<section id="sec-glossary">
<h2>Quick Reference Glossary</h2>
<div class="ckp-table-wrap">
  <table class="ckp-table">
    <thead>
      <tr>
        <th>Term</th>
        <th>Meaning</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td class="term">Min-Entropy $H_{\infty}$</td>
        <td>Worst-case entropy: $-\log_2$ of the maximum outcome probability. The adversary's optimal single guess determines the security of a key drawn from the source.</td>
      </tr>
      <tr>
        <td class="term">Conditional Min-Entropy $\tilde{H}_{\infty}(X \mid E)$</td>
        <td>Average min-entropy of $X$ given side information $E$ available to the adversary. The certifiable object for any entropy source.</td>
      </tr>
      <tr>
        <td class="term">Stochastic Model $p(x \mid \theta)$</td>
        <td>A probability distribution for raw source outputs, derived from device physics, with parameter vector $\theta$ tied to measurable quantities.</td>
      </tr>
      <tr>
        <td class="term">Raw Data</td>
        <td>Digitised noise-source samples measured upstream of any conditioner, hash, corrector, or debiasing step.</td>
      </tr>
      <tr>
        <td class="term">Conditioner</td>
        <td>A deterministic function (hash_df, HMAC, CMAC) that compresses raw samples into a shorter, near-uniform output. Cannot create entropy; can only concentrate existing entropy.</td>
      </tr>
      <tr>
        <td class="term">Health Test</td>
        <td>An online statistical test whose threshold is computed from model parameters, designed to alarm when the source leaves its certified operating envelope.</td>
      </tr>
      <tr>
        <td class="term">Leftover Hash Lemma (LHL)</td>
        <td>Information-theoretic result: a universal hash can extract $m$ near-uniform bits from a source of min-entropy $k$ provided $m \leq k - 2\log_2(1/\varepsilon)$.</td>
      </tr>
      <tr>
        <td class="term">Jitter Quality Factor $Q$</td>
        <td>Normalised accumulated phase variance $\sigma_{\text{acc}}^2 / T_0^2$; the single parameter governing entropy in a ring-oscillator jitter source.</td>
      </tr>
      <tr>
        <td class="term">Shot-Noise Clearance Ratio $r$</td>
        <td>Ratio $\sigma_q^2 / \sigma_e^2$ of quantum to classical variance in a homodyne QRNG. A security parameter, not a performance metric.</td>
      </tr>
      <tr>
        <td class="term">SP 800-90B Non-IID Track</td>
        <td>NIST procedure for estimating min-entropy on samples that may have serial dependence, taking the minimum over ten distinct estimators.</td>
      </tr>
      <tr>
        <td class="term">AIS 31 PTG.3</td>
        <td>BSI's highest entropy-source class, requiring an explicit stochastic model with validated parameters and model-bound online tests.</td>
      </tr>
    </tbody>
  </table>
</div>
</section>
<!-- ─── REFERENCES ─────────────────────────────────────────── -->
<section id="references" class="ckp-refs">
<h2>References</h2>
<p><span class="ref-num">[Turan2018]</span> M. S. Turan, E. Barker, J. Kelsey, K. A. McKay, M. L. Baish, M. Boyle. <em>Recommendation for the Entropy Sources Used for Random Bit Generation.</em> NIST Special Publication 800-90B (2018).</p>
<p><span class="ref-num">[Barker2015]</span> E. Barker, J. Kelsey. <em>Recommendation for Random Number Generation Using Deterministic Random Bit Generators.</em> NIST SP 800-90A Rev. 1 (2015).</p>
<p><span class="ref-num">[Barker2025]</span> E. Barker, J. Kelsey, K. A. McKay, A. Roginsky, M. S. Turan. <em>Recommendation for Random Bit Generator (RBG) Constructions.</em> NIST SP 800-90C (final, 2025).</p>
<p><span class="ref-num">[Killmann2011]</span> W. Killmann, W. Schindler. <em>A Proposal for: Functionality Classes for Random Number Generators, Version 2.0.</em> BSI AIS 20/AIS 31 (2011).</p>
<p><span class="ref-num">[Peter2024]</span> M. Peter, W. Schindler. <em>A Proposal for: Functionality Classes for Random Number Generators, Version 3.0.</em> BSI mathematical-technical reference for AIS 20/AIS 31 (Sept. 2024).</p>
<p><span class="ref-num">[Schindler2023]</span> W. Schindler. <em>Overview of AIS 20/31.</em> NIST RNG workshop presentation (2023).</p>
<p><span class="ref-num">[Shumow2007]</span> D. Shumow, N. Ferguson. <em>On the Possibility of a Back Door in the NIST SP 800-90 Dual_EC_DRBG.</em> CRYPTO 2007 Rump Session (2007).</p>
<p><span class="ref-num">[Bernstein2016]</span> D. J. Bernstein, T. Lange, R. Niederhagen. <em>Dual EC: A Standardized Back Door.</em> LNCS 9100, pp. 256–281. Springer (2016).</p>
<p><span class="ref-num">[Impagliazzo1989]</span> R. Impagliazzo, L. A. Levin, M. Luby. <em>Pseudo-random Generation from One-way Functions.</em> STOC 1989, pp. 12–24. ACM (1989).</p>
<p><span class="ref-num">[Dodis2008]</span> Y. Dodis, R. Ostrovsky, L. Reyzin, A. Smith. <em>Fuzzy Extractors: How to Generate Strong Keys from Biometrics and Other Noisy Data.</em> SIAM J. Comput. 38(1), 97–139 (2008).</p>
<p><span class="ref-num">[Baudet2011]</span> M. Baudet, D. Lubicz, J. Micolod, A. Tassiaux. <em>On the Security of Oscillator-Based Random Number Generators.</em> J. Cryptology 24(2), 398–425 (2011).</p>
<p><span class="ref-num">[Killmann2008]</span> W. Killmann, W. Schindler. <em>A Design for a Physical RNG with Robust Entropy Estimators.</em> CHES 2008, LNCS 5154, pp. 146–163. Springer (2008).</p>
<p><span class="ref-num">[Kohlbrenner2004]</span> P. Kohlbrenner, K. Gaj. <em>An Embedded True Random Number Generator for FPGAs.</em> FPGA 2004, pp. 71–78. ACM (2004).</p>
<p><span class="ref-num">[Bucci2003]</span> M. Bucci, L. Germani, R. Luzzi, A. Trifiletti, M. Varanonuovo. <em>A High-Speed Oscillator-Based Truly Random Number Source for Cryptographic Applications on a Smart Card IC.</em> IEEE Trans. Computers 52(4), 403–409 (2003).</p>
<p><span class="ref-num">[Petrie2000]</span> C. S. Petrie, J. A. Connelly. <em>A Noise-Based IC Random Number Generator for Applications in Cryptography.</em> IEEE Trans. Circuits and Systems I 47(5), 615–621 (2000).</p>
<p><span class="ref-num">[Tokunaga2008]</span> C. Tokunaga, D. Blaauw, T. Mudge. <em>True Random Number Generator with a Metastability-Based Quality Control.</em> IEEE J. Solid-State Circuits 43(1), 78–85 (2008).</p>
<p><span class="ref-num">[Vasyltsov2008]</span> I. Vasyltsov, E. Hambardzumyan, Y.-S. Kim, B. Karpinskyy. <em>Fast Digital TRNG Based on Metastable Ring Oscillator.</em> CHES 2008, LNCS 5154, pp. 164–180. Springer (2008).</p>
<p><span class="ref-num">[Markettos2009]</span> A. T. Markettos, S. W. Moore. <em>The Frequency Injection Attack on Ring-Oscillator-Based True Random Number Generators.</em> CHES 2009, LNCS 5747, pp. 317–331. Springer (2009).</p>
<p><span class="ref-num">[Bayon2012]</span> P. Bayon, L. Bossuet, A. Aubert, V. Fischer, F. Poucheret, B. Robisson, P. Maurine. <em>Contactless Electromagnetic Active Attack on Ring Oscillator Based True Random Number Generator.</em> COSADE 2012, LNCS 7275, pp. 151–166. Springer (2012).</p>
<p><span class="ref-num">[Dodis2013]</span> Y. Dodis, D. Pointcheval, S. Ruhault, D. Vergnaud, D. Wichs. <em>Security Analysis of Pseudorandom Number Generators with Input: /dev/random is Not Robust.</em> ACM CCS 2013, pp. 647–658. ACM (2013).</p>
<p><span class="ref-num">[Ferguson2010]</span> N. Ferguson, B. Schneier, T. Kohno. <em>Cryptography Engineering.</em> Wiley (2010).</p>
<p><span class="ref-num">[FIPS140-3]</span> NIST. <em>Security Requirements for Cryptographic Modules.</em> FIPS PUB 140-3 (2019).</p>
<p><span class="ref-num">[SP800-140F]</span> NIST. <em>CMVP Approved Non-Invasive Attack Mitigation Test Metrics.</em> SP 800-140F.</p>
<p><span class="ref-num">[Herrero2017]</span> M. Herrero-Collantes, J. C. Garcia-Escartin. <em>Quantum Random Number Generators.</em> Reviews of Modern Physics 89, 015004 (2017).</p>
<p><span class="ref-num">[Ma2016]</span> X. Ma, X. Yuan, Z. Cao, B. Qi, Z. Zhang. <em>Quantum Random Number Generation.</em> npj Quantum Information 2, 16021 (2016).</p>
<p><span class="ref-num">[Gabriel2010]</span> C. Gabriel, C. Wittmann, D. Sych, R. Dong, W. Mauerer, U. L. Andersen, C. Marquardt, G. Leuchs. <em>A Generator for Unique Quantum Random Numbers Based on Vacuum States.</em> Nature Photonics 4, 711–715 (2010).</p>
<p><span class="ref-num">[Haw2015]</span> J. Y. Haw, S. M. Assad, A. M. Lance, N. H. Y. Ng, V. Sharma, P. K. Lam, T. Symul. <em>Maximization of Extractable Randomness in a Quantum Random-Number Generator.</em> Physical Review Applied 3, 054004 (2015).</p>
<p><span class="ref-num">[IDQ]</span> ID Quantique. <em>Quantis QRNG — AIS 31 / SP 800-90B Certification and Stochastic-Model Documentation.</em> Vendor certification documentation.</p>
<p><span class="ref-num">[Stipcevic2014]</span> M. Stipčević, Ç. K. Koç. <em>True Random Number Generators.</em> Open Problems in Mathematics and Computational Science, pp. 275–315. Springer (2014).</p>
</section>
</div><!-- end ckp-body -->
</div><!-- end ckp-layout -->
</article>
<script>
// Mobile TOC toggle
(function() {
  var toggle = document.getElementById('ckp-mob-toc-toggle');
  var list = document.getElementById('ckp-mob-toc-list');
  if (toggle && list) {
    toggle.addEventListener('click', function() {
      list.style.display = list.style.display === 'block' ? 'none' : 'block';
    });
  }

  // Scroll progress bar
  var bar = document.getElementById('ckp-progress');
  if (bar) {
    window.addEventListener('scroll', function() {
      var scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
      var scrollHeight = document.documentElement.scrollHeight - document.documentElement.clientHeight;
      var pct = scrollHeight > 0 ? (scrollTop / scrollHeight) * 100 : 0;
      bar.style.width = pct + '%';
    });
  }
})();
</script>