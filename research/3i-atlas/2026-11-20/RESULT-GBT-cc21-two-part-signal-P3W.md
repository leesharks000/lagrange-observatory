# GBT cc21, the two-part signal that resolves only with a third (P3W, P3W-B): both validations failed; no telescope data read; no lead

**2026-11-21.** The author's question: a tripartite tone that looks like noise until its third is added. Two components whose phases wander together, so that their sum or difference phase stays fixed, are noise to every earlier test of the search; a steady third at the sum or difference frequency would lock the triple. The test is the phase stability of the pair across segments, on C21's first 32 frames (saved by N1625). Two plans were frozen; each stopped at its own validation, as frozen.

Canonical runs, frozen plans, code, hashes: [PLAN-P3W.md](https://github.com/leesharks000/alexanarch/blob/main/rebuild/3i-atlas-signal-search/claude/run-2026-11-03/r13/M/P3W/PLAN-P3W.md), [RESULTS-P3W.md](https://github.com/leesharks000/alexanarch/blob/main/rebuild/3i-atlas-signal-search/claude/run-2026-11-03/r13/M/P3W/RESULTS-P3W.md), [P3W-PRODUCTS.sha256](https://github.com/leesharks000/alexanarch/blob/main/rebuild/3i-atlas-signal-search/claude/run-2026-11-03/r13/M/P3W/P3W-PRODUCTS.sha256), [p3w.py](https://github.com/leesharks000/alexanarch/blob/main/rebuild/3i-atlas-signal-search/claude/run-2026-11-03/r13/M/P3W/p3w.py); [PLAN-P3W-B.md](https://github.com/leesharks000/alexanarch/blob/main/rebuild/3i-atlas-signal-search/claude/run-2026-11-03/r13/M/P3W/PLAN-P3W-B.md), [RESULTS-P3W-B.md](https://github.com/leesharks000/alexanarch/blob/main/rebuild/3i-atlas-signal-search/claude/run-2026-11-03/r13/M/P3W/RESULTS-P3W-B.md), [P3W-B-PRODUCTS.sha256](https://github.com/leesharks000/alexanarch/blob/main/rebuild/3i-atlas-signal-search/claude/run-2026-11-03/r13/M/P3W/P3W-B-PRODUCTS.sha256), [p3wb.py](https://github.com/leesharks000/alexanarch/blob/main/rebuild/3i-atlas-signal-search/claude/run-2026-11-03/r13/M/P3W/p3wb.py).

The text below is RESULTS-P3W and RESULTS-P3W-B as committed there.

---


Run 2026-11-21 under PLAN-P3W (sha256 bd3d128b…). The plan's rule: "If not accepted, the run stops at validation." It was not accepted, and no telescope data were read (validation.json).

## Validation

| form | 0.1 | 0.25 | 0.5 |
|---|---|---|---|
| sum within X | p 0.475 | p 0.90 | **p 0.025, pair 137–301, 3.07×** |
| difference within X | p 0.275 | p 0.85 | **p 0.025, pair 137–301, 3.09×** |
| sum across feeds | p 0.325 | p 0.825 | **p 0.025, pair 137–301, 3.00×** |
| difference across feeds | p 0.025, wrong pair | p 0.85 | **p 0.025, pair 137–301, 3.02×** |

Amplitudes are the tone's per-bin amplitude over the noise's. "×" is the score over the median surrogate maximum.

- Noise-only: 6 of 20 trials have some family at p ≤ 0.05 (XY+ 3, XY− 2, Y+ 1). That is 6 of 120 family tests, 5% per family.
- Stationary tone: X− p = 0.025; the other families 0.125–0.925.
- Uncoupled pair: no family at p ≤ 0.05 (0.10–0.90).

## Why it failed

1. **Sensitivity is at 0.5, not 0.25.** For a coupled pair at per-bin amplitude ratio a, the expected coupling is about (√π/2 · a)²: about 0.05 at 0.25. The noise maximum over about 130,000 allowed pairs and 4,096 segments is about √(ln(2.6×10⁵)/4,096) ≈ 0.055. At 0.5 the coupling is about 0.20, well clear. The plan's bar was set below what this length of data can reach. At 0.5 each tone carries a quarter of its bin's noise power: invisible in power, below the tonal mask.
2. **The false-alarm bar was per trial; it should have been per family.** With six families, about 26% of noise trials show one family at p ≤ 0.05 by chance. The observed per-family rate, 5%, is nominal.
3. **Steady tones leak into the difference form.** A stationary tone's leakage reaches many bins, each with the tone's own phase advance per segment. Their difference phases are therefore locked, and the 2× power mask does not catch sidelobes below it. In a band with carriers, the difference families would fire on interference.

## What a second plan would change

Frozen before any data, if the author gives the word:
- **Acceptance at 0.5:** the validated sensitivity.
- **False alarms per family:** at most 10%.
- **Sidelobe exclusion:** bins with a steady phase advance of their own excluded. That is any bin whose self-coherence |mean P[s+1,k]·conj(P[s,k])| is significant, at analytic p ≤ 10⁻³, which removes tone leakage wherever it reaches.
- **Validation repeated** with the stationary tone, a set of tones, and the coupled pair at 0.5.

---


Run 2026-11-21 under PLAN-P3W-B (sha256 eca84bad…), with p3wb.py (sha256 019f17ed…) over p3w.py. The plan's rule: "If not accepted, the run stops at validation." It was not accepted, and no telescope data were read (validationB.json; 884 s).

## Validation

| form | 0.25 | 0.5 |
|---|---|---|
| sum within X | p 0.525, pair 282–341, 0.99× | **p 0.025, pair 137–301, 3.11× (recovered)** |
| difference within X | p 0.3, pair 11–370, 1.03× | **p 0.025, pair 137–301, 3.30× (recovered)** |
| sum across feeds | p 0.025, pair 137–301, 1.22× (recovered) | **p 0.025, pair 137–301, 3.13× (recovered)** |
| difference across feeds | p 0.85, pair 489–405, 0.96× | **p 0.025, pair 137–301, 3.11× (recovered)** |

Amplitudes are the tone's per-bin amplitude over the noise's. "×" is the score over the median surrogate maximum.

| criterion | rule | result | |
|---|---|---|---|
| four forms at 0.5 | each p ≤ 0.05 at the injected pair | all four, p 0.025 at 137–301 | met |
| noise only | ≤ 12 of 120 family tests at p ≤ 0.05 | 4 of 120 | met |
| stationary tone | no family at p ≤ 0.05 | X+ 0.45, X- 0.125, Y+ 0.75, Y- 0.775, XY+ 0.775, XY- 0.15 | met |
| five stationary tones | no family at p ≤ 0.05 | X+ 0.675, X- 0.025, Y+ 0.9, Y- 0.05, XY+ 0.75, XY- 0.05 | **not met** (X−, Y−, XY−) |
| uncoupled pair at 0.5 | no family at p ≤ 0.05 | X+ 0.4, X- 0.425, Y+ 0.7, Y- 0.4, XY+ 0.075, XY- 0.35 | met |

At 0.25 the sum across feeds was recovered (p 0.025, 1.2×); the other three were not. 0.25 is reported, not required.

## Why it failed

1. **The exclusion works for one tone and not for five.** The single stationary tone, which flagged the difference form under PLAN-P3W (X− p 0.025), no longer flags anything (lowest p 0.125). With five tones, all three difference families flag (X− 0.025, Y− 0.05, XY− 0.05), and no sum family does.
2. **Most likely mechanism, not tested here.** Each bin is tested for a steady phase advance on its own, at p ≤ 10⁻³. Far from a tone its leakage is weak, so its self-coherence stays under that bar and the bin is kept. The difference of two steady advances is itself steady, so pairs of such bins, one from each tone's leakage, have locked difference phases. The family statistic sums over many such pairs, so it can find a lock that no single-bin test can see. With one tone there are no cross-tone pairs, which fits the stationary control passing.
3. **What it means for the data.** The bands of this search carry steady carriers, among them the 1546.98 MHz line (C4850/READING-C4850-line-1546977840.md). Where more than one stands in a band, the difference families would fire on interference, which is what this control exists to catch.

## What stands

- The sum families pass every control, and they are recovered at 0.5 in both forms.
- Noise-only false alarms are within the bar (4 of 120, about 3% per family).
- No telescope data were read under PLAN-P3W or PLAN-P3W-B.

Products: PLAN-P3W-B.md, p3wb.py, validationB.json and this file, hashed in P3W-B-PRODUCTS.sha256. valB.log is the run's console log and is not hashed.
