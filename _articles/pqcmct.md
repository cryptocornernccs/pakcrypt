---
layout: post
title: "On PQC Certificates"
math: true
---

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no, viewport-fit=cover">
<title>Uncharted Territory of PQC: Quantum Certificates</title>
<meta name="description" content="A field briefing on post-quantum TLS, certificate size, Merkle Tree Certificates, and the fork forming between the Web PKI and private PKI.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:ital,wght@0,400;0,500;0,600;0,700;1,400;1,600&family=IBM+Plex+Mono:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#fafafa;
    --surface:#ffffff;
    --border:#e4e4e9;
    --border-soft:#ececf0;
    --ink:#1b1b1e;
    --muted:#6b6b74;
    --muted-2:#9a9aa2;
    --accent:#1f6f6d;
    --accent-dark:#154f4d;
    --accent-soft:#e7f3f2;
    --accent-soft-2:#f1f8f7;
    --warn-bg:#f7f7f7;
    --mono-bg:#f5f5f7;
    --radius:10px;
    --maxw:740px;
  }
  *{box-sizing:border-box;}
  html{-webkit-text-size-adjust:100%;}
  body{
    margin:0;
    background:var(--bg);
    color:var(--ink);
    font-family:'IBM Plex Sans', system-ui, -apple-system, 'Segoe UI', Roboto, sans-serif;
    font-size:17px;
    line-height:1.65;
    -webkit-font-smoothing:antialiased;
  }
  a{color:var(--accent-dark); text-decoration:none; border-bottom:1px solid var(--accent-soft);}
  a:hover{border-bottom-color:var(--accent-dark);}
  .mono{font-family:'IBM Plex Mono', ui-monospace, SFMono-Regular, Menlo, monospace;}
  code{
    font-family:'IBM Plex Mono', ui-monospace, monospace;
    font-size:0.88em;
    background:var(--mono-bg);
    border:1px solid var(--border-soft);
    border-radius:4px;
    padding:0.1em 0.35em;
  }
  pre{
    font-family:'IBM Plex Mono', ui-monospace, monospace;
    font-size:0.85rem;
    line-height:1.6;
    background:var(--mono-bg);
    border:1px solid var(--border);
    border-radius:var(--radius);
    padding:1.1rem 1.25rem;
    overflow-x:auto;
    color:#26262b;
  }
  pre code{background:none;border:none;padding:0;font-size:1em;}

  /* ---------- shell ---------- */
  .topbar{
    background:var(--ink);
    color:#cfcfd2;
    font-size:0.78rem;
    letter-spacing:0.04em;
    text-align:center;
    padding:0.55rem 1rem;
  }
  .topbar strong{color:#fff; font-weight:600;}
  .wrap{
    max-width:var(--maxw);
    margin:0 auto;
    padding:0 1.25rem;
  }

  /* ---------- masthead ---------- */
  .masthead{padding:3rem 0 1.6rem;}
  .kicker{
    font-family:'IBM Plex Mono', monospace;
    text-transform:uppercase;
    letter-spacing:0.12em;
    font-size:0.74rem;
    color:var(--accent-dark);
    font-weight:600;
    margin-bottom:0.9rem;
  }
  h1{
    font-size:2.05rem;
    line-height:1.2;
    margin:0 0 1rem;
    font-weight:700;
    letter-spacing:-0.01em;
  }
  h1 em{font-style:italic; color:var(--accent-dark); font-weight:600;}
  .dek{
    font-size:1.08rem;
    color:#3c3c42;
    margin:0 0 1.4rem;
    max-width:640px;
  }
  .byline{
    font-size:0.9rem;
    color:var(--muted);
    margin:0 0 1.1rem;
  }
  .byline strong{color:var(--ink);}
  .badge-row{
    display:flex;
    gap:0.6rem;
    flex-wrap:wrap;
    align-items:center;
    font-size:0.82rem;
    color:var(--muted);
    background:var(--accent-soft-2);
    border:1px solid var(--border-soft);
    border-radius:8px;
    padding:0.55rem 0.9rem;
    margin:0 0 1.2rem;
  }
  .badge-row .sep{color:var(--muted-2);}
  .tag-row{display:flex; gap:0.5rem; flex-wrap:wrap; margin-bottom:0.4rem;}
  .tag{
    font-family:'IBM Plex Mono', monospace;
    font-size:0.72rem;
    color:var(--accent-dark);
    background:var(--accent-soft);
    border:1px solid #d7e8e6;
    border-radius:999px;
    padding:0.28rem 0.7rem;
    white-space:nowrap;
  }

  /* ---------- table of contents ---------- */
  details.toc{
    margin:1.8rem 0 2.4rem;
    border:1px solid var(--border);
    border-radius:var(--radius);
    background:var(--surface);
  }
  details.toc summary{
    cursor:pointer;
    list-style:none;
    padding:0.85rem 1.1rem;
    font-weight:600;
    font-size:0.95rem;
    display:flex;
    align-items:center;
    justify-content:space-between;
  }
  details.toc summary::-webkit-details-marker{display:none;}
  details.toc summary::after{content:"+"; color:var(--accent-dark); font-weight:700; font-size:1.1rem;}
  details.toc[open] summary::after{content:"–";}
  .toc-list{
    margin:0;
    padding:0 1.1rem 1.1rem 1.1rem;
    list-style:none;
    border-top:1px solid var(--border-soft);
    padding-top:0.7rem;
  }
  .toc-list li{
    counter-increment:toc;
    padding:0.32rem 0;
    font-size:0.93rem;
  }
  .toc-list{counter-reset:toc;}
  .toc-list li::before{
    content: counter(toc) ".";
    font-family:'IBM Plex Mono', monospace;
    color:var(--muted-2);
    margin-right:0.5rem;
    font-size:0.85rem;
  }
  .toc-list a{border-bottom:none; color:var(--ink);}
  .toc-list a:hover{color:var(--accent-dark);}

  /* ---------- abstract ---------- */
  .abstract{
    background:var(--surface);
    border:1px solid var(--border);
    border-radius:var(--radius);
    padding:1.4rem 1.5rem;
    margin:0 0 2rem;
  }
  .abstract .label{
    font-family:'IBM Plex Mono', monospace;
    text-transform:uppercase;
    letter-spacing:0.1em;
    font-size:0.72rem;
    color:var(--muted);
    margin-bottom:0.7rem;
    font-weight:600;
  }
  .abstract p{margin:0 0 0.9rem;}
  .abstract p:last-child{margin-bottom:0;}
  .abstract .pull{
    font-style:italic;
    color:#3c3c42;
    border-left:2px solid var(--accent);
    padding-left:0.9rem;
  }

  /* ---------- stat grid ---------- */
  .stat-grid{
    display:grid;
    grid-template-columns:repeat(4, 1fr);
    gap:0.8rem;
    margin:0 0 2.4rem;
  }
  .stat-card{
    background:var(--surface);
    border:1px solid var(--border);
    border-radius:var(--radius);
    padding:1rem 0.9rem;
    text-align:left;
  }
  .stat-value{
    font-family:'IBM Plex Mono', monospace;
    font-size:1.35rem;
    font-weight:600;
    color:var(--accent-dark);
    display:block;
    margin-bottom:0.3rem;
  }
  .stat-label{
    font-size:0.76rem;
    color:var(--muted);
    line-height:1.3;
  }

  /* ---------- article sections ---------- */
  article{padding-bottom:2rem;}
  section{margin:2.6rem 0;}
  section > .eyebrow{
    font-family:'IBM Plex Mono', monospace;
    text-transform:uppercase;
    letter-spacing:0.12em;
    font-size:0.72rem;
    color:var(--accent-dark);
    font-weight:600;
    margin-bottom:0.5rem;
  }
  h2{
    font-size:1.5rem;
    line-height:1.3;
    margin:0 0 1.1rem;
    padding-bottom:0.7rem;
    border-bottom:1px solid var(--border);
    scroll-margin-top:1.5rem;
  }
  h3{
    font-size:1.12rem;
    margin:1.8rem 0 0.8rem;
    color:#26262b;
    scroll-margin-top:1.5rem;
  }
  p{margin:0 0 1rem;}
  ul, ol{margin:0 0 1rem; padding-left:1.3rem;}
  li{margin-bottom:0.45rem;}
  strong{font-weight:600; color:#111113;}

  .callout{
    background:var(--accent-soft-2);
    border-left:3px solid var(--accent);
    border-radius:0 8px 8px 0;
    padding:1rem 1.2rem;
    margin:1.4rem 0;
  }
  .callout .callout-title{
    display:block;
    font-weight:600;
    color:var(--accent-dark);
    margin-bottom:0.4rem;
    font-size:0.95rem;
  }
  .callout p{margin:0; font-size:0.96rem;}

  .table-wrap{overflow-x:auto; margin:1.3rem 0;}
  table{
    width:100%;
    border-collapse:collapse;
    font-size:0.92rem;
    min-width:480px;
  }
  th, td{
    text-align:left;
    padding:0.55rem 0.8rem;
    border-bottom:1px solid var(--border-soft);
  }
  th{
    background:var(--accent-soft);
    color:var(--accent-dark);
    font-weight:600;
    font-size:0.82rem;
    text-transform:uppercase;
    letter-spacing:0.04em;
  }
  tr:last-child td{border-bottom:1px solid var(--border);}
  td.num, th.num{text-align:right; font-family:'IBM Plex Mono', monospace;}

  .glossary td:first-child{font-weight:600; white-space:nowrap; color:#111113;}

  /* numbered "chain" cards for the forecast section */
  .chain{list-style:none; margin:1.4rem 0; padding:0; counter-reset:chain;}
  .chain li{
    counter-increment:chain;
    position:relative;
    padding:0 0 1.2rem 2.6rem;
    margin-bottom:0;
  }
  .chain li::before{
    content: counter(chain);
    position:absolute;
    left:0; top:0;
    width:1.7rem; height:1.7rem;
    border-radius:50%;
    background:var(--accent);
    color:#fff;
    font-family:'IBM Plex Mono', monospace;
    font-size:0.85rem;
    font-weight:600;
    display:flex; align-items:center; justify-content:center;
  }
  .chain li::after{
    content:"";
    position:absolute;
    left:0.85rem; top:1.9rem; bottom:0;
    width:1px;
    background:var(--border);
  }
  .chain li:last-child::after{display:none;}
  .chain p{margin:0;}

  .checklist{list-style:none; padding:0; margin:1.2rem 0;}
  .checklist li{
    padding-left:1.6rem;
    position:relative;
    margin-bottom:0.85rem;
  }
  .checklist li::before{
    content:"→";
    position:absolute;
    left:0;
    color:var(--accent-dark);
    font-weight:600;
  }

  hr.divider{
    border:none;
    border-top:1px solid var(--border);
    margin:2.6rem 0;
  }

  .refs{list-style:none; padding:0; margin:0; counter-reset:refs;}
  .refs li{
    counter-increment:refs;
    padding-left:2.2rem;
    position:relative;
    margin-bottom:0.9rem;
    font-size:0.93rem;
    color:#3c3c42;
  }
  .refs li::before{
    content:"[" counter(refs) "]";
    position:absolute;
    left:0;
    font-family:'IBM Plex Mono', monospace;
    color:var(--muted-2);
    font-size:0.85rem;
  }
  .refs a{font-weight:500;}

  footer.note{
    border-top:1px solid var(--border);
    padding:1.6rem 0 3rem;
    font-size:0.85rem;
    color:var(--muted);
  }

  blockquote.shamir{
    margin:1.4rem 0;
    padding:0.2rem 0 0.2rem 1.1rem;
    border-left:2px solid var(--muted-2);
    font-style:italic;
    color:#3c3c42;
  }

  @media (max-width: 640px){
    body{font-size:16px;}
    h1{font-size:1.65rem;}
    .stat-grid{grid-template-columns:repeat(2, 1fr);}
    .masthead{padding:2rem 0 1.2rem;}
  }
</style>
</head>
<body>

<div class="topbar">A field briefing for professionals entering the industry &nbsp;·&nbsp; <strong>PQC Migration Series</strong></div>

<div class="wrap">

  <header class="masthead">
    <div class="kicker">Post-Quantum Certificate Infrastructure</div>
    <h1>Uncharted Territory of PQC:<br><em>Quantum Certificates</em></h1>
    <p class="dek">A field briefing on post-quantum TLS, certificate size, Merkle Tree Certificates, and the fork forming between the Web PKI and private PKI — written for professionals entering the industry, by someone who has to make these decisions for a living.</p>
    <p class="byline">By <strong>Sara Malik</strong> — PakCrypt</p>
    <div class="badge-row">
      <span>PQC Migration Series</span><span class="sep">·</span>
      <span>CTO Field Notes · 2026</span><span class="sep">·</span>
      <span>~30 min read</span>
    </div>
    <div class="tag-row">
      <span class="tag">Post-Quantum Cryptography</span>
      <span class="tag">X.509</span>
      <span class="tag">ML-DSA</span>
      <span class="tag">Merkle Tree Certificates</span>
      <span class="tag">TLS 1.3</span>
      <span class="tag">Certificate Transparency</span>
      <span class="tag">DNS SVCB</span>
    </div>
  </header>

  <details class="toc">
    <summary>Contents</summary>
    <ol class="toc-list">
      <li><a href="#sec-kex">Why Key Exchange Moved First</a></li>
      <li><a href="#sec-history">A Short History of "The Last Time We Did This"</a></li>
      <li><a href="#sec-size">The Size Problem, With Correct Numbers</a></li>
      <li><a href="#sec-mtc">Merkle Tree Certificates: What They Actually Buy You</a></li>
      <li><a href="#sec-bill">The Bill Nobody Itemized Yet</a></li>
      <li><a href="#sec-industry">Where the Industry Is Actually Going</a></li>
      <li><a href="#sec-forecast">Five Years Out: A Forecast, Not a Promise</a></li>
      <li><a href="#sec-practical">What This Means For You, Practically</a></li>
      <li><a href="#sec-glossary">Glossary</a></li>
      <li><a href="#sec-references">References</a></li>
    </ol>
  </details>

  <section class="abstract">
    <div class="label">Abstract</div>
    <p>This blog explains where post-quantum certificate infrastructure actually stands today. It is written for people new to the field who need a working mental model before they make their first design decision on a production system.</p>
    <p>We cover four things in order. First, why the industry moved on key exchange before it moved on signatures, and why that is not the same problem solved twice. Second, the concrete arithmetic of certificate and handshake size under classical, lattice-based, and Merkle Tree Certificate schemes, with corrected numbers and worked examples. Third, the new operational dependencies — landmark distribution, DNS-based discovery, dual-certificate serving — that nobody fully solved before announcing a roadmap. Fourth, a five-year outlook on where the Web PKI, private PKI, and the algorithms underneath them are likely to diverge, and what that divergence will cost the people running infrastructure.</p>
    <p class="pull">The themes here are not new. Every cryptographic transition this industry has lived through — DES to AES, MD5 to SHA-2, RSA to ECC — eventually exposed the same lesson: the math is rarely the hard part. We will return to that point throughout.</p>
  </section>

  <div class="stat-grid">
    <div class="stat-card"><span class="stat-value">544 B</span><span class="stat-label">Classical baseline (ECDSA P-256/P-384 chain)</span></div>
    <div class="stat-card"><span class="stat-value">14,724 B</span><span class="stat-label">Traditional X.509 chain, ML-DSA-44 throughout</span></div>
    <div class="stat-card"><span class="stat-value">4,468 B</span><span class="stat-label">Landmark-relative MTC, ML-DSA-44</span></div>
    <div class="stat-card"><span class="stat-value">8.2×</span><span class="stat-label">Best-case PQC multiple over the classical baseline</span></div>
  </div>

  <article>

    <section id="sec-kex">
      <div class="eyebrow">Threat Model</div>
      <h2>1. Why Key Exchange Moved First</h2>

      <h3>1.1 The threat model is asymmetric, and that asymmetry drove the roadmap</h3>
      <p>Post-quantum migration did not arrive as one project. It arrived as two projects running at different speeds, because the two halves of TLS face different clocks.</p>
      <p><strong>Key exchange</strong> protects confidentiality. An adversary who records encrypted traffic today and later acquires a cryptographically relevant quantum computer (CRQC) can decrypt that traffic retroactively, because the session key was derived from a key exchange that a CRQC can break after the fact. This is the "harvest now, decrypt later" threat, and it is live today — traffic captured this afternoon is already at risk for whatever its confidentiality window turns out to be. If you operate infrastructure that protects secrets with a shelf life longer than "however many years until a CRQC exists," you have already lost some of those secrets to an adversary patient enough to wait.</p>
      <p><strong>Authentication</strong> protects integrity, and integrity does not have the same retroactive failure mode. A signature forged after the fact is useless to an adversary that needed to forge it <em>during</em> a live handshake, three years ago, to impersonate a server in real time. You cannot harvest a signature today and use it to retroactively convince a 2023 client that it was talking to a legitimate server. The signature problem only matters once a CRQC actually exists and is used live against a connection happening <em>then</em>.</p>

      <div class="callout">
        <span class="callout-title">Key Concept: Why "harvest now" doesn't apply to signatures</span>
        <p>Confidentiality is broken by a future attacker reading something recorded in the past. Authentication is broken by a present attacker forging something used right now. A CRQC arriving in year N breaks all key exchanges recorded since day one. It only breaks signatures created from year N onward. This is the single fact that explains the entire shape of the current migration.</p>
      </div>

      <p>This is why the industry's <em>immediate</em> deployment focus is the hybrid key exchange <code>X25519MLKEM768</code>, and not certificate signature replacement. It is also why this is correct prioritization rather than an arbitrary choice.</p>

      <h3>1.2 What X25519MLKEM768 actually is, and what it requires</h3>
      <p><code>X25519MLKEM768</code> is a named group for TLS 1.3 key exchange, standardized through the IETF TLS working group, that concatenates an X25519 elliptic-curve Diffie-Hellman exchange with an ML-KEM-768 key encapsulation exchange. The hybrid approach combines both mechanisms so that the session key is derived from both exchanges, and if either algorithm is broken — a classical attack on ML-KEM, or a CRQC applied to X25519 — the session remains secure because the other exchange is still sound. The IANA codepoint is <code>0x11ec</code>.</p>
      <p>Three things make this deployable <em>immediately</em>, in a way certificate signature migration is not:</p>
      <ul>
        <li><strong>No certificate management.</strong> Key exchange happens fresh, in-band, on every handshake. The server does not need a certificate that says "I support ML-KEM" — it just needs a TLS stack that offers the named group. There is no chain of trust to rebuild, no CA to involve, no root store to update.</li>
        <li><strong>No interoperability cliff.</strong> A hybrid group degrades gracefully. If one side does not support it, the connection falls back to a classical group. Nothing breaks; you simply do not yet have post-quantum protection on that connection.</li>
        <li><strong>Already shipped.</strong> X25519MLKEM768 is the default for Chrome 131+, Firefox 132+, and Edge 131+, accounting for roughly 95% of post-quantum TLS traffic observed today. Server-side, OpenSSL 3.5, NGINX, HAProxy, and the JDK 27 early-access builds all carry support, the last enabling it by default so that TLS clients offer both a hybrid X25519MLKEM768 key share and a traditional x25519 key share without requiring any application code changes.</li>
      </ul>
      <p>You can, in fact, turn this on today, on a server you control, and the next browser visit will very likely use it. That is rare in this industry. Treat it as the easy half of the migration, not the whole migration.</p>

      <h3>1.3 What this hybrid does <strong>not</strong> address</h3>
      <p>It is worth being precise about scope, because vendors are not always precise about scope when they say "post-quantum ready."</p>
      <ul>
        <li><strong>It does not protect authentication.</strong> The server's certificate is still signed with ECDSA or RSA. A CRQC that exists at connection time can still forge that signature and run a live man-in-the-middle attack, hybrid key exchange notwithstanding. Confidentiality and authenticity are independent properties and this migration only buys you the first.</li>
        <li><strong>It does not address signed software, code-signing, or document signatures</strong>, all of which depend on the same vulnerable signature algorithms and have their own, separately unaddressed harvest-now risk for long-lived artifacts.</li>
        <li><strong>It is not "quantum-proof."</strong> ML-KEM is a newer algorithm with a shorter public cryptanalytic record than X25519. The hybrid construction exists specifically because confidence in ML-KEM alone is not yet considered sufficient by the IETF for general deployment during this transition period. You are buying defense in depth against two different failure modes, not certainty against either.</li>
        <li><strong>FIPS compliance has a wrinkle.</strong> In the U.S. FIPS validation regime, ML-KEM is FIPS-approved but X25519 is not, which makes SecP256r1MLKEM768 — not X25519MLKEM768 — the strictly FIPS-compliant hybrid, and Chrome does not ship that variant by default. If you are in a regulated environment, check which named group your compliance posture actually requires before assuming "we enabled PQC" closes that box.</li>
      </ul>
      <p>The remainder of this paper is about the half of the problem this hybrid does not touch: certificate signatures, and the size, infrastructure, and governance consequences of replacing them.</p>
    </section>

    <hr class="divider">

    <section id="sec-history">
      <div class="eyebrow">Historical Pattern</div>
      <h2>2. A Short History of "The Last Time We Did This"</h2>
      <p>Anyone surprised by the current confusion has not been paying attention to how every previous cryptographic transition in this industry actually went. A brief recap, because the present moment rhymes with all of it.</p>

      <h3>2.1 DSA and the early X.509 era</h3>
      <p>X.509 itself dates to 1988, designed for a world of small, centrally-issued directories, not a billion-endpoint public internet. DSA, standardized by NIST in 1994, was itself a product of a contentious, multi-year standardization process with public disputes over patent claims and design rationale — the pattern of "the algorithm exists before the deployment story does" is not new.</p>

      <h3>2.2 The RSA-to-ECC transition took over a decade, and most of the delay was not cryptographic</h3>
      <p>NIST recommended elliptic curve cryptography as early as the late 1990s, and ECC offered smaller keys and faster operations than RSA at equivalent security levels from the start. Yet RSA remained the dominant Web PKI signature algorithm well into the 2010s. The holdup was never "is ECC secure" — it was: hardware support in embedded devices, legacy client compatibility, certificate authority tooling, patent uncertainty around specific curve implementations, and the simple fact that nobody wants to be the first CA to issue a certificate type half the internet cannot validate. ECC adoption accelerated only once browsers, then CAs, then enterprise software all independently decided the compatibility risk had become acceptable — a coordination problem, not a math problem.</p>

      <h3>2.3 Certificate Transparency was bolted on, not designed in</h3>
      <p>Certificate Transparency (CT), and the Signed Certificate Timestamps (SCTs) every TLS handshake now carries, exist because the CA ecosystem suffered real, damaging mis-issuance incidents that public logging was retrofitted to detect. CT was not part of the original X.509 design; it is a patch, applied after the trust model already existed, and it shows: SCTs add bytes to every handshake to solve a governance problem the original certificate format never anticipated. This matters directly to our topic, because Merkle Tree Certificates are explicitly designed to fold CT <em>into</em> issuance from the start rather than bolt it on afterward — a deliberate correction of this exact historical mistake.</p>

      <div class="callout">
        <span class="callout-title">The pattern, stated once</span>
        <p>In every prior transition, the new algorithm was technically ready years before the ecosystem was operationally ready. The gap was always filled with patches — hybrid modes, transparency logs, deprecation timelines — bolted onto a system that was not designed to anticipate them. We are watching this happen again, in real time, with PQC certificates. The useful skill is not predicting which algorithm wins; it is recognizing which operational dependency is about to get bolted on next.</p>
      </div>
    </section>

    <hr class="divider">

    <section id="sec-size">
      <div class="eyebrow">Size Arithmetic</div>
      <h2>3. The Size Problem, With Correct Numbers</h2>

      <h3>3.1 Reference sizes for classical and post-quantum signature schemes</h3>
      <p>Before doing handshake arithmetic, fix the per-algorithm numbers. These are the values specified in FIPS 204 for ML-DSA, and standard reference values for the classical algorithms.</p>

      <div class="table-wrap">
        <table>
          <thead>
            <tr><th>Algorithm</th><th>Security Level</th><th class="num">Public Key (bytes)</th><th class="num">Signature (bytes)</th></tr>
          </thead>
          <tbody>
            <tr><td>ECDSA P-256</td><td>~128-bit classical</td><td class="num">64</td><td class="num">64</td></tr>
            <tr><td>ECDSA P-384</td><td>~192-bit classical</td><td class="num">96</td><td class="num">96</td></tr>
            <tr><td>RSA-2048</td><td>~112-bit classical</td><td class="num">256</td><td class="num">256</td></tr>
            <tr><td>ML-DSA-44</td><td>NIST Level 1 (≈128-bit)</td><td class="num">1,312</td><td class="num">2,420</td></tr>
            <tr><td>ML-DSA-65</td><td>NIST Level 3 (≈192-bit)</td><td class="num">1,952</td><td class="num">3,293</td></tr>
            <tr><td>ML-DSA-87</td><td>NIST Level 5 (≈256-bit)</td><td class="num">2,592</td><td class="num">4,627</td></tr>
          </tbody>
        </table>
      </div>

      <p>A few things jump out immediately. Going from ML-DSA-44 to ML-DSA-87 — the natural choice if you actually want 256-bit-class assurance rather than the minimum NIST level — roughly doubles both public key and signature size again, on top of an already roughly 20-to-40-times increase over ECDSA. Almost every public size comparison you will find online quotes ML-DSA-44 numbers, because it is the smallest option, and that quietly understates the cost of higher-assurance deployments. If your organization's risk posture calls for ML-DSA-65 or ML-DSA-87 — and several signals below suggest serious institutions are heading exactly there — multiply the size problem accordingly before you trust a vendor's slide that only shows Level 1 figures.</p>

      <h3>3.2 What a TLS 1.3 handshake actually needs to authenticate a server</h3>
      <p>Your structural model of the handshake is correct, with one refinement worth stating precisely. To authenticate a server, the client must validate, at minimum:</p>
      <ul>
        <li>A <strong>leaf certificate</strong>: the server's public key, signed by the intermediate CA.</li>
        <li><strong>Two or more SCTs</strong>: each one a signature from a CT log operator, attesting the leaf certificate was logged.</li>
        <li>An <strong>intermediate certificate</strong>: the intermediate's public key, signed by the root CA.</li>
        <li>A <strong>transcript signature</strong>: the server's live signature over the handshake transcript, proving possession of the leaf private key — this is what actually authenticates <em>this</em> connection, as opposed to the certificate, which only authenticates the binding between identity and public key.</li>
      </ul>
      <p>So the inventory of cryptographic material crossing the wire for one signature algorithm, single algorithm throughout, is: 1 leaf public key + 1 transcript signature + 2 SCT signatures + 1 intermediate public key + 1 intermediate signature (by the root) + 1 leaf-certificate signature (by the intermediate) — that is 2 public keys and 5 signatures, 7 cryptographic objects in total. This matches the figure independently reported in coverage of Let's Encrypt's roadmap announcement: a typical TLS handshake today transmits about 1,248 bytes of authentication data across five signatures and two public keys.</p>

      <h3>3.3 Worked arithmetic: classical algorithms</h3>
      <p>Using a P-256 leaf under a P-384 intermediate, your numbers are correct:</p>
      <pre><code>Leaf public key (P-256):            64
Transcript signature (P-256):       64
2 × SCT signature (P-256):         128
Intermediate public key (P-384):    96
Intermediate→root signature (P-384):96
Leaf signature, by intermediate:    96
                                   -----
Total:                             544 bytes</code></pre>
      <p>For an all-RSA-2048 chain, with 7 objects at 256 bytes each: <strong>1,792 bytes</strong>, matching your figure. Real-world chains are frequently mixed, so the 544-to-1,792-byte range is a reasonable bound for what the Web PKI costs today in pure authentication material, excluding TCP/TLS record overhead.</p>

      <h3>3.4 Worked arithmetic: ML-DSA-44</h3>
      <p>Checking the structure: 2 public keys (leaf + intermediate) and 5 signatures (transcript, 2 SCTs, intermediate-by-root, leaf-by-intermediate) is exactly right, structurally. The arithmetic itself: <code>2 × 1,312 = 2,624</code>, and <code>5 × 2,420 = 12,100</code>. Sum: <code>2,624 + 12,100 = 14,724</code>. I want to be explicit about that, because the independent figure from industry coverage of Let's Encrypt's announcement lands at the same order of magnitude: replacing today's roughly 1,248 bytes of authentication data with ML-DSA-44 would push that figure past 14,700 bytes.</p>
      <p>The consequence is concrete and worth stating in absolute terms, not just relative ones: a standard Ethernet MTU is 1,500 bytes. A single round of ML-DSA-44 authentication material alone is roughly ten Ethernet frames. The initial TCP congestion window on many stacks (10 segments, per RFC 6928) is barely enough to carry this handshake's authentication data, before you even add the ML-KEM-768 key exchange material from Section 1, the TLS record headers, extensions, or anything else. This is not a rounding error. It is a structural problem for TLS as currently engineered, which is exactly why the industry did not simply ship ML-DSA into existing X.509 chains and call the problem solved.</p>

      <h3>3.5 Higher assurance levels make this worse, not better</h3>
      <p>If you redo this arithmetic at ML-DSA-65 (2 × 1,952 + 5 × 3,293 = 20,369 bytes) or ML-DSA-87 (2 × 2,592 + 5 × 4,627 = 28,319 bytes), the picture deteriorates further. This is the comparison the industry's size discussions mostly skip, and it is exactly the comparison an organization choosing a long-lived root CA key needs to make, because root keys are typically provisioned for the highest assurance level the organization can justify, not the cheapest one.</p>
    </section>

    <hr class="divider">

    <section id="sec-mtc">
      <div class="eyebrow">Merkle Trees</div>
      <h2>4. Merkle Tree Certificates: What They Actually Buy You</h2>

      <h3>4.1 The core idea</h3>
      <p>Under the Merkle Tree Certificate model, a Certification Authority signs a single "Tree Head" representing potentially millions of certificates, and the certificate sent to the browser is a lightweight proof of inclusion in that tree. Instead of paying a full signature's cost for every single certificate, you pay it once, for an entire batch, and every certificate in that batch carries only a small, logarithmically-sized proof that it belongs to the batch the CA already vouched for.</p>
      <p>This is the single design idea behind every number improvement described below, and it generalizes a tool the industry already trusts: it is the same Merkle-tree inclusion-proof construction that underlies Certificate Transparency itself, applied to the certificate's own existence rather than bolted on afterward as a separate log.</p>

      <h3>4.2 Standalone MTCs</h3>
      <p>A standalone MTC needs: 1 transcript signature (2,420 bytes at ML-DSA-44), 1 public key (1,312 bytes), 1 inclusion proof (384 bytes, for the specific tree depth assumed), and 2 or more co-signatures from independent witnesses (2 × 2,420 = 4,840 bytes). Total: <code>2,420 + 1,312 + 384 + 4,840 = 8,956 bytes</code>. Your figure checks out.</p>
      <p>This is meaningfully better than 14,724 bytes — a roughly 39% reduction — but it is still over sixteen times the size of the 544-byte classical baseline. The co-signatures are still the dominant cost, because a standalone MTC still has to convince the client, on the spot, that the witnesses actually vouched for this particular tree head.</p>

      <h3>4.3 Landmark-relative MTCs</h3>
      <p>The improvement comes from removing the co-signatures from the live handshake entirely. Replacing per-certificate signatures with compact hash-based inclusion proofs, the architecture shrinks quantum-resistant TLS authentication data from roughly 14,700 bytes down to as little as 736 bytes. If the client already trusts a recent landmark — a periodically co-signed tree head it obtained out of band, independent of this specific connection — the server need only send a transcript signature, a public key, and an inclusion proof relative to that already-trusted landmark.</p>
      <p>The numbers — 2,420 + 1,312 + 736 = 4,468 bytes — are internally consistent with this model and with the 736-byte figure reported as Google's headline result for the landmark-relative case. Note that the 736-byte inclusion proof assumes a specific landmark cadence (hourly, on the order of millions of certificates per landmark, roughly 23 hashes deep); change that cadence and the proof size moves logarithmically, not linearly, so this number is sensitive to operational choices CAs haven't all finalized yet.</p>

      <div class="table-wrap">
        <table>
          <thead><tr><th>Scheme</th><th class="num">Authentication bytes</th><th class="num">Multiple of classical (544 B)</th></tr></thead>
          <tbody>
            <tr><td>ECDSA P-256 / P-384 chain (classical baseline)</td><td class="num">544</td><td class="num">1×</td></tr>
            <tr><td>RSA-2048 chain</td><td class="num">1,792</td><td class="num">3.3×</td></tr>
            <tr><td>Traditional X.509, ML-DSA-44 throughout</td><td class="num">14,724</td><td class="num">27×</td></tr>
            <tr><td>Standalone MTC, ML-DSA-44</td><td class="num">8,956</td><td class="num">16.5×</td></tr>
            <tr><td>Landmark-relative MTC, ML-DSA-44</td><td class="num">4,468</td><td class="num">8.2×</td></tr>
          </tbody>
        </table>
      </div>

      <h3>4.4 The honest framing: MTCs are an enormous improvement and still not free</h3>
      <p>8.2 times the byte cost of a classical handshake is genuinely good engineering, given the constraint that one must use a NIST-standardized post-quantum signature somewhere in the chain. It is not, however, "as small as classical," and treating it as solved would be premature. Every operational dependency described in Section 5 exists specifically to make that 736-byte number achievable in practice, and none of those dependencies are fully built yet.</p>
    </section>

    <hr class="divider">

    <section id="sec-bill">
      <div class="eyebrow">Operational Debt</div>
      <h2>5. The Bill Nobody Itemized Yet</h2>
      <p>Reducing a number on a slide and operating a working system at internet scale are different achievements. Here is what landmark-relative MTCs actually require, none of which is optional if one wants the 4,468-byte figure rather than the 8,956-byte fallback.</p>

      <h3>5.1 Issuance delay</h3>
      <p>Landmark-relative MTCs are signed in batches against a periodic landmark, not on demand. That means certificate issuance is no longer instantaneous in the way a same-day Let's Encrypt ECDSA certificate is today. The industry has not yet published hard numbers on what that delay will be in production; "assume it's short" is a reasonable working assumption for now, but it is an assumption, not a specification, and anyone designing automated certificate issuance pipelines (ACME-style, just-in-time, ephemeral) needs to track this number specifically as it firms up.</p>

      <h3>5.2 Landmark discovery without an extra round trip</h3>
      <p>A client needs to know, before it connects, which landmark a given server's certificate chain will be relative to — different CAs produce different landmarks, the way different root programs trust different root certificates today. Discovering this by asking the server first would cost an extra round trip on every connection, which defeats much of the size win. The mechanism the industry has converged on for this is TLS Trust Anchor Identifiers, advertised via the <code>tls-trust-anchors</code> parameter on HTTPS or SVCB DNS records, so the client can compute the intersection between its configured trust anchors and the server's available ones before initiating the handshake at all.</p>
      <p>This is a real new dependency. SVCB and HTTPS DNS record types (RFC 9460) are still inconsistently supported across resolvers, stub libraries, and middleboxes. If an organization's DNS infrastructure does not yet resolve and parse these record types reliably, that is now squarely in scope for any PQC migration plan.</p>

      <h3>5.3 Servers need to support both standalone and landmark-relative certificates, simultaneously</h3>
      <p>A server cannot assume every client presents a fresh landmark. Clients may have no landmark at all, or an outdated one the server no longer recognizes. The fallback is the standalone MTC — full cost, co-signatures included. That means a production server needs both certificate types provisioned and live at once, plus the logic to atomically pick the right one per ClientHello, plus the operational discipline to rotate and renew both in sync. This roughly doubles the certificate-management surface area compared to a single-certificate world, and it is new complexity, not a simplification, however good the best-case byte count looks.</p>

      <h3>5.4 Landmark freshness becomes an operating-system-level problem</h3>
      <p>Landmarks function as trust anchors — conceptually adjacent to today's root certificate bundle, except landmarks expire and rotate on a much shorter cycle (the example cadence cited above is hourly). Browsers already have infrastructure for pushing frequent updates to internal trust data; most other TLS clients — embedded devices, IoT firmware, language-runtime TLS stacks, command-line tools, internal microservices — do not, and rely on trust bundles that today are updated rarely, sometimes only at OS or package upgrade time.</p>
      <p>Making landmark-relative MTCs work universally implies something close to an OS-level or distribution-level landmark-updating service, running continuously, for every platform that wants the smaller certificate. Google's rollout deliberately keeps the Chrome Quantum-resistant Root Store as an addition alongside, not a replacement for, the existing Chrome Root Store — a sensible hedge, but one that also signals Google itself is not assuming this problem is solved outside the browser. Nobody has published a detailed design for "landmark updates for everything that isn't a browser." That is a gap, and it is worth tracking who fills it.</p>

      <h3>5.5 The bifurcation risk this creates</h3>
      <p>Put 5.2 through 5.4 together, and we get a real risk: browsers — practically, a small number of major browser vendors — solve landmark freshness and discovery for themselves, because they control the update channel and the DNS-aware infrastructure to do it. Everything else — libraries, embedded TLS stacks, internal service mesh implementations, IoT — falls back to standalone MTCs or, worse, stays on classical certificates because nobody ships them a landmark updater. The current rollout phases place initial bootstrapping and CA onboarding for the quantum-resistant root store on a 2027 timeline, run by a small number of organizations setting the technical direction for everyone else. That concentration of design authority is a legitimate governance concern independent of whether the cryptography itself is sound, and it is worth professionals entering this field forming their own view on it rather than treating it as someone else's problem.</p>
    </section>

    <hr class="divider">

    <section id="sec-industry">
      <div class="eyebrow">Industry Split</div>
      <h2>6. Where the Industry Is Actually Going</h2>

      <h3>6.1 MTC adoption, with current commitments</h3>
      <p>On June 3, 2026, Let's Encrypt — the nonprofit certificate authority that secures more than 500 million websites — published its post-quantum roadmap and named Merkle Tree Certificates as its chosen path, targeting a staging environment that issues MTCs in late 2026 and a production-ready environment in 2027. This is the single most consequential adoption signal to date, because Let's Encrypt issued 54.4% of all public SSL/TLS certificates in Q1 2026, meaning its adoption of MTCs essentially makes the standard viable for the majority of the encrypted web, independent of what any other CA decides to do.</p>
      <p>Google has stated it has no immediate plan to add traditional X.509 certificates containing post-quantum signatures to the Chrome Root Store, and will instead use a new Chrome Quantum-resistant Root Store and corresponding Root Program that only supports MTCs. Field testing is already under way, with Cloudflare operating roughly one thousand TLS certificates in the experiment, and phase two is planned for Q1 2027, inviting Certificate Transparency log operators that already had a usable log in Chrome before February 1, 2026, to help bootstrap public MTCs, with the CA onboarding framework for the new root program targeted around Q3 2027.</p>
      <p>The CA/B Forum — the body that, in principle, sets baseline requirements across the entire commercial CA industry — has, by contrast, moved markedly slower. As of this writing there is no MTC-specific baseline requirement; participant commentary so far amounts to early-stage investigation. This is a real asymmetry in the industry's governance, not a rhetorical flourish: a handful of browser-and-CDN organizations are setting de facto technical direction faster than the cross-industry standards body that nominally governs Web PKI baseline requirements.</p>

      <h3>6.2 ML-DSA adoption is moving on a separate, slower, and more conservative track</h3>
      <p>While MTCs target the <em>public</em> Web PKI, ML-DSA itself is being adopted directly — full X.509 certificates, no Merkle tree — in contexts where certificate size matters less than algorithm assurance and where the client population is small and controlled.</p>
      <p>Google is adding native ML-DSA support for private PKI use in Chrome, separate from and faster-moving than its public Web PKI plans, which remain MTC-only. Microsoft has signaled support for ML-DSA certificates in CA/B Forum discussions, reportedly leaning toward ML-DSA-87 — the highest, most conservative, and largest-byte-cost security level, consistent with an enterprise posture that prioritizes assurance margin over the byte-count concerns driving the public web's MTC push. The CA/B Forum's Baseline Requirements for S/MIME already permit ML-DSA, ahead of the Web-PKI baseline requirements, which do not yet.</p>
      <p>The financial sector has built its own dedicated infrastructure rather than wait: a new X9 Financial PKI, operated by DigiCert, with ML-DSA support built in from the start. This is a sector with both the regulatory mandate and the resources to build bespoke PKI rather than wait for Web PKI consensus, and it has chosen straightforward ML-DSA X.509 certificates over MTCs — a different calculus than Google's, made by a different industry with different constraints (closed client populations, regulatory certainty requirements, less sensitivity to a few extra kilobytes per handshake).</p>

      <h3>6.3 The structural split, stated plainly</h3>
      <p>The public Web PKI is converging on Merkle Tree Certificates, driven by Google, Cloudflare, and Let's Encrypt, optimizing for handshake size at internet scale with an open, heterogeneous client population. Private PKI — enterprise, financial-sector, S/MIME — is converging on direct ML-DSA X.509 certificates, optimizing for implementation simplicity and assurance level, in contexts where the client population is closed and controlled and a few extra kilobytes per connection is an acceptable price.</p>
      <p>These are not competing proposals where one will eventually win. They are two different answers to two different constraint sets, and both are likely to persist. That has a direct, practical consequence: TLS and HTTPS stacks going forward will need to correctly implement and select between multiple X.509-adjacent certificate formats, not migrate cleanly from one format to a single successor. Budget engineering time accordingly.</p>
    </section>

    <hr class="divider">

    <section id="sec-forecast">
      <div class="eyebrow">Five-Year Forecast</div>
      <h2>7. Five Years Out: A Forecast, Not a Promise</h2>
      <p>Treat everything in this section as informed extrapolation from current trajectories, not certainty. Cryptographic migrations have a long history of running later than announced, and PQC certificates are unlikely to be the exception.</p>

      <ol class="chain">
        <li><p><strong>Key exchange will be fully post-quantum by default, broadly.</strong> Hybrid key exchange is cheap, already deployed at scale, and has no certificate-management dependency. Expect near-universal default-on hybrid key exchange across major browsers, CDNs, and server software well before the certificate-signature problem is anywhere close to resolved. This part of the migration is genuinely close to done.</p></li>
        <li><p><strong>The public Web PKI will be mid-transition to MTCs, not finished.</strong> Given the Q3 2027 target for CA onboarding into Chrome's quantum-resistant root program, and the multi-year history of every prior CA ecosystem transition (the ECC migration took over a decade; CT enforcement took years to reach universal logging), expect partial MTC deployment by major CDN-fronted sites, with the long tail of the Web PKI — smaller hosting providers, self-managed servers, embedded web services — still on classical or transitional certificates. Full MTC ubiquity in five years is optimistic; meaningful MTC presence among the highest-traffic sites is realistic.</p></li>
        <li><p><strong>Private PKI will have moved faster, and more unevenly, than the public web.</strong> Financial services, defense, and other regulated sectors with mandate-driven timelines and controlled client populations will likely have completed ML-DSA migrations for new infrastructure well before the Web PKI's MTC rollout matures, simply because their constraint set is simpler: no anonymous client population, no DNS-discovery problem, often no requirement to interoperate with arbitrary external software.</p></li>
        <li><p><strong>Landmark distribution will be the long pole, and possibly the source of the next visible failure.</strong> Watch specifically for whether non-browser TLS clients — package managers, IoT firmware, internal service meshes, embedded libraries — get a credible landmark-update mechanism. If they don't, by year five expect either widespread silent fallback to standalone MTCs (functional but not realizing the headline size win) or, in the worst case, a security incident traceable to stale landmark data being trusted past its intended freshness window. This is the single most under-specified piece of the entire architecture today, and it is worth professionals tracking closely rather than assuming someone else has it handled.</p></li>
        <li><p><strong>SVCB/HTTPS DNS record support will become a quiet prerequisite for PQC readiness.</strong> Organizations that have not modernized their DNS infrastructure to reliably serve and resolve these record types will find that gap blocking landmark discovery, independent of how ready their TLS stack otherwise is. This is exactly the kind of unglamorous dependency that derails migration timelines, the same way legacy hardware TLS termination quietly delayed the RSA-to-ECC transition for years in some sectors.</p></li>
        <li><p><strong>The Web PKI and private PKI will not re-converge within five years.</strong> The constraint sets driving MTCs (public, open, byte-sensitive) and direct ML-DSA (private, controlled, assurance-sensitive) are structural, not incidental, and nothing on the current roadmap suggests they merge. Expect the bifurcation Section 6.3 describes to be a permanent feature of the landscape professionals in this field need to know how to navigate, not a temporary transitional artifact.</p></li>
      </ol>
    </section>

    <hr class="divider">

    <section id="sec-practical">
      <div class="eyebrow">Practical Guidance</div>
      <h2>8. What This Means Practically</h2>
      <p>For someone entering information security today, a few concrete, actionable takeaways, separate from the forecasting above:</p>

      <ul class="checklist">
        <li><strong>Enable hybrid key exchange now.</strong> It is low-risk, already supported broadly, and addresses a live threat (harvest-now-decrypt-later) that is accruing cost every day we delay. There is no good reason for a production TLS server to not be offering <code>X25519MLKEM768</code> today.</li>
        <li><strong>Do not conflate "we enabled hybrid key exchange" with "we are post-quantum ready."</strong> Authentication is still classical almost everywhere. Be precise about which half of the problem any given deployment has actually addressed when we report status upward.</li>
        <li><strong>If you operate DNS infrastructure, start testing SVCB/HTTPS record support now.</strong> This dependency is easy to deprioritize because it looks unrelated to cryptography, and that is exactly why it will be underestimated until it becomes a blocker.</li>
        <li><strong>If you are choosing a security level for a long-lived key (root CA, code-signing, anything provisioned for a decade or more), do the size arithmetic at ML-DSA-65 or ML-DSA-87, not just ML-DSA-44.</strong> Most public comparisons quote the smallest, cheapest option; your risk tolerance for a long-lived key is probably not the smallest, cheapest option.</li>
        <li><strong>Track Let's Encrypt's staging MTC environment as the most concrete, observable bellwether.</strong> A nonprofit CA issuing the majority of public certificates committing to a late-2026 staging timeline is a far more reliable signal of real progress than any vendor announcement.</li>
        <li><strong>Remember Shamir's observation, because it will be true again here.</strong> The largest practical risk in this entire transition is probably not a cryptographic break. It is operational complexity — dual-certificate handling, stale landmarks, misconfigured DNS, a fallback path nobody tested — creating a bypass that has nothing to do with whether ML-DSA or MTCs are mathematically sound.</li>
      </ul>

      <blockquote class="shamir">"Cryptography is typically bypassed, not penetrated." — Adi Shamir</blockquote>
    </section>

    <hr class="divider">

    <section id="sec-glossary">
      <div class="eyebrow">Quick Reference</div>
      <h2>Quick Reference Glossary</h2>
      <div class="table-wrap">
        <table class="glossary">
          <thead><tr><th>Term</th><th>Meaning</th></tr></thead>
          <tbody>
            <tr><td>Harvest now, decrypt later</td><td>Recording encrypted traffic today to decrypt retroactively once a quantum computer capable of breaking the key exchange exists.</td></tr>
            <tr><td>ML-KEM</td><td>Module-Lattice-Based Key Encapsulation Mechanism, FIPS 203, the NIST-standardized post-quantum key exchange algorithm used in hybrid TLS groups.</td></tr>
            <tr><td>ML-DSA</td><td>Module-Lattice-Based Digital Signature Algorithm, FIPS 204, the NIST-standardized post-quantum signature algorithm, formerly CRYSTALS-Dilithium.</td></tr>
            <tr><td>Hybrid key exchange</td><td>A TLS key exchange combining a classical algorithm (e.g. X25519) with a post-quantum one (e.g. ML-KEM-768), so security holds if either alone is broken.</td></tr>
            <tr><td>SCT</td><td>Signed Certificate Timestamp; a signature from a Certificate Transparency log attesting a certificate was publicly logged.</td></tr>
            <tr><td>Merkle Tree Certificate (MTC)</td><td>An experimental certificate format in which a CA signs one tree head covering many certificates, and each certificate is authenticated by a compact inclusion proof rather than its own full signature.</td></tr>
            <tr><td>Landmark</td><td>A periodically co-signed MTC tree head that a client has already obtained and trusts, allowing a server to send only a small inclusion proof relative to it instead of full co-signatures.</td></tr>
            <tr><td>PLANTS</td><td>The IETF working group ("PKI, Logs, And Tree Signatures") standardizing the MTC specification.</td></tr>
            <tr><td>SVCB / HTTPS DNS records</td><td>RFC 9460 DNS record types allowing a server to advertise service parameters — including, via TLS Trust Anchor Identifiers, which certificate trust anchors it supports — before a TLS handshake begins.</td></tr>
            <tr><td>CQRS</td><td>Chrome Quantum-resistant Root Store, Google's planned new Chrome root program supporting only MTCs.</td></tr>
          </tbody>
        </table>
      </div>
    </section>

    <hr class="divider">

    <section id="sec-references">
      <div class="eyebrow">Sources</div>
      <h2>References</h2>
      <ol class="refs">
        <li id="ref-jep527">JEP 527: Post-Quantum Hybrid Key Exchange for TLS 1.3. OpenJDK. <a href="https://openjdk.org/jeps/527">openjdk.org/jeps/527</a></li>
        <li id="ref-draft-ecdhe-mlkem">Kwiatkowski, K., Kampanakis, P., Westerbaan, B.E., Stebila, D. <em>Post-quantum hybrid ECDHE-MLKEM Key Agreement for TLSv1.3</em>. IETF Internet-Draft, draft-ietf-tls-ecdhe-mlkem. <a href="https://datatracker.ietf.org/doc/draft-ietf-tls-ecdhe-mlkem/">datatracker.ietf.org/doc/draft-ietf-tls-ecdhe-mlkem</a></li>
        <li id="ref-draft-hybrid-design"><em>Hybrid key exchange in TLS 1.3</em>. IETF Internet-Draft, draft-ietf-tls-hybrid-design. <a href="https://datatracker.ietf.org/doc/html/draft-ietf-tls-hybrid-design">datatracker.ietf.org/doc/html/draft-ietf-tls-hybrid-design</a></li>
        <li id="ref-fips204">NIST. <em>FIPS 204: Module-Lattice-Based Digital Signature Standard</em>. <a href="https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.204.ipd.pdf">nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.204.ipd.pdf</a></li>
        <li id="ref-draft-dilithium-certs"><em>Internet X.509 Public Key Infrastructure: Algorithm Identifiers for ML-DSA</em>. IETF Internet-Draft, draft-ietf-lamps-dilithium-certificates. <a href="https://www.ietf.org/archive/id/draft-ietf-lamps-dilithium-certificates-07.html">ietf.org/archive/id/draft-ietf-lamps-dilithium-certificates-07.html</a></li>
        <li id="ref-thehackernews-mtc"><em>Google Develops Merkle Tree Certificates to Enable Quantum-Resistant HTTPS in Chrome</em>. The Hacker News, March 2026. <a href="https://thehackernews.com/2026/03/google-develops-merkle-tree.html">thehackernews.com/2026/03/google-develops-merkle-tree.html</a></li>
        <li id="ref-encryptionconsulting"><em>Merkle Tree Certificates: Rethinking the WebPKI for the Post-Quantum Era</em>. Encryption Consulting. <a href="https://www.encryptionconsulting.com/about-merkle-tree-certificates/">encryptionconsulting.com/about-merkle-tree-certificates</a></li>
        <li id="ref-postquantum-google"><em>Google's Merkle Tree (MTC) Gambit to Quantum-Proof HTTPS</em>. postquantum.com, April 2026. <a href="https://postquantum.com/security-pqc/googles-merkle-tree-mtc-https/">postquantum.com/security-pqc/googles-merkle-tree-mtc-https</a></li>
        <li id="ref-postquantum-le"><em>Let's Encrypt Commits to Merkle Tree Certificates</em>. postquantum.com. <a href="https://postquantum.com/security-pqc/lets-encrypt-merkle-tree-mtc-post-quantum/">postquantum.com/security-pqc/lets-encrypt-merkle-tree-mtc-post-quantum</a></li>
        <li id="ref-letsencrypt-pq"><em>A Post-Quantum Future for Let's Encrypt</em>. Let's Encrypt, June 3, 2026. <a href="https://letsencrypt.org/2026/06/03/pq-certs">letsencrypt.org/2026/06/03/pq-certs</a></li>
        <li id="ref-cybersecurefox"><em>Google And Cloudflare Pilot Merkle Tree Certificates To Secure Chrome HTTPS Against Post-Quantum Attacks</em>. cybersecurefox.com, March 2026. <a href="https://cybersecurefox.com/en/google-merkle-tree-certificates-post-quantum-chrome/">cybersecurefox.com/en/google-merkle-tree-certificates-post-quantum-chrome</a></li>
        <li id="ref-securitybrief"><em>Google tests Merkle Tree Certificates for quantum web</em>. securitybrief.com.au, March 2026. <a href="https://securitybrief.com.au/story/google-tests-merkle-tree-certificates-for-quantum-web">securitybrief.com.au/story/google-tests-merkle-tree-certificates-for-quantum-web</a></li>
        <li id="ref-trust-anchor-ids">Beck, et al. <em>TLS Trust Anchor Identifiers</em>. IETF Internet-Draft, draft-ietf-tls-trust-anchor-ids. <a href="https://datatracker.ietf.org/doc/draft-ietf-tls-trust-anchor-ids/">datatracker.ietf.org/doc/draft-ietf-tls-trust-anchor-ids</a></li>
        <li id="ref-netguardia"><em>Hybrid Key Exchange Today: Why X25519 + ML-KEM Is the Interim Default</em>. netguardia.com, April 2026. <a href="https://netguardia.com/privacy/encryption/hybrid-key-exchange-today-why-x25519-ml-kem-is-the-interim-default/">netguardia.com/privacy/encryption/hybrid-key-exchange-today-why-x25519-ml-kem-is-the-interim-default</a></li>
        <li id="ref-systemshardening"><em>Post-Quantum TLS 1.3 in Production: Deploying X25519+ML-KEM-768 with OpenSSL 3.5, NGINX, and HAProxy</em>. systemshardening.com, May 2026. <a href="https://www.systemshardening.com/articles/network/tls-post-quantum-hybrid-deployment/">systemshardening.com/articles/network/tls-post-quantum-hybrid-deployment</a></li>
        <li id="ref-rfc9460">Schwartz, B., Bishop, M., Nygren, E. <em>Service Binding and Parameter Specification via the DNS (SVCB and HTTPS Resource Records)</em>. RFC 9460, November 2023.</li>
      </ol>
    </section>

  </article>

  <footer class="note">
    This paper reflects the state of post-quantum certificate infrastructure as publicly documented as of June 2026. Several of the timelines cited (CA onboarding to Chrome's quantum-resistant root store, Let's Encrypt's production MTC environment) are vendor-stated targets, not delivered milestones. Treat dates beyond the current quarter as subject to revision, consistent with the historical pattern this paper describes in Section 2.
  </footer>

</div>
</body>
</html>
