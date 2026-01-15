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
### Decision table
| Situation | Primary strategy | Minimum requirements |
| --- | --- | --- |
| New behaviour with clear acceptance criteria | True test-driven development | Tests defined before change, assertions aligned to acceptance criteria |
| Legacy behaviour with unclear intent | Characterisation testing | Baseline tests capturing current behaviour before changes |
| External contract or integration boundary | Contract testing | Tests validating inputs, outputs, and error handling |
| High ambiguity or unknown coupling | Characterisation testing | Baseline coverage plus explicit risk notes |
| High risk change with defined behaviour | True test-driven development | New tests plus coverage of critical paths |
| Mixed new and legacy behaviour | Combined strategy | Characterisation for existing behaviour, true test-driven development for new behaviour |

### Definitions
1. **True test-driven development**: Tests MUST be written before implementation and MUST drive design decisions.
2. **Characterisation testing**: Tests MUST capture existing behaviour without altering outcomes before refactoring.
3. **Contract testing**: Tests MUST validate behaviour at a defined boundary and MUST detect incompatible changes.

### What does NOT count as a safety net
1. Manual verification without recorded evidence.
2. Assertions that only check for successful execution.
3. Tests that rely on unstable or random data.
4. Tests that are not repeatable in the same environment.
5. Tests that only check formatting or presentation.
6. Tests that skip error paths and failure scenarios.
7. Tests that depend on shared state without isolation.
8. Tests that pass without verifying outcomes against acceptance criteria.
9. Tests that are flaky or intermittently failing.
10. Tests that are not reviewed against risk classification.

### Minimum acceptable test quality checklist
1. Tests MUST map to acceptance criteria and non-goals.
2. Tests MUST cover success and failure paths relevant to risk.
3. Tests MUST be deterministic per [Section 6](#6-determinism-scaffolding).
4. Tests MUST isolate behaviour at the intended boundary.
5. Tests MUST include clear, specific assertions.
6. Tests MUST record setup, inputs, and expected outcomes.
7. Tests MUST avoid shared mutable state across cases.
8. Tests MUST run within agreed time limits.
9. Tests MUST include coverage for rollback or reversibility expectations.
10. Tests MUST be reviewed against the current change classification in [Section 3](#3-change-classification-and-risk-model).
11. Tests SHOULD document any known gaps and risk trade-offs.
12. Tests SHOULD be updated when acceptance criteria change.
## 6. Determinism Scaffolding
### Boundary selection rules
1. Boundaries MUST be defined before test design begins.
2. Boundaries MUST align to the change scope and risk classification in [Section 3](#3-change-classification-and-risk-model).
3. Each boundary MUST declare inputs, outputs, and failure modes.
4. If boundaries overlap or conflict, work MUST stop and a decision MUST be recorded.

### Normalising nondeterminism rules
1. Sources of nondeterminism MUST be identified and listed before testing.
2. Nondeterministic inputs MUST be stabilised or controlled.
3. Time-dependent behaviour MUST be controlled with fixed references.
4. Randomness MUST be replaced with fixed values for tests.
5. External dependencies MUST be isolated or simulated.
6. If nondeterminism cannot be controlled, work MUST stop and escalation MUST follow [Section 13](#13-compliance-and-enforcement).

### Fixture and data stability rules
1. Fixtures MUST use stable identifiers and deterministic values.
2. Fixtures MUST be minimal and aligned to acceptance criteria.
3. Shared fixtures MUST include ownership and update rules.
4. Data setup MUST be repeatable across runs.
5. If fixture changes affect expected outcomes, change classification MUST be revisited.

### Acceptable assertions
1. Assertions that verify specific outputs against expected values.
2. Assertions that verify explicit error handling and failure responses.
3. Assertions that verify state transitions are complete and correct.
4. Assertions that verify ordering when ordering is an explicit requirement.
5. Assertions that verify boundary inputs and outputs match contracts.
6. Assertions that verify reversibility or rollback requirements.
7. Assertions that verify non-goals are preserved.
8. Assertions that verify determinism assumptions remain true.

### Forbidden assertions
1. Assertions that only check for successful execution.
2. Assertions that only check for non-null results.
3. Assertions that depend on current system time.
4. Assertions that depend on random values.
5. Assertions that accept any output without constraints.
6. Assertions that rely on external services without control.
7. Assertions that ignore error paths or failure modes.
8. Assertions that mask or silence failures.

### Safety net ready checklist
1. Boundaries are documented with inputs, outputs, and failure modes.
2. Nondeterminism controls are implemented and recorded.
3. Fixtures are minimal, stable, and reviewed.
4. Assertions cover success and failure paths.
5. Failure conditions are tested and observable.
6. Tests run deterministically under agreed conditions.
7. Risk classification aligns with test coverage in [Section 3](#3-change-classification-and-risk-model).
8. Verification readiness aligns with [Section 9](#9-review-and-verification-gates).
## 7. AI Usage Rules
### Allowed actions
1. Summarise requirements, scope, and constraints for confirmation.
2. Draft options and trade-offs for human decision.
3. Propose change classifications using [Section 3](#3-change-classification-and-risk-model).
4. Draft Change Briefs and execution artefacts per [Section 11](#11-documentation-and-artefacts).
5. Suggest test strategies using [Section 5](#5-test-strategy-decision-framework).
6. Draft determinism scaffolding steps per [Section 6](#6-determinism-scaffolding).
7. Generate change plans aligned to [Section 4](#4-mandatory-workflow-order-of-execution).
8. Implement changes within approved scope and files.
9. Summarise verification evidence per [Section 9](#9-review-and-verification-gates).
10. Flag missing information or ambiguous requirements.
11. Highlight risks, dependencies, and potential failure modes.
12. Propose release and rollback steps for approval.

### Restricted actions with conditions
1. Editing files beyond approved scope MAY occur only with explicit human approval.
2. Introducing new dependencies MAY occur only with explicit approval and risk reclassification.
3. Refactoring behaviour MAY occur only after characterisation testing per [Section 5](#5-test-strategy-decision-framework).
4. Expanding scope MAY occur only after reclassification per [Section 3](#3-change-classification-and-risk-model).
5. Modifying shared contracts MAY occur only with documented impact assessment.
6. Editing tests MAY occur only when linked to acceptance criteria changes.
7. Adjusting verification steps MAY occur only with human approval.
8. Modifying release or rollback plans MAY occur only with human approval.
9. Using generated artefacts for decisions MAY occur only after human review.
10. Proceeding after a stop condition MAY occur only after resolution per [Section 13](#13-compliance-and-enforcement).

### Prohibited actions
1. Approving or authorising a change.
2. Claiming verification passed without evidence.
3. Skipping or reordering steps in [Section 4](#4-mandatory-workflow-order-of-execution).
4. Concealing uncertainty or unresolved ambiguity.
5. Modifying scope without reclassification.
6. Bypassing determinism scaffolding in [Section 6](#6-determinism-scaffolding).
7. Altering compliance rules or enforcement decisions.
8. Releasing changes without human approval.
9. Changing acceptance criteria without updating artefacts.
10. Making security-sensitive changes without human review.
11. Inventing requirements or constraints.
12. Overwriting evidence or audit records.

### Prompting requirements checklist
1. Prompts MUST state goals, non-goals, and acceptance criteria.
2. Prompts MUST state change scope and file boundaries.
3. Prompts MUST state change classification assumptions or request classification.
4. Prompts MUST cite required artefacts from [Section 11](#11-documentation-and-artefacts).
5. Prompts MUST include stop conditions and escalation paths.
6. Prompts MUST request disclosure of uncertainty and assumptions.
7. Prompts SHOULD request links to relevant sections.
8. Prompts SHOULD request diffs for review.

### Output validation rules
1. Output MUST align to stated scope and constraints.
2. Output MUST reference required artefacts and evidence.
3. Output MUST include known risks and trade-offs.
4. Output MUST identify any missing information.
5. Output MUST be checked for prohibited actions.
6. Output MUST be verified against acceptance criteria.
7. Output MUST reference the workflow in [Section 4](#4-mandatory-workflow-order-of-execution).
8. Output MUST include stop conditions when ambiguity remains.
## 8. Change Execution Rules
### Diff size and scope limits
1. Each change MUST align to the approved scope and boundaries.
2. Large or multi-area changes MUST be decomposed into ordered steps.
3. If the diff exceeds the agreed scope, work MUST stop and reclassify per [Section 3](#3-change-classification-and-risk-model).
4. If required files exceed the planned set, work MUST stop and request approval.

### Dependency introduction rules
1. New dependencies MUST have explicit approval and documented rationale.
2. Dependency changes MUST include impact assessment and rollback notes.
3. If a dependency increases risk classification, work MUST stop and reclassify.
4. Dependency changes MUST be reflected in artefacts per [Section 11](#11-documentation-and-artefacts).

### Refactoring rules
1. Behaviour-preserving refactors MUST be separated from behaviour changes.
2. Behaviour changes MUST follow characterisation testing per [Section 5](#5-test-strategy-decision-framework) before refactoring.
3. Refactors MUST keep contracts stable unless approved.
4. If refactoring alters expected outcomes, work MUST stop and update classification.

### Interface and contract stability rules
1. Interfaces and contracts MUST remain stable unless change classification permits alteration.
2. Contract changes MUST include explicit impact assessment and migration steps.
3. If contract consumers are unclear, work MUST stop and identify owners.
4. Contract changes MUST include verification steps per [Section 9](#9-review-and-verification-gates).

### Failure handling expectations
1. Failures MUST be recorded with context, inputs, and expected outcomes.
2. Recovery steps MUST be documented for every failure path.
3. If failures are not understood, work MUST stop and request clarification.
4. Verification MUST include failure paths aligned to [Section 5](#5-test-strategy-decision-framework).
## 9. Review and Verification Gates
### Test review checklist
1. Tests map to acceptance criteria and non-goals.
2. Tests cover critical success paths for the change.
3. Tests cover failure paths and error handling.
4. Tests align to the chosen strategy in [Section 5](#5-test-strategy-decision-framework).
5. Tests include determinism controls per [Section 6](#6-determinism-scaffolding).
6. Tests isolate boundaries and avoid hidden coupling.
7. Tests use stable data and fixtures.
8. Tests include rollback or reversibility coverage where required.
9. Tests include evidence for changed behaviour.
10. Tests include evidence for unchanged behaviour where expected.
11. Tests document known gaps and risk trade-offs.
12. Tests include clear assertions and expected outcomes.

### Code review focus list
1. Changes align with approved scope and artefacts.
2. Risk classification matches the change complexity in [Section 3](#3-change-classification-and-risk-model).
3. Contracts and interfaces remain stable or have approved changes.
4. Dependencies follow [Section 8](#8-change-execution-rules) rules.
5. Determinism scaffolding is applied where needed.
6. Failure handling and recovery paths are complete.
7. Logging and error reporting are sufficient for verification.
8. Review evidence includes outputs and data changes.
9. Scope changes are reclassified and documented.
10. Security-sensitive changes have human review.
11. Verification evidence matches the checklist in this section.
12. Artefacts are updated per [Section 11](#11-documentation-and-artefacts).

### Verification checklist
- **Automated**
  1. All required tests pass for the change classification.
  2. Deterministic tests run without flakiness.
  3. Test results are recorded and traceable.
  4. Checks for failure paths are executed.
- **Manual**
  1. Manual verification steps are recorded with evidence.
  2. Manual checks cover risk areas and edge cases.
  3. Manual checks confirm non-goals remain unchanged.
  4. Manual checks align with acceptance criteria.
- **Observability**
  1. Monitoring signals are defined for risk areas.
  2. Observability includes alerts for failure conditions.
  3. Observability data is reviewed after change completion.
  4. Observability gaps are recorded for follow-up.

### Triggers requiring heightened review
1. High risk classification or large change size.
2. Changes to shared contracts or interfaces.
3. Changes affecting security or compliance expectations.
4. Changes that alter rollback complexity.
5. Changes with unresolved ambiguity.
6. Changes lacking determinism scaffolding or stable tests.
7. Changes introducing new dependencies.
8. Changes with limited or missing verification evidence.
## 10. Release and Rollback Discipline
### Preconditions for release
1. Verification gates MUST be complete per [Section 9](#9-review-and-verification-gates).
2. Required artefacts MUST be approved per [Section 11](#11-documentation-and-artefacts).
3. Risk classification MUST be current and documented per [Section 3](#3-change-classification-and-risk-model).
4. Release and rollback plans MUST be approved for medium or large changes.
5. If preconditions are not met, release MUST stop and follow [Section 13](#13-compliance-and-enforcement).

### Rollback plan requirements
1. Rollback steps MUST be defined, ordered, and testable.
2. Rollback MUST specify triggers and decision authority.
3. Rollback MUST include data or state recovery steps where required.
4. Rollback MUST include verification steps after execution.
5. If rollback cannot be executed safely, release MUST stop and escalate.

### Monitoring expectations
1. Monitoring signals MUST be defined for critical outcomes.
2. Monitoring MUST include alert thresholds for failure conditions.
3. Monitoring MUST be aligned to acceptance criteria and non-goals.
4. Monitoring ownership MUST be assigned before release.

### Post-release verification steps
1. Verify critical outcomes using documented criteria.
2. Confirm error and failure signals remain within thresholds.
3. Confirm rollback readiness remains available.
4. Record outcomes and follow-up actions in release artefacts.
## 11. Documentation and Artefacts
### Required artefacts and minimum contents
- **Change Brief**
  1. Goal and non-goals.
  2. Scope boundaries and constraints.
  3. Acceptance criteria and risk classification.
- **Execution Plan**
  1. Ordered steps aligned to [Section 4](#4-mandatory-workflow-order-of-execution).
  2. Dependencies and assumptions.
  3. Verification checkpoints and evidence outputs.
- **Safety Net Plan**
  1. Selected testing strategy per [Section 5](#5-test-strategy-decision-framework).
  2. Boundaries and determinism controls per [Section 6](#6-determinism-scaffolding).
  3. Coverage for success and failure paths.
- **Architecture Decision Record**
  1. Decision statement and rationale.
  2. Options considered and trade-offs.
  3. Consequences and follow-up actions.
- **Verification Checklist**
  1. Automated verification steps.
  2. Manual verification steps.
  3. Observability signals per [Section 9](#9-review-and-verification-gates).
- **Release and Rollback Plan**
  1. Release prerequisites and approvals.
  2. Rollback triggers, steps, and verification.
  3. Monitoring expectations per [Section 10](#10-release-and-rollback-discipline).
## 12. Learning and Continuous Improvement
### Post-change review template
1. Summary of change and intended outcomes.
2. Verification results and evidence links.
3. Gaps or defects discovered after release.
4. Root causes for any unexpected outcomes.
5. Actions to prevent recurrence and owners.
6. Updates required to playbook sections.

### Rules for updating the playbook
1. Updates MUST be tied to observed gaps or recurring failures.
2. Updates MUST reference affected sections and rationale.
3. Updates MUST be reviewed using [Section 9](#9-review-and-verification-gates).
4. If updates affect enforcement, work MUST follow [Section 13](#13-compliance-and-enforcement).
5. If updates introduce new requirements, work MUST update [Section 11](#11-documentation-and-artefacts).

### Deprecation process
1. Deprecated rules MUST include a replacement or removal rationale.
2. Deprecation MUST include a transition plan and owners.
3. Deprecation MUST include a cut-off date and verification criteria.
4. If a deprecation affects workflows, work MUST update [Section 4](#4-mandatory-workflow-order-of-execution).
## 13. Compliance and Enforcement
### Enforcement expectations
1. Enforcement MUST be automated where feasible and recorded.
2. Enforcement rules MUST align with [Section 9](#9-review-and-verification-gates).
3. If enforcement checks fail, work MUST stop and remediation MUST be recorded.
4. Enforcement scope MUST cover artefacts in [Section 11](#11-documentation-and-artefacts).

### Non-compliance handling
1. Non-compliance MUST be recorded with scope, impact, and owner.
2. Non-compliance MUST trigger a risk reclassification per [Section 3](#3-change-classification-and-risk-model).
3. Remediation MUST include deadlines and verification steps.
4. Repeat non-compliance MUST trigger a playbook update per [Section 12](#12-learning-and-continuous-improvement).

### Exceptions process
1. Exceptions MUST be requested before execution begins.
2. Exceptions MUST include scope, duration, and rationale.
3. Exceptions MUST include compensating controls and verification steps.
4. Exceptions MUST be approved by accountable owners.
5. If an exception affects release criteria, [Section 10](#10-release-and-rollback-discipline) MUST be followed.

### Measuring adherence
1. Adherence metrics MUST track verification completion and artefact coverage.
2. Adherence metrics MUST track exception frequency and outcomes.
3. Adherence metrics MUST be reviewed on a regular cadence.
4. If adherence falls below agreed thresholds, remediation MUST be planned.
## 14. Relationship to Stack-Specific Playbooks
## 15. Glossary and Definitions
## 16. Appendix
