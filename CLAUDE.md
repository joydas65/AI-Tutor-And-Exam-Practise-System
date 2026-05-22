# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A 10-member course project building an AI Tutor & Exam Practice System. The MVP targets CBSE Class 10 Mathematics for selected chapters, while keeping the architecture extensible to other boards, grades, and subjects. Two core flows:

1. **Doubt resolution** — retrieve and answer student queries grounded in curriculum material
2. **Mock exams** — generate, administer, and evaluate practice tests

Current phase: **0 — Repository scaffold / SDD setup.** No application logic exists yet.

## Repository Structure

```
data/syllabus/            Curriculum content (input corpus)
data/question_bank/       Exam questions
data/sample_answers/      Reference answers for evaluation

src/ingestion/            Data ingestion and preprocessing
src/rag/                  Retrieval-Augmented Generation pipeline
src/generator/            Question and answer generation
src/tagging/              Topic and difficulty tagging
src/evaluation/           Answer evaluation logic
src/analytics/            Usage analytics
src/tutor/                Tutoring session orchestration
src/api/                  External API layer
src/evaluation_harness/   Automated evaluation framework

tests/                    Test suite
specs/                    Per-module SDD specs (one file per src/ module)
exports/                  Exported agent session transcripts (professor evidence)
agent_usage/              Raw prompt logs per session
artifacts/screenshots/    UI / system screenshots
artifacts/demo_outputs/   Sample system outputs
artifacts/evaluation_results/ Evaluation run outputs

app.py                    Entry point (stub)
requirements.txt          Dependencies (stub)
```

## Governance Files

| File | Purpose |
|---|---|
| PROJECT_SPEC.md | Requirements and constraints (Phase 1) |
| ARCHITECTURE.md | System design (Phase 2) |
| TEAM_WORKFLOW.md | Phase plan, roles, agent usage policy |
| TEAM_TRACKER.md | Per-member assignments |
| TOKEN_USAGE.md | AI token log — fill after every session |
| FINAL_REPORT.md | End-of-project report (Phase 6) |
| results.md | Evaluation results (Phase 5) |

## Agent Usage Rules

- Log every AI session in `TOKEN_USAGE.md` immediately after it ends.
- Export full session transcripts to `exports/`; save prompt logs to `agent_usage/`.
- No AI-generated code merges without a linked spec in `specs/`.
- All AI output must be reviewed by a human before merging.

## Code Attribution

The `.github/instructions/wmt-copilot.instructions.md` file governs GitHub Copilot attribution markers and is gitignored. Claude Code is not bound by those rules, but the no-public-sources policy applies to all AI tools on this project.
