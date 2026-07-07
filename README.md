# OpenCode

AI-powered development environment with persistent memory and production-ready application building skills.

## Skills

### agent-memory
Persistent memory across sessions — learns from mistakes, remembers user preferences, tracks session progress, and prevents repeating past errors.

### production-app
Step-by-step guide to building production-ready applications from idea to deployment.

## Getting Started

```bash
# Install dependencies
pnpm install

# Start development
pnpm dev
```

## Memory System

The agent memory lives in `.opencode/memory/` and includes:
- `MISTAKES.md` — Never-repeat errors
- `PREFERENCES.md` — How you like things done
- `SESSIONS.md` — Session history
- `ACTIVE_TASKS.md` — What's in progress
- `CONVENTIONS.md` — Project-specific rules
- `CONTEXT.md` — Project background
