---
layout: post
title: "Nobody Needs to Hack Your Phone"
math: true
---

<style>
/* ─── Google Fonts ─────────────────────────────────────────────── */
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;0,700;0,900;1,400;1,700&family=Source+Serif+4:ital,opsz,wght@0,8..60,300;0,8..60,400;0,8..60,600;1,8..60,300;1,8..60,400&family=JetBrains+Mono:wght@400;600&display=swap');

/* ─── Design tokens (scoped, so site theme is untouched) ───────── */
.ckp-article {
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
  --amber:        #e0935c;
  --blue:         #6bb5d6;
  --green:        #6dcf94;
  --font-serif:   'Source Serif 4', Georgia, serif;
  --font-display: 'Playfair Display', Georgia, serif;
  --font-mono:    'JetBrains Mono', 'Courier New', monospace;
}

.ckp-article * { box-sizing: border-box; }
.ckp-article {
  font-family: var(--font-serif);
  font-size: 1.1rem;
  line-height: 1.85;
  color: var(--text);
  max-width: 100%;
  position: relative;
}

/* ─── Progress Bar ─────────────────────────────────────────────── */
#ckp-progress {
  position: fixed;
  top: 0; left: 0;
  height: 3px; width: 0%;
  background: linear-gradient(90deg, #c9a84c, #e8c96a);
  z-index: 9999;
  transition: width 0.1s linear;
  box-shadow: 0 0 10px rgba(201,168,76,0.5);
}

/* ─── Hero ─────────────────────────────────────────────────────── */
.ckp-hero {
  padding: 3.5rem 0 2rem;
  border-bottom: 1px solid var(--border);
}
.ckp-kicker {
  font-family: var(--font-mono);
  font-size: 0.72rem;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 1.2rem;
  display: flex; align-items: center; gap: 0.75rem;
}
.ckp-kicker::before {
  content: ''; display: inline-block;
  width: 28px; height: 1px; background: var(--accent);
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
.ckp-hero h1 em { font-style: italic; color: var(--accent); }
.ckp-deck {
  font-size: clamp(1rem, 2vw, 1.2rem);
  font-weight: 300;
  color: var(--text-muted);
  line-height: 1.6;
  max-width: 680px;
  margin-bottom: 1.8rem;
  font-style: italic;
}
.ckp-meta {
  display: flex; flex-wrap: wrap; align-items: center; gap: 1.2rem;
  font-family: var(--font-mono);
  font-size: 0.72rem;
  color: var(--text-muted);
  letter-spacing: 0.06em;
}
.ckp-meta span { display: flex; align-items: center; gap: 0.4rem; }
.ckp-meta .dot {
  width: 3px; height: 3px; border-radius: 50%;
  background: var(--border); display: inline-block;
}
.ckp-meta a { color: var(--accent); text-decoration: none; border-bottom: 1px solid transparent; }
.ckp-meta a:hover { border-color: var(--accent); }

/* ─── Single-column body (no sidebar: this is a shorter read) ──── */
.ckp-body {
  max-width: 720px;
  margin: 2.5rem auto 0;
  min-width: 0;
}
.ckp-body section { margin-bottom: 3.5rem; }
.ckp-body h2 {
  font-family: var(--font-display);
  font-size: clamp(1.45rem, 3vw, 2.05rem);
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
  font-size: 1.22rem;
  font-weight: 600;
  color: #dcdce0;
  margin: 2.5rem 0 0.8rem;
}
.ckp-body p { margin: 0 0 1.35rem; }
.ckp-body a { color: var(--accent); text-decoration: none; border-bottom: 1px solid rgba(201,168,76,0.3); }
.ckp-body a:hover { border-bottom-color: var(--accent); }
.ckp-body .drop-cap::first-letter {
  font-family: var(--font-display);
  font-size: 4.4rem; font-weight: 900;
  float: left; line-height: 0.78;
  margin: 0.12em 0.12em -0.06em 0;
  color: var(--accent);
}

/* ─── Pull quotes ─────────────────────────────────────────────── */
.ckp-pull {
  margin: 2.6rem -1.5rem;
  padding: 1.8rem 2.2rem 1.8rem 2.5rem;
  border-left: 3px solid var(--accent);
  background: var(--accent-glow);
  position: relative;
}
@media (max-width: 700px) { .ckp-pull { margin: 2rem 0; } }
.ckp-pull::before {
  content: '\201C';
  font-family: var(--font-display);
  font-size: 5rem; color: var(--accent); opacity: 0.25;
  position: absolute; top: -0.5rem; left: 0.5rem; line-height: 1;
}
.ckp-pull p {
  font-family: var(--font-display);
  font-size: clamp(1.12rem, 2vw, 1.32rem);
  font-style: italic; font-weight: 400;
  color: #f0f0f0; line-height: 1.5; margin: 0; position: relative;
}
.ckp-pull cite {
  display: block; margin-top: 0.7rem;
  font-family: var(--font-mono);
  font-size: 0.68rem; letter-spacing: 0.1em;
  text-transform: uppercase; color: var(--text-muted); font-style: normal;
}

/* ─── Standfirst ──────────────────────────────────────────────── */
.ckp-abstract {
  background: var(--surface);
  border: 1px solid var(--border);
  border-top: 3px solid var(--accent);
  padding: 1.8rem 2rem;
  margin-bottom: 2.5rem;
  font-size: 0.97rem;
}
.ckp-abstract-label {
  font-family: var(--font-mono);
  font-size: 0.65rem; letter-spacing: 0.2em;
  text-transform: uppercase; color: var(--accent);
  margin-bottom: 0.8rem;
}
.ckp-abstract p { margin: 0; color: var(--text-muted); font-style: italic; }

/* ─── Callouts ────────────────────────────────────────────────── */
.ckp-callout {
  background: var(--surface);
  border: 1px solid var(--border);
  border-left: 3px solid var(--blue);
  padding: 1.2rem 1.5rem;
  margin: 2rem 0;
  font-size: 0.94rem;
}
.ckp-callout.warn { border-left-color: var(--amber); }
.ckp-callout.key  { border-left-color: var(--green); }
.ckp-callout.bad  { border-left-color: var(--red); }
.ckp-callout p:last-child { margin-bottom: 0; }
.ckp-callout strong:first-child {
  font-family: var(--font-mono);
  font-size: 0.68rem; letter-spacing: 0.14em;
  text-transform: uppercase; color: var(--blue);
  display: block; margin-bottom: 0.5rem;
}
.ckp-callout.warn strong:first-child { color: var(--amber); }
.ckp-callout.key  strong:first-child { color: var(--green); }
.ckp-callout.bad  strong:first-child { color: var(--red); }

/* ─── Hierarchy list ──────────────────────────────────────────── */
.ckp-hier { margin: 1.6rem 0; padding: 0; list-style: none; }
.ckp-hier li {
  display: flex; gap: 1rem; align-items: flex-start;
  padding: 0.8rem 1rem;
  border-bottom: 1px solid var(--border);
  font-size: 0.95rem;
}
.ckp-hier li:first-child { border-top: 1px solid var(--border); }
.ckp-hier li::before {
  content: '▸'; color: var(--accent); font-size: 0.75rem;
  margin-top: 0.35rem; flex-shrink: 0;
}

/* ─── Stats ───────────────────────────────────────────────────── */
.ckp-stat-row {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 1px; background: var(--border);
  border: 1px solid var(--border);
  margin: 2rem 0;
}
.ckp-stat { background: var(--surface); padding: 1.2rem 1.2rem; text-align: center; }
.ckp-stat .stat-num {
  font-family: var(--font-display);
  font-size: 1.9rem; font-weight: 700;
  color: var(--accent); line-height: 1; display: block;
}
.ckp-stat .stat-label {
  font-family: var(--font-mono);
  font-size: 0.62rem; letter-spacing: 0.1em;
  text-transform: uppercase; color: var(--text-muted);
  margin-top: 0.4rem; display: block; line-height: 1.45;
}

/* ─── Numbered steps ──────────────────────────────────────────── */
.ckp-chain { margin: 2rem 0; }
.ckp-chain-item {
  display: grid; grid-template-columns: 44px 1fr; gap: 1rem;
  margin-bottom: 1.6rem; align-items: start;
}
.ckp-chain-num {
  width: 44px; height: 44px;
  border: 2px solid var(--accent);
  display: flex; align-items: center; justify-content: center;
  font-family: var(--font-mono); font-weight: 600; font-size: 0.85rem;
  color: var(--accent); flex-shrink: 0; background: var(--accent-dim);
}
.ckp-chain-content h4 {
  font-family: var(--font-display);
  font-size: 1.03rem; font-weight: 700; color: #f0f0f0;
  margin: 0.45rem 0 0.4rem;
}
.ckp-chain-content p { margin: 0; font-size: 0.92rem; color: var(--text-muted); }

/* ─── Tables ──────────────────────────────────────────────────── */
.ckp-table-wrap { overflow-x: auto; margin: 2rem -0.5rem; -webkit-overflow-scrolling: touch; }
.ckp-table { width: 100%; min-width: 480px; border-collapse: collapse; font-size: 0.86rem; }
.ckp-table thead tr { background: var(--surface2); }
.ckp-table th {
  font-family: var(--font-mono);
  font-size: 0.65rem; letter-spacing: 0.12em; text-transform: uppercase;
  color: var(--text-muted); padding: 0.8rem 1rem; text-align: left;
  border-bottom: 2px solid var(--accent); white-space: nowrap;
}
.ckp-table td {
  padding: 0.8rem 1rem; border-bottom: 1px solid var(--border);
  vertical-align: top; color: var(--text); line-height: 1.5;
}
.ckp-table tr:hover td { background: var(--surface); }
.ckp-table .term { font-family: var(--font-display); font-weight: 700; color: #f0f0f0; }

.ckp-pill {
  font-family: var(--font-mono);
  font-size: 0.6rem; letter-spacing: 0.1em; text-transform: uppercase;
  padding: 0.18rem 0.5rem; border: 1px solid; white-space: nowrap;
  display: inline-block; line-height: 1.4;
}
.ckp-pill.ok      { color: var(--green); border-color: rgba(109,207,148,0.45); background: rgba(109,207,148,0.08); }
.ckp-pill.partial { color: var(--amber); border-color: rgba(224,147,92,0.45);  background: rgba(224,147,92,0.08); }
.ckp-pill.no      { color: var(--red);   border-color: rgba(224,92,92,0.45);   background: rgba(224,92,92,0.08); }

/* ─── Diagram ─────────────────────────────────────────────────── */
.ckp-diagram {
  margin: 2rem 0;
  background: var(--surface);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
}
.ckp-diagram-head {
  padding: 0.6rem 1rem;
  border-bottom: 1px solid var(--border);
  background: var(--surface2);
  font-family: var(--font-mono);
  font-size: 0.62rem; letter-spacing: 0.15em;
  text-transform: uppercase; color: var(--text-muted);
}
.ckp-diagram pre {
  margin: 0; padding: 1.1rem 1.2rem;
  line-height: 1.28; overflow-x: auto;
  background: none; border: none;
  -webkit-overflow-scrolling: touch;
}
.ckp-diagram code {
  font-family: var(--font-mono);
  font-size: 0.74rem; color: var(--text);
  white-space: pre; background: none; padding: 0;
}
@media (max-width: 600px) { .ckp-diagram code { font-size: 0.62rem; } }
.ckp-body p code, .ckp-body li code {
  font-family: var(--font-mono); font-size: 0.86em;
  color: var(--blue); background: var(--surface2);
  padding: 0.08em 0.35em; border: 1px solid var(--border);
}

/* ─── Separator ───────────────────────────────────────────────── */
.ckp-sep {
  display: flex; align-items: center; gap: 1rem; margin: 3rem 0;
  font-family: var(--font-mono); font-size: 0.7rem;
  letter-spacing: 0.2em; text-transform: uppercase; color: var(--text-muted);
}
.ckp-sep::before, .ckp-sep::after {
  content: ''; flex: 1; height: 1px; background: var(--border);
}

/* ─── Further reading ─────────────────────────────────────────── */
.ckp-further {
  background: var(--surface);
  border: 1px solid var(--border);
  border-top: 3px solid var(--accent);
  padding: 1.5rem 1.8rem;
  margin: 3rem 0 0;
}
.ckp-further-label {
  font-family: var(--font-mono);
  font-size: 0.65rem; letter-spacing: 0.2em;
  text-transform: uppercase; color: var(--accent);
  margin-bottom: 0.7rem;
}
.ckp-further p { margin: 0; font-size: 0.94rem; color: var(--text-muted); }

/* ─── References ──────────────────────────────────────────────── */
.ckp-refs {
  margin-top: 3rem; padding-top: 1.5rem;
  border-top: 1px solid var(--border);
  font-size: 0.82rem; color: var(--text-muted);
}
.ckp-refs h2 { font-size: 1rem; margin-bottom: 1rem; border: none; padding: 0; }
.ckp-refs p { margin: 0 0 0.7rem; line-height: 1.5; }
.ckp-refs .ref-num { color: var(--accent); font-family: var(--font-mono); font-size: 0.7rem; }
.ckp-refs a { color: var(--text-muted); border-bottom: 1px dotted var(--border); text-decoration: none; word-break: break-word; }
.ckp-refs a:hover { color: var(--accent); }

/* ─── Keywords ────────────────────────────────────────────────── */
.ckp-keywords { display: flex; flex-wrap: wrap; gap: 0.5rem; margin: 1.5rem 0 0; }
.ckp-kw {
  font-family: var(--font-mono); font-size: 0.68rem; letter-spacing: 0.08em;
  background: var(--surface2); border: 1px solid var(--border);
  color: var(--text-muted); padding: 0.25rem 0.7rem;
}

/* ─── Back to top ─────────────────────────────────────────────── */
#ckp-top {
  position: fixed; right: 1.4rem; bottom: 1.4rem;
  width: 40px; height: 40px;
  border: 1px solid #383840; background: #242428; color: #c9a84c;
  font-family: 'JetBrains Mono', monospace; font-size: 0.9rem;
  cursor: pointer; display: flex; align-items: center; justify-content: center;
  opacity: 0; pointer-events: none;
  transition: opacity 0.25s, border-color 0.2s; z-index: 9998;
}
#ckp-top.show { opacity: 1; pointer-events: auto; }
#ckp-top:hover { border-color: #c9a84c; }

/* ─── Animation ───────────────────────────────────────────────── */
@keyframes ckp-fade-in {
  from { opacity: 0; transform: translateY(16px); }
  to   { opacity: 1; transform: translateY(0); }
}
.ckp-hero     { animation: ckp-fade-in 0.6s ease both; }
.ckp-abstract { animation: ckp-fade-in 0.6s ease 0.15s both; }
@media (prefers-reduced-motion: reduce) {
  .ckp-hero, .ckp-abstract { animation: none; }
  #ckp-progress { transition: none; }
}

/* ─── Print ───────────────────────────────────────────────────── */
@media print {
  #ckp-progress, #ckp-top { display: none !important; }
  .ckp-article { color: #000; font-size: 10.5pt; line-height: 1.5; }
  .ckp-hero h1, .ckp-body h2, .ckp-body h3 { color: #000; }
  .ckp-abstract, .ckp-callout, .ckp-diagram, .ckp-stat, .ckp-further {
    background: #fff !important; border-color: #999 !important;
  }
  .ckp-body h2 { page-break-after: avoid; }
  .ckp-diagram, .ckp-table, .ckp-callout, .ckp-pull { page-break-inside: avoid; }
  .ckp-table td, .ckp-table th { color: #000; }
}
</style>

<div id="ckp-progress"></div>
<button id="ckp-top" aria-label="Back to top">↑</button>

<article class="ckp-article">

<div class="ckp-hero">
  <div class="ckp-kicker">Privacy · How the Ad Industry Works · Why It Matters</div>
  <h1>Nobody Needs to <em>Hack</em> Your Phone</h1>
  <p class="ckp-deck">Following someone used to require a warrant, a van, or a skilled intruder. Now it mostly requires a credit card. Here is how ordinary apps came to produce a map of your life, why calling that data "anonymous" is a technicality, and what can actually be done about it.</p>
  <div class="ckp-meta">
    <span>Sara Malik &amp; Naveed A. Aun</span>
    <span class="dot"></span>
    <span>~15 min read</span>
    <span class="dot"></span>
    <span><a href="mailto:smk@pakcrypt.org">smk@pakcrypt.org</a></span>
  </div>
  <div class="ckp-keywords">
    <span class="ckp-kw">Location Data</span>
    <span class="ckp-kw">Data Brokers</span>
    <span class="ckp-kw">Advertising ID</span>
    <span class="ckp-kw">Pattern of Life</span>
    <span class="ckp-kw">Mobile Privacy</span>
  </div>
</div>

<div class="ckp-body">

<div class="ckp-abstract">
  <div class="ckp-abstract-label">In short</div>
  <p>The apps on an ordinary phone generate a stream of small, boring records — an app opened, a location fixed, an advert requested. Individually they are nothing. Stacked up over weeks, they describe where you sleep, where you work, who you travel with and when your routine changes. That stream is a legitimate industry, it is bought and sold, and in 2026 the US military confirmed it had switched off part of it on government phones because adversaries were using it to find soldiers.</p>
</div>

<section id="sec-week">
<h2>What a week looks like from the outside</h2>

<p class="drop-cap">Imagine a list. Every row has four things: a long random-looking code, a pair of coordinates, a timestamp, and the name of whichever app happened to be open. There are a few hundred rows for a given phone in a given week. Nothing in the list is a name, an address, a photograph or a message.</p>

<p>Now sort the rows by that random code and plot them on a map.</p>

<p>The place the code sits still between midnight and six in the morning is, almost always, where that person sleeps. The place it sits between nine and five on weekdays is where they work. A second code that appears at the same two places at the same times probably belongs to someone in the same household. A code that travels the same route as yours every Tuesday evening belongs to whoever you go to the gym with.</p>

<p>You did not have to be identified for any of that to be true. The map was drawn entirely from records that contained no name at all.</p>

<div class="ckp-pull">
  <p>Nobody read your messages. Nobody planted anything. The information was produced by your phone working exactly as intended, and sold by companies operating entirely within the law.</p>
  <cite>The uncomfortable part</cite>
</div>

<p>This is the thing that people consistently underestimate about location data. The privacy risk is not in any single record. It is in the fact that human beings are extraordinarily regular, and regularity is easy to detect. You do not need to know much about a person to recognise them by their routine. The routine <em>is</em> the identifier.</p>
</section>

<div class="ckp-sep">How It Happens</div>

<section id="sec-how">
<h2>How your phone came to be a data source</h2>

<p>Almost no app makes money by being an app. Free apps make money by showing adverts, and showing the <em>right</em> advert to the right person is worth many times more than showing a random one. So an industry grew up to answer one question very fast: who is this, roughly, and what are they likely to want?</p>

<p>To answer it, the industry needed three things. A way to recognise the same phone across different apps. Some context about what that phone is doing. And a market where advertisers could bid for the chance to reach it.</p>

<h3>The identifier</h3>

<p>Every Android phone has an <strong>advertising ID</strong> — a long code that apps can read. Apple has an equivalent. It is deliberately not your name; it is resettable, and you can switch it off. Its whole purpose is to let unrelated companies agree that "the phone that did this" and "the phone that did that" are the same phone, without any of them knowing who you are.</p>

<p>That sounds like a privacy feature, and in a narrow sense it is. But a stable code that links your behaviour across every app you use is exactly what is needed to build the map described above. Anonymity that survives being followed around for a year is not really anonymity.</p>

<h3>The context</h3>

<p>Apps collect what they are permitted to collect. A maps app that has location permission genuinely needs it. The wrinkle is that advertising code doesn't live outside the app — it is a library bundled <em>inside</em> it, and the phone cannot tell the two apart.</p>

<div class="ckp-callout">
  <strong>Why "app permissions" don't work the way you'd expect</strong>
  <p>When you grant an app access to your location, you are granting it to everything inside that app — including the advertising and analytics libraries the developer included. Android has no way to say "the weather feature may use my location, but the ad library bundled into it may not." They share one identity as far as the operating system is concerned. This is not a bug someone forgot to fix; it is a consequence of how apps are built and packaged.</p>
</div>

<h3>The auction</h3>

<p>Here is the part most people have never heard of, and it is the part that matters most.</p>

<p>When an app displays an advert, it does not simply fetch one. It runs an auction, in about a tenth of a second. A description of the opportunity — roughly what kind of phone this is, roughly where it is, what app is open, and often that advertising ID — is broadcast to a large number of potential buyers, who bid. One wins and their advert appears.</p>

<div class="ckp-diagram">
  <div class="ckp-diagram-head">How one advert slot becomes many copies of your data</div>
<pre><code>      your phone opens an app
                 |
                 v
 "ad slot available" + device context
                 |
                 v
            AD EXCHANGE
                 |
      +------+------+------+------+
      |      |      |      |      |
      v      v      v      v      v
   bidder bidder bidder bidder bidder    ... often dozens
      |
      +--&gt; one wins, shows you an advert
           the others saw your data anyway</code></pre>
</div>

<p>Everyone who was invited to bid saw the description. Only one of them needed it. There is no technical mechanism that stops the losers keeping a copy.</p>

<p>This is not theoretical. In a 2024 enforcement action, US regulators found that one company had been bidding in these auctions and retaining the data from auctions it <em>lost</em> — accumulating more than 500 million unique advertising IDs paired with precise location over roughly two and a half years <a href="#ref-ftc">[1]</a>. Participating in the marketplace was itself the collection method.</p>

<div class="ckp-stat-row">
  <div class="ckp-stat"><span class="stat-num">500M+</span><span class="stat-label">Device IDs with precise location, one company, one case</span></div>
  <div class="ckp-stat"><span class="stat-num">~0.1s</span><span class="stat-label">Time an ad auction takes</span></div>
  <div class="ckp-stat"><span class="stat-num">1</span><span class="stat-label">Bidders who actually needed your data</span></div>
</div>
</section>

<div class="ckp-sep">The Anonymity Question</div>

<section id="sec-anon">
<h2>"But it's anonymous"</h2>

<p>This is the industry's standard answer, and it is worth taking seriously rather than dismissing, because it is not a straightforward lie. The records really do not contain your name. The companies involved often genuinely do not know who you are and have no particular interest in finding out.</p>

<p>The problem is that "does not contain a name" and "cannot be connected to a person" are very different claims, and only the first one is true.</p>

<ul class="ckp-hier">
  <li><strong>Your home address identifies you.</strong> The place a device rests overnight, cross-referenced against any public record of who lives there, is a name.</li>
  <li><strong>You log in to things.</strong> The moment a service knows both your account and your device, the "anonymous" code has a person attached to it — and that link can be shared onward.</li>
  <li><strong>Resetting the ID doesn't erase history.</strong> It starts a new chapter; it does not delete the old one, and companies specifically build systems to bridge across resets.</li>
  <li><strong>Other identifiers survive.</strong> Individual apps keep their own internal codes, which are unaffected by anything you do to the advertising ID.</li>
</ul>

<p>US regulators have stated the point plainly in enforcement actions: raw location data tied to an advertising ID is not anonymised, and can be used to trace a device to the places its user visited <a href="#ref-ftc">[1]</a>.</p>

<div class="ckp-callout warn">
  <strong>One thing that is <em>not</em> happening</strong>
  <p>Your phone is almost certainly not secretly listening to your conversations through the microphone to target adverts. This is the single most common belief about ad tracking and there is no good public evidence for it. It would be enormously expensive, legally catastrophic if discovered, and — crucially — <em>unnecessary</em>. Everything described in this article explains the eerily accurate advert perfectly well without it. If you mentioned a holiday out loud and then saw a holiday advert, the likelier explanation is that you, or someone whose network and routine you share, searched for it.</p>
  <p>This matters beyond trivia. Believing in the microphone makes the real mechanism harder to see, and the real mechanism is worse: it is continuous, it is documented, and it is legal.</p>
</div>
</section>

<div class="ckp-sep">Where It Stops Being About Adverts</div>

<section id="sec-military">
<h2>The moment this became a security problem</h2>

<p>Everything above is a consumer privacy story. It became something else when people noticed that the same market is open to anyone with money — including governments, and including hostile ones.</p>

<p>Consider what the data shows if the phone in question belongs to a soldier. The overnight location is their home, which puts their family on a map. The weekday location is their base. A cluster of devices that move from that base to an airfield and then stop appearing is a deployment. Devices that always travel together are a unit. None of this requires knowing a single name.</p>

<p>In September 2026, correspondence released by two members of the US Congress confirmed that the Army, the Air Force, the Department of the Navy and Special Operations Command had each disabled the advertising identifier on government-issued phones and computers <a href="#ref-mil">[2]</a>. The changes followed reporting that commercially available location data had been used to track and target American personnel in the Middle East. Some branches had only made the change months earlier.</p>

<p>The legislators who released the letters did not treat it as a success story. They asked the Department of Defense's Inspector General to examine whether the measures were effective at all, and said publicly that they were not.</p>

<div class="ckp-pull">
  <p>An adversary who wants to follow a soldier no longer needs an intelligence service. It needs a corporate identity and a purchase order.</p>
  <cite>Why this is different from ordinary surveillance</cite>
</div>

<p>There is a broader point here that applies well beyond the military. Regulators have documented data products built around visits to health clinics, places of worship, political gatherings and domestic violence shelters. In February 2026 the US Federal Trade Commission wrote to thirteen data brokers about a law restricting sales of sensitive data to foreign adversaries, noting that it had found companies offering products involving whether an individual is a member of the armed forces <a href="#ref-padfaa">[3]</a>.</p>

<p>If your routine reveals something about you that you would rather not advertise — a medical condition, a faith, a relationship, a political commitment, a job — then it is already in the same pipeline, described by the same coordinates, sold on the same terms.</p>
</section>

<div class="ckp-sep">What Helps</div>

<section id="sec-doesnt">
<h2>The half-measures, honestly rated</h2>

<p>Before the things that work, the things that mostly don't — because a false sense of protection is worse than none.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead><tr><th>Measure</th><th>Verdict</th><th>What it actually does</th></tr></thead>
<tbody>
<tr>
  <td><span class="term">Resetting your advertising ID</span></td>
  <td><span class="ckp-pill partial">Partial</span></td>
  <td>Breaks the chain going forward. Doesn't delete what exists, and doesn't touch the separate codes each app keeps internally.</td>
</tr>
<tr>
  <td><span class="term">A consumer VPN</span></td>
  <td><span class="ckp-pill no">Largely no</span></td>
  <td>Hides your network address from websites and your browsing from your ISP. Does nothing about an app that has your GPS location and sends it to its own servers. Most of the tracking described here passes straight through a VPN untouched.</td>
</tr>
<tr>
  <td><span class="term">Private / incognito browsing</span></td>
  <td><span class="ckp-pill no">No</span></td>
  <td>Affects browser history on your own device. Irrelevant to apps.</td>
</tr>
<tr>
  <td><span class="term">Ad blockers</span></td>
  <td><span class="ckp-pill partial">Partial</span></td>
  <td>Effective in a browser. Much weaker inside apps, and blocks nothing when an app sends your data to its own servers first and passes it on afterwards.</td>
</tr>
<tr>
  <td><span class="term">"I have nothing to hide"</span></td>
  <td><span class="ckp-pill no">No</span></td>
  <td>The data does not describe what you're hiding. It describes where you are, on a schedule, forever. Whether that's harmless depends entirely on who buys it and why — which you don't control.</td>
</tr>
</tbody>
</table>
</div>

<p>None of these are useless. They are just aimed at different problems from the one described in this article.</p>
</section>

<section id="sec-you">
<h2>What actually helps — if you're a person</h2>

<p>The realistic goal is not invisibility. It is reducing how many companies receive a usable copy of your routine, and how easily those copies can be joined together. That is achievable, and the highest-value actions are unglamorous.</p>

<div class="ckp-chain">
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">01</div>
    <div class="ckp-chain-content">
      <h4>Cut the number of apps</h4>
      <p>The single most effective step, and the one nobody wants to hear. Every app is a separate company with separate commercial incentives. Deleting the free game you play twice a year removes an entire data source permanently. Fewer apps beats better settings.</p>
    </div>
  </div>
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">02</div>
    <div class="ckp-chain-content">
      <h4>Be strict about location, and especially background location</h4>
      <p>Most apps that ask for your location do not need it, and very few need it while closed. Modern phones let you grant location only while an app is open, or grant an approximate area instead of a precise point. Background location is the setting that produces the overnight-and-weekday map. Give it to almost nothing.</p>
    </div>
  </div>
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">03</div>
    <div class="ckp-chain-content">
      <h4>Turn off the advertising ID</h4>
      <p>Both major phone platforms let you delete or disable it outright, not merely reset it. It is a genuine improvement, it takes a minute, and it costs you nothing except less relevant adverts. Just don't mistake it for a solution on its own.</p>
    </div>
  </div>
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">04</div>
    <div class="ckp-chain-content">
      <h4>Prefer apps you pay for</h4>
      <p>An app with no advertising business model has far less reason to carry tracking libraries. Paying a few currency units for a weather or notes app is often the cheapest privacy measure available.</p>
    </div>
  </div>
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">05</div>
    <div class="ckp-chain-content">
      <h4>Use a browser instead of the app, where you can</h4>
      <p>A website generally sees much less about your device than the same company's app does, and browser defences against tracking are considerably more mature than anything available inside apps.</p>
    </div>
  </div>
  <div class="ckp-chain-item">
    <div class="ckp-chain-num">06</div>
    <div class="ckp-chain-content">
      <h4>Keep the phone updated, and buy one that gets updates</h4>
      <p>Not strictly about advertising — but every restriction described here only exists because the platform enforces it, and those enforcement mechanisms arrive in updates. A phone that stopped receiving them is a phone where the old rules still apply.</p>
    </div>
  </div>
</div>

<div class="ckp-callout key">
  <strong>What you're actually achieving</strong>
  <p>Do all of this and you are still visible to your mobile network, to the services you log in to, and to any app you decided you needed. What you have removed is the long tail: the dozen incidental apps quietly contributing rows to a shared map of your week. That's a real reduction, and it's the part you control.</p>
</div>
</section>

<section id="sec-org">
<h2>What actually helps — if you run an organisation</h2>

<p>For a company, a government department or anyone responsible for other people's phones, the individual advice does not scale and settings that users can change are not controls. The approach that works is different in kind, and it comes down to four ideas.</p>

<div class="ckp-table-wrap">
<table class="ckp-table">
<thead><tr><th>Idea</th><th>In practice</th></tr></thead>
<tbody>
<tr>
  <td><span class="term">Decide what may run</span></td>
  <td>On a managed phone, the organisation chooses the apps, not the user. Every app is a separate company receiving data, so the list of approved apps <em>is</em> the list of companies you've decided to trust. Keeping it short does more than any filtering technology.</td>
</tr>
<tr>
  <td><span class="term">Decide what it may reach</span></td>
  <td>Sensitive permissions — location, microphone, contacts — granted deliberately per app rather than left to whoever taps "Allow", and identifiers switched off centrally rather than hopefully.</td>
</tr>
<tr>
  <td><span class="term">Decide where it may talk</span></td>
  <td>Route the phone's traffic through infrastructure the organisation controls, so an approved app can only reach destinations it has a documented reason to reach. This is the layer that catches apps behaving unexpectedly.</td>
</tr>
<tr>
  <td><span class="term">Check, then keep checking</span></td>
  <td>Before an app is approved, run it in a test environment and watch where it actually sends data — which is often not what its documentation says. Then repeat it for every update, because behaviour changes between versions.</td>
</tr>
</tbody>
</table>
</div>

<p>That last one is the least popular and the most important. Approving "the mapping app" is meaningless; approving <em>a specific version</em> of it, having watched what it does, is a real control. It is also the only part of this that addresses the hardest case: an approved app that legitimately sends data to its own servers, where the company later sells it on. No technology on the phone can see that happen. The only defences are choosing the app carefully, negotiating a version without the tracking, or writing it into the contract.</p>

<div class="ckp-callout bad">
  <strong>Two things to be sceptical of</strong>
  <p><strong>Products that promise you cannot be tracked.</strong> None of this makes a phone untraceable. The mobile network necessarily knows roughly where every phone is — that is how calls reach you — and no app-level measure changes that. A vendor claiming otherwise is either confused or selling.</p>
  <p><strong>Solutions that are only a blocklist.</strong> Blocking known tracking servers is worth doing and is not a strategy. It cannot help when an app sends data to its own perfectly legitimate servers and the onward sale happens later, somewhere you cannot see.</p>
</div>
</section>

<div class="ckp-sep">Where This Leaves Us</div>

<section id="sec-end">
<h2>The honest ending</h2>

<p>There is a version of this article that ends with a reassuring checklist, and it would be dishonest. So here is the accurate version.</p>

<p>You cannot opt out of this entirely while carrying a phone. The mobile network knows where you are by design. The services you log in to know it's you because you told them. Data already collected is not recalled by a setting you change today, and it does not expire quickly.</p>

<p>What you <em>can</em> do is change the scale. The difference between a phone with forty apps, most of them free and permission-hungry, and a phone with twelve, chosen deliberately, with location off by default and the advertising ID disabled, is not a rounding error. It is the difference between contributing a detailed weekly map to a dozen commercial datasets and contributing fragments to one or two.</p>

<div class="ckp-pull">
  <p>This is not a problem you solve. It is a problem you reduce, deliberately, knowing what you're trading and what you're keeping.</p>
  <cite>The realistic goal</cite>
</div>

<p>And the broader point is not really about settings at all. A market exists in which anyone with money can buy a detailed record of where large numbers of people have been. That market was built to sell trainers and takeaways. It turns out to work just as well for finding soldiers, identifying who attended a protest, or working out which building an unmarked facility occupies — and it was never designed with any of that in mind.</p>

<p>That is a policy problem, not a phone-settings problem. But it is much easier to argue about once you know it exists, which is the entire reason this article is not shorter.</p>
</section>

<div class="ckp-further">
  <div class="ckp-further-label">Further reading</div>
  <p>A full technical treatment of this subject — the complete catalogue of signals a phone emits, the routes data takes off the device, an evaluated reference architecture for organisations, and the verification tests required before anyone claims it works — is published separately as <a href="/articles/android-tracking/">Bought, Not Hacked</a>. It is written for engineers and assumes familiarity with mobile platform internals.</p>
</div>

<div class="ckp-refs" id="references">
<h2>Sources</h2>

<p id="ref-ftc"><span class="ref-num">[1]</span> US Federal Trade Commission, <em>FTC Takes Action Against Mobilewalla for Collecting and Selling Sensitive Location Data</em> (December 2024) — the source for the 500 million figure, for data being retained from lost auctions, and for the finding that location data tied to advertising IDs is not anonymised. <a href="https://www.ftc.gov/news-events/news/press-releases/2024/12/ftc-takes-action-against-mobilewalla-collecting-selling-sensitive-location-data">ftc.gov</a>. See also the FTC's own explainer on how real-time bidding works: <a href="https://www.ftc.gov/policy/advocacy-research/tech-at-ftc/2024/12/unpacking-real-time-bidding-through-ftcs-case-mobilewalla">Unpacking Real Time Bidding</a>.</p>

<p id="ref-mil"><span class="ref-num">[2]</span> Reuters, reporting on correspondence released by Sen. Ron Wyden and Rep. Pat Harrigan, 4–5 September 2026, confirming that US military branches disabled advertising identifiers on government devices and requesting an Inspector General review. Widely syndicated; an accessible account is at <a href="https://taskandpurpose.com/news/military-cybersecurity-ad-trackers-iran/">Task &amp; Purpose</a>.</p>

<p id="ref-padfaa"><span class="ref-num">[3]</span> US Federal Trade Commission, <em>FTC Reminds Data Brokers of Their Obligations to Comply with PADFAA</em> (February 2026), and the accompanying <a href="https://www.ftc.gov/legal-library/browse/warning-letters/protecting-americans-data-foreign-adversaries-act-padfaa-warning-letter-template">warning letter template</a>, which references products involving armed-forces status. <a href="https://www.ftc.gov/news-events/news/press-releases/2026/02/ftc-reminds-data-brokers-their-obligations-comply-padfaa">ftc.gov</a></p>

<p style="margin-top:1.4rem; padding-top:1rem; border-top:1px solid var(--border); font-style:italic;">Corrections are welcome and will be published rather than quietly applied: <a href="mailto:smk@pakcrypt.org">smk@pakcrypt.org</a></p>
</div>

</div><!-- end .ckp-body -->
</article>

<script>
(function() {
  var bar = document.getElementById('ckp-progress');
  function updateProgress() {
    var scrolled = window.scrollY || window.pageYOffset;
    var total = document.documentElement.scrollHeight - window.innerHeight;
    bar.style.width = total > 0 ? (scrolled / total * 100) + '%' : '0%';
  }
  window.addEventListener('scroll', updateProgress, { passive: true });
  updateProgress();

  var topBtn = document.getElementById('ckp-top');
  if (topBtn) {
    topBtn.addEventListener('click', function() {
      window.scrollTo({ top: 0, behavior: 'smooth' });
    });
    window.addEventListener('scroll', function() {
      topBtn.classList.toggle('show', (window.scrollY || window.pageYOffset) > 600);
    }, { passive: true });
  }
})();
</script>
