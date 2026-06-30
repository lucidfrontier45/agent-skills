---
name: make-plan
description: Draft structured plans through clarifying questions without modifying any code. Use when user says "plan", "make a plan", "plan this out", or asks for a design on a non-trivial task.
---

# Plan

Goal: clarify intent → draft plan → confirm → optional write to `.plan/`.

## Core rules

- **No code edits.** Read files for context only.
- **Ask before assuming.** Batch focused questions, max 3–5 per turn.
- **No writes without consent.** Always confirm before persisting.

## Workflow

### 1. Clarify

Pose questions in rounds until ambiguity is low. Cover:
- Goal / success criteria
- Scope boundaries (in / out)
- Constraints (tech, time, deps, compat)
- Assumptions to validate
- Deliverable shape

Track answers inline. Re-ask if answers contradict.

### 2. Draft

Produce plan with these sections:
- **Goal** — one-line outcome
- **Background** — context the reader needs
- **Approach** — step-by-step, numbered
- **Trade-offs** — alternatives considered + why rejected
- **Open questions** — unresolved items
- **Next step** — first concrete action

Present draft in chat. Do not write yet.

### 3. Confirm

Ask: "Plan complete. Write to `.plan/<slug>.md`? (yes / revise / no)"

- **yes** → generate filename (see below), write file.
- **revise** → loop back with targeted questions on gaps.
- **no** → return draft in chat, no file.

## File naming

Auto-generate: `YYYY-MM-DD-HHmm-<slug>.md`
- `slug` = lowercase, kebab-case, 2–4 words from goal keywords.
- On collision, append `-2`, `-3`, etc.
- Path is relative to project root: `./.plan/`.

## Revisions

When one or more `.plan/*.md` files exist for the current topic:
- Read existing file(s).
- Ask: **revise in place**, **append new section**, or **new plan file**.
- For in-place edits, bump filename to next collision-suffix (`-2`, `-3`) — never overwrite history.

## Anti-patterns

- Drafting before asking.
- 10+ questions in one turn.
- Auto-writing without explicit "yes".
- Editing code "to verify the plan".
