# Mindfulness

Three reasoning practices for AI assistants, built as Claude Skills and packaged as a Claude Code slash command. Each one targets a specific, recurring failure mode in how language models generate answers — not by adding rules, but by naming the mechanism that causes the failure and giving the model something concrete to check.

New here? Read **[ONE-PAGER.md](./ONE-PAGER.md)** first — it explains the three problems this solves in plain language, no background needed.

## What's in this repo

| Path | What it is |
|---|---|
| `ONE-PAGER.md` | Plain-language explainer — start here |
| `mindfulness.md` | The full combined framework (all three practices + wrapper) |
| `commands/mindfulness.md` | Claude Code slash command — `/mindfulness` loads all three at once |
| `skills/follow-your-input/SKILL.md` | Standalone skill — attention / context drift |
| `skills/noting/SKILL.md` | Standalone skill — unexamined assumptions |
| `skills/rest-in-uncertainty/SKILL.md` | Standalone skill — premature certainty |

## The three practices

**Follow Your Input** — catches the model answering the conversation it expects instead of the message actually in front of it. Most likely to misfire in long conversations, multi-step agentic tasks, or any time momentum has built up.

**Noting** — catches an unexamined assumption (tone, audience, scope, format) quietly organizing a response before it's ever been checked against the evidence. Doesn't need a long conversation — can happen on the very first message.

**Rest in Uncertainty** — catches the model manufacturing a confident, tidy answer when the evidence genuinely doesn't support one yet. Not an argument for more hedging; it's about collapsing ambiguity only when it's actually earned.

All three share one line as their common thread:

> Don't let the mechanism that produces an answer override the conditions that would make the answer true.

## How to use it

**⚠️ If you use the skills route (Option B below), install all three skills together — not just one or two.** They're built as a set: noting and rest-in-uncertainty each contain an internal fallback for cases where the other practices didn't fire, precisely because a partial install leaves real gaps the design assumes are covered. Options A and C aren't affected by this — they already load all three at once by definition.

**Option A — Claude Code slash command (recommended if you use Claude Code):**

```bash
mkdir -p ~/.claude/commands
cp commands/mindfulness.md ~/.claude/commands/mindfulness.md
```

Then type `/mindfulness` in any Claude Code session to load all three practices at once for that session.

**Option B — Individual skills (install all three, not a subset):** copy **all three** folders under `skills/` — `follow-your-input`, `noting`, and `rest-in-uncertainty` — into your own Claude Skills directory. Each one triggers contingently, based on relevance to the current message, rather than loading all three up front — but the three are meant to function as a matched set. Installing only one or two breaks the dependencies described in each SKILL.md's "Relationship to..." section.

**Option C — Persistent instructions:** paste `mindfulness.md` into a Project's custom instructions, a `CLAUDE.md` file, or a system prompt if you want the framework always active rather than invoked on demand. This is the most expensive option token-wise (the whole document loads on every message) but it's the only one that guarantees all three practices are co-present without relying on relevance-matching or a manual command.

## Why three separate things instead of one

Each practice targets a different point in the reasoning pipeline — attention, interpretation, and resolution — and each has a different failure signature (one needs conversational history to misfire, one doesn't need any history at all, one depends on the other two already being correct). Collapsing them into a single instruction tends to blur those distinctions and makes the individual failure modes harder to catch. Keeping them separate, callable independently or together, preserves the distinction while still letting them combine cleanly.

## Where this comes from

The framework borrows its structure from vipassanā meditation, and more specifically from Thanissaro Bhikkhu's presentation of the Buddha's teaching in [*Wings to Awakening: An Anthology from the Pali Canon*](https://www.accesstoinsight.org/lib/authors/thanissaro/wings/index.html) — in particular the idea that skill is trained attention, and that the failure mode to guard against is the mind grasping at premature closure. This is a statement of inspiration and lineage, not a claim that the framework's specific mechanics map rigorously onto that text — see [WHITEPAPER.md](./WHITEPAPER.md) §2 for the concrete concepts folded in from it.

## Status: tested, and still mostly unproven

This has moved past "untested framework pitch." Two empirical studies have been run, and it's worth being direct about what they found: **both returned nulls.** On every automated and human-judged metric measured so far, the framework has been indistinguishable from a generic "be thoughtful" placebo.

That is not the same as "it doesn't work" — both studies were, by their own design and admission, aimed at axes the framework isn't really about (single-response quality, largely ceiling-bound), rather than its actual central claim (holding conversational thread and fidelity across a long, drifting exchange). Neither study is a disproof. Neither is a validation. Read the full, unspun writeups before citing either result as evidence of anything:

- **[Evaluation: v2 First Empirical Test](https://github.com/motiondelacruz2/Mindfulness/wiki/Evaluation:-v2-First-Empirical-Test)** (wiki) — an automated 3-arm study (control / placebo / treatment), blind-graded by a separate model. Treatment and placebo scored identically on every metric. The most useful finding was methodological: the eval caught a bug in its own answer key, which produced a real refinement (the Type-A/Type-B decision-sensitivity distinction, now folded into `noting`).
- **[Evaluation: Blind Pairwise Study](https://github.com/motiondelacruz2/Mindfulness/wiki/Evaluation:-Blind-Pairwise-Study)** (wiki) — a blind human-preference study (N=1 rater, the framework's author), forced-choice treatment vs. placebo across 10 prompts. Result: a coin flip. The rater's own critique, taken seriously: single-turn prompts can't test a claim about holding context across a conversation.
- **[WHITEPAPER.md](./WHITEPAPER.md)** — the full write-up tying the framework, its meditation-derived concepts, and both evaluations together, plus the design of the study that would actually test the central claim.
- Raw reports and transcripts for each study live under [`evaluations/`](https://github.com/motiondelacruz2/Mindfulness/tree/main/evaluations).

Each practice also went through iterative adversarial testing (drafted, stress-tested against deliberately tricky prompts, revised, retested) before being combined — see the "Relationship to the other two practices" sections in each SKILL.md for the ordering dependencies that surfaced.

This is a live framework, not a finished spec, and — per its own third practice — its status should be held the same way: plausible, unproven, and honestly reported either way. Feedback and adversarial test cases welcome.
