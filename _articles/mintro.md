---
layout: post
title: "No Entropy Without a Model"
math: true
---

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
  <div class="ckp-kicker">Applied Cryptography · Entropy Sources · True & Quantum RNGs</div>
  <h1>No Entropy Without a <em>Model</em></h1>
  <p class="ckp-deck">Why "it looks random" is never enough — and what it actually takes to prove that the numbers guarding your secrets are unpredictable to the one person trying to guess them.</p>
  <div class="ckp-meta">
    <span>Applied Cryptography Series</span>
    <span class="dot"></span>
    <span>PakCrypt · 2026</span>
    <span class="dot"></span>
    <span>~22 min read</span>
    <span class="dot"></span>
    <span>A popular-science companion</span>
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
  <span>Contents</span><span>▾</span>
</div>
<div class="ckp-mobile-toc-list" id="ckp-mob-toc-list">
  <a href="#abstract">Abstract</a>
  <a href="#sec-error">1. The Number That Looks Random</a>
  <a href="#sec-entropy">2. Entropy Is About the Adversary</a>
  <a href="#sec-hash">3. A Hash Cannot Make Entropy</a>
  <a href="#sec-model">4. Why You Need a Model</a>
  <a href="#sec-sources">5. Five Sources, Five Models</a>
  <a href="#sec-monitor">6. Measure, Monitor, Margin</a>
  <a href="#sec-leakage">7. The Side Door</a>
  <a href="#sec-quantum">8. The Quantum Question</a>
  <a href="#sec-chain">9. The Whole Chain</a>
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
  <p>Hardware and quantum random number generators are usually justified the same way: the physics is unpredictable, the output passes a battery of statistical tests, so the numbers must be good. This article argues that the justification is missing the only thing that matters. Unpredictability is not a property of a string of bits — it is a property of how little an attacker knows. The honest object to defend is a proven lower bound on the source's <em>conditional min-entropy</em>: a number derived from a physical model, kept true while the device runs by health tests tied to that model, protected from side channels that would quietly hand the attacker the very uncertainty you are counting on, and only then squeezed by a conditioner that spends entropy honestly. A hash cannot manufacture randomness a model never proved. This is the discipline, told for a general technical reader.</p>
</div>

<!-- STATS BAR -->
<div class="ckp-stat-row">
  <div class="ckp-stat"><span class="stat-num">5</span><span class="stat-label">Physical source classes modeled from first principles</span></div>
  <div class="ckp-stat"><span class="stat-num">2007</span><span class="stat-label">Year a "random" generator was shown to have a backdoor</span></div>
  <div class="ckp-stat"><span class="stat-num">0.15</span><span class="stat-label">Bits left in a "fair" coin an attacker can peek at</span></div>
  <div class="ckp-stat"><span class="stat-num">+64</span><span class="stat-label">The honest conditioning safety margin, in bits</span></div>
</div>

<!-- ─── SECTION 1 ─────────────────────────────────────────── -->
<section id="sec-error">
<h2>1. The Number That Looks Random</h2>

<p class="drop-cap">A random number generator that merely <em>looks</em> unpredictable offers a cryptographer almost nothing — because essentially every broken generator in history looked unpredictable right up until it was broken. The most famous example has a name that still makes engineers wince: <strong>Dual_EC_DRBG</strong>.</p>

<p>Dual_EC was a standardised generator. It shipped by default in widely deployed software. It sailed through the standard statistical test batteries without a single complaint. And in 2007, Dan Shumow and Niels Ferguson showed that anyone who knew a secret mathematical relationship between two fixed numbers baked into the design could watch a short run of its output and then predict everything it would ever produce afterwards [<a href="#ref-Shumow2007">Shumow2007</a>, <a href="#ref-Bernstein2016">Bernstein2016</a>]. To everyone without that secret, the output was indistinguishable from noise. To the one person holding it, the generator was an open book.</p>

<div class="ckp-callout warn">
  <strong>"Passes the tests" and "is unpredictable" are different properties</strong>
  <p>Here is a generator with zero randomness that defeats every statistical test you can throw at it: take a simple counter — 1, 2, 3, 4, … — and encrypt each value under AES with a secret key. The output is uniform, has no detectable bias, and passes the whole NIST and Dieharder suites. Yet to anyone who knows the key, the next output is fully determined. Counting is not randomness, no matter how convincing the disguise.</p>
</div>

<p>A purely innocent example makes the same point without any villain. The <strong>Mersenne Twister</strong> is a widely used pseudo-random generator that passes most of the standard test suites. But once an observer has seen 624 consecutive outputs, its entire future is fixed forever. The tests never noticed; the structure was always there.</p>

<p>So what <em>is</em> randomness, if it is not a visible feature of the bits coming out of a box? It is a gap — the gap between what the attacker knows and what the attacker would need to know to predict your next number. Building an entropy source is the discipline of measuring that gap from below, and of keeping it open while the device runs, through heat, ageing, and a determined adversary. Everything in this article follows from taking that one sentence literally.</p>

<div class="ckp-pull">
  <p>Randomness is not a property of the output. It is the size of the attacker's blind spot — and a security argument has to prove that blind spot is large.</p>
  <cite>— The thesis in one sentence</cite>
</div>

<p>The bad argument we want to retire goes like this: <em>the source is physically unpredictable; a hash compresses it; the compressed stream passes the tests; therefore it has full entropy.</em> Every step is either a non-sequitur or false. "Physically unpredictable" means nothing until a model attaches an actual number to it. Compression can only ever preserve or destroy randomness — never create it. And a passing test battery detects gross structure while certifying nothing about how much an informed attacker already knows. In place of <em>"unpredictable, compressed, and tested,"</em> this article offers five words: <strong>modeled, measured, monitored, margined, and shielded.</strong></p>
</section>

<div class="ckp-sep">The Right Quantity</div>

<!-- ─── SECTION 2 ─────────────────────────────────────────── -->
<section id="sec-entropy">
<h2>2. Entropy Is About the Adversary, Not the Bits</h2>

<p>Cryptographers almost never use the "entropy" most people learned in school. The familiar one — <em>Shannon entropy</em> — measures average surprise. That is the wrong average for a secret key, because an attacker does not guess your key on average. They guess it once, with their single best guess. The right quantity is the worst case, called <strong>min-entropy</strong>.</p>

<div class="ckp-eq">
  <span class="eq-label">Min-Entropy — Eq. (1)</span>
  $$H_\infty(X) = -\log_2 \max_i p_i \tag{1}$$
</div>

<p>In words: find the single most likely outcome, take its probability, and that probability alone sets the score. Nothing else about the distribution matters, because the attacker will simply guess that most likely outcome first.</p>

<h3>Why the worst case is the only case</h3>

<p>Picture a source with 129 possible symbols. Half the time it emits one fixed symbol; the other half of the time it spreads its output evenly over the remaining 128. Its Shannon entropy works out to a comfortable-sounding 4.5 bits. Its min-entropy is exactly 1 bit — because an attacker who always guesses that one fixed symbol is right half the time. A key drawn from this source is cracked on the very first guess with probability one-half. Shannon entropy is blind to that fact. Min-entropy reports it exactly. This is why cryptographic accounting is always a worst-case, lower-bound discipline.</p>

<h3>Now let the attacker look over your shoulder</h3>

<p>Real sources are not sealed in a vault, and the attacker is not blind. They may see the power-supply ripple, the electronic noise, the temperature — any side information the device leaks or the attacker can nudge. Call everything the attacker can see or control $E$. The honest object is then the <strong>conditional min-entropy</strong>: how unpredictable the output still is <em>after</em> the attacker has seen $E$.</p>

<div class="ckp-eq">
  <span class="eq-label">Conditional Min-Entropy — Eq. (2)</span>
  $$\widetilde{H}_\infty(X \mid E) = -\log_2 \; \mathbb{E}_{e \leftarrow E}\Big[\max_x \Pr(X = x \mid E = e)\Big] \tag{2}$$
</div>

<p>The formula looks heavy but says something simple. The inner part is the attacker's best guess once they have seen a particular slice of side information. The expectation averages their success over all the side information they will actually encounter. The logarithm turns that success rate into bits.</p>

<div class="ckp-callout">
  <strong>A coin that is worth almost nothing</strong>
  <p>Suppose $X$ is a perfectly fair bit — one full bit of entropy in isolation. But a cheap sensor leaks a related value $E$ that happens to agree with $X$ ninety percent of the time. An attacker who reads $E$ and simply guesses that $X$ matches it is right 90% of the time. The "fair" coin is now worth only about <strong>0.15 bits</strong> to that attacker. It still looks flawlessly random to anyone watching $X$ alone. It is nearly worthless to anyone who can also see $E$.</p>
</div>

<p>This is exactly why a vacuum-fluctuation quantum generator cannot simply quote the variance of its measured signal as "entropy." Part of that variance is ordinary classical noise the attacker is allowed to know. The randomness you actually get to keep is whatever survives once you condition on $E$ — never the whole thing.</p>
</section>

<div class="ckp-sep">The Price of Squeezing</div>

<!-- ─── SECTION 3 ─────────────────────────────────────────── -->
<section id="sec-hash">
<h2>3. A Hash Cannot Make Entropy</h2>

<p>Raw physical noise is rarely clean. It is biased, correlated, lumpy. So designers run it through a <em>conditioner</em> — a hash function, an XOR mixer, a von Neumann corrector — to produce a short, smooth, near-uniform output. It is tempting to believe this step manufactures quality. It does not. A conditioner can only ever <em>concentrate</em> randomness that was already there.</p>

<p>The mathematical reason is a one-line fact called the data-processing inequality: any deterministic function of $X$ can have at most as much min-entropy as $X$ itself, written $H_\infty(f(X)) \le H_\infty(X)$. Any strategy for guessing the squeezed output gives you an at-least-as-good strategy for guessing the input. Squeezing a sponge that is only a quarter full of water does not give you more water.</p>

<h3>The Leftover Hash Lemma — and what it actually costs</h3>

<p>The tool that prices the squeeze is the <strong>Leftover Hash Lemma</strong>. Feed a source carrying $k$ bits of (conditional) min-entropy into the right kind of hash family with a public random seed, and you can extract an output that is within a tiny distance $\varepsilon$ of perfectly uniform — provided you do not ask for too much:</p>

<div class="ckp-eq">
  <span class="eq-label">Leftover Hash Lemma — Eq. (3)</span>
  $$m \le k - 2\log_2(1/\varepsilon) \tag{3}$$
</div>

<p>Read it plainly: you can keep $m$ output bits, but only up to your input entropy $k$ minus a small toll for near-perfection. The crucial consequence kills the "amplification" fantasy in a single stroke — <em>if $k$ is small, no choice of hash makes $m$ large.</em> There is no clever function that turns a trickle of entropy into a flood.</p>

<div class="ckp-callout warn">
  <strong>One honest caveat about real conditioners</strong>
  <p>The Leftover Hash Lemma is unconditional — it holds against any attacker — but only for a "universal hash with a public random seed." The conditioners the standards actually use (hashes built on SHA-2 or SHA-3, HMAC, AES-based CMAC) are <em>fixed</em> functions, not seeded draws from such a family. Their entropy-preservation is therefore a weaker, computational claim: that a specific function behaves enough like an ideal one on real input. The famous "+64" safety margin in the standards is the heuristic price for that gap — the same shape of accounting, ported from a provable world to an assumption-based one.</p>
</div>

<p>The practical takeaway is the mental model every engineer should carry. What you must defend is a trustworthy <em>lower bound</em> on the input min-entropy. A source whose true randomness is, say, 7 bits per byte but that you cannot prove is above 7 — because you have no model, or no health test tied to it — is not a 7-bit source for accounting. It is an unbounded source, and you are in the dark. The danger is never that your measured bound is too conservative. The danger is claiming a bound you cannot defend, because the conditioner will faithfully whiten the output either way and hide the difference.</p>
</section>

<div class="ckp-sep">Why a Model</div>

<!-- ─── SECTION 4 ─────────────────────────────────────────── -->
<section id="sec-model">
<h2>4. Why You Need a Model, Not Just a Measurement</h2>

<p>A fair objection: if I capture raw data, run the standard min-entropy estimators, and get a healthy number, why isn't that enough? Because an estimator only measures the sample sitting in front of it, under the assumption that the sample is representative. A <em>model</em> is what licenses that assumption — and what tells you when it fails. Three reasons make the model non-negotiable.</p>

<ul class="ckp-hier">
  <li><strong>Coverage.</strong> An entropy source must hold across an entire operating envelope — process, voltage, temperature, ageing — that no finite lab capture can exhaust. The model is what extends a bound measured at a few corners to the corners you never tested, because it names <em>which</em> physical parameter governs the entropy and how. Without it, a clean reading at room temperature says nothing about the cold corner.</li>
  <li><strong>Discrimination.</strong> An estimator cannot tell genuine randomness from deterministic structure that merely looks complicated. A weakly chaotic circuit, or one secretly locked to an attacker's injected signal, can produce data the estimators rate as high-entropy while the true unpredictability against an informed attacker is near zero. That is the Dual_EC situation reappearing at the level of physics. Only a model — which predicts the <em>shape</em> the distribution should have, and lets you reject the data when the shape is wrong — catches it.</li>
  <li><strong>Meaning.</strong> A model is what makes a health test meaningful. A test threshold computed from a physical parameter is a test of the entropy. A generic statistical test run on the output is a test of the conditioner — the one component specifically designed to hide failures.</li>
</ul>

<div class="ckp-definition">
  <div class="ckp-def-label">Definition — Certifiable Entropy Source</div>
  <p>A source is certifiable when three things exist together: a stochastic model of its physics; a measured lower bound on its conditional min-entropy that is valid across the whole declared operating envelope; and an online test that rejects any run where the model's parameters wander out of the region where that bound holds. Unpredictability that cannot be written in this form is an aesthetic judgement, not a security parameter.</p>
</div>
</section>

<div class="ckp-sep">The Physics</div>

<!-- ─── SECTION 5 ─────────────────────────────────────────── -->
<section id="sec-sources">
<h2>5. Five Sources, Five Models</h2>

<p>To show the discipline is concrete and not a sermon, consider five physical sources that span the field — three classical, two quantum. For each one, the physics hands you an output model, the model names a single governing knob, and that knob both sets the entropy and tells you exactly what failure looks like.</p>

<h3>The classical three</h3>

<p><strong>Oscillator jitter.</strong> A free-running ring oscillator drifts in phase because thermal noise jostles each gate delay; over time those nudges add up into a random walk. The accumulated jitter, measured against the clock period, gives a single quality factor $Q = \sigma_{\text{acc}}^2 / T_0^2$. A larger $Q$ means more genuine wander and more entropy per bit. Measure one jitter variance and one period, and you have bounded both the bias and the correlation at once. The tell-tale sign of <em>real</em> thermal jitter is that it grows linearly with time; if it doesn't, you are probably looking at interference or an attacker's injected tone, not randomness.</p>

<p><strong>Amplified thermal noise.</strong> The charge carriers in any resistor jitter purely because of temperature — the Johnson–Nyquist law, $\sigma_v^2 = 4 k_B T R B$, ties that voltage noise directly to temperature, resistance, and bandwidth. This is irreducible physics, not a circuit artefact, which is what makes it attractive. Amplify it, compare it to a threshold, and the output bit is the sign of the noise. The entropy is then controlled by how large the amplifier's offset is relative to the amplified noise — a clean, measurable ratio.</p>

<p><strong>Metastability.</strong> A cross-coupled latch can be driven to a knife-edge between its two stable states, and thermal noise decides which way it falls. In principle this is beautiful; in practice it is the trickiest of the three, because manufacturing mismatch gives every latch a built-in lean, and that lean drifts with voltage and temperature. Worse, incomplete settling makes each output depend on the last, so the honest model is not a clean coin flip but a two-state Markov chain — and treating it as a coin flip overstates its entropy.</p>

<h3>The quantum two</h3>

<p><strong>Single-photon which-path.</strong> Send one photon at a balanced beam splitter; quantum mechanics assigns each path a clean one-half probability and one ideal bit of entropy. Reality intrudes through unequal detector efficiencies, dark counts, dead time, and afterpulsing — all classical imperfections an attacker may know or probe. Commercial devices in this family have been certified under both major standards, and those certifications rest on a model of precisely these imperfections, not on the ideal bit alone.</p>

<p><strong>Vacuum-fluctuation homodyne.</strong> Here the device measures the quantum "shot noise" of the vacuum against a strong reference beam. The catch: the measured signal mixes the true quantum variance with ordinary classical electronic noise. Quoting the <em>total</em> variance as entropy is the single most common overstatement in this whole field, because it credits you with randomness the attacker controls through the classical part.</p>

<div class="ckp-callout key">
  <strong>The clearance ratio is a security parameter, not a spec-sheet number</strong>
  <p>For the homodyne source, the ratio of quantum noise to classical noise — the "shot-noise clearance ratio" — decides how much of the measured signal is honestly random. The paper's simulations make the gap quantitative: as the clearance ratio worsens, the <em>honest</em> conditional min-entropy stays pinned at the value set by the genuine quantum noise, while the naive total-variance figure inflates without bound. When the two kinds of noise are equal, the overstatement is already about half a bit per sample; push classical noise higher and it tops a full bit. That shaded gap between the two curves is randomness the attacker controls.</p>
</div>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr>
    <th>Source</th>
    <th>Where the randomness lives</th>
    <th>Governing knob</th>
    <th>What failure looks like</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><span class="term">Oscillator jitter</span></td>
    <td>Thermal phase drift of a ring oscillator</td>
    <td>Jitter quality factor $Q$</td>
    <td>$Q$ collapses; jitter stops scaling with time (injection locking)</td>
  </tr>
  <tr>
    <td><span class="term">Amplified thermal</span></td>
    <td>Johnson–Nyquist noise in a resistor</td>
    <td>Offset vs. amplified noise</td>
    <td>Bias drift, amplifier saturation, $1/f$ contamination</td>
  </tr>
  <tr>
    <td><span class="term">Metastability</span></td>
    <td>A latch balanced on a knife-edge</td>
    <td>Built-in offset; Markov transitions</td>
    <td>Bias survives calibration; correlation won't vanish</td>
  </tr>
  <tr>
    <td><span class="term">Photon which-path</span></td>
    <td>One photon, two paths, Born rule</td>
    <td>Efficiency mismatch, dark counts</td>
    <td>Measured bias disagrees with the imperfection model</td>
  </tr>
  <tr>
    <td><span class="term">Vacuum homodyne</span></td>
    <td>Quantum shot noise of the vacuum</td>
    <td>Shot-noise clearance ratio</td>
    <td>"Quantum" variance fails to track the reference beam</td>
  </tr>
</tbody>
</table>
</div>

<p>Notice the last column. Every model comes with a way to be proven wrong by measurement. A model no experiment could ever contradict carries no information — and in a real evaluation lab, that falsification test <em>is</em> the acceptance test.</p>
</section>

<div class="ckp-sep">Keeping It True</div>

<!-- ─── SECTION 6 ─────────────────────────────────────────── -->
<section id="sec-monitor">
<h2>6. Measure, Monitor, Margin</h2>

<p>A model proves a number at design time. Three field disciplines keep that number honest at run time.</p>

<h3>Measure the raw source — before the conditioner</h3>

<p>The cardinal rule is procedural: tap the signal <em>upstream</em> of any hash or corrector. A conditioner whitens everything it touches, including failure. Measure after it and you are measuring the conditioner, not the source. Debiasing, XOR, von Neumann correction — all allowed in the data path, but they live <em>downstream</em> of the measurement point, they can never raise the min-entropy, and you may never credit their cleaned-up statistics as if they were the raw source.</p>

<h3>Estimate the hard way — assume nothing is independent</h3>

<p>Run the conservative non-IID estimators and report the <em>minimum</em> across all of them. This is not just caution; it is a free diagnosis. The estimator that wins tells you the failure mode. If a Markov estimator dominates, the source has serial dependence — the metastability latch with incomplete settling. If a longer-range predictor dominates, there is periodic structure an attacker may be injecting. If "most-common-value" dominates, the source is simply biased. Reading the winner is reading the disease.</p>

<h3>Tie every health test to a physical knob</h3>

<p>The standard built-in tests catch catastrophe — a source that drops dead or jams at one value. They do <em>not</em> catch the failure that actually happens in the field: a source that quietly slumps from 0.9 bits to 0.6 bits as the chip warms up, all while still looking noisy. The fix is to monitor, online, the very parameter the model says governs entropy — the jitter $Q$, the offset drift, the clearance ratio — and alarm the moment it crosses the value where your entropy claim would break.</p>

<div class="ckp-pull">
  <p>A generic output test asks "does this look random?" A model-bound test asks "is the physical thing that makes the randomness still doing its job?"</p>
  <cite>— The whole point of binding tests to parameters</cite>
</div>

<h3>Prove your alarm works by attacking it yourself</h3>

<p>A health test you have never tried to fool is decoration — a smoke detector you have never held a match to. So you inject the failures you fear: supply droop, electromagnetic pulses, thermal shock, manipulation of a laser's reference beam, deliberate illumination of a photon detector. The acceptance criterion is a <em>latency</em> statement. For each attack, the test must alarm before the true entropy falls below your claim, and the number of below-claim outputs emitted in the gap between collapse and alarm must be counted and bounded.</p>

<div class="ckp-callout">
  <strong>A worked alarm, in numbers</strong>
  <p>In the paper's simulation, a jitter source runs happily near 0.98 bits per sample. At a chosen instant, an injection-locking attack collapses its quality factor and the true entropy crashes to about 0.11 bits. A sliding-window monitor watches the estimate fall and fires its alarm as it crosses the claimed floor of 0.8 — with a detection latency of 160 outputs. That 160 is the concrete, reportable number an integrator must buffer or discard behind the alarm. An entropy claim with no latency bound is a statement about the past, not a guarantee about the next sample.</p>
</div>
</section>

<div class="ckp-sep">Confidentiality</div>

<!-- ─── SECTION 7 ─────────────────────────────────────────── -->
<section id="sec-leakage">
<h2>7. The Side Door</h2>

<p>The conditional min-entropy $\widetilde{H}_\infty(X \mid E)$ is only as honest as the side information $E$ it conditions on. If a physical side channel hands the attacker something the model left out of $E$, the true entropy is lower than the certified one, and every downstream guarantee silently fails. Leakage is therefore not a separate worry bolted on at the end. It <em>is</em> the question of whether your $E$ is complete.</p>

<p>And the stakes are sharper here than for an ordinary cipher. Leaking one key bit costs you one secret. Leaking the <em>state</em> of your noise source — the oscillator's phase, the comparator's instantaneous input, the laser's amplitude — can collapse the entropy of every future output, because an attacker who learns the source's state can predict samples rather than recover a single secret. Power and electromagnetic emanations carry exactly these quantities: the switching of the sampling logic, the comparator's decision, the analog-to-digital conversion are all correlated with the raw sample, and modern probes with machine-learning analysis pull such correlations out cheaply.</p>

<div class="ckp-callout warn">
  <strong>Some attacks run the monitor in reverse</strong>
  <p>Several of the faults from the previous section are also side channels played backwards. Injecting a tone into a ring oscillator can both <em>reduce</em> its entropy and <em>synchronise</em> it to the attacker's clock — and this has been demonstrated wirelessly, with no physical contact. A device that is monitored for entropy but not shielded for leakage can be driven into a low-entropy, attacker-synchronised state its health test was never designed to see.</p>
</div>

<p>A design that takes leakage seriously keeps the noise source and its first amplifier inside the same shielded, power-conditioned boundary as the conditioner, so the raw sample is never exposed on an external rail; treats the sampling clock and conversion events as leakage sources to be masked or randomly timed; optionally adds a decoy whose emanations are indistinguishable from the live source; and extends the fault-injection campaign to emission measurement, verifying that what an external probe can recover about the raw sample stays below a stated bound. The leakage budget is then reported right alongside the entropy budget. A conditional-entropy claim that does not even state which $E$ it assumed is not yet a claim.</p>
</section>

<div class="ckp-sep">The Quantum Question</div>

<!-- ─── SECTION 8 ─────────────────────────────────────────── -->
<section id="sec-quantum">
<h2>8. The Quantum Question</h2>

<p>The word "quantum" does more rhetorical work in this market than almost any other, so it deserves a careful answer to three separate questions that get routinely tangled together.</p>

<h3>Does a quantum generator carry a real advantage?</h3>

<p>Yes — a genuine one, worth paying for. Its ideal model has a first-principles entropy that is a consequence of quantum measurement itself, not an estimate of some messy classical process. But that advantage lives in the <em>ceiling</em>. Your security parameter is the <em>floor</em>, and the floor is classical: the single-photon device leaks through detector imperfections, the homodyne device through classical excess noise. Quantum mechanics guarantees the ceiling is high. It says nothing about where the floor sits — and the floor is where you stand.</p>

<div class="ckp-pull">
  <p>Quantum mechanics provides a ceiling on unpredictability. It is silent about the floor — and the floor is set entirely by how well the real apparatus approximates the ideal.</p>
  <cite>— The heart of the quantum case</cite>
</div>

<h3>Do quantum computers threaten hardware RNGs?</h3>

<p>Not at the entropy-source layer. A quantum computer attacks the hard-math assumptions behind public-key cryptography and, via Grover's algorithm, halves the effective strength of symmetric keys. It does not predict a well-characterised physical noise source, whose security at the raw layer is information-theoretic and rests on no computational assumption at all. The post-quantum transition is a story about the algorithms <em>downstream</em> of the generator — with one caveat: the hash or cipher used for conditioning should keep adequate strength under Grover, which the standard 256-bit choices already do.</p>

<h3>Do better quantum sensors make sources more predictable?</h3>

<p>This is the genuinely interesting threat. Improved quantum-limited sensing lowers the cost of measuring exactly the classical quantities that make up $E$ — a laser's phase, a detector's afterpulsing, a faint emanation — and so can enlarge the attacker's side information against a source whose leakage budget was set against weaker instruments. This is a leakage question, and the right response is to state, in the model, what measurement capability you assumed the attacker has.</p>

<div class="ckp-callout key">
  <strong>The question to ask any QRNG vendor</strong>
  <p>Not "is it quantum?" Ask instead: <em>What is your conditional min-entropy given your own classical noise? Which online test holds it there? And what attacker measurement capability did your leakage budget assume?</em> A transparent, certified classical generator with a defended conditional-entropy bound beats an opaque quantum one that merely ships the ideal bit. Transparency of the model is not a marketing nicety — under the definition in Section 4, it is what "certified" actually means.</p>
</div>
</section>

<div class="ckp-sep">The Full Picture</div>

<!-- ─── SECTION 9 ─────────────────────────────────────────── -->
<section id="sec-chain">
<h2>9. The Whole Chain in One Line</h2>

<p>The model, the measurement, the health test, the entropy accounting, and the leakage budget are routinely dismissed as compliance overhead laid on top of a source that is "obviously random." The order of dependence is the reverse. Those five are the only content the word <em>random</em> has in a cryptographic setting — the source is nothing without them. They link into a single chain, and dropping any one makes the others stop meaning anything.</p>

<div class="ckp-chain">

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">1</div>
    <div class="ckp-chain-content">
      <h4>Modeled</h4>
      <p>A stochastic model derived from the device physics turns a vague claim of "unpredictable" into an actual number, with the entropy tied to a measurable knob.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">2</div>
    <div class="ckp-chain-content">
      <h4>Measured</h4>
      <p>A conservative lower bound on conditional min-entropy is measured on the <em>raw</em> source, before any conditioning, with the most pessimistic applicable estimator.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">3</div>
    <div class="ckp-chain-content">
      <h4>Monitored</h4>
      <p>Health tests bound to the model's parameter keep the number true over time and temperature — and are proven to alarm fast enough by attacking them on purpose.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">4</div>
    <div class="ckp-chain-content">
      <h4>Margined</h4>
      <p>The conditioner spends the entropy honestly. With $n$ output bits needed, it must consume input carrying at least $n + 64$ bits of proven min-entropy.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">5</div>
    <div class="ckp-chain-content">
      <h4>Shielded</h4>
      <p>A leakage argument proves the attacker has not already been handed the source's secret through a side door of power, EM, timing, or photons.</p>
    </div>
  </div>

</div>

<h3>The accounting, made concrete</h3>

<p>The chain ends in arithmetic. If your live health test guarantees $\rho$ bits of min-entropy per raw bit, and you want a 256-bit full-entropy block, the rule is to consume enough raw bits to clear $256 + 64 = 320$ bits of proven entropy. A cleaner source needs fewer raw bits; a degraded one simply consumes more — until it crosses the floor, at which point the health test has already alarmed. The same number the model predicts, the estimator confirms, and the health test defends is the number that sizes the conditioner.</p>

<div class="ckp-eq">
  <span class="eq-label">Conditioning Margin — Eq. (4)</span>
  $$h_{\text{in}} \ge n_{\text{out}} + 64 \tag{4}$$
</div>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr>
    <th>Source (design target)</th>
    <th>Min-entropy ρ per raw bit</th>
    <th>Raw bits for a 256-bit block</th>
    <th>Conditioner</th>
  </tr>
</thead>
<tbody>
  <tr><td><span class="term">Oscillator jitter</span></td><td>0.50</td><td>640</td><td>SHA-256</td></tr>
  <tr><td><span class="term">Amplified thermal</span></td><td>0.80</td><td>400</td><td>SHA-256</td></tr>
  <tr><td><span class="term">Metastability</span></td><td>0.60</td><td>534</td><td>SHA-256</td></tr>
  <tr><td><span class="term">Vacuum homodyne</span></td><td>0.95</td><td>337</td><td>SHA-256</td></tr>
</tbody>
</table>
</div>

<div class="ckp-callout warn">
  <strong>A caveat the simple table hides</strong>
  <p>That tidy division assumes min-entropy simply adds up bit by bit — which is only true for a source whose samples are independent. A source like metastability is explicitly <em>not</em> independent; it follows a Markov model with memory. For such a source, the true entropy of a whole block is found by working through the joint distribution, not by naively multiplying an average per-sample rate. The honest accountant keeps the dependence in view.</p>
</div>

<p>And so the conclusion writes itself. Unpredictability is necessary — and once it is written as a proven, monitored, leak-contained lower bound on conditional min-entropy, it is also sufficient, because at that point the Leftover Hash Lemma supplies the rest for free. The error worth eradicating is the belief that a conditioner can rescue a source the model never characterised. It cannot.</p>

<div class="ckp-pull">
  <p>A hash function is an excellent way to hide that you do not know how much entropy you have — and a poor way to obtain any.</p>
  <cite>— The closing line of the argument</cite>
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
    <td><span class="term">Min-Entropy</span></td>
    <td>$H_\infty(X) = -\log_2 \max_i p_i$ — the worst-case measure of unpredictability, set by the single most likely outcome. The right entropy for a key.</td>
  </tr>
  <tr>
    <td><span class="term">Conditional Min-Entropy</span></td>
    <td>How unpredictable the output remains after the attacker has seen all the side information $E$ they can access. The quantity a real claim must lower-bound.</td>
  </tr>
  <tr>
    <td><span class="term">Side Information ($E$)</span></td>
    <td>Everything an attacker can observe or control — supply ripple, electronic noise, temperature, classical excess noise, leaked emanations.</td>
  </tr>
  <tr>
    <td><span class="term">Stochastic Model</span></td>
    <td>A physics-derived description $p(x\mid\theta)$ of the raw source, with parameters tied to measurable electrical or optical quantities.</td>
  </tr>
  <tr>
    <td><span class="term">Conditioner</span></td>
    <td>A deterministic step (hash, XOR, von Neumann corrector) that concentrates existing entropy into a shorter, smoother string. It can never create entropy.</td>
  </tr>
  <tr>
    <td><span class="term">Leftover Hash Lemma</span></td>
    <td>The theorem that prices extraction: from $k$ input bits you can pull at most $m \le k - 2\log_2(1/\varepsilon)$ near-uniform output bits.</td>
  </tr>
  <tr>
    <td><span class="term">Health Test</span></td>
    <td>An online check that the source still meets its entropy claim. Most useful when its threshold is computed from a model parameter, not from generic output statistics.</td>
  </tr>
  <tr>
    <td><span class="term">Detection Latency</span></td>
    <td>The number of below-claim outputs a health test lets through between an entropy collapse and its alarm. Must be measured and bounded.</td>
  </tr>
  <tr>
    <td><span class="term">Clearance Ratio</span></td>
    <td>For a homodyne QRNG, the ratio of genuine quantum noise to classical noise — a monitored security parameter, not a performance figure.</td>
  </tr>
  <tr>
    <td><span class="term">SP 800-90B / AIS 31</span></td>
    <td>The two major evaluation traditions for entropy sources: NIST's estimator-centric battery, and BSI's model-centric requirement for a stochastic model.</td>
  </tr>
</tbody>
</table>
</div>
</section>

<!-- ─── REFERENCES ─────────────────────────────────────────── -->
<div class="ckp-refs" id="references">
<h2>References</h2>
<p id="ref-SP90B"><span class="ref-num">[SP90B]</span> Turan, M.S., Barker, E., Kelsey, J., McKay, K.A., Baish, M.L., Boyle, M.: Recommendation for the Entropy Sources Used for Random Bit Generation. NIST Special Publication 800-90B (2018).</p>
<p id="ref-SP90A"><span class="ref-num">[SP90A]</span> Barker, E., Kelsey, J.: Recommendation for Random Number Generation Using Deterministic Random Bit Generators. NIST SP 800-90A Rev. 1 (2015).</p>
<p id="ref-SP90C"><span class="ref-num">[SP90C]</span> Barker, E., Kelsey, J., McKay, K.A., Roginsky, A., Turan, M.S.: Recommendation for Random Bit Generator (RBG) Constructions. NIST SP 800-90C (final, 2025).</p>
<p id="ref-AIS31v3"><span class="ref-num">[AIS31v3]</span> Peter, M., Schindler, W.: A Proposal for: Functionality Classes for Random Number Generators, Version 3.0. BSI, mathematical-technical reference for AIS 20/AIS 31 (10 September 2024).</p>
<p id="ref-AIS31v2"><span class="ref-num">[AIS31v2]</span> Killmann, W., Schindler, W.: A Proposal for: Functionality Classes for Random Number Generators, Version 2.0. BSI AIS 20/AIS 31 (2011).</p>
<p id="ref-Shumow2007"><span class="ref-num">[Shumow2007]</span> Shumow, D., Ferguson, N.: On the Possibility of a Back Door in the NIST SP 800-90 Dual_EC_PRNG. CRYPTO 2007 Rump Session (2007).</p>
<p id="ref-Bernstein2016"><span class="ref-num">[Bernstein2016]</span> Bernstein, D.J., Lange, T., Niederhagen, R.: Dual EC: A Standardized Back Door. In: The New Codebreakers, LNCS 9100, pp. 256–281. Springer (2016).</p>
<p id="ref-ILL1989"><span class="ref-num">[ILL1989]</span> Impagliazzo, R., Levin, L.A., Luby, M.: Pseudo-random Generation from One-way Functions. In: STOC 1989, pp. 12–24. ACM (1989).</p>
<p id="ref-Dodis2008"><span class="ref-num">[Dodis2008]</span> Dodis, Y., Ostrovsky, R., Reyzin, L., Smith, A.: Fuzzy Extractors: How to Generate Strong Keys from Biometrics and Other Noisy Data. SIAM J. Computing 38(1), 97–139 (2008).</p>
<p id="ref-Baudet2011"><span class="ref-num">[Baudet2011]</span> Baudet, M., Lubicz, D., Micolod, J., Tassiaux, A.: On the Security of Oscillator-Based Random Number Generators. J. Cryptology 24(2), 398–425 (2011).</p>
<p id="ref-Petrie2000"><span class="ref-num">[Petrie2000]</span> Petrie, C.S., Connelly, J.A.: A Noise-Based IC Random Number Generator for Applications in Cryptography. IEEE TCAS I 47(5), 615–621 (2000).</p>
<p id="ref-Tokunaga2008"><span class="ref-num">[Tokunaga2008]</span> Tokunaga, C., Blaauw, D., Mudge, T.: True Random Number Generator with a Metastability-Based Quality Control. IEEE JSSC 43(1), 78–85 (2008).</p>
<p id="ref-Markettos2009"><span class="ref-num">[Markettos2009]</span> Markettos, A.T., Moore, S.W.: The Frequency Injection Attack on Ring-Oscillator-Based True Random Number Generators. In: CHES 2009, LNCS 5747, pp. 317–331. Springer (2009).</p>
<p id="ref-Bayon2012"><span class="ref-num">[Bayon2012]</span> Bayon, P., et al.: Contactless Electromagnetic Active Attack on Ring Oscillator Based TRNG. In: COSADE 2012, LNCS 7275, pp. 151–166. Springer (2012).</p>
<p id="ref-Dodis2013"><span class="ref-num">[Dodis2013]</span> Dodis, Y., Pointcheval, D., Ruhault, S., Vergnaud, D., Wichs, D.: Security Analysis of Pseudorandom Number Generators with Input: /dev/random is Not Robust. In: ACM CCS 2013, pp. 647–658.</p>
<p id="ref-Fortuna"><span class="ref-num">[Fortuna]</span> Ferguson, N., Schneier, B., Kohno, T.: Cryptography Engineering (Fortuna generator). Wiley (2010).</p>
<p id="ref-FIPS140"><span class="ref-num">[FIPS140-3]</span> NIST: Security Requirements for Cryptographic Modules. FIPS PUB 140-3 (2019); adopts ISO/IEC 19790:2012.</p>
<p id="ref-HerreroCollantes"><span class="ref-num">[HC2017]</span> Herrero-Collantes, M., Garcia-Escartin, J.C.: Quantum Random Number Generators. Rev. Mod. Phys. 89, 015004 (2017).</p>
<p id="ref-Ma2016"><span class="ref-num">[Ma2016]</span> Ma, X., Yuan, X., Cao, Z., Qi, B., Zhang, Z.: Quantum Random Number Generation. npj Quantum Information 2, 16021 (2016).</p>
<p id="ref-Haw2015"><span class="ref-num">[Haw2015]</span> Haw, J.Y., et al.: Maximization of Extractable Randomness in a Quantum Random-Number Generator. Phys. Rev. Applied 3, 054004 (2015).</p>
<p id="ref-IDQ"><span class="ref-num">[IDQ]</span> ID Quantique: Quantis QRNG — AIS 31 / SP 800-90B Certification and Stochastic-Model Documentation. Vendor certification documentation.</p>
</div>

</div><!-- end .ckp-body -->

<!-- ─── Sidebar TOC ─────────────────────────────────────────── -->
<aside class="ckp-sidebar">
  <div class="ckp-toc-label">Contents</div>
  <ul class="ckp-toc-list" id="ckp-toc">
    <li data-section="abstract"><a href="#abstract">Abstract</a></li>
    <li data-section="sec-error"><a href="#sec-error">1. The Number That Looks Random</a></li>
    <li data-section="sec-entropy"><a href="#sec-entropy">2. Entropy Is About the Adversary</a></li>
    <li class="toc-sub" data-section="sec-entropy"><a href="#sec-entropy">Min-Entropy</a></li>
    <li class="toc-sub" data-section="sec-entropy"><a href="#sec-entropy">Conditional Min-Entropy</a></li>
    <li data-section="sec-hash"><a href="#sec-hash">3. A Hash Cannot Make Entropy</a></li>
    <li class="toc-sub" data-section="sec-hash"><a href="#sec-hash">Leftover Hash Lemma</a></li>
    <li data-section="sec-model"><a href="#sec-model">4. Why You Need a Model</a></li>
    <li data-section="sec-sources"><a href="#sec-sources">5. Five Sources, Five Models</a></li>
    <li class="toc-sub" data-section="sec-sources"><a href="#sec-sources">Classical Three</a></li>
    <li class="toc-sub" data-section="sec-sources"><a href="#sec-sources">Quantum Two</a></li>
    <li data-section="sec-monitor"><a href="#sec-monitor">6. Measure, Monitor, Margin</a></li>
    <li data-section="sec-leakage"><a href="#sec-leakage">7. The Side Door</a></li>
    <li data-section="sec-quantum"><a href="#sec-quantum">8. The Quantum Question</a></li>
    <li data-section="sec-chain"><a href="#sec-chain">9. The Whole Chain</a></li>
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
  var sections = ['abstract','sec-error','sec-entropy','sec-hash','sec-model','sec-sources','sec-monitor','sec-leakage','sec-quantum','sec-chain','sec-glossary','references'];
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