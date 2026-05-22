# MODULE_SPEC_<NAME>.md — <Module Name>

> **Status:** Draft / Under Review / Approved
> **Primary Owner:** Member N — Name
> **Supporting Owner:** Member N — Name
> **Architect Approval:** Pending / Approved (date)
> **Aligned with:** PROJECT_SPEC.md §__, ARCHITECTURE.md §__

---

## 1. Module Goal

One sentence. What this module does and why it exists in the system.

---

## 2. Owner and Supporting Owner

| Role | Member | Responsibility |
|---|---|---|
| Primary Owner | Member N | Spec, implementation, tests, exports |
| Supporting Owner | Member N | Review, backup implementation, peer testing |

---

## 3. Inputs

| Input | Type | Source | Required |
|---|---|---|---|
| — | — | — | — |

---

## 4. Outputs

| Output | Type | Destination | Notes |
|---|---|---|---|
| — | — | — | — |

---

## 5. Dependencies

| Dependency | Type | Owner | Notes |
|---|---|---|---|
| — | Module / Library / Data file | — | — |

---

## 6. Data Schema

Define any input or output data structures this module owns or produces.

```json
{
  "field": "type — description"
}
```

If this module depends on a schema owned by another module (e.g. simulated_attempts.json, rubric JSON), reference it here by filename and owner. Do not redefine it.

---

## 7. Public Interface Contract

List every function `src/api/` or other modules will call. Fill in signatures before implementation begins.

```python
def function_name(param: type, param: type) -> return_type:
    ...
```

All LLM calls must go through the shared LLM adapter. No direct SDK calls in module code.

---

## 8. Acceptance Criteria

Derived from PROJECT_SPEC.md §13. Each criterion must be measurable.

| # | Criterion | Pass condition |
|---|---|---|
| 1 | — | — |

---

## 9. Test and Verification Plan

| Test | File | What it asserts |
|---|---|---|
| — | `tests/test_<module>.py` | — |

- Tests must run without live API credentials. Use the LLM mock adapter for all LLM-dependent paths.
- Final metrics must come from script output, not hand-written results.

---

## 10. Anti-Hallucination Rules

List the specific constraints that prevent this module from generating unsupported output.

- [ ] All LLM calls use retrieved chunks from RAG, not parametric memory alone.
- [ ] Low-confidence retrievals (score < 0.60) must not trigger LLM generation.
- [ ] All generated content must include source_context_id or chunk_id references where applicable.
- [ ] Add any module-specific rules below.

---

## 11. Token-Saving Plan

| Session | Scope | What to paste into Claude Code |
|---|---|---|
| Phase A | — | Relevant spec section only — §__ |
| Phase B | — | Relevant spec section only — §__ |

- One phase per session. Do not paste the full spec or architecture doc.
- Target one function or class per prompt.

---

## 12. Files to Produce

| File | Purpose |
|---|---|
| `src/<module>/<file>.py` | — |
| `tests/test_<module>.py` | Module acceptance tests |
| `exports/m<N>_<module>_<date>.md` | Claude Code session export |
| `agent_usage/m<N>_<module>_usage.md` | Agent usage summary |

---

## 13. Corrections Made to AI Output

> **Required.** "None" is not acceptable. Record every correction, rejection, or manual addition made after AI generation. If no corrections were needed, explain what was manually verified and why.

| Session | What AI produced | What was corrected or rejected | Reason |
|---|---|---|---|
| — | — | — | — |

---

## 14. What Not to Implement

List scope boundaries — things that are explicitly out of scope for this module.

- Do not implement features belonging to another module's folder.
- Do not call LLM providers directly — use the adapter.
- Do not fabricate test results or metrics.
- Add any module-specific exclusions below.

---

## 15. Export and Agent Usage Requirements

| Requirement | File | Status |
|---|---|---|
| Claude Code session export | `exports/m<N>_<module>_<date>.md` | Pending |
| Agent usage summary | `agent_usage/m<N>_<module>_usage.md` | Pending |
| Token usage row in TOKEN_USAGE.md | Row for Member N | Pending |

Export must be filed after every substantive session. Agent usage summary must record prompts used, what was produced, and what was manually corrected.
