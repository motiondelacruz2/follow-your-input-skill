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

## Status

Each practice went through iterative adversarial testing (drafted, stress-tested against deliberately tricky prompts, revised, retested) before being combined. That process surfaced and fixed several real behavioral bugs, not just wording issues — see the "Relationship to the other two practices" sections in each SKILL.md for specifics on the ordering dependencies this uncovered.

This is a live framework, not a finished spec. Feedback and adversarial test cases welcome.
