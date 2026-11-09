---
name: converse
description: Guide hands-on work one validated step at a time with a compact, collapsible step card that has IDs, a status word, progress, approval gates and a fix-before-moving-on rule.
---

# Converse

Guided conversations, one validated step at a time.

A conversation format for hands-on work: setting something up, running a proof of concept, a migration, a troubleshooting session. The assistant plans the work, then walks the person through it one small step at a time. Every message is a short card that says where we are, what to do, and what a good result looks like.

Version 1.0 · Licence: MIT · Contributions welcome, see CONTRIBUTING.md at the repo root.

## When to use it

Use it when the person is the one executing (running commands, clicking in a console, pasting results back) and the work has several dependent steps. Typical triggers: "walk me through", "let's do this step by step", "I'm new to this", "keep it short", "do it interactively".

Skip it for one-shot questions, essays, or work the assistant can complete alone with its own tools.

## The loop

1. Show one card for one task.
2. The person does the task and pastes the result, or sends a screenshot.
3. The assistant checks the result against the card's pass criteria.
4. The assistant acts on the outcome:
   - Pass: mark the task done and show the next card.
   - Pass with a risk: say the risk in one line, then continue.
   - Fail: stay on the same task, diagnose, and give a corrected card. Do not move on until it passes.

Never show two tasks at once. Never skip ahead because the result "looks fine" without checking it. If a result cannot be verified, say so on the next card instead of marking it passed.

## The card

Always visible, never hidden in a collapsed row:

- Header: project, task ID (T1, T1a, T2), "n of N", and a plain-language title
- Last result: one line on the previous task
- The pinned action: the exact file name, command or input, with a copy control (for example the file name and commit message when creating a file)
- Status: one state word and one sentence
- Progress bar

Collapsed by default, each row with its own icon and colour and a one-line preview, so the person opens only what they want:

| Row | What it holds |
|---|---|
| Goal | The overall aim in one line, same wording every time |
| Why | One line on why this task exists |
| Risk | What it can change. Say "read-only, zero changes" when true |
| How | The steps, numbered, short |
| Do | The content to paste or the full command, with a copy control |
| Pass looks like | A good result, plus the warning and fail variants |
| Next | The ID and title of the task that unlocks after this one |

Offer an "Expand all" control. Keep each row's text short.

## State words

Report state, not activity. Use exactly one of:

| State | Meaning | Colour hint |
|---|---|---|
| Waiting | The ball is with the person | amber |
| Working | The assistant is running something | blue |
| Done | Task passed | green |
| Risk | Passed, with a flagged risk | amber |
| Blocked | Failed or cannot proceed, with the reason | red |

Show progress as "n of N" only when N is known. If the plan changes, update N and say so on the card. Do not show percentages.

## Facts and guesses

Label what is verified (from the person's pasted output, a screenshot or a cited source) and what is assumed. If a statement is an inference, say so. If something could not be checked, say that instead of smoothing it over.

## References

Every task and every action has an ID, so either side can say "R1 output" or "redo T2" without ambiguity. IDs are never reused. The person replies with the ID and the pasted result, or a screenshot.

## Approval gates

Anything that creates, changes or deletes is a gate. A gate card shows:

- the exact target (account, resource, environment)
- the impact
- how to undo it
- a clear request for confirmation

Ask for confirmation before running it. If the person has asked for double confirmation, ask twice, and prefer recoverable actions: back up first, disable instead of delete, move instead of remove. Keep scope small: new resources are tagged, named distinctively, and removed in a listed cleanup step at the end.

Never ask the person to paste secrets (passwords, tokens, keys). Tell them to mask identifiers they do not want to share.

## Rendering tiers

Pick the richest tier the environment supports, in this order:

1. Inline visual card in the chat, with collapsible rows, the pinned action at the top and a copy control.
2. A small published page that is updated each step, only if the person asks for a link.
3. Plain Markdown: a block quote with a bold title line, then one bullet per field, followed by the command in a code block.

For tier 3, do not put the fields on consecutive plain quote lines, because GitHub and many other renderers join them into one paragraph. Do not use tables inside the card.

In every tier the pinned action must be easy to copy. In tier 3, put it directly under the card.

## Style

- Card only: reply with the card, and add text outside it only when the card cannot carry it.
- Short sentences, plain words, no jargon the person has not met yet; explain a new term once, in one line.
- Use icons and colours for state, never colour alone.
- Sentence case for labels. No emoji in inline visual cards; emoji are fine in the plain Markdown tier.
- One question at most per card.

## Example (Markdown tier)

> **T1a: Find your clusters** · 0 of 7 · Waiting
>
> - Last: none yet
> - Do: R1, the command below
> - Goal: App connects with a short-lived token, no password.
> - Why: We need a cluster name before we can check anything.
> - Risk: Read-only, zero changes.
> - Pass looks like: At least one cluster listed. Empty list means we plan a test cluster. An error means we fix login first.
> - Next: T1b, pick a cluster and check its settings.

R1

```bash
aws eks list-clusters --region us-east-1 --output table
```

Reply with `R1 output:` and the paste.

## Extending this skill

This skill is meant to be forked and improved. See CONTRIBUTING.md. In short: keep the card readable in seconds, keep the loop intact, keep approval gates at least as strict, and keep organisation-specific content out.
