---
layout: post
title: "Randomness, Entropy, Unpredictability, and Information"
---

## <span style="color: seagreen;"> **1. Intro** </span> 

Most of the confusion around randomness dissolves once one accepts a single uncomfortable fact: **the words "random," "unpredictable," "entropic," and "nondeterministic" do not name a single property of the world.** They name a family of distinct notions — some statistical, some algorithmic, some physical, some epistemic, some ontic — that only partially overlap. Treating them as synonyms is the root cause of confusion in cryptography, physics, and philosophy alike.

This article separates those notions cleanly, shows how they relate, identifies what is actually measurable and what is not, and draws the line between what is scientific and what is irreducibly philosophical.

---

## <span style="color: seagreen;"> **2. Statistical Randomness** </span> 

**Statistical randomness** is a property of a *sequence* (or of the distribution a sequence is drawn from), not of its source. A sequence is statistically random with respect to a family of tests if its empirical statistics — frequencies, correlations, block distributions, runs, spectral properties — are indistinguishable, within prescribed tolerances, from what one would expect of an i.i.d. uniform sample.

Crucially, statistical randomness is **test-relative**. A sequence passes or fails relative to a chosen battery. The digits of π pass essentially every statistical test ever devised, yet π is as deterministic as a sequence can be. AES in counter mode, seeded with a fixed key, produces output that passes every known polynomial-time statistical test — and is perfectly predictable to anyone holding the key.

### How We Measure It

The standard toolkits are NIST SP 800-22, Dieharder, TestU01 (Crush / BigCrush), and the German BSI's AIS 20/31 procedure A/B tests. Each applies a battery of hypothesis tests — monobit, runs, serial, spectral (DFT), linear complexity, approximate entropy, Maurer's universal test, and so on — each producing a p-value under the null hypothesis that the data is i.i.d. uniform. Pass rates are compared to expected distributions.

These tests tell you one thing only: **that the output looks uniform at the orders of statistical structure the tests examine.** They say nothing about the source.

---

## <span style="color: seagreen;"> **3. Unpredictability: A Different Beast** </span> 

Unpredictability is a property of a *source relative to an adversary*. A bit is unpredictable to adversary A at time t if A's best guess of the bit, given everything A knows, has success probability negligibly above one-half.

This is fundamentally different from statistical randomness:

- A deterministic PRNG can be statistically indistinguishable from uniform yet trivially predictable to anyone who has the seed.
- A biased coin (say 70/30) is statistically non-uniform but, after a single flip, still unpredictable in the sense that no observer can guess better than 70%.

Cryptography cares about unpredictability, not statistical randomness. Statistical randomness is necessary but vastly insufficient. This is why NIST-style black-box testing cannot, even in principle, validate a generator for cryptographic use — it cannot see the seed, the state, or the adversary's side information.

### The BSI White-Box Answer

The German BSI's AIS 20/31 framework recognizes this and mandates a **stochastic model of the entropy source**. Rather than treating the RNG as a black box and running statistical tests on its output, evaluators must model the physical noise source, justify the model from device physics, and derive a lower bound on **min-entropy per output bit** from that model. The statistical tests then serve only as a sanity check and as a health monitor for the deployed device.

This is the right methodological move: unpredictability cannot be certified by looking at outputs alone; it requires a white-box argument about the source. But — and this is critical — the model itself is an assumption. BSI white-box analysis does not *measure* unpredictability; it *bounds* it under an explicitly stated physical model. The certification is no stronger than the model.

---

## <span style="color: seagreen;"> **4. Entropy: Which One?** </span>  

"Entropy" is overloaded. The distinctions matter enormously in cryptography.

**Shannon entropy** H(X) = −Σ p(x) log p(x) measures the average uncertainty of a distribution. It is the right notion for communication theory (source coding theorem, channel capacity) and for data compression. It is the *wrong* notion for key material.

**Min-entropy** H∞(X) = −log max_x p(x) measures the probability of the *most likely* outcome. If H∞(X) = k, then no adversary can guess X with probability better than 2^−k. This is what you want for seeding a cryptographic extractor. A distribution can have high Shannon entropy and catastrophically low min-entropy (consider a distribution that is uniform on half its support and puts 1/2 mass on one point).

**Rényi entropies** H_α form a family parameterized by α, with Shannon at α→1 and min-entropy at α→∞. Collision entropy (α=2) governs universal hashing and leftover-hash-lemma arguments.

**Kolmogorov complexity** K(x) measures the length of the shortest program that outputs x. This is the algorithmic notion of randomness: a string is Martin-Löf random iff its prefixes have Kolmogorov complexity close to their length. K(x) is uncomputable — this is not a practical limitation but a theorem. We cannot, in general, measure the algorithmic randomness of a finite string.

**Thermodynamic entropy** S = k_B ln Ω (Boltzmann) or S = −k_B Σ p_i ln p_i (Gibbs) is, modulo the Boltzmann constant and the choice of macrostate coarse-graining, the same mathematical object as Shannon entropy applied to the microstate distribution given macroscopic constraints. Jaynes's maximum-entropy derivation of statistical mechanics makes this identity explicit and rigorous: thermodynamic entropy *is* information-theoretic entropy about microstates.

### Can We Truly Measure Entropy?

No — not in any absolute sense. Entropy is a property of a **distribution**, not of a sample. From a finite sequence of outputs we can only estimate entropy under modeling assumptions. Shannon-entropy estimators converge slowly and are badly biased; min-entropy estimators (NIST SP 800-90B) are conservative and rely on assumed source structure (IID vs non-IID tracks). Every entropy number on a datasheet is a number relative to a model.

This is the deep reason BSI insists on a stochastic model: **without a model, "entropy of this data" is not a well-defined quantity.**

---

## <span style="color: seagreen;"> **5. Hypothesis Testing: What It Actually Measures** </span>  

A statistical test computes a statistic T(x) on observed data x and asks: under the null hypothesis H₀ (typically "the data is i.i.d. uniform"), how unlikely is a value of T at least as extreme as the one observed? That tail probability is the p-value.

What hypothesis testing *actually* measures is **evidence against a specific null, in a specific direction, given a specific test statistic**. It does not measure:

- The probability that H₀ is true (that is a Bayesian posterior, not a p-value).
- Unpredictability.
- Entropy.
- Fitness for cryptographic use.

The limitations are structural. A test with statistic T is blind to any deviation orthogonal to T. A generator engineered to pass a specific battery will pass it and tell you nothing. Multiple-testing issues (running hundreds of sub-tests) produce expected false positives even for perfect generators. Asymptotic null distributions are approximations. And no finite battery can ever rule out adversarially constructed structure.

Statistical testing is a filter for gross defects, not a certification of quality.

---

## <span style="color: seagreen;"> **6. Epistemic vs Ontic Randomness** </span> 

Here the philosophy enters, and it cannot be avoided.

**Epistemic randomness** is randomness due to ignorance. The outcome is fixed by prior conditions, but we lack the information or computational power to predict it. Classical coin flips, dice, thermal noise in resistors, and the output of a chaotic but deterministic system are epistemically random. Laplace's demon, equipped with complete state information and unlimited compute, would see no randomness here at all.

**Ontic randomness** (sometimes called objective chance) is randomness that is a feature of the world itself, not of our knowledge. The question of whether any ontic randomness exists is the central question of the interpretation of quantum mechanics — and it is not settled by any experiment.

Unpredictability is always at least partly epistemic and relative: unpredictable *to whom*, *with what side information*, *with what compute budget*? A sequence unpredictable to a polynomial-time adversary may be trivially predictable to an unbounded one. This is precisely the gap between cryptographic pseudorandomness (Blum–Micali, Yao) and information-theoretic randomness.

---

## <span style="color: seagreen;"> **7. Quantum Indeterminacy — The Only Ontic Candidate?** </span> 

Quantum mechanics is the only place in physics where the mathematical formalism, on its face, delivers irreducible, objective chance. The Born rule prescribes probabilities for measurement outcomes, and the no-hidden-variables theorems (Bell, Kochen–Specker, PBR) rule out broad classes of deterministic underpinnings compatible with quantum predictions and locality.

But "irreducible randomness in QM" is interpretation-dependent:

- **Copenhagen / standard:** Measurement outcomes are genuinely, ontically random. Ontic randomness exists.
- **Many-worlds (Everett):** The global wavefunction evolves unitarily and deterministically; apparent randomness is self-locating uncertainty within a branch. No ontic randomness at the fundamental level.
- **De Broglie–Bohm (pilot wave):** Fully deterministic, with randomness arising from ignorance of initial particle positions (quantum equilibrium hypothesis). Purely epistemic.
- **QBism / relational:** Probabilities are degrees of belief of an agent; the question of "ontic" randomness is malformed.
- **Objective collapse (GRW, CSL):** Genuine stochastic dynamics added to the Schrödinger equation. Ontic randomness exists and is physical.

No experiment presently distinguishes these. Whether the universe contains irreducible randomness is, as of today, a **philosophical choice constrained by physics, not a scientific fact**. Device-independent quantum random number generators (based on loophole-free Bell-inequality violations) produce output certified to be unpredictable *assuming* no superdeterminism and no faster-than-light signaling — strong assumptions, but the best we have.

Beyond QM, classical chaos, thermal fluctuations, and cosmological initial conditions all contribute to *practical* unpredictability but not, on standard physics, to ontic randomness.

---

## <span style="color: seagreen;"> **8. Can Algorithms Increase Entropy?** </span> 

A deterministic algorithm applied to a fixed input cannot increase the Shannon or min-entropy of the joint system. This is a theorem: deterministic post-processing is a function, and for any function f, H(f(X)) ≤ H(X). If you start with a seed of k bits of min-entropy, no PRNG, hash, or cipher can give you more than k bits of unpredictability to an adversary who knows the algorithm.

What algorithms *can* do is **concentrate** entropy. A randomness extractor (e.g., Leftover Hash Lemma with universal hashing, or Trevisan's extractor) takes a source with m bits of min-entropy spread over n > m bits and produces ≈ m nearly-uniform bits. The total entropy does not rise; it is compressed into a smaller, higher-quality output. Similarly, a CSPRNG stretches k bits of seed entropy into arbitrarily many bits of *computational* pseudorandomness — indistinguishable from uniform to bounded adversaries, but containing no additional information-theoretic entropy.

This is the precise sense in which "an algorithm adds no entropy": entropy is conserved under deterministic maps, and pseudorandomness is a computational, not information-theoretic, resource.

---

## <span style="color: seagreen;"> **9. Thermodynamics, Information, and Landauer** </span> 

The Second Law of Thermodynamics says the entropy of an isolated system does not decrease. Via the Shannon–Gibbs identification, this is a statement about our *macroscopic* information about microstates: under generic dynamics, macroscopic observables become less informative about microscopic configurations.

Landauer's principle ties information to thermodynamics operationally: erasing one bit of information in a system at temperature T dissipates at least k_B T ln 2 joules of heat. Information is physical. Maxwell's demon is exorcised not by denying that information could in principle be used to decrease thermodynamic entropy, but by accounting for the thermodynamic cost of the demon's own memory operations.

The upshot is that Shannon entropy, thermodynamic entropy, and the arrow of time are not three separate things with the same name. They are three facets of a single structure: the statistics of microstates under coarse-grained observation.

---

## <span style="color: seagreen;"> **10. Information Preservation and the Rewindability of the Universe** </span> 

At the level of fundamental physics, unitary quantum evolution is **information-preserving and reversible**. Given the exact global state and the Hamiltonian, past and future are mutually determined. The apparent irreversibility of thermodynamics emerges from coarse-graining and low-entropy initial conditions (the Past Hypothesis), not from a fundamental asymmetry in the laws.

This is why the black hole information paradox is a paradox: semiclassical calculations (Hawking) suggested information loss, which would violate unitarity. The current consensus — supported by AdS/CFT, the Page curve, and recent entanglement-wedge computations — is that information *is* preserved even through black hole evaporation, albeit scrambled beyond any practical recovery.

So is the universe "fully rewindable"? Under unitary QM: yes, in principle, at the level of the universal wavefunction. In practice: no, because (i) we never have the exact global state, (ii) decoherence distributes information into astronomically many degrees of freedom, and (iii) under objective-collapse or Copenhagen interpretations, measurement is genuinely irreversible.

As for the future: if the underlying dynamics is unitary and deterministic (MWI, Bohm), the future is fixed given the present state, though not knowable to any finite agent. If collapse is real (GRW, Copenhagen), the future is ontically open. **Whether there is inherent indeterminacy in the future is the same question as whether ontic randomness exists** — and, again, physics has not answered it.

---

## <span style="color: seagreen;"> **11. Interrelations — A Compact Map** </span> 

- **Statistical randomness** is a property of distributions/sequences relative to a test family.
- **Unpredictability** is a property of a source relative to an adversary's knowledge and compute.
- **Entropy** (Shannon, min-, Rényi) quantifies unpredictability of a distribution to an observer who knows only the distribution.
- **Kolmogorov complexity** quantifies the irreducibility of an individual string under any computable description.
- **Thermodynamic entropy** is Shannon entropy of microstates given macroscopic constraints, with k_B converting nats to joules per kelvin.
- **Information** is the dual of entropy: information gained equals entropy reduced.
- **Determinism vs indeterminism** is the question of whether the laws of physics uniquely fix the future from the present — a question about the laws, not about our knowledge.
- **Uncertainty** is our epistemic state; **indeterminacy** is (if it exists) a feature of the world.

Unpredictability is relative; entropy is model-relative; statistical randomness is test-relative; algorithmic randomness is uncomputable; thermodynamic entropy is coarse-graining-relative; ontic randomness is interpretation-dependent. Every one of these concepts has a parameter that must be specified before the concept is well-defined. Confusion arises almost entirely from leaving those parameters implicit.

---

## <span style="color: seagreen;"> **12. Science and Philosophy: Where the Line Runs** </span> 

**Scientific and measurable:**
- Statistical properties of finite sequences (under a test family).
- Entropy estimates (under a source model).
- Predictability by specific adversary classes (under complexity assumptions).
- Quantum probabilities (operationally, via the Born rule).
- Thermodynamic entropy differences (via calorimetry).

**Philosophical, not empirically decidable with current physics:**
- Whether randomness is ontic or purely epistemic.
- Which interpretation of quantum mechanics is "correct."
- Whether the universe is fundamentally deterministic.
- Whether the future is ontically open.
- Whether probability is frequency, propensity, or degree of belief.

Philosophy is not a placeholder for "things science hasn't gotten to yet." In the case of determinism and the interpretation of probability, philosophy is where the actual work of clarifying concepts happens, and no amount of additional experimental data will close the questions unless those concepts are first sharpened.

---

## <span style="color: seagreen;"> **13. A Cryptographer's Practical Synthesis** </span> 

For someone building or evaluating cryptographic systems, the conclusions are concrete:

1. Never trust black-box statistical testing as evidence of cryptographic quality. It detects only gross failures.
2. Require a **white-box stochastic model** of any entropy source, in the BSI sense. Certification is an argument from physics plus conservative min-entropy bounds, not a p-value.
3. Track **min-entropy**, not Shannon entropy, for all seeding operations. Use proven extractors (leftover hash lemma, HKDF-Extract) to concentrate raw entropy into uniform key material.
4. Treat CSPRNG output as computational pseudorandomness — unpredictable to bounded adversaries under unbroken assumptions, and containing no more information-theoretic entropy than the seed.
5. When you care about long-term unpredictability against unbounded adversaries, your only recourse is a physical entropy source with a trusted model, ideally device-independent quantum where the threat model justifies the cost.
6. Accept that "how random is this data?" is not a well-posed question. "How much min-entropy does this source produce per output, under model M, with confidence 1−α?" is.

---

## <span style="color: seagreen;"> **4. Closing** </span> 

There is more to randomness than any one discipline can hold. Statistics gives you indistinguishability; complexity theory gives you hardness; information theory gives you entropy; thermodynamics gives you the arrow of time; quantum mechanics gives you the only known candidate for ontic chance; and philosophy gives you the conceptual scaffolding without which none of the above has a clear meaning. The confusion you began with is not a personal failing — it is the natural result of a word ("randomness") that encodes at least six genuinely distinct technical ideas.

Clarity comes not from finding the "true" definition, but from always specifying **which randomness, relative to whom, under what model, and in what sense**. Once those parameters are fixed, every question in this paper has a precise and often surprisingly clean answer. Leave them implicit, and no answer is possible.
