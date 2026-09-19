---
layout: post
title: "The Square Law of Code"
math: true
---

# The Square Law of Code

### Why a hundred times faster at writing software buys you only four times more of it

*A popular-science summary of "The Square Law of Code: Allocating the AI Productivity Windfall Across Quantity, Quality, and Security" by Sara Malik, PakCrypt.Org.*

---

## The trap

AI can now write code at a rate that would have looked like science fiction in 2020. The obvious conclusion follows: if we can write software ten times faster, we should build ten times as much software.

The obvious conclusion is wrong. It is wrong for a reason that predates AI by half a century, and the reason is arithmetic.

Software is made of features. Features interact. A login page interacts with a password-reset flow, which interacts with an email service, which interacts with a logging library. The work of writing features grows in a straight line with their number. The work of making sure they behave together grows much faster, because the number of ways they can misbehave together is the number of *pairs* of features, and pairs grow with the square. Add a determined attacker, who chains one misbehaving pair into another, and the number of things to worry about grows with the square of the square.

That is the Square Law. Double the features, quadruple the testing, and multiply the security work by sixteen.

---

## What the windfall actually looks like

Before allocating a windfall it is worth checking its size. The measurements from 2023 to 2026 tell a story with a twist.

| What was measured | Result | Source |
|---|---|---|
| Developers on a small, isolated task with an AI assistant | **55.8% faster** | Peng et al., 2023 |
| Experienced maintainers on their own mature codebases | **19% slower** (they believed they were 20% faster) | METR, July 2025 |
| METR's follow-up with 57 developers | Somewhere between −4% and +18%, intervals crossing zero | METR, Feb 2026 |
| Effect of a 25% rise in AI adoption on delivery stability | **−7.2%** | DORA, 2024 |
| Duplicated code blocks since 2023 | **+81%**; refactoring fell from 21% to 3.8% of changes | GitClear, Jan 2026 |
| AI-generated code passing basic security checks | **55%**, unchanged for two years | Veracode, Mar 2026 |
| Developers who trust AI accuracy | **33%** trust, **46%** distrust; 66% cite "almost right" as their top frustration | Stack Overflow, 2025 |

Read the table from top to bottom and the pattern is clear. The speed-up is real when the task is small and nobody has to live with the result. It fades as the codebase gets older and more connected. And the code that comes out is more duplicated, less maintained, and about as secure as a coin toss. The models became fluent. They did not become safe.

The most striking line is the second one. Developers in a controlled trial were slower with AI and were convinced they were faster. Generated code *feels* like progress in a way that testing never will. That feeling is the real hazard.

---

## The law, in one line

Call the windfall **W**: how many times more engineering capacity AI gives you. Call **q** the factor by which you grow your product. The paper's cost model says you can sustain a growth of **q** only if

> **q + q² + q⁴ ≤ 3W**

The three terms are writing, testing, and securing. They grow as the line, the square, and the square of the square.

Solve that inequality and something humbling falls out. The sustainable growth in features is roughly the **fourth root** of the windfall.

| Windfall W | Sustainable product growth q | Testing budget (q²) | Security budget (q⁴) |
|---:|---:|---:|---:|
| 2× | 1.3× | 1.7× | 3× |
| 7× | **2×** | **4×** | **16×** |
| 10× | 2.2× | 4.8× | 23× |
| 100× | **4.1×** | 17× | 279× |
| 1000× | 7.4× | 54× | 2,938× |

A hundredfold windfall buys a fourfold product. The row at 7× is where the famous "2, 4, 16" comes from.

And if a team ignores this and spends a 10× windfall entirely on volume? The paper counts the unfunded work: about 10,000 units of testing and security effort, against 27 units of added capacity. That is negative productivity. A team that ships a hundred features in a day and spends a month patching what broke has moved backwards in every unit that matters.

---

## Where the exponents come from

The "square" for testing is old, well-measured news. In 2004, researchers at NIST examined real failures in medical devices, browsers, web servers, and NASA systems. Nearly every failure was triggered by the interaction of one or two settings; none needed more than six. Testing that covers pairs catches most bugs, and the number of pairs grows with the square of the number of features. Meir Lehman wrote in 1980 that a program's complexity rises unless work is spent holding it down. The GitClear data show that work collapsing precisely while volume rose.

The "square of the square" for security is the paper's own claim, and its authors say so plainly. The argument is that modern attacks are chains. Log4Shell in 2021 was a logging library, a string-substitution feature, a directory lookup, and a network client, each harmless alone, composed into remote code execution across a very large fraction of the world's Java. The xz backdoor of 2024 composed a build quirk, a test fixture, a linker feature, and the SSH daemon. Neither flaw lived in a feature. Both lived in the *edges between edges*. Counting two-link chains over a system's interactions gives the fourth power, and real chains are often longer.

The paper also reports the evidence that cuts against it: studies showing weak links between per-file complexity and vulnerabilities, and OpenBSD getting safer with age. Its reply is that per-file metrics measure the linear term while vulnerabilities live in the cross-file terms, and that a codebase held at constant size can pay its debt down. A codebase quadrupled in a quarter cannot.

---

## Who pays for sixteen times the security work?

This is the objection every manager raises. Sixteen times the security staff is unavailable at any price.

The answer is the paper's central twist: **the same AI that writes insecure code is now very good at finding it.**

- Google's Big Sleep agent found an exploitable bug in SQLite before it reached a release (2024).
- DARPA's AI Cyber Challenge had autonomous systems find 54 of 63 planted vulnerabilities, patch 43, and stumble on 18 real zero-days, at about $152 per task (2025).
- Anthropic's Project Glasswing reported more than ten thousand high- or critical-severity findings in a month, with over 90% of a checked sample confirmed real (2026).

Set that next to the 55% security pass rate for generated code. The explanation is simple. Writing safe code means satisfying every constraint at once. Finding unsafe code means violating one. Search is easier than synthesis. The q⁴ term is paid in machine time, and machine time is the one input whose price keeps falling.

The paper proposes a workflow it calls the **A³ loop**:

1. **Author** — a model writes the feature.
2. **Adversary** — a *different* model, from a different vendor, is told to break it: generate interaction tests, fuzz the edges, build exploit chains through neighbouring features.
3. **Auditor** — a third role confirms the adversary's findings actually reproduce (AI auditors hallucinate too) and produces the fix.
4. **Arbiter** — the human. Reads the reports, decides what ships, owns the residual risk.

A feature ships only when its interaction coverage meets threshold and confirmed findings are zero. Under that rule, spending the windfall on volume alone becomes impossible by construction: the adversary's queue grows as q⁴, and the arbiter has only so many hours.

---

## Measuring the right thing

None of this survives a manager who counts features shipped. The paper proposes replacing output metrics with outcome metrics:

- **Verified-feature throughput** — features that passed interaction testing per unit time. An untested feature counts as zero.
- **Interaction coverage ratio** — tested feature pairs over total pairs. This is the number that should visibly fall when a team overspends on volume.
- **Security debt ratio** — unfixed findings, weighted by severity, per verified feature.
- **Mean time to remediate** — discovery to deployed fix.

Tony Hoare said there are two ways to build software: so simple there are obviously no deficiencies, or so complicated there are no obvious deficiencies. Every code generator in production is optimized for the second. Fluency is the enemy of obviousness.

---

## Why this is about survival

Two facts make the law a defensive necessity rather than a best practice.

**Monoculture.** If most new code is written by a handful of model families, a blind spot in a model becomes a blind spot in the world. Veracode's data show every model failing the same log-injection test. One study found that 5% of commercial-model and 22% of open-source-model code samples import packages that do not exist, producing over 200,000 unique fictional package names. Register one of those names and you own a supply-chain attack. It already has a name: slopsquatting.

**The adversary got the windfall too.** In November 2025, Anthropic disclosed a state-linked campaign in which an AI agent carried out an estimated 80 to 90 percent of the tactical intrusion work against roughly thirty targets. The paper borrows Lanchester's square law of 1916, which says fighting strength grows with the square of numbers under aimed fire. Every generated feature is a target; every composition a firing solution; and the attacker's search parallelizes perfectly. A defender who multiplies volume by W and holds security constant faces an exchange ratio of roughly W³ against them.

The vulnerability registry has noticed. NIST reported in April 2026 that CVE submissions grew 263% between 2020 and 2025 and that the National Vulnerability Database would henceforth triage rather than analyze everything. The finders scale. The fixers do not.

---

## The honest part

The authors are explicit about what they have and have not shown. The square for testing rests on decades of measurement. The fourth power for security rests on a counting argument and case evidence. They chose the smallest plausible chain length, which makes the law conservative, and ignored the fact that most chains are unreachable, which makes it aggressive. They state a falsification test: measure vulnerabilities against feature count in AI-accelerated codebases with controlled review effort, and if the exponent comes out below 1.5, the law is dead.

They also note that the paper was drafted with AI assistance and reviewed by the authors under the paper's own rule: a different adversary, a human arbiter.

---

## The one-sentence version

AI accelerates the only part of software engineering whose cost was ever linear, so the windfall must be spent mostly on the parts that were never linear, and the same machine has to be pointed the other way to pay for it.

---

*Sources cited in the full paper include Brooks (1975, 1987), Lehman (1980), Kuhn et al. (2004), Howard, Pincus & Wing (2003), Geer et al. (2003), Lanchester (1916), Pearce et al. (IEEE S&P 2022), Perry et al. (CCS 2023), Spracklen et al. (USENIX Security 2025), Peng et al. (2023), METR (2025, 2026), DORA (2024), GitClear (2026), Veracode (2026), Stack Overflow (2025), Google Project Zero (2024), DARPA AIxCC (2025), Anthropic (2025, 2026), and NIST (2026).*
