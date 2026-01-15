# AI Playbook - Codex Task Plan

This file defines the section-by-section task plan for building the AI Development Playbook. Each task MUST be self-contained, commit-sized, deterministic, and safe to run without prior chat context.

## How to use this plan
- Tasks MUST run in order and MUST NOT be skipped.
- If a task target is already complete, work MUST stop and confirmation MUST be requested.
- If instructions conflict, work MUST stop and Section 13 MUST be followed.
- If scope changes, update this plan before proceeding.

## Global instruction (prepend to every task prompt)

Paste this at the top of every Codex prompt:

```
You are editing a Git repo. Target file: docs/ai/AI_PLAYBOOK.md.

Writing rules:
- Use UK English.
- Use explicit normative language: MUST / MUST NOT / SHOULD / MAY.
- Prefer bullets, tables, and checklists over paragraphs.
- No em dashes.
- No stack or language specifics.
- Add explicit stop conditions where ambiguity exists.
- Do not duplicate content that belongs in later sections; add cross-references by section number instead.
- Keep each section concise, enforceable, and testable.
```

---

## Task 0 - Repository scaffold (one-time) [x]

**Goal:** Create the initial structure with no prose dependency on prior context.

**Codex prompt:**
```
Create the initial repo documentation scaffold for an AI development playbook.

Do:
1) Create docs/ai/AI_PLAYBOOK.md containing ONLY the following table of contents (headings only, no prose):

# AI-Assisted Development Playbook

## 0. Purpose and Scope
## 1. Core Principles (Non-Negotiable)
## 2. Roles and Responsibility Boundaries
## 3. Change Classification and Risk Model
## 4. Mandatory Workflow (Order of Execution)
## 5. Test Strategy Decision Framework
## 6. Determinism Scaffolding
## 7. AI Usage Rules
## 8. Change Execution Rules
## 9. Review and Verification Gates
## 10. Release and Rollback Discipline
## 11. Documentation and Artefacts
## 12. Learning and Continuous Improvement
## 13. Compliance and Enforcement
## 14. Relationship to Stack-Specific Playbooks
## 15. Glossary and Definitions
## 16. Appendix

2) Create docs/ai/README.md (max 200 words) describing:
- what docs/ai contains,
- that AI_PLAYBOOK.md is canonical,
- that stack playbooks layer on top without redefining core rules.

3) Create templates/CHANGE_BRIEF_TEMPLATE.md with headings only:
- Goal
- Non-goals
- Acceptance criteria
- Constraints
- Risk and blast radius
- Test strategy
- Execution plan (ordered)
- Verification
- Rollback
- Notes/links

4) Create templates/PULL_REQUEST_TEMPLATE.md with headings only:
- Summary (what/why)
- Scope (in/out)
- Tests (what added/updated)
- Verification steps
- Risk assessment
- Rollback
- Checklist

Constraints:
- Use UK English.
- No em dashes.
- Do not add stack-specific guidance.
- Do not fill content beyond headings.
- Return a short list of files created.
```

**Stop conditions:**
- If any file already exists with content, stop and confirm whether to overwrite.
- If repo rules require commits, request explicit approval before committing.

---

## Task 1 - Section 0: Purpose and Scope [x]

Fill Section 0 of `docs/ai/AI_PLAYBOOK.md`.

Include:
- Purpose (1 to 3 bullets).
- Scope boundaries (governed vs not governed).
- Authority and precedence rules.
- How humans and AI tools are expected to use this document.

Constraints:
- Max 350 words.
- No examples.

---

## Task 2 - Section 1: Core Principles (Non-Negotiable) [x]

Fill Section 1.

Include exactly 7 principles.

For each principle:
- One sentence normative rule.
- One short "Why it exists" bullet (max 12 words).

Constraints:
- Conceptual only.
- No workflow steps.

---

## Task 3 - Section 2: Roles and Responsibility Boundaries [x]

Fill Section 2.

Include:
- A table with columns: Area | Human OWNS | AI MAY DO.
- A list of AI MUST NOT actions (minimum 10).
- Explicit stop-and-ask conditions.

Constraints:
- No tool or vendor references.

---

## Task 4 - Section 3: Change Classification and Risk Model [x]

Fill Section 3.

Include:
- Definitions for Small / Medium / Large changes.
- Risk dimensions: blast radius, reversibility, ambiguity.
- Matrix: change size × risk → required artefacts (reference Section 11).
- Forbidden change patterns (minimum 8).
- Stop-and-ask criteria (minimum 6).

---

## Task 5 - Section 4: Mandatory Workflow (Order of Execution) [x]

Fill Section 4.

Include:
- The only permitted workflow as a numbered list (6 to 10 steps).
- For each step: input, action, output (max 3 bullets each).
- Explicit rule forbidding skipping steps without exception.

Constraints:
- Refer to Sections 5 to 10 for detail.

---

## Task 6 - Section 5: Test Strategy Decision Framework [x]

Fill Section 5.

Include:
- Decision table: situation → primary strategy → minimum requirements.
- Definitions for:
  - True TDD
  - Characterisation testing
  - Contract testing
- What does NOT count as a safety net (minimum 8).
- Minimum acceptable test quality checklist (minimum 10).

---

## Task 7 - Section 6: Determinism Scaffolding [x]

Fill Section 6.

Include:
- Boundary selection rules.
- Normalising nondeterminism rules.
- Fixture and data stability rules.
- Acceptable assertions vs forbidden assertions (minimum 8 each).
- "Safety net ready" checklist (minimum 8).

---

## Task 8 - Section 7: AI Usage Rules [ ]

Fill Section 7.

Include:
- Allowed AI actions (minimum 12).
- Restricted actions with conditions (minimum 10).
- Prohibited actions (minimum 10).
- Prompting requirements checklist.
- Output validation rules.

---

## Task 9 - Section 8: Change Execution Rules [ ]

Fill Section 8.

Include:
- Diff size and scope limits (enforceable guidance).
- Dependency introduction rules.
- Refactoring rules (behaviour-preserving first).
- Interface and contract stability rules.
- Failure handling expectations.

---

## Task 10 - Section 9: Review and Verification Gates [ ]

Fill Section 9.

Include:
- Test review checklist (minimum 12).
- Code review focus list (minimum 12).
- Verification checklist split into:
  - Automated
  - Manual
  - Observability
- Triggers requiring heightened review.

---

## Task 11 - Section 10: Release and Rollback Discipline [ ]

Fill Section 10.

Include:
- Preconditions for release.
- Rollback plan requirements.
- Monitoring expectations.
- Post-release verification steps.

---

## Task 12 - Section 11: Documentation and Artefacts [ ]

Fill Section 11.

Define required artefacts and their minimum contents:
- Change Brief
- Execution Plan
- Safety Net Plan
- ADR
- Verification Checklist
- Release/Rollback Plan

Do not include examples.

---

## Task 13 - Section 12: Learning and Continuous Improvement [ ]

Fill Section 12.

Include:
- Lightweight post-change review template.
- Rules for updating the playbook.
- Deprecation process.

---

## Task 14 - Section 13: Compliance and Enforcement [ ]

Fill Section 13.

Include:
- CI enforcement expectations (generic).
- Non-compliance handling.
- Exceptions process.
- Measuring adherence.

---

## Task 15 - Section 14: Relationship to Stack-Specific Playbooks [ ]

Fill Section 14.

Include:
- Layering model.
- Override rules.
- Conflict resolution.
- Process for adding a new stack playbook.

---

## Task 16 - Section 15: Glossary and Definitions [ ]

Fill Section 15.

Define key terms concisely (1 to 2 sentences each), including:
- determinism scaffolding
- safety net
- characterisation test
- contract test
- boundary
- blast radius
- reversibility
- ambiguity
- stop condition
- acceptance criteria
- non-goal
- ADR

---

## Task 17 - Section 16: Appendix (Examples) [ ]

Fill Section 16.

Include:
- Example Change Brief
- Example Execution Plan
- Example AI prompt wrapper
- Example failure scenarios (minimum 5)
- Example compliant vs non-compliant changes (minimum 6 pairs)

Keep examples generic and stack-agnostic.

---

## Task 18 - Quality control pass (final) [ ]

Audit `docs/ai/AI_PLAYBOOK.md` for:
- duplication,
- ambiguity,
- missing stop conditions,
- missing cross-references,
- stack-specific leakage,
- use of em dashes.

Apply fixes directly and produce a short changelog.

**Stop conditions:**
- If fixes require new sections or scope expansion, stop and seek approval.
- If changes exceed the documented constraints, stop and request guidance.
