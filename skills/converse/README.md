# Converse

Guided conversations, one validated step at a time.

You do not need to know anything about AI agents to use this.

Converse is a set of instructions you give to an AI assistant. After that, the assistant stops sending long walls of text. It gives you one small task at a time, checks your result, and only then moves on. If a step fails, it fixes that step first.

It suits work where you do the typing: setting something up, running a proof of concept, a migration, a troubleshooting session.

## Try it in 60 seconds

1. Open [SKILL.md](SKILL.md) and click the copy icon at the top right of the file view.

2. Start a new chat with your AI assistant and paste the file.

3. On a new line, add a request like this:

```text
Use the Converse skill.
Help me set up a Postgres database on my laptop.
I will run the commands and paste the results back.```

4. Do the one task on the first card. Paste the result (or a screenshot) back. The assistant checks it and gives you the next card.

## What you will see

Each reply is one short card:

- **Header:** the task name and where you are, for example 2 of 6
- **Do:** the exact command or input to use, ready to copy
- **Pass looks like:** how to tell it worked
- **Status:** one word, Waiting, Working, Done, Risk or Blocked

Anything that creates, changes or deletes something shows the target, the impact and how to undo it, and asks you first.

For a plain Markdown version of the card, see [examples/markdown-card.md](examples/markdown-card.md).

## Install it as a skill

Pasting works everywhere. If your tool supports skills, install this folder once and it is always available.

- **Claude app:** zip this folder and add it from the skills section in settings. Menu names change, so check the current help page if you cannot find it.

- **Claude Code:** copy this folder into `~/.claude/skills/` (all projects) or `.claude/skills/` inside a project.

- **Other assistants:** paste the contents of SKILL.md into the custom instructions, rules or system prompt field, or into an AGENTS.md file if your tool reads one.

## Good to know

- Converse works best when you run the steps yourself and paste the results back.

- Never paste passwords, tokens or keys into a chat. The skill tells the assistant not to ask for them. Mask anything private.

- It is a convention, not software. Edit it to suit you.

## Contributing

Improvements are welcome. See [CONTRIBUTING.md](../../CONTRIBUTING.md).
