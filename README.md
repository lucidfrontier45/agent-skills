# agent-skills

Personal repo for Agent skills. Each skill = standalone `SKILL.md` with frontmatter + workflow.

## Skills

### `make-plan/`
**Trigger:** "plan", "make a plan", "plan this out", design ask on non-trivial task.
**Flow:** clarify (rounds of 3–5 questions) → draft (Goal/Background/Approach/Trade-offs/Open Qs/Next step) → confirm → optional write to `.plan/`.
**Rule:** no code edits, no writes without consent.

### `execute-plan-with-todo/`
**Trigger:** "execute plan with {file}" or "run plan {file}".
**Flow:** locate plan → parse via `ctx_execute_file` (bytes stay sandbox) → derive TODOs from H2/H3 phases → write to `.todos/{file}.md` → execute step-by-step, mark done live.
**Rule:** no raw plan bytes in context, all derivation runs in code.

### `ddd-layer-rules/`
**Trigger:** DDD, layered/hexagonal/clean architecture, dirs like `domain/ usecase/ infrastructure/ entrypoint/ common/`, "where do I put this?", cross-layer refactor.
**Rules:** five layers (Domain / Use Case / Infrastructure / Entrypoint / Shared), dependency direction inward (Domain depends on nothing), repo interfaces in Domain, impls in Infrastructure. Language-agnostic.

## Layout
```
agent-skills/
├── README.md
├── make-plan/SKILL.md
├── execute-plan-with-todo/SKILL.md
└── ddd-layer-rules/SKILL.md
```
