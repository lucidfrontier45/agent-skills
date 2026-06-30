---
name: execute-plan-with-todo
description: Execute plan file as sequence of tasks with live TODO tracking. Use when user says "execute plan with {plan_file_name}" or "run plan {plan_file_name}".
---

# Execute Plan With Todo

## Trigger

User says: `execute plan with {plan_file_name}` or `run plan {plan_file_name}`.

## Workflow

### 1. Locate + read plan

- Resolve path (rg/find if relative)
- Parse with `ctx_execute_file` — extract structure into memory, do NOT hold raw bytes in context

### 2. Generate TODO list

- Plan has no pre-existing checkboxes required
- Derive tasks from plan: each H2/H3 phase + sub-step = one TODO
- Write derived list to `.todos/{plan_file_name}.md`
- TODO schema:

```
# TODO: {plan_file_name}

## Phase 1: {name}
- [ ] {task} — {1-line deps or notes}
- [ ] {task}

## Phase 2: {name}
- [ ] {task}
```

- File lives under workspace `.todos/` (create if missing)

### 3. Context-mode tool hierarchy

Use Context-mode tool if available.

Default order, top = preferred:

1. `ctx_search` — recall prior indexed knowledge
2. `ctx_batch_execute` — multi-command research
3. `ctx_execute` — derive answers from data
4. `ctx_execute_file` — read file contents
5. `ctx_fetch_and_index` — web content
6. `ctx_index` — store docs for later search
7. `ctx_stats` / `ctx_doctor` / `ctx_upgrade` / `ctx_purge` — maintenance
8. `read` / `edit` / `write` / `bash` — file ops + small reads only

Never raw-cat large outputs.

### 4. Execute per task

For each `- [ ]` in `.todos/` file, in order:

1. Print task header
2. Gather context via ctx tools
3. Apply edits with `edit` tool (LINE#HASH anchors from `read`)
4. Verify: build/test/lint per project conventions
5. Mark `- [ ]` → `- [x]` in `.todos/{plan_file_name}.md`

### 5. Report

- Per task: 1-line status
- Per phase: summary
- On plan complete: full report + deviations + new dependencies

## Stop conditions

- Plan file missing → ask user for path
- Task fails verification → stop, report, ask user
- Ambiguous task → stop, ask user to clarify
- `.todos/` not writable → report + ask user for alt path

## Anti-patterns

- Don't assume plan has checkboxes — generate them
- Don't edit `.todos/` checkboxes before task verified
- Don't re-read full plan repeatedly — hold structure
- Don't skip ctx tools for convenience
