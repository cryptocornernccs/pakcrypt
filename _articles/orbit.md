---
layout: post
title: "Keys From Orbit"
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
  <div class="ckp-kicker">Quantum Communication · Satellite QKD · Space Engineering</div>
  <h1>Keys From <em>Orbit</em></h1>
  <p class="ckp-deck">Forty years after two researchers proposed encoding secrets in single photons, spacecraft are distributing cryptographic keys between continents. The physics is settled. The engineering — pointing a metre-wide beam of single photons at a telescope from 800 kilometres up, at night, in clear weather, while moving at 7.5 kilometres a second — is where the real story lives.</p>
  <div class="ckp-meta">
    <span>Quantum Technologies</span>
    <span class="dot"></span>
    <span>Feature · 2026</span>
    <span class="dot"></span>
    <span>~26 min read</span>
  </div>
</div>

<!-- Keywords -->
<div class="ckp-keywords">
  <span class="ckp-kw">Quantum Key Distribution</span>
  <span class="ckp-kw">BB84</span>
  <span class="ckp-kw">Decoy States</span>
  <span class="ckp-kw">Entanglement</span>
  <span class="ckp-kw">Optical Ground Station</span>
  <span class="ckp-kw">Trusted Node</span>
  <span class="ckp-kw">SNSPD</span>
  <span class="ckp-kw">Post-Quantum Cryptography</span>
</div>

<!-- Mobile TOC -->
<div class="ckp-mobile-toc" id="ckp-mob-toc-toggle">
  <span>Contents</span><span>▾</span>
</div>
<div class="ckp-mobile-toc-list" id="ckp-mob-toc-list">
  <a href="#abstract">In Brief</a>
  <a href="#sec-why">1. Why Put Cryptography in Orbit</a>
  <a href="#sec-history">2. Fifty Years in Five Acts</a>
  <a href="#sec-how">3. How a Satellite Makes a Key</a>
  <a href="#sec-photon">4. Nine Photons Out of a Billion</a>
  <a href="#sec-hardware">5. Catching, Counting and Clocking</a>
  <a href="#sec-sky">6. The Sky Gets a Vote</a>
  <a href="#sec-trust">7. Whom Do You Trust?</a>
  <a href="#sec-numbers">8. The Numbers, Without the Marketing</a>
  <a href="#sec-debate">9. Is Any of This Worth It?</a>
  <a href="#sec-next">10. What Comes Next</a>
  <a href="#sec-glossary">Glossary</a>
  <a href="#references">References</a>
</div>

<!-- ═══════════════════ LAYOUT ════════════════════════════════ -->
<div class="ckp-layout">

<!-- ─── Main Body ─────────────────────────────────────────── -->
<div class="ckp-body">

<!-- ABSTRACT -->
<div class="ckp-abstract" id="abstract">
  <div class="ckp-abstract-label">In Brief</div>
  <p>Quantum key distribution lets two parties share a secret whose security rests on the laws of physics rather than on the difficulty of a mathematical problem. Optical fibre cannot carry it more than a few hundred kilometres, because a quantum signal cannot be amplified. Satellites can — and since 2016 they have. This article traces how the idea travelled from a physicist's unpublishable manuscript to spacecraft linking Beijing and Cape Town, and then examines, honestly, the seven engineering problems that still make satellite QKD one of the hardest communication technologies humans have ever attempted to operate routinely.</p>
</div>

<!-- STATS BAR -->
<div class="ckp-stat-row">
  <div class="ckp-stat"><span class="stat-num">1,203</span><span class="stat-label">km entanglement from orbit, 2017</span></div>
  <div class="ckp-stat"><span class="stat-num">~40 dB</span><span class="stat-label">Typical downlink photon loss</span></div>
  <div class="ckp-stat"><span class="stat-num">0.12</span><span class="stat-label">bits per second, best entangled link</span></div>
  <div class="ckp-stat"><span class="stat-num">1.07 Mbit</span><span class="stat-label">Secure key in one microsatellite pass</span></div>
</div>

<!-- ─── SECTION 1 ─────────────────────────────────────────── -->
<section id="sec-why">
<h2>1. Why Put Cryptography in Orbit</h2>

<p class="drop-cap">Every secure connection you make today — to a bank, a government portal, a messaging app — begins with a handshake in which two strangers who have never met agree on a secret number. That handshake is the most quietly astonishing trick in computing, and it rests on a mathematical wager: that certain problems, such as factoring a large integer or reversing an elliptic-curve multiplication, are too hard to solve in any reasonable time.</p>

<p>A sufficiently large quantum computer would win that wager. Peter Shor showed in 1994 that such a machine could factor integers and compute discrete logarithms efficiently, which retires essentially every public-key algorithm now in service. Nobody knows when such a machine will exist. What everyone in the field does know is that the threat has a peculiar time signature: an adversary can record encrypted traffic today and decrypt it whenever the machine arrives. Cryptographers call this <em>harvest now, decrypt later</em>. For anything that must stay secret for thirty or fifty years — diplomatic cables, medical genomics, industrial designs, state archives — the exposure is not in the future. It is already running.</p>

<p>There are two serious responses. The first, and by far the more important, is <strong>post-quantum cryptography</strong>: replace the vulnerable mathematics with new mathematics believed hard for quantum computers too. It is software, it works over the existing internet, and international standards were finalised in 2024 [<a href="#ref-FIPS">FIPS2024</a>]. For almost every purpose it is the right answer, and the rest of this article should not be read as an argument against it.</p>

<p>The second response abandons mathematical assumptions altogether. In <strong>quantum key distribution</strong> (QKD), the secret is not computed; it is <em>measured</em>. Two parties derive shared random bits from the outcomes of measurements on individual quantum particles, and the laws of quantum mechanics place a hard, quantifiable ceiling on how much an eavesdropper can have learned. The key that comes out is not "hard to break". It is <em>information-theoretically secure</em>: no future computer, however powerful, retroactively reveals it.</p>

<div class="ckp-callout key">
  <strong>The property that makes QKD different</strong>
  <p>A key established by post-quantum cryptography in 2026 and recorded by an adversary can, in principle, be broken in 2050 if the underlying mathematics falls. A key established by QKD in 2026 cannot. To learn it, the eavesdropper had to be physically present, interfering with individual photons, on the night the key was made — and that interference is detectable. Cryptographers call this <em>everlasting secrecy</em>.</p>
</div>

<p>So why go to space for it? Because on the ground, quantum signals die. A single photon in optical fibre has perhaps a 95 % chance of surviving each kilometre at telecom wavelengths — a loss of about 0.2 decibels per kilometre. That sounds gentle until you compound it. Over 100 km, roughly one photon in a hundred survives. Over 500 km, about one in <em>ten billion</em>. Classical networks solve this with amplifiers and repeaters every few tens of kilometres. Quantum networks cannot: the <strong>no-cloning theorem</strong>, the same principle that makes eavesdropping detectable, forbids copying an unknown quantum state. You cannot amplify what you are not allowed to duplicate.</p>

<p>That leaves two options for long distances. Either you chain together <em>trusted relay stations</em> that decrypt and re-encrypt the key at each hop — which means every hut along the route knows your secret — or you go up. Above about 10 kilometres of altitude the atmosphere effectively ends, and the remaining 780 kilometres to a low-orbit satellite are vacuum, where a photon travels essentially for free. The loss on a space link is dominated not by absorption but by geometry: the beam simply spreads out. And geometric spreading scales with the <em>square</em> of distance, not exponentially.</p>

<div class="ckp-pull">
  <p>Fibre loss is exponential in distance. Free-space loss is quadratic. Somewhere past a few hundred kilometres, the sky becomes the cheaper medium — which is the entire argument for satellite QKD in one sentence.</p>
</div>
</section>

<div class="ckp-sep">Origins</div>

<!-- ─── SECTION 2 ─────────────────────────────────────────── -->
<section id="sec-history">
<h2>2. Fifty Years in Five Acts</h2>

<p>The history of quantum cryptography is unusually well documented, partly because so much of it happened between a handful of people who kept in touch, and partly because its origin story is genuinely strange.</p>

<h3>Act I: A paper nobody would publish</h3>

<p>Around 1970, Stephen Wiesner — then a graduate student at Columbia — wrote up an idea he called <em>conjugate coding</em>. Because certain pairs of quantum properties cannot be measured simultaneously with arbitrary precision, he argued, one could make banknotes carrying quantum "watermarks" that a counterfeiter could not copy, and could encode two messages such that reading one destroyed the other. Journals rejected it. The manuscript circulated informally for over a decade before finally appearing in a computing newsletter in 1983 [<a href="#ref-Wiesner">Wiesner1983</a>].</p>

<p>One of the few people who took it seriously was Charles Bennett, who had met Wiesner as a student. In the early 1980s Bennett, at IBM, and Gilles Brassard, at the Université de Montréal, turned the idea from a curiosity about money into a protocol for keys. Their 1984 conference paper [<a href="#ref-BB84">BB84</a>] — four pages, in a proceedings volume that was for years difficult to obtain — described what is still the workhorse of the field. Everyone calls it <strong>BB84</strong>.</p>

<p>In 1991 Artur Ekert, then in Oxford, published an independent route to the same goal [<a href="#ref-Ekert">Ekert1991</a>]: instead of sending prepared states, distribute <em>entangled pairs</em> and let the correlations themselves certify security, using a violation of Bell's inequality as the proof that nobody has tampered. That distinction — prepare-and-measure versus entanglement — still divides the field's architectures today, and it turns out to matter enormously for satellites.</p>

<h3>Act II: Thirty-two centimetres</h3>

<p>In 1989 Bennett, Brassard and colleagues built the first working demonstration. It transmitted a key across 32.5 centimetres of open air on an optical bench [<a href="#ref-Bennett1992">Bennett1992</a>]. The apparatus made an audible noise when it switched polarisation states, which meant that the machine, as Brassard later liked to observe, was perfectly secure against any eavesdropper who happened to be deaf. It is a useful reminder of a theme this article returns to repeatedly: the mathematics of QKD is airtight, and the hardware leaks.</p>

<p>Fibre demonstrations followed through the 1990s, first over kilometres, then tens of kilometres. But the exponential wall was obvious from the start, and attention turned to open air.</p>

<h3>Act III: Mountain to mountain</h3>

<p>Free-space experiments escalated quickly. A 1998 Los Alamos experiment ran a link of about a kilometre in daylight. In 2002 a European team pushed a key across 23.4 km between two Alpine peaks, at night [<a href="#ref-Kurtsiefer">Kurtsiefer2002</a>]. Then in 2007 came the result that convinced people space was feasible: a 144-kilometre link between the Canary Islands of La Palma and Tenerife, using an optical ground station originally built by the European Space Agency for laser communication tests [<a href="#ref-SMB2007">Schmitt-Manderbach2007</a>]. Both prepare-and-measure and entanglement-based keys were demonstrated over that path [<a href="#ref-Ursin2007">Ursin2007</a>].</p>

<p>The significance was not the distance itself but the <em>loss</em>. A 144-kilometre horizontal path through dense low-altitude air is optically about as punishing as a slant path from a low-orbit satellite to a mountain-top telescope. The Canary link showed the photon budget could be closed. What remained was to put one end on a moving platform.</p>

<p>That happened in stages: keys exchanged with a transmitter on an aircraft in 2013, and in the same year with a payload on a hot-air balloon and a floating platform, deliberately testing what happens when the sender is in motion and the pointing loop must work in real time [<a href="#ref-Nauerth">Nauerth2013</a>, <a href="#ref-WangJY">WangJY2013</a>].</p>

<h3>Act IV: Micius</h3>

<p>On 16 August 2016, China launched a 635-kilogram spacecraft named after the ancient philosopher Micius. It carried a 300-millimetre transmitting telescope, an entangled-photon source, and a decoy-state BB84 transmitter operating at 850 nanometres. Within a year it had produced three results that between them defined the field [<a href="#ref-Lu2022">Lu2022</a>].</p>

<div class="ckp-chain">

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">2017</div>
    <div class="ckp-chain-content">
      <h4>Satellite-to-ground key distribution</h4>
      <p>Decoy-state BB84 downlinks to metre-class ground telescopes produced kilobit-per-second secret keys at ranges up to 1,200 km — around 20 orders of magnitude more efficient than sending the same photons through fibre over the same distance [<a href="#ref-Liao2017">Liao2017</a>].</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">2017</div>
    <div class="ckp-chain-content">
      <h4>Entanglement across a continent</h4>
      <p>The satellite beamed one photon of an entangled pair to each of two ground stations 1,203 km apart, and the pairs still violated a Bell inequality on arrival — the first demonstration that entanglement survives a trip from orbit through the atmosphere at that scale [<a href="#ref-Yin2017">Yin2017</a>].</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">2018</div>
    <div class="ckp-chain-content">
      <h4>Intercontinental video call</h4>
      <p>Using the satellite as a relay, keys were shared between stations near Beijing and Vienna — about 7,600 km apart — and used to encrypt a video conference. The satellite made a separate key with each side and combined them, a mechanism explained below [<a href="#ref-Liao2018">Liao2018</a>].</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">2020</div>
    <div class="ckp-chain-content">
      <h4>Entanglement-based keys, at last</h4>
      <p>Not merely distributing entanglement but distilling a finite-key-secure cryptographic key from it, over 1,120 km. The rate: <strong>0.12 bits per second</strong>. That number, four orders of magnitude below the prepare-and-measure result, is the single most important figure in the entire architecture debate [<a href="#ref-Yin2020">Yin2020</a>].</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">2022</div>
    <div class="ckp-chain-content">
      <h4>Miniaturisation</h4>
      <p>A microsatellite of about 100 kg, carrying a 23-kg quantum payload, launched into low orbit — a tenth the mass of Micius, built to be manufactured in numbers rather than as a one-off science mission.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">2025</div>
    <div class="ckp-chain-content">
      <h4>Real time, and a portable ground station</h4>
      <p>The microsatellite demonstrated real-time key distillation on board, delivering up to <strong>1.07 megabits</strong> of secure key in a single pass to a ground terminal weighing under 100 kg rather than the multi-tonne observatories used previously — and relayed keys between stations in China and South Africa, about 12,900 km apart [<a href="#ref-Li2025">Li2025</a>].</p>
    </div>
  </div>

</div>

<h3>Act V: Everyone else</h3>

<p>What began as one country's science programme is now a crowded field, and the diversity of approaches is itself informative.</p>

<ul class="ckp-hier">
  <li><strong>CubeSats.</strong> A Singapore-led team flew an entangled-photon source in a nanosatellite, demonstrating in 2020 that the delicate business of generating correlated photon pairs survives launch and orbit in a shoebox-sized package [<a href="#ref-Villar">Villar2020</a>]. Successor missions with UK partners launched in 2025 and 2026, aimed squarely at driving cost down.</li>
  <li><strong>Europe.</strong> A dedicated QKD satellite developed by an industrial consortium under space-agency and Commission funding is scheduled for launch in the late-2026 window, intended as the space segment of a continent-wide quantum communication infrastructure. Its stated purpose is sovereignty: not depending on cryptographic infrastructure controlled elsewhere.</li>
  <li><strong>Canada.</strong> A mission taking the opposite architectural bet — putting the <em>receiver</em> in orbit and the sources on the ground. Uplinks suffer worse turbulence, but they let you keep the complicated, upgradeable hardware where engineers can reach it.</li>
  <li><strong>Fibre integration.</strong> Meanwhile the terrestrial backbone kept growing. A national network exceeding 10,000 km of fibre with well over a hundred backbone nodes now ingests satellite-derived keys alongside fibre-derived ones [<a href="#ref-Chen2025">Chen2025</a>].</li>
</ul>

<div class="ckp-callout">
  <strong>The pattern worth noticing</strong>
  <p>Every satellite QKD system that is <em>operational</em> today uses the same architecture: prepare-and-measure decoy-state BB84, on a single downlink, at night, in clear weather, serving a small number of large ground stations. Every entanglement payload in orbit is a demonstrator. That is not a coincidence or a failure of ambition — the rest of this article explains why the physics pushes every programme to the same answer.</p>
</div>
</section>

<div class="ckp-sep">Mechanism</div>

<!-- ─── SECTION 3 ─────────────────────────────────────────── -->
<section id="sec-how">
<h2>3. How a Satellite Actually Makes a Key</h2>

<p>Strip away the vocabulary and BB84 is a game about mismatched rulers.</p>

<p>The sender — conventionally Alice, here aboard the spacecraft — emits a photon and encodes a random bit in its polarisation. But she also picks, at random, one of two <em>bases</em>: she might use the rectilinear basis, where horizontal means 0 and vertical means 1, or the diagonal basis, where 45° means 0 and 135° means 1. The receiver, Bob, on the ground, has no idea which she chose, so he too picks a basis at random for each arriving photon.</p>

<p>When their choices match, Bob's measurement reproduces Alice's bit. When they differ, quantum mechanics guarantees the result is pure coin-flip noise. Afterwards, over an ordinary public radio or internet channel, they compare which <em>bases</em> they used — never the bits — and discard every event where they disagreed. Roughly half the data survives. That surviving string is the raw key.</p>

<p>The security comes from what an eavesdropper must do. To learn anything, Eve has to measure the photons in transit. She does not know the basis either. Half the time she picks wrong, and her measurement irreversibly scrambles the state she then forwards. Her interference shows up as errors in the small sample of key bits Alice and Bob publicly compare. Below a threshold error rate they can mathematically squeeze out a shorter key about which Eve provably knows almost nothing. Above it, they abort. There is no middle ground where Eve reads the traffic undetected.</p>

<div class="ckp-callout warn">
  <strong>Weak lasers and the decoy trick</strong>
  <p>Nobody has a perfect single-photon source that works in orbit. Real systems fire heavily attenuated laser pulses containing, on average, about half a photon. Occasionally a pulse contains two — and Eve could then split one off, keep it, and let the other through undisturbed.</p>
  <p>The fix, developed in the 2000s and now universal, is <em>decoy states</em>: Alice randomly varies the brightness of her pulses among a few preset levels. Eve cannot tell which level she is attacking, so any photon-splitting strategy distorts the statistics of the different levels differently — and the distortion is visible. Decoy-state BB84 is what every operational satellite flies.</p>
</div>

<p>What comes out of the sky is not yet a key. It is a stream of detection events riddled with errors, most of them from noise rather than attackers. Four classical steps follow, and they matter more to real systems than most popular accounts admit: <em>sifting</em> (discarding mismatched bases and non-detections), <em>parameter estimation</em> (measuring the error rate and bounding Eve's information), <em>error correction</em> (reconciling the two strings while leaking as little as possible), and <em>privacy amplification</em> (hashing the reconciled string down to a shorter one about which the leaked information is negligible).</p>

<p>There is a fifth step that satellite links cannot skip. Security proofs are cleanest when you have infinitely many photons; a satellite pass lasts perhaps five to eight minutes. <strong>Finite-key analysis</strong> applies statistical corrections for the short block, and those corrections can eat tens of percent of the apparent yield. When a vendor quotes a key rate without saying whether finite-key effects were included, they have quoted a number that does not exist.</p>

<h3>The relay trick — and its price</h3>

<p>A satellite in low orbit cannot see two distant continents at once. So how did keys get from Beijing to Vienna?</p>

<div class="ckp-chain">
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">1</div>
    <div class="ckp-chain-content">
      <h4>Make a key with A</h4>
      <p>On a night pass over the first station, the satellite and station A run BB84 and end up sharing a secret string $K_A$. The satellite stores it.</p>
    </div>
  </div>
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">2</div>
    <div class="ckp-chain-content">
      <h4>Make a different key with B</h4>
      <p>Hours later, over the second station, it independently establishes $K_B$.</p>
    </div>
  </div>
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">3</div>
    <div class="ckp-chain-content">
      <h4>Broadcast the combination</h4>
      <p>It computes the bitwise exclusive-or $K_A \oplus K_B$ and transmits that publicly over ordinary radio. Anyone may listen; the combination reveals nothing about either key on its own.</p>
    </div>
  </div>
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">4</div>
    <div class="ckp-chain-content">
      <h4>Station B recovers A's key</h4>
      <p>Because B knows $K_B$, it computes $(K_A \oplus K_B) \oplus K_B = K_A$. The two ground stations now share a key, and they never needed to see the satellite at the same moment.</p>
    </div>
  </div>
</div>

<p>This is elegant, it works, and it has one consequence that shapes every national programme on Earth: <strong>the satellite knew both keys.</strong> It is what the field calls a <em>trusted node</em>. Whoever built it, wrote its firmware, generated its random numbers and commands it can, in principle, recover every key it ever relayed. We will come back to this.</p>
</section>

<div class="ckp-sep">Challenge One</div>

<!-- ─── SECTION 4 ─────────────────────────────────────────── -->
<section id="sec-photon">
<h2>4. Nine Photons Out of a Billion</h2>

<p>Ask an engineer what makes satellite QKD hard and you will get a different answer depending on which subsystem they lost sleep over. But every answer eventually reduces to the same root cause: you are trying to deliver individual photons across hundreds of kilometres, and you are not allowed to make more of them.</p>

<h3>The tyranny of diffraction</h3>

<p>Light will not travel in a perfectly straight line. Push a beam through an aperture of diameter $D$ and it spreads with an angle set by the wavelength:</p>

<div class="ckp-eq">
  <span class="eq-label">Diffraction-limited divergence — Eq. (1)</span>
  $$\theta \;\approx\; \frac{2.44\,\lambda}{D} \tag{1}$$
</div>

<p>The numbers are unforgiving. A 200-millimetre telescope sending 850-nanometre light has a divergence of roughly ten microradians — about 0.0006 degrees, which sounds superb until you multiply by distance. At 800 kilometres, that beam has swelled into a patch on the ground some <strong>ten to fifteen metres across</strong>. A ground telescope of 0.8 metres captures the fraction of the patch it happens to cover:</p>

<div class="ckp-eq">
  <span class="eq-label">Geometric collection efficiency — Eq. (2)</span>
  $$\eta_{\text{geo}} \;=\; \left(\frac{D_{\text{rx}}}{\theta R}\right)^{\!2} \tag{2}$$
</div>

<p>Plug the numbers in: about 0.5 %, or a loss of roughly 23 decibels, before anything else has gone wrong. Add atmospheric absorption and scattering (2–3 dB straight up from a high, dry site, considerably more at low elevation angles), imperfect pointing, losses in the receiving optics, the narrow filters, and the detector's own inefficiency, and the total for a realistic link sits somewhere around <strong>35 to 45 decibels</strong>.</p>

<div class="ckp-callout">
  <strong>What 40 decibels means</strong>
  <p>It means one part in ten thousand. Fire a hundred million photons per second at the sky and you may collect ten thousand per second on the ground — from which, after sifting, error correction and privacy amplification, you might keep one or two thousand bits of actual secret key per second. A radio engineer would simply turn up the power. Here you cannot: turning up the power means putting more photons in each pulse, which is precisely what hands an eavesdropper an attack. The link budget is not a starting point for negotiation. It is the whole game.</p>
</div>

<h3>Hitting a moving coin</h3>

<p>A satellite in an 800-kilometre orbit travels at about 7.5 kilometres per second and crosses the sky in five to eight minutes. Seen from the ground it sweeps across at roughly half a degree per second — slow enough to look leisurely, catastrophically fast for an optical link whose beam is ten microradians wide. To stay locked, both ends must hold their aim to within a few microradians. That is roughly the angle a one-euro coin subtends at a distance of five kilometres, and it must be held continuously, on a moving target, for minutes at a time.</p>

<p>Nothing about a conventional satellite dish helps here. The pointing chain is closer to astronomy than to telecommunications, and it runs in stages:</p>

<ul class="ckp-hier">
  <li><strong>Prediction.</strong> Orbital ephemeris propagated forward gets both ends pointing within a tenth of a degree — good enough to be in the right part of the sky, hopeless for the link itself.</li>
  <li><strong>Beacon acquisition.</strong> The ground station fires a bright laser beacon, deliberately spread over about half a milliradian so that it will actually land on the spacecraft despite the pointing error. The satellite sees it on a camera or quadrant detector and knows precisely where the ground station is.</li>
  <li><strong>Closing the loop.</strong> A <em>fast steering mirror</em> — a small mirror on piezoelectric actuators, correcting a thousand times a second — takes over the fine work, holding the beam to one or two microradians while the whole spacecraft slews. The ground station closes its own loop on a beacon coming down.</li>
  <li><strong>Only then, the quantum signal.</strong> Photons are sent only while both loops report lock, and every microradian of residual jitter shows up directly as lost key.</li>
</ul>

<p>Engineers who have built these systems will tell you, almost without exception, that this control loop — not the exotic quantum hardware — is where programmes fail. A telescope that cannot point is an expensive mirror.</p>

<p>Ground stations, meanwhile, are not telecom equipment. A working optical ground station is an astronomical observatory with a cryptographic annexe: a 0.6- to 1-metre diffraction-limited telescope on a direct-drive mount, a dome, a concrete pier isolated from the surrounding ground so that a passing truck does not shake the link, adaptive or tip–tilt optics to fight atmospheric blurring, and a control room. Nobody puts one on a rooftop in a city centre, for reasons the next sections make painfully clear.</p>
</section>

<div class="ckp-sep">Challenge Two</div>

<!-- ─── SECTION 5 ─────────────────────────────────────────── -->
<section id="sec-hardware">
<h2>5. Catching, Counting and Clocking</h2>

<h3>Detecting one photon at a time</h3>

<p>At the bottom of the link sits a device that must reliably register the arrival of a single quantum of light, and — just as importantly — must almost never claim to have seen one when it has not. Two technologies compete.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr>
    <th>Property</th>
    <th>Silicon avalanche photodiode (SPAD)</th>
    <th>Superconducting nanowire (SNSPD)</th>
  </tr>
</thead>
<tbody>
  <tr><td><span class="term">Efficiency</span></td><td>50–65 % at 850 nm</td><td>85–95 %</td></tr>
  <tr><td><span class="term">False counts</span></td><td>A few hundred per second</td><td>Tens per second</td></tr>
  <tr><td><span class="term">Timing precision</span></td><td>350–500 picoseconds</td><td>Under 50 picoseconds</td></tr>
  <tr><td><span class="term">Cooling</span></td><td>Thermoelectric, −30 °C</td><td>Cryogenic, 1–2.5 kelvin</td></tr>
  <tr><td><span class="term">Practical consequence</span></td><td>Cheap, rugged, deployable anywhere</td><td>Best performance, needs a closed-cycle cryocooler, kilowatts of power and regular servicing</td></tr>
</tbody>
</table>
</div>

<p>The superconducting detector is a nanometre-thin wire of niobium nitride held just below its critical current. A single absorbed photon deposits enough energy to break superconductivity in a tiny hotspot, producing a measurable voltage pulse. It is a beautiful device and its performance is not really matched by anything else. Its cost, though, is dominated not by the wire but by the refrigerator wrapped around it — which is why several programmes deliberately begin with the humbler semiconductor detector, get the rest of the system working, and add cryogenics later.</p>

<h3>Knowing exactly when to look</h3>

<p>Here is the trick that makes the whole thing possible at all. Background light — starlight, scattered city glow, airglow, moonlight — arrives at random times. The signal photons do not: they leave the spacecraft at precisely known instants, dictated by a clock. So the receiver simply refuses to listen except during a window about a <em>nanosecond</em> wide, timed to when the photon is expected. That single measure throws away well over 99.9 % of the background.</p>

<p>Making it work requires a timing chain most people never think about: an atomic-grade frequency reference (typically a rubidium oscillator disciplined by satellite navigation signals) at each end, time-tagging electronics resolving tens of picoseconds, and bright synchronisation pulses interleaved into the quantum stream — one every thousand pulses or so — to keep the two clocks locked to each other.</p>

<h3>Doppler, in two flavours</h3>

<p>A source hurtling towards you and then away from you shifts the wavelength of its light:</p>

<div class="ckp-eq">
  <span class="eq-label">Relativistic Doppler shift, first order — Eq. (3)</span>
  $$\frac{\Delta\lambda}{\lambda} \;=\; \frac{v_{\text{los}}}{c} \tag{3}$$
</div>

<p>With a line-of-sight velocity of a few kilometres per second, that fraction is around $10^{-5}$ — a shift of roughly ten <em>picometres</em> at 850 nm. Against a typical filter 0.1 nanometres wide, that is a tenth of the passband: noticeable, but harmless. It only becomes an engineering headache if you narrow the filter drastically, which is exactly what daylight operation demands. Then the filter must be actively temperature-tuned to chase the shift through the pass.</p>

<p>The more troublesome effect is temporal. As the range changes at kilometres per second, the flight time of the photons drifts — by around ten <em>microseconds</em> for every second that elapses. Against a one-nanosecond detection window, that is enormous. The receiver must continuously predict and compensate the drift from the orbital model, correcting itself against the arriving synchronisation pulses. Get it wrong by a nanosecond and the gate closes on empty sky.</p>

<div class="ckp-callout key">
  <strong>Three beams, one telescope</strong>
  <p>A working link is not one optical channel but three, sharing the same aperture and separated by wavelength and brightness: a strong <em>beacon</em> for tracking, bright <em>synchronisation</em> pulses for the clock, and the almost-invisible <em>quantum</em> signal carrying the key. Designing them so the loud ones do not blind the receiver looking for the quiet one is its own small art.</p>
</div>
</section>

<div class="ckp-sep">Challenge Three</div>

<!-- ─── SECTION 6 ─────────────────────────────────────────── -->
<section id="sec-sky">
<h2>6. The Sky Gets a Vote</h2>

<p>Every operational satellite QKD system in the world today works at night, in clear weather. This is not conservatism or a lack of engineering ambition. It follows from the physics of trying to detect one photon in the presence of a star.</p>

<h3>The sun is a very loud transmitter</h3>

<p>A receiver cannot distinguish a signal photon from a background photon that happens to arrive in the same direction, at the same wavelength, at the same instant. So rejection has to happen in all three domains at once: a narrow spectral filter, a tight field of view, and the nanosecond time gate. In darkness, at a good site, those measures reduce background to a few hundred counts per second against a signal of tens of thousands — an error rate around 1 %, comfortably below the threshold at which a key can still be extracted.</p>

<p>In daylight the sky delivers something like a million counts per second into the same filter. The error rate saturates at 50 % — the value you would get from pure noise — and no key exists at any rate. Daylight quantum links <em>have</em> been demonstrated, using extreme filtering, longer wavelengths where the sky is dimmer, and single-mode fibre as an ultra-tight spatial filter. They are impressive. They are also slower, far more complex, and not yet how any national network schedules its service.</p>

<p>The moon is a milder version of the same problem. Around full moon the background can climb tenfold, and operators plan around it much as astronomers do.</p>

<h3>Cloud is not attenuation. It is a wall</h3>

<div class="ckp-callout warn">
  <strong>Why weather is binary</strong>
  <p>A radio link degrades gracefully through cloud and rain. An optical quantum link does not degrade — it stops. Even modest cloud imposes tens of decibels of loss on a budget that has no margin left. There is no clever modulation, no error-correcting code, no power increase that recovers it. The only engineering responses are choosing dry, high sites; spreading stations across regions with uncorrelated weather; and scheduling around forecasts.</p>
</div>

<p>This is why the operational model of every deployed system is not real-time encryption but <strong>key accumulation</strong>. On clear nights the satellite fills a buffer of key material at each ground station; that buffer is then drawn down during the day, in fog, and through the monsoon, feeding conventional symmetric encryption. If the buffer holds a month's worth, a month of bad weather is invisible to the people using the network.</p>

<p>The weather problem has a much sharper edge for entanglement-based architectures. There, both ground stations must have clear sky <em>at the same moment</em>. If one site is usable on 60 % of nights and another on 70 %, the joint availability is roughly the product — 42 % — and it falls further as you add stations. Prepare-and-measure links need only one site clear per pass, and can collect the other half of the relationship on a different night entirely.</p>

<h3>Turbulence, the astronomer's old enemy</h3>

<p>Finally, the atmosphere is not a uniform slab. Thermal turbulence in the last few kilometres above the receiver bends and breaks the incoming wavefront — the same effect that makes stars twinkle. For a quantum link it causes the beam to wander off the detector, and it destroys the ability to couple the light into a single-mode fibre, which the best detectors want. Mitigations range from a simple fast tip–tilt mirror to full adaptive optics with a deformable mirror. All of them are cheaper than choosing a bad site and trying to compensate afterwards.</p>
</section>

<div class="ckp-sep">Challenge Four</div>

<!-- ─── SECTION 7 ─────────────────────────────────────────── -->
<section id="sec-trust">
<h2>7. Whom Do You Trust?</h2>

<p>Suppose every engineering problem above is solved. A subtler one remains, and it is the reason the field has not simply converged on a single global system.</p>

<h3>The trusted node problem</h3>

<p>Recall the relay: the satellite makes a key with each station and publishes the exclusive-or. It works beautifully and it means the spacecraft holds both secrets in the clear. The physics guarantee — that no eavesdropper on the <em>channel</em> can learn the key — says nothing whatsoever about the operator of the relay.</p>

<p>For a network run by and for a single organisation, that may be entirely acceptable: the satellite is inside the trust perimeter, like a safe in the basement. For anyone buying a turnkey system built abroad, it is not a footnote but the central question. The manufacturer of the payload wrote the firmware, supplied the random number generator, and specified the key store. The whole point of an information-theoretic key is to remove trust assumptions; a foreign-built trusted node re-introduces a different one and merely relocates the problem.</p>

<div class="ckp-pull">
  <p>Quantum key distribution eliminates the need to trust mathematics. It does not eliminate the need to trust whoever built the box.</p>
</div>

<h3>The entanglement escape route, and its cost</h3>

<p>There is a way out, and it is the reason Ekert's 1991 protocol still matters. If the satellite instead generates <em>entangled pairs</em> and sends one photon to each of two ground stations, it never learns the key at all. The correlations are certified by a Bell test performed by the ground stations themselves. Security survives even if the spacecraft was built by your adversary. This is what "untrusted node" means, and as a security property it is close to ideal.</p>

<p>The price is arithmetic. For prepare-and-measure, the key rate falls in proportion to the channel transmittance $\eta$. For dual-downlink entanglement, both photons must survive independent journeys:</p>

<div class="ckp-eq">
  <span class="eq-label">Rate scaling: single vs. dual downlink — Eq. (4)</span>
  $$R_{\text{single}} \;\propto\; \eta \qquad\text{versus}\qquad R_{\text{dual}} \;\propto\; \eta_A\,\eta_B \tag{4}$$
</div>

<p>In decibels, the losses add. A downlink of 40 dB becomes a dual downlink of 70 to 90 dB. Recall that 40 dB already meant one part in ten thousand; 80 dB means one part in a hundred million. That is precisely why the best entanglement-based key on record ran at 0.12 bits per second while contemporary prepare-and-measure links delivered megabits per pass. At 0.12 bits per second, a single 256-bit key takes over half an hour of perfect conditions at both stations simultaneously.</p>

<p>There is a further practical obstacle. To serve pairs of stations that are <em>not</em> simultaneously visible — which, for a low-orbit satellite, is most pairs on Earth — you would need to store one photon of an entangled pair until the second station comes into view. That requires a space-qualified <em>quantum memory</em> with storage times and efficiencies far beyond anything demonstrated. Together with entanglement swapping between satellites, that is the technology that would eventually enable a true global quantum internet with no trusted nodes anywhere. It is a research programme for the 2040s, not a procurement option today.</p>

<h3>Attacking the hardware instead of the mathematics</h3>

<p>The final trust problem is the oldest lesson in the field, and the one first taught by that audibly clicking bench apparatus in 1989. Security proofs describe idealised devices. Real devices have imperfections, and imperfections are attack surfaces. A partial catalogue of demonstrated attacks on real QKD systems:</p>

<ul class="ckp-hier">
  <li><strong>Detector blinding.</strong> Shine a bright continuous light into the receiver and the single-photon detectors stop behaving quantum-mechanically, becoming ordinary classical light meters an attacker can drive at will — while both parties see a perfectly normal-looking error rate [<a href="#ref-Lydersen">Lydersen2010</a>].</li>
  <li><strong>Time-shift and efficiency-mismatch attacks.</strong> Two detectors are never identical; their sensitivity peaks at slightly different instants. Nudge the arrival time and you bias which outcome gets recorded.</li>
  <li><strong>Trojan-horse probing.</strong> Send light <em>into</em> the transmitter and read the reflections to learn what state it is currently preparing. The countermeasure is a sixty-decibel optical isolator and a watchdog photodiode.</li>
  <li><strong>Source side channels.</strong> If the four polarisation states differ measurably in their spectrum, timing or spatial mode, an eavesdropper may distinguish them without touching the polarisation at all.</li>
  <li><strong>Weak randomness.</strong> If the basis choices are predictable, everything else is irrelevant. The random number generator is the most security-critical component in the system and the easiest to neglect.</li>
</ul>

<p>None of these breaks quantum mechanics; all of them break products. The field's response has been to formalise it: international standards for the security requirements and test methods of QKD systems now exist, along with a Common Criteria protection profile for prepare-and-measure modules — meaning independent laboratories can evaluate whether a given box actually deserves the guarantee its brochure claims [<a href="#ref-Xu2020">Xu2020</a>].</p>
</section>

<div class="ckp-sep">Reality Check</div>

<!-- ─── SECTION 8 ─────────────────────────────────────────── -->
<section id="sec-numbers">
<h2>8. The Numbers, Without the Marketing</h2>

<p>Quantum communication attracts more than its share of enthusiastic claims. The most useful antidote is a table of what has actually been measured, and what the physics permits.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr>
    <th>Architecture</th>
    <th>Channel loss</th>
    <th>Demonstrated key rate</th>
    <th>Status</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><span class="term">Trusted node, prepare-and-measure downlink</span></td>
    <td>~35–45 dB</td>
    <td>kbit/s during a pass; up to 1.07 Mbit total per pass</td>
    <td>Operational; several spacecraft flying</td>
  </tr>
  <tr>
    <td><span class="term">Untrusted node, dual-downlink entanglement</span></td>
    <td>~70–90 dB</td>
    <td>0.12 bit/s over 1,120 km</td>
    <td>Demonstrated once, as an experiment</td>
  </tr>
  <tr>
    <td><span class="term">Geostationary orbit</span></td>
    <td>Adds ~33 dB over a 800 km orbit</td>
    <td>Studied, not flown for QKD</td>
    <td>Feasible on paper with metre-class space optics</td>
  </tr>
  <tr>
    <td><span class="term">Terrestrial fibre, no relay</span></td>
    <td>0.2 dB/km — 100 dB at 500 km</td>
    <td>Mbit/s below 100 km; effectively zero past ~400 km</td>
    <td>Widely deployed at metropolitan scale</td>
  </tr>
</tbody>
</table>
</div>

<h3>Why not geostationary orbit?</h3>

<p>It is a fair question, and a popular one, because a geostationary satellite hangs motionless in the sky: no tracking slew, no Doppler sweep, no five-minute scramble. The problem is that geometric loss scales with the square of the distance, and geostationary orbit is 45 times farther away than a typical low orbit. That is an extra 33 decibels — a factor of two thousand — on a budget that was already down to one part in ten thousand. Recovering it means metre-class diffraction-limited optics in space and a spacecraft an order of magnitude larger and more expensive. Feasibility studies conclude it can be done, and it has an interesting advantage for untrusted-node schemes, since a geostationary platform can see two distant ground stations continuously. Nobody has flown one for quantum key distribution.</p>

<h3>What a night's worth of key is actually good for</h3>

<p>Suppose a station collects a few hundred kilobits to a megabit of secret key on a good night. What does that buy?</p>

<ul class="ckp-hier">
  <li><strong>Plenty:</strong> refreshing the symmetric keys of a few hundred high-value links several times a day. A 256-bit key is 256 bits; a megabit is thousands of them.</li>
  <li><strong>Plenty:</strong> seeding a key-management system that then derives session keys conventionally, so that the quantum material anchors a much larger classical structure.</li>
  <li><strong>Just about:</strong> one-time-pad encryption of short, extremely sensitive messages — a megabit is around 125 kilobytes of perfectly unbreakable text per night.</li>
  <li><strong>Absolutely not:</strong> one-time-pad encryption of ordinary traffic. Video calls, database replication, or a national network's day-to-day communications would exhaust a night's key production in seconds. Any proposal that implies otherwise has an arithmetic problem.</li>
</ul>

<p>The same arithmetic explains why nobody builds a ground station in every town. A single satellite in low orbit gets one or two usable night passes over a given site, and can realistically service only a handful of stations per night in total. Serving hundreds of sites would require either hundreds of satellites or a wait of many months between visits — and each station is an observatory costing on the order of a million dollars or more to build and a six-figure sum every year to run. Every serious network therefore looks the same: a small number of regional hubs collecting key from orbit, with conventional cryptography carrying the assurance the last few hundred kilometres to the users.</p>
</section>

<div class="ckp-sep">The Argument</div>

<!-- ─── SECTION 9 ─────────────────────────────────────────── -->
<section id="sec-debate">
<h2>9. Is Any of This Worth It?</h2>

<p>Given everything above — night-only service, weather dependence, observatory-grade ground stations, trusted relays and a decade of hardware attacks — a reasonable person might ask why anyone bothers, when post-quantum cryptography is a software update.</p>

<p>That is not a rhetorical question. It is the live position of several of the world's most capable signals-intelligence and cyber-security agencies. The United States National Security Agency has published guidance stating that it does not support the use of quantum key distribution for protecting communications in national security systems, and lists five specific limitations: it provides no source authentication on its own; it requires special-purpose hardware; trusted relays add cost and insider risk; validating real implementations is difficult; and it is unusually easy to deny service to [<a href="#ref-NSA">NSA</a>]. The United Kingdom's National Cyber Security Centre reaches a similar conclusion and recommends post-quantum cryptography as the preferred mitigation [<a href="#ref-NCSC">NCSC</a>]. A joint position paper from French, German, Dutch and Swedish authorities concluded in 2024 that QKD is presently usable only in niche cases and that clear priority should go to post-quantum cryptography [<a href="#ref-ANSSI">ANSSI2024</a>].</p>

<p>Each of those five limitations is technically correct, and the first deserves unpacking because it looks fatal at first glance.</p>

<div class="ckp-definition">
  <div class="ckp-def-label">The authentication paradox</div>
  <p>QKD guarantees that nobody eavesdropped on the key. It does not tell you <em>who</em> is at the far end of the beam. Without authentication of the public discussion channel, an attacker could simply impersonate the satellite and establish a perfectly secure key with a victim. So QKD needs classical authentication — either a pre-shared symmetric key or a post-quantum signature. Which prompts the obvious objection: if you need conventional cryptography anyway, why not use it for the key as well?</p>
</div>

<p>The answer turns on a difference in <em>lifetime</em>. Authentication only has to hold at the instant it is used. If the signature algorithm is broken in 2045, the attacker gains the ability to impersonate people from 2045 onward; he cannot travel back to a night in 2028 and physically insert himself into a ten-metre-wide beam between a spacecraft and a guarded mountain-top telescope. Confidentiality is the opposite: if the key-establishment mathematics falls in 2045, every recorded session from 2028 unlocks retroactively. So the sensible design uses each tool where it is strong — post-quantum signatures for the fleeting act of authentication, quantum physics for the decades-long obligation of secrecy.</p>

<p>The other four limitations are real and are handled, where they are handled at all, by architecture rather than denial: hybrid systems keep a conventional key pool alongside the quantum one and fall back automatically when cloud or jamming stops the photons; independent evaluation against published standards addresses implementation flaws; and owning the spacecraft addresses the trusted node.</p>

<p>Meanwhile, some of the same countries whose agencies signed those cautions are funding satellite QKD programmes. That is less contradictory than it appears. The agencies' guidance addresses general-purpose government and commercial networks, where QKD is genuinely a poor fit. The funding addresses a narrower question: whether a state wants the option of a key whose secrecy does not depend on a mathematical assumption, and whose root of trust it controls end to end. Framed that way, the technology is not a competitor to post-quantum cryptography. It is an insurance policy on it, purchased for a small number of links where the cost of eventual failure is effectively unbounded.</p>

<div class="ckp-callout key">
  <strong>The honest summary</strong>
  <p>For 99 % of the world's traffic — banking, messaging, commerce, ordinary government business — post-quantum cryptography is the correct and sufficient answer, and satellite QKD would be an absurd extravagance. For a small class of secrets that must survive fifty years, and for organisations unwilling to bet those secrets on a mathematical conjecture holding for half a century, a physics-based key has a property no algorithm can offer. Both statements are true at once. Most of the public argument consists of people asserting one of them at people asserting the other.</p>
</div>
</section>

<div class="ckp-sep">Horizon</div>

<!-- ─── SECTION 10 ────────────────────────────────────────── -->
<section id="sec-next">
<h2>10. What Comes Next</h2>

<p>Four lines of work will determine whether satellite quantum communication becomes ordinary infrastructure or remains a specialist instrument.</p>

<div class="ckp-chain">

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">01</div>
    <div class="ckp-chain-content">
      <h4>Smaller, cheaper, more numerous</h4>
      <p>The trajectory from a 635-kg science satellite to a 100-kg microsatellite to CubeSat demonstrators, and from multi-tonne observatories to portable ground terminals under 100 kg, is the single most consequential trend in the field. A technology that requires a national observatory serves a handful of users; one that fits in a van serves many.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">02</div>
    <div class="ckp-chain-content">
      <h4>Daylight operation</h4>
      <p>Moving to longer wavelengths where the sky is dimmer, filtering in wavelength, angle and time simultaneously, and using single-mode fibre as an ultra-tight spatial filter have all produced working daylight links on the ground. Carrying that into routine orbital service would roughly double the available contact time and remove the field's most awkward operational constraint.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">03</div>
    <div class="ckp-chain-content">
      <h4>Getting rid of trusted nodes</h4>
      <p>Measurement-device-independent and twin-field protocols close the detector attack surface and change how the key rate scales with loss. Entanglement payloads keep improving. But the decisive step is a space-qualified quantum memory that can hold half of an entangled pair until a second ground station comes into view — the enabling technology for entanglement swapping and, eventually, a genuine quantum internet.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">04</div>
    <div class="ckp-chain-content">
      <h4>Integration, which is where value actually appears</h4>
      <p>Key that nothing consumes is worthless. The unglamorous work — standard interfaces between quantum systems and key-management infrastructure, policy engines that decide which key source serves which application, automatic fallback when the sky closes — is what turns a physics demonstration into a service. Every mature programme has discovered this the same way: by building the optics first and then finding nothing plugged into them.</p>
    </div>
  </div>

</div>

<p>It is worth stepping back to appreciate what has already happened. In 1989 the first quantum key crossed 32 centimetres of laboratory air. Within thirty years, single photons prepared aboard a spacecraft were being caught by telescopes on the ground and turned into keys that linked cities on opposite sides of the planet. The physics never changed — Wiesner's insight about conjugate variables is the same one exploited today. What changed was that engineers learned to point a beam of individual photons at a moving target from eight hundred kilometres away, to catch them with superconducting wire, and to know, to within a nanosecond, exactly when to look.</p>

<div class="ckp-pull">
  <p>The security of quantum key distribution is guaranteed by the laws of physics. Everything else about it — the pointing, the clocks, the cryogenics, the weather, the trust — is engineering. And engineering is where it will be won or lost.</p>
</div>
</section>

<div class="ckp-sep">Reference</div>

<!-- ─── GLOSSARY ──────────────────────────────────────────── -->
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
  <tr><td><span class="term">QKD</span></td><td>Quantum key distribution: deriving shared secret bits from quantum measurements, with an eavesdropper's knowledge bounded by physics rather than by computational difficulty.</td></tr>
  <tr><td><span class="term">BB84</span></td><td>The 1984 prepare-and-measure protocol in which random bits are encoded in randomly chosen conjugate bases. Still the basis of every operational satellite system.</td></tr>
  <tr><td><span class="term">Decoy states</span></td><td>Randomly varying the brightness of transmitted pulses so that photon-number-splitting attacks reveal themselves in the statistics.</td></tr>
  <tr><td><span class="term">No-cloning theorem</span></td><td>An unknown quantum state cannot be copied. The source of QKD's security — and the reason quantum signals cannot be amplified.</td></tr>
  <tr><td><span class="term">QBER</span></td><td>Quantum bit error rate: the fraction of mismatched bits in the sifted key. Above roughly 11 % for BB84, no secret key can be extracted at all.</td></tr>
  <tr><td><span class="term">Sifting</span></td><td>Publicly comparing measurement bases and discarding events where they disagreed, without revealing any bit values.</td></tr>
  <tr><td><span class="term">Privacy amplification</span></td><td>Hashing a partially compromised string down to a shorter one about which an eavesdropper's information is provably negligible.</td></tr>
  <tr><td><span class="term">Finite-key analysis</span></td><td>Statistical corrections accounting for the limited number of photons collected in a short pass. Ignoring it inflates quoted key rates.</td></tr>
  <tr><td><span class="term">Trusted node</span></td><td>A relay that holds key material in the clear — such as a satellite combining two keys by exclusive-or. Secure against channel eavesdroppers, not against its own operator.</td></tr>
  <tr><td><span class="term">Dual downlink</span></td><td>Entanglement architecture sending one photon of a pair to each of two ground stations. Removes the trusted node; multiplies the loss.</td></tr>
  <tr><td><span class="term">Optical ground station</span></td><td>The receiving end: a diffraction-limited telescope, precision mount, dome, filters, single-photon detectors and timing electronics. An observatory, not a dish.</td></tr>
  <tr><td><span class="term">SNSPD</span></td><td>Superconducting nanowire single-photon detector: over 90 % efficient with picosecond timing, at the cost of cooling to a couple of degrees above absolute zero.</td></tr>
  <tr><td><span class="term">Post-quantum cryptography</span></td><td>Classical algorithms believed hard for quantum computers, standardised in 2024. Software, scalable, and the primary answer for almost all traffic.</td></tr>
  <tr><td><span class="term">Harvest now, decrypt later</span></td><td>Recording encrypted traffic today to decrypt it once a capable quantum computer exists. The reason long-lived secrets are already exposed.</td></tr>
</tbody>
</table>
</div>
</section>

<!-- ─── REFERENCES ─────────────────────────────────────────── -->
<div class="ckp-refs" id="references">
<h2>References</h2>
<p id="ref-Wiesner"><span class="ref-num">[Wiesner1983]</span> Wiesner, S.: Conjugate coding. <em>ACM SIGACT News</em> <strong>15</strong>(1), 78–88 (1983). Written c. 1970; rejected by journals for over a decade.</p>
<p id="ref-BB84"><span class="ref-num">[BB84]</span> Bennett, C.H., Brassard, G.: Quantum cryptography: public key distribution and coin tossing. <em>Proc. IEEE Int. Conf. on Computers, Systems and Signal Processing</em>, Bangalore, 175–179 (1984). Reprinted in <em>Theor. Comput. Sci.</em> <strong>560</strong>, 7–11 (2014).</p>
<p id="ref-Ekert"><span class="ref-num">[Ekert1991]</span> Ekert, A.K.: Quantum cryptography based on Bell's theorem. <em>Phys. Rev. Lett.</em> <strong>67</strong>(6), 661–663 (1991).</p>
<p id="ref-Bennett1992"><span class="ref-num">[Bennett1992]</span> Bennett, C.H., Bessette, F., Brassard, G., Salvail, L., Smolin, J.: Experimental quantum cryptography. <em>J. Cryptology</em> <strong>5</strong>, 3–28 (1992).</p>
<p id="ref-Kurtsiefer"><span class="ref-num">[Kurtsiefer2002]</span> Kurtsiefer, C., et al.: A step towards global key distribution. <em>Nature</em> <strong>419</strong>, 450 (2002).</p>
<p id="ref-SMB2007"><span class="ref-num">[Schmitt-Manderbach2007]</span> Schmitt-Manderbach, T., et al.: Experimental demonstration of free-space decoy-state quantum key distribution over 144 km. <em>Phys. Rev. Lett.</em> <strong>98</strong>, 010504 (2007).</p>
<p id="ref-Ursin2007"><span class="ref-num">[Ursin2007]</span> Ursin, R., et al.: Entanglement-based quantum communication over 144 km. <em>Nature Physics</em> <strong>3</strong>, 481–486 (2007).</p>
<p id="ref-Nauerth"><span class="ref-num">[Nauerth2013]</span> Nauerth, S., et al.: Air-to-ground quantum communication. <em>Nature Photonics</em> <strong>7</strong>, 382–386 (2013).</p>
<p id="ref-WangJY"><span class="ref-num">[WangJY2013]</span> Wang, J.-Y., et al.: Direct and full-scale experimental verifications towards ground–satellite quantum key distribution. <em>Nature Photonics</em> <strong>7</strong>, 387–393 (2013).</p>
<p id="ref-Liao2017"><span class="ref-num">[Liao2017]</span> Liao, S.-K., et al.: Satellite-to-ground quantum key distribution. <em>Nature</em> <strong>549</strong>, 43–47 (2017). <a href="https://doi.org/10.1038/nature23655">doi:10.1038/nature23655</a></p>
<p id="ref-Yin2017"><span class="ref-num">[Yin2017]</span> Yin, J., et al.: Satellite-based entanglement distribution over 1200 kilometers. <em>Science</em> <strong>356</strong>, 1140–1144 (2017). <a href="https://doi.org/10.1126/science.aan3211">doi:10.1126/science.aan3211</a></p>
<p id="ref-Liao2018"><span class="ref-num">[Liao2018]</span> Liao, S.-K., et al.: Satellite-relayed intercontinental quantum network. <em>Phys. Rev. Lett.</em> <strong>120</strong>, 030501 (2018).</p>
<p id="ref-Yin2020"><span class="ref-num">[Yin2020]</span> Yin, J., et al.: Entanglement-based secure quantum cryptography over 1,120 kilometres. <em>Nature</em> <strong>582</strong>, 501–505 (2020). <a href="https://doi.org/10.1038/s41586-020-2401-y">doi:10.1038/s41586-020-2401-y</a></p>
<p id="ref-Villar"><span class="ref-num">[Villar2020]</span> Villar, A., et al.: Entanglement demonstration on board a nano-satellite. <em>Optica</em> <strong>7</strong>(7), 734–737 (2020).</p>
<p id="ref-Lu2022"><span class="ref-num">[Lu2022]</span> Lu, C.-Y., Cao, Y., Peng, C.-Z., Pan, J.-W.: Micius quantum experiments in space. <em>Rev. Mod. Phys.</em> <strong>94</strong>, 035001 (2022).</p>
<p id="ref-Li2025"><span class="ref-num">[Li2025]</span> Li, Y., et al.: Microsatellite-based real-time quantum key distribution. <em>Nature</em> <strong>640</strong>, 47–54 (2025). <a href="https://doi.org/10.1038/s41586-025-08739-z">doi:10.1038/s41586-025-08739-z</a></p>
<p id="ref-Chen2025"><span class="ref-num">[Chen2025]</span> Chen, H.-Z., et al.: China quantum communication network. <em>npj Quantum Information</em> <strong>11</strong>, 137 (2025).</p>
<p id="ref-Lydersen"><span class="ref-num">[Lydersen2010]</span> Lydersen, L., et al.: Hacking commercial quantum cryptography systems by tailored bright illumination. <em>Nature Photonics</em> <strong>4</strong>, 686–689 (2010).</p>
<p id="ref-Xu2020"><span class="ref-num">[Xu2020]</span> Xu, F., Ma, X., Zhang, Q., Lo, H.-K., Pan, J.-W.: Secure quantum key distribution with realistic devices. <em>Rev. Mod. Phys.</em> <strong>92</strong>, 025002 (2020).</p>
<p id="ref-Pirandola"><span class="ref-num">[Pirandola2020]</span> Pirandola, S., et al.: Advances in quantum cryptography. <em>Adv. Opt. Photon.</em> <strong>12</strong>(4), 1012–1236 (2020).</p>
<p id="ref-FIPS"><span class="ref-num">[FIPS2024]</span> National Institute of Standards and Technology: FIPS 203 (ML-KEM), FIPS 204 (ML-DSA) and FIPS 205 (SLH-DSA), August 2024.</p>
<p id="ref-NSA"><span class="ref-num">[NSA]</span> National Security Agency / Central Security Service: <em>Quantum Key Distribution (QKD) and Quantum Cryptography (QC)</em>, cybersecurity guidance.</p>
<p id="ref-NCSC"><span class="ref-num">[NCSC]</span> UK National Cyber Security Centre: <em>Quantum security technologies</em>, white paper.</p>
<p id="ref-ANSSI"><span class="ref-num">[ANSSI2024]</span> ANSSI (France), BSI (Germany), NLNCSA (Netherlands) and the Swedish National Communications Security Authority: <em>Position paper on quantum key distribution</em> (2024).</p>
</div>

</div><!-- end .ckp-body -->

<!-- ─── Sidebar TOC ─────────────────────────────────────────── -->
<aside class="ckp-sidebar">
  <div class="ckp-toc-label">Contents</div>
  <ul class="ckp-toc-list" id="ckp-toc">
    <li data-section="abstract"><a href="#abstract">In Brief</a></li>
    <li data-section="sec-why"><a href="#sec-why">1. Why Cryptography in Orbit</a></li>
    <li class="toc-sub" data-section="sec-why"><a href="#sec-why">The Fibre Wall</a></li>
    <li data-section="sec-history"><a href="#sec-history">2. Fifty Years in Five Acts</a></li>
    <li class="toc-sub" data-section="sec-history"><a href="#sec-history">Wiesner to BB84</a></li>
    <li class="toc-sub" data-section="sec-history"><a href="#sec-history">Micius and After</a></li>
    <li data-section="sec-how"><a href="#sec-how">3. How a Satellite Makes a Key</a></li>
    <li class="toc-sub" data-section="sec-how"><a href="#sec-how">Decoy States</a></li>
    <li class="toc-sub" data-section="sec-how"><a href="#sec-how">The Relay Trick</a></li>
    <li data-section="sec-photon"><a href="#sec-photon">4. Nine Photons in a Billion</a></li>
    <li class="toc-sub" data-section="sec-photon"><a href="#sec-photon">Diffraction and Loss</a></li>
    <li class="toc-sub" data-section="sec-photon"><a href="#sec-photon">Microradian Pointing</a></li>
    <li data-section="sec-hardware"><a href="#sec-hardware">5. Catching and Clocking</a></li>
    <li class="toc-sub" data-section="sec-hardware"><a href="#sec-hardware">Detectors</a></li>
    <li class="toc-sub" data-section="sec-hardware"><a href="#sec-hardware">Doppler and Timing</a></li>
    <li data-section="sec-sky"><a href="#sec-sky">6. The Sky Gets a Vote</a></li>
    <li class="toc-sub" data-section="sec-sky"><a href="#sec-sky">Daylight, Cloud, Turbulence</a></li>
    <li data-section="sec-trust"><a href="#sec-trust">7. Whom Do You Trust?</a></li>
    <li class="toc-sub" data-section="sec-trust"><a href="#sec-trust">Trusted Nodes</a></li>
    <li class="toc-sub" data-section="sec-trust"><a href="#sec-trust">Quantum Hacking</a></li>
    <li data-section="sec-numbers"><a href="#sec-numbers">8. The Numbers</a></li>
    <li data-section="sec-debate"><a href="#sec-debate">9. Is It Worth It?</a></li>
    <li data-section="sec-next"><a href="#sec-next">10. What Comes Next</a></li>
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
  var sections = ['abstract','sec-why','sec-history','sec-how','sec-photon','sec-hardware','sec-sky','sec-trust','sec-numbers','sec-debate','sec-next','sec-glossary','references'];
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
