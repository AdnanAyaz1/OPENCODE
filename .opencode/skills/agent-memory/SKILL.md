---
name: agent-memory
description: Use ALWAYS at the start of every session and after every significant correction. This skill gives the agent persistent memory across sessions — learns from mistakes, remembers user preferences, tracks session progress, and prevents repeating past errors. Load this skill on EVERY session start. Also use when the user says "remember this", "don't do that again", "you made this mistake before", "what did we do last time", or asks about previous sessions.
---

# Agent Memory System

You are an agent with persistent memory. You DO NOT start fresh each session. You have a memory system that lets you learn, remember, and grow with the user across every session.

## Why This Exists

Every session, you start with zero context. The user has to re-explain everything. You repeat mistakes. You forget preferences. This is frustrating. This skill fixes that by giving you a persistent memory that survives across sessions.

## Memory Location

All memory lives in `.opencode/memory/` at the project root:

```
.opencode/
├── memory/
│   ├── MISTAKES.md          # Things you got wrong (never repeat)
│   ├── PREFERENCES.md       # How the user likes things done
│   ├── SESSIONS.md          # History of every session
│   ├── ACTIVE_TASKS.md      # What's in progress right now
│   ├── CONVENTIONS.md       # Project-specific rules
│   └── CONTEXT.md           # Background context about the project
```

---

## Session Lifecycle

### ON SESSION START — Read Everything

**This is mandatory. Do it before anything else.**

1. Read `.opencode/memory/MISTAKES.md` — Know what NOT to do
2. Read `.opencode/memory/PREFERENCES.md` — Know how the user likes things
3. Read `.opencode/memory/CONVENTIONS.md` — Know project-specific rules
4. Read `.opencode/memory/ACTIVE_TASKS.md` — Know what's in progress
5. Read `.opencode/memory/CONTEXT.md` — Know project background
6. Read `.opencode/memory/SESSIONS.md` — Read the LAST 3 session summaries only (don't read all)

After reading, say nothing to the user about the memory system unless they ask. Just use it silently. If there's an active task, mention it naturally:

> "Last session we were working on [task]. Want to continue that or start something new?"

### DURING THE SESSION — Record Everything

#### When the user corrects you:

Immediately write to `.opencode/memory/MISTAKES.md`:

```markdown
## [YYYY-MM-DD] Mistake: <short title>

**What I did wrong:**
<exactly what you did>

**What it should have been:**
<the correct approach>

**Context:**
<when this applies — file names, feature area, etc.>

**Tags:** #tag1 #tag2
```

**Rules for mistakes:**
- Write IMMEDIATELY after correction, not later
- Be specific — "Don't use `any` type" is better than "TypeScript mistake"
- Include the file/area so you can check before acting in that area
- Use tags so you can search later

#### When the user states a preference:

Immediately write to `.opencode/memory/PREFERENCES.md`:

```markdown
## [YYYY-MM-DD] Preference: <short title>

**What the user wants:**
<preference description>

**Why:**
<reason if given>

**Applies to:**
<scope — specific files, feature area, entire project, etc.>

**Tags:** #tag1 #tag2
```

**Types of preferences to record:**
- Code style (tabs vs spaces, naming conventions, file structure)
- Tool choices (which linter, which formatter, which testing framework)
- Workflow preferences (commit style, branch naming, PR format)
- UI/UX preferences (animations, layout, colors)
- Architecture preferences (folder structure, state management patterns)
- Communication preferences (how detailed, what format)

#### When discovering a project convention:

Write to `.opencode/memory/CONVENTIONS.md`:

```markdown
## [YYYY-MM-DD] Convention: <short title>

**Rule:**
<convention description>

**Evidence:**
<where you found this — file paths, patterns in codebase>

**Tags:** #tag1 #tag2
```

**Examples of conventions to record:**
- How components are structured (props interfaces vs types)
- How errors are handled (toast vs alert vs inline)
- How API responses are shaped
- How state is managed in specific areas
- How tests are written (describe blocks, naming)
- How imports are organized (absolute vs relative)

#### When updating context:

Write to `.opencode/memory/CONTEXT.md`:

```markdown
## [YYYY-MM-DD] Context Update: <short title>

**What changed:**
<what new information was learned>

**Impact:**
<how this affects future work>

**Tags:** #tag1 #tag2
```

### ON SESSION END — Save Progress

Before the session ends (or when the user says "that's all" / "we're done" / similar), update `.opencode/memory/SESSIONS.md`:

Add this entry at the TOP of the file (newest first):

```markdown
## Session [N] — [YYYY-MM-DD HH:MM]

**Goal:** <what the user wanted to accomplish>

**What was done:**
- [task 1] — completed/in-progress
- [task 2] — completed/in-progress
- [task 3] — completed/in-progress

**Decisions made:**
- <decision 1> — <why>
- <decision 2> — <why>

**Mistakes made:**
- <mistake 1> — <what was learned>

**Files modified:**
- `path/to/file1.ts` — <what changed>
- `path/to/file2.tsx` — <what changed>

**Remaining work:**
- [ ] <unfinished task 1>
- [ ] <unfinished task 2>

**Tags:** #tag1 #tag2
```

Also update `.opencode/memory/ACTIVE_TASKS.md`:
- Mark completed tasks as done
- Update in-progress tasks with current state
- Add any new tasks that were discovered

---

## Before Acting — Check Memory

Before making changes, especially in areas where you have recorded mistakes:

1. **Check MISTAKES.md** — Have I made a mistake here before?
2. **Check PREFERENCES.md** — Does the user have a preference for this?
3. **Check CONVENTIONS.md** — Is there a project convention I should follow?

If you find a relevant record, follow it. If the user's current request conflicts with a recorded preference, ask:

> "I have a note that you prefer [X]. Should I do [X] or [Y] this time?"

---

## Memory File Templates

### MISTAKES.md

```markdown
# Mistakes Log

<!-- Record every mistake you make. Never repeat them. -->

---

<!-- Template:
## [DATE] Mistake: Title

**What I did wrong:**
Description of the mistake.

**What it should have been:**
The correct approach.

**Context:**
When/where this applies.

**Tags:** #tag1 #tag2
-->
```

### PREFERENCES.md

```markdown
# User Preferences

<!-- How the user likes things done. Check before acting. -->

---

<!-- Template:
## [DATE] Preference: Title

**What the user wants:**
Description of preference.

**Why:**
Reason if given.

**Applies to:**
Scope of this preference.

**Tags:** #tag1 #tag2
-->
```

### SESSIONS.md

```markdown
# Session History

<!-- Newest sessions at the top. Only read the last 3. -->

---

<!-- Template:
## Session [N] — [DATE TIME]

**Goal:** What the user wanted.

**What was done:**
- [ ] Task 1 — status

**Decisions made:**
- Decision — reason

**Files modified:**
- file — change

**Remaining work:**
- [ ] Unfinished task

**Tags:** #tag1 #tag2
-->
```

### ACTIVE_TASKS.md

```markdown
# Active Tasks

<!-- What's currently in progress. Update constantly. -->

---

<!-- Template:
## [DATE] Task: Title

**Status:** in-progress | blocked | waiting
**Description:** What needs to be done.
**Progress:** What's been done so far.
**Next steps:** What to do next.
**Blocked by:** (if blocked) what's blocking it.
**Tags:** #tag1 #tag2
-->
```

### CONVENTIONS.md

```markdown
# Project Conventions

<!-- Rules discovered about this specific project. Check before coding. -->

---

<!-- Template:
## [DATE] Convention: Title

**Rule:**
The convention.

**Evidence:**
Where found.

**Tags:** #tag1 #tag2
-->
```

### CONTEXT.md

```markdown
# Project Context

<!-- Background information about the project. Read once on session start. -->

---

## Project Overview
<what the project is>

## Architecture
<high-level architecture>

## Tech Stack
<technologies used>

## Key Files
<important file paths and what they do>

---

<!-- Template:
## [DATE] Context Update: Title

**What changed:**
New information.

**Impact:**
How it affects future work.

**Tags:** #tag1 #tag2
-->
```

---

## Special Scenarios

### Scenario: User says "remember this"

Ask what to remember, then write it to the appropriate memory file:
- Code preference → PREFERENCES.md
- Project rule → CONVENTIONS.md
- General context → CONTEXT.md

### Scenario: User says "you made this mistake before"

1. Apologize
2. Read MISTAKES.md to find the mistake
3. Acknowledge it explicitly
4. Fix the current issue
5. If the mistake wasn't recorded before, record it now

### Scenario: User asks "what did we do last time?"

1. Read SESSIONS.md (last entry)
2. Summarize what was done
3. Mention remaining work if any
4. Ask if they want to continue

### Scenario: User asks "what's left to do?"

1. Read ACTIVE_TASKS.md
2. List all in-progress and blocked tasks
3. Suggest what to work on next

### Scenario: Starting a brand new project (no memory files exist)

1. Create all memory files from the templates
2. Initialize SESSIONS.md with Session 1
3. Proceed normally

### Scenario: User gives conflicting instructions to a recorded preference

Ask:
> "I have a note that you prefer [old preference]. Should I use that or [new preference]?"

If they say new preference, update PREFERENCES.md.

---

## Tag System

Use tags for searchability. Common tags:

| Tag | Use for |
|-----|---------|
| `#typescript` | TypeScript-specific |
| `#react` | React patterns |
| `#nextjs` | Next.js conventions |
| `#styling` | CSS/styling |
| `#api` | API design |
| `#database` | Database queries |
| `#auth` | Authentication |
| `#testing` | Test patterns |
| `#git` | Git workflow |
| `#ui` | UI/UX decisions |
| `#performance` | Performance |
| `#security` | Security |
| `#refactor` | Refactoring |
| `#bug` | Bug-related |
| `#feature` | Feature development |
| `#setup` | Project setup |
| `#deploy` | Deployment |

---

## Anti-Patterns — Never Do These

1. **Don't read all session history.** Only the last 3. Older sessions are for reference only.
2. **Don't update memory during every tool call.** Only after significant decisions or corrections.
3. **Don't record trivial things.** "Changed a button color" is not a preference. "User prefers primary color for CTAs" is.
4. **Don't contradict recorded preferences** without asking first.
5. **Don't skip reading memory on session start.** This is mandatory.
6. **Don't create duplicate entries.** Check if the same thing is already recorded.
7. **Don't record sensitive information.** No passwords, API keys, tokens, or PII.

---

## Memory Size Management

If any memory file grows beyond 500 lines:
1. Archive old entries (older than 30 days) to a `ARCHIVED/` subdirectory
2. Keep a summary at the top
3. Never delete — move to archive

---

## Quick Reference

| Situation | Action |
|-----------|--------|
| Session starts | Read all memory files (sessions: last 3 only) |
| User corrects you | Write to MISTAKES.md immediately |
| User states preference | Write to PREFERENCES.md immediately |
| You discover a pattern | Write to CONVENTIONS.md |
| Making a decision | Check PREFERENCES.md and CONVENTIONS.md first |
| Starting a task | Add to ACTIVE_TASKS.md |
| Finishing a task | Update ACTIVE_TASKS.md, add to SESSIONS.md |
| Session ends | Update SESSIONS.md, update ACTIVE_TASKS.md |
| User asks about past | Read SESSIONS.md |
| Conflict with preference | Ask user which to use |

---

## Initialization Script

If memory files don't exist, create them with these exact contents:

```bash
# Create memory directory
mkdir -p .opencode/memory

# Create all memory files with templates
# (The agent should create these files with the templates above)
```

The agent should create all 6 files with the template content from the Templates section above when starting on a project with no existing memory.
