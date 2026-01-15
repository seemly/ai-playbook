# AI Development Playbook

This repository defines a **disciplined, repeatable approach to AI‑assisted software development**.

It exists to ensure that the use of AI tools:
- increases delivery speed without increasing long‑term risk,
- produces deterministic, maintainable systems rather than probabilistic ones,
- and preserves human ownership of intent, judgement, and outcomes.

This is not a tool guide.  
It is a **governance and execution framework**.

---

## Goals

The goals of this playbook are to:

- Provide a **clear, enforceable operating model** for AI‑assisted development.
- Make implicit senior‑level practices **explicit and documentable**.
- Reduce risk when working in legacy or unfamiliar systems.
- Ensure changes are **intent‑driven, test‑backed, and reversible**.
- Allow AI to be used safely as an implementation accelerator.
- Produce artefacts that scale across teams, stacks, and organisations.

If AI were removed tomorrow, the practices in this repository would still represent strong engineering discipline.

---

## Non‑Goals

This repository does **not** aim to:

- Teach programming languages or frameworks.
- Promote specific AI vendors or tools.
- Replace human decision‑making with automation.
- Define product requirements or business strategy.
- Maximise code generation volume.

Speed without control is explicitly rejected.

---

## Core Principles

The playbook is built around a small set of non‑negotiable ideas:

- **Determinism over generation**  
  Behaviour is fixed by tests and contracts, not by how code is produced.

- **Intent before implementation**  
  Every change starts with explicit goals, constraints, and non‑goals.

- **Behaviour before refactor**  
  Existing behaviour is frozen before being modified.

- **Small, reversible steps**  
  Large changes are decomposed into safe, reviewable units.

- **Human ownership of outcomes**  
  AI may generate code; humans remain accountable.

These principles are expanded and enforced in the main playbook.

---

## Repository Structure

```
.
├── README.md
├── docs
│   └── ai
│       ├── AI_PLAYBOOK.md
│       ├── README.md
│       └── (stack playbooks live here)
├── templates
│   ├── CHANGE_BRIEF_TEMPLATE.md
│   └── PULL_REQUEST_TEMPLATE.md
├── scripts
│   └── (optional helpers)
└── .github
    └── workflows
        └── (optional CI enforcement)
```

### `docs/ai/AI_PLAYBOOK.md`
The **canonical source of truth**.

Defines:
- mandatory workflow and order of execution,
- test strategy decision framework,
- AI delegation rules,
- review and release gates,
- required artefacts for any change.

This document is stack‑agnostic and changes slowly.

### Stack‑specific playbooks
Separate documents that **layer on top of the generic playbook**.

They describe how the generic rules apply to a specific stack
(e.g. frontend, backend, WordPress, Laravel, TypeScript).

They must not redefine core principles or workflow.

### `templates/`
Reusable templates that make the process concrete:
- Change briefs
- Pull request structure
- Verification and rollback checklists

These are designed to be lightweight and copied into other repos.

---

## How This Repository Is Intended to Be Used

### As a personal operating system
- Use this repo as the reference for how you plan and execute changes.
- Apply the workflow to real work.
- Evolve the playbook as you learn, using version control.

### As a team or organisation artefact
- Adopt the generic playbook as a shared standard.
- Add stack playbooks incrementally.
- Enforce key rules via CI where appropriate.
- Treat exceptions as explicit, documented decisions.

### With AI tools
- Provide relevant documents from this repo as context.
- Require AI to follow the playbook rules.
- Use AI for drafting and implementation, not decision‑making.
- Stop AI when intent is unclear.

---

## Why This Exists

Most engineering organisations rely on:
- tribal knowledge,
- implicit judgement,
- informal reviews,
- and individual heroics.

AI exposes the fragility of that model.

This playbook exists to make **good engineering boring, repeatable, and safe** —
even when powerful generative tools are involved.

---

## Status

This repository is intentionally iterative.

- Expect changes.
- Expect refinement.
- Expect sections to be opinionated.

Stability is achieved through clarity, not completeness.

---

## Licence / Reuse

This repository is intended as a **methodology**, not proprietary code.

You are free to:
- fork it,
- adapt it,
- copy sections into other projects,
- or use it as a reference when designing your own standards.

Remove or adapt anything that conflicts with your organisation’s policies.

---

## Next Steps

If you are starting fresh:
1. Read `docs/ai/AI_PLAYBOOK.md` end‑to‑end.
2. Apply the workflow to a small, real change.
3. Add a first stack‑specific playbook only when needed.
4. Keep the playbook honest by updating it when it fails you.
