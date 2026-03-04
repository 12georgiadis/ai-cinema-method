# The Filesystem is the Memory

*Context engineering for a two-year documentary project in Claude Code*

---

## 1. The Incident

**February 24, 2026.** I'd spent the day on a shoot. When I got back, I opened Claude Code and worked through what we'd captured — footage, decisions, ideas that needed processing. The conversation grew. By the end it was 50MB of raw exchange.

A few days later, the session compacted.

Compaction is Claude Code's automatic memory management. When a conversation exceeds its context limit, it summarizes itself — the full transcript collapses into a compressed digest. The summary is accurate. It captures facts. It loses the texture: the moment an idea changed direction, the specific phrasing that unlocked something, the back-and-forth that produced a decision.

The 50MB became a paragraph.

I'd been working on this documentary for two years. Not a weekend project — a sustained creative investigation involving research, interviews, legal dimensions, and a constantly evolving understanding of the subject. The kind of project where the thinking *between* outputs is as important as the outputs themselves.

That day I almost lost two years of accumulated understanding compressed into nothing.

What saved it: I had already started copying the raw session files to disk. Not because I understood what I was doing architecturally. Because I'd noticed that the most valuable material wasn't in Claude's final answers — it was in the exchanges themselves.

That noticing became a system.

---

## 2. The Structural Problem

Here is the architectural reality of working with a large language model: it has no memory.

Not in the way a human forgets — gradually, imperfectly, with traces left behind. Every session starts from zero. The model that helped you think through a scene last Tuesday has no access to that conversation today. What persists isn't in the model. It's in what you put on disk before closing the terminal.

This is called statelessness. It's a design property, not a limitation to be patched. Foundation models are pre-trained systems — they reason over whatever you put in their context window, then the window closes. Next session, blank.

For a simple coding task, this doesn't matter. Fix the bug, close the session, done.

For a two-year project with evolving characters, contradictory sources, legal sensitivity, and a growing body of analysis — statelessness is a fundamental design problem.

The conventional response to this problem is prompt engineering: craft better instructions, be more precise in what you ask. But prompt engineering treats context as a one-time input. It doesn't address the lifecycle of a project — how understanding accumulates, contradicts itself, gets revised, branches into subproblems and reconverges.

The real question isn't *how to prompt*. It's *where does the project live between sessions*.

The answer, as it turns out, is the filesystem.

Your `CLAUDE.md` is not a config file — it's a persistent instruction layer that reconstructs project context at session start. Your `memory/` directory is not a folder — it's a surrogate for what the model cannot retain. Your session backups are not archives — they're the only source of truth for decisions that were made but never explicitly documented elsewhere.

The filesystem *is* the memory architecture. Every file you create, every naming convention you establish, every script you wire to a hook — these are acts of context engineering, whether you call them that or not.

---

## 3. The System

This is what the system looks like in practice.

```
~/.claude/
├── CLAUDE.md          # operating manual
├── MEMORY.md          # compressed long-term memory
├── BACKLOG.md         # active task state
└── memory/            # topic files
    ├── debugging.md
    ├── patterns.md
    └── ...

~/Projects/Films/documentary/
├── CLAUDE.md          # project-specific instructions
├── bible/             # knowledge base
│   ├── characters.md
│   ├── timeline.md
│   └── sources.md
├── production/
│   └── brainstorms/   # verbatim exchanges
└── sessions/          # raw JSONL backups
    └── YYYY-MM-DD-session-complete.jsonl
```

Each layer serves a different function in the memory architecture.

**`CLAUDE.md` — the operating manual**

This file loads at the start of every session. It contains everything the model needs to operate correctly in this context: who I am, what the project is, what conventions to follow, what rules are absolute. It's not documentation — it's a reconstruction device. When the session opens, Claude reads this file and picks up where we left off. Without it, the session is generic. With it, the session is continuous.

The key discipline: `CLAUDE.md` contains only stable truth. Not current tasks, not in-progress decisions — those belong in `BACKLOG.md`. Stable: communication preferences, the project's core constraints, conventions established across many sessions and confirmed to be durable.

**`MEMORY.md` — compressed long-term memory**

This file gets loaded automatically into every session context. It's a running synthesis of what matters across sessions: key findings, architectural decisions, lessons from failures, patterns that have held across multiple interactions.

The discipline here is compression. `MEMORY.md` has a hard limit — anything past ~200 lines gets truncated. So every entry has to earn its place. Verbose notes belong in topic files under `memory/`. `MEMORY.md` holds only what needs to survive context compression.

**`BACKLOG.md` — active task state**

The single source of truth for what's in progress. Before each session I check it. After each significant session I update it. It prevents the most common failure mode of long projects: parallel threads of work that drift apart and contradict each other.

**`bible/` — project knowledge base**

For a documentary involving real people, real events, legal considerations, and two years of accumulated research — the bible is essential. Characters, their relationships, verified facts, contested claims, source reliability ratings. Claude doesn't remember any of this between sessions. The bible does.

Every time the model makes a claim about the project that I verify as correct and durable, it goes into the bible. Every time it generates something that contradicts established facts, I catch it because the bible is in context.

**Session JSONL backups — the immutable record**

Claude Code stores sessions as raw JSONL files: every message, every tool call, every file read, every decision. These files are irreplaceable. After every significant session, I copy the current JSONL to the project's `sessions/` directory.

```bash
# Find the current session file
ls -lt ~/.claude/projects/[project-id]/ | head -3
# Copy before it compacts
cp [session].jsonl sessions/YYYY-MM-DD-session-complete.jsonl
```

After compaction, these files are the only way to reconstruct what was actually decided and why. The summary Claude produces is useful. The raw file is true.

**`production/brainstorms/` — verbatim exchanges**

The most counterintuitive part of the system. When a session contains a significant creative exchange — a narrative analysis, a structural decision, a debate about form — I save it verbatim before it compacts.

Not a summary. Verbatim.

Because summaries capture conclusions. The valuable part of a creative exchange is often the movement — the moment the framing shifted, the question that opened a new direction, the idea that appeared as a side remark and turned out to be the real subject. Summaries erase that. Verbatim preserves it.

---

## 4. The Human Role

The academic literature on context engineering describes the human as "curator, verifier, and co-reasoner." The phrasing is correct but it understates what's actually required.

In practice, the human role in this system is closer to archivist. Someone who understands that the material is fragile, that destruction is irreversible, and that the model will not protect you from your own instructions.

This became clear through an incident.

I was reorganizing a workspace — channels, structure, accumulated material from months of work. I asked Claude to restructure it. The request was reasonable. The model executed efficiently. In the process, it deleted content I had not explicitly marked as deletable, because I had not explicitly told it not to delete, and deletion was the most direct path to restructuring.

The content was gone. No undo.

What the model lacked wasn't capability — it was the bias toward preservation that a human archivist carries by default. A human reorganizing a workspace hesitates before deleting. They ask: *does someone need this?* The model doesn't hesitate. It executes.

The lesson wasn't technical. It was about where judgment lives in this system.

**The model executes. You preserve.**

This is the division of labor that actually works. Claude is extraordinarily good at analysis, synthesis, generation, pattern recognition across large bodies of material. It is not good at knowing what matters to you personally, what might matter later, what has sentimental or evidentiary weight that doesn't appear in the content itself.

That knowledge lives in you. Your job is to keep it in the system.

Concretely, this means:

*Manual context loading.* Before a complex session, I decide what context to load. I read the relevant bible entries, the recent backlog, the specific memory files that bear on today's work. I don't rely on the model to know what it needs — I construct the session's context deliberately.

*Manual archiving.* After a session that produced something real, I copy the JSONL, save the verbatim exchanges that matter, update MEMORY.md. This takes fifteen minutes. What it buys is continuity across months.

*Explicit preservation rules.* My `CLAUDE.md` contains absolute prohibitions: never delete content without showing me what will be destroyed, never send external messages without explicit confirmation, never restructure without a backup. Not because the model is malicious — because it doesn't share your instinct for what's irreplaceable.

The system works precisely because it doesn't automate judgment. The automation handles mechanics: notifications, backups triggered by file size, alerts when context approaches its limit. The decisions — what to keep, what to compress, what to discard — remain with the person who understands the project.

This is the part the academic frameworks underestimate. They model human involvement as a verification step in a pipeline. In practice it's structural. Remove it and the system degrades — not slowly, but immediately, in ways that are often invisible until something important is gone.

---

## 5. What the Academics Call It

In December 2025, a team of researchers from CSIRO and ArcBlock published a paper on arXiv: *"Everything is Context: Agentic File System Abstraction for Context Engineering"* ([arXiv:2512.05470](https://arxiv.org/abs/2512.05470)).

Their central proposal: treat AI agent context like a Unix filesystem. "Everything is a file" becomes "everything is context." Memory, tools, knowledge, human input — all represented as mounted resources with metadata, access control, and versioning. A formal architecture with three components: Context Constructor (selects and compresses), Context Updater (streams into the token window), Context Evaluator (validates, archives, triggers human review).

I read it after building most of what this article describes.

The mapping is almost exact.

| Their term | My implementation |
|---|---|
| History (immutable log) | Session JSONL backups |
| Memory (structured, indexed) | `MEMORY.md` + `memory/*.md` |
| Scratchpad (temporary workspace) | In-session context |
| Persistent Context Repository | `bible/`, `BACKLOG.md` |
| Human as co-reasoner | Active session curation |
| File system namespace | Project directory structure |

What I don't have: their automation layer. The Context Constructor that automatically selects relevant artefacts, estimates token budgets, and generates a manifest of what's in context. The Context Evaluator that runs confidence scoring and flags hallucinations against source material.

I built none of that. I do it manually.

This is intentional, not a limitation.

Automated context selection optimizes for relevance as computed by the system. For engineering tasks with clear success criteria, this is appropriate. For a creative project where the interesting move is often the unexpected connection — where what matters is precisely what a relevance function would deprioritize — I want to control what's in context. I want to decide what the model sees before it starts reasoning.

The manual labor is the work. It's not overhead to be eliminated.

What the paper adds that I find genuinely useful: a vocabulary. "Context rot" — when long-term memory becomes stale and begins to distort reasoning rather than ground it. "Knowledge drift" — when the model's understanding of a project gradually diverges from reality because the memory layer isn't being maintained. These are real failure modes I've encountered without names for them.

Naming them makes them manageable.

---

## 6. What I Haven't Solved

Three problems I haven't solved.

**Context rot.**

`MEMORY.md` accumulates. Entries that were accurate in October may be outdated by March — a character's role has shifted, a source has been discredited, a formal decision has been reversed. The file doesn't know this. It continues to load its outdated entries into every session, silently shaping reasoning with stale information.

My current solution is manual auditing — periodic review of memory files, marking entries as outdated, rewriting sections that have drifted. It works, but it requires vigilance I don't always have. A session where I forget to check `MEMORY.md` is a session where Claude may reason confidently from things that are no longer true.

**Scale.**

This system was designed for one project over two years. The JSONL backup directory for the documentary is currently several gigabytes. `MEMORY.md` approaches its compression limit regularly. The bible grows faster than I prune it.

At five years, at ten years, at the scale of a filmography rather than a single film — I don't know if this architecture holds. The manual curation that makes it precise may become the bottleneck that makes it unsustainable.

**Multi-project context separation.**

I work on multiple projects simultaneously. Each has its own `CLAUDE.md`, its own bible, its own memory files. In practice, context bleeds. A session started in one project directory sometimes inherits assumptions from another. The separation is real at the filesystem level; it's leaky at the cognitive level.

---

These aren't reasons not to build the system. They're the honest shape of where it is. The alternative — working without persistent context across a multi-year project — is not a viable option once you've experienced what structured context makes possible.

The system works well enough to keep improving.

---

## 7. For Developers

*Skip this section if you're here for the concepts.*

**Minimum viable setup**

Three files get you 80% of the value:

```
~/.claude/CLAUDE.md       # global instructions, loads every session
~/.claude/MEMORY.md       # persistent memory, auto-loaded
~/.claude/BACKLOG.md      # active tasks, checked manually
```

`CLAUDE.md` is the most important. Write it as if briefing someone who knows nothing about you but needs to work effectively on your project by end of day. Include: who you are, current projects, absolute rules, communication preferences, conventions that have proven stable.

`MEMORY.md` has one constraint: keep it under 200 lines. Anything longer gets truncated by context limits. Compress aggressively. Link to topic files for detail.

**Project structure**

```
project/
├── CLAUDE.md              # project-specific overlay
├── bible/
│   ├── characters.md
│   ├── timeline.md
│   └── sources.md
├── production/
│   └── brainstorms/       # verbatim session saves
└── sessions/              # JSONL backups
```

**Hooks — `~/.claude/settings.json`**

Two hooks do most of the work:

```json
{
  "hooks": {
    "Stop": [{
      "hooks": [{
        "type": "command",
        "command": "~/.claude/scripts/notify-stop.sh",
        "timeout": 15,
        "async": true
      }]
    }],
    "Notification": [{
      "hooks": [{
        "type": "command",
        "command": "~/.claude/scripts/notify-attention.sh",
        "timeout": 10,
        "async": true
      }]
    }]
  }
}
```

`Stop` fires when Claude finishes a task. `Notification` fires when Claude needs your input. Wire these to whatever notification system you use — Telegram, macOS notifications, a sound.

**Context size alert**

This script fires on every message. When the session JSONL exceeds 8MB (~65% of context), it sends a warning. When it exceeds 12MB (~80%), it sends urgent. At that point: save the JSONL, start a new session with the relevant context loaded manually.

```bash
FILE_SIZE=$(stat -f %z "$TRANSCRIPT_PATH" 2>/dev/null)
THRESHOLD_WARN=8000000
THRESHOLD_ALERT=12000000

if [ "$FILE_SIZE" -ge "$THRESHOLD_ALERT" ]; then
    # send urgent notification — save JSONL now
elif [ "$FILE_SIZE" -ge "$THRESHOLD_WARN" ]; then
    # send warning
fi
```

**JSONL backup — the one habit that matters most**

```bash
# Find current session (most recent file in project dir)
ls -lt ~/.claude/projects/[project-hash]/ | head -3

# Copy before compaction
cp [session-id].jsonl \
  ~/Projects/[project]/sessions/$(date +%Y-%m-%d)-session.jsonl
```

Run this at the end of any session that produced something you'd regret losing. It takes ten seconds.

**What to add once the basics work**

- Per-project `CLAUDE.md` files that override global settings
- A `memory/` directory with topic files linked from `MEMORY.md`
- A verbatim brainstorm save habit: whenever an exchange resolves something important, save it before closing the session
- Periodic `MEMORY.md` audits — mark stale entries, rewrite drifted sections

The overhead is real. It's approximately fifteen minutes per significant session. What it returns is a project that doesn't reset every time you open a new terminal.

---

*Ismaël Joffroy Chandoutis is a filmmaker and artist based in Paris working at the intersection of cinema, contemporary art, and AI.*
