# AGENTS.md

> Entry point for any AI assistant working in this repository. Read this first.

## Where to start
**Every initiative starts with the `Architect` agent.** Select the **Architect** chat mode (`.github/agents/architect.agent.md`) before doing anything else. The Architect plans work, writes task briefs, and maintains the `.ai-docs/` definitions.

Typical flow:
1. **Architect** — discuss the need, produce/update a task brief under `.ai-docs/briefs/`.
2. **Developer** — implement the approved brief on a feature branch (per `.ai-docs/VERSIONING.md`).
3. **Reviewer** — validate the implementation against the brief and conventions.
4. **Integrator** — merge the reviewed branch into `main`.

## Always load context first
Before any action, read `.ai-docs/CONTEXT.md` and every file it references:
- `.ai-docs/FUNCTIONAL.md` — what the system does
- `.ai-docs/TECH.md` — technology stack (authoritative)
- `.ai-docs/INFRA.md` — ports, services, networking
- `.ai-docs/STYLE.md` — coding conventions
- `.ai-docs/SECURITY.md` — security requirements
- `.ai-docs/VERSIONING.md` — branching and release rules
- `.ai-docs/ROADMAP.md` — required, Architect-maintained prioritized backlog; decouples brief creation order from execution order

## Governance model
- Agents live in `.github/agents/` (Architect, Developer, Reviewer, Integrator).
- Templates live in `.ai-agents/templates/` (read-only): task briefs, reviews, session-close.
- Durable records:
  - Task briefs → `.ai-docs/briefs/`
  - Reviews → `.ai-docs/reviews/`
  - Developer reports → `.ai-docs/reports/`
  - Session-close records → `.ai-docs/sessions/`
  - Prioritized backlog → `.ai-docs/ROADMAP.md` (required; Architect-maintained)

## Rules of thumb
- Source of truth for any convention is the relevant `.ai-docs/` file — never inline assumptions.
- Only the Architect writes under `.ai-docs/`; agents never write into `.ai-agents/` (read-only).
- All artifacts in English.
