# Worked example

A short, made-up conversation that shows the loop: one task at a time, a failed step fixed before moving on, and an approval gate before a change.

The commands are examples for macOS. Use your own package manager.

**You:** Use the Converse skill. Help me set up a Postgres test database on my laptop. I will run the commands and paste the results back.

## Card 1: a read-only check

> **T1: Check what is installed** · 0 of 4 · Waiting
>
> - Last: none yet
> - Do: R1, the command below
> - Goal: A local test database I can connect to
> - Why: We need to know whether Postgres is already installed
> - Risk: Read-only, zero changes
> - Pass looks like: A version number such as `psql (PostgreSQL) 16`. "command not found" means we install it first
> - Next: T2, create the test database

R1

```bash
psql --version
```

**You:**

```text
R1 output: bash: psql: command not found
```

## Card 2: the step failed, so we stay on T1

The assistant does not move on. It explains the result and asks before changing anything.

> **T1: Install Postgres** · 0 of 4 · Waiting for your OK
>
> - Last: R1 failed. psql is not installed
> - Target: Your laptop, through the Homebrew package manager
> - Impact: Installs the PostgreSQL packages
> - Undo: `brew uninstall postgresql@16` removes them
> - Confirm: Reply `yes` to run R2

R2

```bash
brew install postgresql@16
```

**You:** yes, and then pasted the output, which ended with a normal install summary.

## Card 3: the fix passed, so we move on

> **T2: Create the test database** · 1 of 4 · Waiting
>
> - Last: T1 done. Postgres 16 is installed
> - Do: R3, the command below
> - Goal: A local test database I can connect to
> - Why: The database must exist before we can connect to it
> - Risk: Creates one new empty database called `converse_demo`. Nothing else changes
> - Pass looks like: No output. Any error message means we fix this step first
> - Next: T3, connect and run a test query

R3

```bash
createdb converse_demo
```

## What to notice

- Only one task is shown at a time.

- A failed result keeps you on the same task until it is fixed.

- Anything that installs, creates or deletes asks first, with the target, the impact and the undo.

- Task IDs (T1) and action IDs (R1) let either side say "redo R2" without confusion.

- Progress is "1 of 4", never a percentage.
