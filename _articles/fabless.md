---
layout: post
title: "Guide to ASIC Design with Open Source Tools"
---

<style>
@import url('https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Serif+Display:ital@0;1&family=IBM+Plex+Mono:wght@400;500;600&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300;1,9..40,400&display=swap');

:root {
  --bg:         #1b1b1e;
  --surf:       #242428;
  --surf2:      #2c2c32;
  --surf3:      #32323a;
  --border:     #3a3a44;
  --text:       #dddde2;
  --muted:      #8888a0;
  --acc:        #5b9cf6;
  --grn:        #7ed4a6;
  --warn:       #e08a4a;
  --red:        #e05c6c;
  --acc-dim:    rgba(91,156,246,0.12);
  --acc-glow:   rgba(91,156,246,0.06);
  --f-disp:     'DM Serif Display', Georgia, serif;
  --f-head:     'Syne', sans-serif;
  --f-body:     'DM Sans', system-ui, sans-serif;
  --f-mono:     'IBM Plex Mono', 'Courier New', monospace;
}

.fa * { box-sizing: border-box; }
.fa {
  font-family: var(--f-body);
  font-size: 1.05rem;
  line-height: 1.8;
  color: var(--text);
}

/* ── Progress ── */
#fa-prog {
  position: fixed; top: 0; left: 0;
  height: 2px; width: 0%;
  background: linear-gradient(90deg, var(--acc), var(--grn));
  z-index: 9999;
  box-shadow: 0 0 8px rgba(91,156,246,0.55);
  transition: width 0.1s linear;
}

/* ── Hero ── */
.fa-hero {
  padding: 3rem 0 2.2rem;
  border-bottom: 1px solid var(--border);
  position: relative; overflow: hidden;
}
.fa-hero::before {
  content: '';
  position: absolute; top: -80px; right: -80px;
  width: 360px; height: 360px;
  background: radial-gradient(circle, rgba(91,156,246,0.07) 0%, transparent 68%);
  pointer-events: none;
}
.fa-eyebrow {
  display: flex; align-items: center; gap: 0.75rem;
  font-family: var(--f-mono);
  font-size: 0.67rem; letter-spacing: 0.18em; text-transform: uppercase;
  color: var(--acc); margin-bottom: 1.2rem;
}
.fa-eyebrow::before { content: '◈'; font-size: 0.85rem; color: var(--grn); }
.fa-hero h1 {
  font-family: var(--f-head);
  font-size: clamp(1.9rem, 4.2vw, 3.3rem);
  font-weight: 800; line-height: 1.09;
  color: #f0f0f5; margin: 0 0 1rem;
  letter-spacing: -0.022em;
}
.fa-hero h1 .hi { color: var(--acc); }
.fa-deck {
  font-size: clamp(0.97rem, 1.8vw, 1.13rem);
  font-weight: 300; color: var(--muted);
  max-width: 680px; line-height: 1.65; margin-bottom: 1.8rem;
}
.fa-meta {
  display: flex; flex-wrap: wrap; align-items: center;
  gap: 0.9rem;
  font-family: var(--f-mono); font-size: 0.67rem;
  color: var(--muted); letter-spacing: 0.06em;
}
.fa-meta a { color: var(--acc); text-decoration: none; }
.fa-meta a:hover { text-decoration: underline; }
.fa-meta .sep { color: var(--border); }

/* ── Override Jekyll's narrow post container ── */
/* Targets common Jekyll themes: Minima, Cayman, minimal, hacker, etc.        */
/* We widen the post/content wrapper and let .fa fill the available space.    */
.post, .post-content, .page-content .post,
article.post, .wrapper > .post,
.content, .markdown-body,
.inner, .site-content {
  max-width: none !important;
  width: 100% !important;
  padding-left: 0 !important;
  padding-right: 0 !important;
}

/* The .fa wrapper spans the full available width with comfortable side padding */
.fa {
  width: 100%;
  max-width: 1280px;
  margin-left: auto;
  margin-right: auto;
  padding: 0 clamp(1rem, 4vw, 3rem);
  box-sizing: border-box;
  overflow-x: hidden;
}

/* ── Layout ── */
.fa-layout {
  display: grid;
  grid-template-columns: 1fr 252px;
  gap: 3rem;
  align-items: start;
  margin-top: 2.5rem;
}
.fa-hero, .fa-mob-btn, .fa-mob-list, .fa-abstract, .fa-stats {
  /* no extra max-width needed — .fa already constrains width */
}
@media (max-width: 1060px) {
  .fa-layout { grid-template-columns: 1fr; }
  .fa-sidebar { display: none; }
}

/* ── Sidebar ── */
.fa-sidebar {
  position: sticky; top: 5rem;
  max-height: calc(100vh - 7rem);
  overflow-y: auto;
  scrollbar-width: thin; scrollbar-color: var(--border) transparent;
}
.fa-toc-hd {
  font-family: var(--f-mono);
  font-size: 0.61rem; letter-spacing: 0.2em; text-transform: uppercase;
  color: var(--muted);
  padding-bottom: 0.65rem; border-bottom: 1px solid var(--border);
  margin-bottom: 0.8rem;
}
.fa-toc ul { list-style: none; padding: 0; margin: 0; }
.fa-toc li { border-left: 2px solid transparent; transition: border-color 0.2s; }
.fa-toc li.on { border-color: var(--acc); }
.fa-toc a {
  display: block; padding: 0.28rem 0.8rem;
  font-family: var(--f-body); font-size: 0.77rem;
  color: var(--muted); text-decoration: none;
  line-height: 1.4; transition: color 0.2s;
}
.fa-toc li.on a, .fa-toc a:hover { color: var(--acc); }
.fa-toc .sub a { padding-left: 1.6rem; font-size: 0.71rem; opacity: 0.8; }

/* ── Body ── */
.fa-body { min-width: 0; }
.fa-body section { margin-bottom: 3.2rem; }
.fa-body h2 {
  font-family: var(--f-head);
  font-size: clamp(1.3rem, 2.5vw, 1.9rem);
  font-weight: 700; color: #f0f0f5;
  margin: 3.5rem 0 1.1rem;
  padding-top: 1rem; border-top: 1px solid var(--border);
  scroll-margin-top: 5rem; letter-spacing: -0.01em;
}
.fa-body h3 {
  font-family: var(--f-head);
  font-size: 1.08rem; font-weight: 600;
  color: #dddde8; margin: 2.2rem 0 0.65rem;
  scroll-margin-top: 5rem;
}
.fa-body h4 {
  font-family: var(--f-mono);
  font-size: 0.68rem; letter-spacing: 0.15em; text-transform: uppercase;
  color: var(--grn); margin: 1.8rem 0 0.5rem;
}
.fa-body p { margin: 0 0 1.15rem; }
.fa-body .lead::first-letter {
  font-family: var(--f-disp);
  font-size: 4.2rem; font-weight: 400;
  float: left; line-height: 0.8;
  margin: 0.15em 0.1em -0.05em 0;
  color: var(--acc);
}

/* ── Image placeholder ── */
.fa-img {
  margin: 2rem 0;
  border: 1px dashed var(--border);
  background: var(--surf);
  display: flex; flex-direction: column;
  align-items: center; justify-content: center;
  padding: 2.5rem 1.5rem;
  text-align: center;
  position: relative;
}
.fa-img::before {
  content: '';
  position: absolute; inset: 6px;
  border: 1px dashed var(--surf3);
  pointer-events: none;
}
.fa-img .img-icon {
  font-size: 2rem; margin-bottom: 0.5rem; opacity: 0.35;
}
.fa-img .img-name {
  font-family: var(--f-mono); font-size: 0.75rem;
  color: var(--acc); letter-spacing: 0.08em; margin-bottom: 0.3rem;
}
.fa-img .img-cap {
  font-size: 0.8rem; color: var(--muted);
  max-width: 500px; line-height: 1.45;
}
.fa-img.wide { min-height: 180px; }
.fa-img.tall { min-height: 260px; }

/* ── Pull quote ── */
.fa-pull {
  margin: 2.5rem -1rem;
  padding: 1.5rem 2rem 1.5rem 2.2rem;
  border-left: 3px solid var(--acc);
  background: var(--acc-glow);
}
@media (max-width: 660px) { .fa-pull { margin: 2rem 0; } }
.fa-pull p {
  font-family: var(--f-disp);
  font-size: clamp(1.05rem, 2vw, 1.26rem);
  font-style: italic; color: #f0f0f5;
  margin: 0; line-height: 1.5;
}
.fa-pull cite {
  display: block; margin-top: 0.6rem;
  font-family: var(--f-mono); font-size: 0.64rem;
  letter-spacing: 0.1em; text-transform: uppercase;
  color: var(--muted); font-style: normal;
}

/* ── Abstract ── */
.fa-abstract {
  background: var(--surf); border: 1px solid var(--border);
  border-top: 3px solid var(--acc);
  padding: 1.6rem 1.8rem; margin-bottom: 2.2rem;
}
.fa-abs-lbl {
  font-family: var(--f-mono); font-size: 0.61rem;
  letter-spacing: 0.2em; text-transform: uppercase;
  color: var(--acc); margin-bottom: 0.65rem;
}
.fa-abstract p {
  margin: 0; font-size: 0.93rem;
  color: var(--muted); font-style: italic; line-height: 1.65;
}

/* ── Stats ── */
.fa-stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 1px; background: var(--border);
  border: 1px solid var(--border); margin: 2rem 0;
}
.fa-stat {
  background: var(--surf); padding: 1.1rem 1.2rem; text-align: center;
}
.fa-stat .n {
  display: block; font-family: var(--f-head);
  font-size: 1.75rem; font-weight: 800;
  color: var(--acc); line-height: 1;
}
.fa-stat .l {
  display: block; font-family: var(--f-mono);
  font-size: 0.59rem; letter-spacing: 0.11em; text-transform: uppercase;
  color: var(--muted); margin-top: 0.3rem;
}

/* ── Callout ── */
.fa-call {
  background: var(--surf); border: 1px solid var(--border);
  border-left: 3px solid var(--grn);
  padding: 1.1rem 1.4rem; margin: 1.8rem 0; font-size: 0.9rem;
}
.fa-call.warn { border-left-color: var(--warn); }
.fa-call.danger { border-left-color: var(--red); }
.fa-call strong {
  font-family: var(--f-mono); font-size: 0.61rem;
  letter-spacing: 0.14em; text-transform: uppercase;
  color: var(--grn); display: block; margin-bottom: 0.45rem;
}
.fa-call.warn strong { color: var(--warn); }
.fa-call.danger strong { color: var(--red); }

/* ── Definition ── */
.fa-def {
  background: var(--surf); border: 1px solid var(--border);
  border-left: 3px solid var(--grn);
  padding: 1.1rem 1.5rem; margin: 1.5rem 0;
}
.fa-def-lbl {
  font-family: var(--f-mono); font-size: 0.61rem;
  letter-spacing: 0.18em; text-transform: uppercase;
  color: var(--grn); margin-bottom: 0.5rem;
}
.fa-def p { margin: 0; font-size: 0.9rem; font-style: italic; }

/* ── Pipeline ── */
.fa-pipeline { margin: 2rem 0; }
.fa-pstep {
  display: grid; grid-template-columns: 48px 1fr;
  gap: 0; position: relative;
}
.fa-pstep:not(:last-child)::after {
  content: ''; position: absolute;
  left: 23px; top: 48px;
  width: 2px; height: calc(100% - 18px);
  background: var(--border);
}
.fa-picon {
  width: 48px; height: 48px; border-radius: 50%;
  background: var(--surf2); border: 2px solid var(--border);
  display: flex; align-items: center; justify-content: center;
  font-family: var(--f-mono); font-size: 0.72rem; font-weight: 600;
  color: var(--acc); flex-shrink: 0;
  position: relative; z-index: 1;
  transition: border-color 0.2s, background 0.2s;
}
.fa-pstep:hover .fa-picon { border-color: var(--acc); background: var(--acc-dim); }
.fa-pbody { padding: 0.3rem 0 1.6rem 1.2rem; }
.fa-pbody h4 {
  font-family: var(--f-head); font-size: 0.95rem; font-weight: 700;
  color: var(--text); margin: 0.3rem 0 0.3rem;
  text-transform: none; letter-spacing: normal;
}
.fa-pbody p { margin: 0; font-size: 0.86rem; color: var(--muted); line-height: 1.55; }
.fa-ptool {
  display: inline-block; background: var(--surf3);
  border: 1px solid var(--border);
  font-family: var(--f-mono); font-size: 0.67rem;
  color: var(--grn); padding: 0.14rem 0.52rem;
  margin: 0.4rem 0.2rem 0 0; letter-spacing: 0.04em;
}

/* ── Comparison table ── */
.fa-tbl-wrap { overflow-x: auto; margin: 1.5rem -0.5rem; -webkit-overflow-scrolling: touch; }
.fa-tbl { width: 100%; min-width: 540px; border-collapse: collapse; font-size: 0.82rem; }
.fa-tbl thead tr { background: var(--surf2); }
.fa-tbl th {
  font-family: var(--f-mono); font-size: 0.61rem;
  letter-spacing: 0.12em; text-transform: uppercase;
  color: var(--muted); padding: 0.7rem 1rem;
  text-align: left; border-bottom: 2px solid var(--acc);
  white-space: nowrap;
}
.fa-tbl td {
  padding: 0.68rem 1rem; border-bottom: 1px solid var(--border);
  vertical-align: top; line-height: 1.45;
}
.fa-tbl tr:hover td { background: var(--surf); }
.fa-tbl .attr { font-family: var(--f-mono); font-size: 0.7rem; color: var(--muted); white-space: nowrap; }
.fa-tbl .col-a { color: var(--warn); }
.fa-tbl .col-b { color: var(--grn); }
.fa-tbl.cost th { border-bottom-color: var(--warn); }
.fa-tbl .ci { font-weight: 500; color: #e0e0ea; }
.fa-tbl .cv { font-family: var(--f-mono); font-size: 0.78rem; color: var(--warn); white-space: nowrap; }
.fa-tbl .cn { font-size: 0.77rem; color: var(--muted); }

/* ── Node bar chart ── */
.fa-bars { margin: 1.5rem 0; }
.fa-bar-hd {
  font-family: var(--f-mono); font-size: 0.61rem;
  letter-spacing: 0.14em; text-transform: uppercase;
  color: var(--muted); margin-bottom: 0.8rem;
}
.fa-bar-row {
  display: grid; grid-template-columns: 68px 1fr 100px;
  align-items: center; gap: 0.75rem; margin-bottom: 0.55rem;
}
.fa-bar-lbl { font-family: var(--f-mono); font-size: 0.71rem; color: var(--muted); text-align: right; }
.fa-bar-track {
  height: 22px; background: var(--surf2); border-radius: 2px;
  overflow: hidden; position: relative;
}
.fa-bar-fill {
  height: 100%; display: flex; align-items: center;
  padding-left: 0.5rem;
  font-family: var(--f-mono); font-size: 0.6rem;
  letter-spacing: 0.06em; color: rgba(255,255,255,0.75);
}
.fa-bar-val { font-family: var(--f-mono); font-size: 0.71rem; color: var(--warn); text-align: right; }
.fa-bar-note { font-family: var(--f-mono); font-size: 0.59rem; color: var(--muted); margin-top: 0.3rem; }

/* ── EDA bar chart (horizontal grouped) ── */
.fa-eda-chart { margin: 1.5rem 0; }
.fa-eda-row {
  display: grid; grid-template-columns: 160px 1fr 1fr;
  gap: 0.5rem; align-items: center; margin-bottom: 0.5rem;
  font-size: 0.8rem;
}
@media (max-width: 600px) { .fa-eda-row { grid-template-columns: 100px 1fr 1fr; } }
.fa-eda-tool { font-family: var(--f-mono); font-size: 0.7rem; color: var(--muted); }
.fa-eda-bar-wrap { height: 18px; background: var(--surf2); border-radius: 2px; overflow: hidden; }
.fa-eda-bar {
  height: 100%; display: flex; align-items: center;
  padding-left: 0.4rem;
  font-family: var(--f-mono); font-size: 0.58rem;
  color: rgba(255,255,255,0.7); white-space: nowrap;
}
.fa-eda-legend {
  display: flex; gap: 1.5rem; margin-bottom: 0.75rem;
  font-family: var(--f-mono); font-size: 0.62rem; color: var(--muted);
}
.fa-eda-legend span { display: flex; align-items: center; gap: 0.4rem; }
.fa-eda-legend .dot { width: 10px; height: 10px; border-radius: 2px; flex-shrink: 0; }

/* ── Foundry cards ── */
.fa-foundry-grid {
  display: grid; grid-template-columns: 1fr 1fr;
  gap: 1px; background: var(--border);
  border: 1px solid var(--border); margin: 1.5rem 0;
}
@media (max-width: 580px) { .fa-foundry-grid { grid-template-columns: 1fr; } }
.fa-fcard { background: var(--surf); padding: 1.4rem 1.5rem; }
.fa-fcard .fn { font-family: var(--f-head); font-size: 1.1rem; font-weight: 700; color: #f0f0f5; margin-bottom: 0.2rem; }
.fa-fcard .fs { font-family: var(--f-mono); font-size: 0.62rem; letter-spacing: 0.1em; text-transform: uppercase; color: var(--muted); margin-bottom: 1rem; }
.fa-fcard .fr { display: flex; justify-content: space-between; align-items: baseline; padding: 0.38rem 0; border-bottom: 1px solid var(--border); font-size: 0.82rem; }
.fa-fcard .fr:last-of-type { border: none; }
.fa-fcard .fk { color: var(--muted); font-size: 0.78rem; }
.fa-fcard .fv { font-family: var(--f-mono); font-size: 0.77rem; color: var(--grn); text-align: right; }
.fa-fcard.tsmc .fn { color: var(--acc); }
.fa-fcard.smic .fn { color: var(--grn); }
.fa-tag {
  display: inline-block; font-family: var(--f-mono);
  font-size: 0.61rem; letter-spacing: 0.1em; text-transform: uppercase;
  padding: 0.18rem 0.6rem; border: 1px solid; margin-top: 0.8rem;
}
.fa-tag.prem { color: var(--acc); border-color: rgba(91,156,246,0.4); }
.fa-tag.budg { color: var(--grn); border-color: rgba(126,212,166,0.4); }
.fa-tag.risk { color: var(--red); border-color: rgba(224,92,108,0.4); }

/* ── Phases ── */
.fa-phases {
  display: grid; grid-template-columns: repeat(3,1fr);
  gap: 1px; background: var(--border);
  border: 1px solid var(--border); margin: 1.5rem 0;
}
@media (max-width: 600px) { .fa-phases { grid-template-columns: 1fr; } }
.fa-phase { background: var(--surf); padding: 1.3rem 1.4rem; position: relative; }
.fa-phase-n {
  font-family: var(--f-head); font-size: 2.8rem; font-weight: 800;
  color: var(--surf3); line-height: 1;
  position: absolute; top: 0.8rem; right: 1rem;
}
.fa-phase h4 {
  font-family: var(--f-head); font-size: 0.88rem; font-weight: 700;
  color: var(--acc); margin: 0 0 0.5rem;
  text-transform: none; letter-spacing: normal; position: relative;
}
.fa-phase p { margin: 0; font-size: 0.82rem; color: var(--muted); line-height: 1.55; position: relative; }

/* ── Use-case grid ── */
.fa-use-grid {
  display: grid; grid-template-columns: repeat(auto-fit, minmax(195px,1fr));
  gap: 1px; background: var(--border);
  border: 1px solid var(--border); margin: 1.5rem 0;
}
.fa-uc { background: var(--surf); padding: 1.3rem 1.4rem; }
.fa-uc .ui { font-size: 1.3rem; margin-bottom: 0.55rem; display: block; }
.fa-uc h4 {
  font-family: var(--f-head); font-size: 0.88rem; font-weight: 700;
  color: #f0f0f5; margin: 0 0 0.4rem;
  text-transform: none; letter-spacing: normal;
}
.fa-uc p { margin: 0; font-size: 0.82rem; color: var(--muted); line-height: 1.5; }

/* ── Key term inline ── */
.t {
  font-family: var(--f-mono); font-size: 0.87em;
  color: var(--grn); background: rgba(126,212,166,0.09);
  padding: 0.04em 0.33em; border-radius: 2px;
}

/* ── Verification scenario cards ── */
.fa-verif-grid {
  display: grid; grid-template-columns: repeat(auto-fit, minmax(200px,1fr));
  gap: 1px; background: var(--border);
  border: 1px solid var(--border); margin: 1.5rem 0;
}
.fa-verif { background: var(--surf); padding: 1.2rem 1.3rem; }
.fa-verif .vn {
  font-family: var(--f-mono); font-size: 0.62rem;
  letter-spacing: 0.14em; text-transform: uppercase;
  color: var(--muted); margin-bottom: 0.5rem; display: block;
}
.fa-verif .vc {
  font-family: var(--f-head); font-size: 1.15rem; font-weight: 700;
  color: var(--warn); margin-bottom: 0.4rem; display: block;
}
.fa-verif p { margin: 0; font-size: 0.8rem; color: var(--muted); line-height: 1.5; }

/* ── Titan-I spec table ── */
.fa-titan { margin: 1.5rem 0; border: 1px solid var(--border); }
.fa-titan-row {
  display: grid; grid-template-columns: 180px 1fr;
  border-bottom: 1px solid var(--border);
}
.fa-titan-row:last-child { border-bottom: none; }
.fa-titan-row:hover { background: var(--surf); }
.fa-titan-k {
  padding: 0.7rem 1rem;
  font-family: var(--f-mono); font-size: 0.7rem;
  color: var(--muted); border-right: 1px solid var(--border);
  display: flex; align-items: center;
}
.fa-titan-v { padding: 0.7rem 1rem; font-size: 0.85rem; line-height: 1.4; }

/* ── References ── */
.fa-refs {
  margin-top: 3rem; padding-top: 1.5rem;
  border-top: 1px solid var(--border);
  font-size: 0.79rem; color: var(--muted);
  columns: 2; column-gap: 2rem;
}
@media (max-width: 620px) { .fa-refs { columns: 1; } }
.fa-refs p { margin: 0 0 0.5rem; break-inside: avoid; line-height: 1.4; }
.fa-refs .rn { color: var(--acc); font-family: var(--f-mono); font-size: 0.65rem; }

/* ── Mobile TOC ── */
.fa-mob-btn {
  display: none; background: var(--surf);
  border: 1px solid var(--border); padding: 0.7rem 1.1rem;
  font-family: var(--f-mono); font-size: 0.67rem;
  letter-spacing: 0.12em; text-transform: uppercase;
  color: var(--muted); cursor: pointer;
  justify-content: space-between; align-items: center;
  margin-bottom: 1.5rem;
}
.fa-mob-list {
  display: none; background: var(--surf);
  border: 1px solid var(--border); border-top: none;
  padding: 0.8rem 1.1rem; margin-bottom: 1.5rem; margin-top: -2px;
}
.fa-mob-list a { display: block; padding: 0.3rem 0; font-size: 0.83rem; color: var(--muted); text-decoration: none; }
.fa-mob-list a:hover { color: var(--acc); }
@media (max-width: 880px) { .fa-mob-btn { display: flex; } }

/* ── Separator ── */
.fa-sep {
  display: flex; align-items: center; gap: 1rem; margin: 3rem 0;
  font-family: var(--f-mono); font-size: 0.64rem;
  letter-spacing: 0.18em; text-transform: uppercase; color: var(--muted);
}
.fa-sep::before, .fa-sep::after { content: ''; flex: 1; height: 1px; background: var(--border); }

/* ── Animate in ── */
@keyframes fa-in { from { opacity:0; transform:translateY(14px); } to { opacity:1; transform:translateY(0); } }
.fa-hero { animation: fa-in 0.5s ease both; }
.fa-abstract { animation: fa-in 0.5s 0.1s ease both; }
.fa-stats { animation: fa-in 0.5s 0.18s ease both; }
</style>

<div id="fa-prog"></div>

<article class="fa">

<!-- ═══════════ HERO ═══════════════════════════════════════════ -->
<div class="fa-hero">
  <div class="fa-eyebrow">Business Case · Fabless ASIC · Open-Source EDA · Q2 2026</div>
  <h1>A Guide to <span class="hi">Cost-Effective</span><br>ASIC Design with<br>Open-Source Tools</h1>
  <p class="fa-deck">Custom silicon is no longer the exclusive domain of big corporations. Two historic barriers — the capital cost of owning a fab and the six-figure annual price of proprietary EDA software — have effectively collapsed. A startup with FPGA experience can now design a production-grade chip on a free toolchain and have it manufactured by a world-class foundry for $100–200K.</p>
  <div class="fa-meta">
    <span>Ji Won · Naveed A.A. · PakCrypt NPO</span>
    <span class="sep">·</span><span>Q2 2026</span>
    <span class="sep">·</span><span>~28 min read</span>
    <span class="sep">·</span><a href="/assets/whitepapers/FABLESS.pdf">PDF ↗</a>
  </div>
</div>

<!-- Mobile TOC -->
<div class="fa-mob-btn" id="fa-mob-btn"><span>Contents</span><span>▾</span></div>
<div class="fa-mob-list" id="fa-mob-list">
  <a href="#summary">Executive Summary</a>
  <a href="#introduction">Introduction</a>
  <a href="#technology">Technology Tour</a>
  <a href="#pdks">PDKs &amp; Workflow</a>
  <a href="#eda-tooling">Open-Source EDA Tooling</a>
  <a href="#titan">Titan-I: Proof of Concept</a>
  <a href="#foundry">Foundry Economics</a>
  <a href="#costs">Complete Cost Breakdown</a>
  <a href="#roadmap">Roadmap to Production</a>
  <a href="#use-cases">Use Cases</a>
  <a href="#final">Final Words</a>
</div>

<!-- ═══════════ LAYOUT ═════════════════════════════════════════ -->
<div class="fa-layout">
<div class="fa-body">

<!-- ── ABSTRACT ── -->
<div class="fa-abstract" id="summary">
  <div class="fa-abs-lbl">Executive Summary</div>
  <p>No fab, no software lock-in — the fabless model removes fabrication capex, while Multi-Project Wafer (MPW) shuttles let dozens of startups share a single mask set. A complete open-source flow — Yosys, OpenROAD, Verilator, KLayout — carries a design from RTL all the way to manufacturable GDSII. FPGA front-end expertise transfers directly. The 28nm planar node is the proven sweet spot for embedded, AI-edge, automotive, and IoT chips, running up to ~1.5–1.8 GHz. The open-source Titan-I RISC-V vector processor was designed, verified, and synthesised with this flow down to 7nm. You can now embark on the journey of proprietary silicon with a budget of $100–200K.</p>
</div>

<!-- Stats -->
<div class="fa-stats">
  <div class="fa-stat"><span class="n">$100K</span><span class="l">Minimum viable budget</span></div>
  <div class="fa-stat"><span class="n">28nm</span><span class="l">Optimal startup node</span></div>
  <div class="fa-stat"><span class="n">1.8GHz</span><span class="l">Planar frequency ceiling</span></div>
  <div class="fa-stat"><span class="n">40–50</span><span class="l">Dies per MPW slot</span></div>
  <div class="fa-stat"><span class="n">7nm</span><span class="l">Open-source flow validated to</span></div>
  <div class="fa-stat"><span class="n">3–4mo</span><span class="l">GDSII to bare die</span></div>
</div>

<!-- ── SECTION 1: INTRODUCTION ── -->
<section id="introduction">
<h2>1 — Introduction: How the Barriers Fell</h2>

<p class="lead">The global semiconductor landscape is undergoing a profound structural shift — one driven not by a single breakthrough, but by the quiet convergence of two independent revolutions happening simultaneously on opposite sides of the design chain. On the manufacturing side, the fabless business model has matured to the point where a startup can access world-class TSMC fabrication capacity without owning a single piece of cleanroom equipment. On the software side, a decade of academic and community investment has produced an open-source EDA toolchain capable of taking a chip design all the way from Verilog code to a manufacturable GDSII layout file — for free.</p>

<div class="fa-img wide">
  <img src="{{ '/assets/images/articles/fabless/pic1.png' | relative_url }}"
       alt="Traditional semiconductor industry value chain">
  <div class="img-cap">The traditional semiconductor industry value chain, from chip design through EDA, IP licensing, foundry fabrication, and OSAT packaging — showing where the fabless model inserts a startup.</div>
</div>

<h3>1.1 — IC Manufacturing Before Fabless</h3>
<p>Historically, the domain of custom IC design was an exclusive preserve of large technology corporations capable of shouldering colossal capital expenditures. Constructing a state-of-the-art fab for leading-edge technologies now requires investments upwards of US$15–20B — encompassing multi-story cleanroom environments, intricate global supply chains for specialised materials, and the acquisition of ultra-expensive lithography machines such as those used for Extreme Ultraviolet (EUV) processing. This immense upfront capital requirement created a formidable moat, preventing all but the well-funded entities from participating in the creation of integrated circuits.</p>

<p>The economics did not merely disadvantage small companies — they made custom silicon structurally impossible for them. A startup could not amortise a $20B fab across its first product run. The minimum viable scale was tens of millions of units. For decades, this confined innovation at the silicon level to a narrow band of incumbents.</p>

<h3>1.2 — EDA Tools: From Commercial Monopoly to Open Source</h3>
<p>For decades, EDA software was the exclusive domain of three large, publicly-traded corporations: Synopsys, Cadence Design Systems, and Siemens EDA (formerly Mentor Graphics). Their proprietary suites, often costing hundreds of thousands of dollars per engineer per year, formed a significant part of the economic barrier that prevented smaller companies and academic institutions from entering the field of custom silicon design.</p>


<p>A quiet revolution has been underway since around 2016, culminating in a robust, fully-integrated, open-source EDA ecosystem capable of supporting a complete <span class="t">RTL-to-GDSII</span> design flow for production-grade chips. This development has been the critical enabler for growth of the fabless model among small teams, removing the prohibitive software licensing costs that once formed the second wall after fabrication capital.</p>

<div class="fa-def">
  <div class="fa-def-lbl">RTL to GDSII — Explained</div>
  <p>RTL (Register Transfer Level) is a hardware design abstraction describing a chip's behaviour in Verilog or VHDL — the human-readable blueprint of a digital circuit. GDSII (Graphic Data System II) is the final geometric layout file containing every transistor, wire, metal layer, and mask shape required for fabrication. The RTL-to-GDSII flow transforms an abstract functional description into a manufacturing-ready layout through synthesis, placement, routing, timing checks, and physical verification.</p>
</div>

<h3>1.3 — The Fabless Business Model</h3>
<p>A fabless company strategically outsources the entire physical production of its chips to specialised, independent foundries — allowing it to concentrate its resources and expertise on architecture, logic design, and software integration. The foundry achieves economies of scale by dedicating its multibillion-dollar facilities exclusively to manufacturing, serving a diverse clientele ranging from established giants to agile startups. TSMC, for example, accounted for 34% of the pure-play foundry industry in 2024.</p>

<p>The emergence of robust, open-source EDA toolchains has now eliminated the second major barrier to entry — the prohibitive cost of proprietary software licences. This convergence of the fabless business model and accessible design tools has created a fertile ground for innovation, empowering startups to compete in niche markets that were previously inaccessible.</p>

<h3>1.4 — From FPGA to ASIC: A Natural Evolution</h3>
<p>For most computer engineering professionals experienced in Xilinx FPGA-based development, the transition to ASIC design represents a natural and logical evolution. The skills acquired in defining system constraints, writing RTL in Verilog, and performing functional verification are directly transferable to the world of Application-Specific Integrated Circuit (ASIC) design.</p>

<div class="fa-call">
  <strong>The Core Difference</strong>
  <p>On an FPGA, routing tracks, clock trees, and IO blocks are pre-fabricated — the Vivado tool simply routes signals through existing hardware switches. In an ASIC, every single wire, buffer, transistor, and clock distribution network must be synthesised, placed, and routed entirely from scratch onto a blank die. What Xilinx handled silently in the back-end becomes your explicit responsibility — and the open-source tools now make that responsibility tractable.</p>
</div>

<h3>1.5 — How Large Fabs Support the Fabless Model</h3>
<p>Large fabs like TSMC and Samsung Foundry solve the NRE cost problem by aggregating multiple fabless designs onto a single Multi-Project Wafer (MPW). Instead of each customer paying for an entire mask set, the MPW service partitions the reticle area, allowing up to 40–60 different designs to share the same physical masks. This substantially reduces the cost for startups.</p>

<p>TSMC's Open Innovation Platform® (OIP) is a cornerstone of this strategy, providing customers with Process Design Kits (PDKs) and extensive technical support to streamline the design-to-manufacturing handoff and optimise yields. SMIC, China's largest contract chip maker, leverages heavily subsidised domestic capacity expansions to aggressively price mature nodes, making it a highly competitive option for startups focused on strict unit-cost optimisation.</p>

<div class="fa-img wide">
  <img src="{{ '/assets/images/articles/fabless/pic3.png' | relative_url }}"
       alt="Multi Project Wafer">
  <div class="img-cap">Multi-Project Wafer (MPW) shuttle concept — showing how up to 40–60 different startup chip designs share a single wafer's reticle area and mask set, dramatically reducing per-project NRE costs.</div>
</div>

</section>

<div class="fa-sep">Technology</div>

<!-- ── SECTION 2: TECHNOLOGY TOUR ── -->
<section id="technology">
<h2>2 — Technology Tour: Choosing Your Node</h2>

<p>The selection of a semiconductor manufacturing technology node is arguably the most consequential commercial decision a fabless company makes. This choice dictates the chip's performance potential, power consumption, transistor density, and, most critically, its cost of production.</p>

<h3>2.1 — The 28nm Sweet Spot</h3>
<p>The fundamental reason for 28nm's enduring appeal lies in the stark economic divide between mature planar CMOS technology and the more advanced 3D FinFET geometries used in nodes smaller than 28nm. The 28nm process uses a planar transistor architecture — a highly evolved and perfected version of classical CMOS technology — where the gate sits flat on top of the channel.</p>

<p>Below 28nm, planar structures suffer from severe short-channel effects, primarily leakage current, where electrons tunnel through the increasingly thin gate oxide. To combat this, foundries adopted the FinFET (Fin Field-Effect Transistor) structure, where the gate wraps around the channel on three sides. While technologically superior, FinFETs are vastly more complex and expensive to manufacture — requiring up to 80–100 separate photomasks and, at advanced nodes, prohibitively expensive EUV lithography equipment.</p>

<!-- Node cost bar chart -->
<div class="fa-bars">
  <div class="fa-bar-hd">Full Mask Set NRE Cost by Technology Node</div>
  <div class="fa-bar-row">
    <div class="fa-bar-lbl">130nm</div>
    <div class="fa-bar-track"><div class="fa-bar-fill" style="width:4%;background:var(--grn);">Planar</div></div>
    <div class="fa-bar-val">~$200K</div>
  </div>
  <div class="fa-bar-row">
    <div class="fa-bar-lbl">28nm</div>
    <div class="fa-bar-track"><div class="fa-bar-fill" style="width:12%;background:var(--grn);">Planar</div></div>
    <div class="fa-bar-val">~$1.5–2.5M</div>
  </div>
  <div class="fa-bar-row">
    <div class="fa-bar-lbl">16nm</div>
    <div class="fa-bar-track"><div class="fa-bar-fill" style="width:28%;background:var(--acc);">FinFET</div></div>
    <div class="fa-bar-val">~$4–6M</div>
  </div>
  <div class="fa-bar-row">
    <div class="fa-bar-lbl">7nm</div>
    <div class="fa-bar-track"><div class="fa-bar-fill" style="width:65%;background:var(--warn);">FinFET + EUV</div></div>
    <div class="fa-bar-val">~$10–12M</div>
  </div>
  <div class="fa-bar-row">
    <div class="fa-bar-lbl">5nm</div>
    <div class="fa-bar-track"><div class="fa-bar-fill" style="width:100%;background:var(--red);">Full EUV</div></div>
    <div class="fa-bar-val">~$15M+</div>
  </div>
  <div class="fa-bar-note">Bar length proportional to relative NRE cost. TSMC's 28nm DUV equipment is fully depreciated — only operational costs and margin are charged to customers.</div>
</div>

<p>Because the capital cost of 28nm equipment has already been paid off at TSMC and other foundries, they can offer 28nm manufacturing at a significantly lower price point — recovering only operational costs and profit margin, not amortising billions in new capital expenditure. This economic advantage makes 28nm exceptionally cost-effective for volume production.</p>

<div class="fa-img">
  <img src="{{ '/assets/images/articles/fabless/pic4.png' | relative_url }}"
       alt="Gate Structure">
  <div class="img-cap">Planar MOSFET (28nm and above) vs. FinFET structure (below 28nm) — cross-section showing how the gate wraps around the fin on three sides in FinFET geometry to suppress short-channel leakage effects.</div>
</div>

<h3>2.2 — Clock Frequency and Power Envelope</h3>
<p>The 28nm planar process is perfectly aligned with the needs of embedded processors and low-power, high-efficiency applications. Running a 28nm planar chip beyond approximately 1.5–1.8 GHz leads to a dramatic increase in power consumption and heat generation due to leakage currents and dynamic power dissipation — creating a thermal wall that is difficult and inefficient to overcome.</p>

<p>For a target RISC-V embedded processor running at 150 MHz, this limitation is entirely irrelevant. Even for high-performance automotive Electronic Control Units (ECUs) targeting up to 1.2 GHz, the 28nm planar process offers ample performance. For applications requiring clock speeds above 2.5 GHz — top-tier CPUs or AI training accelerators — the performance benefits of FinFET nodes may justify their premium cost. For the majority of IoT controllers, edge devices, and embedded systems, the leap to a FinFET process is economically unjustifiable.</p>

<div class="fa-call warn">
  <strong>The Thermal Wall</strong>
  <p>Do not design a 28nm chip expecting to push it past 1.8 GHz in production. Leakage current and dynamic power scale super-linearly above this point on planar CMOS. Clock frequency above the thermal wall should be treated as a process selection trigger, not a design parameter — if you genuinely need 2.5 GHz+, budget for 16nm FinFET and multiply your NRE accordingly.</p>
</div>

</section>

<div class="fa-sep">PDKs &amp; Workflow</div>

<!-- ── SECTION 3: PDKs ── -->
<section id="pdks">
<h2>3 — PDKs, Tool Access, and the Hybrid Workflow</h2>

<h3>3.1 — Process Design Kits</h3>
<p>The viability of any ASIC toolchain rests upon the Process Design Kit (PDK) — a collection of technology files provided by a semiconductor foundry containing the foundational data required to design manufacturable circuits for a specific process node. This includes transistor models, geometric design rules, parasitic extraction data, and pre-characterised standard cell libraries.</p>

<p>Historically, PDKs were treated as highly confidential intellectual property, accessible only under strict Non-Disclosure Agreements (NDAs). The open-source hardware movement gained critical momentum when foundries began releasing open PDKs for mature process nodes:</p>

<ul style="color:var(--text);padding-left:1.4rem;margin-bottom:1rem;">
  <li style="margin-bottom:0.5rem;"><span class="t">SkyWater SKY130</span> (130nm) — Released as a fully open-source PDK, serving as the foundational proving ground for modern open-source EDA tools. The first tape-out-ready open PDK, produced in partnership with Google.</li>
  <li style="margin-bottom:0.5rem;"><span class="t">GlobalFoundries GF180MCU</span> (180nm) — Made publicly available, targeting low-cost, mixed-signal, and microcontroller-focused designs.</li>
  <li><span class="t">OpenRPDK28</span> (28nm template) — Developed by RIOS Lab as an open-source PDK template that mimics industrial 28nm technology, enabling design exploration and layout dry-runs before porting to the secure NDA environment.</li>
</ul>

<p>For commercial foundries such as TSMC or SMIC, access to the actual 28nm PDK requires a corporate NDA signed through a silicon broker or aggregator — MOSIS, imec IC-link, VLSIShuttle, Muse Semiconductor, or Europractice. These brokers act as the legal interface between the startup and the foundry, handling contract administration, NDA management, MPW slot booking, and sign-off verification services.</p>

<h3>3.2 — The Hybrid Workflow for TSMC 28nm</h3>
<p>Using open-source EDA tools to design a commercial chip on a proprietary node like TSMC 28nm is possible, but it requires a carefully managed hybrid workflow. Open-source tools like OpenROAD and Yosys are highly capable of handling the placement and routing mathematics for a 28nm design — even down to 5nm — however, TSMC will not accept a raw design file unless it has been verified by industry-standard commercial sign-off tools. The critical bridge is the silicon broker's Calibre verification service.</p>


<div class="fa-pipeline">

  <div class="fa-pstep">
    <div class="fa-picon">S1</div>
    <div class="fa-pbody">
      <h4>Legal Foundation</h4>
      <p>TSMC and silicon brokers will not sign contracts with individuals or loose collectives. Register as a formal private limited company with a commercial business address (an incubation centre works perfectly), a corporate website, and a corporate email domain. This is a non-negotiable prerequisite — not a formality.</p>
    </div>
  </div>

  <div class="fa-pstep">
    <div class="fa-picon">S2</div>
    <div class="fa-pbody">
      <h4>Legal PDK Access via Broker</h4>
      <p>Apply for access through a commercial aggregator such as MOSIS, imec IC-link, or VLSIShuttle. You sign a corporate NDA with the broker — this grants your startup legal access to the TSMC 28nm PDK and standard cell libraries without requiring direct engagement with TSMC, which reserves direct customer relationships for high-volume accounts.</p>
      <span class="fa-ptool">MOSIS</span><span class="fa-ptool">imec IC-link</span><span class="fa-ptool">VLSIShuttle</span><span class="fa-ptool">Muse Semi</span>
    </div>
  </div>

  <div class="fa-pstep">
    <div class="fa-picon">S3</div>
    <div class="fa-pbody">
      <h4>Extract Non-Proprietary PDK Files</h4>
      <p>TSMC's native PDK is built for Cadence/Synopsys proprietary environments. To use open-source tools, extract the standard, non-proprietary files from inside the PDK package: <span class="t">.lib</span> (Liberty timing files for synthesis), <span class="t">.lef</span> (Library Exchange Format for physical cell geometries), and <span class="t">.v</span> (Verilog structural models for simulation). These formats are vendor-neutral and fully compatible with Yosys and OpenROAD.</p>
    </div>
  </div>

  <div class="fa-pstep">
    <div class="fa-picon">S4</div>
    <div class="fa-pbody">
      <h4>Open-Source Physical Design</h4>
      <p>Set up a containerised open-source toolchain (OpenLane or OpenROAD-flow-scripts). Use <span class="t">Verilator</span> or <span class="t">Icarus Verilog</span> for functional simulation. Synthesise RTL to gate-level netlist via <span class="t">Yosys</span> using the extracted 28nm <span class="t">.lib</span> files. Run <span class="t">OpenROAD</span> for floorplanning, placement, Clock Tree Synthesis (CTS), and detailed routing using the <span class="t">.lef</span> files. Output: a raw GDSII layout file ready for sign-off.</p>
      <span class="fa-ptool">Yosys</span><span class="fa-ptool">OpenROAD</span><span class="fa-ptool">Verilator</span><span class="fa-ptool">OpenLane</span><span class="fa-ptool">KLayout</span>
    </div>
  </div>

  <div class="fa-pstep">
    <div class="fa-picon">S5</div>
    <div class="fa-pbody">
      <h4>Commercial Sign-Off — The Bridge</h4>
      <p>Open-source physical verification tools (Magic, Netgen) cannot process TSMC's highly complex 28nm DRC and LVS decks. TSMC will reject any GDSII not verified by a commercial sign-off engine such as Siemens Calibre. Rather than purchasing a Calibre licence (which would cost more than the MPW slot itself), pay the silicon broker for their sign-off verification service. They run Calibre on their servers, return the error logs, and you fix the layout in your open-source tools until it passes clean.</p>
      <span class="fa-ptool">Siemens Calibre</span><span class="fa-ptool">Cadence Pegasus</span><span class="fa-ptool">Synopsys IC Validator</span>
    </div>
  </div>

  <div class="fa-pstep">
    <div class="fa-picon">S6</div>
    <div class="fa-pbody">
      <h4>Manufacturing &amp; Packaging</h4>
      <p>Once the design passes the broker's commercial sign-off check, the broker submits the GDSII directly to TSMC for the next available MPW shuttle run. Manufactured dies arrive at your doorstep approximately 3–4 months after tape-out. Ship the bare dies to a prototype packaging service (Quik-Pak, Novapack). Packaged chips arrive 2–4 weeks after that.</p>
      <span class="fa-ptool">TSMC CyberShuttle®</span><span class="fa-ptool">SMIC MPW</span><span class="fa-ptool">Quik-Pak</span><span class="fa-ptool">Novapack</span>
    </div>
  </div>

</div><!-- end pipeline -->

<h3>3.3 — Commercial EDA: The Startup Escape Hatch</h3>
<p>If your startup wants to completely bypass the open-source workflow and use the official gold-standard commercial EDA software that TSMC natively accepts, EDA vendors all offer Startup Accelerator Programs that slash standard enterprise costs by 80–90%. On-premise installation requires applying to the Synopsys Startup Program or Cadence Startup Partner Program. To qualify, your company must be under 5 years old, under $10M in valuation, with annual revenue close to zero.</p>

<!-- EDA Subscription cost chart -->
<div class="fa-eda-chart">
  <div class="fa-bar-hd">Estimated Annual Cost Per Single-User Seat — TSMC 28nm Digital Implementation Flow</div>
  <div class="fa-eda-legend">
    <span><span class="dot" style="background:var(--red);"></span>Enterprise Retail</span>
    <span><span class="dot" style="background:var(--acc);"></span>Startup Discount (~85% off)</span>
  </div>
  <div class="fa-eda-row">
    <div class="fa-eda-tool">Synopsys Fusion</div>
    <div class="fa-eda-bar-wrap"><div class="fa-eda-bar" style="width:95%;background:var(--red);">$450K+/yr</div></div>
    <div class="fa-eda-bar-wrap"><div class="fa-eda-bar" style="width:14%;background:var(--acc);">~$60K/yr</div></div>
  </div>
  <div class="fa-eda-row">
    <div class="fa-eda-tool">Cadence Genus+Innovus</div>
    <div class="fa-eda-bar-wrap"><div class="fa-eda-bar" style="width:90%;background:var(--red);">$420K+/yr</div></div>
    <div class="fa-eda-bar-wrap"><div class="fa-eda-bar" style="width:13%;background:var(--acc);">~$55K/yr</div></div>
  </div>
  <div class="fa-eda-row">
    <div class="fa-eda-tool">Siemens Calibre</div>
    <div class="fa-eda-bar-wrap"><div class="fa-eda-bar" style="width:80%;background:var(--red);">$380K+/yr</div></div>
    <div class="fa-eda-bar-wrap"><div class="fa-eda-bar" style="width:12%;background:var(--acc);">~$50K/yr</div></div>
  </div>
  <div class="fa-eda-row">
    <div class="fa-eda-tool">Ansys RaptorX</div>
    <div class="fa-eda-bar-wrap"><div class="fa-eda-bar" style="width:55%;background:var(--red);">$260K+/yr</div></div>
    <div class="fa-eda-bar-wrap"><div class="fa-eda-bar" style="width:9%;background:var(--acc);">~$38K/yr</div></div>
  </div>
  <div class="fa-eda-row">
    <div class="fa-eda-tool">Silvaco Victory</div>
    <div class="fa-eda-bar-wrap"><div class="fa-eda-bar" style="width:40%;background:var(--red);">$190K+/yr</div></div>
    <div class="fa-eda-bar-wrap"><div class="fa-eda-bar" style="width:7%;background:var(--acc);">~$28K/yr</div></div>
  </div>
  <div class="fa-bar-note">Startup discount programmes require: company ≤5 years old, valuation &lt;$10M, annual revenue near zero. Cloud pay-per-use during a 2-month synthesis/P&amp;R sprint typically totals $20K–$35K for the entire project lifecycle — the most cost-effective option for an early-stage startup.</div>
</div>


</section>

<div class="fa-sep">EDA Tooling</div>

<!-- ── SECTION 4: EDA TOOLING ── -->
<section id="eda-tooling">
<h2>4 — Open-Source EDA Tooling: RTL to GDSII in Seven Steps</h2>

<h3>4.1 — FPGA vs. ASIC Architecture</h3>
<p>In an FPGA development environment, the physical substrate is pre-fabricated — the vendor's compiler automatically maps logical operations into pre-allocated Lookup Tables, Block RAMs, and rigid global clock distribution networks. Designing an ASIC on the TSMC 28nm node requires the physical realisation of every transistor, standard cell, custom memory macro, power rail, and clock tree wire from the ground up. The transition is summarised below.</p>

<div class="fa-tbl-wrap">
<table class="fa-tbl">
<thead><tr>
  <th>Attribute</th>
  <th class="col-a">FPGA Prototyping</th>
  <th class="col-b">ASIC @ 28nm</th>
</tr></thead>
<tbody>
<tr>
  <td class="attr">Logic Realization</td>
  <td class="col-a">Configurable LUTs &amp; flip-flops with fixed physical boundaries</td>
  <td class="col-b">Standard Cell Libraries — physical layouts of gates (NAND, NOR, AOI, DFF)</td>
</tr>
<tr>
  <td class="attr">Interconnect Physics</td>
  <td class="col-a">Segmented, pre-routed copper tracks with high intrinsic resistance and programmable switch matrices</td>
  <td class="col-b">Custom-routed metal layers (9–11 copper layers) optimised for minimum wire length and delay</td>
</tr>
<tr>
  <td class="attr">Clock Distribution</td>
  <td class="col-a">Hardwired low-skew buffers (BUFG, BUFGCE) through dedicated clock networks</td>
  <td class="col-b">Synthesised Clock Trees built from clock buffers/inverters, dynamically balanced to minimise skew and insertion delay</td>
</tr>
<tr>
  <td class="attr">Memory Architecture</td>
  <td class="col-a">Pre-allocated BRAMs and UltraRAMs with fixed ports, aspect ratios, and positions</td>
  <td class="col-b">Custom compiler-generated SRAM macros tailored to exact word counts, bit widths, and multiplexing factors</td>
</tr>
<tr>
  <td class="attr">Timing Sign-Off</td>
  <td class="col-a">Highly pessimistic vendor-packaged timing models; physical layout failures impossible</td>
  <td class="col-b">Multi-Corner Multi-Mode (MCMM) STA accounting for extreme physical variations and lithographic defects</td>
</tr>
<tr>
  <td class="attr">Mistakes</td>
  <td class="col-a">Corrected with a bitstream re-upload — minutes of work</td>
  <td class="col-b">A mistake after tape-out costs months and tens of thousands of dollars to correct</td>
</tr>
<tr>
  <td class="attr">Lithographic Constraints</td>
  <td class="col-a">Abstracted by FPGA vendor; not exposed to the engineer</td>
  <td class="col-b">Strict physical rules: double patterning, density limits, antenna effects, ESD protection</td>
</tr>
</tbody>
</table>
</div>

<h3>4.2 — Environment Determinism: Docker and Nix</h3>
<p>Before writing a single line of RTL, standardise the toolchain environment. Use <span class="t">Nix Flakes</span> or <span class="t">Docker</span> to package the compiler, simulator, and physical design tools with specific pinned version numbers. The Titan-I project distributes pre-built Docker containers and Nix environments containing specific, pinned versions of Verilator, Spike, and the OpenROAD toolchain — ensuring that every engineer on the team synthesises identical netlists and identical layouts. This eliminates the "works on my machine" failure mode, which is catastrophically expensive when discovered after a $60K tape-out.</p>

<h3>4.3 — The OpenRPDK28 Bridge</h3>
<p>Because TSMC 28nm physical design rules are protected under strict NDAs, direct integration with open-source tools can be challenging. The academic-to-industrial bridge <span class="t">OpenRPDK28</span>, developed by RIOS Lab at Peking University, acts as an open-source PDK template that mimics industrial 28nm technology. It provides open-source cell libraries, symbols, and SPICE models; preliminary design rules, layer maps, and ESD structures; and runsets for physical verification (DRC/LVS). Use OpenRPDK28 for initial physical design exploration and layout dry-runs before porting the design into the secure foundry-NDA environment. This practice can catch gross physical violations before the clock is ticking on paid broker verification runs.</p>

<h3>4.4 — Detailed Physical Design Pipeline</h3>

<h4>Step 1 — High-Level RTL Design with Chisel</h4>
<p>Traditional Verilog and SystemVerilog are static and prone to scaling errors in highly parallel designs. For complex designs, use <span class="t">Chisel</span> (Constructing Hardware in a Scala Embedded Language) — it allows hardware engineers to write object-oriented generators that programmatically output highly optimised, synthesisable Verilog, adjusting parameters such as number of execution lanes, cache size, or bus widths without error-prone manual editing. The Titan-I project uses Chisel to generate a full RISC-V vector processor from a parameterised description — changing lane count from 4 to 8 takes a parameter edit, not a Verilog rewrite.</p>

<h4>Step 2 — Verification and Co-Simulation</h4>
<p>Before committing to physical design, achieve full functional verification using open-source simulation engines. <span class="t">Verilator</span> compiles synthesisable Verilog directly into highly optimised C++ code, achieving cycle-accurate execution speeds orders of magnitude faster than interpreted simulators like ModelSim. <span class="t">Cocotb</span> drives test benches with Python co-routines, enabling modern verification techniques, assertions, and randomised testing without a commercial UVM licence.</p>

<p>For CPU designs, run your Verilated RTL in lockstep with the golden <span class="t">Spike</span> Instruction Set Simulator. Spike checks register states on every instruction commit, flagging functional bugs instantly before synthesis. Any discrepancy between Spike's architectural model and your RTL implementation is caught at zero NRE cost — before a single dollar of mask money is spent.</p>

<h4>Step 3 — Logic Synthesis via Yosys</h4>
<p><span class="t">Yosys</span>, the premier open-source synthesis engine, parses SystemVerilog files, performs logical optimisations, and maps the design to the TSMC 28nm standard cells using technology mapping scripts and the extracted <span class="t">.lib</span> files. Key considerations for 28nm:</p>

<ul style="color:var(--text);padding-left:1.4rem;margin-bottom:1rem;">
  <li style="margin-bottom:0.5rem;"><strong>Track Height Selection:</strong> Select 7-track (7T) high-density cells for logic-heavy, area-constrained sub-blocks, or 9-track (9T) standard cells for speed-critical modules.</li>
  <li style="margin-bottom:0.5rem;"><strong>Multi-Threshold Voltage (Vt) Partitioning:</strong> Map non-critical paths to high-Vt (HVT) cells to reduce static leakage current; map critical timing paths to low-Vt (LVT) cells to maximise performance.</li>
  <li><strong>DFT Insertion:</strong> Insert scan chains and memory Built-In Self-Test (BIST) logic during or immediately after synthesis to make the fabricated silicon testable. Silicon testing is not optional — without DFT, a failed chip tells you nothing useful about why it failed.</li>
</ul>

<h4>Step 4 — Floorplanning and Macro Placement</h4>
<p>Memory blocks (SRAM macros generated via TSMC's compiler) and analog IP must be floorplanned carefully. Hand-placing dozens of SRAMs in a complex vector processor often leads to routing congestion and clock distribution issues. Key rules: enforce placement halos around SRAM boundaries — keep at least 2–3 μm clear of standard cells to ensure macro pins are fully accessible by the routing engine. Design the Power Delivery Network (PDN) in OpenROAD by routing a low-impedance mesh of horizontal and vertical power straps on upper metals (M7, M8, M9) to combat dynamic IR drop, which becomes a yield risk in high-frequency designs.</p>


<h4>Step 5 — Placement, CTS, and Routing in OpenROAD</h4>
<p>Once the floorplan is fixed, use the OpenROAD tool suite to execute the core physical design flow autonomously:</p>
<ul style="color:var(--text);padding-left:1.4rem;margin-bottom:1rem;">
  <li style="margin-bottom:0.5rem;"><strong>Global Placement (RePlAce) &amp; Detail Placement (OpenDP):</strong> Distribute standard cells uniformly across rows. Well-tap cells must be placed every 30–40 μm to prevent latch-up.</li>
  <li style="margin-bottom:0.5rem;"><strong>Clock Tree Synthesis (TritonCTS):</strong> Synthesises a balanced clock tree using symmetric H-tree topologies. Apply Non-Default Routing (NDR) rules to clock lines — double spacing and double width — to minimise clock skew and coupling jitter.</li>
  <li><strong>Detailed Routing (TritonRoute):</strong> Assigns nets to specific copper tracks. At 28nm, the router must natively support double patterning (Litho-Etch-Litho-Etch, LELE) rules on lower critical metal layers (M1, M2), assigning mask colours to resolve pitch conflicts. TritonRoute must also insert antenna diodes near standard-cell inputs to prevent dielectric charge damage during plasma etching.</li>
</ul>

<h4>Step 6 — Parasitic Extraction and Static Timing Analysis</h4>
<p>Extract actual wire resistances and capacitances to generate standard SPEF files. Run <span class="t">OpenSTA</span> to verify timing across multiple corners. Unlike older nodes, 28nm requires Parametric On-Chip Variation (POCV) modelling to dynamically calculate local variations based on physical path depth — preventing overly pessimistic margins while catching real violations. Verify timing closure using standard setup and hold equations across all required PVT (Process-Voltage-Temperature) corners.</p>

<h4>Step 7 — Physical Verification and DFM in KLayout</h4>
<p><span class="t">KLayout</span> runs the final local verification passes before broker submission:</p>
<ul style="color:var(--text);padding-left:1.4rem;margin-bottom:1rem;">
  <li style="margin-bottom:0.5rem;"><strong>DRC (Design Rule Checking):</strong> Verify minimum spacing, widths, and enclosure rules using OpenRPDK28 rule decks or the broker's preliminary decks.</li>
  <li style="margin-bottom:0.5rem;"><strong>LVS (Layout vs. Schematic):</strong> Compare the extracted SPICE netlist from KLayout against the synthesised gate netlist to ensure they describe identical circuits.</li>
  <li><strong>DFM (Design for Manufacturability):</strong> Run automated Python scripts in KLayout to insert dummy metal fill across empty regions — ensuring a uniform metal density profile to prevent planarisation dishing — and insert redundant vias on all critical routing paths to prevent single-via open failures in production.</li>
</ul>


<h3>4.5 — Verification Sign-Off Scenarios and Costs</h3>
<p>The broker's sign-off verification service comes in four distinct scenarios with very different cost implications. Choosing the right scenario requires understanding your open-source toolchain's maturity and your schedule tolerance.</p>

<div class="fa-verif-grid">
  <div class="fa-verif">
    <span class="vn">Option A — Free</span>
    <span class="vc">$0</span>
    <p>1–3 pre-shuttle sign-off runs are included in the baseline MPW slot price. The broker includes these to protect the rest of the wafer from being contaminated by a defective design submission.</p>
  </div>
  <div class="fa-verif">
    <span class="vn">Option B — Extra Runs</span>
    <span class="vc">$3K–$6K</span>
    <p>Per run, if your open-source toolchain outputs messy GDSII that exhausts the free runs. The broker bills a flat engineering fee each time they spin up their Calibre cluster to re-verify your layout fixes.</p>
  </div>
  <div class="fa-verif">
    <span class="vn">Option C — Dry Run</span>
    <span class="vc">$5K–$10K</span>
    <p>A standalone verification run months before buying an MPW slot — to check if your open-source flow can hit 28nm metrics at all. The broker runs your GDSII through the golden deck and returns the raw Calibre error database.</p>
  </div>
  <div class="fa-verif">
    <span class="vn">Option D — Full Package</span>
    <span class="vc">$15K–$35K</span>
    <p>The broker's physical design engineers act as your hands — actively running verification, fixing advanced 28nm issues (density violations, antenna effects, dummy metal fill), and bringing your layout to 100% compliance.</p>
  </div>
</div>

<div class="fa-call warn">
  <strong>Practical Recommendation</strong>
  <p>Run a Dry Run (Option C) approximately 2 months before your target MPW shuttle window. This gives you time to fix systematic flow issues — mis-configured DRC rules, layer-map errors, density violations — without burning your free shuttle-included runs on avoidable mistakes. Factor this $5–10K into your budget from day one.</p>
</div>

</section>

<div class="fa-sep">Titan-I</div>

<!-- ── SECTION 5: TITAN-I ── -->
<section id="titan">
<h2>5 — Titan-I: Open-Source Silicon at Scale</h2>

<p>A common concern among system designers is whether open-source hardware tools and architectures can produce high-performance, manufacturing-worthy silicon. Historically, complex high-performance processors were considered the exclusive domain of proprietary EDA toolchains and closed-source IP. The Titan-I project challenges this view definitively.</p>

<h3>5.1 — Project Origin</h3>
<p>Titan-I (T1) is an open-source, high-performance out-of-order (OoO) RISC-V Vector (RVV) processor core. It was developed by a collaborative research group including Jiuyang Liu, Qinjun Li, Yunqian Luo, and Mingyu Gao, with contributions spanning Huazhong University of Science and Technology, Tsinghua University, and the Institute of Software at the Chinese Academy of Sciences (ISCAS). The processor was presented at the 58th IEEE/ACM International Symposium on Microarchitecture (MICRO 2025) in Seoul, South Korea — one of the most selective venues in computer architecture research.</p>


<h3>5.2 — Architecture</h3>
<p>Titan-I is designed to scale both Instruction-Level Parallelism (ILP) and Data-Level Parallelism (DLP) by decoupling scalar instruction execution from a wide, multi-lane parallel vector execution engine. The architecture fully complies with the official RISC-V Vector Extension (RVV 1.0) specification, enabling efficient parallel computation of multi-precision integers and floating-point datatypes. The microarchitecture is optimised for highly parallelised applications — deep neural networks, HPC kernels, and cryptographic workloads.</p>

<div class="fa-titan">
  <div class="fa-titan-row">
    <div class="fa-titan-k">ISA</div>
    <div class="fa-titan-v">RISC-V RV64GV (RVV 1.0 compliant)</div>
  </div>
  <div class="fa-titan-row">
    <div class="fa-titan-k">Execution</div>
    <div class="fa-titan-v">Out-of-order scalar + multi-lane in-order vector</div>
  </div>
  <div class="fa-titan-row">
    <div class="fa-titan-k">Implementation Language</div>
    <div class="fa-titan-v">Chisel (Scala DSL), generates synthesisable Verilog</div>
  </div>
  <div class="fa-titan-row">
    <div class="fa-titan-k">Physical Design Tool</div>
    <div class="fa-titan-v">OpenROAD (fully open-source)</div>
  </div>
  <div class="fa-titan-row">
    <div class="fa-titan-k">Nodes Evaluated</div>
    <div class="fa-titan-v">Synthesis evaluated down to 7nm technology</div>
  </div>
  <div class="fa-titan-row">
    <div class="fa-titan-k">Simulation</div>
    <div class="fa-titan-v">Verilator + Spike ISS co-simulation (lockstep verification)</div>
  </div>
  <div class="fa-titan-row">
    <div class="fa-titan-k">Target Workloads</div>
    <div class="fa-titan-v">DNN inference, HPC kernels, cryptographic acceleration</div>
  </div>
  <div class="fa-titan-row">
    <div class="fa-titan-k">Published</div>
    <div class="fa-titan-v">IEEE/ACM MICRO 2025, Seoul, South Korea</div>
  </div>
</div>

<h3>5.3 — Design and Physical Execution</h3>
<p>Titan-I is implemented in Chisel, which raises the level of hardware design abstraction by providing object-oriented programming, functional programming, and strongly-typed parameterised generators. Instead of manual edits to static Verilog code, Chisel allows the T1 architecture to be configured programmatically — adjusting parameters such as vector register file size, vector register length, and number of physical execution lanes, causing the Chisel generator to dynamically restructure the execution datapath and output optimised synthesisable Verilog.</p>

<p>The physical design flow of Titan-I is executed using the open-source OpenROAD physical synthesis tool suite. This automated, scriptable flow performs physical synthesis, placement, clock tree synthesis, and detailed routing — with successful physical synthesis evaluations down to 7nm technology. This demonstrates conclusively that open-source tools can resolve the complex lithographic and electrical design rules of modern sub-10nm silicon manufacturing.</p>

<div class="fa-pull">
  <p>Titan-I is not an academic toy — it is a full, out-of-order vector processor synthesised to real silicon geometry using entirely free tools. The question is no longer whether open-source EDA can do this; it is whether your team is disciplined enough to execute the flow.</p>
  <cite>— On the significance of the Titan-I result</cite>
</div>


</section>

<div class="fa-sep">Economics</div>

<!-- ── SECTION 6: FOUNDRY ECONOMICS ── -->
<section id="foundry">
<h2>6 — Foundry Economics: TSMC vs. SMIC</h2>

<p>Once a design has been completed using an open-source toolchain and a target node selected, the next critical step is engaging with a semiconductor foundry for fabrication. The two dominant players in the mature-node space are TSMC and SMIC. While both offer 28nm manufacturing services, their business models, cost structures, and geopolitical contexts create distinctly different value propositions.</p>

<div class="fa-foundry-grid">
  <div class="fa-fcard tsmc">
    <div class="fn">TSMC</div>
    <div class="fs">Taiwan · Industry Gold Standard</div>
    <div class="fr"><span class="fk">Market share (2024)</span><span class="fv">34% pure-play</span></div>
    <div class="fr"><span class="fk">28nm wafer cost</span><span class="fv">$3,000–$3,500/mm²</span></div>
    <div class="fr"><span class="fk">Full mask set NRE</span><span class="fv">$1.5–2.5M</span></div>
    <div class="fr"><span class="fk">MPW slot (4mm², 40–50 dies)</span><span class="fv">$52K–$64K</span></div>
    <div class="fr"><span class="fk">IP ecosystem</span><span class="fv">Extensive (PCIe, DDR, SerDes)</span></div>
    <div class="fr"><span class="fk">Geopolitical risk</span><span class="fv">Moderate</span></div>
    <div class="fr"><span class="fk">Western export compliance</span><span class="fv">Straightforward</span></div>
    <span class="fa-tag prem">Premium yield</span>
  </div>
  <div class="fa-fcard smic">
    <div class="fn">SMIC</div>
    <div class="fs">China · Budget Competitor</div>
    <div class="fr"><span class="fk">Node options</span><span class="fv">28nm PolySiON / HKMG</span></div>
    <div class="fr"><span class="fk">28nm wafer cost</span><span class="fv">$2,200–$2,600/mm²</span></div>
    <div class="fr"><span class="fk">Full mask set NRE</span><span class="fv">$0.8–1.5M</span></div>
    <div class="fr"><span class="fk">MPW slot (2–5mm²)</span><span class="fv">$20K–$65K</span></div>
    <div class="fr"><span class="fk">Price vs. TSMC</span><span class="fv">~30% cheaper</span></div>
    <div class="fr"><span class="fk">Geopolitical risk</span><span class="fv">Significant</span></div>
    <div class="fr"><span class="fk">Crypto IP compliance</span><span class="fv">Complex — ECCN required</span></div>
    <span class="fa-tag budg">Lower cost</span>
    <span class="fa-tag risk">Geo risk</span>
  </div>
</div>

<div class="fa-call danger">
  <strong>Geopolitical Caveat — SMIC + Cryptographic IP</strong>
  <p>Designs containing cryptographic hardware fall under strict dual-use export regulations — the Wassenaar Arrangement and US Export Administration Regulations (EAR). Sending a tape-out with advanced crypto IP to SMIC (Mainland China) requires rigorous legal compliance, export licences, and ECCN (Export Control Classification Number) declarations. Any future regulatory changes or tightening of export controls could retroactively impact supply-chain continuity. Taping out at TSMC (Taiwan) is generally a smoother administrative process for Western entities, though ECCN declarations remain mandatory regardless of foundry choice. Retain qualified export-control legal counsel before committing to a SMIC tape-out containing crypto IP.</p>
</div>

<h3>6.1 — MPW Silicon Fabrication Costs</h3>
<p>Foundries and shuttle aggregators price MPW runs per square millimetre, but strictly enforce minimum area rules. Even if your chip is 3mm², you will pay for the foundry's minimum block size (often 4mm² or 9mm²). An MPW run typically delivers 40–100 bare dies.</p>

<div class="fa-tbl-wrap">
<table class="fa-tbl cost">
<thead><tr>
  <th>Foundry &amp; Node</th>
  <th>Est. Cost / mm²</th>
  <th>Typical Min. Area</th>
  <th>Estimated Silicon Cost (40–100 dies)</th>
</tr></thead>
<tbody>
<tr>
  <td class="ci">TSMC 28nm (HPC/HPC+)</td>
  <td class="cv">$13K–$16K</td>
  <td>1mm² (mini@sic)</td>
  <td class="cv">$52K–$64K+ (4mm²)</td>
</tr>
<tr>
  <td class="ci">TSMC 40nm (LP/G)</td>
  <td class="cv">$6K–$10K</td>
  <td>3mm²</td>
  <td class="cv">$18K–$30K</td>
</tr>
<tr>
  <td class="ci">SMIC 28nm (PolySiON/HKMG)</td>
  <td class="cv">$10K–$13K</td>
  <td>2–5mm²</td>
  <td class="cv">$20K–$65K</td>
</tr>
<tr>
  <td class="ci">SMIC 40nm (LL/G)</td>
  <td class="cv">$4K–$7K</td>
  <td>3–4mm²</td>
  <td class="cv">$12K–$28K</td>
</tr>
</tbody>
</table>
</div>

<p>SMIC is generally ~30% cheaper than TSMC for mature nodes — acting as a highly competitive option if you are price-sensitive at the prototyping stage and your design does not contain regulated IP.</p>

</section>

<div class="fa-sep">Complete Costs</div>

<!-- ── SECTION 7: COSTS ── -->
<section id="costs">
<h2>7 — Complete Cost Breakdown: First 50 Packaged Prototypes</h2>

<p>Taking a design from a 100% complete GDSII to fifty packaged prototypes is a major milestone. The baseline assumption: a dual-core RISC processor with embedded SRAM, cryptographic accelerators (AES, SHA, RSA/ECC), and a Root of Trust — a realistic starting point for many security-focused embedded designs. At 40nm or 28nm with an optimised layout, this scope typically requires a die area between 4mm² and 9mm².</p>

<div class="fa-tbl-wrap">
<table class="fa-tbl cost">
<thead><tr>
  <th>Line Item</th>
  <th>Typical Cost (TSMC 28nm)</th>
  <th>Notes</th>
</tr></thead>
<tbody>
<tr>
  <td class="ci">MPW prototype slot (4mm², ~40–50 dies)</td>
  <td class="cv">$52K–$64K</td>
  <td class="cn">SMIC ~30% lower; minimum block size 4mm² even if design is smaller</td>
</tr>
<tr>
  <td class="ci">Broker sign-off verification (Calibre)</td>
  <td class="cv">$0–$35K</td>
  <td class="cn">1–3 free pre-shuttle runs included; extras $3K–$6K per run; full package $15K–$35K</td>
</tr>
<tr>
  <td class="ci">Commercial EDA (cloud, startup pricing)</td>
  <td class="cv">$20K–$35K</td>
  <td class="cn">Cloud pay-per-use during final 2-month sprint; startup programmes slash enterprise rates by 80–90%</td>
</tr>
<tr>
  <td class="ci">Prototype packaging (~50 units)</td>
  <td class="cv">$4.5K–$8K</td>
  <td class="cn">Open-cavity QFNs or ceramic PGAs; $2–3K setup + $50–100/chip for wire-bond assembly</td>
</tr>
<tr>
  <td class="ci" style="border-top:1px solid var(--acc);"><strong>Total</strong></td>
  <td class="cv" style="border-top:1px solid var(--acc);font-size:0.88rem;color:#f0d090;"><strong>$76K–$142K</strong></td>
  <td class="cn" style="border-top:1px solid var(--acc);">Budget $100–200K with contingency. SMIC brings this to ~$55–100K.</td>
</tr>
</tbody>
</table>
</div>

<h3>7.1 — Prototype Packaging Details</h3>
<p>Because you only need 40–50 units, designing a custom organic substrate (like a standard mass-market BGA) is entirely cost-prohibitive — custom tooling NREs alone run $10,000–$30,000 just for the substrate design. Instead, use prototype packaging services with standard, off-the-shelf packages that require no custom tooling:</p>

<ul style="color:var(--text);padding-left:1.4rem;margin-bottom:1rem;">
  <li style="margin-bottom:0.5rem;"><strong>Open-Cavity QFNs or Ceramic PGAs:</strong> The die is glued into a pre-made package and wire-bonded based on a custom bonding diagram.</li>
  <li style="margin-bottom:0.5rem;"><strong>Setup Fee:</strong> ~$2,000–$3,000 for creating the wire-bond profile and machine setup.</li>
  <li style="margin-bottom:0.5rem;"><strong>Per-Unit Cost:</strong> ~$50–$100 per chip for low-volume manual/semi-automated assembly.</li>
  <li><strong>Total:</strong> $4,500–$8,000 for approximately 50 packaged units.</li>
</ul>


<h3>7.2 — Hidden Execution Factors</h3>
<p><strong>Lead Times:</strong> GDSII to bare die on a mature node MPW typically takes 3–4 months. Prototype packaging adds another 2–4 weeks. You will be bound to the foundry's pre-published shuttle schedule — typically 3–4 runs per year for these specific nodes. Missing the tape-out window by even one day means waiting 3 months for the next one. Build the shuttle calendar into your project plan from day one, working backwards from your tape-out date to set RTL freeze, verification completion, and sign-off milestones.</p>

<p><strong>Shuttle Access Fees:</strong> If you are not a direct customer of the foundry — which requires massive volume commitments — you will go through a Channel Partner/Aggregator. They may charge a one-time onboarding or IP-handling fee in addition to the per-slot price. Budget $2,000–$5,000 for this.</p>

<p><strong>EDA Programme Timing:</strong> Synopsys and Cadence startup programme applications can take 4–8 weeks to process. Apply well before you need access — do not start this process when you are 3 weeks from your synthesis sprint.</p>

</section>

<div class="fa-sep">Roadmap</div>

<!-- ── SECTION 8: ROADMAP ── -->
<section id="roadmap">
<h2>8 — Roadmap: From First Tape-Out to Full Production</h2>

<p>Armed with an understanding of the economic landscape, the power of open-source tools, and the technical nuances of the ASIC design flow, a clear strategic roadmap emerges. The recommended strategy is a phased approach that leverages cost-sharing manufacturing models before committing to a full production run — retiring technical risk before serious capital is spent.</p>

<div class="fa-phases">
  <div class="fa-phase">
    <div class="fa-phase-n">1</div>
    <h4>Phase 1 — MPW Shuttle Prototype</h4>
    <p>Fabricate a prototype using a Multi-Project Wafer service — TSMC CyberShuttle® or SMIC MPW. The primary goal is not a final product but to validate the RTL design at the silicon level, verify real-world functionality, and collect initial yield data. This yield data provides a realistic basis for calculating per-die cost for future production runs and identifies any unforeseen physical design issues. Budget: $52K–$80K total.</p>
  </div>
  <div class="fa-phase">
    <div class="fa-phase-n">2</div>
    <h4>Phase 2 — MLM Refinement</h4>
    <p>Based on MPW learnings, employ a Multi-Layer Mask (MLM) or Multi-Layer Reticle (MLR) service — combining up to four design layers onto a single physical mask plate. This significantly lowers the initial investment compared to a full mask set, enabling low-to-medium volume production of hundreds of units on a stable, validated design without the high cost of full-volume tooling. Budget: $200K–$600K.</p>
  </div>
  <div class="fa-phase">
    <div class="fa-phase-n">3</div>
    <h4>Phase 3 — Full Production Run</h4>
    <p>Once the design achieves functional sign-off through an MPW shuttle, commit to a full production run: a dedicated mask set (NRE) and minimum wafer start order. Technical risk is mitigated because the design has been validated in silicon and timing closed across all required PVT corners. The financial stakes are high — but the engineering is de-risked. Budget: $1.5M+ NRE at TSMC 28nm.</p>
  </div>
</div>


<div class="fa-pull">
  <p>The phased strategy — proving the design on an MPW shuttle, refining through a multi-layer mask run, and only then committing to a full production mask set — allows you to retire technical risk before you spend serious capital.</p>
  <cite>— The core financial discipline of fabless silicon</cite>
</div>

</section>

<div class="fa-sep">Use Cases</div>

<!-- ── SECTION 9: USE CASES ── -->
<section id="use-cases">
<h2>9 — Extended Use Cases: Beyond the RISC-V Processor</h2>

<p>The principles and workflows outlined in this guide are not limited to RISC-V embedded processors. They can be generalised to address a wide spectrum of modern computing challenges. The 28nm open-source flow is particularly well-suited to four application domains where custom silicon delivers asymmetric competitive advantage.</p>

<div class="fa-use-grid">
  <div class="fa-uc">
    <span class="ui">⚡</span>
    <h4>AI Edge Accelerators</h4>
    <p>The 28nm node is the industry's optimal sweet spot for cost-versus-performance in edge AI inference. While advanced FinFET nodes offer superior absolute power efficiency, their mask costs are prohibitive for startups and niche architectures. A 28nm HKMG process allows designers to maximise logic density within a viable economic framework. Projects like e-GPU — an open-source, configurable RISC-V platform for TinyAI devices — demonstrate the feasibility of sophisticated compute accelerators on this flow without incurring compounding software licensing costs.</p>
  </div>
  <div class="fa-uc">
    <span class="ui">🚗</span>
    <h4>Automotive ECUs</h4>
    <p>The automotive industry is moving toward mixed-criticality SoCs where multiple operational domains run concurrently on a single chip — a challenge suited to the architectural flexibility of RISC-V. While safety-critical drive systems require ISO 26262 toolchain qualifications that open-source tools are still maturing toward, the open-flow is highly disruptive for secure telematics, infotainment, and V2X communication research. The Titan-I project's chiplet-based RISC-V SoC for secure nano-UAVs demonstrates the potential for heterogeneous, highly secure architectures using this decentralised methodology.</p>
  </div>
  <div class="fa-uc">
    <span class="ui">📡</span>
    <h4>Edge Computing &amp; IoT</h4>
    <p>The 28nm process excels in this domain by providing frequency scaling for real-time sensor fusion and local data processing while maintaining a compact physical footprint. By utilising an open-source flow, designers can strip away generic, redundant IP blocks found in commercial microcontrollers — engineering a lean, workload-optimised SoC that minimises active power dissipation. The UET-RVMCU project demonstrated successful transformation of an application-class SoC architecture into a streamlined, feature-rich microcontroller using this open-source physical design flow.</p>
  </div>
  <div class="fa-uc">
    <span class="ui">🔒</span>
    <h4>Cryptographic Hardware</h4>
    <p>The open-source nature of the entire toolchain — from processor core to physical design synthesis — enables unprecedented transparency for security auditing and custom cryptographic extensions. Hardware-native AES, SHA-3, RSA/ECC, and post-quantum lattice cores can be implemented with full auditability at the RTL and GDSII level — a feature impossible with closed commercial IP. Note: designs containing cryptographic IP are subject to strict Wassenaar/EAR dual-use export regulations regardless of foundry choice. Retain qualified export-control counsel before tape-out.</p>
  </div>
</div>

<div class="fa-img wide">
  <img src="{{ '/assets/images/articles/fabless/pic13.png' | relative_url }}"
       alt="Gate Structure">
  <div class="img-cap">Application-specific performance-cost positioning chart — showing where AI edge accelerators, automotive ECUs, IoT SoCs, and crypto engines sit relative to clock frequency, die area, and process node choice, with the 28nm sweet-spot zone highlighted.</div>
</div>

</section>

<!-- ── SECTION 10: FINAL WORDS ── -->
<section id="final">
<h2>10 — Final Words</h2>

<p>The path to fabless ASIC design has never been more open to small teams. Two barriers that once confined custom silicon to a handful of corporations — the multibillion-dollar fabrication plant and the six-figure-per-seat EDA licence — have effectively fallen away. The fabless model lets you rent world-class manufacturing through Multi-Project Wafer shuttles, while a mature open-source toolchain now carries a design all the way from RTL to a manufacturable GDSII layout. For an engineer already fluent in FPGA development, the front-end skills transfer almost directly; what you are really learning is the discipline of the back-end physical flow.</p>

<p>That openness is not the same as ease, and it is worth being honest about what the journey demands. Unlike an FPGA bitstream, a fabricated die cannot be re-uploaded — a mistake caught after tape-out costs months and tens of thousands of dollars to correct. Foundries still require final sign-off on certified commercial tools, so a hybrid flow and a working relationship with a silicon broker are unavoidable. Foundry selection is a genuine trade-off: TSMC offers premium yield and a rich IP ecosystem at a higher price, while SMIC is markedly cheaper but carries geopolitical and export-control exposure that must be managed deliberately — particularly for designs containing cryptographic IP. None of these obstacles is disqualifying, but each rewards planning over improvisation.</p>


<p>Taken as a whole, it is the economics that make the opportunity compelling. A complete, state-of-the-art design environment is now within reach of a modest budget, and the phased strategy recommended in this paper — proving the design on an MPW shuttle, refining it through a multi-layer mask run, and only then committing to a full production mask set — allows you to retire technical risk before you spend serious capital. The 28nm planar node sits at the centre of this strategy, offering the rare convergence of low cost, ample performance, and proven manufacturability for the embedded controllers, AI accelerators, automotive subsystems, and edge devices where most startups will compete.</p>

<p>For founders willing to pair that engineering discipline with sound commercial judgment, the reward is substantial: the ability to build differentiated, workload-optimised silicon that was, until very recently, the exclusive territory of the largest semiconductor firms.</p>

<p style="font-family:var(--f-head);font-size:1.05rem;font-weight:700;color:#f0f0f5;margin-top:2rem;">The tools, the foundry access, and the business model are all in place. What remains is the decision to begin — and the teams that move thoughtfully now will be the ones that define the next generation of custom hardware.</p>

<!-- References -->
<div class="fa-refs">
  <p><span class="rn">[1]</span> TSMC Open Innovation Platform® (OIP) — tsmc.com/english/dedicatedFoundry/services/Open_Innovation_Platform</p>
  <p><span class="rn">[2]</span> SkyWater SKY130 Open PDK — github.com/google/skywater-pdk</p>
  <p><span class="rn">[3]</span> GlobalFoundries GF180MCU Open PDK — github.com/google/gf180mcu-pdk</p>
  <p><span class="rn">[4]</span> OpenROAD Project — openroad.readthedocs.io</p>
  <p><span class="rn">[5]</span> Yosys Open Synthesis Suite — yosyshq.net/yosys</p>
  <p><span class="rn">[6]</span> KLayout — klayout.de</p>
  <p><span class="rn">[7]</span> Verilator — veripool.org/verilator</p>
  <p><span class="rn">[8]</span> OpenRPDK28, RIOS Lab — github.com/rioslab/openrpdk28</p>
  <p><span class="rn">[9]</span> Liu, J. et al.: Titan-I, IEEE/ACM MICRO 2025, Seoul (2025)</p>
  <p><span class="rn">[10]</span> Chisel Hardware Construction Language — chisel-lang.org</p>
  <p><span class="rn">[11]</span> Spike RISC-V ISA Simulator — github.com/riscv-software-src/riscv-isa-sim</p>
  <p><span class="rn">[12]</span> OpenLane ASIC Flow — github.com/The-OpenROAD-Project/OpenLane</p>
  <p><span class="rn">[13]</span> Siemens Calibre — eda.sw.siemens.com/en-US/ic/calibre</p>
  <p><span class="rn">[14]</span> MOSIS Service — mosis.com</p>
  <p><span class="rn">[15]</span> imec IC-link MPW — iclink.imec.be</p>
  <p><span class="rn">[16]</span> Synopsys Startup Program — synopsys.com/company/programs/startup-program</p>
  <p><span class="rn">[17]</span> Cadence Startup Partner Program — cadence.com</p>
  <p><span class="rn">[18]</span> Wassenaar Arrangement — wassenaar.org</p>
  <p><span class="rn">[19]</span> US Export Administration Regulations (EAR) — bis.doc.gov</p>
  <p><span class="rn">[20]</span> RISC-V International Vector Extension (RVV 1.0) — riscv.org/specifications</p>
  <p><span class="rn">[21]</span> Cocotb — docs.cocotb.org</p>
  <p><span class="rn">[22]</span> e-GPU TinyAI Platform — github.com/e-GPU</p>
  <p><span class="rn">[23]</span> UET-RVMCU Project — github.com/uet-rvmcu</p>
  <p><span class="rn">[24]</span> Europractice MPW Service — europractice-ic.com</p>
  <p><span class="rn">[25]</span> Muse Semiconductor — musesemi.com</p>
</div>

</section>

</div><!-- end .fa-body -->

<!-- ── SIDEBAR TOC ── -->
<aside class="fa-sidebar">
  <div class="fa-toc-hd">Contents</div>
  <nav class="fa-toc">
    <ul>
      <li data-s="summary"><a href="#summary">Executive Summary</a></li>
      <li data-s="introduction"><a href="#introduction">1 — Introduction</a></li>
      <li class="sub" data-s="introduction"><a href="#introduction">Before Fabless</a></li>
      <li class="sub" data-s="introduction"><a href="#introduction">EDA Revolution</a></li>
      <li class="sub" data-s="introduction"><a href="#introduction">FPGA → ASIC</a></li>
      <li class="sub" data-s="introduction"><a href="#introduction">MPW &amp; Large Fabs</a></li>
      <li data-s="technology"><a href="#technology">2 — Technology Tour</a></li>
      <li class="sub" data-s="technology"><a href="#technology">Why 28nm</a></li>
      <li class="sub" data-s="technology"><a href="#technology">NRE Cost Chart</a></li>
      <li class="sub" data-s="technology"><a href="#technology">Clock &amp; Power</a></li>
      <li data-s="pdks"><a href="#pdks">3 — PDKs &amp; Workflow</a></li>
      <li class="sub" data-s="pdks"><a href="#pdks">Process Design Kits</a></li>
      <li class="sub" data-s="pdks"><a href="#pdks">Hybrid Workflow Steps</a></li>
      <li class="sub" data-s="pdks"><a href="#pdks">EDA Cost Chart</a></li>
      <li data-s="eda-tooling"><a href="#eda-tooling">4 — EDA Tooling</a></li>
      <li class="sub" data-s="eda-tooling"><a href="#eda-tooling">FPGA vs ASIC Table</a></li>
      <li class="sub" data-s="eda-tooling"><a href="#eda-tooling">Design Pipeline (7 Steps)</a></li>
      <li class="sub" data-s="eda-tooling"><a href="#eda-tooling">Verification Scenarios</a></li>
      <li data-s="titan"><a href="#titan">5 — Titan-I Processor</a></li>
      <li class="sub" data-s="titan"><a href="#titan">Architecture</a></li>
      <li class="sub" data-s="titan"><a href="#titan">Physical Execution</a></li>
      <li data-s="foundry"><a href="#foundry">6 — Foundry Economics</a></li>
      <li class="sub" data-s="foundry"><a href="#foundry">TSMC vs SMIC</a></li>
      <li class="sub" data-s="foundry"><a href="#foundry">MPW Cost Table</a></li>
      <li data-s="costs"><a href="#costs">7 — Cost Breakdown</a></li>
      <li class="sub" data-s="costs"><a href="#costs">First 50 Prototypes</a></li>
      <li class="sub" data-s="costs"><a href="#costs">Hidden Factors</a></li>
      <li data-s="roadmap"><a href="#roadmap">8 — Roadmap</a></li>
      <li data-s="use-cases"><a href="#use-cases">9 — Use Cases</a></li>
      <li data-s="final"><a href="#final">10 — Final Words</a></li>
    </ul>
  </nav>
</aside>

</div><!-- end .fa-layout -->
</article>

<script>
(function(){
  var bar = document.getElementById('fa-prog');
  function upP(){
    var s=window.scrollY||window.pageYOffset;
    var t=document.documentElement.scrollHeight-window.innerHeight;
    bar.style.width=t>0?(s/t*100)+'%':'0%';
  }
  window.addEventListener('scroll',upP,{passive:true}); upP();

  var secs=['summary','introduction','technology','pdks','eda-tooling','titan','foundry','costs','roadmap','use-cases','final'];
  var its=document.querySelectorAll('.fa-toc li[data-s]');
  function upT(){
    var cur='';
    secs.forEach(function(id){
      var el=document.getElementById(id);
      if(el&&el.getBoundingClientRect().top<=115) cur=id;
    });
    its.forEach(function(li){ li.classList.toggle('on',li.dataset.s===cur); });
  }
  window.addEventListener('scroll',upT,{passive:true}); upT();

  var mb=document.getElementById('fa-mob-btn');
  var ml=document.getElementById('fa-mob-list');
  if(mb&&ml){
    mb.addEventListener('click',function(){
      var o=ml.style.display==='block';
      ml.style.display=o?'none':'block';
      mb.querySelector('span:last-child').textContent=o?'▾':'▴';
    });
    ml.querySelectorAll('a').forEach(function(a){
      a.addEventListener('click',function(){
        ml.style.display='none';
        mb.querySelector('span:last-child').textContent='▾';
      });
    });
  }

  document.querySelectorAll('.fa-toc a,.fa-mob-list a').forEach(function(a){
    a.addEventListener('click',function(e){
      var id=this.getAttribute('href').slice(1);
      var t=document.getElementById(id);
      if(t){e.preventDefault();t.scrollIntoView({behavior:'smooth',block:'start'});}
    });
  });
})();
</script>