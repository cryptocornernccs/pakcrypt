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
<style >
/* ─── Google Fonts ─────────────────────────────────────────────── */
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;0,700;0,900;1, 400;1,700 &family=Source+Serif+4:ital,opsz,wght@0,8..60,300;0,8..60,400;0,8..60,600;1,8..60,300;1,8..60,400 &family=JetBrains+Mono:wght@400;600 &display=swap');

/* ─── CSS Variables (dark-theme aware) ─────────────────────────── */
:root {
--bg:           #1b1b1e;
--surface:      #242428;
--surface2:     #2c2c31;
--border :       #383840;
--text:         #e2e2e4;
--text-muted:   #9898a4;
--accent:       #c9a84c;
--accent-dim:   rgba(201,168,76,0.15);
--accent-glow:  rgba(201,168,76,0.08);
--red:           #e05c5c;
--blue:         #6bb5d6;
--green:        #6dcf94;
--font-serif:   'Source Serif 4', Georgia, serif;
--font-display: 'Playfair Display', Georgia, serif;
--font-mono:     'JetBrains Mono', 'Courier New', monospace;
}

/* ─── Reset  & Layout ───────────────────────────────────────────── */
.ckp-article * { box-sizing: border-box; }
.ckp-article {
font-family: var(--font-serif);
font-size: 1.08rem;
line-height:  1.82;
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
align-items:  center;
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
border-radius: 50% ;
background: var(--border);
display: inline-block;
}
.ckp-meta a {
color: var(--accent);
text-decoration: none;
border-bottom: 1px solid transparent;
transition: border-color 0.2s ;
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
margin:  0;
border-left: 2px solid transparent;
transition: border-color 0.2s;
}
.ckp-toc-list li.active {
border-color: var(--accent);
}
.ckp-toc-list a {
display: block;
padding: 0.35rem  0.75rem;
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

/* ─── Body prose ──────────────────────────────────────────────── */
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
position: relative ;
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
padding:  1.2rem 1.5rem;
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
.ckp-callout.warn  strong { color: #e0935c; }
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
margin-bottom:  0.6rem;
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
content:  '▸';
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
background : var(--surface);
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
text-transform:  none;
letter-spacing: normal;
}
.ckp-chain-content p { margin: 0; font-size: 0.88rem; color: var(--text-muted); }

/* ─── Comparison / Glossary table ───────────────────────────────── */
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
.ckp-table .term { font-family : var(--font-display); font-weight: 700; color: #f0f0f0; }

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
@media (max-width: 700px) { .ckp-refs { columns:  1; } }
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
to   { opacity: 1 ; transform: translateY(0); }
}
.ckp-hero    { animation: ckp-fade-in 0.6s ease both; }
.ckp-abstract { animation: ckp-fade-in 0.6s ease 0.15s both; }

/* ─── Keywords strip ──────────────────────────────────────────── */
.ckp-keywords {
display: flex;
flex-wrap: wrap;
gap: 0.5rem;
margin: 1.5rem 0 2rem;
}
.ckp-kw {
font-family: var(--font-mono);
font-size : 0.68rem;
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
    <div class="ckp-kicker">Cryptographic Engineering · Entropy Sources · RNG Security</div>
    <h1>No Entropy <em>Without a Model</em></h1>
    <p class="ckp-deck">A model-based discipline for entropy sources. Why physical unpredictability and statistical tests are insufficient, and how to rigorously bound conditional min-entropy from first principles.</p>
    <div class="ckp-meta">
        <span>Sara Malik & Naveed A. Aun</span>
        <span class="dot"></span>
        <span>PakCrypt NPO</span>
        <span class="dot"></span>
        <span>~25 min read</span>
    </div>
</div>

<!-- Keywords -->
<div class="ckp-keywords">
    <span class="ckp-kw">Min-Entropy</span>
    <span class="ckp-kw">Stochastic Model</span>
    <span class="ckp-kw">SP 800-90B</span>
    <span class="ckp-kw">AIS 31</span>
    <span class="ckp-kw">QRNG</span>
    <span class="ckp-kw">Side-Channel Leakage</span>
    <span class="ckp-kw">Conditioning</span>
</div>

<!-- Mobile TOC -->
<div class="ckp-mobile-toc" id="ckp-mob-toc-toggle">
    <span>Contents</span> <span>▾</span>
</div>
<div class="ckp-mobile-toc-list" id="ckp-mob-toc-list">
    <a href="#abstract">Abstract</a>
    <a href="#sec-intro">1. The Error of "Unpredictable, Compressed, and Tested"</a>
    <a href="#sec-math">2. From Unpredictability to Conditional Min-Entropy</a>
    <a href="#sec-models">3. Analytical Output Models</a>
    <a href="#sec-health">4. Measurement & Health Tests</a>
    <a href="#sec-leakage">5. Leakage & Side-Channels</a>
    <a href="#sec-accounting">6. Conditioning & Entropy Accounting</a>
    <a href="#sec-quantum">7. The Quantum Case</a>
    <a href="#sec-conclusion">8. Conclusion</a>
    <a href="#references">References</a>
</div>

<!-- ═══════════════════ LAYOUT ════════════════════════════════ -->
<div class="ckp-layout">
    <!-- ─── Main Body ─────────────────────────────────────────── -->
    <div class="ckp-body">
        <!-- ABSTRACT -->
        <div class="ckp-abstract" id="abstract">
            <div class="ckp-abstract-label">Abstract</div>
            <p>Hardware and quantum random number generators are routinely justified by an appeal to physical unpredictability followed by a clean pass through a statistical test battery. We argue that this justification is insufficient. Unpredictability is not a property of an output string; it is a property of an adversary’s uncertainty. The admissible object is a proven lower bound on the conditional min-entropy of the raw source, derived from a stochastic model of the underlying physics, held invariant online by health tests, protected from side-channel leakage, and only then passed to an entropy-preserving conditioner. A conditioner cannot manufacture entropy a model never proved.</p>
        </div>

        <!-- STATS BAR -->
        <div class="ckp-stat-row">
            <div class="ckp-stat"> <span class="stat-num">5</span> <span class="stat-label">Core Obligations</span> </div>
            <div class="ckp-stat"> <span class="stat-num">5</span> <span class="stat-label">Source Classes Analyzed</span> </div>
            <div class="ckp-stat"> <span class="stat-num">+64</span> <span class="stat-label">NIST Conditioning Margin</span> </div>
            <div class="ckp-stat"> <span class="stat-num">$H_\infty$</span> <span class="stat-label">Conditional Min-Entropy</span> </div>
        </div>

        <!-- ─── SECTION 1 ─────────────────────────────────────────── -->
        <section id="sec-intro">
            <h2>1. The Error of "Unpredictable, Compressed, and Tested"</h2>
            <p class="drop-cap">A random number generator that merely looks unpredictable offers a cryptographer little assurance. The clearest illustration is Dual_EC_DRBG. It was standardised in NIST SP 800-90, shipped by default in widely deployed libraries, and passes statistical test batteries without complaint; yet an adversary who knows a secret relation between two curve points can reconstruct the generator’s internal state and predict everything that follows. "Passes the tests" and "is unpredictable to the adversary" are simply different properties.</p>
            
            <div class="ckp-pull">
                <p>Randomness is not a visible feature of a bit string emerging from a black box. It is the gap between what the adversary knows and what the adversary would need to know to predict the next sample.</p>
                <cite>— The core thesis of model-based entropy</cite>
            </div>

            <p>Quantum mechanics provides a ceiling on unpredictability, guaranteeing that an ideal measurement is intrinsically random. But it says nothing about the floor, which is set entirely by how well the real apparatus approximates the ideal and by how much of the observed fluctuation is classical noise the adversary may share. The extractable randomness is the conditional min-entropy of the realised detector event given classical side information.</p>

            <h3>The Five Linked Obligations</h3>
            <p>An entropy claim is admissible if and only if it is the conclusion of the following linked obligations. We replace "unpredictable, compressed, and tested" with "modeled, measured, monitored, margined, and shielded."</p>
            
            <div class="ckp-chain">
                <div class="ckp-chain-item">
                    <div class="ckp-chain-num">1</div>
                    <div class="ckp-chain-content">
                        <h4>Stochastic Model</h4>
                        <p>A model $p(x|\theta)$ of the raw source, derived from device physics, with parameters identified with measurable quantities.</p>
                    </div>
                </div>
                <div class="ckp-chain-item">
                    <div class="ckp-chain-num">2</div>
                    <div class="ckp-chain-content">
                        <h4>Measured Lower Bound</h4>
                        <p>A measured lower confidence bound on the conditional min-entropy per raw sample, obtained on raw, pre-conditioning data.</p>
                    </div>
                </div>
                <div class="ckp-chain-item">
                    <div class="ckp-chain-num">3</div>
                    <div class="ckp-chain-content">
                        <h4>Model-Bound Health Tests</h4>
                        <p>Online tests whose alarm thresholds are computed from the model’s worst-case parameters, proven to fire before entropy falls below the claim.</p>
                    </div>
                </div>
                <div class="ckp-chain-item">
                    <div class="ckp-chain-num">4</div>
                    <div class="ckp-chain-content">
                        <h4>Conditioner Margin</h4>
                        <p>A conditioner whose input-entropy margin is accounted for explicitly, so output entropy is a consequence of the bound, not an assumption.</p>
                    </div>
                </div>
                <div class="ckp-chain-item">
                    <div class="ckp-chain-num">5</div>
                    <div class="ckp-chain-content">
                        <h4>Leakage Containment</h4>
                        <p>An argument that the side information $E$ in the conditional bound is complete—no physical side channel hands the adversary omitted information.</p>
                    </div>
                </div>
            </div>
        </section>

        <div class="ckp-sep">The Mathematics of Uncertainty</div>

        <!-- ─── SECTION 2 ─────────────────────────────────────────── -->
        <section id="sec-math">
            <h2>2. From Unpredictability to Conditional Min-Entropy</h2>
            <p>Shannon entropy measures the average surprise, which is the wrong average for a key. The relevant quantity is the worst case, the min-entropy:</p>
            <div class="ckp-eq">
                <span class="eq-label">Min-Entropy — Eq. (1)</span>
                $$H_\infty(X) = -\log_2 \max_i p_i \tag{1}$$
            </div>
            
            <p>Real sources are not isolated. Let $E$ denote all side information available to the adversary. The correct object is the average conditional min-entropy:</p>
            <div class="ckp-eq">
                <span class="eq-label">Conditional Min-Entropy — Eq. (2)</span>
                $$\tilde{H}_\infty(X|E) = -\log_2 \mathbb{E}_{e \leftarrow E}\left[\max_x \Pr(X=x|E=e)\right] \tag{2}$$
            </div>

            <h3>The Leftover Hash Lemma</h3>
            <p>A conditioner cannot create min-entropy; the best it can do is concentrate existing min-entropy into a shorter, nearly uniform string. The tool that prices it is the Leftover Hash Lemma. Applied with a public uniform seed to a source of conditional min-entropy $k$, such a family yields output within statistical distance $\epsilon$ of uniform provided:</p>
            <div class="ckp-eq">
                <span class="eq-label">Leftover Hash Lemma — Eq. (3)</span>
                $$m \leq k - 2 \log_2(1/\epsilon) \tag{3}$$
            </div>
            <p>This disposes of the amplification fantasy in one line: if $k$ is small, no choice of hash makes $m$ large. The $2\log_2(1/\epsilon)$ term is the entropy gap one pays for near-uniformity; in cryptographically hardened form it reappears as the "+64" in the NIST conditioning rule.</p>
        </section>

        <div class="ckp-sep">First-Principles Physics</div>

        <!-- ─── SECTION 3 ─────────────────────────────────────────── -->
        <section id="sec-models">
            <h2>3. Analytical Output Models</h2>
            <p>We study five source classes chosen to span the field. For each, we give a physics-grounded derivation of the output model $p(x|\theta)$, identify $\theta$ with measurable quantities, and state the per-sample min-entropy.</p>
            
            <ul class="ckp-hier">
                <li><strong>Oscillator Jitter (Classical):</strong> Phase diffusion modeled as a Wiener process. The accumulated jitter variance normalized by the squared period ($Q$) governs the bias and serial correlation. Falsified if scaling departs from the Wiener model (e.g., injection locking).</li>
                <li><strong>Amplified Thermal Noise (Classical):</strong> Johnson-Nyquist law. Bias is the comparator offset measured in units of the amplified noise standard deviation. Falsified if the pre-comparator distribution departs from Gaussian or if variance ignores temperature.</li>
                <li><strong>Metastability (Classical):</strong> A cross-coupled latch driven to its unstable equilibrium. The honest model is a two-state Markov chain due to hysteresis and incomplete settling. Falsified if bias persists after offset cancellation.</li>
                <li><strong>Single-Photon Which-Path (Quantum):</strong> Born rule assigns 1 bit of ideal entropy, but the floor is set by classical imperfections: efficiency mismatch, dark counts, and afterpulsing. Falsified if realized bias disagrees with independently measured detector parameters.</li>
                <li><strong>Vacuum-Fluctuation Homodyne (Quantum):</strong> Extractable randomness is the discretised conditional min-entropy given classical electronic excess noise. Quoting the total variance is the most common over-statement in continuous-variable QRNGs.</li>
            </ul>
        </section>

        <div class="ckp-sep">Operational Discipline</div>

        <!-- ─── SECTION 4 ─────────────────────────────────────────── -->
        <section id="sec-health">
            <h2>4. Measurement & Model-Bound Health Tests</h2>
            <div class="ckp-callout key">
                <strong>The Cardinal Rule</strong>
                <p>Tap the digitiser output <em>upstream</em> of any hash or von Neumann corrector. A conditioner whitens everything, including failure. Measuring after it measures the conditioner, not the source.</p>
            </div>
            <p>Do not assume independence. Run the SP 800-90B non-IID track and report the minimum over the estimators. The dominating estimator names the structure the source is leaking (e.g., Markov estimator implies first-order serial dependence; LZ78Y implies longer-range periodic structure).</p>
            
            <h3>Tying Tests to Model Parameters</h3>
            <p>A generic output test asks "does this look random?"; a model-bound test asks "is the physical quantity that produces the randomness still in its certified range?". For example, in an oscillator jitter source, a sliding-window estimator tracks $Q$; the alarm fires when $Q$ falls below the value at which $H_\infty$ meets the claim. This catches slow drifts and injection locking that catastrophic continuous tests miss.</p>
            
            <p>Effectiveness is proven by adversarial fault injection. The acceptance criterion is a latency statement: for each fault, the relevant test must alarm before the measured min-entropy crosses below the claim, and the number of below-claim outputs emitted must be quantified and bounded.</p>
        </section>

        <!-- ─── SECTION 5 ─────────────────────────────────────────── -->
        <section id="sec-leakage">
            <h2>5. Leakage: Unpredictability Must Be Confidential</h2>
            <p>The conditional min-entropy $\tilde{H}_\infty(X|E)$ is only as honest as the side information $E$ it conditions on. If a physical side channel hands the adversary information the model omitted from $E$, the true conditional min-entropy is lower than the certified one.</p>
            <p>Leaking the state of the noise source can collapse the entropy of every subsequent output. Power and electromagnetic emanations carry exactly these quantities. A device that is monitored for entropy but not shielded for leakage can be driven into a low-entropy, attacker-synchronised regime that its health test was never designed to see. The leakage budget must be reported alongside the entropy budget.</p>
        </section>

        <div class="ckp-sep">Entropy Accounting</div>

        <!-- ─── SECTION 6 ─────────────────────────────────────────── -->
        <section id="sec-accounting">
            <h2>6. Conditioning & Entropy Accounting</h2>
            <p>For a vetted component producing $n_{out}$ bits of full entropy, SP 800-90B and SP 800-90C require the input min-entropy to satisfy:</p>
            <div class="ckp-eq">
                <span class="eq-label">NIST Conditioning Rule — Eq. (4)</span>
                $$h_{in} \geq n_{out} + 64 \tag{4}$$
            </div>
            <p>The accounting turns the online health test's live lower bound $\rho$ (per-bit min-entropy) into the compression ratio the conditioner must apply: consume $\lceil(n_{out} + 64)/\rho\rceil$ raw bits per output block.</p>

            <h3>Worked Accounting (256-bit Output)</h3>
            <div class="ckp-table-wrap">
                <table class="ckp-table">
                    <thead>
                        <tr>
                            <th>Source (Conservative $\rho$)</th>
                            <th>$\rho$</th>
                            <th>$n_{out}$</th>
                            <th>Req. $h_{in}$</th>
                            <th>Raw Bits</th>
                            <th>Conditioner</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td class="term">Oscillator Jitter</td>
                            <td>0.50</td>
                            <td>256</td>
                            <td>320</td>
                            <td>640</td>
                            <td>SHA-256 df</td>
                        </tr>
                        <tr>
                            <td class="term">Amplified Thermal</td>
                            <td>0.80</td>
                            <td>256</td>
                            <td>320</td>
                            <td>400</td>
                            <td>SHA-256 df</td>
                        </tr>
                        <tr>
                            <td class="term">Metastability</td>
                            <td>0.60</td>
                            <td>256</td>
                            <td>320</td>
                            <td>534</td>
                            <td>SHA-256 df</td>
                        </tr>
                        <tr>
                            <td class="term">Vacuum Homodyne</td>
                            <td>0.95</td>
                            <td>256</td>
                            <td>320</td>
                            <td>337</td>
                            <td>SHA-256 df</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </section>

        <!-- ─── SECTION 7 ─────────────────────────────────────────── -->
        <section id="sec-quantum">
            <h2>7. The Quantum Case</h2>
            <p>We single out the quantum case because it is where the word "quantum" does the most rhetorical work relative to its logical content.</p>
            <div class="ckp-callout warn">
                <strong>The Ceiling vs. The Floor</strong>
                <p>Does a QRNG carry a real advantage? Yes. Its ideal model has a first-principles entropy that is a consequence of quantum measurement. But it is an advantage in the <em>ceiling</em>; the security parameter is the <em>floor</em>, and the floor is classical. The single-photon device leaks through detector imperfections; the homodyne device leaks through classical excess noise.</p>
            </div>
            <p>Do quantum computers threaten hardware RNGs? Not at the entropy-source layer. A quantum computer does not predict a well-characterised physical entropy source, whose security is information-theoretic at the raw layer. The post-quantum transition is a story about algorithms downstream of the RBG, not about the noise source.</p>
            <p>The discriminating question to ask any QRNG vendor is not "is it quantum?" but "what is your conditional min-entropy given your own classical noise, which online test holds it, and what adversary measurement capability did your leakage budget assume?"</p>
        </section>

        <div class="ckp-sep">Final Thoughts</div>

        <!-- ─── SECTION 8 ─────────────────────────────────────────── -->
        <section id="sec-conclusion">
            <h2>8. Conclusion</h2>
            <p>The community has the right standards and, sometimes, the wrong emphasis. The model, the health test, the leakage budget and the entropy accounting are routinely treated as compliance burden laid over a source that is "obviously random." The order of dependence is the reverse: those four are the only content the word random has in a cryptographic setting, and the source is nothing without them.</p>
            
            <div class="ckp-pull">
                <p>The error worth eradicating is the belief that the conditioner can rescue a source the model never characterised. It cannot: a hash function is an excellent way to hide that one does not know how much entropy one has, and a poor way to obtain any.</p>
                <cite>— Malik & Aun, PakCrypt NPO</cite>
            </div>
        </section>

        <!-- ─── REFERENCES ─────────────────────────────────────────── -->
        <div class="ckp-refs" id="references">
            <h2>References</h2>
            <p id="ref-1"><span class="ref-num">[1]</span> M. S. Turan et al.: Recommendation for the Entropy Sources Used for Random Bit Generation. NIST SP 800-90B (2018).</p>
            <p id="ref-2"><span class="ref-num">[2]</span> E. Barker, J. Kelsey: Recommendation for Random Number Generation Using DRBGs. NIST SP 800-90A Rev. 1 (2015).</p>
            <p id="ref-3"><span class="ref-num">[3]</span> E. Barker et al.: Recommendation for Random Bit Generator (RBG) Constructions. NIST SP 800-90C (2025).</p>
            <p id="ref-4"><span class="ref-num">[4]</span> W. Killmann, W. Schindler: A Proposal for: Functionality Classes for RNGs, Version 2.0. BSI AIS 20/31 (2011).</p>
            <p id="ref-5"><span class="ref-num">[5]</span> M. Peter, W. Schindler: A Proposal for: Functionality Classes for RNGs, Version 3.0. BSI (2024).</p>
            <p id="ref-6"><span class="ref-num">[6]</span> W. Schindler: Overview of AIS 20/31. NIST RNG workshop (2023).</p>
            <p id="ref-7"><span class="ref-num">[7]</span> D. Shumow, N. Ferguson: On the Possibility of a Back Door in the NIST SP 800-90 Dual_EC_PRNG. CRYPTO 2007.</p>
            <p id="ref-8"><span class="ref-num">[8]</span> D. J. Bernstein et al.: Dual EC: A Standardized Back Door. The New Codebreakers, LNCS 9100 (2016).</p>
            <p id="ref-9"><span class="ref-num">[9]</span> R. Impagliazzo et al.: Pseudo-random Generation from One-way Functions. STOC 1989.</p>
            <p id="ref-10"><span class="ref-num">[10]</span> Y. Dodis et al.: Fuzzy Extractors: How to Generate Strong Keys from Biometrics. SIAM J. Comput. (2008).</p>
            <p id="ref-11"><span class="ref-num">[11]</span> M. Baudet et al.: On the Security of Oscillator-Based RNGs. Journal of Cryptology (2011).</p>
            <p id="ref-12"><span class="ref-num">[12]</span> W. Killmann, W. Schindler: A Design for a Physical RNG with Robust Entropy Estimators. CHES 2008.</p>
            <p id="ref-13"><span class="ref-num">[13]</span> P. Kohlbrenner, K. Gaj: An Embedded TRNG for FPGAs. FPGA 2004.</p>
            <p id="ref-14"><span class="ref-num">[14]</span> M. Bucci et al.: A High-Speed Oscillator-Based Truly Random Source. IEEE Trans. Comput. (2003).</p>
            <p id="ref-15"><span class="ref-num">[15]</span> C. S. Petrie, J. A. Connelly: A Noise-Based IC RNG for Applications in Cryptography. IEEE TCAS I (2000).</p>
            <p id="ref-16"><span class="ref-num">[16]</span> C. Tokunaga et al.: True Random Number Generator with a Metastability-Based Quality Control. IEEE JSSC (2008).</p>
            <p id="ref-17"><span class="ref-num">[17]</span> I. Vasyltsov et al.: Fast Digital TRNG Based on Metastable Ring Oscillator. CHES 2008.</p>
            <p id="ref-18"><span class="ref-num">[18]</span> A. T. Markettos, S. W. Moore: The Frequency Injection Attack on Ring-Oscillator-Based TRNGs. CHES 2009.</p>
            <p id="ref-19"><span class="ref-num">[19]</span> P. Bayon et al.: Contactless Electromagnetic Active Attack on Ring Oscillator Based TRNG. COSADE 2012.</p>
            <p id="ref-20"><span class="ref-num">[20]</span> Y. Dodis et al.: Security Analysis of PRNGs with Input: /dev/random is Not Robust. ACM CCS 2013.</p>
            <p id="ref-21"><span class="ref-num">[21]</span> N. Ferguson, B. Schneier, T. Kohno: Cryptography Engineering. Wiley (2010).</p>
            <p id="ref-22"><span class="ref-num">[22]</span> NIST: Security Requirements for Cryptographic Modules. FIPS PUB 140-3 (2019).</p>
            <p id="ref-23"><span class="ref-num">[23]</span> NIST: CMVP Approved Non-Invasive Attack Mitigation Test Metrics. SP 800-140F.</p>
            <p id="ref-24"><span class="ref-num">[24]</span> M. Herrero-Collantes, J. C. Garcia-Escartin: Quantum Random Number Generators. Rev. Mod. Phys. (2017).</p>
            <p id="ref-25"><span class="ref-num">[25]</span> X. Ma et al.: Quantum Random Number Generation. npj Quantum Information (2016).</p>
            <p id="ref-26"><span class="ref-num">[26]</span> C. Gabriel et al.: A Generator for Unique Quantum Random Numbers Based on Vacuum States. Nature Photonics (2010).</p>
            <p id="ref-27"><span class="ref-num">[27]</span> J. Y. Haw et al.: Maximization of Extractable Randomness in a QRNG. Physical Review Applied (2015).</p>
            <p id="ref-28"><span class="ref-num">[28]</span> ID Quantique: Quantis QRNG— AIS 31/ SP 800-90B Certification Documentation.</p>
            <p id="ref-29"><span class="ref-num">[29]</span> M. Stipčević, Ç. K. Koç: True Random Number Generators. Open Problems in Mathematics (2014).</p>
        </div>
    </div><!-- end .ckp-body -->

    <!-- ─── Sidebar TOC ─────────────────────────────────────────── -->
    <aside class="ckp-sidebar">
        <div class="ckp-toc-label">Contents</div>
        <ul class="ckp-toc-list" id="ckp-toc">
            <li data-section="abstract"> <a href="#abstract">Abstract</a> </li>
            <li data-section="sec-intro"> <a href="#sec-intro">1. The Error of "Unpredictable..."</a> </li>
            <li class="toc-sub" data-section="sec-intro"> <a href="#sec-intro">Five Obligations</a> </li>
            <li data-section="sec-math"> <a href="#sec-math">2. Conditional Min-Entropy</a> </li>
            <li class="toc-sub" data-section="sec-math"> <a href="#sec-math">Leftover Hash Lemma</a> </li>
            <li data-section="sec-models"> <a href="#sec-models">3. Analytical Output Models</a> </li>
            <li data-section="sec-health"> <a href="#sec-health">4. Measurement & Health Tests</a> </li>
            <li data-section="sec-leakage"> <a href="#sec-leakage">5. Leakage & Side-Channels</a> </li>
            <li data-section="sec-accounting"> <a href="#sec-accounting">6. Conditioning & Accounting</a> </li>
            <li class="toc-sub" data-section="sec-accounting"> <a href="#sec-accounting">NIST +64 Rule</a> </li>
            <li data-section="sec-quantum"> <a href="#sec-quantum">7. The Quantum Case</a> </li>
            <li data-section="sec-conclusion"> <a href="#sec-conclusion">8. Conclusion</a> </li>
            <li data-section="references"> <a href="#references">References</a> </li>
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
var sections = ['abstract','sec-intro','sec-math','sec-models','sec-health','sec-leakage','sec-accounting','sec-quantum','sec-conclusion','references'];
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