# AI-Assisted Development Playbook

## 0. Purpose and Scope
### Purpose
1. This playbook MUST define the minimum rules for AI-assisted change delivery.
2. This playbook MUST protect safety, quality, and accountability across the repository.
3. This playbook MUST define minimum artefacts and evidence for review.
4. This playbook SHOULD enable consistent decision-making and predictable outcomes.

### Scope boundaries
- **Governed**
  1. All changes that use AI assistance for analysis, design, code, or documentation.
  2. All changes that modify tracked files or tooling used in delivery.
  3. All changes that alter prompts, instructions, or outputs stored in the repo.
  4. All changes that affect tests, review gates, releases, or compliance artefacts.
  5. All changes that affect determinism scaffolding or reproducibility controls.
- **Not governed**
  1. Personal notes, drafts, or experimental work outside the repository.
  2. Non-repo communications, planning tools, or external issue trackers.
  3. Third-party documentation and vendor policies not checked into the repo.
  4. Stack-specific rules, which MUST live in Section 14 and its referenced documents.
  5. Runtime operations outside defined release and rollback procedures in Section 10.

### Precedence rules
1. Repo rules and security policies MUST take precedence over this playbook.
2. This playbook MUST take precedence over stack-specific playbooks.
3. If a stack-specific playbook is stricter, the stricter rule MUST be followed.
4. If two rules conflict and precedence is unclear, work MUST stop and a decision MUST be recorded.
5. If a rule is missing for a required action, work MUST stop and [Section 13](#13-compliance-and-enforcement) MUST be followed.

### How to use this document
1. Humans MUST read [Section 4](#4-mandatory-workflow-order-of-execution) before starting any change.
2. Humans SHOULD classify change risk using [Section 3](#3-change-classification-and-risk-model).
3. AI tools MUST follow [Section 7](#7-ai-usage-rules) and [Section 8](#8-change-execution-rules) verbatim.
4. AI tools MUST stop and request input when scope is unclear.
5. AI tools SHOULD reference section numbers when requesting decisions.
6. If a mandatory step cannot be completed, work MUST stop and [Section 13](#13-compliance-and-enforcement) MUST be followed.
7. Everyone MUST verify gates using [Section 9](#9-review-and-verification-gates) before release.
8. Everyone SHOULD record required artefacts per [Section 11](#11-documentation-and-artefacts).
9. Re-evaluate [Section 0](#0-purpose-and-scope) when scope changes or new constraints appear.
## 1. Core Principles (Non-Negotiable)
### Principles
1. Human accountability
   - Rule: A human owner MUST remain accountable for every change and outcome.
   - Why it exists: Ensures ownership and legal responsibility.
2. Safety before speed
   - Rule: Safety and reversibility MUST take priority over delivery speed.
   - Why it exists: Reduces harm and recovery cost.
3. Evidence-based decisions
   - Rule: Decisions MUST be supported by recorded evidence and rationale.
   - Why it exists: Improves traceability and auditability.
4. Determinism first
   - Rule: Changes MUST be made testable and repeatable through determinism scaffolding.
   - Why it exists: Prevents flaky outcomes and hidden regressions.
5. Minimal change surface
   - Rule: Changes SHOULD be the smallest coherent unit that meets the goal.
   - Why it exists: Limits blast radius and review burden.
6. Explicit boundaries
   - Rule: Boundaries, constraints, and non-goals MUST be stated before execution.
   - Why it exists: Avoids scope creep and ambiguity.
7. Respect policy hierarchy
   - Rule: Conflicts MUST be resolved using [Section 0](#0-purpose-and-scope) precedence rules.
   - Why it exists: Prevents inconsistent application of rules.
## 2. Roles and Responsibility Boundaries
### Responsibility matrix
| Area | Human OWNS | AI MAY DO |
| --- | --- | --- |
| Goals and acceptance criteria | Define objectives, scope, and success criteria | Summarise requirements and highlight gaps for approval |
| Risk classification | Classify change size and risk using [Section 3](#3-change-classification-and-risk-model) | Propose classification and cite rationale for review |
| Change brief and artefacts | Approve required artefacts per [Section 11](#11-documentation-and-artefacts) | Draft artefacts for human review |
| Design decisions | Approve final decisions and constraints | Offer options, trade-offs, and decision questions |
| Implementation | Own edits and approve final changes | Draft edits within agreed scope |
| Testing strategy | Choose strategy using [Section 5](#5-test-strategy-decision-framework) | Propose tests and coverage gaps |
| Verification | Confirm gates in [Section 9](#9-review-and-verification-gates) | Summarise verification evidence |
| Release and rollback | Approve release and rollback per [Section 10](#10-release-and-rollback-discipline) | Draft release steps and risk notes |
| Compliance and exceptions | Approve exceptions using [Section 13](#13-compliance-and-enforcement) | Identify compliance risks and missing evidence |

### AI MUST NOT actions
1. AI MUST NOT approve or authorise a change.
2. AI MUST NOT change scope, goals, or acceptance criteria without human approval.
3. AI MUST NOT execute releases or rollbacks.
4. AI MUST NOT alter compliance rules or enforcement decisions.
5. AI MUST NOT bypass or disable verification gates in [Section 9](#9-review-and-verification-gates).
6. AI MUST NOT introduce dependencies without explicit approval.
7. AI MUST NOT modify security-sensitive material without human review.
8. AI MUST NOT edit outside agreed files or directories.
9. AI MUST NOT claim a step is complete without evidence.
10. AI MUST NOT proceed when a stop condition is triggered.
11. AI MUST NOT invent requirements, constraints, or acceptance criteria.
12. AI MUST NOT conceal uncertainty or unresolved ambiguity.

### Stop and ask conditions
1. If ownership is unclear for any area in the matrix, work MUST stop and a human decision MUST be recorded.
2. If requested work conflicts with [Section 0](#0-purpose-and-scope) or repo rules, work MUST stop and a decision MUST be recorded.
3. If change size or risk cannot be classified using [Section 3](#3-change-classification-and-risk-model), work MUST stop and a human decision MUST be recorded.
4. If required artefacts are missing per [Section 11](#11-documentation-and-artefacts), work MUST stop until they exist.
5. If verification gates in [Section 9](#9-review-and-verification-gates) cannot be met, work MUST stop and escalation MUST follow [Section 13](#13-compliance-and-enforcement).
6. If release or rollback approval is absent, work MUST stop and approval MUST be requested per [Section 10](#10-release-and-rollback-discipline).
7. If AI output cannot be validated against scope or constraints, work MUST stop and request clarification.
8. If any prohibited action in [Section 7](#7-ai-usage-rules) would be required, work MUST stop and request an alternative.
## 3. Change Classification and Risk Model
### Change size definitions
- **Small**
  1. Limited to a single component or isolated change surface.
  2. Low risk of cross-cutting impact or behavioural shift.
  3. Reversal is straightforward without complex dependency changes.
- **Medium**
  1. Spans multiple components or interfaces within a bounded area.
  2. Moderate risk of behavioural change or integration impact.
  3. Reversal requires coordinated changes but remains feasible.
- **Large**
  1. Spans multiple domains, interfaces, or shared contracts.
  2. High risk of systemic impact or ambiguous behaviour.
  3. Reversal is complex or requires multi-step remediation.

### Risk dimensions
- **Blast radius**
  1. The number of components, users, or workflows affected by failure.
  2. The scope of downstream impact if the change behaves incorrectly.
- **Reversibility**
  1. The effort and time required to undo the change safely.
  2. The residual impact after rollback or remediation.
- **Ambiguity**
  1. The level of uncertainty in requirements, outcomes, or constraints.
  2. The degree of hidden coupling or unknown dependencies.

### Required artefacts matrix
| Change size | Low risk | Medium risk | High risk |
| --- | --- | --- | --- |
| Small | Change Brief, Safety Net Plan | Change Brief, Safety Net Plan, Verification Checklist | Change Brief, Safety Net Plan, Verification Checklist, Execution Plan |
| Medium | Change Brief, Safety Net Plan, Execution Plan | Change Brief, Safety Net Plan, Execution Plan, Verification Checklist | Change Brief, Safety Net Plan, Execution Plan, Verification Checklist, Release/Rollback Plan |
| Large | Change Brief, Safety Net Plan, Execution Plan, Verification Checklist | Change Brief, Safety Net Plan, Execution Plan, Verification Checklist, Release/Rollback Plan | Change Brief, Safety Net Plan, Execution Plan, Verification Checklist, Release/Rollback Plan, Architecture Decision Record |
- Artefact definitions and minimum contents MUST follow [Section 11](#11-documentation-and-artefacts).

### Forbidden change patterns
1. Changing acceptance criteria without updating required artefacts.
2. Shipping changes with undefined ownership or accountability.
3. Skipping verification gates in [Section 9](#9-review-and-verification-gates).
4. Introducing new dependencies without explicit approval.
5. Expanding scope after execution begins without reclassification.
6. Proceeding with ambiguous requirements or unstated constraints.
7. Modifying shared contracts without impact assessment.
8. Bypassing determinism scaffolding for tests in [Section 6](#6-determinism-scaffolding).
9. Making irreversible changes without a rollback plan.
10. Releasing without evidence of required tests or checks.

### Stop and ask criteria
1. If change size or risk cannot be agreed, work MUST stop and [Section 2](#2-roles-and-responsibility-boundaries) MUST be followed.
2. If any risk dimension is high and artefacts are missing, work MUST stop until artefacts exist.
3. If a change triggers a forbidden pattern, work MUST stop and a decision MUST be recorded.
4. If scope expands beyond the current classification, work MUST stop and reclassify.
5. If dependencies or contracts change unexpectedly, work MUST stop and re-evaluate risk.
6. If ambiguity remains after clarification attempts, work MUST stop and a decision MUST be recorded.
7. If verification evidence is missing for the current risk level, work MUST stop and follow [Section 9](#9-review-and-verification-gates).
## 4. Mandatory Workflow (Order of Execution)
### Workflow rule
1. Steps MUST NOT be skipped or reordered.
2. If a step cannot be completed, work MUST stop and follow [Section 13](#13-compliance-and-enforcement).

### Workflow
1. Classify change and risk
   - Input: Current scope, constraints, and intended outcomes.
   - Action: Classify size and risk using [Section 3](#3-change-classification-and-risk-model).
   - Output: Recorded change size, risk level, and rationale.
2. Define artefacts and plan
   - Input: Classification outcome and requirements.
   - Action: Prepare required artefacts per [Section 11](#11-documentation-and-artefacts).
   - Output: Approved Change Brief and execution plan draft.
3. Design and boundary decisions
   - Input: Artefact drafts and constraints.
   - Action: Confirm boundaries and decisions with [Section 6](#6-determinism-scaffolding) in view.
   - Output: Approved boundaries, assumptions, and constraints.
4. Implement change
   - Input: Approved plan and boundaries.
   - Action: Make changes within scope following [Section 8](#8-change-execution-rules).
   - Output: Traceable changes ready for verification.
5. Build safety net
   - Input: Updated change set.
   - Action: Select and apply testing strategy per [Section 5](#5-test-strategy-decision-framework).
   - Output: Evidence of test coverage and determinism scaffolding.
6. Verify and review
   - Input: Change set and test evidence.
   - Action: Run verification gates per [Section 9](#9-review-and-verification-gates).
   - Output: Recorded verification results and decision.
7. Release and rollback readiness
   - Input: Verification results and risk level.
   - Action: Prepare release and rollback per [Section 10](#10-release-and-rollback-discipline).
   - Output: Release or rollback plan with approval status.
8. Close and record
   - Input: Release outcome and evidence.
   - Action: Record artefacts and outcomes per [Section 11](#11-documentation-and-artefacts).
   - Output: Updated documentation and audit trail.
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
