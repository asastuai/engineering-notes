# Memory layers

Two layers of persistence. One per project. One across projects. Loaded automatically. Used to survive across sessions.

Without memory layers, every conversation starts from zero. The author re-explains. The AI re-asks. The work loses days to context rebuilding. The layers are the cheapest single intervention that compounds across sessions.

---

## The two layers

### Layer 1: per-project auto-memory

A directory on the local filesystem. One markdown file per memory entry. An index file (`MEMORY.md`) that lists the entries.

Path on this machine: `~/.claude/projects/<project-slug>/memory/`.

Loaded automatically at the start of every session in that project. The contents become part of the AI's working context before the first prompt.

Used for memories scoped to a single project: project-specific decisions, conventions, files of record, in-flight tasks.

### Layer 2: cross-project memory

A persistent memory provider that survives across all projects on the same account. Saved entries can be retrieved from any session in any working directory by querying a topic key or a search string.

Used for memories that travel: user preferences, working-style choices, signature, working habits, anything that should be loaded regardless of which repository the AI is operating in.

The two layers do not duplicate each other except by deliberate choice. A memory that should travel goes to cross-project. A memory scoped to a project goes to per-project. A memory that is critical and should survive both a project deletion and a cross-project outage goes to both.

---

## What gets saved

The protocol is conservative. Most things are not memories.

### Saved

- Decisions about architecture, naming, conventions, workflow. Especially decisions that took time to reach.
- Bug fixes with non-obvious root causes.
- Patterns established (naming, structure, design).
- User preferences and constraints once they are stable.
- Discoveries about the codebase or domain that would be expensive to rediscover.
- Reference pointers (Linear projects, dashboards, external docs) when the AI will need them.

### Not saved

- Code patterns visible by reading the code. Use grep instead.
- Git history. Use git log instead.
- Recent changes the user can see in the diff.
- Debugging recipes. The fix is in the code; the commit message has the context.
- Anything in CLAUDE.md or other auto-loaded files.
- Ephemeral task state. In-progress work. Current conversation context.

The discipline of *not* saving keeps the memory layer signal-rich. A memory layer that holds everything holds nothing.

---

## Memory hygiene

The layers are not write-only. Memories decay. Some decay faster than others.

### Long-lived memories

Working preferences. Stable conventions. Author profile.

These do not decay quickly. They are referenced by topic key and updated only when the underlying preference changes.

### Project memories

Architecture decisions in a specific repo. Conventions in a specific codebase. In-flight migrations.

These decay when the project moves on. A decision that was load-bearing in week one may be overridden in week six. When a recalled memory conflicts with current code, trust the current code and update the memory.

### Reference memories

Pointers to external systems. Dashboard URLs. Channel names. Project codes.

These decay when the external system changes. Verify before acting on a recalled reference.

---

## How a new session bootstraps

When opening a new session in a project that already has memory:

1. Per-project memory loads from the index.
2. Specific memory files are loaded as their topics become relevant. Some are eager, some on demand.
3. Cross-project memories load by topic key when relevant.
4. The AI begins responding with context that survived the previous session boundary.

When opening a new session in a project that has no memory:

1. Per-project layer is empty. AI starts from zero on project specifics.
2. Cross-project memories still load by topic.
3. As the session produces decisions, conventions, discoveries, the AI saves them.

The asymmetry: a project that has been worked on for a while is much faster to resume than one being entered for the first time. This is a feature. The cost of the first session is amortized across all subsequent ones.

---

## When to save

The AI saves without being asked when:

- A decision is made about architecture, naming, or convention.
- A non-obvious bug is fixed (root cause goes into the memory).
- A user preference is learned.
- A pattern is established.
- A discovery is made that would be expensive to rediscover.
- A user explicitly asks the AI to remember something.

The AI does not save when:

- The information is derivable from the code.
- The information is ephemeral.
- A duplicate already exists with the same topic key (in which case the AI updates rather than creating a new entry).

---

## A simple rule that captures the protocol

If a future agent reading this memory in three months would benefit from it more than from reading the code at that point, save it.

If the code at that point would tell the future agent everything they need, do not save.

The rule is a heuristic. The protocol is the discipline of applying it.

---

Juan Cruz Maisú ♥
