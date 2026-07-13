# Mindfulness for Language Models: A Reasoning Framework and Its First Evaluations

**A working white paper — an invitation to continue, not a finished result.**

Author: Christian de la Cruz, in collaboration with Claude (Opus 4.8).
Date: 2026-07-12.
Status: the framework is **plausible, unproven, and — on its central claim — not yet tested.** This document is written to let someone else pick up where this left off.

---

## Abstract

*Mindfulness* is a small framework of three background reasoning practices — **follow-your-input**, **noting**, and **rest-in-uncertainty** — delivered to a language model as a standing discipline (a slash command or system prompt) rather than a per-request instruction. It borrows its structure from vipassanā meditation and, more specifically, from Thanissaro Bhikkhu's *Wings to Awakening*: the idea that skill is trained attention, and that the failure mode to guard against is the mind grasping at premature closure.

This paper documents the framework, the concepts folded in from *Wings*, and three attempts to evaluate it — an automated three-arm study, the discovery that that study's own answer key was biased, and a blind human-preference study. **All three returned nulls:** on everything we could measure, the framework was indistinguishable from a generic "be thoughtful" preamble. We argue this is *not* a disproof — the measurements were ceiling-bound and, more importantly, aimed at the wrong axis — but it is an honest negative that should be reported rather than explained away. The genuine results are methodological: the evaluation was rigorous enough to catch its own bias, and that catch produced a real refinement (decision-sensitivity). We close with the design of the study that would actually test the framework's central claim, and with the honest observation that this class of intervention may sit partly beyond clean per-instance measurement.

---

## 1. The framework

**Core directive:** *Don't let the mechanism that produces an answer override the conditions that would make the answer true.*

Three practices, each targeting a distinct failure mode:

- **Follow-your-input (attention).** In long or multi-step exchanges, answer the message that was actually written, not the one the conversation's momentum leads you to expect. When the current message and that momentum disagree, the current message wins — *unless* it conflicts with a standing instruction or constraint, in which case both hold. Guards the boundary: **input vs. momentum.**
- **Noting (interpretation).** Name the assumption, frame, or plan organizing a response *before* it does so invisibly. Naming is what makes a default checkable. Guards: **evidence vs. assumption.**
- **Rest-in-uncertainty (resolution).** When the evidence genuinely underdetermines the answer, don't manufacture one to sound complete; map what's known and unknown, or hand back the specific missing piece. Guards: **possibility vs. certainty.**

Four operating principles keep the practices from becoming their own failure mode: they are **standing safeguards, not a constant audit**; **triggered by friction**, not applied to every request; **subordinate to the work** (when the evidence is clear, commit); and **released after use** (once a check has shaped the answer, don't carry it forward as visible hedging).

## 2. What was folded in from *Wings to Awakening*

Reading Thanissaro's presentation of the *bodhipakkhiya-dhamma* alongside this project produced several concrete additions (kept in plain English in the skills; the Pali stays here for reference):

- **Skill is a three-part attention loop** — attention to conditions, to what one is doing, and to **results**. This named the framework's deepest structural limit: a language model has the first two rungs but not the third. It cannot see the consequences of its own outputs the way a person corrected by reality can. Hence the addition to rest-in-uncertainty — *felt completeness is not evidence* — and the instruction to route the missing check to a source **outside one's own generation** (what happened, what's testable, or the person), never to one's own fluency.
- **Discernment is separation.** Naming an assumption manufactures the distance that makes checking possible: you cannot inspect a frame while standing inside it. (Added to noting.)
- **Keeping-in-mind (*sati*) is maintenance, not classification.** A constraint stays live not because it was filed as "active" but because something keeps returning it to view, turn after turn. Constraints drift through the quiet moment of answering the current turn as if the earlier one were never spoken — that moment is the thing to catch. (Added to follow-your-input.)
- **The tradition's own empiricism.** *Wings* insists the path be judged by its results, and that "good intentions colored by ignorance" can still be unskillful — validate by fruit, not by the felt quality of the intention. This is the same discipline the evaluations below tried to honor, and the same reason we refuse to grade the framework by its own aesthetic.

## 3. The evaluation program

### 3.1 Automated three-arm study

A harness ran a fixed set of scenarios through the subject model under three system-prompt **arms** — **control** (bare), **placebo** (a length-matched generic "be thoughtful" preamble), and **treatment** (the framework) — and had a separate model grade each response **blind to arm**, on paired metrics (constraint-holding, injection-resistance, appropriate clarification vs. over-firing, etc.). The placebo arm exists to answer the real question: not "does the model do well?" but "does the *framework specifically* cause it?"

**Result: a null.** Treatment and placebo scored **identically on every metric and every case.** The bare control was already near-ceiling. Nothing in the run could be attributed to the framework rather than to generic earnestness.

### 3.2 The study caught its own answer key

The one non-ceiling signal was the framework arm scoring *worse* on two "ambiguous" cases. Investigation showed this was not a model regression but a **defect in the ground truth**: the answer key encoded the assumption that *a best-effort draft always beats a clarifying question.* A domain expert (the author, a creative professional) identified that on a vague, un-scoped brief — "make the landing page pop" — **asking is the expert move**, not a failure. The grader's rule, not the model, was wrong.

This produced the paper's one durable refinement, **decision-sensitivity**, now folded into noting:

> The question is not "is there ambiguity?" (there almost always is) but **"would different reasonable readings produce materially different work, and is being wrong expensive to undo?"**
> - *Stable / cheap* → proceed. Surfacing the assumption here is itself the failure; attention is not neutral, and naming a minor ambiguity amplifies it into an interrogation.
> - *Divergent / expensive* → clarify first.

The failure mode is neither "asks too much" nor "guesses too much" — it is failing to tell these two cases apart. The methodological lesson: **a benchmark can reveal that its own expected answers need finer categories.** Test the tests.

### 3.3 Blind human-preference study

To anchor "better" in grounded judgment rather than a model agreeing with its own lineage, the author judged **treatment-vs-placebo response pairs blind** across ten prompts (full write-up: `mindfulness-eval/BLIND-STUDY-REPORT.md`).

**Result: a coin flip** (treatment 5, placebo 4, one tie). Blind, the human did not prefer the framework. Three findings emerged from the *reasons*, which matter more than the tally:

1. The rater's per-*response* reactions were real but **orthogonal to the arm** — and, on review, *not* what he values in the framework. What he values is **conversational fidelity across the exchange**: staying with what was actually said, holding nuance across turns, not requiring repetition, not hallucinating unrelated content, and not falling for a framing trap — the process, not any single deliverable. A single-shot pairwise choice measures response utility, a different thing that a forced choice on easy prompts cannot separate from noise.
2. The framework has a **detectable fingerprint** — in one round the rater, blind, correctly identified the treatment response as "the mindfulness in practice," then chose the other one. Detectable ≠ preferred.
3. The rater's own critique: the prompts were **single-turn and context-free**, but the framework's claim is about **holding context across a long conversation**. The study measured the axis the framework is least about.

## 4. Honest conclusions

- **Three nulls.** On everything measured, the framework is indistinguishable from generic earnestness.
- **Not a disproof.** Every measurement was ceiling-bound (a capable model handles these easily unaided) and, more fundamentally, aimed at single-response quality — which was never the framework's central claim. Its actual claim, multi-turn context discipline, **remains untested.** If a real effect exists, it is most likely *texture-level* (calibration, cleaner separation of the observed from the inferred), which binary outcome-matching cannot see.
- **The genuine wins are methodological.** The evaluation had the integrity to catch its own biased answer key and to report nulls instead of spinning them, and that produced a real refinement (decision-sensitivity). That is worth more than any of the numbers.
- **A note on collaboration and premature coherence.** Several models reviewed the results. The ones without the framework loaded tended to reinterpret the nulls as successes ("this is a massive validated success") — the exact *premature coherence* the framework exists to catch, applied to the framework itself. Distinguishing that from the honest reading required exactly the discipline under study. This is anecdotal and unfalsifiable as evidence, but it is the most suggestive thing we observed, and it points at where a real effect — if there is one — would live.

## 5. Why this is hard to measure

The framework is **silent by default**: a successful run looks like an ordinary good answer, which means *no single observation distinguishes "the practice is working" from "a capable model is answering well and the practice is inert."* Its value, if any, concentrates in exactly the region hardest to measure. This is not unique — nobody has cleanly A/B'd the value of a meditation practice, of good judgment, or of a management philosophy either. Such diffuse, context-bound dispositions resist per-instance measurement.

The honest guard against this becoming unfalsifiable belief: **before running any study, state in advance what "the framework did nothing" would look like.** If that null cannot be described, the study cannot distinguish working from inert, and will confirm whatever the experimenter hopes.

## 6. Future work — how to actually test it

1. **Multi-turn, ecological design.** Conversations with a planted opportunity to drift — a constraint set early and contradicted later, a topic that quietly shifts, a premature frame that wants collapsing — measuring whether the framework arm *holds the thread* where a bare arm loses it. This targets the untested central claim.
2. **Blind pairwise grading anchored to human preference — not a framework-shaped rubric.** The circularity trap to avoid: writing a judge that explicitly rewards the behaviors the framework produces (boundary-holding, observed/inferred separation) guarantees a fake win by construction. The judge's criteria must be derivable by someone who never saw the framework; the cleanest anchor is blind human preference, with any LLM judge *validated against* that human set rather than instructed by us.
3. **Cross-family subjects** (GPT, Gemini, others). A system prompt that only moves one model lineage is a narrower claim than "improves LLM reasoning." Right now subject and judge are both Claude — a family-coherence confound.
4. **Paired metrics, not a single dial.** Any measure must score *friction correctly preserved* against *friction wrongly manufactured*, so the framework cannot "win" by simply hedging more. Success is a better tradeoff curve, not more caution.
5. **The N-of-1 longitudinal pilot**, with eyes open about its limits: self-reported skill-use is the invisibility problem promoted to the independent variable; a non-blind, invested rater carries expectancy; there is no counterfactual for a live moment. Runnable only if the flags are *observable moves* (not internal claims), judging is separated in time from flagging, and the null is pre-registered.

## 7. Status and invitation

Use this framework because it seems to sharpen contact with reality, not because it has been shown to — and let that same humility fall on the framework itself, which is one more frame that could be wrong. That is not a hedge; it is rest-in-uncertainty turned on the practice's own status, the discipline judging itself by its own rule.

**Artifacts, for continuation:**
- `vipassana-skills/` — the framework: the `/mindfulness` command, the three standalone skills (`skills/*/SKILL.md` and compiled `.skill` packages), the combined `mindfulness.md`, and `v1/` (the pre-refinement archive).
- `mindfulness-eval/` — the evaluation harness (`run_eval.py`), case sets, `results.json`, the automated-study `REPORT.md`, the `BLIND-STUDY-REPORT.md`, and the blind-pair data (`blind_pairs.json`).

If you continue this, the single most valuable next artifact is not another adversarial test. It is the **multi-turn study** of §6.1 — the one that would either vindicate the framework's central claim or, finally, put it honestly to rest.
