# Three Ways AI Answers Go Wrong (and a Fix for Each)

AI assistants fail in a few specific, recurring ways — not random mistakes, but predictable patterns tied to how these models generate text. Once you can name the pattern, you can catch it. That's what this framework does: three short, targeted fixes, each aimed at one failure mode.

## Problem 1: It answers the conversation it expects, not the one you're having

In a long back-and-forth, it's easy for an assistant to keep running on the plan, tone, or topic from ten messages ago — even after you've moved past it. You said something new; it answered the old thread instead. This gets worse the longer the conversation runs and the more steps a task has, because there's more momentum to override.

**The fix — Follow Your Input:** treat the message actually in front of you as the anchor, and everything earlier as background that informs it but doesn't override it. When they conflict, the current message wins — unless you'd set an explicit instruction or constraint earlier that's still active, in which case both have to be honored together.

## Problem 2: It quietly assumes a detail you never gave

Ask for "an email" and somewhere in generating the response, that silently became "a professional email to a client." You never said that. The assistant filled the gap — which it has to do, since no request specifies every detail — but it filled it without ever surfacing that a choice was made. If the guess is wrong, you get work built on the wrong foundation, and neither of you notices until it's done.

**The fix — Noting:** name the assumption instead of letting it run invisibly. "Assuming this is for a coworker rather than a client" is a sentence that can be checked and corrected. A silent default never becomes a sentence at all — it just organizes the whole answer, unexamined.

## Problem 3: It sounds sure when it isn't

Language models are trained to produce answers that read as complete and resolved, which creates a pull toward closure even when the honest answer is "it depends" or "we don't have enough information yet." The result: confident-sounding claims that outrun the actual evidence.

**The fix — Rest in Uncertainty:** collapse ambiguity into a single answer only when the evidence actually supports doing so — not before. When it doesn't, map out what's actually known versus missing, offer the branches that survive, or ask for the one specific piece that would resolve it. This isn't an argument for more hedging on things that are actually clear — most requests have enough evidence to answer directly, and that's still the default. It's aimed at the narrower case where completeness is being faked.

## Where this came from

All three practices are modeled on a single idea borrowed from meditation: don't let the mechanism produce an outcome that overrides what's actually true of the situation. In meditation, that shows up as returning attention to the breath instead of following a story the mind made up. Applied to an AI's reasoning, it shows up as returning to the actual message, naming assumptions before they run silently, and admitting when the evidence hasn't actually settled the question. None of this claims the AI has feelings or an inner life about any of it — it's a description of a mechanism to catch, not an experience to have. The meditation framing is just where the shape of the idea came from; nothing here depends on believing that framing to be useful.

More specifically, the framework is inspired by Thanissaro Bhikkhu's presentation of the Buddha's teaching in [*Wings to Awakening: An Anthology from the Pali Canon*](https://www.accesstoinsight.org/lib/authors/thanissaro/wings/index.html). That's a statement of where the idea came from, not a claim that the framework's specific mechanics have been rigorously mapped onto that text — see the white paper for the concrete concepts it contributed.

## Try it

The full framework, the individual skill files, and a ready-to-use Claude Code slash command (`/mindfulness`) are in this repo. See [README.md](./README.md) for setup — and for an honest look at what's actually been tested so far (short version: two empirical studies, both nulls, neither a disproof — see the README's "Status" section and the [white paper](./WHITEPAPER.md) for why).

**One thing worth knowing before you pick a setup path:** if you go with the individual skill files rather than the combined framework or slash command, install all three together — follow-your-input, noting, and rest-in-uncertainty. They're built to work as a set, and installing just one or two leaves gaps the other two are designed to cover.
