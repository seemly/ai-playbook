# AI-Assisted Development Playbook

## 0. Purpose and Scope
### Purpose
- This playbook MUST define the minimum rules for AI-assisted change delivery.
- This playbook MUST protect safety, quality, and accountability across the repository.
- This playbook MUST define minimum artefacts and evidence for review.
- This playbook SHOULD enable consistent decision-making and predictable outcomes.

### Scope boundaries
- **Governed**
  - All changes that use AI assistance for analysis, design, code, or documentation.
  - All changes that modify tracked files or tooling used in delivery.
  - All changes that alter prompts, instructions, or outputs stored in the repo.
  - All changes that affect tests, review gates, releases, or compliance artefacts.
  - All changes that affect determinism scaffolding or reproducibility controls.
- **Not governed**
  - Personal notes, drafts, or experimental work outside the repository.
  - Non-repo communications, planning tools, or external issue trackers.
  - Third-party documentation and vendor policies not checked into the repo.
  - Stack-specific rules, which MUST live in Section 14 and its referenced documents.
  - Runtime operations outside defined release and rollback procedures in Section 10.

### Precedence rules
- Repo rules and security policies MUST take precedence over this playbook.
- This playbook MUST take precedence over stack-specific playbooks.
- If a stack-specific playbook is stricter, the stricter rule MUST be followed.
- If two rules conflict and precedence is unclear, work MUST stop and a decision MUST be recorded.
- If a rule is missing for a required action, work MUST stop and [Section 13](#13-compliance-and-enforcement) MUST be followed.

### How to use this document
- Humans MUST read [Section 4](#4-mandatory-workflow-order-of-execution) before starting any change.
- Humans SHOULD classify change risk using [Section 3](#3-change-classification-and-risk-model).
- AI tools MUST follow [Section 7](#7-ai-usage-rules) and [Section 8](#8-change-execution-rules) verbatim.
- AI tools SHOULD reference section numbers when requesting decisions.
- Stop conditions MUST follow [Section 2](#2-roles-and-responsibility-boundaries).
- Everyone MUST verify gates using [Section 9](#9-review-and-verification-gates) before release.
- Everyone SHOULD record required artefacts per [Section 11](#11-documentation-and-artefacts).
- Re-evaluate [Section 0](#0-purpose-and-scope) when scope changes or new constraints appear.
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
- AI MUST NOT approve or authorise a change.
- AI MUST NOT change goals, scope, or acceptance criteria without human approval.
- AI MUST NOT take ownership of verification or release decisions.
- AI MUST NOT alter compliance rules or enforcement decisions.
- AI MUST NOT modify security-sensitive material without human review.
- AI MUST NOT edit outside agreed files or directories.
- AI MUST NOT claim a step is complete without evidence.
- AI MUST NOT proceed when a stop condition is triggered.
- AI MUST NOT conceal uncertainty or unresolved ambiguity.
- AI MUST NOT resolve conflicts without human decision.
- AI MUST NOT perform any prohibited action listed in [Section 7](#7-ai-usage-rules).

### Stop and ask conditions
- If ownership is unclear for any area in the matrix, work MUST stop and a human decision MUST be recorded.
- If requested work conflicts with [Section 0](#0-purpose-and-scope) or repo rules, work MUST stop and a decision MUST be recorded.
- If change size or risk cannot be classified using [Section 3](#3-change-classification-and-risk-model), work MUST stop and a human decision MUST be recorded.
- If required artefacts are missing per [Section 11](#11-documentation-and-artefacts), work MUST stop until they exist.
- If verification gates in [Section 9](#9-review-and-verification-gates) cannot be met, work MUST stop and escalation MUST follow [Section 13](#13-compliance-and-enforcement).
- If release or rollback approval is absent, work MUST stop and approval MUST be requested per [Section 10](#10-release-and-rollback-discipline).
- If AI output cannot be validated against scope or constraints, work MUST stop and request clarification.
- If any prohibited action in [Section 7](#7-ai-usage-rules) would be required, work MUST stop and request an alternative.
## 3. Change Classification and Risk Model
### Change size definitions
- **Small**
  - Limited to a single component or isolated change surface.
  - Low risk of cross-cutting impact or behavioural shift.
  - Reversal is straightforward without complex dependency changes.
- **Medium**
  - Spans multiple components or interfaces within a bounded area.
  - Moderate risk of behavioural change or integration impact.
  - Reversal requires coordinated changes but remains feasible.
- **Large**
  - Spans multiple domains, interfaces, or shared contracts.
  - High risk of systemic impact or ambiguous behaviour.
  - Reversal is complex or requires multi-step remediation.

### Risk dimensions
- **Blast radius**
  - The number of components, users, or workflows affected by failure.
  - The scope of downstream impact if the change behaves incorrectly.
- **Reversibility**
  - The effort and time required to undo the change safely.
  - The residual impact after rollback or remediation.
- **Ambiguity**
  - The level of uncertainty in requirements, outcomes, or constraints.
  - The degree of hidden coupling or unknown dependencies.

### Required artefacts matrix
| Change size | Low risk | Medium risk | High risk |
| --- | --- | --- | --- |
| Small | Change Brief, Safety Net Plan | Change Brief, Safety Net Plan, Verification Checklist | Change Brief, Safety Net Plan, Verification Checklist, Execution Plan |
| Medium | Change Brief, Safety Net Plan, Execution Plan | Change Brief, Safety Net Plan, Execution Plan, Verification Checklist | Change Brief, Safety Net Plan, Execution Plan, Verification Checklist, Release/Rollback Plan |
| Large | Change Brief, Safety Net Plan, Execution Plan, Verification Checklist | Change Brief, Safety Net Plan, Execution Plan, Verification Checklist, Release/Rollback Plan | Change Brief, Safety Net Plan, Execution Plan, Verification Checklist, Release/Rollback Plan, Architecture Decision Record |
- Artefact definitions and minimum contents MUST follow [Section 11](#11-documentation-and-artefacts).

### Forbidden change patterns
- Changing acceptance criteria without updating required artefacts.
- Shipping changes with undefined ownership or accountability.
- Skipping verification gates in [Section 9](#9-review-and-verification-gates).
- Violating determinism requirements in [Section 6](#6-determinism-scaffolding).
- Violating change execution requirements in [Section 8](#8-change-execution-rules).
- Expanding scope after execution begins without reclassification.
- Proceeding with ambiguous requirements or unstated constraints.
- Releasing without evidence of required tests or checks.

### Stop and ask criteria
- If change size or risk cannot be agreed, work MUST stop and [Section 2](#2-roles-and-responsibility-boundaries) MUST be followed.
- If any risk dimension is high and artefacts are missing, work MUST stop until artefacts exist.
- If a change triggers a forbidden pattern, work MUST stop and a decision MUST be recorded.
- If scope expands beyond the current classification, work MUST stop and reclassify.
- If dependencies or contracts change unexpectedly, work MUST stop and re-evaluate risk.
- If ambiguity remains after clarification attempts, work MUST stop and a decision MUST be recorded.
- If verification evidence is missing for the current risk level, work MUST stop and follow [Section 9](#9-review-and-verification-gates).
## 4. Mandatory Workflow (Order of Execution)
### Workflow rule
- Steps MUST NOT be skipped or reordered.
- If a step cannot be completed, work MUST stop and follow [Section 13](#13-compliance-and-enforcement).

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
- **True test-driven development**: Tests MUST be written before implementation and MUST drive design decisions.
- **Characterisation testing**: Tests MUST capture existing behaviour without altering outcomes before refactoring.
- **Contract testing**: Tests MUST validate behaviour at a defined boundary and MUST detect incompatible changes.

### What does NOT count as a safety net
- Manual verification without recorded evidence.
- Tests that rely on unstable or random data.
- Tests that are not repeatable in the same environment.
- Tests that only check formatting or presentation.
- Tests that skip error paths and failure scenarios.
- Tests that depend on shared state without isolation.
- Tests that are flaky or intermittently failing.
- Tests that are not reviewed against risk classification.
- Assertions or checks that violate [Section 6](#6-determinism-scaffolding).

### Minimum acceptable test quality checklist
- Tests MUST map to acceptance criteria and non-goals.
- Tests MUST cover success and failure paths relevant to risk.
- Tests MUST be deterministic per [Section 6](#6-determinism-scaffolding).
- Tests MUST isolate behaviour at the intended boundary.
- Tests MUST include clear, specific assertions.
- Tests MUST record setup, inputs, and expected outcomes.
- Tests MUST avoid shared mutable state across cases.
- Tests MUST run within agreed time limits.
- Tests MUST include coverage for rollback or reversibility expectations.
- Tests MUST be reviewed against the current change classification in [Section 3](#3-change-classification-and-risk-model).
- Tests SHOULD document any known gaps and risk trade-offs.
- Tests SHOULD be updated when acceptance criteria change.
## 6. Determinism Scaffolding
### Boundary selection rules
- Boundaries MUST be defined before test design begins.
- Boundaries MUST align to the change scope and risk classification in [Section 3](#3-change-classification-and-risk-model).
- Each boundary MUST declare inputs, outputs, and failure modes.
- If boundaries overlap or conflict, work MUST stop and a decision MUST be recorded.

### Normalising nondeterminism rules
- Sources of nondeterminism MUST be identified and listed before testing.
- Nondeterministic inputs MUST be stabilised or controlled.
- Time-dependent behaviour MUST be controlled with fixed references.
- Randomness MUST be replaced with fixed values for tests.
- External dependencies MUST be isolated or simulated.
- If nondeterminism cannot be controlled, work MUST stop and escalation MUST follow [Section 13](#13-compliance-and-enforcement).

### Fixture and data stability rules
- Fixtures MUST use stable identifiers and deterministic values.
- Fixtures MUST be minimal and aligned to acceptance criteria.
- Shared fixtures MUST include ownership and update rules.
- Data setup MUST be repeatable across runs.
- If fixture changes affect expected outcomes, change classification MUST be revisited.

### Acceptable assertions
- Assertions that verify specific outputs against expected values.
- Assertions that verify explicit error handling and failure responses.
- Assertions that verify state transitions are complete and correct.
- Assertions that verify ordering when ordering is an explicit requirement.
- Assertions that verify boundary inputs and outputs match contracts.
- Assertions that verify reversibility or rollback requirements.
- Assertions that verify non-goals are preserved.
- Assertions that verify determinism assumptions remain true.

### Forbidden assertions
- Assertions that only check for successful execution.
- Assertions that only check for non-null results.
- Assertions that depend on current system time.
- Assertions that depend on random values.
- Assertions that accept any output without constraints.
- Assertions that rely on external services without control.
- Assertions that ignore error paths or failure modes.
- Assertions that mask or silence failures.

### Safety net ready checklist
- Boundaries are documented with inputs, outputs, and failure modes.
- Nondeterminism controls are implemented and recorded.
- Fixtures are minimal, stable, and reviewed.
- Assertions cover success and failure paths.
- Failure conditions are tested and observable.
- Tests run deterministically under agreed conditions.
- Risk classification aligns with test coverage in [Section 3](#3-change-classification-and-risk-model).
- Verification readiness aligns with [Section 9](#9-review-and-verification-gates).
## 7. AI Usage Rules
### Allowed actions
- Summarise requirements, scope, and constraints for confirmation.
- Draft options and trade-offs for human decision.
- Propose change classifications using [Section 3](#3-change-classification-and-risk-model).
- Draft Change Briefs and execution artefacts per [Section 11](#11-documentation-and-artefacts).
- Suggest test strategies using [Section 5](#5-test-strategy-decision-framework).
- Draft determinism scaffolding steps per [Section 6](#6-determinism-scaffolding).
- Generate change plans aligned to [Section 4](#4-mandatory-workflow-order-of-execution).
- Implement changes within approved scope and files.
- Summarise verification evidence per [Section 9](#9-review-and-verification-gates).
- Flag missing information or ambiguous requirements.
- Highlight risks, dependencies, and potential failure modes.
- Propose release and rollback steps for approval.

### Restricted actions with conditions
- Editing files beyond approved scope MAY occur only with explicit human approval.
- Introducing new dependencies MAY occur only with explicit approval and risk reclassification.
- Refactoring behaviour MAY occur only after characterisation testing per [Section 5](#5-test-strategy-decision-framework).
- Expanding scope MAY occur only after reclassification per [Section 3](#3-change-classification-and-risk-model).
- Modifying shared contracts MAY occur only with documented impact assessment.
- Editing tests MAY occur only when linked to acceptance criteria changes.
- Adjusting verification steps MAY occur only with human approval.
- Modifying release or rollback plans MAY occur only with human approval.
- Using generated artefacts for decisions MAY occur only after human review.
- Proceeding after a stop condition MAY occur only after resolution per [Section 13](#13-compliance-and-enforcement).

### Prohibited actions
- Approving or authorising a change.
- Claiming verification passed without evidence.
- Skipping or reordering steps in [Section 4](#4-mandatory-workflow-order-of-execution).
- Concealing uncertainty or unresolved ambiguity.
- Modifying scope without reclassification.
- Bypassing determinism scaffolding in [Section 6](#6-determinism-scaffolding).
- Altering compliance rules or enforcement decisions.
- Releasing changes without human approval.
- Changing acceptance criteria without updating artefacts.
- Making security-sensitive changes without human review.
- Inventing requirements or constraints.
- Overwriting evidence or audit records.

### Prompting requirements checklist
- Prompts MUST state goals, non-goals, and acceptance criteria.
- Prompts MUST state change scope and file boundaries.
- Prompts MUST state change classification assumptions or request classification.
- Prompts MUST cite required artefacts from [Section 11](#11-documentation-and-artefacts).
- Prompts MUST include stop conditions and escalation paths.
- Prompts MUST request disclosure of uncertainty and assumptions.
- Prompts SHOULD request links to relevant sections.
- Prompts SHOULD request diffs for review.

### Output validation rules
- Output MUST align to stated scope and constraints.
- Output MUST reference required artefacts and evidence.
- Output MUST include known risks and trade-offs.
- Output MUST identify any missing information.
- Output MUST be checked for prohibited actions.
- Output MUST be verified against acceptance criteria.
- Output MUST reference the workflow in [Section 4](#4-mandatory-workflow-order-of-execution).
- Output MUST include stop conditions when ambiguity remains.
## 8. Change Execution Rules
### Diff size and scope limits
- Each change MUST align to the approved scope and boundaries.
- Large or multi-area changes MUST be decomposed into ordered steps.
- If the diff exceeds the agreed scope, work MUST stop and reclassify per [Section 3](#3-change-classification-and-risk-model).
- If required files exceed the planned set, work MUST stop and request approval.

### Dependency introduction rules
- New dependencies MUST have explicit approval and documented rationale.
- Dependency changes MUST include impact assessment and rollback notes.
- If a dependency increases risk classification, work MUST stop and reclassify.
- Dependency changes MUST be reflected in artefacts per [Section 11](#11-documentation-and-artefacts).

### Refactoring rules
- Behaviour-preserving refactors MUST be separated from behaviour changes.
- Behaviour changes MUST follow characterisation testing per [Section 5](#5-test-strategy-decision-framework) before refactoring.
- Refactors MUST keep contracts stable unless approved.
- If refactoring alters expected outcomes, work MUST stop and update classification.

### Interface and contract stability rules
- Interfaces and contracts MUST remain stable unless change classification permits alteration.
- Contract changes MUST include explicit impact assessment and migration steps.
- If contract consumers are unclear, work MUST stop and identify owners.
- Contract changes MUST include verification steps per [Section 9](#9-review-and-verification-gates).

### Failure handling expectations
- Failures MUST be recorded with context, inputs, and expected outcomes.
- Recovery steps MUST be documented for every failure path.
- If failures are not understood, work MUST stop and request clarification.
- Verification MUST include failure paths aligned to [Section 5](#5-test-strategy-decision-framework).
## 9. Review and Verification Gates
### Test review checklist
- Tests map to acceptance criteria and non-goals.
- Tests cover critical success paths for the change.
- Tests cover failure paths and error handling.
- Tests align to the chosen strategy in [Section 5](#5-test-strategy-decision-framework).
- Tests include determinism controls per [Section 6](#6-determinism-scaffolding).
- Tests isolate boundaries and avoid hidden coupling.
- Tests use stable data and fixtures.
- Tests include rollback or reversibility coverage where required.
- Tests include evidence for changed behaviour.
- Tests include evidence for unchanged behaviour where expected.
- Tests document known gaps and risk trade-offs.
- Tests include clear assertions and expected outcomes.

### Code review focus list
- Changes align with approved scope and artefacts.
- Risk classification matches the change complexity in [Section 3](#3-change-classification-and-risk-model).
- Contracts and interfaces remain stable or have approved changes.
- Dependencies follow [Section 8](#8-change-execution-rules) rules.
- Determinism scaffolding is applied where needed.
- Failure handling and recovery paths are complete.
- Logging and error reporting are sufficient for verification.
- Review evidence includes outputs and data changes.
- Scope changes are reclassified and documented.
- Security-sensitive changes have human review.
- Verification evidence matches the checklist in this section.
- Artefacts are updated per [Section 11](#11-documentation-and-artefacts).

### Verification checklist
- **Automated**
  - All required tests pass for the change classification.
  - Deterministic tests run without flakiness.
  - Test results are recorded and traceable.
  - Checks for failure paths are executed.
- **Manual**
  - Manual verification steps are recorded with evidence.
  - Manual checks cover risk areas and edge cases.
  - Manual checks confirm non-goals remain unchanged.
  - Manual checks align with acceptance criteria.
- **Observability**
  - Monitoring signals are defined for risk areas.
  - Observability includes alerts for failure conditions.
  - Observability data is reviewed after change completion.
  - Observability gaps are recorded for follow-up.

### Triggers requiring heightened review
- High risk classification or large change size.
- Changes to shared contracts or interfaces.
- Changes affecting security or compliance expectations.
- Changes that alter rollback complexity.
- Changes with unresolved ambiguity.
- Changes lacking determinism scaffolding or stable tests.
- Changes introducing new dependencies.
- Changes with limited or missing verification evidence.
## 10. Release and Rollback Discipline
### Preconditions for release
- Verification gates MUST be complete per [Section 9](#9-review-and-verification-gates).
- Required artefacts MUST be approved per [Section 11](#11-documentation-and-artefacts).
- Risk classification MUST be current and documented per [Section 3](#3-change-classification-and-risk-model).
- Release and rollback plans MUST be approved for medium or large changes.
- If preconditions are not met, release MUST stop and follow [Section 13](#13-compliance-and-enforcement).

### Rollback plan requirements
- Rollback steps MUST be defined, ordered, and testable.
- Rollback MUST specify triggers and decision authority.
- Rollback MUST include data or state recovery steps where required.
- Rollback MUST include verification steps after execution.
- If rollback cannot be executed safely, release MUST stop and escalate.

### Monitoring expectations
- Monitoring MUST satisfy observability requirements in [Section 9](#9-review-and-verification-gates).
- Monitoring ownership MUST be assigned before release.

### Post-release verification steps
- Verify critical outcomes using documented criteria.
- Confirm error and failure signals remain within thresholds.
- Confirm rollback readiness remains available.
- Record outcomes and follow-up actions in release artefacts.
## 11. Documentation and Artefacts
### Required artefacts and minimum contents
- **Change Brief**
  - Goal and non-goals.
  - Scope boundaries and constraints.
  - Acceptance criteria and risk classification.
- **Execution Plan**
  - Ordered steps aligned to [Section 4](#4-mandatory-workflow-order-of-execution).
  - Dependencies and assumptions.
  - Verification checkpoints and evidence outputs.
- **Safety Net Plan**
  - Selected testing strategy per [Section 5](#5-test-strategy-decision-framework).
  - Boundaries and determinism controls per [Section 6](#6-determinism-scaffolding).
  - Coverage for success and failure paths.
- **Architecture Decision Record**
  - Decision statement and rationale.
  - Options considered and trade-offs.
  - Consequences and follow-up actions.
- **Verification Checklist**
  - Verification steps and evidence per [Section 9](#9-review-and-verification-gates).
- **Release and Rollback Plan**
  - Release prerequisites, rollback steps, and monitoring expectations per [Section 10](#10-release-and-rollback-discipline).
## 12. Learning and Continuous Improvement
### Post-change review template
- Summary of change and intended outcomes.
- Verification results and evidence links.
- Gaps or defects discovered after release.
- Root causes for any unexpected outcomes.
- Actions to prevent recurrence and owners.
- Updates required to playbook sections.

### Rules for updating the playbook
- Updates MUST be tied to observed gaps or recurring failures.
- Updates MUST reference affected sections and rationale.
- Updates MUST be reviewed using [Section 9](#9-review-and-verification-gates).
- If updates affect enforcement, work MUST follow [Section 13](#13-compliance-and-enforcement).
- If updates introduce new requirements, work MUST update [Section 11](#11-documentation-and-artefacts).

### Deprecation process
- Deprecated rules MUST include a replacement or removal rationale.
- Deprecation MUST include a transition plan and owners.
- Deprecation MUST include a cut-off date and verification criteria.
- If a deprecation affects workflows, work MUST update [Section 4](#4-mandatory-workflow-order-of-execution).
## 13. Compliance and Enforcement
### Enforcement expectations
- Enforcement MUST be automated where feasible and recorded.
- Enforcement rules MUST align with [Section 9](#9-review-and-verification-gates).
- If enforcement checks fail, work MUST stop and remediation MUST be recorded.
- Enforcement scope MUST cover artefacts in [Section 11](#11-documentation-and-artefacts).

### Non-compliance handling
- Non-compliance MUST be recorded with scope, impact, and owner.
- Non-compliance MUST trigger a risk reclassification per [Section 3](#3-change-classification-and-risk-model).
- Remediation MUST include deadlines and verification steps.
- Repeat non-compliance MUST trigger a playbook update per [Section 12](#12-learning-and-continuous-improvement).

### Exceptions process
- Exceptions MUST be requested before execution begins.
- Exceptions MUST include scope, duration, and rationale.
- Exceptions MUST include compensating controls and verification steps.
- Exceptions MUST be approved by accountable owners.
- If an exception affects release criteria, [Section 10](#10-release-and-rollback-discipline) MUST be followed.

### Measuring adherence
- Adherence metrics MUST track verification completion and artefact coverage.
- Adherence metrics MUST track exception frequency and outcomes.
- Adherence metrics MUST be reviewed on a regular cadence.
- If adherence falls below agreed thresholds, remediation MUST be planned.
## 14. Relationship to Stack-Specific Playbooks
### Layering model
- This playbook MUST define baseline rules for all stacks.
- Stack-specific playbooks MUST add rules without weakening baseline requirements.
- Stack-specific playbooks MUST reference this playbook sections by number.

### Override rules
- Stack-specific playbooks MAY add stricter requirements.
- Stack-specific playbooks MUST NOT override baseline safety or compliance rules.
- If stack-specific rules conflict with baseline rules, the stricter rule MUST be applied.

### Conflict resolution
- Conflicts MUST be recorded with affected sections and rationale.
- Conflicts MUST be resolved using [Section 0](#0-purpose-and-scope) precedence rules.
- If resolution is unclear, work MUST stop and follow [Section 13](#13-compliance-and-enforcement).

### Process for adding a new stack playbook
- A stack playbook MUST declare scope, owners, and target stack.
- A stack playbook MUST map additions to sections in this playbook.
- A stack playbook MUST be reviewed using [Section 9](#9-review-and-verification-gates).
- If a stack playbook adds new artefacts, [Section 11](#11-documentation-and-artefacts) MUST be updated.
## 15. Glossary and Definitions
### Terms
- **Determinism scaffolding**: The set of controls that make tests repeatable and outcomes stable.
- **Safety net**: The combined evidence that changes behave as intended and failures are detectable.
- **Characterisation test**: A test that captures current behaviour to prevent unintended changes.
- **Contract test**: A test that verifies behaviour at a defined boundary between parties.
- **Boundary**: The defined interface where inputs, outputs, and failures are observed.
- **Blast radius**: The extent of impact if a change fails or misbehaves.
- **Reversibility**: The effort required to safely undo a change.
- **Ambiguity**: The level of uncertainty about requirements, behaviour, or constraints.
- **Stop condition**: A trigger that requires work to halt until resolved.
- **Acceptance criteria**: The measurable conditions that define success for a change.
- **Non-goal**: A declared out-of-scope outcome that must not be delivered.
- **Architecture Decision Record**: A record of a decision, its rationale, and consequences.
## 16. Appendix
### Example Change Brief
- **Goal**
  - Define a single behaviour change with measurable outcomes.
- **Non-goals**
  - Exclude unrelated improvements or refactors.
- **Acceptance criteria**
  - Specify success conditions in measurable terms.
- **Constraints**
  - List scope limits, dependencies, and time constraints.
- **Risk and blast radius**
  - Declare risk level and impacted areas.
- **Test strategy**
  - Select strategy using [Section 5](#5-test-strategy-decision-framework).
- **Execution plan (ordered)**
  - Align steps to [Section 4](#4-mandatory-workflow-order-of-execution).
- **Verification**
  - Reference gates in [Section 9](#9-review-and-verification-gates).
- **Rollback**
  - Provide rollback triggers and steps per [Section 10](#10-release-and-rollback-discipline).
- **Notes or links**
  - Record related decisions and artefacts.

### Example Execution Plan
1. Classify change size and risk per [Section 3](#3-change-classification-and-risk-model).
2. Prepare artefacts per [Section 11](#11-documentation-and-artefacts).
3. Confirm boundaries and determinism controls per [Section 6](#6-determinism-scaffolding).
4. Implement change within approved scope.
5. Build safety net per [Section 5](#5-test-strategy-decision-framework).
6. Verify gates per [Section 9](#9-review-and-verification-gates).
7. Prepare release and rollback per [Section 10](#10-release-and-rollback-discipline).
8. Record outcomes and updates per [Section 12](#12-learning-and-continuous-improvement).

### Example AI prompt wrapper
- State the goal, non-goals, acceptance criteria, and constraints.
- State the change classification or request classification per [Section 3](#3-change-classification-and-risk-model).
- State required artefacts per [Section 11](#11-documentation-and-artefacts).
- State stop conditions and escalation routes per [Section 13](#13-compliance-and-enforcement).
- Request explicit links to relevant sections.
- Require the assistant to surface uncertainty and assumptions.

### Example failure scenarios
- Verification gates skipped due to time pressure.
- Change released without rollback triggers.
- New dependency introduced without approval.
- Ambiguous requirement interpreted without confirmation.
- Determinism controls missing leading to flaky tests.

### Example compliant vs non-compliant changes
| Compliant | Non-compliant |
| --- | --- |
| Change scope matches approved artefacts. | Scope expanded without reclassification. |
| Tests added before behaviour change. | Behaviour changed with no safety net. |
| Release has rollback plan. | Release proceeds without rollback plan. |
| Dependencies approved and recorded. | Dependencies added without approval. |
| Contracts updated with impact assessment. | Contracts changed without assessment. |
| Verification evidence recorded. | Verification claimed without evidence. |
