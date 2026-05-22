# Agent Usage — Architect Phase 1

## Session Name

ai-tutor-sdd-architect-session

## Role

Member 1 — Project Architect and SDD Lead

## Work Completed in This Session

- Initialized SDD-oriented repository structure.
- Created and refined project-level governance artifacts.
- Created and refined PROJECT_SPEC.md.
- Reviewed PROJECT_SPEC.md for ambiguity, overclaiming, hallucination risk, missing acceptance criteria, and professor alignment.
- Created ARCHITECTURE.md after PROJECT_SPEC.md was reviewed.
- Recorded major architecture decisions before implementation.
- Exported the Claude Code session as evidence.

## Architecture Decisions Recorded

- Streamlit-first MVP.
- src/tutor/ is a unified Tutor & Remediation package.
- Local ChromaDB for MVP vector store, with in-memory fallback if needed.
- File-based JSON for student profiles.
- JSON rubrics under data/rubrics/.
- src/api/ is an orchestration layer, not a REST API in the MVP.
- LLM access goes through a mockable adapter interface.
- data/sources.md is required before ingestion.

## Token / Cost Usage

Claude Code usage was captured using `/cost` after the architect Phase 1 session.

| Metric | Value |
|---|---|
| Total cost | $1.29 |
| Total API duration | 9m 45s |
| Total wall duration | 1d 22h 30m |
| Total code/doc changes | 592 lines added, 38 lines removed |
| Model used | claude-sonnet-4-6 |
| Input tokens | 2.5k |
| Output tokens | 26.7k |
| Cache read tokens | 1.2m |
| Cache write tokens | 139.7k |
| Session usage | 37% used |
| Weekly usage | 32% used |

Note: Usage is approximate and based on local Claude Code sessions on this machine, as reported by Claude Code. It may not include usage from other devices or claude.ai.

## Token-Saving Practices Followed

- Used project files such as PROJECT_SPEC.md and ARCHITECTURE.md as reusable source-of-truth context.
- Asked Claude to review and summarize instead of repeatedly reprinting full files.
- Avoided implementation code during planning and architecture phases.
- Used phased work: repository skeleton → project spec → spec review → architecture plan → architecture document → export.
- Requested concise summaries after each phase.
- Exported after the architecture milestone so the next phase can start with a smaller context.

## Hallucination-Control Practices Followed

- Treated PROJECT_SPEC.md as the source of truth.
- Asked Claude to identify ambiguity and overclaiming before architecture.
- Added measurable grounding rules and source-governance requirements.
- Deferred implementation until specification and architecture were reviewed.
