# PROJECT_SPEC.md — AI Tutor & Exam Practice System

## 1. Problem Statement

School students across boards such as CBSE, ICSE/CISCE, and IGCSE often need exam-oriented practice, topic-level feedback, and personalized remediation. Existing tools may generate generic answers or practice questions without grounding them in the correct syllabus, learning outcomes, previous papers, or marking schemes.

This project builds an AI Tutor & Exam Practice System that generates syllabus-grounded practice, evaluates student answers, detects weak areas, and gives personalized remediation.

The project must demonstrate responsible agentic development using Spec-Driven Development. The professor will evaluate whether the team used Claude Code with understanding and control, or simply performed vibe coding.

---

## 2. MVP Scope

The MVP will implement one complete vertical slice.

- Board: CBSE
- Grade: Class 10
- Subject: Mathematics
- Chapters: 2–3 selected chapters

Initial chapters:

- Quadratic Equations
- Applications of Trigonometry
- Arithmetic Progressions

The system design should remain extensible to ICSE/CISCE and IGCSE, but the working implementation will focus only on the MVP scope above.

The final report must clearly distinguish between implemented features and future extensions.

---

## 3. Non-Goals

The MVP will not claim full support for all boards, all grades, or all subjects.

The MVP will not ingest complete textbooks at large scale.

The MVP will not guarantee official board-level grading accuracy.

The MVP will not generate answers without retrieved syllabus or study context.

The MVP will not claim that LLM-generated questions are official board questions.

The MVP will not fabricate evaluation metrics, token usage, or official source coverage.

Case-based questions are a stretch goal. The MVP must support MCQ, short answer, and long answer questions first.

---

## 4. Target Users

Primary users:

- School students preparing for exams
- Teachers who want practice papers and topic-level analysis
- Parents or mentors who want weak-area summaries

Secondary users:

- Project evaluators who want to inspect whether the AI system is grounded, tested, and responsibly built
- Developers who want to extend the system to other boards, grades, or subjects

---

## 5. Core Modules

The system will contain the following product modules:

1. Syllabus ingestion
2. RAG-based retrieval
3. Practice paper generation
4. Question tagging and difficulty classification
5. Automatic answer evaluation
6. Weakness detection and mastery tracking
7. Personalized remediation
8. Tutor chatbot
9. UI / integration layer

The project will also contain the following infrastructure and evidence modules:

10. Trust & Evaluation Dashboard
11. Evaluation harness
12. Agentic evidence tracking

Folder mapping:

- src/ingestion/ maps to Syllabus ingestion.
- src/rag/ maps to RAG-based retrieval.
- src/generator/ maps to Practice paper generation.
- src/tagging/ maps to Question tagging and difficulty classification.
- src/evaluation/ maps to Automatic answer evaluation.
- src/analytics/ maps to Weakness detection and mastery tracking.
- src/tutor/ maps to Personalized remediation and Tutor chatbot.
- src/api/ maps to UI / integration layer.
- src/evaluation_harness/ maps to Evaluation harness and Trust Dashboard support.

Delivery target:

The MVP user interface will be implemented using Streamlit or a simple API-backed UI. The final choice must be recorded in ARCHITECTURE.md before UI implementation begins.

Each module must have a module-specific SPEC file before implementation begins.

---

## 6. Data Model and Source Governance

The syllabus will be represented using the following hierarchy:

Board → Grade → Subject → Chapter → Topic → Learning Outcome

Each syllabus item should include:

- board
- grade
- subject
- chapter
- topic
- learning_outcome
- source_reference
- source_id
- chunk_id

Example conceptual record:

- board: CBSE
- grade: Class 10
- subject: Mathematics
- chapter: Quadratic Equations
- topic: Nature of Roots
- learning_outcome: Student can determine the nature of roots using the discriminant
- source_reference: Official syllabus or curated study material reference
- source_id: cbse_math_10_syllabus
- chunk_id: cbse_math_10_quad_eq_chunk_01

Source governance rules:

- All source documents used for syllabus, study material, sample questions, answer keys, and rubrics must be listed in data/sources.md before ingestion.
- Source entries must include source_id, title, board, grade, subject, source type, and review status.
- Curated study material must be human-reviewed before it is treated as reliable retrieval context.
- Answer keys must be human-authored or human-reviewed before being used for evaluation.
- Rubrics and marking schemes must be human-authored or human-reviewed. LLM-generated rubrics must not be used as the sole grading authority.

The system should store source metadata wherever AI generation depends on external or curriculum-specific content.

---

## 7. RAG Grounding Rules

The system must use Retrieval-Augmented Generation wherever an AI-generated response depends on syllabus, study material, previous questions, marking schemes, or learning outcomes.

RAG must be used for:

- tutor chatbot answers
- remediation notes
- practice question generation
- explanation generation
- subjective answer feedback, wherever rubric or context is required

Each retrieved chunk must include metadata:

- board
- grade
- subject
- chapter
- topic
- source_id
- chunk_id

Generated answers should include source references wherever possible.

For the MVP, retrieval confidence is treated as low if the top retrieved chunk score is below the threshold selected in the RAG module spec. The initial default threshold is 0.60 cosine similarity for embedding-based retrieval. The RAG module owner may adjust this threshold after testing, but the reason must be documented in the RAG module spec or evaluation notes.

If retrieval confidence is low, the system must not confidently answer. It should either ask for clarification or return a controlled message saying that the query is outside the current syllabus scope.

Out-of-syllabus queries must be detected and flagged.

For every non-trivial tutor answer, the system must log retrieved chunk IDs. A response fails the grounding check if no retrieved chunk is attached.

The MVP corpus must contain at least 5 indexed chunks per selected chapter.

The system must avoid generating unsupported facts that are not grounded in the selected board, grade, subject, and chapter context.

---

## 8. Practice Paper Generation Rules

The practice paper generator must generate questions only from the selected syllabus scope.

Inputs:

- board
- grade
- subject
- chapter or topic
- total marks
- difficulty distribution
- question type distribution

MVP-supported question types:

- MCQ
- short answer
- long answer

Stretch question type:

- case-based question

Each generated question must include:

- question_id
- question_text
- board
- grade
- subject
- chapter
- topic
- marks
- difficulty: easy / medium / hard
- question_type
- skill_tested: recall / application / reasoning
- source_context_id

The generator must ensure that total marks match the requested paper configuration.

The generator must not create questions from chapters or topics outside the selected scope.

Generated questions should be traceable to retrieved syllabus chunks or sample question patterns.

Verification rules:

- A unit test or verification script must assert that generated paper marks sum to the requested total.
- source_context_id must refer to an indexed chunk or approved sample-question source.
- The evaluation harness must check that at least 90% of generated questions in the MVP demo carry a valid source_context_id.

---

## 9. Answer Evaluation Rules

Objective questions such as MCQs must be evaluated deterministically using answer keys.

Subjective questions must be evaluated using a rubric or marking scheme.

The evaluator must output:

- awarded_score
- max_score
- feedback
- missing_concepts
- error_type, if identifiable
- confidence
- rubric_id or marking_scheme_id, wherever applicable

For Mathematics, the evaluator should support step-wise scoring where feasible.

For the MVP, step-wise scoring must be demonstrated for at least one worked Mathematics question from one selected chapter. Other subjective questions may use rubric-based scoring.

Example scoring dimensions:

- correct formula selection
- correct substitution
- correct intermediate calculation
- correct final answer
- proper reasoning or explanation

The system must not assign subjective marks without reference to a rubric, marking scheme, or expected answer structure.

The evaluator must not fabricate official board scores. The output should be presented as AI-assisted evaluation, not official grading.

---

## 10. Weakness Detection Rules

The system must maintain a student knowledge profile at topic level.

Profile format:

Topic → Accuracy → Time Taken → Attempts → Confidence → Mastery Score

For each student attempt, the system should update:

- topic attempted
- question type
- difficulty
- score
- time taken
- number of attempts
- mistake type, if available

Student confidence may be captured in two ways:

- self-reported confidence, if the UI asks the student after an attempt
- system-inferred confidence, estimated from score, time taken, attempts, and difficulty

For the MVP, system-inferred confidence is sufficient. The formula must be documented in the analytics module spec.

Weakness detection should identify topics where the student shows:

- low accuracy
- repeated mistakes
- high time taken
- low confidence
- poor performance on application or reasoning questions

Weak-area summaries must be derived from stored attempt data such as topic accuracy, score, time taken, and mistake type. They must not be open-ended unsupported generation.

The system should produce a weak-area summary such as:

"The student is weak in Applications of Trigonometry. Formula recall is acceptable, but mistakes occur in diagram interpretation and selecting the correct trigonometric ratio."

For the MVP, a simple mastery score is acceptable. Full Bayesian Knowledge Tracing can be discussed as an extension if not fully implemented.

The test fixture for weakness detection must include a small JSON file of simulated student attempts. The analytics module must use this fixture to verify that the weakest topic is identified correctly.

---

## 11. Remediation and Tutor Chatbot Rules

For weak topics, the system should generate personalized remediation.

Supported remediation outputs:

- short notes
- formula sheet
- 5-minute revision card
- extra practice questions
- step-by-step explanation
- static prerequisite-based learning path within the selected chapters

Formula sheets and short notes must be generated from verified retrieved chunks, not from the LLM's parametric memory alone.

The tutor chatbot must answer according to the selected:

- board
- grade
- subject
- chapter
- topic

The chatbot must use retrieved context before answering syllabus-specific questions.

The chatbot should avoid overly advanced explanations unless explicitly requested.

If a student asks an out-of-syllabus question, the chatbot should either:

- say that the question is outside the current syllabus scope, or
- ask the student to change board, grade, subject, or chapter context

The chatbot must not hallucinate textbook claims, marking rules, or board-specific requirements without retrieved support.

---

## 12. Trust & Evaluation Dashboard

The Trust & Evaluation Dashboard is a professor-facing and developer-facing feature that shows whether the system is grounded, tested, and built responsibly.

For the MVP, the dashboard may be implemented as a script-generated report and/or a Streamlit view. It does not need to be a fully live production dashboard.

The dashboard should summarize:

- number of generated questions
- percentage of generated questions with valid source_context_id
- number of tutor answers with retrieved source chunks
- number of out-of-syllabus queries detected
- answer evaluation consistency checks
- test pass/fail summary
- module-wise acceptance criteria status
- export log availability for each member
- agent usage file availability for each member
- Git commit summary by member
- token usage availability, if captured

The dashboard must not fabricate token counts or evaluation scores.

If token usage is unavailable, it should state:

"Exact token count was not captured."

The dashboard should help prove that the team did not rely on vibe coding.

---

## 13. Acceptance Criteria

The project is acceptable if the following criteria are met.

### MVP Demo Flow

The MVP demo must support the following end-to-end flow:

1. Student selects board, grade, subject, and chapter.
2. System retrieves syllabus or study context for the selected scope.
3. System generates a short practice paper from the selected chapter.
4. Student submits answers for at least one objective and one subjective question.
5. Objective answer is checked deterministically.
6. Subjective answer is evaluated using rubric or expected-answer context.
7. System updates the topic-level student profile.
8. System identifies at least one weak topic.
9. System generates remediation notes or extra practice for the weak topic.
10. Student asks one doubt.
11. Tutor chatbot answers using retrieved context or refuses if out of scope.
12. Trust & Evaluation Dashboard reports grounding, tests, exports, token usage availability, and Git evidence.

### Functional Criteria

- One end-to-end demo flow works.
- The MVP supports CBSE Class 10 Mathematics for selected chapters.
- Syllabus data follows the hierarchy: Board → Grade → Subject → Chapter → Topic → Learning Outcome.
- The MVP corpus contains at least 5 indexed chunks per selected chapter.
- RAG retrieval returns relevant chunks with metadata.
- RAG retrieval logs retrieved chunk IDs for non-trivial generated answers.
- Practice paper generation produces questions with topic, marks, difficulty, type, and source_context_id.
- At least 90% of generated questions in the MVP demo have valid source_context_id.
- Generated paper total marks match the requested paper configuration.
- Objective answer evaluation works deterministically.
- Subjective answer evaluation uses rubric or expected answer context.
- Step-wise scoring is demonstrated for at least one worked Mathematics question.
- Weakness detection identifies at least one weak topic from simulated student attempts.
- Remediation generates topic-specific notes or practice using retrieved context.
- Tutor chatbot answers are grounded in retrieved context.
- Out-of-syllabus queries are flagged or refused.
- Trust & Evaluation Dashboard reports grounding, tests, exports, token usage availability, and Git evidence.
- RAG retrieval should complete within 5 seconds for a single query on the MVP corpus on a normal development machine.
- Chatbot response generation should complete within a reasonable demo-time limit. The exact target must be finalized in the tutor module spec based on the selected LLM/API setup.

### Process Criteria

- CLAUDE.md exists and defines project-level agent rules.
- PROJECT_SPEC.md exists before implementation.
- Each module has a module-specific SPEC file.
- Each module spec includes a "Corrections made to AI output" section.
- Each member has at least one raw Claude Code export log for their module.
- Each member has an agent usage summary.
- Git history shows distributed work.
- Each member should make at least 5 meaningful commits, each linked to a spec, test, implementation phase, or documentation update.
- Module work must be merged through pull requests into main.
- Tests or verification scripts exist for core modules.
- Each module must include at least one test or verification script covering its main acceptance criteria.
- Final metrics are generated from actual scripts or command outputs.
- No token usage or evaluation metric is fabricated.

---

## 14. Required Output Files

Project-level files:

- CLAUDE.md
- PROJECT_SPEC.md
- README.md
- ARCHITECTURE.md
- TEAM_WORKFLOW.md
- TEAM_TRACKER.md
- FINAL_REPORT.md
- TOKEN_USAGE.md
- results.md
- requirements.txt

Module folders:

- src/ingestion/
- src/rag/
- src/generator/
- src/tagging/
- src/evaluation/
- src/analytics/
- src/tutor/
- src/api/
- src/evaluation_harness/

Evidence folders:

- specs/
- tests/
- exports/
- agent_usage/
- artifacts/screenshots/
- artifacts/demo_outputs/
- artifacts/evaluation_results/

Important final artifacts:

- data/sources.md
- module SPEC files
- test outputs
- simulated student attempts fixture
- evaluation summary
- demo screenshots
- per-member exports
- per-member agent usage files
- Git history summary

---

## 15. Team Deliverables

Each member must provide:

- module-specific SPEC file
- code or documentation contribution
- test or verification output
- Claude Code /export file
- agent usage summary
- meaningful Git commits

Each module owner must follow:

spec → review → plan → approve → implement phase → verify → commit → export

The workflow reviewer/approver must be defined in TEAM_WORKFLOW.md. At minimum, the architect must review every module spec before implementation begins.

The team must avoid having one person generate all files.

Every member should show visible effort through:

- module planning
- spec review
- manual corrections
- test execution
- Git commits
- export logs

The architect must maintain:

- project-level spec
- team workflow
- team tracker
- architecture document
- final report structure
- submission checklist

TEAM_TRACKER.md must assign a primary owner and supporting owner for each module before module implementation begins.

TOKEN_USAGE.md must include one row per member and must record token/cost usage if available. If exact usage is unavailable, it must state that exact token count was not captured.

---

## 16. Professor-Facing Evidence

The final submission should clearly demonstrate that the team did not do vibe coding.

Evidence should include:

- project-level CLAUDE.md
- project-level PROJECT_SPEC.md
- module-level SPEC files
- raw Claude Code exports from all members
- agent usage summaries from all members
- Git commit history
- pull request history
- tests and command outputs
- evaluation dashboard output
- final results file
- demo screenshots or demo recording notes

The final report should explicitly explain:

- how SDD was followed
- how hallucination was reduced
- how token usage was controlled
- how RAG grounding was enforced
- how outputs were verified
- how each team member contributed

The team must not fabricate:

- token usage
- test results
- model outputs
- retrieval scores
- evaluation scores
- official board coverage

If a feature is only partially implemented, the report must clearly mark it as a limitation or future work.
