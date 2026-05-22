# TEAM_TRACKER.md — AI Tutor & Exam Practice System

> **Last updated:** 2026-05-22
> **Author:** Member 1 (Architect & SDD Lead)

---

## 1. Project Phase Tracker

| Phase | Name | Owner | Status |
|---|---|---|---|
| 0 | Repository scaffold and SDD setup | Member 1 | Completed |
| 1 | PROJECT_SPEC.md | Member 1 | Completed |
| 2 | ARCHITECTURE.md | Member 1 | Completed |
| 3 | TEAM_WORKFLOW.md, TEAM_TRACKER.md, module spec template | Member 1 | In Progress |
| 4 | Module SPEC writing | All module leads | Pending |
| 5 | Module implementation | All module leads | Pending |
| 6 | Integration and evaluation harness | Member 9, Member 10 | Pending |
| 7 | Final report, exports, token usage, demo | All | Pending |

---

## 2. Member Ownership Table

| Member | Name | Role | Primary Module | Folder | Module Spec File |
|---|---|---|---|---|---|
| Member 1 | Joy Das | Architect + SDD Lead | Governance and project docs | — | — |
| Member 2 | TBD | Syllabus Ingestion Engineer | Syllabus ingestion | `src/ingestion/` | `specs/MODULE_SPEC_INGESTION.md` |
| Member 3 | Priyanka Kumar | RAG Retrieval Engineer | RAG engine | `src/rag/` | `specs/MODULE_SPEC_RAG.md` |
| Member 4 | Keshav Kumar | Practice Paper Generator Engineer | Question generation | `src/generator/` | `specs/MODULE_SPEC_GENERATOR.md` |
| Member 5 | TBD | Question Tagging Engineer | Tagging and difficulty | `src/tagging/` | `specs/MODULE_SPEC_TAGGING.md` |
| Member 6 | TBD | Answer Evaluation Engineer | Evaluation and rubrics | `src/evaluation/` | `specs/MODULE_SPEC_EVALUATION.md` |
| Member 7 | TBD | Analytics Engineer | Weakness detection | `src/analytics/` | `specs/MODULE_SPEC_ANALYTICS.md` |
| Member 8 | TBD | Tutor and Remediation Engineer | Tutor chatbot and remediation | `src/tutor/` | `specs/MODULE_SPEC_TUTOR.md` |
| Member 9 | TBD | Streamlit Integration Engineer | UI and orchestration | `src/api/` | `specs/MODULE_SPEC_API.md` |
| Member 10 | TBD | Evaluation Harness Engineer | Harness and Trust Dashboard | `src/evaluation_harness/` | `specs/MODULE_SPEC_EVAL_HARNESS.md` |

---

## 3. Module SPEC Status

| Module | Primary Owner | Supporting Owner | Spec File | Spec Drafted | Architect Review | Spec Approved | Notes |
|---|---|---|---|---|---|---|---|
| Ingestion | Member 2 | TBD | `specs/MODULE_SPEC_INGESTION.md` | No | No | No | — |
| RAG | Member 3 | TBD | `specs/MODULE_SPEC_RAG.md` | No | No | No | LLM adapter contract required; provider can remain configurable |
| Generator | Member 4 | TBD | `specs/MODULE_SPEC_GENERATOR.md` | No | No | No | Depends on RAG spec |
| Tagging | Member 5 | TBD | `specs/MODULE_SPEC_TAGGING.md` | No | No | No | Depends on Generator spec |
| Evaluation | Member 6 | TBD | `specs/MODULE_SPEC_EVALUATION.md` | No | No | No | Rubric JSON schema must be defined in spec |
| Analytics | Member 7 | TBD | `specs/MODULE_SPEC_ANALYTICS.md` | No | No | No | Simulated attempt fixture schema must be defined |
| Tutor | Member 8 | TBD | `specs/MODULE_SPEC_TUTOR.md` | No | No | No | Latency target deferred to spec; must use mockable LLM adapter |
| API / Streamlit | Member 9 | TBD | `specs/MODULE_SPEC_API.md` | No | No | No | Depends on all upstream module interfaces |
| Eval Harness | Member 10 | TBD | `specs/MODULE_SPEC_EVAL_HARNESS.md` | No | No | No | Depends on analytics fixture schema |

---

## 4. Implementation and Evidence Status

| Module | Primary Owner | Impl Started | Impl Complete | Tests Written | Tests Passing | Export Filed | Agent Usage Filed | PR Merged | Notes |
|---|---|---|---|---|---|---|---|---|---|
| Ingestion | Member 2 | No | No | No | No | No | No | No | — |
| RAG | Member 3 | No | No | No | No | No | No | No | — |
| Generator | Member 4 | No | No | No | No | No | No | No | — |
| Tagging | Member 5 | No | No | No | No | No | No | No | — |
| Evaluation | Member 6 | No | No | No | No | No | No | No | — |
| Analytics | Member 7 | No | No | No | No | No | No | No | — |
| Tutor | Member 8 | No | No | No | No | No | No | No | — |
| API / Streamlit | Member 9 | No | No | No | No | No | No | No | — |
| Eval Harness | Member 10 | No | No | No | No | No | No | No | — |

---

## 5. Commit Count Tracker

| Member | Role | Commits (target: ≥ 5) | Last Commit | Notes |
|---|---|---|---|---|
| Member 1 | Architect | TBD | — | — |
| Member 2 | Ingestion | TBD | — | — |
| Member 3 | RAG | TBD | — | — |
| Member 4 | Generator | TBD | — | — |
| Member 5 | Tagging | TBD | — | — |
| Member 6 | Evaluation | TBD | — | — |
| Member 7 | Analytics | TBD | — | — |
| Member 8 | Tutor | TBD | — | — |
| Member 9 | API | TBD | — | — |
| Member 10 | Eval Harness | TBD | — | — |
