# TEAM_WORKFLOW.md — AI Tutor & Exam Practice System

> **Status:** Phase 3 in progress — workflow defined, tracker and module spec template pending.
> **Author:** Member 1 (Architect & SDD Lead)
> **Aligned with:** PROJECT_SPEC.md, ARCHITECTURE.md, CLAUDE.md

---

## 1. Purpose

This file enforces Spec-Driven Development (SDD) across all 10 team members. Every gate, rule, and checklist in this document exists to prevent vibe coding — the practice of asking an AI agent to generate code without prior design, review, or grounding in a written specification.

The professor will evaluate whether the team used Claude Code with understanding and control. Evidence of SDD includes:

- Written and reviewed module specs before implementation
- Human corrections to AI output documented in each spec
- Phase-by-phase commits traceable to spec sections
- Real test outputs and evaluation metrics, not manually written results
- Per-member export logs and agent usage files

Following this workflow is mandatory. Deviations must be discussed with the Architect before proceeding.

---

## 2. Project Phases

| Phase | Name | Owner | Status |
|---|---|---|---|
| 0 | Repository scaffold and SDD setup | Member 1 | Completed |
| 1 | PROJECT_SPEC.md | Member 1 | Completed |
| 2 | ARCHITECTURE.md | Member 1 | Completed |
| 3 | TEAM_WORKFLOW.md, TEAM_TRACKER.md, module spec template | Member 1 | In Progress |
| 4 | Module SPEC writing — one spec per module | All module leads | Pending |
| 5 | Module implementation — per-spec, phase-by-phase | All module leads | Pending |
| 6 | Integration and evaluation harness | Member 9, Member 10 | Pending |
| 7 | Final report, exports, token usage, demo | All | Pending |

### Phase gate rules

- No Phase 5 work begins before the relevant Phase 4 spec is approved by the Architect.
- No Phase 6 integration begins before Phase 5 modules pass their own module-level tests.
- No Phase 7 submission is made before the evaluation harness generates a real Trust Dashboard report.
- Status must be updated in this file as each phase completes.

---

## 3. Team Role Allocation

| Member | Role | Primary Module | Module Spec File |
|---|---|---|---|
| Member 1 | Architect + SDD Lead | Project docs, ARCHITECTURE.md, TEAM_TRACKER.md, FINAL_REPORT.md, governance | — |
| Member 2 | Syllabus Ingestion Engineer | `src/ingestion/` | `specs/MODULE_SPEC_INGESTION.md` |
| Member 3 | RAG Retrieval Engineer | `src/rag/` | `specs/MODULE_SPEC_RAG.md` |
| Member 4 | Practice Paper Generator Engineer | `src/generator/` | `specs/MODULE_SPEC_GENERATOR.md` |
| Member 5 | Question Tagging Engineer | `src/tagging/` | `specs/MODULE_SPEC_TAGGING.md` |
| Member 6 | Answer Evaluation Engineer | `src/evaluation/` | `specs/MODULE_SPEC_EVALUATION.md` |
| Member 7 | Analytics and Weakness Detection Engineer | `src/analytics/` | `specs/MODULE_SPEC_ANALYTICS.md` |
| Member 8 | Tutor and Remediation Engineer | `src/tutor/` | `specs/MODULE_SPEC_TUTOR.md` |
| Member 9 | Streamlit Integration Engineer | `src/api/` | `specs/MODULE_SPEC_API.md` |
| Member 10 | Evaluation Harness and Trust Dashboard Engineer | `src/evaluation_harness/` | `specs/MODULE_SPEC_EVAL_HARNESS.md` |

Each module lead is the primary owner of their folder, spec file, tests, exports, and agent usage log. Supporting owners are defined in TEAM_TRACKER.md.

---

## 4. Branch Naming Rules

All work happens on feature branches. No direct commits to `main`.

### Naming format

```
<type>/<short-slug>
```

### Allowed types

| Type | Use |
|---|---|
| `feature/` | New implementation or spec |
| `fix/` | Bug fix or correction |
| `docs/` | Documentation only |
| `test/` | Tests or verification scripts only |
| `spec/` | Module SPEC file only |

### Examples

```
feature/project-sdd-setup
feature/rag-retrieval
feature/paper-generator
feature/evaluation-harness
spec/ingestion-module
fix/rag-cosine-threshold
test/analytics-weak-topic
docs/token-usage-update
```

### Rules

- Branch names must be lowercase and hyphen-separated.
- Branch names must not include member names or generic terms like `update` or `changes`.
- One branch per module phase — do not bundle multiple modules in one branch.
- Branches must be deleted after the PR is merged.

---

## 5. Commit Message Rules

All commits must follow the Conventional Commits format:

```
type(scope): short imperative description
```

### Allowed types

| Type | Use |
|---|---|
| `docs` | Documentation, spec, governance files |
| `spec` | Module SPEC writing or updates |
| `feat` | New implementation code |
| `fix` | Bug fix |
| `test` | Tests or verification scripts |
| `refactor` | Code restructuring with no behaviour change |
| `verify` | Verification run output or evaluation result |
| `chore` | Setup, config, dependency, or scaffold |

### Scope

The scope is the module or file being changed:

```
ingestion, rag, generator, tagging, evaluation, analytics, tutor, api,
eval_harness, spec, workflow, tracker, report, token_usage, sources
```

### Examples

```
docs(spec): add project specification sections 1–10
spec(rag): define cosine similarity threshold and chunk log contract
feat(generator): implement marks-sum assertion and scope validation
test(analytics): add simulated attempts fixture and weak-topic detection test
fix(tutor): correct out-of-syllabus detection logic in guardrails
verify(eval_harness): run grounding check and record results
chore(ingestion): add chromadb and sentence-transformers to requirements
```

### Rules

- The description must be imperative (add, fix, implement — not added, fixing).
- The description must be specific enough to locate the change without reading the diff.
- Vague messages such as `update`, `fix stuff`, `wip`, or `changes` are not acceptable.
- Each commit must be traceable to a spec section, acceptance criterion, or phase gate.
- Every member must make at least 5 meaningful commits. See Section 11 for the definition of meaningful.

---

## 6. Pull Request Rules

### General rules

- No direct commits to `main`. All work merges through pull requests.
- Every module — spec, implementation, tests, and verification — must be merged through a PR.
- PRs must not bundle multiple modules. One PR per module phase.
- A PR must not be merged by its own author. At least one reviewer must approve.
- The Architect (Member 1) must review and approve any PR that touches governance files: CLAUDE.md, PROJECT_SPEC.md, ARCHITECTURE.md, TEAM_WORKFLOW.md, TEAM_TRACKER.md.

### PR description requirements

Every PR description must include:

1. **Module:** which module this PR covers
2. **Phase:** spec / implementation / tests / integration
3. **Spec reference:** link to the module spec section this PR satisfies
4. **What changed:** two to five bullet points describing the actual changes
5. **Human review note:** what the author manually reviewed, corrected, or verified
6. **Test or verification:** what test or script was run and what the result was
7. **Export file:** filename of the Claude Code export log for this session (e.g. `exports/m3_rag_2026-05-22.md`)
8. **Agent usage file:** filename of the agent usage summary for this session

### Example PR description

```
## Module
src/rag/ — RAG retrieval engine

## Phase
Implementation — Phase 5

## Spec reference
specs/MODULE_SPEC_RAG.md §3 (retrieval), §5 (chunk logging)

## What changed
- Implemented embed_query() using sentence-transformers
- Implemented search_chromadb() with top-k and 0.60 threshold
- Added chunk ID logging to chunk_log for every non-trivial response
- Added low-confidence fallback returning controlled message

## Human review note
The AI initially omitted the fallback branch for low-confidence queries.
I added the out-of-syllabus detection and controlled return message manually.
Threshold value confirmed against MODULE_SPEC_RAG.md §5.

## Test / verification
Ran tests/test_rag.py — 4/4 tests passed.
Verified chunk_log populated correctly for a sample query.

## Export file
exports/m3_rag_2026-05-22.md

## Agent usage file
agent_usage/m3_rag_usage.md
```

---

## 7. Module SPEC Review Gate

### The gate

No implementation code may be written, committed, or merged until the module spec for that module is reviewed and approved by the Architect.

### Process

1. Module lead drafts `specs/MODULE_SPEC_<MODULE>.md` on a `spec/<module-name>` branch.
2. Module lead opens a PR for the spec.
3. Architect reviews the spec and leaves written feedback as a PR comment.
4. Module lead addresses feedback and updates the spec.
5. Architect comments **"Spec approved — implementation may begin"** on the PR.
6. Spec PR is merged to `main`.
7. Module lead may now open an implementation branch.

### Required sections in every module spec

Each module spec must contain:

- **Purpose** — what this module does and why
- **Inputs and outputs** — exact function signatures or data contracts
- **Acceptance criteria** — measurable pass/fail conditions aligned with PROJECT_SPEC.md §13
- **Interface contract** — how `src/api/` or other modules call this module
- **Dependencies** — other modules, data stores, or external libraries required
- **Test plan** — what tests will be written and what they will assert
- **Corrections made to AI output** — see Section 10 for requirements
- **Open risks** — unresolved decisions blocking implementation

### If a spec changes significantly after approval

If a module lead makes substantial changes to an approved spec during implementation — for example, changing the interface contract or removing an acceptance criterion — they must notify the Architect and get a re-approval comment before continuing.

---

## 8. Phase-Wise Implementation Rule

Implementation must happen one phase at a time, one logical unit at a time. AI agents must not be given "build the entire module" prompts.

### Correct approach — phase-by-phase prompts

```
Phase A: Write the data parsing function only. Align with spec §2.
Phase B: Write the embedding function. Use the interface defined in spec §3.
Phase C: Write the ChromaDB write function. Align with the chunk schema in spec §4.
Phase D: Write the unit tests for each function above.
```

### After each implementation phase

1. Read the generated code against the spec section it was meant to satisfy.
2. Manually identify and correct any deviations, hallucinations, or missing logic.
3. Run the relevant test or verification script.
4. Commit with a specific message referencing the spec section.
5. Record corrections in the spec's "Corrections made to AI output" section.

### Prohibited prompts

The following types of prompts are not acceptable in this project:

- "Build the entire RAG module."
- "Write all the code for ingestion."
- "Create the full tutor chatbot."
- "Finish my module."

Each prompt must target one specific function, class, or script at a time.

---

## 9. Agent Usage Requirements

### Per-session export

After every substantive Claude Code session, the member must run `/export` to save the full session transcript.

- Save the file to: `exports/<member-id>_<module>_<date>.md`
- Example: `exports/m3_rag_2026-05-22.md`
- At least one export per module is required in the final submission.
- The export must cover the session where the spec or implementation was produced.

### Per-member agent usage summary

Each member must maintain `agent_usage/<member-id>_<module>_usage.md`.

This file must contain one row or block per session with:

- Session date
- Prompts used (summarized — not copy-pasted verbatim)
- What the agent produced
- What the member manually corrected, rejected, or rewrote
- Approximate token count, or the statement: "Exact token count was not captured."

This file is human-authored. It is distinct from the export log, which is a raw transcript.

### Token usage before export

Before running `/export`, members should attempt to run `/cost` or `/stats` if available in their Claude Code version. If token cost data is shown, record it in `TOKEN_USAGE.md` immediately.

### Fabrication prohibition

Token counts, session costs, and model outputs must not be fabricated or estimated without basis. If exact data is unavailable, write "Exact token count was not captured." This is acceptable. A made-up number is not.

---

## 10. Token-Saving Rules

These rules reduce token consumption per session and keep prompts focused.

1. **Use spec files as the source of truth.** Before each session, paste only the relevant spec section — not the entire spec, the entire architecture doc, or the entire project spec.
2. **Do not paste large files repeatedly.** If a file was pasted in the same session, refer to it by name in subsequent prompts.
3. **Ask for concise summaries first.** When exploring a module's design, ask the agent for a short plan before asking it to generate code.
4. **Use phase-wise prompts.** Target one function or class per prompt. See Section 8.
5. **Export after milestones, not at arbitrary intervals.** Export after a spec is complete, after a phase of implementation is complete, or after tests pass — not mid-session.
6. **Clear context when switching modules.** Start a new session when switching from one module to another. Do not carry prior module context into a new module's session.

---

## 11. Test and Verification Expectations

### Minimum requirement

Every module must include at least one test or verification script in `tests/`.

The test must cover the module's primary acceptance criterion from its spec, as derived from PROJECT_SPEC.md §13.

### Module-specific requirements

| Module | Required test or verification |
|---|---|
| `src/ingestion/` | Assert that chunked documents produce metadata with all required fields (board, grade, subject, chapter, topic, source_id, chunk_id) |
| `src/rag/` | Assert chunk IDs are logged for a sample query; assert low-confidence queries return the controlled fallback and no LLM response |
| `src/generator/` | Assert generated paper marks sum equals requested total; assert all questions carry source_context_id |
| `src/tagging/` | Assert difficulty, skill_tested, and question_type are assigned to every question; assert source_context_id is present |
| `src/evaluation/` | Assert MCQ evaluation is deterministic; assert rubric-based evaluator loads rubric by rubric_id from data/rubrics/ |
| `src/analytics/` | Load simulated_attempts.json fixture; assert the weakest topic is correctly identified |
| `src/tutor/` | Assert out-of-syllabus queries are refused; assert remediation output contains retrieved chunk references |
| `src/api/` | Assert end-to-end demo flow executes without error for a sample scope input |
| `src/evaluation_harness/` | Assert grounding percentage is computed correctly; assert Trust Dashboard report is generated |

### Verification rules

- Tests must be runnable from the command line with no manual setup beyond installing requirements.
- No live API credentials should be required to run tests. Use the LLM mock adapter for all LLM-dependent paths.
- Final metrics in `results.md` must come from actual script or command output — not written by hand.
- If a test fails, it must be fixed before the implementation PR is merged.

---

## 12. What Members Must Not Do

The following actions are prohibited for all team members:

### Implementation gates

- Do not write, commit, or open a PR for implementation code before the module spec is approved by the Architect.
- Do not open a Phase 6 integration PR before Phase 5 modules pass their own tests.

### Scope and accuracy

- Do not claim the system supports all boards, all grades, or all subjects. The MVP supports CBSE Class 10 Mathematics for the three selected chapters only.
- Do not generate questions, answers, remediation notes, or tutor responses without RAG grounding.
- Do not use the LLM's parametric memory alone as the source for syllabus-specific content.

### Fabrication

- Do not fabricate token usage, test results, evaluation scores, retrieval scores, or Git commit counts.
- Do not write results.md or TOKEN_USAGE.md entries by hand without running the underlying script or session.
- Do not claim a feature is implemented if it is only stubbed or partially written.

### AI usage discipline

- Do not merge AI-generated output without human review.
- Do not leave the "Corrections made to AI output" section blank or as "None." If truly no corrections were needed, explain what was verified manually.
- Do not use "build the entire module" prompts. See Section 8.
- Do not skip the `/export` and agent usage steps after any AI session.

### Git and PR hygiene

- Do not commit directly to `main`.
- Do not merge your own PR without reviewer approval.
- Do not bundle multiple modules in one PR or one branch.
- Do not commit secrets, API keys, or credentials to the repository.
- Do not bypass pre-commit hooks or skip PR review steps.

---

## 13. Final Submission Evidence Checklist

The following files and folders must be present and complete before final submission.

### Project-level governance

- [ ] `CLAUDE.md` — project-level agent rules
- [ ] `PROJECT_SPEC.md` — requirements and constraints
- [ ] `ARCHITECTURE.md` — system design and component boundaries
- [ ] `TEAM_WORKFLOW.md` — this file, complete and up to date
- [ ] `TEAM_TRACKER.md` — per-member assignments with status
- [ ] `TOKEN_USAGE.md` — one row per member, no fabricated entries
- [ ] `FINAL_REPORT.md` — end-of-project report
- [ ] `results.md` — evaluation results from actual script runs
- [ ] `README.md` — project overview and setup instructions
- [ ] `requirements.txt` — complete dependency list

### Module specs

- [ ] `specs/MODULE_SPEC_INGESTION.md`
- [ ] `specs/MODULE_SPEC_RAG.md`
- [ ] `specs/MODULE_SPEC_GENERATOR.md`
- [ ] `specs/MODULE_SPEC_TAGGING.md`
- [ ] `specs/MODULE_SPEC_EVALUATION.md`
- [ ] `specs/MODULE_SPEC_ANALYTICS.md`
- [ ] `specs/MODULE_SPEC_TUTOR.md`
- [ ] `specs/MODULE_SPEC_API.md`
- [ ] `specs/MODULE_SPEC_EVAL_HARNESS.md`

Each spec must include a "Corrections made to AI output" section with a non-empty, honest entry.

### Per-member evidence

- [ ] At least one Claude Code export in `exports/` per member
- [ ] Agent usage summary in `agent_usage/` per member
- [ ] At least 5 meaningful commits per member in Git history

A commit is meaningful if it: adds, modifies, or tests a named module artifact (spec, code file, test, fixture, or verification script), has a conventional commit message, and is traceable to a spec section or acceptance criterion.

### Source and data governance

- [ ] `data/sources.md` — source registry with review status for all ingested documents
- [ ] `data/rubrics/` — human-authored or human-reviewed rubric JSON files
- [ ] `data/fixtures/simulated_attempts.json` — student attempt fixture for analytics testing

### Tests and verification

- [ ] At least one test or verification script per module in `tests/`
- [ ] All module tests passing
- [ ] Evaluation harness generating a real Trust Dashboard report

### Artifacts

- [ ] `artifacts/screenshots/` — demo screenshots
- [ ] `artifacts/demo_outputs/` — sample system outputs
- [ ] `artifacts/evaluation_results/` — evaluation harness output files

### Pull request history

- [ ] All module work merged through PRs, not direct commits
- [ ] PR history visible in Git log and GitHub

---

## Appendix: Workflow Summary Card

```
Before writing any code:
  1. Draft module spec
  2. Submit spec PR
  3. Get Architect approval ("Spec approved — implementation may begin")
  4. Open implementation branch

For each implementation phase:
  1. Write one focused prompt targeting one function or class
  2. Review and correct AI output against spec
  3. Run test or verification script
  4. Commit with conventional commit message
  5. Record corrections in spec's "Corrections made to AI output" section

After each session:
  1. Run /cost or /stats if available
  2. Log row in TOKEN_USAGE.md
  3. Run /export and save to exports/
  4. Update agent_usage/<member-id>_<module>_usage.md

Before merging:
  1. Complete PR description (all 8 fields — see Section 6)
  2. Ensure tests pass
  3. Get reviewer approval
```
