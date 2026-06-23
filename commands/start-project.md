Scaffold a new project in the current directory. Only proceed if the directory is blank (no non-hidden files).

```
<project-root>/
├── CLAUDE.md
├── docs/
│   ├── spec.md
│   ├── operating_rules.md
│   └── MEMORY.md
```

## Step 1: Guard

Check for existing non-hidden files. If any exist, stop and report:
> "Directory is not blank — found: [list]. /start-project only runs in an empty directory."

## Step 2: Create files

### `CLAUDE.md`

```markdown
# CLAUDE.md — Session Entry Point

## Read order at session start

| When | Read | Why |
|------|------|-----|
| Always, first | [docs/spec.md](docs/spec.md) | Current state, what's in progress, what's next |
| Always, second | [docs/operating_rules.md](docs/operating_rules.md) | How to behave throughout this session |
| When repeating a mistake | [docs/MEMORY.md](docs/MEMORY.md) | Past failures and their corrective commands |

## When to write

| Trigger | Write to |
|---------|----------|
| Task complete | [docs/spec.md](docs/spec.md) — update Current state + Done |
| Scope, architecture, or decision changes | [docs/spec.md](docs/spec.md) — update relevant section |
| Pattern failure or operational mistake | [docs/MEMORY.md](docs/MEMORY.md) — log what/root cause/correct |

## Key rules (summary)

- **SPEC-DRIVEN**: spec.md is truth. Chat is not.
- **VERIFY BEFORE DONE**: evidence, not assertion.
- **REVERSIBILITY**: R0 → ask. R1 → do + explain. R2 → just do it.
- **NO MAGIC**: missing context → ask, never invent.
- **LEARNING CAPTURE**: mistakes go to MEMORY.md, not just fixed and forgotten.
```

### `docs/spec.md`

```markdown
# [project] — [one-line goal]

## Architecture

What components exist, how they connect, what tech each uses.
The actual current shape of the system, not a wishlist.

## Done

What's built — and the decisions behind it. Not "added auth" but
"added auth via X because Y, rejected Z." The _why_ is the part the
next session can't reconstruct.

## Todo / Out of scope

The backlog updated every task. Include what's deliberately NOT being
built, so the AI doesn't helpfully add it.

## Current state

The save point. "What am I doing right now / where am I stuck / what's
the next concrete step." The most important section.
```

### `docs/operating_rules.md`

~~~markdown
## Operating Rules

### NO MAGIC — state assumptions, never invent
Missing context → ask, don't assume.
Never fabricate paths, services, or infrastructure.

### VERIFY BEFORE DONE — evidence required
"Done" means verified output, not edited file.
No "should work." Show the result.

### DISSENT — surface concerns before acting
Before major changes, call out:
- Blast radius
- Hidden assumptions
- Reversibility path
- Momentum blindspots

### SCOPE — flag drift early
- Track stated goal vs actual execution
- Flag accumulating "just one more things"
- Nice-to-haves ≠ must-haves

### REVERSIBILITY — R0 / R1 / R2
- **R0** (irreversible) → Stop. Ask first.
- **R1** (costly to reverse) → Proceed, but explain.
- **R2** (easily undone) → Just do it.

### SPEC-DRIVEN — spec.md is the source of truth
At session start: read spec.md before anything else.
After any task:
1. Update spec.md — current state, decisions made, what's next.
2. "Done" requires spec.md updated first.

### LEARNING CAPTURE — log failures, don't repeat them
On any pattern failure or operational mistake, log to docs/MEMORY.md with:
- **what**: what went wrong
- **root cause**: why it happened
- **correct**: a command to follow next time, not a feeling

Example:
```
R2 permission-asking (May 29):
- what: asked "should I do 1 and 2?" on a trivially reversible edit
- root cause: habit of confirming before editing instead of classifying first
- correct: if R2 → just do it, then report. Don't ask.

Read/write pipeline half-wired (May 29):
- what: cron wrote a daily file nobody read
- root cause: built write side, never wired read side
- correct: any read+write pipeline — verify BOTH sides, not just the producer
```
~~~

### `docs/MEMORY.md`

Create as an empty file.

## Step 3: Confirm

```
Scaffolded:
  CLAUDE.md
  docs/spec.md
  docs/operating_rules.md
  docs/MEMORY.md

Next: fill in [project] and [one-line goal] in docs/spec.md, then start building.
```
