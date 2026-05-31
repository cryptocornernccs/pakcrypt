---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
pin: true
custom_css: true
---

<style >
@import url('https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800 &family=DM+Mono:wght@300;400;500 &family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300 &display=swap');

/* ═══════════════════════════════════════════════════════════
   ESCAPE CHIRPY'S CONTENT COLUMN (FIXED)
   ═══════════════════════════════════════════════════════════ */
/* Hide the standard header */
article.px-1 > header { display: none !important; }

/* Clean up padding but do NOT touch margins on the article */
article.px-1 { padding: 0 !important; }

/* Make content full-width, but allow visible overflow */
div.content { 
  max-width: 100% !important; 
  padding: 0 !important; 
  margin: 0 !important;
  overflow-x: visible !important;
}

/* ═══════════════════════════════════════════════════════════
   CRITICAL FIX FOR SIDEBAR FREEZE
   Do NOT modify main-wrapper or core-wrapper!
   ═══════════════════════════════════════════════════════════ */
/* 
   The lines below were causing the sidebar freeze by stripping
   the structural padding required for the Chirpy layout.
   They have been removed.
   
#main-wrapper, #core-wrapper, .row.filler { 
  padding: 0 !important; 
  margin: 0 !important;
}
*/

/* ═══════════════════════════════════════════════════════════
   TOKENS
   ═══════════════════════════════════════════════════════════ */
:root {
  --q-ink:    #09090f;
  --q-ink2:   #0f0f17;
  --q-card:   #111119;
  --q-line:   #1d1d29;
  --q-muted:  #7a7a96;
  --q-text:   #c4c4d4;
  --q-light:  #eeeef5;
  --q-accent: #00e5c0;
  --q-acct2:  #7b61ff;
  --q-fh:     'Syne', sans-serif;
  --q-fm:     'DM Mono', monospace;
  --q-fb:     'DM Sans', sans-serif;
}

/* ══════════════════════════════════════════════════════════
   ROOT WRAPPER
   ═══════════════════════════════════════════════════════════ */
#q {
  background: var(--q-ink);
  color: var(--q-text);
  font-family: var(--q-fb);
  font-weight: 300;
  line-height: 1.7;
  overflow-x: visible;
  margin-left: 0;
  margin-right: 0;
}
#q *, #q *::before, #q *::after { box-sizing: border-box; }
#q h1, #q h2, #q h3 { color: var(--q-light); border: none; padding: 0; margin: 0; }
#q p  { color: var(--q-text); margin: 0; }
#q a  { text-decoration: none; }
#q ul { list-style: none; padding: 0; margin: 0; }
#q blockquote { border: none; padding: 0; margin: 0; color: var(--q-text); }
#q strong { color: var(--q-light); font-weight: 600; }

/* ═══════════════════════════════════════════════════════════
   HERO
   ═══════════════════════════════════════════════════════════ */
.q-hero {
  background: var(--q-ink);
  position: relative;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  padding: clamp(2rem, 8vw, 6rem);
  overflow: hidden;
}
.q-hero__grid {
  position: absolute; inset: 0; z-index: 0;
  background-image:
    linear-gradient(rgba(0,229,192,.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,229,192,.03) 1px, transparent 1px);
  background-size: 60px 60px;
  animation: qGrid 30s linear infinite;
}
@keyframes qGrid {
  to { background-position: 60px 60px; }
}
.q-glow {
  position: absolute; border-radius: 50%;
  filter: blur(110px); pointer-events: none; z-index: 0;
}
.q-glow-a {
  width: 560px; height: 560px;
  background: radial-gradient(circle, rgba(0,229,192,.16) 0%, transparent 70%);
  top: -180px; right: -80px;
  animation: qGlow 9s ease-in-out infinite;
}
.q-glow-b {
  width: 380px; height: 380px;
  background: radial-gradient(circle, rgba(123,97,255,.13) 0%, transparent 70%);
  bottom: -40px; left: -80px;
  animation: qGlow 11s ease-in-out infinite reverse;
}
@keyframes qGlow {
  0%,100% { opacity:.7; transform:scale(1); }
  50%      { opacity:1;  transform:scale(1.07); }
}
.q-hero__chip {
  position: absolute;
  top: clamp(1.25rem,4vw,3rem);
  right: clamp(1.25rem,4vw,3rem);
  z-index: 2;
  font-family: var(--q-fm);
  font-size: .68rem; letter-spacing: .14em;
  color: var(--q-muted);
  border: 1px solid var(--q-line);
  padding: .4rem 1rem;
  border-radius: 999px;
  background: rgba(9,9,15,.75);
  backdrop-filter: blur(12px);
}
.q-hero__eye {
  position: relative; z-index: 1;
  font-family: var(--q-fm);
  font-size: .7rem; letter-spacing: .22em;
  text-transform: uppercase;
  color: var(--q-accent);
  margin-bottom: 1.25rem;
  display: flex; align-items: center; gap: .75rem;
}
.q-hero__eye::before {
  content: '';
  width: 2.5rem; height: 1px;
  background: var(--q-accent);
  flex-shrink: 0;
  display: inline-block;
}
.q-hero__h1 {
  position: relative; z-index: 1;
  font-family: var(--q-fh) !important;
  font-size: clamp(3.5rem, 8vw, 6rem) !important;
  font-weight: 800 !important;
  line-height: 1.0 !important;
  letter-spacing: -.03em;
  color: var(--q-light) !important;
  word-break: normal !important;
  overflow-wrap: normal !important;
}
.q-hero__h1 em {
  font-style: normal;
  -webkit-text-stroke: 1.5px var(--q-accent);
  color: transparent !important;
}
.q-hero__sub {
  position: relative; z-index: 1;
  font-family: var(--q-fb);
  font-size: clamp(.9rem, 2vw, 1.1rem);
  color: var(--q-muted);
  max-width: 500px;
  margin-top: 1.5rem;
  line-height: 1.8;
}
.q-hero__scroll {
  position: relative; z-index: 1;
  margin-top: 3rem;
  display: flex; align-items: center; gap: 1rem;
  font-family: var(--q-fm); font-size: .67rem;
  letter-spacing: .16em; text-transform: uppercase;
  color: var(--q-muted);
}
.q-hero__scroll-bar {
  width: 4rem; height: 1px;
  background: linear-gradient(90deg, var(--q-accent), transparent);
  animation: qScrollBar 2s ease-in-out infinite;
}
@keyframes qScrollBar {
  0%,100% { width:4rem; opacity:1; }
  50%      { width:7rem; opacity:.5; }
}

/* ══════════════════════════════════════════════════════════
   STATS STRIP
   ══════════════════════════════════════════════════════════ */
.q-stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%,160px),1fr));
  background: var(--q-ink);
  border-top: 1px solid var(--q-line);
  border-bottom: 1px solid var(--q-line);
}
.q-stat {
  background: var(--q-ink);
  padding: 1.5rem 0.8rem;
  border-right: 1px solid var(--q-line);
  position: relative; overflow: hidden;
  transition: background .25s;
  text-align: center;
}
.q-stat:last-child { border-right: none; }
.q-stat:hover { background: var(--q-ink2); }
.q-stat__n {
  font-family: var(--q-fh) !important;
  font-size: clamp(1.8rem, 2.5vw, 2.5rem) !important; 
  font-weight: 800 !important;
  color: var(--q-light) !important;
  line-height: 1.1;
  letter-spacing: -.04em;
  white-space: nowrap !important;
}
.q-stat__n span { color: var(--q-accent) !important; }
.q-stat__l {
  font-family: var(--q-fm);
  font-size: .66rem; letter-spacing: .15em;
  text-transform: uppercase;
  color: var(--q-muted);
  margin-top: .4rem;
}
.q-stat__glow {
  position: absolute; bottom: -30px; right: -30px;
  width: 100px; height: 100px;
  background: radial-gradient(circle, rgba(0,229,192,.07) 0%, transparent 70%);
  border-radius: 50%;
}

/* ═══════════════════════════════════════════════════════════
   SECTIONS
   ═══════════════════════════════════════════════════════════ */
.q-sec {
  background: var(--q-ink);
  padding: clamp(4rem,10vw,8rem) clamp(1.5rem,5vw,5rem);
  position: relative;
}
.q-sec--alt { background: var(--q-ink2); }
.q-hr { height: 1px; background: var(--q-line); margin: 0; border: none; }

.q-lbl {
  font-family: var(--q-fm);
  font-size: .67rem; letter-spacing: .22em;
  text-transform: uppercase;
  color: var(--q-accent);
  margin-bottom: 1.25rem;
  display: flex; align-items: center; gap: .75rem;
}
.q-lbl::before { 
  content: ''; width: 1.5rem; height: 1px;
  background: var(--q-accent); flex-shrink: 0; display: inline-block;
}

.q-head {
  font-family: var(--q-fh) !important;
  font-size: clamp(1.8rem,5vw,3.4rem) !important;
  font-weight: 700 !important;
  line-height: 1.1 !important;
  color: var(--q-light) !important;
  letter-spacing: -.02em;
  margin-bottom: 2.5rem !important;
}
.q-head span { color: var(--q-accent) !important; }

.q-wrap { max-width: 1200px; margin: 0 auto; }
.q-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%,320px),1fr));
  gap: 2px;
}
.q-block {
  background: var(--q-card);
  padding: 2.25rem;
  border-top: 2px solid transparent;
  position: relative; overflow: hidden;
  transition: border-color .3s, background .3s;
}
.q-block:hover { border-color: var(--q-accent); background: #13131f; }
.q-block::before {
  content: '';
  position: absolute; top: 0; left: 0; right: 0; height: 2px;
  background: linear-gradient(90deg, var(--q-accent), var(--q-acct2));
  opacity: 0; transition: opacity .3s;
}
.q-block:hover::before { opacity: 1; } 
.q-block__icon { font-size: 1.8rem; margin-bottom: 1rem; display: block; }
.q-block__title {
  font-family: var(--q-fh) !important;
  font-size: 1.15rem !important; font-weight: 700 !important;
  color: var(--q-light) !important;
  margin-bottom: .6rem !important;
}
.q-block p {
  font-size: .92rem;
  color: var(--q-muted) !important;
  line-height: 1.85;
}

.q-quote {
  margin-top: 3.5rem;
  border-left: 3px solid var(--q-accent);
  padding: 1.4rem 2rem;
  background: rgba(0,229,192,.04);
  font-family: var(--q-fh) !important;
  font-size: clamp(1rem,2.5vw,1.4rem) !important;
  font-weight: 600 !important;
  color: var(--q-light) !important;
  line-height: 1.55;
}
.q-quote cite {
  display: block; margin-top: .65rem;
  font-family: var(--q-fm); 
  font-size: .7rem; letter-spacing: .1em;
  color: var(--q-muted) !important;
  font-style: normal;
}

/* ═══════════════════════════════════════════════════════════
   TEAM GRID
   ═══════════════════════════════════════════════════════════ */
.q-team {
  display: grid;
  /* auto-fill + smaller min-width = natural 2/3/4 columns depending on viewport */
  grid-template-columns: repeat(auto-fill, minmax(190px, 1fr)); 
  gap: 2px;
  max-width: 1200px;
  margin: 0 auto;
}
.q-card {
  background: var(--q-card);
  position: relative; overflow: hidden;
  aspect-ratio: 3/4;
  display: flex; flex-direction: column; justify-content: flex-end;
}
@media (min-width: 860px) {
  .q-card--lead { grid-column: span 2; aspect-ratio: 16/9; }
  .q-card--lead .q-card__name { font-size: 1.7rem !important; }
  .q-card--lead .q-card__body { padding: 2.25rem !important; }
}
.q-card__img {
  position: absolute; inset: 0;
  width: 100%; height: 100%;
  object-fit: cover; object-position: top center;
  filter: grayscale(20%) contrast(1.05);
  transition: filter .5s, transform .6s cubic-bezier(.16,1,.3,1);
  display: block;
}
.q-card:hover .q-card__img {
  filter: grayscale(0%) contrast(1.08);
  transform: scale(1.04);
}
.q-card__over {
  position: absolute; inset: 0;
  background: linear-gradient(
    to top,
    rgba(9,9,15,.97) 0%,
    rgba(9,9,15,.52) 36%,
    rgba(9,9,15,.07) 66%,
    transparent 100%
  );
  transition: background .4s;
}
.q-card:hover .q-card__over {
  background: linear-gradient(
    to top,
    rgba(9,9,15,.99) 0%,
    rgba(9,9,15,.78) 48%,
    rgba(9,9,15,.28) 76%,
    transparent 100%
  );
}
.q-card__bar {
  position: absolute; bottom: 0; left: 0; right: 0; height: 2px;
  background: linear-gradient(90deg, var(--q-accent), var(--q-acct2));
  transform: scaleX(0); transform-origin: left;
  transition: transform .4s cubic-bezier(.16,1,.3,1);
}
.q-card:hover .q-card__bar { transform: scaleX(1); }
.q-card__body { position: relative; z-index: 1; padding: 1.4rem; }
.q-card__role {
  font-family: var(--q-fm) !important;
  font-size: .61rem !important; letter-spacing: .18em;
  text-transform: uppercase;
  color: var(--q-accent) !important;
  margin-bottom: .3rem !important;
}
.q-card__name {
  font-family: var(--q-fh) !important;
  font-size: 1.15rem !important; font-weight: 700 !important;
  color: var(--q-light) !important;
  letter-spacing: -.01em; line-height: 1.2;
}
.q-card__idx {
  position: absolute; top: .9rem; left: .9rem;
  font-family: var(--q-fm); font-size: .6rem; letter-spacing: .1em;
  color: rgba(196,196,212,.22);
  z-index: 1;
}

/* ═══════════════════════════════════════════════════════════
   ABOUT STRIP
   ═══════════════════════════════════════════════════════════ */
.q-about {
  max-width: 1200px; margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: clamp(2rem,5vw,5rem);
  align-items: start;
}
@media (max-width: 680px) { .q-about { grid-template-columns: 1fr; } }

.q-about__head {
  font-family: var(--q-fh) !important;
  font-size: clamp(1.6rem,4vw,2.6rem) !important;
  font-weight: 700 !important;
  color: var(--q-light) !important;
  letter-spacing: -.02em; line-height: 1.15;
  margin-bottom: 1.2rem !important;
}
.q-about__head span { color: var(--q-accent) !important; }

.q-about p {
  font-size: .96rem;
  color: var(--q-muted) !important;
  line-height: 1.9; margin-bottom: .85rem !important;
}
.q-about__list { margin-top: 1.4rem !important; }
.q-about__list li {
  display: flex; align-items: flex-start; gap: .7rem;
  padding: .52rem 0;
  border-bottom: 1px solid var(--q-line);
  font-size: .89rem;
  color: var(--q-text) !important;
}
.q-about__list li::before {
  content: '→'; color: var(--q-accent);
  font-family: var(--q-fm); flex-shrink: 0;
}

.q-box {
  background: var(--q-card);
  border: 1px solid var(--q-line);
  padding: 2.25rem;
  position: relative; overflow: hidden;
}
.q-box::after {
  content: '';
  position: absolute; top: 0; right: 0;
  width: 120px; height: 120px;
  background: radial-gradient(circle, rgba(0,229,192,.08) 0%, transparent 70%);
  pointer-events: none;
}
.q-box__eye {
  font-family: var(--q-fm);
  font-size: .63rem; letter-spacing: .2em;
  text-transform: uppercase;
  color: var(--q-accent);
  margin-bottom: .85rem;
}
.q-box__title {
  font-family: var(--q-fh) !important;
  font-size: 1.4rem !important; font-weight: 700 !important;
  color: var(--q-light) !important;
  margin-bottom: .85rem !important;
}
.q-box__text {
  font-size: .92rem;
  color: var(--q-muted) !important;
  line-height: 1.85;
}
.q-box__text strong { color: var(--q-light) !important; }
.q-box__cta {
  display: inline-flex; align-items: center; gap: .5rem;
  margin-top: 1.4rem;
  font-family: var(--q-fm); font-size: .71rem;
  letter-spacing: .1em; text-transform: uppercase;
  color: var(--q-accent) !important;
  border-bottom: 1px solid var(--q-accent);
  padding-bottom: 2px;
  transition: gap .3s;
}
.q-box__cta:hover { gap: .9rem; }

/* ═══════════════════════════════════════════════════════════
   CTA BAND
   ═══════════════════════════════════════════════════════════ */
.q-cta {
  background: var(--q-card);
  padding: clamp(4rem,8vw,7rem) clamp(1.5rem,5vw,5rem);
  text-align: center;
  position: relative; overflow: hidden;
}
.q-cta::before {
  content: '';
  position: absolute; inset: 0;
  background: repeating-linear-gradient(
    -45deg,
    rgba(0,229,192,.016) 0, rgba(0,229,192,.016) 1px,
    transparent 1px, transparent 20px
  );
  pointer-events: none;
}
.q-cta__head {
  font-family: var(--q-fh) !important;
  font-size: clamp(1.8rem,5vw,3.4rem) !important;
  font-weight: 800 !important;
  color: var(--q-light) !important;
  letter-spacing: -.03em; line-height: 1.1;
  margin-bottom: .9rem !important;
  position: relative; z-index: 1;
}
.q-cta__sub {
  font-size: .98rem;
  color: var(--q-muted) !important;
  max-width: 440px; margin: 0 auto 2.25rem !important;
  line-height: 1.8;
  position: relative; z-index: 1;
}
.q-btn-row { position: relative; z-index: 1; display: flex; flex-wrap: wrap; gap: .7rem; justify-content: center; }
.q-btn {
  display: inline-flex; align-items: center; gap: .5rem;
  background: var(--q-accent);
  color: var(--q-ink) !important;
  font-family: var(--q-fh) !important;
  font-size: .87rem !important; font-weight: 700 !important;
  padding: .82rem 1.8rem;
  border-radius: 2px;
  transition: background .22s, transform .22s, box-shadow .22s;
}
.q-btn:hover {
  background: var(--q-light);
  color: var(--q-ink) !important;
  transform: translateY(-2px);
  box-shadow: 0 8px 28px rgba(0,229,192,.2);
}
.q-btn--ghost {
  background: transparent !important;
  color: var(--q-accent) !important;
  border: 1px solid var(--q-accent);
}
.q-btn--ghost:hover {
  background: rgba(0,229,192,.07) !important;
  color: var(--q-accent) !important;
  transform: translateY(-2px);
}

/* ═══════════════════════════════════════════════════════════
   FOOTER
   ═══════════════════════════════════════════════════════════ */
.q-foot {
  background: var(--q-ink);
  border-top: 1px solid var(--q-line);
  padding: 2rem clamp(1.5rem,5vw,5rem);
  display: flex; justify-content: space-between;
  align-items: center; flex-wrap: wrap; gap: 1rem;
  font-family: var(--q-fm); font-size: .67rem; letter-spacing: .1em;
  color: var(--q-muted) !important;
}
.q-foot a { color: var(--q-muted) !important; transition: color .2s; }
.q-foot a:hover { color: var(--q-accent) !important; }

/* ═══════════════════════════════════════════════════════════
   FADE ANIMATIONS
   ═══════════════════════════════════════════════════════════ */
.q-fade {
  opacity: 0; transform: translateY(20px);
  transition: opacity .7s cubic-bezier(.16,1,.3,1), transform .7s cubic-bezier(.16,1,.3,1);
}
.q-fade.q-in { opacity: 1; transform: none; }

.q-stagger  > * {
  opacity: 0; transform: translateY(16px);
  transition: opacity .6s cubic-bezier(.16,1,.3,1), transform .6s cubic-bezier(.16,1,.3,1);
}
.q-stagger.q-in  > * { opacity: 1; transform: none; }
.q-stagger.q-in  > *:nth-child(1)  { transition-delay:.00s }
.q-stagger.q-in  > *:nth-child(2)  { transition-delay:.07s }
.q-stagger.q-in  > *:nth-child(3)  { transition-delay:.14s }
.q-stagger.q-in  > *:nth-child(4)  { transition-delay:.21s }
.q-stagger.q-in  > *:nth-child(5)  { transition-delay:.28s }
.q-stagger.q-in  > *:nth-child(6)  { transition-delay:.35s }
.q-stagger.q-in  > *:nth-child(7)  { transition-delay:.42s }
.q-stagger.q-in  > *:nth-child(8)  { transition-delay:.49s }
.q-stagger.q-in  > *:nth-child(9)  { transition-delay:.56s }
.q-stagger.q-in  > *:nth-child(10) { transition-delay:.63s }
.q-stagger.q-in  > *:nth-child(11) { transition-delay:.70s }
.q-stagger.q-in  > *:nth-child(12) { transition-delay:.77s }

@media (max-width:560px) {
  .q-stat { padding: 1.4rem 1rem; }
  .q-block { padding: 1.6rem; }
}
</style >

<div id="q">
  <!-- ════════════ HERO ════════════ -->
  <section class="q-hero">
    <div class="q-hero__grid"></div>
    <div class="q-glow q-glow-a"></div>
    <div class="q-glow q-glow-b"></div>
    <div class="q-hero__chip">Est. 2022 · Islamabad, PK</div>
    <div class="q-hero__eye">PakCrypt · Our Team</div>
    <h2 class="q-hero__h1">
      People &amp; <br><em>Purpose</em> <br>Behind <br>PakCrypt
    </h2>
    <p class="q-hero__sub">
      A multidisciplinary team of cryptographers, engineers, researchers, and educators — united by one conviction: that mathematical rigour and cryptographic literacy are our most strategic intellectual assets.
    </p>
    <div class="q-hero__scroll">
      <div class="q-hero__scroll-bar"></div>
      Scroll to explore
    </div>
  </section>

  <!-- ════════════ STATS ════════════ -->
  <div class="q-stats q-stagger">
    <div class="q-stat"><div class="q-stat__n">5<span>th</span></div><div class="q-stat__l">Annual Edition</div><div class="q-stat__glow"></div></div>
    <div class="q-stat"><div class="q-stat__n">1K<span>+</span></div><div class="q-stat__l">Expected Participants</div><div class="q-stat__glow"></div></div>
    <div class="q-stat"><div class="q-stat__n">13<span>+</span></div><div class="q-stat__l">Intl Experts (2025)</div><div class="q-stat__glow"></div></div>
    <div class="q-stat"><div class="q-stat__n">5M</div><div class="q-stat__l">PKR Total Prizes</div><div class="q-stat__glow"></div></div>
    <div class="q-stat"><div class="q-stat__n">2</div><div class="q-stat__l">Competition Tracks</div><div class="q-stat__glow"></div></div>
  </div>
  <hr class="q-hr">

  <!-- ════════════ NARRATIVE ════════════ -->
  <section class="q-sec q-sec--alt">
    <div class="q-wrap">
      <p class="q-lbl">Why We Exist</p>
      <h2 class="q-head">Mathematics is not a subject.<br>It is the <span>language of trust</span>.</h2>
      <div class="q-grid q-stagger">
        <div class="q-block">
          <span class="q-block__icon">∮</span>
          <div class="q-block__title">The Mathematical Foundation</div>
          <p>Every encrypted message, every digital signature, every secure transaction rests on theorems proved centuries before computers existed. Number theory, abstract algebra, elliptic curves — these are the load-bearing structures of the digital world.</p>
        </div>
        <div class="q-block">
          <span class="q-block__icon">🔐</span>
          <div class="q-block__title">Cryptography as Civilisational Infrastructure</div>
          <p>Banking, governance, healthcare, defence, communications — every critical system today depends on cryptographic primitives for its integrity and confidentiality. A nation that cannot independently reason about cryptography is not sovereign in any meaningful technological sense.</p>
        </div>
        <div class="q-block">
          <span class="q-block__icon">️</span>
          <div class="q-block__title">The Post-Quantum Imperative</div>
          <p>Quantum computers capable of breaking RSA and ECC are approaching. NIST has already standardised post-quantum algorithms. Pakistan cannot afford to be a late adopter — the cost is measured not in dollars, but in compromised state secrets and national communications.</p>
        </div>
        <div class="q-block">
          <span class="q-block__icon">⚡</span>
          <div class="q-block__title">Building Homegrown Expertise</div>
          <p>PakCrypt was founded on the conviction that world-class cryptographic talent can be cultivated in Pakistan. Through competitions that demand real mathematical depth, symposiums that connect local talent with IACR-affiliated researchers, and thesis support programmes, we are building a pipeline — not importing one.</p>
        </div>
        <div class="q-block">
          <span class="q-block__icon">🎓</span>
          <div class="q-block__title">Education Without Borders</div>
          <p>The IACR Cryptography Winter School we co-host annually brings the world's leading cryptographers to Islamabad. This is not a lecture series — it is hands-on mentorship from the people who design the protocols the world depends on.</p>
        </div>
        <div class="q-block">
          <span class="q-block__icon"></span>
          <div class="q-block__title">Community, Not Just Competition</div>
          <p>PakCrypt is not a trophy-hunting exercise. Our non-profit structure means every rupee of prize money and operational budget goes toward the mission. Our networking dinners, expert Q&amp;A sessions, and open symposiums collapse the hierarchy between established professionals and emerging talent.</p>
        </div>
      </div>
      <blockquote class="q-quote q-fade">
        "The security of the world's information infrastructure is ultimately a mathematics problem. Nations that invest in mathematical education today will write the cryptographic standards of tomorrow."
        <cite>— PakCrypt founding principle, 2022</cite>
      </blockquote>
    </div>
  </section>
  <hr class="q-hr">

  <!-- ════════════ TEAM ════════════ -->
  <section class="q-sec">
    <p class="q-lbl">The People</p>
    <h2 class="q-head" style="margin-bottom:2.5rem">Meet the <span>Team</span></h2>
    <div class="q-team q-stagger">
      <!-- Lead Cards -->
      <div class="q-card">
        <img class="q-card__img" src="{{ '/assets/images/tm/2.jpg' | relative_url }}" alt="Naveed A. Aun" loading="lazy">
        <div class="q-card__over"></div><div class="q-card__bar"></div>
        <span class="q-card__idx">02</span>
        <div class="q-card__body">
          <div class="q-card__role">Chief Information Officer</div>
          <div class="q-card__name">Naveed A. Aun</div>
        </div>
      </div>
      <div class="q-card">
        <img class="q-card__img" src="{{ '/assets/images/tm/3.jpg' | relative_url }}" alt="Zubair Ansari" loading="lazy">
        <div class="q-card__over"></div><div class="q-card__bar"></div>
        <span class="q-card__idx">03</span>
        <div class="q-card__body">
          <div class="q-card__role">Chief Technology Officer</div>
          <div class="q-card__name">Zubair Ansari</div>
        </div>
      </div>
      <!-- Regular Cards -->
      <div class="q-card">
        <img class="q-card__img" src="{{ '/assets/images/tm/1.jpg' | relative_url }}" alt="Saeed Ullah" loading="lazy">
        <div class="q-card__over"></div><div class="q-card__bar"></div>
        <span class="q-card__idx">01</span>
        <div class="q-card__body">
          <div class="q-card__role">Head of Marketing</div>
          <div class="q-card__name">Saeed Ullah</div>
        </div>
      </div>
      <div class="q-card">
        <img class="q-card__img" src="{{ '/assets/images/tm/4.jpg' | relative_url }}" alt="Sara Malik" loading="lazy">
        <div class="q-card__over"></div><div class="q-card__bar"></div>
        <span class="q-card__idx">04</span>
        <div class="q-card__body">
          <div class="q-card__role">Head of Research</div>
          <div class="q-card__name">Sara Malik</div>
        </div>
      </div>
      <div class="q-card">
        <img class="q-card__img" src="{{ '/assets/images/tm/8.jpg' | relative_url }}" alt="Ji Won" loading="lazy">
        <div class="q-card__over"></div><div class="q-card__bar"></div>
        <span class="q-card__idx">08</span>
        <div class="q-card__body">
          <div class="q-card__role">Head of Innovations</div>
          <div class="q-card__name">Ji Won</div>
        </div>
      </div>
      <div class="q-card">
        <img class="q-card__img" src="{{ '/assets/images/tm/9.jpg' | relative_url }}" alt="Zeynep Akata" loading="lazy">
        <div class="q-card__over"></div><div class="q-card__bar"></div>
        <span class="q-card__idx">09</span>
        <div class="q-card__body">
          <div class="q-card__role">Research Fellow</div>
          <div class="q-card__name">Zeynep Akata</div>
        </div>
      </div>
      <div class="q-card">
        <img class="q-card__img" src="{{ '/assets/images/tm/10.jpg' | relative_url }}" alt="David Chen" loading="lazy">
        <div class="q-card__over"></div><div class="q-card__bar"></div>
        <span class="q-card__idx">10</span>
        <div class="q-card__body">
          <div class="q-card__role">Research Fellow</div>
          <div class="q-card__name">David Chen</div>
        </div>
      </div>
      <div class="q-card">
        <img class="q-card__img" src="{{ '/assets/images/tm/11.jpg' | relative_url }}" alt="Fatima Khan" loading="lazy">
        <div class="q-card__over"></div><div class="q-card__bar"></div>
        <span class="q-card__idx">11</span>
        <div class="q-card__body">
          <div class="q-card__role">Research Fellow</div>
          <div class="q-card__name">Fatima Khan</div>
        </div>
      </div>
      <div class="q-card">
        <img class="q-card__img" src="{{ '/assets/images/tm/5.jpg' | relative_url }}" alt="Noman A. Riaz" loading="lazy">
        <div class="q-card__over"></div><div class="q-card__bar"></div>
        <span class="q-card__idx">05</span>
        <div class="q-card__body">
          <div class="q-card__role">Advisor</div>
          <div class="q-card__name">Noman A. Riaz</div>
        </div>
      </div>
      <div class="q-card">
        <img class="q-card__img" src="{{ '/assets/images/tm/6.jpg' | relative_url }}" alt="Christina Tunder" loading="lazy">
        <div class="q-card__over"></div><div class="q-card__bar"></div>
        <span class="q-card__idx">06</span>
        <div class="q-card__body">
          <div class="q-card__role">Senior Advisor</div>
          <div class="q-card__name">Christina Tunder</div>
        </div>
      </div>
      <div class="q-card">
        <img class="q-card__img" src="{{ '/assets/images/tm/7.jpg' | relative_url }}" alt="Nadia Waheed" loading="lazy">
        <div class="q-card__over"></div><div class="q-card__bar"></div>
        <span class="q-card__idx">07</span>
        <div class="q-card__body">
          <div class="q-card__role">Advisor</div>
          <div class="q-card__name">Nadia Waheed</div>
        </div>
      </div>
      <div class="q-card">
        <img class="q-card__img" src="{{ '/assets/images/tm/12.jpg' | relative_url }}" alt="Grieg Greger" loading="lazy">
        <div class="q-card__over"></div><div class="q-card__bar"></div>
        <span class="q-card__idx">12</span>
        <div class="q-card__body">
          <div class="q-card__role">Advisor</div>
          <div class="q-card__name">Grieg Greger</div>
        </div>
      </div>
    </div>
  </section>
  <hr class="q-hr">

  <!-- ════════════ ABOUT ════════════ -->
  <section class="q-sec q-sec--alt">
    <div class="q-about">
      <div class="q-fade">
        <p class="q-lbl">What We Do</p>
        <h2 class="q-about__head">From competition<br>to <span>community</span></h2>
        <p>PakCrypt is a non-profit organisation based in Islamabad. Since 2022, we have run Pakistan's most rigorous annual cryptography competition, drawing participants from universities and industry across the country.</p>
        <p>Our scope has expanded every year — from a single competition to a full international symposium co-hosted with IACR, a thesis support programme, and a growing library of technical articles and whitepapers.</p>
        <ul class="q-about__list">
          <li>Annual international cryptography competition (Professional &amp; Amateur tracks)</li>
          <li>IACR Cryptography Winter School, Islamabad</li>
          <li>International Cyber Security Symposium</li>
          <li>Thesis funding for undergraduate researchers (Rs. 100K–200K)</li>
          <li>Technical publications, whitepapers, and Crypt Pulse news</li>
        </ul>
      </div>
      <div class="q-box q-fade">
        <div class="q-box__eye">PakCrypt 2026</div>
        <div class="q-box__title">Register for the 5th Annual Edition</div>
        <div class="q-box__text">
          NCCS, Air University, Islamabad · November 2026 (tentative)<br><br>
          Pre-Qualifying Round opens September 2026. Two tracks: <strong>Professional</strong> (open to all) and <strong>Amateur</strong> (under 20). Total prize pool: <strong style="color:var(--q-accent)">Rs. 5.0 million</strong>. Finalists receive full sponsorship — travel, accommodation, meals, and free IACR Winter School registration.
        </div>
        <a href="https://pakcrypt.org/pc26" class="q-box__cta" target="_blank" rel="noopener">Register Now →</a>
      </div>
    </div>
  </section>
  <hr class="q-hr">

  <!-- ════════════ CTA ═══════════ -->
  <section class="q-cta">
    <h2 class="q-cta__head">Ready to prove<br>your cryptographic mettle?</h2>
    <p class="q-cta__sub">Join Pakistan's most rigorous cryptography challenge. Pre-qualifying opens September 2026 — open to all.</p>
    <div class="q-btn-row">
      <a href="https://pakcrypt.org/pc26" class="q-btn" target="_blank" rel="noopener">Join PakCrypt 2026 →</a>
      <a href="https://pakcrypt.org/assets/doc/pc26samv1.pdf" class="q-btn q-btn--ghost" target="_blank" rel="noopener">Sample Problems (PDF)</a>
    </div>
  </section>

  <!-- ════════════ FOOTER ════════════ -->
  <footer class="q-foot">
    <span>&copy; 2026 PakCrypt NPO, Islamabad, Pakistan</span>
    <span>
      <a href="https://pakcrypt.org">pakcrypt.org</a> ·
      <a href="https://twitter.com/PakCryptOrg" target="_blank" rel="noopener">@PakCryptOrg</a> ·
      <a href="https://iacr.org" target="_blank" rel="noopener">iacr.org</a>
    </span>
  </footer>
</div>

<script>
(function(){
  var io = new IntersectionObserver(function(entries){
    entries.forEach(function(e){
      if(e.isIntersecting){ e.target.classList.add('q-in'); io.unobserve(e.target); }
    });
  },{threshold:0.07,rootMargin:'0px 0px -40px 0px'});
  document.querySelectorAll('.q-fade,.q-stagger').forEach(function(el){ io.observe(el); });

  if(window.matchMedia('(min-width:768px) and (prefers-reduced-motion:no-preference)').matches){
    var ga=document.querySelector('.q-glow-a'), gb=document.querySelector('.q-glow-b'), raf;
    document.addEventListener('mousemove',function(e){
      cancelAnimationFrame(raf);
      raf=requestAnimationFrame(function(){
        var x=(e.clientX/innerWidth-.5)*26, y=(e.clientY/innerHeight-.5)*26;
        if(ga) ga.style.transform='translate('+x+'px,'+y+'px)';
        if(gb) gb.style.transform='translate('+(-x*.6)+'px,'+(-y*.6)+'px)';
      });
    });
  }
})();
</script>