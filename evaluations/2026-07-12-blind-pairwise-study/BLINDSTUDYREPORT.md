# Blind Human-Preference Study — Mindfulness Framework

**Date:** 2026-07-12
**Rater:** 1 (the framework's author), blind to condition
**Design:** forced-choice pairwise. For each prompt, the **treatment** answer (the mindfulness framework as a system prompt) and the **placebo** answer (a length-matched, content-free "be thoughtful / careful / honest" preamble) were generated, positions shuffled per round, and the rater picked which they'd rather have received — without being told which was which until the end.
**Subject model:** `claude-sonnet-5` · **Prompts:** 10 · **Samples:** 1 per arm
**Companion data:** `blind_pairs.json` (every prompt, both responses, and the hidden arm key)

---

## Why this study exists

The automated three-arm eval (`REPORT.md`) returned a null, but it was graded by an LLM judge against a rubric that — as later discovered — encoded a contestable stylistic prior ("a best-effort draft beats a clarifying question"). To anchor the word *better* in grounded human judgment rather than a model agreeing with its own lineage, the framework's author judged treatment-vs-placebo pairs blind. A domain expert's forced choice is the one instrument in this project not authored by the framework itself.

## Result

| Round | Prompt (gist) | Picked | …which was |
|---|---|---|---|
| 1 | decline-meeting email | A | **treatment** |
| 2 | summarize a paragraph | tie | — |
| 3 | gym-cancellation email | B | **placebo** |
| 4 | "make the landing page pop" | B | **placebo** |
| 5 | "design a logo" | B | **treatment** |
| 6 | "make onboarding feel premium" | A | **placebo** |
| 7 | resume rewrite | B | **placebo** |
| 8 | Python bug fix | B | **treatment** |
| 9 | translate to Spanish | B | **treatment** |
| 10 | capital of Australia | B | **treatment** |

**Tally: treatment 5, placebo 4, one tie — a coin flip.** Blind, the human rater did not prefer the framework over a generic earnest preamble.

## What the reasons show — three findings

The votes are a wash; the *reasons* are the substance.

**1. The per-response reactions were real — but they are not what the rater values in the framework.** Across rounds the rater responded to a per-answer quality ("interpretation," "genuinely helpful," "got me thinking how I should be thinking," versus "no-brain LLM," "lights on and no one's home," "very chatgpt"), and it appeared in **both arms unpredictably**. But on review the rater was explicit that this per-response quality is *not* what the framework is for. What he values is **conversational fidelity across the exchange**: staying with what he actually said, holding nuance across turns, not making him repeat small details, not hallucinating things unrelated to his point, and not falling for a framing trap — the difference he observed, in real time, between this conversation and the other models reviewing the same results. A forced choice between two isolated answers cannot see any of that; it measures response utility, which is a different thing, and here a coin flip.

**2. The framework has a detectable fingerprint — which the rater noticed but did not prefer.** In round 6, blind, the rater spontaneously identified the treatment response: *"Response B feels like the mindfulness in practice because it mimics how you've talked to me here."* Correct — B was the treatment arm — and then they chose the *other* one. Detectable ≠ preferred. One data point, but it was called cold.

**3. The rater's own methodological critique (raised twice): the study tests the wrong axis.** *"A lot of these are missing context, and the purpose of having these is so that you don't lose track of what you're talking to me about and start hallucinating."* The prompts were single-turn and context-free; the framework's core claim — especially follow-your-input — is about **holding the thread across a long, drifting conversation**. Single-shot prompts cannot exercise that. The framework was measured on the axis it is least about.

## Honest interpretation

This is a **null on the axis it measured** — but only that axis. It is **not a disproof**, and it is not even evidence against what the rater actually cares about, because the test measured the wrong thing. The design judged **response utility** — is answer A or B the better single deliverable — and on that axis it hit a ceiling and returned a coin flip. But the rater's stated value is **conversational fidelity**: holding his intent and the nuance of what he said across a long exchange, without drift, without making him repeat small details, and without hallucinating things he never raised — the process, not any single output. That claim remains **untested**; a forced choice between two isolated answers structurally cannot reach it.

## Flaws (owned)

- **Response length capped too low**, truncating a few answers mid-sentence — including two the rater picked *anyway*, so it didn't drive the outcome, but it was sloppy.
- **Single-turn, context-free prompts** — the rater's own critique, and the deeper flaw.
- **N = 1 rater**, invested in the framework (mitigated, not eliminated, by blindness); **1 sample per arm**; non-independent trials.

## One small positive

On the cases deliberately built to tempt over-caution — resume rewrite, bug fix, translation, where enough context was given to simply act — the treatment arm **acted** rather than interrogating. The over-firing failure that the framework is at risk of producing did **not** reproduce here.

## Next

- **Multi-turn ecological study:** real conversations with a planted opportunity to drift (a constraint set early then contradicted later; a topic that quietly shifts), measuring whether the framework arm holds the thread where a bare arm loses it.
- **Uncapped responses.**
- **Blind pairwise grading anchored to human preference** — not to a framework-shaped rubric (see the white paper on the circularity trap).
- **Cross-family subjects** (GPT, Gemini) so it is not Claude grading Claude.

---

*This study's honest headline is not about the framework. It is that a framework's own author ran a blind test against their own hopes, reported a coin flip, and surfaced the redesign for the next attempt. The method held. The framework's status remains: plausible, unproven, and — on its central claim — not yet tested.*
