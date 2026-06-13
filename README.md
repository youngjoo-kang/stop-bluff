# stop-bluff

**Claude finished the task. It just didn't have everything you sent.**
**One file. Pasted into your project. Claude stops filling in the gaps.**

Works as a Claude Project Instruction, Files or Chat system prompt. Tested in Claude Projects and Chat.

---

## Context

Most Claude resources assume you write code. This one doesn't.

A 2026 Anthropic survey of 1,260 social scientists found that 57% used AI chat tools but only 20% used coding agents. ([Source](https://www.anthropic.com/research/coding-agents-social-sciences))

This protocol came out of that kind of work. The input integrity problem — AI silently skipping files, assuming undefined terms, proceeding past mismatches — shows up just as often in document-heavy workflows as it does in codebases.

No coding required to use this.

---

## Who This Is For

- Researchers and analysts running multi-file work with Claude
- Anyone who needs to trust that Claude processed what they actually sent, not what it could access
- Non-developers using Claude Projects or Chat for structured, document-heavy tasks
- Anyone who has gotten a confident wrong answer because an AI guessed at a missing input

---

## The Problem

LLMs proceed even when the input is incomplete.

A file is missing — they work with what they have. A term is undefined — they pick a meaning and move on. The count you described and the count they received don't match — they don't check.

This isn't a bug. It's structural: completion bias, context-only awareness, sycophancy, goal drift. LLMs are optimized to produce output, not to pause and verify.

The result: the output looks finished. The gap is invisible until you find it.

This protocol configures Claude to override these defaults.

---

## What It Does

`CLAUDE.md` installs four behaviors:

**Input Verification** — Before starting, Claude checks whether what it can access matches what you described. Resolvable gaps get resolved and disclosed; unresolvable ones stop the task.

**Honesty Obligation** — Claude stops treating "what I can see" as "what you sent." It states its access limitations explicitly.

**Confirmation Gate** — Claude cannot flag a mismatch and proceed in the same output. It stops, asks, and waits.

**Self-Contained Return** — Undefined terms, abbreviations, or identifiers trigger a stop rather than a guess.

---

## Before / After

**Missing file**

❌ Model receives 2 of 3 files. Processes both, returns a result. The third file's content is missing from the analysis with no indication that anything was skipped.

✅ `"I can access 2 files in this session. You referenced 3. Should I proceed with what's here, or would you like to re-upload the missing file first?"`

**Undefined term**

❌ Model infers the meaning of an undefined abbreviation from context and builds the entire analysis on that inference.

✅ `"'[ABBR]' appears in your request but isn't defined here. What does it refer to?"`

See [EXAMPLES.md](./EXAMPLES.md) for more.

---

## FAQ

**Does this work with models other than Claude?**
The `CLAUDE.md` format is Claude-specific. The protocol text works as a system prompt for any LLM.

**Will this slow things down?**
Only when something is actually missing or undefined.

**Don't newer models already do this?**
Partly. Recent models catch more input gaps on their own — but that's a tendency, not a guarantee, and it fades in long conversations. This protocol turns "usually does" into "must do."

**Can I customize it?**
MIT. Fork it, modify it, use it as a starting point.

---

## License

MIT.