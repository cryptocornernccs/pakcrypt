---
layout: page
title: "PakCrypt — Team"
description: "Meet the people behind Pakistan's premier cryptography community"
---

<style>
@import url('https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300&display=swap');

/* ═══════════════════════════════════════════════════════
   NUCLEAR THEME RESET — force dark everywhere the Jekyll
   theme tries to impose a light background or dark text
═══════════════════════════════════════════════════════ */

/* Force the page body to dark so no white bleeds through */
body { background-color: #0a0a0f !important; color: #c8c8d8 !important; }

/* Kill all Jekyll wrapper padding / max-width constraints */
.page-content,
.post-content,
.post,
article,
main,
.main,
.content,
#content,
.site-content,
.wrapper,
.container,
.inner { 
  max-width: 100% !important; 
  padding: 0 !important; 
  margin: 0 !important;
  background: transparent !important;
}

/* Any ancestor that might be white */
.page-content { background-color: #0a0a0f !important; }

/* Kill any default link colors the theme sets inside our scope */
#pc-team-page a { text-decoration: none; }

/* ═══════════════════════════════════════════════════════
   DESIGN TOKENS
═══════════════════════════════════════════════════════ */
:root {
  --ink:     #0a0a0f;
  --ink2:    #0f0f18;
  --card:    #111119;
  --card2:   #13131f;
  --line:    #1e1e2a;
  --muted:   #7a7a96;
  --text:    #c8c8d8;
  --light:   #eeeef5;
  --accent:  #00e5c0;
  --accent2: #7b61ff;
  --font-h:  'Syne', sans-serif;
  --font-m:  'DM Mono', monospace;
  --font-b:  'DM Sans', sans-serif;
}

/* ═══════════════════════════════════════════════════════
   PAGE WRAPPER — everything lives inside here
═══════════════════════════════════════════════════════ */
#pc-team-page {
  background-color: #0a0a0f !important;
  color: #c8c8d8 !important;
  font-family: var(--font-b) !important;
  font-weight: 300;
  line-height: 1.7;
  overflow-x: hidden;
  margin-left: calc(-50vw + 50%) !important;
  margin-right: calc(-50vw + 50%) !important;
  width: 100vw !important;
  position: relative;
}

/* Force every child's text to be our colours */
#pc-team-page * {
  box-sizing: border-box;
}

/* ═══════════════════════════════════════════════════════
   HERO
═══════════════════════════════════════════════════════ */
.pc-hero {
  background-color: #0a0a0f !important;
  color: #eeeef5 !important;
  position: relative;
  min-height: 100svh;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  padding: clamp(2rem, 8vw, 6rem);
  overflow: hidden;
}
.pc-hero__grid {
  position: absolute; inset: 0; z-index: 0;
  background-image:
    linear-gradient(rgba(0,229,192,.035) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,229,192,.035) 1px, transparent 1px);
  background-size: 60px 60px;
  animation: pcGridDrift 30s linear infinite;
}
@keyframes pcGridDrift {
  0%   { transform: translate(0,0); }
  100% { transform: translate(60px,60px); }
}
.pc-glow {
  position: absolute; border-radius: 50%;
  filter: blur(120px); pointer-events: none; z-index: 0;
}
.pc-glow--a {
  width: 600px; height: 600px;
  background: radial-gradient(circle, rgba(0,229,192,.16) 0%, transparent 70%);
  top: -200px; right: -100px;
  animation: pcGlowPulse 8s ease-in-out infinite;
}
.pc-glow--b {
  width: 400px; height: 400px;
  background: radial-gradient(circle, rgba(123,97,255,.13) 0%, transparent 70%);
  bottom: 0; left: -100px;
  animation: pcGlowPulse 10s ease-in-out infinite reverse;
}
@keyframes pcGlowPulse {
  0%,100% { opacity:.7; transform:scale(1); }
  50%      { opacity:1;  transform:scale(1.08); }
}
.pc-hero__tag {
  position: absolute;
  top: clamp(1.25rem, 4vw, 3rem);
  right: clamp(1.25rem, 4vw, 3rem);
  z-index: 2;
  font-family: var(--font-m);
  font-size: .7rem;
  letter-spacing: .12em;
  color: var(--muted) !important;
  border: 1px solid var(--line);
  padding: .45rem 1rem;
  border-radius: 999px;
  background: rgba(10,10,15,.7);
  backdrop-filter: blur(12px);
}
.pc-hero__eyebrow {
  position: relative; z-index: 1;
  font-family: var(--font-m);
  font-size: .72rem;
  letter-spacing: .22em;
  text-transform: uppercase;
  color: var(--accent) !important;
  margin-bottom: 1.25rem;
  display: flex; align-items: center; gap: .75rem;
}
.pc-hero__eyebrow::before {
  content: '';
  display: inline-block;
  width: 2.5rem; height: 1px;
  background: var(--accent);
  flex-shrink: 0;
}
.pc-hero__title {
  position: relative; z-index: 1;
  font-family: var(--font-h) !important;
  font-size: clamp(3rem, 10vw, 8rem);
  font-weight: 800;
  line-height: .92;
  letter-spacing: -.03em;
  color: #eeeef5 !important;
}
.pc-hero__title em {
  font-style: normal;
  -webkit-text-stroke: 1.5px var(--accent);
  color: transparent !important;
}
.pc-hero__sub {
  position: relative; z-index: 1;
  font-family: var(--font-b);
  font-size: clamp(.9rem, 2vw, 1.15rem);
  color: var(--muted) !important;
  max-width: 520px;
  margin-top: 1.5rem;
  line-height: 1.8;
}
.pc-hero__scroll {
  position: relative; z-index: 1;
  margin-top: 3rem;
  display: flex; align-items: center; gap: 1rem;
  font-family: var(--font-m);
  font-size: .68rem;
  letter-spacing: .15em;
  text-transform: uppercase;
  color: var(--muted) !important;
}
.pc-hero__scroll-bar {
  width: 4rem; height: 1px;
  background: linear-gradient(90deg, var(--accent), transparent);
  animation: pcScrollBar 2s ease-in-out infinite;
}
@keyframes pcScrollBar {
  0%,100% { width:4rem; opacity:1; }
  50%      { width:7rem; opacity:.5; }
}

/* ═══════════════════════════════════════════════════════
   STATS STRIP
═══════════════════════════════════════════════════════ */
.pc-stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%,170px),1fr));
  background-color: #0a0a0f !important;
  border-top: 1px solid var(--line);
  border-bottom: 1px solid var(--line);
}
.pc-stat {
  background-color: #0a0a0f !important;
  padding: 2.5rem 1.75rem;
  border-right: 1px solid var(--line);
  position: relative; overflow: hidden;
  transition: background .25s;
}
.pc-stat:last-child { border-right: none; }
.pc-stat:hover { background-color: #0f0f18 !important; }
.pc-stat__num {
  font-family: var(--font-h) !important;
  font-size: clamp(2.4rem, 5vw, 3.5rem);
  font-weight: 800;
  color: #eeeef5 !important;
  line-height: 1;
  letter-spacing: -.04em;
}
.pc-stat__num span { color: var(--accent) !important; }
.pc-stat__label {
  font-family: var(--font-m);
  font-size: .68rem;
  letter-spacing: .15em;
  text-transform: uppercase;
  color: var(--muted) !important;
  margin-top: .45rem;
}
.pc-stat__glow {
  position: absolute; bottom: -30px; right: -30px;
  width: 100px; height: 100px;
  background: radial-gradient(circle, rgba(0,229,192,.07) 0%, transparent 70%);
  border-radius: 50%;
}

/* ═══════════════════════════════════════════════════════
   SHARED SECTION WRAPPER
═══════════════════════════════════════════════════════ */
.pc-sec {
  padding: clamp(4rem, 10vw, 8rem) clamp(1.5rem, 6vw, 5rem);
  position: relative;
  background-color: #0a0a0f !important;
  color: #c8c8d8 !important;
}
.pc-sec--alt {
  background-color: #0f0f18 !important;
}
.pc-divider {
  height: 1px;
  background: var(--line);
  border: none;
  margin: 0;
}

/* Section label */
.pc-lbl {
  font-family: var(--font-m);
  font-size: .68rem;
  letter-spacing: .22em;
  text-transform: uppercase;
  color: var(--accent) !important;
  margin-bottom: 1.25rem;
  display: flex; align-items: center; gap: .75rem;
}
.pc-lbl::before {
  content: '';
  display: inline-block;
  width: 1.5rem; height: 1px;
  background: var(--accent);
  flex-shrink: 0;
}

/* ═══════════════════════════════════════════════════════
   NARRATIVE SECTION
═══════════════════════════════════════════════════════ */
.pc-narr { max-width: 1200px; margin: 0 auto; }
.pc-narr__head {
  font-family: var(--font-h) !important;
  font-size: clamp(1.9rem, 5vw, 3.5rem);
  font-weight: 700;
  line-height: 1.1;
  color: #eeeef5 !important;
  margin-bottom: 3rem;
  letter-spacing: -.02em;
}
.pc-narr__head span { color: var(--accent) !important; }

.pc-narr__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%,330px),1fr));
  gap: 2px;
}
.pc-nb {
  background-color: #111119 !important;
  color: #c8c8d8 !important;
  padding: 2.5rem;
  border-top: 2px solid transparent;
  position: relative; overflow: hidden;
  transition: border-color .3s, background-color .3s;
}
.pc-nb:hover {
  border-color: var(--accent);
  background-color: #13131f !important;
}
.pc-nb::before {
  content: '';
  position: absolute; top: 0; left: 0; right: 0; height: 2px;
  background: linear-gradient(90deg, var(--accent), var(--accent2));
  opacity: 0; transition: opacity .3s;
}
.pc-nb:hover::before { opacity: 1; }
.pc-nb__icon { font-size: 1.9rem; margin-bottom: 1.1rem; display: block; }
.pc-nb__title {
  font-family: var(--font-h) !important;
  font-size: 1.2rem; font-weight: 700;
  color: #eeeef5 !important;
  margin-bottom: .65rem;
  letter-spacing: -.01em;
}
.pc-nb p {
  font-size: .93rem;
  color: #7a7a96 !important;
  line-height: 1.85;
  margin: 0;
}

.pc-quote {
  margin-top: 4rem;
  border-left: 3px solid var(--accent);
  padding: 1.5rem 2rem;
  background: rgba(0,229,192,.04);
  font-family: var(--font-h) !important;
  font-size: clamp(1.05rem, 2.5vw, 1.45rem);
  font-weight: 600;
  color: #eeeef5 !important;
  letter-spacing: -.01em;
  line-height: 1.55;
}
.pc-quote cite {
  display: block;
  margin-top: .7rem;
  font-family: var(--font-m);
  font-size: .72rem;
  letter-spacing: .1em;
  color: #7a7a96 !important;
  font-style: normal;
}

/* ═══════════════════════════════════════════════════════
   TEAM GRID — cinematic portrait cards
═══════════════════════════════════════════════════════ */
.pc-team-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(min(100%,260px),1fr));
  gap: 2px;
  max-width: 1400px;
  margin: 0 auto;
}
.pc-card {
  background-color: #111119 !important;
  position: relative;
  overflow: hidden;
  aspect-ratio: 3/4;
  display: flex; flex-direction: column; justify-content: flex-end;
  cursor: default;
}
.pc-card--lead {
  grid-column: span 1;
}
@media (min-width: 860px) {
  .pc-card--lead { grid-column: span 2; aspect-ratio: 16/9; }
  .pc-card--lead .pc-card__name { font-size: 1.75rem !important; }
  .pc-card--lead .pc-card__body { padding: 2.25rem !important; }
}
.pc-card__img {
  position: absolute; inset: 0;
  width: 100%; height: 100%;
  object-fit: cover;
  object-position: top center;
  filter: grayscale(25%) contrast(1.05);
  transition: filter .5s, transform .6s cubic-bezier(.16,1,.3,1);
  display: block;
}
.pc-card:hover .pc-card__img {
  filter: grayscale(0%) contrast(1.08);
  transform: scale(1.04);
}
.pc-card__overlay {
  position: absolute; inset: 0;
  background: linear-gradient(
    to top,
    rgba(10,10,15,.97) 0%,
    rgba(10,10,15,.55) 38%,
    rgba(10,10,15,.08) 68%,
    transparent 100%
  );
  transition: background .4s;
}
.pc-card:hover .pc-card__overlay {
  background: linear-gradient(
    to top,
    rgba(10,10,15,.99) 0%,
    rgba(10,10,15,.78) 48%,
    rgba(10,10,15,.28) 78%,
    transparent 100%
  );
}
.pc-card__bar {
  position: absolute; bottom: 0; left: 0; right: 0; height: 2px;
  background: linear-gradient(90deg, var(--accent), var(--accent2));
  transform: scaleX(0);
  transform-origin: left;
  transition: transform .4s cubic-bezier(.16,1,.3,1);
}
.pc-card:hover .pc-card__bar { transform: scaleX(1); }
.pc-card__body {
  position: relative; z-index: 1;
  padding: 1.5rem;
}
.pc-card__role {
  font-family: var(--font-m) !important;
  font-size: .63rem;
  letter-spacing: .18em;
  text-transform: uppercase;
  color: var(--accent) !important;
  margin-bottom: .35rem;
}
.pc-card__name {
  font-family: var(--font-h) !important;
  font-size: 1.18rem;
  font-weight: 700;
  color: #eeeef5 !important;
  letter-spacing: -.01em;
  line-height: 1.2;
}
.pc-card__idx {
  position: absolute; top: 1rem; left: 1rem;
  font-family: var(--font-m);
  font-size: .63rem; letter-spacing: .1em;
  color: rgba(200,200,216,.25) !important;
  z-index: 1;
}

/* ═══════════════════════════════════════════════════════
   ABOUT STRIP
═══════════════════════════════════════════════════════ */
.pc-about {
  max-width: 1200px; margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: clamp(2rem, 5vw, 5rem);
  align-items: start;
}
@media (max-width: 700px) { .pc-about { grid-template-columns: 1fr; } }

.pc-about__head {
  font-family: var(--font-h) !important;
  font-size: clamp(1.7rem, 4vw, 2.7rem);
  font-weight: 700;
  color: #eeeef5 !important;
  letter-spacing: -.02em;
  line-height: 1.15;
  margin-bottom: 1.25rem;
}
.pc-about__head span { color: var(--accent) !important; }
.pc-about p {
  font-size: .97rem;
  color: #7a7a96 !important;
  line-height: 1.9;
  margin-bottom: .9rem;
}
.pc-about__list {
  list-style: none !important;
  margin: 1.5rem 0 0 0 !important;
  padding: 0 !important;
}
.pc-about__list li {
  display: flex; align-items: flex-start; gap: .75rem;
  padding: .55rem 0;
  border-bottom: 1px solid var(--line);
  font-size: .9rem;
  color: #c8c8d8 !important;
}
.pc-about__list li::before {
  content: '→';
  color: var(--accent) !important;
  font-family: var(--font-m);
  flex-shrink: 0; margin-top: .05rem;
}

.pc-box {
  background-color: #111119 !important;
  color: #c8c8d8 !important;
  border: 1px solid var(--line);
  padding: 2.5rem;
  position: relative; overflow: hidden;
}
.pc-box::after {
  content: '';
  position: absolute; top: 0; right: 0;
  width: 130px; height: 130px;
  background: radial-gradient(circle, rgba(0,229,192,.09) 0%, transparent 70%);
  pointer-events: none;
}
.pc-box__eye {
  font-family: var(--font-m);
  font-size: .65rem; letter-spacing: .2em;
  text-transform: uppercase;
  color: var(--accent) !important;
  margin-bottom: .9rem;
}
.pc-box__title {
  font-family: var(--font-h) !important;
  font-size: 1.45rem; font-weight: 700;
  color: #eeeef5 !important;
  margin-bottom: .9rem;
  letter-spacing: -.01em;
}
.pc-box__text {
  font-size: .93rem;
  color: #7a7a96 !important;
  line-height: 1.85;
}
.pc-box__text strong { color: #eeeef5 !important; }
.pc-box__cta {
  display: inline-flex; align-items: center; gap: .5rem;
  margin-top: 1.5rem;
  font-family: var(--font-m); font-size: .73rem;
  letter-spacing: .1em; text-transform: uppercase;
  color: var(--accent) !important;
  text-decoration: none !important;
  border-bottom: 1px solid var(--accent);
  padding-bottom: 2px;
  transition: gap .3s;
}
.pc-box__cta:hover { gap: .9rem; }

/* ═══════════════════════════════════════════════════════
   CTA BAND
═══════════════════════════════════════════════════════ */
.pc-cta {
  background-color: #111119 !important;
  color: #eeeef5 !important;
  padding: clamp(4rem, 8vw, 7rem) clamp(1.5rem, 6vw, 5rem);
  text-align: center;
  position: relative; overflow: hidden;
}
.pc-cta::before {
  content: '';
  position: absolute; inset: 0;
  background: repeating-linear-gradient(
    -45deg,
    rgba(0,229,192,.018) 0, rgba(0,229,192,.018) 1px,
    transparent 1px, transparent 20px
  );
  pointer-events: none;
}
.pc-cta__head {
  font-family: var(--font-h) !important;
  font-size: clamp(1.9rem, 5vw, 3.5rem);
  font-weight: 800;
  color: #eeeef5 !important;
  letter-spacing: -.03em;
  line-height: 1.1;
  margin-bottom: 1rem;
  position: relative; z-index: 1;
}
.pc-cta__sub {
  font-size: 1rem;
  color: #7a7a96 !important;
  max-width: 460px; margin: 0 auto 2.5rem;
  line-height: 1.8;
  position: relative; z-index: 1;
}
.pc-btn-row { position: relative; z-index: 1; display: flex; flex-wrap: wrap; gap: .75rem; justify-content: center; }
.pc-btn {
  display: inline-flex; align-items: center; gap: .55rem;
  background: var(--accent) !important;
  color: #0a0a0f !important;
  font-family: var(--font-h) !important;
  font-size: .88rem; font-weight: 700;
  letter-spacing: .03em;
  padding: .85rem 1.9rem;
  border-radius: 2px;
  text-decoration: none !important;
  transition: background .22s, transform .22s, box-shadow .22s;
}
.pc-btn:hover {
  background: #eeeef5 !important;
  color: #0a0a0f !important;
  transform: translateY(-2px);
  box-shadow: 0 8px 30px rgba(0,229,192,.22);
}
.pc-btn--ghost {
  background: transparent !important;
  color: var(--accent) !important;
  border: 1px solid var(--accent);
}
.pc-btn--ghost:hover {
  background: rgba(0,229,192,.08) !important;
  color: var(--accent) !important;
  transform: translateY(-2px);
  box-shadow: 0 4px 18px rgba(0,229,192,.1);
}

/* ═══════════════════════════════════════════════════════
   FOOTER
═══════════════════════════════════════════════════════ */
.pc-foot {
  background-color: #0a0a0f !important;
  color: #7a7a96 !important;
  padding: 2.25rem clamp(1.5rem, 6vw, 5rem);
  border-top: 1px solid var(--line);
  display: flex; justify-content: space-between;
  align-items: center; flex-wrap: wrap; gap: 1rem;
  font-family: var(--font-m); font-size: .68rem; letter-spacing: .1em;
}
.pc-foot a { color: #7a7a96 !important; text-decoration: none !important; transition: color .2s; }
.pc-foot a:hover { color: var(--accent) !important; }

/* ═══════════════════════════════════════════════════════
   SCROLL ANIMATIONS
═══════════════════════════════════════════════════════ */
.pc-fade {
  opacity: 0; transform: translateY(22px);
  transition: opacity .7s cubic-bezier(.16,1,.3,1), transform .7s cubic-bezier(.16,1,.3,1);
}
.pc-fade.pc-in { opacity: 1; transform: none; }

.pc-stagger > * {
  opacity: 0; transform: translateY(18px);
  transition: opacity .6s cubic-bezier(.16,1,.3,1), transform .6s cubic-bezier(.16,1,.3,1);
}
.pc-stagger.pc-in > * { opacity: 1; transform: none; }
.pc-stagger.pc-in > *:nth-child(1)  { transition-delay: 0s; }
.pc-stagger.pc-in > *:nth-child(2)  { transition-delay: .07s; }
.pc-stagger.pc-in > *:nth-child(3)  { transition-delay: .14s; }
.pc-stagger.pc-in > *:nth-child(4)  { transition-delay: .21s; }
.pc-stagger.pc-in > *:nth-child(5)  { transition-delay: .28s; }
.pc-stagger.pc-in > *:nth-child(6)  { transition-delay: .35s; }
.pc-stagger.pc-in > *:nth-child(7)  { transition-delay: .42s; }
.pc-stagger.pc-in > *:nth-child(8)  { transition-delay: .49s; }
.pc-stagger.pc-in > *:nth-child(9)  { transition-delay: .56s; }
.pc-stagger.pc-in > *:nth-child(10) { transition-delay: .63s; }
.pc-stagger.pc-in > *:nth-child(11) { transition-delay: .70s; }
.pc-stagger.pc-in > *:nth-child(12) { transition-delay: .77s; }

/* Mobile tweaks */
@media (max-width: 560px) {
  .pc-stat { padding: 1.5rem 1.1rem; }
  .pc-nb   { padding: 1.75rem; }
  .pc-btn  { width: 100%; max-width: 320px; justify-content: center; }
}
</style>

<div id="pc-team-page">

<!-- ══════════════ HERO ══════════════ -->
<section class="pc-hero">
  <div class="pc-hero__grid"></div>
  <div class="pc-glow pc-glow--a"></div>
  <div class="pc-glow pc-glow--b"></div>
  <div class="pc-hero__tag">Est. 2022 &middot; Islamabad, PK</div>

  <div class="pc-hero__eyebrow">PakCrypt &middot; Our Team</div>

  <h1 class="pc-hero__title">
    People &amp;<br><em>Purpose</em><br>Behind<br>PakCrypt
  </h1>

  <p class="pc-hero__sub">
    A multidisciplinary team of cryptographers, engineers, researchers, and educators — united by one conviction: that mathematical rigour and cryptographic literacy are Pakistan's most strategic intellectual assets.
  </p>

  <div class="pc-hero__scroll">
    <div class="pc-hero__scroll-bar"></div>
    Scroll to explore
  </div>
</section>

<!-- ══════════════ STATS ══════════════ -->
<div class="pc-stats pc-stagger">
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

<hr class="pc-divider">

<!-- ══════════════ MISSION / NARRATIVE ══════════════ -->
<section class="pc-sec pc-sec--alt">
  <div class="pc-narr">
    <p class="pc-lbl">Why We Exist</p>
    <h2 class="pc-narr__head">
      Mathematics is not a subject.<br>
      It is the <span>language of trust</span>.
    </h2>

    <div class="pc-narr__grid pc-stagger">

      <div class="pc-nb">
        <span class="pc-nb__icon">∮</span>
        <div class="pc-nb__title">The Mathematical Foundation</div>
        <p>Every encrypted message, every digital signature, every secure transaction rests on theorems proved centuries before computers existed. Number theory, abstract algebra, elliptic curves — these are not academic abstractions. They are the load-bearing structures of the digital world. Without a deep appreciation of this mathematics, cryptography becomes a black box that no engineer can reason about when it fails.</p>
      </div>

      <div class="pc-nb">
        <span class="pc-nb__icon">🔐</span>
        <div class="pc-nb__title">Cryptography as Civilisational Infrastructure</div>
        <p>Banking, governance, healthcare, defence, communications — every critical system today depends on cryptographic primitives for its integrity and confidentiality. A nation that cannot independently reason about, implement, audit, and innovate in cryptography is not sovereign in any meaningful technological sense. It depends on others to keep its secrets — and to decide when to reveal them.</p>
      </div>

      <div class="pc-nb">
        <span class="pc-nb__icon">⚛️</span>
        <div class="pc-nb__title">The Post-Quantum Imperative</div>
        <p>Quantum computers capable of breaking RSA and ECC are approaching. NIST has already standardised post-quantum algorithms. Organisations that have not begun their cryptographic migration are already behind. Pakistan cannot afford to be a late adopter in this transition — the cost is measured not in dollars, but in compromised state secrets, financial systems, and national communications.</p>
      </div>

      <div class="pc-nb">
        <span class="pc-nb__icon">⚡</span>
        <div class="pc-nb__title">Building Homegrown Expertise</div>
        <p>PakCrypt was founded on the conviction that world-class cryptographic talent can be cultivated in Pakistan. Through competitions that demand real mathematical depth, symposiums that connect local talent with IACR-affiliated researchers, and thesis support programmes that fund original research, we are building a pipeline — not importing one. Every finalist who steps on-site is proof the expertise already exists here.</p>
      </div>

      <div class="pc-nb">
        <span class="pc-nb__icon">🎓</span>
        <div class="pc-nb__title">Education Without Borders</div>
        <p>The IACR Cryptography Winter School we co-host annually brings the world's leading cryptographers to Islamabad. This is not a lecture series — it is hands-on mentorship from the people who design the protocols the world depends on. For a Pakistani student or researcher who cannot afford a conference in Europe or the United States, this is transformative access that changes career trajectories.</p>
      </div>

      <div class="pc-nb">
        <span class="pc-nb__icon">🤝</span>
        <div class="pc-nb__title">Community, Not Just Competition</div>
        <p>PakCrypt is not a trophy-hunting exercise. It is a community-building effort. Our non-profit structure means every rupee of prize money and operational budget goes toward the mission. Our networking dinners, expert Q&amp;A sessions, and open symposiums are deliberately designed to collapse the hierarchy between established professionals and emerging talent — because breakthroughs come from unexpected conversations.</p>
      </div>

    </div><!-- /grid -->

    <blockquote class="pc-quote pc-fade">
      "The security of the world's information infrastructure is ultimately a mathematics problem. Nations that invest in mathematical education today will write the cryptographic standards of tomorrow."
      <cite>— PakCrypt founding principle, 2022</cite>
    </blockquote>
  </div>
</section>

<hr class="pc-divider">

<!-- ══════════════ TEAM ══════════════ -->
<section class="pc-sec">
  <p class="pc-lbl">The People</p>
  <h2 class="pc-narr__head" style="margin-bottom:3rem;">
    Meet the <span>Team</span>
  </h2>

  <div class="pc-team-grid pc-stagger">

    <!-- CIO — lead card -->
    <div class="pc-card pc-card--lead">
      <img class="pc-card__img" src="{{ '/assets/images/tm/2.jpg' | relative_url }}" alt="Naveed A. Aun" loading="lazy">
      <div class="pc-card__overlay"></div>
      <div class="pc-card__bar"></div>
      <span class="pc-card__idx">02</span>
      <div class="pc-card__body">
        <div class="pc-card__role">Chief Information Officer</div>
        <div class="pc-card__name">Naveed A. Aun</div>
      </div>
    </div>

    <!-- CTO — lead card -->
    <div class="pc-card pc-card--lead">
      <img class="pc-card__img" src="{{ '/assets/images/tm/3.jpg' | relative_url }}" alt="Zubair Ansari" loading="lazy">
      <div class="pc-card__overlay"></div>
      <div class="pc-card__bar"></div>
      <span class="pc-card__idx">03</span>
      <div class="pc-card__body">
        <div class="pc-card__role">Chief Technology Officer</div>
        <div class="pc-card__name">Zubair Ansari</div>
      </div>
    </div>

    <!-- 01 Saeed Ullah -->
    <div class="pc-card">
      <img class="pc-card__img" src="{{ '/assets/images/tm/1.jpg' | relative_url }}" alt="Saeed Ullah" loading="lazy">
      <div class="pc-card__overlay"></div>
      <div class="pc-card__bar"></div>
      <span class="pc-card__idx">01</span>
      <div class="pc-card__body">
        <div class="pc-card__role">Head of Marketing</div>
        <div class="pc-card__name">Saeed Ullah</div>
      </div>
    </div>

    <!-- 04 Sara Malik -->
    <div class="pc-card">
      <img class="pc-card__img" src="{{ '/assets/images/tm/4.jpg' | relative_url }}" alt="Sara Malik" loading="lazy">
      <div class="pc-card__overlay"></div>
      <div class="pc-card__bar"></div>
      <span class="pc-card__idx">04</span>
      <div class="pc-card__body">
        <div class="pc-card__role">Head of Research</div>
        <div class="pc-card__name">Sara Malik</div>
      </div>
    </div>

    <!-- 08 Ji Won -->
    <div class="pc-card">
      <img class="pc-card__img" src="{{ '/assets/images/tm/8.jpg' | relative_url }}" alt="Ji Won" loading="lazy">
      <div class="pc-card__overlay"></div>
      <div class="pc-card__bar"></div>
      <span class="pc-card__idx">08</span>
      <div class="pc-card__body">
        <div class="pc-card__role">Head of Innovations</div>
        <div class="pc-card__name">Ji Won</div>
      </div>
    </div>

    <!-- 09 Zeynep Akata -->
    <div class="pc-card">
      <img class="pc-card__img" src="{{ '/assets/images/tm/9.jpg' | relative_url }}" alt="Zeynep Akata" loading="lazy">
      <div class="pc-card__overlay"></div>
      <div class="pc-card__bar"></div>
      <span class="pc-card__idx">09</span>
      <div class="pc-card__body">
        <div class="pc-card__role">Research Fellow</div>
        <div class="pc-card__name">Zeynep Akata</div>
      </div>
    </div>

    <!-- 10 David Chen -->
    <div class="pc-card">
      <img class="pc-card__img" src="{{ '/assets/images/tm/10.jpg' | relative_url }}" alt="David Chen" loading="lazy">
      <div class="pc-card__overlay"></div>
      <div class="pc-card__bar"></div>
      <span class="pc-card__idx">10</span>
      <div class="pc-card__body">
        <div class="pc-card__role">Research Fellow</div>
        <div class="pc-card__name">David Chen</div>
      </div>
    </div>

    <!-- 11 Fatima Khan -->
    <div class="pc-card">
      <img class="pc-card__img" src="{{ '/assets/images/tm/11.jpg' | relative_url }}" alt="Fatima Khan" loading="lazy">
      <div class="pc-card__overlay"></div>
      <div class="pc-card__bar"></div>
      <span class="pc-card__idx">11</span>
      <div class="pc-card__body">
        <div class="pc-card__role">Research Fellow</div>
        <div class="pc-card__name">Fatima Khan</div>
      </div>
    </div>

    <!-- 05 Noman A. Riaz -->
    <div class="pc-card">
      <img class="pc-card__img" src="{{ '/assets/images/tm/5.jpg' | relative_url }}" alt="Noman A. Riaz" loading="lazy">
      <div class="pc-card__overlay"></div>
      <div class="pc-card__bar"></div>
      <span class="pc-card__idx">05</span>
      <div class="pc-card__body">
        <div class="pc-card__role">Advisor</div>
        <div class="pc-card__name">Noman A. Riaz</div>
      </div>
    </div>

    <!-- 06 Christina Tunder -->
    <div class="pc-card">
      <img class="pc-card__img" src="{{ '/assets/images/tm/6.jpg' | relative_url }}" alt="Christina Tunder" loading="lazy">
      <div class="pc-card__overlay"></div>
      <div class="pc-card__bar"></div>
      <span class="pc-card__idx">06</span>
      <div class="pc-card__body">
        <div class="pc-card__role">Senior Advisor</div>
        <div class="pc-card__name">Christina Tunder</div>
      </div>
    </div>

    <!-- 07 Nadia Waheed -->
    <div class="pc-card">
      <img class="pc-card__img" src="{{ '/assets/images/tm/7.jpg' | relative_url }}" alt="Nadia Waheed" loading="lazy">
      <div class="pc-card__overlay"></div>
      <div class="pc-card__bar"></div>
      <span class="pc-card__idx">07</span>
      <div class="pc-card__body">
        <div class="pc-card__role">Advisor</div>
        <div class="pc-card__name">Nadia Waheed</div>
      </div>
    </div>

    <!-- 12 Grieg Greger -->
    <div class="pc-card">
      <img class="pc-card__img" src="{{ '/assets/images/tm/12.jpg' | relative_url }}" alt="Grieg Greger" loading="lazy">
      <div class="pc-card__overlay"></div>
      <div class="pc-card__bar"></div>
      <span class="pc-card__idx">12</span>
      <div class="pc-card__body">
        <div class="pc-card__role">Advisor</div>
        <div class="pc-card__name">Grieg Greger</div>
      </div>
    </div>

  </div><!-- /team-grid -->
</section>

<hr class="pc-divider">

<!-- ══════════════ ABOUT STRIP ══════════════ -->
<section class="pc-sec pc-sec--alt">
  <div class="pc-about">
    <div class="pc-fade">
      <p class="pc-lbl">What We Do</p>
      <h2 class="pc-about__head">
        From competition<br>to <span>community</span>
      </h2>
      <p>PakCrypt is a non-profit organisation based in Islamabad. Since 2022, we have run Pakistan's most rigorous annual cryptography competition, drawing participants from universities and industry across the country.</p>
      <p>Our scope has expanded every year — from a single competition to a full international symposium co-hosted with IACR, a thesis support programme funding original research, and a growing library of technical articles and whitepapers.</p>
      <ul class="pc-about__list">
        <li>Annual international cryptography competition (Professional &amp; Amateur tracks)</li>
        <li>IACR Cryptography Winter School, Islamabad</li>
        <li>International Cyber Security Symposium</li>
        <li>Thesis funding for undergraduate researchers (Rs. 100K–200K)</li>
        <li>Technical publications, whitepapers, and Crypt Pulse news</li>
      </ul>
    </div>

    <div class="pc-box pc-fade">
      <div class="pc-box__eye">PakCrypt 2026</div>
      <div class="pc-box__title">Register for the 5th Annual Edition</div>
      <div class="pc-box__text">
        NCCS, Air University, Islamabad &middot; November 2026 (tentative)<br><br>
        Pre-Qualifying Round opens September 2026. Two tracks: <strong>Professional</strong> (open to all) and <strong>Amateur</strong> (under 20). Total prize pool: <strong style="color:var(--accent)!important;">Rs. 5.0 million</strong>. Finalists receive full sponsorship — travel, accommodation, meals, and free IACR Winter School registration.
      </div>
      <a href="https://forms.gle/miKnbJv5VrTPwiAb8" class="pc-box__cta" target="_blank" rel="noopener">
        Register Now →
      </a>
    </div>
  </div>
</section>

<hr class="pc-divider">

<!-- ══════════════ CTA ══════════════ -->
<section class="pc-cta">
  <h2 class="pc-cta__head">
    Ready to prove<br>your cryptographic mettle?
  </h2>
  <p class="pc-cta__sub">
    Join Pakistan's most rigorous cryptography challenge. Pre-qualifying opens September 2026 — open to all.
  </p>
  <div class="pc-btn-row">
    <a href="https://forms.gle/miKnbJv5VrTPwiAb8" class="pc-btn" target="_blank" rel="noopener">
      Register for PakCrypt 2026 →
    </a>
    <a href="https://pakcrypt.org/assets/doc/pc26samv1.pdf" class="pc-btn pc-btn--ghost" target="_blank" rel="noopener">
      Sample Problems (PDF)
    </a>
  </div>
</section>

<!-- ══════════════ FOOTER ══════════════ -->
<footer class="pc-foot">
  <span>&copy; 2026 PakCrypt NPO, Islamabad, Pakistan</span>
  <span>
    <a href="https://pakcrypt.org" target="_blank" rel="noopener">pakcrypt.org</a>
    &nbsp;&middot;&nbsp;
    <a href="https://twitter.com/PakCryptOrg" target="_blank" rel="noopener">@PakCryptOrg</a>
    &nbsp;&middot;&nbsp;
    <a href="https://iacr.org" target="_blank" rel="noopener">iacr.org</a>
  </span>
</footer>

</div><!-- /#pc-team-page -->

<script>
(function () {
  'use strict';

  // ── Scroll-triggered fade-in ──────────────────────────
  var io = new IntersectionObserver(function (entries) {
    entries.forEach(function (e) {
      if (e.isIntersecting) {
        e.target.classList.add('pc-in');
        io.unobserve(e.target);
      }
    });
  }, { threshold: 0.07, rootMargin: '0px 0px -50px 0px' });

  document.querySelectorAll('.pc-fade, .pc-stagger').forEach(function (el) {
    io.observe(el);
  });

  // ── Gentle mouse-parallax on hero glows (desktop only) ─
  if (window.matchMedia('(min-width: 768px) and (prefers-reduced-motion: no-preference)').matches) {
    var ga = document.querySelector('.pc-glow--a');
    var gb = document.querySelector('.pc-glow--b');
    var rafId;
    document.addEventListener('mousemove', function (e) {
      cancelAnimationFrame(rafId);
      rafId = requestAnimationFrame(function () {
        var x = (e.clientX / window.innerWidth  - .5) * 28;
        var y = (e.clientY / window.innerHeight - .5) * 28;
        if (ga) ga.style.transform = 'translate(' + x + 'px,' + y + 'px)';
        if (gb) gb.style.transform = 'translate(' + (-x*.6) + 'px,' + (-y*.6) + 'px)';
      });
    });
  }
})();
</script>