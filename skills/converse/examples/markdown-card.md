# Markdown card (works anywhere)

Copy, fill in the fields, and paste into any chat, issue or wiki. Use this when the environment cannot show a visual card.

## Task card

> **T{id}: {plain-language title}** · {n} of {N} · {Waiting | Working | Done | Risk | Blocked}
>
> - Last: {one line on the previous task}
> - Do: {the exact file name or command, pinned here}
> - Goal: {the overall aim, same wording every time}
> - Why: {one line}
> - Risk: {what it can change, or "Read-only, zero changes"}
> - Pass looks like: {good result}. {Warning variant}. {Fail variant}.
> - Next: T{id}, {title}

R{id}

```bash
{one command, clean output}
```

Reply with `R{id} output:` and the paste.

## Approval gate card

Use this for anything that creates, changes or deletes.

> **T{id}: {title}** · {n} of {N} · Waiting for your OK
>
> - Target: {account / resource / environment}
> - Impact: {what will be created, changed or deleted}
> - Undo: {how to reverse it}
> - Confirm: reply `yes` to run it. {Reply `yes` again if double confirmation is required.}
