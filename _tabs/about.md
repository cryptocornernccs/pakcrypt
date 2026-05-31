---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
pin: true
---

<style>
  /* ─── Reset Jekyll theme interference ─── */
  .page-content, .post, article, main { padding: 0 !important; margin: 0 !important; max-width: 100% !important; }
  .wrapper, .site-content, #content { max-width: 100% !important; padding: 0 !important; }

  /* ─── Google Fonts ─── */
  @import url('https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&display=swap');

  /* ─── CSS Variables ─── */
  :root {
    --ink:    #0a0a0f;
    --ink2:   #14141c;
    --muted:  #6b6b80;
    --line:   #1e1e2a;
    --accent: #00e5c0;
    --accent2: #7b61ff;
    --warm:   #ff6b35;
    --text:   #c8c8d8;
    --light:  #eeeef5;
    --card:   #111119;
    --font-head: 'Syne', sans-serif;
    --font-mono: 'DM Mono', monospace;
    --font-body: 'DM Sans', sans-serif;
    --radius: 2px;
    --gap: clamp(1rem, 4vw, 2.5rem);
  }

  /* ─── Base ─── */
  #pc-team-page * { box-sizing: border-box; margin: 0; padding: 0; }
  #pc-team-page {
    background: var(--ink);
    color: var(--text);
    font-family: var(--font-body);
    font-weight: 300;
    line-height: 1.7;
    overflow-x: hidden;
  }

  /* ─── HERO ─── */
  .pc-hero {
    position: relative;
    min-height: 100svh;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    padding: clamp(2rem, 8vw, 6rem);
    overflow: hidden;
    background: var(--ink);
  }
  .pc-hero__grid-bg {
    position: absolute; inset: 0; z-index: 0;
    background-image:
      linear-gradient(rgba(0,229,192,.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,229,192,.04) 1px, transparent 1px);
    background-size: 60px 60px;
    animation: gridDrift 30s linear infinite;
  }
  @keyframes gridDrift {
    0%   { transform: translate(0,0); }
    100% { transform: translate(60px,60px); }
  }
  .pc-hero__glow {
    position: absolute; z-index: 0;
    border-radius: 50%;
    filter: blur(120px);
    pointer-events: none;
  }
  .pc-hero__glow--1 {
    width: 600px; height: 600px;
    background: radial-gradient(circle, rgba(0,229,192,.18) 0%, transparent 70%);
    top: -200px; right: -100px;
    animation: glowPulse 8s ease-in-out infinite;
  }
  .pc-hero__glow--2 {
    width: 400px; height: 400px;
    background: radial-gradient(circle, rgba(123,97,255,.14) 0%, transparent 70%);
    bottom: 0; left: -100px;
    animation: glowPulse 10s ease-in-out infinite reverse;
  }
  @keyframes glowPulse {
    0%, 100% { opacity: .7; transform: scale(1); }
    50%       { opacity: 1; transform: scale(1.08); }
  }
  .pc-hero__eyebrow {
    font-family: var(--font-mono);
    font-size: .75rem;
    letter-spacing: .2em;
    color: var(--accent);
    text-transform: uppercase;
    position: relative; z-index: 1;
    margin-bottom: 1.25rem;
    display: flex; align-items: center; gap: .75rem;
  }
  .pc-hero__eyebrow::before {
    content: '';
    display: inline-block;
    width: 2.5rem; height: 1px;
    background: var(--accent);
  }
  .pc-hero__title {
    font-family: var(--font-head);
    font-size: clamp(3.5rem, 10vw, 8rem);
    font-weight: 800;
    line-height: .92;
    position: relative; z-index: 1;
    letter-spacing: -.03em;
    color: var(--light);
  }
  .pc-hero__title em {
    font-style: normal;
    -webkit-text-stroke: 1.5px var(--accent);
    color: transparent;
  }
  .pc-hero__sub {
    font-family: var(--font-body);
    font-size: clamp(.95rem, 2vw, 1.2rem);
    color: var(--muted);
    max-width: 540px;
    margin-top: 1.5rem;
    position: relative; z-index: 1;
    line-height: 1.75;
  }
  .pc-hero__scroll {
    position: relative; z-index: 1;
    margin-top: 3rem;
    display: flex; align-items: center; gap: 1rem;
    font-family: var(--font-mono); font-size: .7rem;
    letter-spacing: .15em; text-transform: uppercase;
    color: var(--muted);
  }
  .pc-hero__scroll-line {
    width: 4rem; height: 1px;
    background: linear-gradient(90deg, var(--accent), transparent);
    animation: scrollLine 2s ease-in-out infinite;
  }
  @keyframes scrollLine {
    0%, 100% { width: 4rem; opacity: 1; }
    50%       { width: 7rem; opacity: .6; }
  }
  .pc-hero__tag {
    position: absolute; top: clamp(1.5rem, 4vw, 3rem); right: clamp(1.5rem, 4vw, 3rem);
    z-index: 1;
    font-family: var(--font-mono); font-size: .7rem;
    letter-spacing: .12em;
    color: var(--muted);
    border: 1px solid var(--line);
    padding: .5rem 1rem;
    border-radius: 999px;
    backdrop-filter: blur(10px);
    background: rgba(10,10,15,.5);
  }

  /* ─── Section wrapper ─── */
  .pc-section {
    padding: clamp(4rem, 10vw, 8rem) clamp(1.5rem, 6vw, 5rem);
    position: relative;
  }
  .pc-section--alt { background: var(--ink2); }

  /* ─── Section label ─── */
  .pc-label {
    font-family: var(--font-mono);
    font-size: .7rem;
    letter-spacing: .2em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 1.25rem;
    display: flex; align-items: center; gap: .75rem;
  }
  .pc-label::before {
    content: '';
    display: inline-block;
    width: 1.5rem; height: 1px;
    background: var(--accent);
  }

  /* ─── MISSION / NARRATIVE ─── */
  .pc-narrative {
    max-width: 1200px;
    margin: 0 auto;
  }
  .pc-narrative__headline {
    font-family: var(--font-head);
    font-size: clamp(2rem, 5vw, 3.5rem);
    font-weight: 700;
    line-height: 1.1;
    color: var(--light);
    margin-bottom: 3rem;
    letter-spacing: -.02em;
  }
  .pc-narrative__headline span { color: var(--accent); }
  .pc-narrative__grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(min(100%, 340px), 1fr));
    gap: 2px;
  }
  .pc-narrative__block {
    background: var(--card);
    padding: 2.5rem;
    border-top: 2px solid transparent;
    transition: border-color .3s, background .3s;
    position: relative;
    overflow: hidden;
  }
  .pc-narrative__block:hover { border-color: var(--accent); background: #13131f; }
  .pc-narrative__block::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    opacity: 0; transition: opacity .3s;
  }
  .pc-narrative__block:hover::before { opacity: 1; }
  .pc-narrative__icon {
    font-size: 2rem; margin-bottom: 1.25rem; display: block;
  }
  .pc-narrative__block-title {
    font-family: var(--font-head);
    font-size: 1.25rem; font-weight: 700;
    color: var(--light);
    margin-bottom: .75rem;
    letter-spacing: -.01em;
  }
  .pc-narrative__block p {
    font-size: .95rem;
    color: var(--muted);
    line-height: 1.8;
  }
  .pc-narrative__quote {
    margin-top: 4rem;
    border-left: 3px solid var(--accent);
    padding: 1.5rem 2rem;
    background: rgba(0,229,192,.04);
    font-family: var(--font-head);
    font-size: clamp(1.1rem, 2.5vw, 1.5rem);
    font-weight: 600;
    color: var(--light);
    letter-spacing: -.01em;
    line-height: 1.5;
  }
  .pc-narrative__quote cite {
    display: block;
    margin-top: .75rem;
    font-family: var(--font-mono);
    font-size: .75rem;
    letter-spacing: .1em;
    color: var(--muted);
    font-style: normal;
  }

  /* ─── STATS STRIP ─── */
  .pc-stats {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(min(100%, 180px), 1fr));
    border-top: 1px solid var(--line);
    border-bottom: 1px solid var(--line);
    background: var(--ink);
  }
  .pc-stat {
    padding: 2.5rem 2rem;
    border-right: 1px solid var(--line);
    position: relative;
    overflow: hidden;
  }
  .pc-stat:last-child { border-right: none; }
  .pc-stat__num {
    font-family: var(--font-head);
    font-size: clamp(2.5rem, 5vw, 3.5rem);
    font-weight: 800;
    color: var(--light);
    line-height: 1;
    letter-spacing: -.04em;
  }
  .pc-stat__num span { color: var(--accent); }
  .pc-stat__label {
    font-family: var(--font-mono);
    font-size: .7rem;
    letter-spacing: .15em;
    text-transform: uppercase;
    color: var(--muted);
    margin-top: .5rem;
  }
  .pc-stat__glow {
    position: absolute; bottom: -30px; right: -30px;
    width: 100px; height: 100px;
    background: radial-gradient(circle, rgba(0,229,192,.08) 0%, transparent 70%);
    border-radius: 50%;
  }

  /* ─── TEAM GRID ─── */
  .pc-team-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(min(100%, 260px), 1fr));
    gap: 2px;
    max-width: 1400px;
    margin: 0 auto;
  }
  .pc-card {
    background: var(--card);
    position: relative;
    overflow: hidden;
    cursor: default;
    aspect-ratio: 3/4;
    display: flex; flex-direction: column; justify-content: flex-end;
  }
  .pc-card__img {
    position: absolute; inset: 0;
    width: 100%; height: 100%;
    object-fit: cover;
    object-position: top center;
    filter: grayscale(30%) contrast(1.05);
    transition: filter .5s, transform .6s;
    display: block;
  }
  .pc-card:hover .pc-card__img {
    filter: grayscale(0%) contrast(1.1);
    transform: scale(1.04);
  }
  .pc-card__overlay {
    position: absolute; inset: 0;
    background: linear-gradient(
      to top,
      rgba(10,10,15,.97) 0%,
      rgba(10,10,15,.6) 40%,
      rgba(10,10,15,.1) 70%,
      transparent 100%
    );
    transition: background .4s;
  }
  .pc-card:hover .pc-card__overlay {
    background: linear-gradient(
      to top,
      rgba(10,10,15,.99) 0%,
      rgba(10,10,15,.8) 50%,
      rgba(10,10,15,.3) 80%,
      transparent 100%
    );
  }
  .pc-card__accent-line {
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform .4s cubic-bezier(.16,1,.3,1);
  }
  .pc-card:hover .pc-card__accent-line { transform: scaleX(1); }
  .pc-card__body {
    position: relative; z-index: 1;
    padding: 1.5rem;
  }
  .pc-card__role {
    font-family: var(--font-mono);
    font-size: .65rem;
    letter-spacing: .18em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: .4rem;
  }
  .pc-card__name {
    font-family: var(--font-head);
    font-size: 1.2rem;
    font-weight: 700;
    color: var(--light);
    letter-spacing: -.01em;
    line-height: 1.2;
  }
  .pc-card__extra {
    margin-top: .6rem;
    height: 0; overflow: hidden;
    transition: height .4s cubic-bezier(.16,1,.3,1);
  }
  .pc-card:hover .pc-card__extra { height: 2rem; }
  .pc-card__num {
    position: absolute; top: 1rem; left: 1rem;
    font-family: var(--font-mono); font-size: .65rem;
    letter-spacing: .1em;
    color: rgba(200,200,216,.3);
    z-index: 1;
  }
  /* Leadership highlight — first 2 cards span wider on big screens */
  @media (min-width: 900px) {
    .pc-card--lead { grid-column: span 2; aspect-ratio: 16/9; }
    .pc-card--lead .pc-card__name { font-size: 1.8rem; }
    .pc-card--lead .pc-card__role { font-size: .75rem; }
    .pc-card--lead .pc-card__body { padding: 2.5rem; }
    .pc-card--lead:hover .pc-card__extra { height: 2.5rem; }
  }

  /* ─── ABOUT STRIPS ─── */
  .pc-about {
    max-width: 1200px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: clamp(2rem, 5vw, 5rem);
    align-items: center;
  }
  @media (max-width: 700px) { .pc-about { grid-template-columns: 1fr; } }
  .pc-about__heading {
    font-family: var(--font-head);
    font-size: clamp(1.75rem, 4vw, 2.75rem);
    font-weight: 700;
    color: var(--light);
    letter-spacing: -.02em;
    line-height: 1.15;
    margin-bottom: 1.25rem;
  }
  .pc-about__heading span { color: var(--accent); }
  .pc-about__text {
    font-size: 1rem;
    color: var(--muted);
    line-height: 1.9;
    margin-bottom: 1rem;
  }
  .pc-about__list {
    list-style: none;
    margin-top: 1.5rem;
  }
  .pc-about__list li {
    display: flex; align-items: flex-start; gap: .75rem;
    padding: .6rem 0;
    border-bottom: 1px solid var(--line);
    font-size: .9rem;
    color: var(--text);
  }
  .pc-about__list li::before {
    content: '→';
    color: var(--accent);
    font-family: var(--font-mono);
    flex-shrink: 0;
    margin-top: .1rem;
  }
  .pc-callout-box {
    background: var(--card);
    border: 1px solid var(--line);
    padding: 2.5rem;
    position: relative;
    overflow: hidden;
  }
  .pc-callout-box::after {
    content: '';
    position: absolute; top: 0; right: 0;
    width: 120px; height: 120px;
    background: radial-gradient(circle, rgba(0,229,192,.1) 0%, transparent 70%);
  }
  .pc-callout-box__eyebrow {
    font-family: var(--font-mono);
    font-size: .65rem; letter-spacing: .2em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 1rem;
  }
  .pc-callout-box__title {
    font-family: var(--font-head);
    font-size: 1.5rem; font-weight: 700;
    color: var(--light);
    margin-bottom: 1rem;
    letter-spacing: -.01em;
  }
  .pc-callout-box__text {
    font-size: .95rem; color: var(--muted); line-height: 1.8;
  }
  .pc-callout-box__cta {
    display: inline-flex; align-items: center; gap: .5rem;
    margin-top: 1.5rem;
    font-family: var(--font-mono); font-size: .75rem;
    letter-spacing: .1em; text-transform: uppercase;
    color: var(--accent);
    text-decoration: none;
    border-bottom: 1px solid var(--accent);
    padding-bottom: 2px;
    transition: gap .3s;
  }
  .pc-callout-box__cta:hover { gap: .9rem; }

  /* ─── CTA BAND ─── */
  .pc-cta {
    padding: clamp(4rem, 8vw, 7rem) clamp(1.5rem, 6vw, 5rem);
    background: var(--card);
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .pc-cta::before {
    content: '';
    position: absolute; inset: 0;
    background: repeating-linear-gradient(
      -45deg,
      rgba(0,229,192,.02) 0,
      rgba(0,229,192,.02) 1px,
      transparent 1px,
      transparent 20px
    );
  }
  .pc-cta__heading {
    font-family: var(--font-head);
    font-size: clamp(2rem, 5vw, 3.5rem);
    font-weight: 800;
    color: var(--light);
    letter-spacing: -.03em;
    line-height: 1.1;
    margin-bottom: 1rem;
    position: relative; z-index: 1;
  }
  .pc-cta__sub {
    font-size: 1.05rem; color: var(--muted);
    max-width: 480px; margin: 0 auto 2.5rem;
    line-height: 1.75;
    position: relative; z-index: 1;
  }
  .pc-btn {
    display: inline-flex; align-items: center; gap: .6rem;
    background: var(--accent);
    color: var(--ink);
    font-family: var(--font-head);
    font-size: .9rem; font-weight: 700;
    letter-spacing: .04em;
    padding: .9rem 2rem;
    border-radius: var(--radius);
    text-decoration: none;
    transition: background .25s, transform .25s, box-shadow .25s;
    position: relative; z-index: 1;
  }
  .pc-btn:hover {
    background: var(--light);
    transform: translateY(-2px);
    box-shadow: 0 8px 32px rgba(0,229,192,.25);
  }
  .pc-btn--ghost {
    background: transparent;
    color: var(--accent);
    border: 1px solid var(--accent);
    margin-left: 1rem;
  }
  .pc-btn--ghost:hover {
    background: rgba(0,229,192,.08);
    color: var(--accent);
    box-shadow: 0 4px 20px rgba(0,229,192,.12);
  }

  /* ─── FOOTER ─── */
  .pc-footer {
    padding: 2.5rem clamp(1.5rem, 6vw, 5rem);
    border-top: 1px solid var(--line);
    display: flex; justify-content: space-between; align-items: center;
    flex-wrap: wrap; gap: 1rem;
    font-family: var(--font-mono); font-size: .7rem;
    letter-spacing: .1em; color: var(--muted);
  }
  .pc-footer a { color: var(--muted); text-decoration: none; }
  .pc-footer a:hover { color: var(--accent); }

  /* ─── Divider ─── */
  .pc-divider {
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--line), transparent);
    margin: 0;
  }

  /* ─── Fade-in animation ─── */
  .pc-fade {
    opacity: 0;
    transform: translateY(24px);
    transition: opacity .7s cubic-bezier(.16,1,.3,1), transform .7s cubic-bezier(.16,1,.3,1);
  }
  .pc-fade.visible { opacity: 1; transform: none; }

  /* Stagger children */
  .pc-fade-stagger > * {
    opacity: 0; transform: translateY(20px);
    transition: opacity .6s cubic-bezier(.16,1,.3,1), transform .6s cubic-bezier(.16,1,.3,1);
  }
  .pc-fade-stagger.visible > * { opacity: 1; transform: none; }
  .pc-fade-stagger.visible > *:nth-child(1)  { transition-delay: 0s; }
  .pc-fade-stagger.visible > *:nth-child(2)  { transition-delay: .08s; }
  .pc-fade-stagger.visible > *:nth-child(3)  { transition-delay: .16s; }
  .pc-fade-stagger.visible > *:nth-child(4)  { transition-delay: .24s; }
  .pc-fade-stagger.visible > *:nth-child(5)  { transition-delay: .32s; }
  .pc-fade-stagger.visible > *:nth-child(6)  { transition-delay: .40s; }
  .pc-fade-stagger.visible > *:nth-child(7)  { transition-delay: .48s; }
  .pc-fade-stagger.visible > *:nth-child(8)  { transition-delay: .56s; }
  .pc-fade-stagger.visible > *:nth-child(9)  { transition-delay: .64s; }
  .pc-fade-stagger.visible > *:nth-child(10) { transition-delay: .72s; }
  .pc-fade-stagger.visible > *:nth-child(11) { transition-delay: .80s; }
  .pc-fade-stagger.visible > *:nth-child(12) { transition-delay: .88s; }

  /* Mobile tweaks */
  @media (max-width: 600px) {
    .pc-btn--ghost { margin-left: 0; margin-top: .75rem; }
    .pc-cta .pc-btn { display: flex; width: 100%; justify-content: center; max-width: 320px; margin: .4rem auto; }
    .pc-stat { padding: 1.75rem 1.25rem; }
    .pc-narrative__block { padding: 1.75rem; }
  }
</style>

<div id="pc-team-page">

  <!-- ═══ HERO ═══ -->
  <section class="pc-hero">
    <div class="pc-hero__grid-bg"></div>
    <div class="pc-hero__glow pc-hero__glow--1"></div>
    <div class="pc-hero__glow pc-hero__glow--2"></div>
    <div class="pc-hero__tag">Est. 2022 · Islamabad, PK</div>
    <div class="pc-hero__eyebrow">PakCrypt · Our People</div>
    <h1 class="pc-hero__title">
      The<br><em>Minds</em><br>Behind<br>the Mission
    </h1>
    <p class="pc-hero__sub">
      A multidisciplinary team of cryptographers, engineers, researchers, and educators — united by a single conviction: that mathematical rigour and cryptographic literacy are Pakistan's most strategic intellectual assets.
    </p>
    <div class="pc-hero__scroll">
      <div class="pc-hero__scroll-line"></div>
      Scroll to explore
    </div>
  </section>

  <!-- ═══ STATS STRIP ═══ -->
  <div class="pc-stats pc-fade-stagger">
    <div class="pc-stat">
      <div class="pc-stat__num">5<span>th</span></div>
      <div class="pc-stat__label">Annual Edition</div>
      <div class="pc-stat__glow"></div>
    </div>
    <div class="pc-stat">
      <div class="pc-stat__num">1<span>K+</span></div>
      <div class="pc-stat__label">Expected Participants</div>
      <div class="pc-stat__glow"></div>
    </div>
    <div class="pc-stat">
      <div class="pc-stat__num">13<span>+</span></div>
      <div class="pc-stat__label">Intl Experts (2025)</div>
      <div class="pc-stat__glow"></div>
    </div>
    <div class="pc-stat">
      <div class="pc-stat__num">5<span>M</span></div>
      <div class="pc-stat__label">PKR Total Prizes</div>
      <div class="pc-stat__glow"></div>
    </div>
    <div class="pc-stat">
      <div class="pc-stat__num">2</div>
      <div class="pc-stat__label">Competition Tracks</div>
      <div class="pc-stat__glow"></div>
    </div>
  </div>

  <div class="pc-divider"></div>

  <!-- ═══ NARRATIVE / MISSION ═══ -->
  <section class="pc-section pc-section--alt">
    <div class="pc-narrative">
      <p class="pc-label">Why We Exist</p>
      <h2 class="pc-narrative__headline">
        Mathematics is not a subject.<br>
        It is the <span>language of trust</span>.
      </h2>

      <div class="pc-narrative__grid pc-fade-stagger">

        <div class="pc-narrative__block">
          <span class="pc-narrative__icon">∮</span>
          <div class="pc-narrative__block-title">The Mathematical Foundation</div>
          <p>Every encrypted message, every digital signature, every secure transaction rests on theorems proved centuries before computers existed. Number theory, abstract algebra, elliptic curves — these are not academic abstractions. They are load-bearing structures of the digital world. Without a deep appreciation of this mathematics, cryptography becomes a black box no engineer can reason about when it fails.</p>
        </div>

        <div class="pc-narrative__block">
          <span class="pc-narrative__icon">🔐</span>
          <div class="pc-narrative__block-title">Cryptography as Civilisational Infrastructure</div>
          <p>Banking, governance, healthcare, defence, communications — every critical system today depends on cryptographic primitives for its integrity and confidentiality. A nation that cannot independently reason about, implement, audit, and innovate in cryptography is not sovereign in any meaningful technological sense. It depends on others to keep its secrets — and to decide when to reveal them.</p>
        </div>

        <div class="pc-narrative__block">
          <span class="pc-narrative__icon">🌐</span>
          <div class="pc-narrative__block-title">The Post-Quantum Imperative</div>
          <p>Quantum computers capable of breaking RSA and ECC are approaching. NIST has already standardised post-quantum algorithms. Organisations that have not begun their cryptographic migration are already behind. Pakistan cannot afford to be a late adopter in this transition — the cost is measured not in dollars, but in compromised state secrets, financial systems, and national communications.</p>
        </div>

        <div class="pc-narrative__block">
          <span class="pc-narrative__icon">⚡</span>
          <div class="pc-narrative__block-title">Building Homegrown Expertise</div>
          <p>PakCrypt was founded on the conviction that world-class cryptographic talent can be cultivated in Pakistan. Through competitions that demand real mathematical depth, symposiums that connect local talent with IACR-affiliated researchers, and thesis support programs that fund original research, we are building a pipeline — not importing one. Every finalist who walks into our on-site event is proof that the expertise exists here.</p>
        </div>

        <div class="pc-narrative__block">
          <span class="pc-narrative__icon">🎓</span>
          <div class="pc-narrative__block-title">Education Without Borders</div>
          <p>The IACR Cryptography Winter School we co-host annually brings the world's leading cryptographers to Islamabad. This is not a lecture series — it is hands-on mentorship from the people who design the protocols the world depends on. For a Pakistani student or researcher who cannot afford a conference in Europe or the United States, this is transformative access that changes career trajectories.</p>
        </div>

        <div class="pc-narrative__block">
          <span class="pc-narrative__icon">🤝</span>
          <div class="pc-narrative__block-title">Community, Not Just Competition</div>
          <p>PakCrypt is not a trophy-hunting exercise. It is a community-building effort. Our non-profit structure means every rupee of prize money and operational budget goes toward the mission. Our networking dinners, expert Q&A sessions, and open symposiums are deliberately designed to collapse the hierarchy between established professionals and emerging talent — because breakthroughs come from unexpected conversations.</p>
        </div>

      </div>

      <blockquote class="pc-narrative__quote pc-fade">
        "The security of the world's information infrastructure is ultimately a mathematics problem. Nations that invest in mathematical education today will write the cryptographic standards of tomorrow."
        <cite>— PakCrypt founding principle, 2022</cite>
      </blockquote>
    </div>
  </section>

  <div class="pc-divider"></div>

  <!-- ═══ TEAM ═══ -->
  <section class="pc-section">
    <p class="pc-label">The People</p>
    <h2 class="pc-narrative__headline" style="margin-bottom: 3rem;">
      Meet the <span>Team</span>
    </h2>

    <div class="pc-team-grid pc-fade-stagger">

      <!-- 1 — Lead: CIO -->
      <div class="pc-card pc-card--lead">
        <img class="pc-card__img"
          src="{{ '/assets/images/tm/2.jpg' | relative_url }}"
          alt="Naveed A. Aun" loading="lazy">
        <div class="pc-card__overlay"></div>
        <div class="pc-card__accent-line"></div>
        <span class="pc-card__num">02</span>
        <div class="pc-card__body">
          <div class="pc-card__role">Chief Information Officer</div>
          <div class="pc-card__name">Naveed A. Aun</div>
          <div class="pc-card__extra">
            <div style="font-family:var(--font-mono);font-size:.65rem;letter-spacing:.1em;color:var(--muted);margin-top:.5rem;">CIO · PakCrypt</div>
          </div>
        </div>
      </div>

      <!-- 3 — Lead: CTO -->
      <div class="pc-card pc-card--lead">
        <img class="pc-card__img"
          src="{{ '/assets/images/tm/3.jpg' | relative_url }}"
          alt="Zubair Ansari" loading="lazy">
        <div class="pc-card__overlay"></div>
        <div class="pc-card__accent-line"></div>
        <span class="pc-card__num">03</span>
        <div class="pc-card__body">
          <div class="pc-card__role">Chief Technology Officer</div>
          <div class="pc-card__name">Zubair Ansari</div>
          <div class="pc-card__extra">
            <div style="font-family:var(--font-mono);font-size:.65rem;letter-spacing:.1em;color:var(--muted);margin-top:.5rem;">CTO · PakCrypt</div>
          </div>
        </div>
      </div>

      <!-- 1 — Marketing Head -->
      <div class="pc-card">
        <img class="pc-card__img"
          src="{{ '/assets/images/tm/1.jpg' | relative_url }}"
          alt="Saeed Ullah" loading="lazy">
        <div class="pc-card__overlay"></div>
        <div class="pc-card__accent-line"></div>
        <span class="pc-card__num">01</span>
        <div class="pc-card__body">
          <div class="pc-card__role">Head of Marketing</div>
          <div class="pc-card__name">Saeed Ullah</div>
        </div>
      </div>

      <!-- 4 — Research -->
      <div class="pc-card">
        <img class="pc-card__img"
          src="{{ '/assets/images/tm/4.jpg' | relative_url }}"
          alt="Sara Malik" loading="lazy">
        <div class="pc-card__overlay"></div>
        <div class="pc-card__accent-line"></div>
        <span class="pc-card__num">04</span>
        <div class="pc-card__body">
          <div class="pc-card__role">Head of Research</div>
          <div class="pc-card__name">Sara Malik</div>
        </div>
      </div>

      <!-- 8 — Innovations -->
      <div class="pc-card">
        <img class="pc-card__img"
          src="{{ '/assets/images/tm/8.jpg' | relative_url }}"
          alt="Ji Won" loading="lazy">
        <div class="pc-card__overlay"></div>
        <div class="pc-card__accent-line"></div>
        <span class="pc-card__num">08</span>
        <div class="pc-card__body">
          <div class="pc-card__role">Head of Innovations</div>
          <div class="pc-card__name">Ji Won</div>
        </div>
      </div>

      <!-- 9 — Researcher Fellow -->
      <div class="pc-card">
        <img class="pc-card__img"
          src="{{ '/assets/images/tm/9.jpg' | relative_url }}"
          alt="Zeynep Akata" loading="lazy">
        <div class="pc-card__overlay"></div>
        <div class="pc-card__accent-line"></div>
        <span class="pc-card__num">09</span>
        <div class="pc-card__body">
          <div class="pc-card__role">Research Fellow</div>
          <div class="pc-card__name">Zeynep Akata</div>
        </div>
      </div>

      <!-- 10 — Researcher Fellow -->
      <div class="pc-card">
        <img class="pc-card__img"
          src="{{ '/assets/images/tm/10.jpg' | relative_url }}"
          alt="David Chen" loading="lazy">
        <div class="pc-card__overlay"></div>
        <div class="pc-card__accent-line"></div>
        <span class="pc-card__num">10</span>
        <div class="pc-card__body">
          <div class="pc-card__role">Research Fellow</div>
          <div class="pc-card__name">David Chen</div>
        </div>
      </div>

      <!-- 11 — Research Fellow -->
      <div class="pc-card">
        <img class="pc-card__img"
          src="{{ '/assets/images/tm/11.jpg' | relative_url }}"
          alt="Fatima Khan" loading="lazy">
        <div class="pc-card__overlay"></div>
        <div class="pc-card__accent-line"></div>
        <span class="pc-card__num">11</span>
        <div class="pc-card__body">
          <div class="pc-card__role">Research Fellow</div>
          <div class="pc-card__name">Fatima Khan</div>
        </div>
      </div>

      <!-- 5 — Advisor -->
      <div class="pc-card">
        <img class="pc-card__img"
          src="{{ '/assets/images/tm/5.jpg' | relative_url }}"
          alt="Noman A. Riaz" loading="lazy">
        <div class="pc-card__overlay"></div>
        <div class="pc-card__accent-line"></div>
        <span class="pc-card__num">05</span>
        <div class="pc-card__body">
          <div class="pc-card__role">Advisor</div>
          <div class="pc-card__name">Noman A. Riaz</div>
        </div>
      </div>

      <!-- 6 — Senior Advisor -->
      <div class="pc-card">
        <img class="pc-card__img"
          src="{{ '/assets/images/tm/6.jpg' | relative_url }}"
          alt="Christina Tunder" loading="lazy">
        <div class="pc-card__overlay"></div>
        <div class="pc-card__accent-line"></div>
        <span class="pc-card__num">06</span>
        <div class="pc-card__body">
          <div class="pc-card__role">Senior Advisor</div>
          <div class="pc-card__name">Christina Tunder</div>
        </div>
      </div>

      <!-- 7 — Advisor -->
      <div class="pc-card">
        <img class="pc-card__img"
          src="{{ '/assets/images/tm/7.jpg' | relative_url }}"
          alt="Nadia Waheed" loading="lazy">
        <div class="pc-card__overlay"></div>
        <div class="pc-card__accent-line"></div>
        <span class="pc-card__num">07</span>
        <div class="pc-card__body">
          <div class="pc-card__role">Advisor</div>
          <div class="pc-card__name">Nadia Waheed</div>
        </div>
      </div>

      <!-- 12 — Advisor -->
      <div class="pc-card">
        <img class="pc-card__img"
          src="{{ '/assets/images/tm/12.jpg' | relative_url }}"
          alt="Grieg Greger" loading="lazy">
        <div class="pc-card__overlay"></div>
        <div class="pc-card__accent-line"></div>
        <span class="pc-card__num">12</span>
        <div class="pc-card__body">
          <div class="pc-card__role">Advisor</div>
          <div class="pc-card__name">Grieg Greger</div>
        </div>
      </div>

    </div><!-- /team-grid -->
  </section>

  <div class="pc-divider"></div>

  <!-- ═══ ABOUT STRIP ═══ -->
  <section class="pc-section pc-section--alt">
    <div class="pc-about">
      <div class="pc-fade">
        <p class="pc-label">What We Do</p>
        <h2 class="pc-about__heading">
          From competition<br>to <span>community</span>
        </h2>
        <p class="pc-about__text">
          PakCrypt is a non-profit organisation based in Islamabad. Since 2022, we have run Pakistan's most rigorous annual cryptography competition, drawing participants from universities and industry across the country.
        </p>
        <p class="pc-about__text">
          Our scope has expanded every year — from a single competition to a full international symposium co-hosted with IACR, a thesis support programme funding original research, and a growing library of technical articles and whitepapers.
        </p>
        <ul class="pc-about__list">
          <li>Annual international cryptography competition (Professional &amp; Amateur tracks)</li>
          <li>IACR Cryptography Winter School, Islamabad</li>
          <li>International Cyber Security Symposium</li>
          <li>Thesis funding programme for undergraduate researchers (Rs. 100K–200K)</li>
          <li>Technical publications, whitepapers, and Crypt Pulse news</li>
        </ul>
      </div>
      <div class="pc-callout-box pc-fade">
        <div class="pc-callout-box__eyebrow">PakCrypt 2026</div>
        <div class="pc-callout-box__title">Register for the 5th Annual Edition</div>
        <div class="pc-callout-box__text">
          NCCS, Air University, Islamabad · November 2026 (tentative)<br><br>
          Pre-Qualifying Round opens September 2026. Two tracks: <strong style="color:var(--light);">Professional</strong> (open to all) and <strong style="color:var(--light);">Amateur</strong> (under 20). Total prize pool: <strong style="color:var(--accent);">Rs. 5.0 million</strong>. Finalists receive full sponsorship — travel, accommodation, meals, and free IACR Winter School registration.
        </div>
        <a href="https://forms.gle/miKnbJv5VrTPwiAb8" class="pc-callout-box__cta" target="_blank" rel="noopener">
          Register Now →
        </a>
      </div>
    </div>
  </section>

  <div class="pc-divider"></div>

  <!-- ═══ CTA ═══ -->
  <section class="pc-cta">
    <h2 class="pc-cta__heading">
      Ready to prove<br>your cryptographic mettle?
    </h2>
    <p class="pc-cta__sub">
      Join Pakistan's most rigorous cryptography challenge. Pre-qualifying opens September 2026 — open to all.
    </p>
    <div>
      <a href="https://forms.gle/miKnbJv5VrTPwiAb8" class="pc-btn" target="_blank" rel="noopener">
        Register for PakCrypt 2026 →
      </a>
      <a href="https://pakcrypt.org/assets/doc/pc26samv1.pdf" class="pc-btn pc-btn--ghost" target="_blank" rel="noopener">
        Sample Problems (PDF)
      </a>
    </div>
  </section>

  <!-- ═══ FOOTER ═══ -->
  <footer class="pc-footer">
    <span>© 2026 PakCrypt NPO, Islamabad, Pakistan</span>
    <span>
      <a href="https://pakcrypt.org" target="_blank" rel="noopener">pakcrypt.org</a>
      &nbsp;·&nbsp;
      <a href="https://twitter.com/PakCryptOrg" target="_blank" rel="noopener">@PakCryptOrg</a>
      &nbsp;·&nbsp;
      <a href="https://iacr.org" target="_blank" rel="noopener">iacr.org</a>
    </span>
  </footer>

</div><!-- /pc-team-page -->

<script>
(function () {
  // Intersection Observer for fade animations
  const observer = new IntersectionObserver(function (entries) {
    entries.forEach(function (entry) {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.08, rootMargin: '0px 0px -60px 0px' });

  document.querySelectorAll('.pc-fade, .pc-fade-stagger').forEach(function (el) {
    observer.observe(el);
  });

  // Parallax-lite on hero glows — only on desktop for perf
  if (window.matchMedia('(min-width: 768px)').matches) {
    var glow1 = document.querySelector('.pc-hero__glow--1');
    var glow2 = document.querySelector('.pc-hero__glow--2');
    document.addEventListener('mousemove', function (e) {
      var x = (e.clientX / window.innerWidth - .5) * 30;
      var y = (e.clientY / window.innerHeight - .5) * 30;
      if (glow1) glow1.style.transform = 'translate(' + x + 'px, ' + y + 'px)';
      if (glow2) glow2.style.transform = 'translate(' + (-x * .6) + 'px, ' + (-y * .6) + 'px)';
    });
  }
})();
</script>