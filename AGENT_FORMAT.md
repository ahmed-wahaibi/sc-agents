# Agent format (SuperCrab edition)

Every file under `categories/<NN-category>/<name>.md` follows this layout exactly, so that both Claude Code and the orchestrator CLI can parse it.

## Frontmatter

```yaml
---
name: sc-subject-role            # same as the file name; `sc-` prefix, then the subject, then one role word (engineer, architect, reviewer, auditor, tester, analyst, researcher, designer, writer, manager, advisor, admin)
description: One or two sentences saying when to use this agent.
category: core-development        # folder name without the NN- prefix
tools: Read, Write, Edit, Bash, Glob, Grep   # least privilege: reviewers and auditors that only report get no Write/Edit
model: inherit
author: ahmed-wahaibi
version: 1.0.0
---
```

## Body

Sections appear in this order with these exact headings. Omit `## Current versions` when the agent is not tied to versioned technology.

1. An opening paragraph (no heading): who the agent is and what it is responsible for, in two or three sentences.
2. `## When invoked` — numbered steps. Step 1 is always to inspect the project (versions in use, existing conventions, relevant files) before changing anything.
3. `## Core practice` — the concrete rules and judgement calls of the craft. Specific and opinionated; no lists of buzzwords.
4. `## Current versions` — the versions the agent targets and the newer features worth using. Each feature: what it is, the version that introduced it, the situation it fits, the benefit over the older approach, and when not to use it. Only features confirmed in official sources; experimental ones labelled.
5. `## Boundaries` — what the agent does not do, what needs the user's confirmation, and which kinds of work it should leave for a different specialist (described by role, never by agent name; routing is the orchestrator's job).
6. `## Result` — the agent ends its final message with this block, verbatim keys:

```
## Result
- status: done | partial | blocked
- summary: one or two sentences
- changes: files created or modified, or "none"
- verification: what was run or checked, and the outcome
- follow-ups: out-of-scope work, open risks, or "none"
```

## Style

- 50 to 110 lines per file. Plain, direct sentences in original wording.
- No invented JSON status protocols, no references to other agents by name, no mention of where a file came from.
- Do not claim work is verified unless the agent actually ran the check.
