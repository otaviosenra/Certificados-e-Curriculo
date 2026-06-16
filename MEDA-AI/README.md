# AI Agent Workflow

A four-role AI agent workflow for GitHub Copilot (VS Code), with portable project-context documentation that every role reads before acting.

> **Start here:** read [`AGENTS.md`](AGENTS.md) — it is the entry point for any AI assistant. Every initiative begins by selecting the **Architect** agent.

## Roles (custom agents — `.github/agents/`)
| Role | Model (latest at setup) | Does |
|------|-------------------------|------|
| **Architect** | Claude Opus 4.8 | Talks in natural language; authors/edits task briefs; maintains `.ai-docs/` definitions; closes sessions. Never edits source. |
| **Developer** | GPT-5.3-Codex | Implements a task brief on a feature branch named per `VERSIONING.md`; emits a report for the Reviewer. |
| **Reviewer** | Claude Sonnet 4.6 | Validates the implementation against report + brief + conventions. Read-only. |
| **Integrator** | GPT-5.3-Codex | Merges the reviewed branch directly into `main` (no PR) with `git merge --no-ff`. |

Roles are chained with **handoffs** (buttons that appear after each turn):
Architect → Developer → Reviewer → Integrator → (back to Architect to close the session). Reviewer can also hand back to the Developer on "CHANGES REQUESTED".

> Model names rotate in the Copilot picker — confirm they match your picker and plan, and bump them when newer versions ship (`# bump on new release` is marked in each agent file).

## Layout
```
.github/agents/        Architect / Developer / Reviewer / Integrator custom agents
.ai-agents/            Read-only. Skill assets shared across projects:
  prompts/             Bootstrap prompts that fill .ai-docs (audit / from-need)
  templates/           task-brief, review, session-close
.ai-docs/              Generated docs + work artifacts:
  CONTEXT.md           Entry-point manifest the agents load first
  FUNCTIONAL/TECH/INFRA/STYLE/SECURITY.md   Project definitions (generate these)
  VERSIONING.md        Git standards: branch naming (incl. workspace code), no-PR merge
  briefs/ reports/ reviews/ sessions/        Created as you work
example.code-workspace VS Code workspace example with the AI_WS_CODE env var
```

## Quick start
1. **Drop this scaffold into your repo root.** The four agents land in `.github/agents/` so VS Code/Copilot picks them up automatically.
2. **Set the workspace code.** Copy `example.code-workspace` per workspace and give each its own `AI_WS_CODE` (used in branch names). One VS Code workspace at a time per workstation.
3. **Fill the project definitions.** Open the Architect (or any chat) and run one of:
   - existing code → paste `.ai-agents/prompts/audit-existing-projects.md`
   - new project from a need → paste `.ai-agents/prompts/generate-from-need.md`
   This populates `.ai-docs/` (FUNCTIONAL, TECH, INFRA, STYLE, SECURITY) and fills `VERSIONING.md` placeholders. Review every `UNKNOWN` / `ASSUMPTION`.
4. **Fill `VERSIONING.md` placeholders** (bracketed `[...]`) with your actual git standards. Keep the workspace-code branch rule and the no-PR direct-to-`main` rule.
5. **Make sure `main` has no branch protection** requiring PRs or approvals, so the Integrator can merge directly.
6. **Work the loop:** Architect drafts a brief → *Start Development* → Developer implements + reports → *Send to Reviewer* → Reviewer validates → *Approve & Integrate* → Integrator merges to `main` → *Close Session*.

## Conventions
- All documentation is in English (consumed by AI agents).
- Branch pattern: `<type>/<ws-code>-<ticket>-<desc>` (e.g. `feat/X-PROJ-123-login`).
- Traceability: every integration is a `--no-ff` merge commit; `git log --first-parent main` is the audit trail.
- If you run the Architect/Reviewer via the standalone Claude Code tool instead of Copilot, move those two to `.claude/agents/` and set the model inside Claude Code — but the VS Code handoffs won't bridge automatically then.
