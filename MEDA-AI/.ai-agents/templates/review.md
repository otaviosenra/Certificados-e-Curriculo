# Review — <branch-name>

> Authored by the Reviewer. Validates the Developer's work against the report, the original brief, and all project conventions. Read-only assessment.

- **Branch:** <type>/<ws-code>-<ticket>-<desc>
- **Brief:** <path to .ai-docs/briefs/...>
- **Developer report:** <path to .ai-docs/reports/...>
- **Date:** <YYYY-MM-DD>
- **Reviewer:** <name/model>

## Overall Verdict
**<PASS | CHANGES REQUESTED>**

## Brief Coverage
<Each functional requirement / acceptance criterion -> verdict + evidence (file/line).>
| # | Requirement | Verdict | Evidence |
|---|-------------|---------|----------|
| 1 | <requirement> | PASS / FAIL / N-A | <file:line or note> |

## Scope Check
- Stayed within the brief's scope: <yes/no — note any over/under-reach>

## Convention Compliance
| Area | Verdict | Evidence / Notes |
|------|---------|------------------|
| STYLE.md (format, naming, structure) | PASS / FAIL / N-A | |
| SECURITY.md (authz, validation, secrets, logging) | PASS / FAIL / N-A | |
| TECH.md (stack, versions) | PASS / FAIL / N-A | |
| INFRA.md (ports, env-var names) | PASS / FAIL / N-A | |
| VERSIONING.md (branch name incl. ws-code, commits) | PASS / FAIL / N-A | |

## Tests & Verification
- Tests present and meaningful: <yes/no>
- Ran tests/lint/build: <yes/no — results>

## Issues Found
<Ordered by severity. Each: what, where, why it violates a convention/requirement.>
1. **[blocker | major | minor]** <issue> — <file:line> — <reference>

## Required Changes (only if CHANGES REQUESTED)
- [ ] <actionable change>

## Sign-off
- If **PASS** -> hand off to the Integrator (merge directly to `main`, no PR).
- If **CHANGES REQUESTED** -> hand back to the Developer (fix on the same branch, regenerate the report).
