# AI-Assisted Development Playbook

## 0. Purpose and Scope
- **Purpose**
  - This playbook MUST define the minimum rules for AI-assisted change delivery.
  - This playbook MUST protect safety, quality, and accountability across the repo.
  - This playbook MUST define minimum artefacts and evidence for review.
  - This playbook SHOULD enable consistent decision-making and predictable outcomes.
- **Scope boundaries**
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
- **Precedence rules**
  - Repo rules and security policies MUST take precedence over this playbook.
  - This playbook MUST take precedence over stack-specific playbooks.
  - If a stack-specific playbook is stricter, the stricter rule MUST be followed.
  - If two rules conflict and precedence is unclear, work MUST stop and a decision MUST be recorded.
  - If a rule is missing for a required action, work MUST stop and Section 13 MUST be followed.
- **How to use this document**
  - [ ] Humans MUST read Section 4 before starting any change.
  - [ ] Humans SHOULD classify change risk using Section 3.
  - [ ] AI tools MUST follow Sections 7 and 8 verbatim.
  - [ ] AI tools MUST stop and request input when scope is unclear.
  - [ ] AI tools SHOULD reference section numbers when requesting decisions.
  - [ ] If a mandatory step cannot be completed, work MUST stop and Section 13 MUST be followed.
  - [ ] Everyone MUST verify gates using Section 9 before release.
  - [ ] Everyone SHOULD record required artefacts per Section 11.
  - [ ] Re-evaluate Section 0 when scope changes or new constraints appear.
## 1. Core Principles (Non-Negotiable)
- **Principle 1: Human accountability**
  - Rule: A human owner MUST remain accountable for every change and outcome.
  - Why it exists: Ensures ownership and legal responsibility.
- **Principle 2: Safety before speed**
  - Rule: Safety and reversibility MUST take priority over delivery speed.
  - Why it exists: Reduces harm and recovery cost.
- **Principle 3: Evidence-based decisions**
  - Rule: Decisions MUST be supported by recorded evidence and rationale.
  - Why it exists: Improves traceability and auditability.
- **Principle 4: Determinism first**
  - Rule: Changes MUST be made testable and repeatable through determinism scaffolding.
  - Why it exists: Prevents flaky outcomes and hidden regressions.
- **Principle 5: Minimal change surface**
  - Rule: Changes SHOULD be the smallest coherent unit that meets the goal.
  - Why it exists: Limits blast radius and review burden.
- **Principle 6: Explicit boundaries**
  - Rule: Boundaries, constraints, and non-goals MUST be stated before execution.
  - Why it exists: Avoids scope creep and ambiguity.
- **Principle 7: Respect policy hierarchy**
  - Rule: Conflicts MUST be resolved using Section 0 precedence rules.
  - Why it exists: Prevents inconsistent application of rules.
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
