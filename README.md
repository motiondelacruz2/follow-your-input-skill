# Follow Your Input — a Claude Skill

This is a "skill" for Claude — a small instruction file that changes how Claude reasons, rather than a tool that produces documents or runs code. It's a skill built by Anthropic (available in Claude Code and Cowork); this repo is just a copy shared for others to use.

## What it does

Claude conversations can run long: many back-and-forth turns, or long multi-step tasks where Claude is calling tools over and over. The longer that history gets, the easier it is for Claude to drift — to keep answering based on the shape of the conversation so far, instead of paying full attention to the message the user just sent.

This skill is a standing reminder for Claude to treat the user's **most recent message** as the main thing to respond to, while still respecting instructions, preferences, and facts established earlier in the conversation. It doesn't produce a file or a report. Instead, it changes Claude's reasoning habit: notice when you might be running on autopilot, and check back against what the user actually just said before answering.

Think of it like a meditation technique, but for an AI: in meditation, you keep gently returning your attention to the breath whenever your mind wanders. This skill asks Claude to do the same thing with the user's latest message — keep returning to it as the anchor, rather than drifting off into assumptions built up over the conversation.

## How to use it

1. Download `SKILL.md` from this repository.
2. Place it in your Claude skills folder (in Claude Code or Cowork, this is typically a folder named `skills`, with each skill living in its own subfolder — for this one, something like `skills/follow-your-input/SKILL.md`).
3. Once it's in place, Claude can pick it up automatically when it's relevant. There's nothing to run and no settings to configure — it's just an instruction Claude reads and applies.

If you're not sure where your skills folder lives, check Claude's settings under Capabilities, or ask Claude directly — it can tell you where to put skill files on your system.

## Files

- `SKILL.md` — the actual skill file, with the instructions Claude follows.
- `README.md` — this file.
