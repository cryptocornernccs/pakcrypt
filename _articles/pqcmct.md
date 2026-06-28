---
layout: post
title: "On PQC Certificates"
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

/* ─── CSS Variables (dark-theme) ────────────────────────────────── */
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
.ckp-body ul, .ckp-body ol {
  margin: 0 0 1.3rem;
  padding-left: 1.4rem;
}
.ckp-body li { margin-bottom: 0.5rem; }

/* Drop cap */
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
  margin: 0 0 0.9rem;
  color: var(--text-muted);
  font-style: italic;
}
.ckp-abstract p:last-child { margin-bottom: 0; }
.ckp-abstract .pull {
  border-left: 2px solid var(--accent);
  padding-left: 0.9rem;
  color: #dcdce0;
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
  font-size: 1.7rem;
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
.ckp-chain { margin: 2rem 0; }
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
  min-width: 520px;
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
.ckp-table .num { text-align: right; font-family: var(--font-mono); }

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
.ckp-refs a { color: var(--blue); text-decoration: none; border-bottom: 1px solid transparent; }
.ckp-refs a:hover { border-color: var(--blue); }

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
.ckp-hero     { animation: ckp-fade-in 0.6s ease both; }
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

/* ─── Code & Pre ─────────────────────────────────────────────────── */
code {
  font-family: var(--font-mono);
  font-size: 0.85em;
  background: var(--surface);
  border: 1px solid var(--border);
  padding: 0.1em 0.35em;
  color: var(--blue);
}
pre {
  font-family: var(--font-mono);
  font-size: 0.83rem;
  line-height: 1.65;
  background: var(--surface);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  padding: 1.2rem 1.5rem;
  overflow-x: auto;
  color: var(--text);
  margin: 1.5rem 0;
}
pre code { background: none; border: none; padding: 0; color: inherit; }
</style>

<div id="ckp-progress"></div>

<article class="ckp-article">

<!-- ═══════════════════ HERO ═══════════════════════════════════ -->
<div class="ckp-hero">
  <div class="ckp-kicker">Post-Quantum Cryptography · TLS Infrastructure · Merkle Tree Certificates</div>
  <h1>Uncharted Territory of <em>PQC</em>: Quantum Certificates</h1>
  <p class="ckp-deck">A field briefing on post-quantum TLS, certificate size, Merkle Tree Certificates, and the fork forming between the Web PKI and private PKI — written for professionals entering the industry, by someone who has to make these decisions for a living.</p>
  <div class="ckp-meta">
    <span>Sara Malik · PakCrypt</span>
    <span class="dot"></span>
    <span>PQC Migration Series · CTO Field Notes · 2026</span>
    <span class="dot"></span>
    <span>~30 min read</span>
  </div>
</div>

<!-- Keywords -->
<div class="ckp-keywords">
  <span class="ckp-kw">Post-Quantum Cryptography</span>
  <span class="ckp-kw">X.509</span>
  <span class="ckp-kw">ML-DSA</span>
  <span class="ckp-kw">Merkle Tree Certificates</span>
  <span class="ckp-kw">TLS 1.3</span>
  <span class="ckp-kw">Certificate Transparency</span>
  <span class="ckp-kw">DNS SVCB</span>
</div>

<!-- Mobile TOC -->
<div class="ckp-mobile-toc" id="ckp-mob-toc-toggle">
  <span>Contents</span><span>▾</span>
</div>
<div class="ckp-mobile-toc-list" id="ckp-mob-toc-list">
  <a href="#abstract">Abstract</a>
  <a href="#sec-kex">1. Why Key Exchange Moved First</a>
  <a href="#sec-history">2. A Short History of Prior Transitions</a>
  <a href="#sec-size">3. The Size Problem, With Correct Numbers</a>
  <a href="#sec-mtc">4. Merkle Tree Certificates</a>
  <a href="#sec-bill">5. The Bill Nobody Itemized Yet</a>
  <a href="#sec-industry">6. Where the Industry Is Actually Going</a>
  <a href="#sec-forecast">7. Five Years Out: A Forecast</a>
  <a href="#sec-practical">8. What This Means Practically</a>
  <a href="#sec-glossary">Quick Reference Glossary</a>
  <a href="#sec-references">References</a>
</div>

<!-- ═══════════════════ LAYOUT ════════════════════════════════ -->
<div class="ckp-layout">

<!-- ─── Main Body ─────────────────────────────────────────── -->
<div class="ckp-body">

<!-- ABSTRACT -->
<div class="ckp-abstract" id="abstract">
  <div class="ckp-abstract-label">Abstract</div>
  <p>This blog explains where post-quantum certificate infrastructure actually stands today. It is written for people new to the field who need a working mental model before they make their first design decision on a production system.</p>
  <p>We cover four things in order. First, why the industry moved on key exchange before it moved on signatures, and why that is not the same problem solved twice. Second, the concrete arithmetic of certificate and handshake size under classical, lattice-based, and Merkle Tree Certificate schemes, with corrected numbers and worked examples. Third, the new operational dependencies — landmark distribution, DNS-based discovery, dual-certificate serving — that nobody fully solved before announcing a roadmap. Fourth, a five-year outlook on where the Web PKI, private PKI, and the algorithms underneath them are likely to diverge, and what that divergence will cost the people running infrastructure.</p>
  <p class="pull">The themes here are not new. Every cryptographic transition this industry has lived through — DES to AES, MD5 to SHA-2, RSA to ECC — eventually exposed the same lesson: the math is rarely the hard part. We will return to that point throughout.</p>
</div>

<!-- STATS BAR -->
<div class="ckp-stat-row">
  <div class="ckp-stat"><span class="stat-num">544 B</span><span class="stat-label">Classical baseline (ECDSA P-256/P-384 chain)</span></div>
  <div class="ckp-stat"><span class="stat-num">14,724 B</span><span class="stat-label">Traditional X.509 chain, ML-DSA-44 throughout</span></div>
  <div class="ckp-stat"><span class="stat-num">4,468 B</span><span class="stat-label">Landmark-relative MTC, ML-DSA-44</span></div>
  <div class="ckp-stat"><span class="stat-num">8.2×</span><span class="stat-label">Best-case PQC multiple over the classical baseline</span></div>
</div>

<!-- ─── SECTION 1 ─────────────────────────────────────────── -->
<section id="sec-kex">
<h2>1. Why Key Exchange Moved First</h2>

<h3>1.1 The Threat Model Is Asymmetric, and That Asymmetry Drove the Roadmap</h3>

<p class="drop-cap">Post-quantum migration did not arrive as one project. It arrived as two projects running at different speeds, because the two halves of TLS face different clocks.</p>

<p><strong>Key exchange</strong> protects confidentiality. An adversary who records encrypted traffic today and later acquires a cryptographically relevant quantum computer (CRQC) can decrypt that traffic retroactively, because the session key was derived from a key exchange that a CRQC can break after the fact. This is the "harvest now, decrypt later" threat, and it is live today — traffic captured this afternoon is already at risk for whatever its confidentiality window turns out to be. If you operate infrastructure that protects secrets with a shelf life longer than "however many years until a CRQC exists," you have already lost some of those secrets to an adversary patient enough to wait.</p>

<p><strong>Authentication</strong> protects integrity, and integrity does not have the same retroactive failure mode. A signature forged after the fact is useless to an adversary that needed to forge it <em>during</em> a live handshake, three years ago, to impersonate a server in real time. You cannot harvest a signature today and use it to retroactively convince a 2023 client that it was talking to a legitimate server. The signature problem only matters once a CRQC actually exists and is used live against a connection happening <em>then</em>.</p>

<div class="ckp-callout key">
  <strong>Key Concept: Why "harvest now" doesn't apply to signatures</strong>
  <p>Confidentiality is broken by a future attacker reading something recorded in the past. Authentication is broken by a present attacker forging something used right now. A CRQC arriving in year N breaks all key exchanges recorded since day one. It only breaks signatures created from year N onward. This is the single fact that explains the entire shape of the current migration.</p>
</div>

<p>This is why the industry's <em>immediate</em> deployment focus is the hybrid key exchange <code>X25519MLKEM768</code>, and not certificate signature replacement. It is also why this is correct prioritization rather than an arbitrary choice.</p>

<h3>1.2 What X25519MLKEM768 Actually Is, and What It Requires</h3>

<p><code>X25519MLKEM768</code> is a named group for TLS 1.3 key exchange, standardized through the IETF TLS working group, that concatenates an X25519 elliptic-curve Diffie-Hellman exchange with an ML-KEM-768 key encapsulation exchange. The hybrid approach combines both mechanisms so that the session key is derived from both exchanges — if either algorithm is broken, a classical attack on ML-KEM or a CRQC applied to X25519, the session remains secure because the other exchange is still sound. The IANA codepoint is <code>0x11ec</code>.</p>

<p>Three things make this deployable <em>immediately</em>, in a way certificate signature migration is not:</p>

<ul>
  <li><strong>No certificate management.</strong> Key exchange happens fresh, in-band, on every handshake. The server does not need a certificate that says "I support ML-KEM" — it just needs a TLS stack that offers the named group. There is no chain of trust to rebuild, no CA to involve, no root store to update.</li>
  <li><strong>No interoperability cliff.</strong> A hybrid group degrades gracefully. If one side does not support it, the connection falls back to a classical group. Nothing breaks; you simply do not yet have post-quantum protection on that connection.</li>
  <li><strong>Already shipped.</strong> X25519MLKEM768 is the default for Chrome 131+, Firefox 132+, and Edge 131+, accounting for roughly 95% of post-quantum TLS traffic observed today. Server-side, OpenSSL 3.5, NGINX, HAProxy, and the JDK 27 early-access builds all carry support, the last enabling it by default so that TLS clients offer both a hybrid X25519MLKEM768 key share and a traditional x25519 key share without requiring any application code changes.</li>
</ul>

<p>You can, in fact, turn this on today, on a server you control, and the next browser visit will very likely use it. That is rare in this industry. Treat it as the easy half of the migration, not the whole migration.</p>

<h3>1.3 What This Hybrid Does Not Address</h3>

<p>It is worth being precise about scope, because vendors are not always precise about scope when they say "post-quantum ready."</p>

<ul>
  <li><strong>It does not protect authentication.</strong> The server's certificate is still signed with ECDSA or RSA. A CRQC that exists at connection time can still forge that signature and run a live man-in-the-middle attack, hybrid key exchange notwithstanding. Confidentiality and authenticity are independent properties; this migration only buys you the first.</li>
  <li><strong>It does not address signed software, code-signing, or document signatures</strong>, all of which depend on the same vulnerable signature algorithms and have their own, separately unaddressed harvest-now risk for long-lived artifacts.</li>
  <li><strong>It is not "quantum-proof."</strong> ML-KEM is a newer algorithm with a shorter public cryptanalytic record than X25519. The hybrid construction exists specifically because confidence in ML-KEM alone is not yet considered sufficient by the IETF for general deployment during this transition period. You are buying defense in depth against two different failure modes, not certainty against either.</li>
  <li><strong>FIPS compliance has a wrinkle.</strong> In the U.S. FIPS validation regime, ML-KEM is FIPS-approved but X25519 is not, which makes SecP256r1MLKEM768 — not X25519MLKEM768 — the strictly FIPS-compliant hybrid, and Chrome does not ship that variant by default. If you are in a regulated environment, check which named group your compliance posture actually requires before assuming "we enabled PQC" closes that box.</li>
</ul>

<p>The remainder of this paper is about the half of the problem this hybrid does not touch: certificate signatures, and the size, infrastructure, and governance consequences of replacing them.</p>
</section>

<div class="ckp-sep">Historical Pattern</div>

<!-- ─── SECTION 2 ─────────────────────────────────────────── -->
<section id="sec-history">
<h2>2. A Short History of "The Last Time We Did This"</h2>

<p>Anyone surprised by the current confusion has not been paying attention to how every previous cryptographic transition in this industry actually went. A brief recap, because the present moment rhymes with all of it.</p>

<h3>2.1 DSA and the Early X.509 Era</h3>

<p>X.509 itself dates to 1988, designed for a world of small, centrally-issued directories, not a billion-endpoint public internet. DSA, standardized by NIST in 1994, was itself a product of a contentious, multi-year standardization process with public disputes over patent claims and design rationale — the pattern of "the algorithm exists before the deployment story does" is not new.</p>

<h3>2.2 The RSA-to-ECC Transition Took Over a Decade, and Most of the Delay Was Not Cryptographic</h3>

<p>NIST recommended elliptic curve cryptography as early as the late 1990s, and ECC offered smaller keys and faster operations than RSA at equivalent security levels from the start. Yet RSA remained the dominant Web PKI signature algorithm well into the 2010s. The holdup was never "is ECC secure" — it was: hardware support in embedded devices, legacy client compatibility, certificate authority tooling, patent uncertainty around specific curve implementations, and the simple fact that nobody wants to be the first CA to issue a certificate type half the internet cannot validate. ECC adoption accelerated only once browsers, then CAs, then enterprise software all independently decided the compatibility risk had become acceptable — a coordination problem, not a math problem.</p>

<h3>2.3 Certificate Transparency Was Bolted On, Not Designed In</h3>

<p>Certificate Transparency (CT), and the Signed Certificate Timestamps (SCTs) every TLS handshake now carries, exist because the CA ecosystem suffered real, damaging mis-issuance incidents that public logging was retrofitted to detect. CT was not part of the original X.509 design; it is a patch, applied after the trust model already existed, and it shows: SCTs add bytes to every handshake to solve a governance problem the original certificate format never anticipated. This matters directly to our topic, because Merkle Tree Certificates are explicitly designed to fold CT <em>into</em> issuance from the start rather than bolt it on afterward — a deliberate correction of this exact historical mistake.</p>

<div class="ckp-callout">
  <strong>The Pattern, Stated Once</strong>
  <p>In every prior transition, the new algorithm was technically ready years before the ecosystem was operationally ready. The gap was always filled with patches — hybrid modes, transparency logs, deprecation timelines — bolted onto a system that was not designed to anticipate them. We are watching this happen again, in real time, with PQC certificates. The useful skill is not predicting which algorithm wins; it is recognizing which operational dependency is about to get bolted on next.</p>
</div>
</section>

<div class="ckp-sep">Size Arithmetic</div>

<!-- ─── SECTION 3 ─────────────────────────────────────────── -->
<section id="sec-size">
<h2>3. The Size Problem, With Correct Numbers</h2>

<h3>3.1 Reference Sizes for Classical and Post-Quantum Signature Schemes</h3>

<p>Before doing handshake arithmetic, fix the per-algorithm numbers. These are the values specified in FIPS 204 for ML-DSA, and standard reference values for the classical algorithms.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr>
    <th>Algorithm</th>
    <th>Security Level</th>
    <th class="num">Public Key (bytes)</th>
    <th class="num">Signature (bytes)</th>
  </tr>
</thead>
<tbody>
  <tr><td>ECDSA P-256</td><td>~128-bit classical</td><td class="num">64</td><td class="num">64</td></tr>
  <tr><td>ECDSA P-384</td><td>~192-bit classical</td><td class="num">96</td><td class="num">96</td></tr>
  <tr><td>RSA-2048</td><td>~112-bit classical</td><td class="num">256</td><td class="num">256</td></tr>
  <tr><td><span class="term">ML-DSA-44</span></td><td>NIST Level 1 (≈128-bit)</td><td class="num">1,312</td><td class="num">2,420</td></tr>
  <tr><td><span class="term">ML-DSA-65</span></td><td>NIST Level 3 (≈192-bit)</td><td class="num">1,952</td><td class="num">3,293</td></tr>
  <tr><td><span class="term">ML-DSA-87</span></td><td>NIST Level 5 (≈256-bit)</td><td class="num">2,592</td><td class="num">4,627</td></tr>
</tbody>
</table>
</div>

<p>A few things jump out immediately. Going from ML-DSA-44 to ML-DSA-87 — the natural choice if you actually want 256-bit-class assurance rather than the minimum NIST level — roughly doubles both public key and signature size again, on top of an already roughly 20-to-40-times increase over ECDSA. Almost every public size comparison you will find online quotes ML-DSA-44 numbers, because it is the smallest option, and that quietly understates the cost of higher-assurance deployments. If your organization's risk posture calls for ML-DSA-65 or ML-DSA-87 — and several signals below suggest serious institutions are heading exactly there — multiply the size problem accordingly before you trust a vendor's slide that only shows Level 1 figures.</p>

<h3>3.2 What a TLS 1.3 Handshake Actually Needs to Authenticate a Server</h3>

<p>To authenticate a server, the client must validate, at minimum:</p>

<ul>
  <li>A <strong>leaf certificate</strong>: the server's public key, signed by the intermediate CA.</li>
  <li><strong>Two or more SCTs</strong>: each one a signature from a CT log operator, attesting the leaf certificate was logged.</li>
  <li>An <strong>intermediate certificate</strong>: the intermediate's public key, signed by the root CA.</li>
  <li>A <strong>transcript signature</strong>: the server's live signature over the handshake transcript, proving possession of the leaf private key — this is what actually authenticates <em>this</em> connection, as opposed to the certificate, which only authenticates the binding between identity and public key.</li>
</ul>

<p>So the inventory of cryptographic material crossing the wire is: 1 leaf public key + 1 transcript signature + 2 SCT signatures + 1 intermediate public key + 1 intermediate signature (by the root) + 1 leaf-certificate signature (by the intermediate) — that is 2 public keys and 5 signatures, 7 cryptographic objects in total. This matches the figure independently reported in coverage of Let's Encrypt's roadmap announcement: a typical TLS handshake today transmits about 1,248 bytes of authentication data across five signatures and two public keys.</p>

<h3>3.3 Worked Arithmetic: Classical Algorithms</h3>

<p>Using a P-256 leaf under a P-384 intermediate, the numbers check out:</p>

<pre><code>Leaf public key (P-256):             64
Transcript signature (P-256):        64
2 × SCT signature (P-256):          128
Intermediate public key (P-384):     96
Intermediate→root signature (P-384): 96
Leaf signature, by intermediate:     96
                                    -----
Total:                              544 bytes</code></pre>

<p>For an all-RSA-2048 chain, with 7 objects at 256 bytes each: <strong>1,792 bytes</strong>. Real-world chains are frequently mixed, so the 544-to-1,792-byte range is a reasonable bound for what the Web PKI costs today in pure authentication material, excluding TCP/TLS record overhead.</p>

<h3>3.4 Worked Arithmetic: ML-DSA-44</h3>

<p>Checking the structure: 2 public keys (leaf + intermediate) and 5 signatures (transcript, 2 SCTs, intermediate-by-root, leaf-by-intermediate) is exactly right, structurally. The arithmetic: <code>2 × 1,312 = 2,624</code>, and <code>5 × 2,420 = 12,100</code>. Sum: <code>2,624 + 12,100 = 14,724 bytes</code>. The independent figure from industry coverage of Let's Encrypt's announcement lands at the same order of magnitude: replacing today's roughly 1,248 bytes of authentication data with ML-DSA-44 would push that figure past 14,700 bytes.</p>

<p>The consequence is concrete and worth stating in absolute terms. A standard Ethernet MTU is 1,500 bytes. A single round of ML-DSA-44 authentication material alone is roughly ten Ethernet frames. The initial TCP congestion window on many stacks (10 segments, per RFC 6928) is barely enough to carry this handshake's authentication data, before you even add the ML-KEM-768 key exchange material, the TLS record headers, extensions, or anything else. This is not a rounding error. It is a structural problem for TLS as currently engineered, which is exactly why the industry did not simply ship ML-DSA into existing X.509 chains and call the problem solved.</p>

<h3>3.5 Higher Assurance Levels Make This Worse, Not Better</h3>

<p>If you redo this arithmetic at ML-DSA-65 (<code>2 × 1,952 + 5 × 3,293 = 20,369 bytes</code>) or ML-DSA-87 (<code>2 × 2,592 + 5 × 4,627 = 28,319 bytes</code>), the picture deteriorates further. This is the comparison the industry's size discussions mostly skip, and it is exactly the comparison an organization choosing a long-lived root CA key needs to make, because root keys are typically provisioned for the highest assurance level the organization can justify, not the cheapest one.</p>
</section>

<div class="ckp-sep">Merkle Trees</div>

<!-- ─── SECTION 4 ─────────────────────────────────────────── -->
<section id="sec-mtc">
<h2>4. Merkle Tree Certificates: What They Actually Buy You</h2>

<h3>4.1 The Core Idea</h3>

<p>Under the Merkle Tree Certificate model, a Certification Authority signs a single "Tree Head" representing potentially millions of certificates, and the certificate sent to the browser is a lightweight proof of inclusion in that tree. Instead of paying a full signature's cost for every single certificate, you pay it once, for an entire batch, and every certificate in that batch carries only a small, logarithmically-sized proof that it belongs to the batch the CA already vouched for.</p>

<p>This is the single design idea behind every number improvement described below, and it generalizes a tool the industry already trusts: it is the same Merkle-tree inclusion-proof construction that underlies Certificate Transparency itself, applied to the certificate's own existence rather than bolted on afterward as a separate log.</p>

<h3>4.2 Standalone MTCs</h3>

<p>A standalone MTC needs: 1 transcript signature (2,420 bytes at ML-DSA-44), 1 public key (1,312 bytes), 1 inclusion proof (384 bytes, for the specific tree depth assumed), and 2 or more co-signatures from independent witnesses (2 × 2,420 = 4,840 bytes). Total: <code>2,420 + 1,312 + 384 + 4,840 = 8,956 bytes</code>.</p>

<p>This is meaningfully better than 14,724 bytes — a roughly 39% reduction — but it is still over sixteen times the size of the 544-byte classical baseline. The co-signatures are still the dominant cost, because a standalone MTC still has to convince the client, on the spot, that the witnesses actually vouched for this particular tree head.</p>

<h3>4.3 Landmark-Relative MTCs</h3>

<p>The improvement comes from removing the co-signatures from the live handshake entirely. Replacing per-certificate signatures with compact hash-based inclusion proofs, the architecture shrinks quantum-resistant TLS authentication data from roughly 14,700 bytes down to as little as 736 bytes. If the client already trusts a recent landmark — a periodically co-signed tree head it obtained out of band, independent of this specific connection — the server need only send a transcript signature, a public key, and an inclusion proof relative to that already-trusted landmark.</p>

<p>The numbers — <code>2,420 + 1,312 + 736 = 4,468 bytes</code> — are internally consistent with this model and with the 736-byte figure reported as Google's headline result for the landmark-relative case. Note that the 736-byte inclusion proof assumes a specific landmark cadence (hourly, on the order of millions of certificates per landmark, roughly 23 hashes deep); change that cadence and the proof size moves logarithmically, not linearly, so this number is sensitive to operational choices CAs haven't all finalized yet.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead>
  <tr>
    <th>Scheme</th>
    <th class="num">Auth Bytes</th>
    <th class="num">Multiple of Classical (544 B)</th>
  </tr>
</thead>
<tbody>
  <tr><td>ECDSA P-256 / P-384 chain (classical baseline)</td><td class="num">544</td><td class="num">1×</td></tr>
  <tr><td>RSA-2048 chain</td><td class="num">1,792</td><td class="num">3.3×</td></tr>
  <tr><td>Traditional X.509, ML-DSA-44 throughout</td><td class="num">14,724</td><td class="num">27×</td></tr>
  <tr><td>Standalone MTC, ML-DSA-44</td><td class="num">8,956</td><td class="num">16.5×</td></tr>
  <tr><td><span class="term">Landmark-relative MTC, ML-DSA-44</span></td><td class="num">4,468</td><td class="num">8.2×</td></tr>
</tbody>
</table>
</div>

<h3>4.4 The Honest Framing: MTCs Are an Enormous Improvement and Still Not Free</h3>

<p>8.2 times the byte cost of a classical handshake is genuinely good engineering, given the constraint that one must use a NIST-standardized post-quantum signature somewhere in the chain. It is not, however, "as small as classical," and treating it as solved would be premature. Every operational dependency described in Section 5 exists specifically to make that 736-byte number achievable in practice, and none of those dependencies are fully built yet.</p>
</section>

<div class="ckp-sep">Operational Debt</div>

<!-- ─── SECTION 5 ─────────────────────────────────────────── -->
<section id="sec-bill">
<h2>5. The Bill Nobody Itemized Yet</h2>

<p>Reducing a number on a slide and operating a working system at internet scale are different achievements. Here is what landmark-relative MTCs actually require, none of which is optional if one wants the 4,468-byte figure rather than the 8,956-byte fallback.</p>

<h3>5.1 Issuance Delay</h3>

<p>Landmark-relative MTCs are signed in batches against a periodic landmark, not on demand. That means certificate issuance is no longer instantaneous in the way a same-day Let's Encrypt ECDSA certificate is today. The industry has not yet published hard numbers on what that delay will be in production; "assume it's short" is a reasonable working assumption for now, but it is an assumption, not a specification, and anyone designing automated certificate issuance pipelines (ACME-style, just-in-time, ephemeral) needs to track this number specifically as it firms up.</p>

<h3>5.2 Landmark Discovery Without an Extra Round Trip</h3>

<p>A client needs to know, before it connects, which landmark a given server's certificate chain will be relative to — different CAs produce different landmarks, the way different root programs trust different root certificates today. Discovering this by asking the server first would cost an extra round trip on every connection, which defeats much of the size win. The mechanism the industry has converged on for this is TLS Trust Anchor Identifiers, advertised via the <code>tls-trust-anchors</code> parameter on HTTPS or SVCB DNS records, so the client can compute the intersection between its configured trust anchors and the server's available ones before initiating the handshake at all.</p>

<p>This is a real new dependency. SVCB and HTTPS DNS record types (RFC 9460) are still inconsistently supported across resolvers, stub libraries, and middleboxes. If an organization's DNS infrastructure does not yet resolve and parse these record types reliably, that is now squarely in scope for any PQC migration plan.</p>

<h3>5.3 Servers Need to Support Both Standalone and Landmark-Relative Certificates, Simultaneously</h3>

<p>A server cannot assume every client presents a fresh landmark. Clients may have no landmark at all, or an outdated one the server no longer recognizes. The fallback is the standalone MTC — full cost, co-signatures included. That means a production server needs both certificate types provisioned and live at once, plus the logic to atomically pick the right one per ClientHello, plus the operational discipline to rotate and renew both in sync. This roughly doubles the certificate-management surface area compared to a single-certificate world, and it is new complexity, not a simplification, however good the best-case byte count looks.</p>

<h3>5.4 Landmark Freshness Becomes an Operating-System-Level Problem</h3>

<p>Landmarks function as trust anchors — conceptually adjacent to today's root certificate bundle, except landmarks expire and rotate on a much shorter cycle (the example cadence cited above is hourly). Browsers already have infrastructure for pushing frequent updates to internal trust data; most other TLS clients — embedded devices, IoT firmware, language-runtime TLS stacks, command-line tools, internal microservices — do not, and rely on trust bundles that today are updated rarely, sometimes only at OS or package upgrade time.</p>

<p>Making landmark-relative MTCs work universally implies something close to an OS-level or distribution-level landmark-updating service, running continuously, for every platform that wants the smaller certificate. Google's rollout deliberately keeps the Chrome Quantum-resistant Root Store as an addition alongside, not a replacement for, the existing Chrome Root Store — a sensible hedge, but one that also signals Google itself is not assuming this problem is solved outside the browser. Nobody has published a detailed design for "landmark updates for everything that isn't a browser." That is a gap, and it is worth tracking who fills it.</p>

<h3>5.5 The Bifurcation Risk This Creates</h3>

<p>Put 5.2 through 5.4 together, and we get a real risk: browsers — practically, a small number of major browser vendors — solve landmark freshness and discovery for themselves, because they control the update channel and the DNS-aware infrastructure to do it. Everything else — libraries, embedded TLS stacks, internal service mesh implementations, IoT — falls back to standalone MTCs or, worse, stays on classical certificates because nobody ships them a landmark updater. The current rollout phases place initial bootstrapping and CA onboarding for the quantum-resistant root store on a 2027 timeline, run by a small number of organizations setting the technical direction for everyone else. That concentration of design authority is a legitimate governance concern independent of whether the cryptography itself is sound, and it is worth professionals entering this field forming their own view on it rather than treating it as someone else's problem.</p>
</section>

<div class="ckp-sep">Industry Split</div>

<!-- ─── SECTION 6 ─────────────────────────────────────────── -->
<section id="sec-industry">
<h2>6. Where the Industry Is Actually Going</h2>

<h3>6.1 MTC Adoption, With Current Commitments</h3>

<p>On June 3, 2026, Let's Encrypt — the nonprofit certificate authority that secures more than 500 million websites — published its post-quantum roadmap and named Merkle Tree Certificates as its chosen path, targeting a staging environment that issues MTCs in late 2026 and a production-ready environment in 2027. This is the single most consequential adoption signal to date, because Let's Encrypt issued 54.4% of all public SSL/TLS certificates in Q1 2026, meaning its adoption of MTCs essentially makes the standard viable for the majority of the encrypted web, independent of what any other CA decides to do.</p>

<p>Google has stated it has no immediate plan to add traditional X.509 certificates containing post-quantum signatures to the Chrome Root Store, and will instead use a new Chrome Quantum-resistant Root Store and corresponding Root Program that only supports MTCs. Field testing is already under way, with Cloudflare operating roughly one thousand TLS certificates in the experiment, and phase two is planned for Q1 2027, inviting Certificate Transparency log operators that already had a usable log in Chrome before February 1, 2026, to help bootstrap public MTCs, with the CA onboarding framework for the new root program targeted around Q3 2027.</p>

<p>The CA/B Forum — the body that, in principle, sets baseline requirements across the entire commercial CA industry — has, by contrast, moved markedly slower. As of this writing there is no MTC-specific baseline requirement; participant commentary so far amounts to early-stage investigation. This is a real asymmetry in the industry's governance, not a rhetorical flourish: a handful of browser-and-CDN organizations are setting de facto technical direction faster than the cross-industry standards body that nominally governs Web PKI baseline requirements.</p>

<h3>6.2 ML-DSA Adoption Is Moving on a Separate, Slower, and More Conservative Track</h3>

<p>While MTCs target the <em>public</em> Web PKI, ML-DSA itself is being adopted directly — full X.509 certificates, no Merkle tree — in contexts where certificate size matters less than algorithm assurance and where the client population is small and controlled.</p>

<p>Google is adding native ML-DSA support for private PKI use in Chrome, separate from and faster-moving than its public Web PKI plans, which remain MTC-only. Microsoft has signaled support for ML-DSA certificates in CA/B Forum discussions, reportedly leaning toward ML-DSA-87 — the highest, most conservative, and largest-byte-cost security level, consistent with an enterprise posture that prioritizes assurance margin over the byte-count concerns driving the public web's MTC push. The CA/B Forum's Baseline Requirements for S/MIME already permit ML-DSA, ahead of the Web-PKI baseline requirements, which do not yet.</p>

<p>The financial sector has built its own dedicated infrastructure rather than wait: a new X9 Financial PKI, operated by DigiCert, with ML-DSA support built in from the start. This is a sector with both the regulatory mandate and the resources to build bespoke PKI rather than wait for Web PKI consensus, and it has chosen straightforward ML-DSA X.509 certificates over MTCs — a different calculus than Google's, made by a different industry with different constraints (closed client populations, regulatory certainty requirements, less sensitivity to a few extra kilobytes per handshake).</p>

<h3>6.3 The Structural Split, Stated Plainly</h3>

<p>The public Web PKI is converging on Merkle Tree Certificates, driven by Google, Cloudflare, and Let's Encrypt, optimizing for handshake size at internet scale with an open, heterogeneous client population. Private PKI — enterprise, financial-sector, S/MIME — is converging on direct ML-DSA X.509 certificates, optimizing for implementation simplicity and assurance level, in contexts where the client population is closed and controlled and a few extra kilobytes per connection is an acceptable price.</p>

<p>These are not competing proposals where one will eventually win. They are two different answers to two different constraint sets, and both are likely to persist. That has a direct, practical consequence: TLS and HTTPS stacks going forward will need to correctly implement and select between multiple X.509-adjacent certificate formats, not migrate cleanly from one format to a single successor. Budget engineering time accordingly.</p>
</section>

<div class="ckp-sep">Five-Year Forecast</div>

<!-- ─── SECTION 7 ─────────────────────────────────────────── -->
<section id="sec-forecast">
<h2>7. Five Years Out: A Forecast, Not a Promise</h2>

<p>Treat everything in this section as informed extrapolation from current trajectories, not certainty. Cryptographic migrations have a long history of running later than announced, and PQC certificates are unlikely to be the exception.</p>

<div class="ckp-chain">

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">1</div>
    <div class="ckp-chain-content">
      <h4>Key Exchange Will Be Fully Post-Quantum By Default, Broadly</h4>
      <p>Hybrid key exchange is cheap, already deployed at scale, and has no certificate-management dependency. Expect near-universal default-on hybrid key exchange across major browsers, CDNs, and server software well before the certificate-signature problem is anywhere close to resolved. This part of the migration is genuinely close to done.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">2</div>
    <div class="ckp-chain-content">
      <h4>The Public Web PKI Will Be Mid-Transition to MTCs, Not Finished</h4>
      <p>Given the Q3 2027 target for CA onboarding into Chrome's quantum-resistant root program, and the multi-year history of every prior CA ecosystem transition (the ECC migration took over a decade; CT enforcement took years to reach universal logging), expect partial MTC deployment by major CDN-fronted sites, with the long tail of the Web PKI still on classical or transitional certificates. Full MTC ubiquity in five years is optimistic; meaningful MTC presence among the highest-traffic sites is realistic.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">3</div>
    <div class="ckp-chain-content">
      <h4>Private PKI Will Have Moved Faster, and More Unevenly, Than the Public Web</h4>
      <p>Financial services, defense, and other regulated sectors with mandate-driven timelines and controlled client populations will likely have completed ML-DSA migrations for new infrastructure well before the Web PKI's MTC rollout matures, simply because their constraint set is simpler: no anonymous client population, no DNS-discovery problem, often no requirement to interoperate with arbitrary external software.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">4</div>
    <div class="ckp-chain-content">
      <h4>Landmark Distribution Will Be the Long Pole, and Possibly the Source of the Next Visible Failure</h4>
      <p>Watch specifically for whether non-browser TLS clients — package managers, IoT firmware, internal service meshes, embedded libraries — get a credible landmark-update mechanism. If they don't, by year five expect either widespread silent fallback to standalone MTCs or, in the worst case, a security incident traceable to stale landmark data being trusted past its intended freshness window. This is the single most under-specified piece of the entire architecture today, and it is worth professionals tracking closely rather than assuming someone else has it handled.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">5</div>
    <div class="ckp-chain-content">
      <h4>SVCB/HTTPS DNS Record Support Will Become a Quiet Prerequisite for PQC Readiness</h4>
      <p>Organizations that have not modernized their DNS infrastructure to reliably serve and resolve these record types will find that gap blocking landmark discovery, independent of how ready their TLS stack otherwise is. This is exactly the kind of unglamorous dependency that derails migration timelines, the same way legacy hardware TLS termination quietly delayed the RSA-to-ECC transition for years in some sectors.</p>
    </div>
  </div>

  <div class="ckp-chain-item">
    <div class="ckp-chain-num">6</div>
    <div class="ckp-chain-content">
      <h4>The Web PKI and Private PKI Will Not Re-Converge Within Five Years</h4>
      <p>The constraint sets driving MTCs (public, open, byte-sensitive) and direct ML-DSA (private, controlled, assurance-sensitive) are structural, not incidental, and nothing on the current roadmap suggests they merge. Expect the bifurcation Section 6.3 describes to be a permanent feature of the landscape professionals in this field need to know how to navigate, not a temporary transitional artifact.</p>
    </div>
  </div>

</div>
</section>

<div class="ckp-sep">Practical Guidance</div>

<!-- ─── SECTION 8 ─────────────────────────────────────────── -->
<section id="sec-practical">
<h2>8. What This Means Practically</h2>

<p>For someone entering information security today, a few concrete, actionable takeaways, separate from the forecasting above:</p>

<ul class="ckp-hier">
  <li><strong>Enable hybrid key exchange now.</strong> It is low-risk, already supported broadly, and addresses a live threat (harvest-now-decrypt-later) that is accruing cost every day we delay. There is no good reason for a production TLS server to not be offering <code>X25519MLKEM768</code> today.</li>
  <li><strong>Do not conflate "we enabled hybrid key exchange" with "we are post-quantum ready."</strong> Authentication is still classical almost everywhere. Be precise about which half of the problem any given deployment has actually addressed when we report status upward.</li>
  <li><strong>If you operate DNS infrastructure, start testing SVCB/HTTPS record support now.</strong> This dependency is easy to deprioritize because it looks unrelated to cryptography, and that is exactly why it will be underestimated until it becomes a blocker.</li>
  <li><strong>If you are choosing a security level for a long-lived key (root CA, code-signing, anything provisioned for a decade or more), do the size arithmetic at ML-DSA-65 or ML-DSA-87, not just ML-DSA-44.</strong> Most public comparisons quote the smallest, cheapest option; your risk tolerance for a long-lived key is probably not the smallest, cheapest option.</li>
  <li><strong>Track Let's Encrypt's staging MTC environment as the most concrete, observable bellwether.</strong> A nonprofit CA issuing the majority of public certificates committing to a late-2026 staging timeline is a far more reliable signal of real progress than any vendor announcement.</li>
  <li><strong>Remember Shamir's observation, because it will be true again here.</strong> The largest practical risk in this entire transition is probably not a cryptographic break. It is operational complexity — dual-certificate handling, stale landmarks, misconfigured DNS, a fallback path nobody tested — creating a bypass that has nothing to do with whether ML-DSA or MTCs are mathematically sound.</li>
</ul>

<div class="ckp-pull">
  <p>Cryptography is typically bypassed, not penetrated.</p>
  <cite>— Adi Shamir</cite>
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
    <td><span class="term">Harvest now, decrypt later</span></td>
    <td>Recording encrypted traffic today to decrypt retroactively once a quantum computer capable of breaking the key exchange exists.</td>
  </tr>
  <tr>
    <td><span class="term">ML-KEM</span></td>
    <td>Module-Lattice-Based Key Encapsulation Mechanism, FIPS 203, the NIST-standardized post-quantum key exchange algorithm used in hybrid TLS groups.</td>
  </tr>
  <tr>
    <td><span class="term">ML-DSA</span></td>
    <td>Module-Lattice-Based Digital Signature Algorithm, FIPS 204, the NIST-standardized post-quantum signature algorithm, formerly CRYSTALS-Dilithium.</td>
  </tr>
  <tr>
    <td><span class="term">Hybrid key exchange</span></td>
    <td>A TLS key exchange combining a classical algorithm (e.g. X25519) with a post-quantum one (e.g. ML-KEM-768), so security holds if either alone is broken.</td>
  </tr>
  <tr>
    <td><span class="term">SCT</span></td>
    <td>Signed Certificate Timestamp; a signature from a Certificate Transparency log attesting a certificate was publicly logged.</td>
  </tr>
  <tr>
    <td><span class="term">Merkle Tree Certificate (MTC)</span></td>
    <td>An experimental certificate format in which a CA signs one tree head covering many certificates, and each certificate is authenticated by a compact inclusion proof rather than its own full signature.</td>
  </tr>
  <tr>
    <td><span class="term">Landmark</span></td>
    <td>A periodically co-signed MTC tree head that a client has already obtained and trusts, allowing a server to send only a small inclusion proof relative to it instead of full co-signatures.</td>
  </tr>
  <tr>
    <td><span class="term">PLANTS</span></td>
    <td>The IETF working group ("PKI, Logs, And Tree Signatures") standardizing the MTC specification.</td>
  </tr>
  <tr>
    <td><span class="term">SVCB / HTTPS DNS records</span></td>
    <td>RFC 9460 DNS record types allowing a server to advertise service parameters — including, via TLS Trust Anchor Identifiers, which certificate trust anchors it supports — before a TLS handshake begins.</td>
  </tr>
  <tr>
    <td><span class="term">CQRS</span></td>
    <td>Chrome Quantum-resistant Root Store, Google's planned new Chrome root program supporting only MTCs.</td>
  </tr>
</tbody>
</table>
</div>
</section>

<!-- ─── REFERENCES ─────────────────────────────────────────── -->
<div class="ckp-refs" id="sec-references">
<h2>References</h2>
<p id="ref-1"><span class="ref-num">[1]</span> JEP 527: Post-Quantum Hybrid Key Exchange for TLS 1.3. OpenJDK. <a href="https://openjdk.org/jeps/527">openjdk.org/jeps/527</a></p>
<p id="ref-2"><span class="ref-num">[2]</span> Kwiatkowski, K., Kampanakis, P., Westerbaan, B.E., Stebila, D. <em>Post-quantum hybrid ECDHE-MLKEM Key Agreement for TLSv1.3</em>. IETF Internet-Draft, draft-ietf-tls-ecdhe-mlkem. <a href="https://datatracker.ietf.org/doc/draft-ietf-tls-ecdhe-mlkem/">datatracker.ietf.org</a></p>
<p id="ref-3"><span class="ref-num">[3]</span> <em>Hybrid key exchange in TLS 1.3</em>. IETF Internet-Draft, draft-ietf-tls-hybrid-design. <a href="https://datatracker.ietf.org/doc/html/draft-ietf-tls-hybrid-design">datatracker.ietf.org</a></p>
<p id="ref-4"><span class="ref-num">[4]</span> NIST. <em>FIPS 204: Module-Lattice-Based Digital Signature Standard</em>. <a href="https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.204.ipd.pdf">nvlpubs.nist.gov</a></p>
<p id="ref-5"><span class="ref-num">[5]</span> <em>Internet X.509 Public Key Infrastructure: Algorithm Identifiers for ML-DSA</em>. IETF Internet-Draft, draft-ietf-lamps-dilithium-certificates. <a href="https://www.ietf.org/archive/id/draft-ietf-lamps-dilithium-certificates-07.html">ietf.org</a></p>
<p id="ref-6"><span class="ref-num">[6]</span> <em>Google Develops Merkle Tree Certificates to Enable Quantum-Resistant HTTPS in Chrome</em>. The Hacker News, March 2026. <a href="https://thehackernews.com/2026/03/google-develops-merkle-tree.html">thehackernews.com</a></p>
<p id="ref-7"><span class="ref-num">[7]</span> <em>Merkle Tree Certificates: Rethinking the WebPKI for the Post-Quantum Era</em>. Encryption Consulting. <a href="https://www.encryptionconsulting.com/about-merkle-tree-certificates/">encryptionconsulting.com</a></p>
<p id="ref-8"><span class="ref-num">[8]</span> <em>Google's Merkle Tree (MTC) Gambit to Quantum-Proof HTTPS</em>. postquantum.com, April 2026. <a href="https://postquantum.com/security-pqc/googles-merkle-tree-mtc-https/">postquantum.com</a></p>
<p id="ref-9"><span class="ref-num">[9]</span> <em>Let's Encrypt Commits to Merkle Tree Certificates</em>. postquantum.com. <a href="https://postquantum.com/security-pqc/lets-encrypt-merkle-tree-mtc-post-quantum/">postquantum.com</a></p>
<p id="ref-10"><span class="ref-num">[10]</span> <em>A Post-Quantum Future for Let's Encrypt</em>. Let's Encrypt, June 3, 2026. <a href="https://letsencrypt.org/2026/06/03/pq-certs">letsencrypt.org</a></p>
<p id="ref-11"><span class="ref-num">[11]</span> <em>Google And Cloudflare Pilot Merkle Tree Certificates To Secure Chrome HTTPS Against Post-Quantum Attacks</em>. cybersecurefox.com, March 2026. <a href="https://cybersecurefox.com/en/google-merkle-tree-certificates-post-quantum-chrome/">cybersecurefox.com</a></p>
<p id="ref-12"><span class="ref-num">[12]</span> <em>Google tests Merkle Tree Certificates for quantum web</em>. securitybrief.com.au, March 2026. <a href="https://securitybrief.com.au/story/google-tests-merkle-tree-certificates-for-quantum-web">securitybrief.com.au</a></p>
<p id="ref-13"><span class="ref-num">[13]</span> Beck, et al. <em>TLS Trust Anchor Identifiers</em>. IETF Internet-Draft, draft-ietf-tls-trust-anchor-ids. <a href="https://datatracker.ietf.org/doc/draft-ietf-tls-trust-anchor-ids/">datatracker.ietf.org</a></p>
<p id="ref-14"><span class="ref-num">[14]</span> <em>Hybrid Key Exchange Today: Why X25519 + ML-KEM Is the Interim Default</em>. netguardia.com, April 2026. <a href="https://netguardia.com/privacy/encryption/hybrid-key-exchange-today-why-x25519-ml-kem-is-the-interim-default/">netguardia.com</a></p>
<p id="ref-15"><span class="ref-num">[15]</span> <em>Post-Quantum TLS 1.3 in Production: Deploying X25519+ML-KEM-768 with OpenSSL 3.5, NGINX, and HAProxy</em>. systemshardening.com, May 2026. <a href="https://www.systemshardening.com/articles/network/tls-post-quantum-hybrid-deployment/">systemshardening.com</a></p>
<p id="ref-16"><span class="ref-num">[16]</span> Schwartz, B., Bishop, M., Nygren, E. <em>Service Binding and Parameter Specification via the DNS (SVCB and HTTPS Resource Records)</em>. RFC 9460, November 2023.</p>
</div>

<div class="ckp-pull" style="margin-top: 3rem;">
  <p>This paper reflects the state of post-quantum certificate infrastructure as publicly documented as of June 2026. Several of the timelines cited are vendor-stated targets, not delivered milestones. Treat dates beyond the current quarter as subject to revision, consistent with the historical pattern this paper describes in Section 2.</p>
</div>

</div><!-- end .ckp-body -->

<!-- ─── Sidebar TOC ─────────────────────────────────────────── -->
<aside class="ckp-sidebar">
  <div class="ckp-toc-label">Contents</div>
  <ul class="ckp-toc-list" id="ckp-toc">
    <li data-section="abstract"><a href="#abstract">Abstract</a></li>
    <li data-section="sec-kex"><a href="#sec-kex">1. Why Key Exchange Moved First</a></li>
    <li class="toc-sub" data-section="sec-kex"><a href="#sec-kex">Threat Model</a></li>
    <li class="toc-sub" data-section="sec-kex"><a href="#sec-kex">X25519MLKEM768</a></li>
    <li data-section="sec-history"><a href="#sec-history">2. History of Prior Transitions</a></li>
    <li class="toc-sub" data-section="sec-history"><a href="#sec-history">RSA-to-ECC</a></li>
    <li class="toc-sub" data-section="sec-history"><a href="#sec-history">CT Bolted On</a></li>
    <li data-section="sec-size"><a href="#sec-size">3. The Size Problem</a></li>
    <li class="toc-sub" data-section="sec-size"><a href="#sec-size">Reference Sizes</a></li>
    <li class="toc-sub" data-section="sec-size"><a href="#sec-size">Worked Arithmetic</a></li>
    <li data-section="sec-mtc"><a href="#sec-mtc">4. Merkle Tree Certificates</a></li>
    <li class="toc-sub" data-section="sec-mtc"><a href="#sec-mtc">Standalone vs. Landmark</a></li>
    <li data-section="sec-bill"><a href="#sec-bill">5. The Bill Nobody Itemized</a></li>
    <li class="toc-sub" data-section="sec-bill"><a href="#sec-bill">Issuance · Discovery · Freshness</a></li>
    <li data-section="sec-industry"><a href="#sec-industry">6. Where the Industry Is Going</a></li>
    <li class="toc-sub" data-section="sec-industry"><a href="#sec-industry">MTC vs. ML-DSA Track</a></li>
    <li class="toc-sub" data-section="sec-industry"><a href="#sec-industry">The Structural Split</a></li>
    <li data-section="sec-forecast"><a href="#sec-forecast">7. Five Years Out</a></li>
    <li data-section="sec-practical"><a href="#sec-practical">8. What This Means Practically</a></li>
    <li data-section="sec-glossary"><a href="#sec-glossary">Glossary</a></li>
    <li data-section="sec-references"><a href="#sec-references">References</a></li>
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
  var sections = ['abstract','sec-kex','sec-history','sec-size','sec-mtc','sec-bill','sec-industry','sec-forecast','sec-practical','sec-glossary','sec-references'];
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