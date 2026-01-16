# AI Coding Standards (JS/TS)

## Index
- [0. Purpose and Scope](#0-purpose-and-scope)
- [1. Style and Naming](#1-style-and-naming)
- [2. Modules and Dependencies](#2-modules-and-dependencies)
- [3. State and Side Effects](#3-state-and-side-effects)
- [4. Data Boundaries](#4-data-boundaries)

## 0. Purpose and Scope
### Purpose
- Define framework-agnostic JS/TS guardrails.
- Keep AI-assisted JS changes predictable, reviewable, and secure.

### Scope
- Applies to browser, server, and tooling JS/TS.
- Follow existing project conventions before using these defaults.
- Supplements [AI Playbook](../PLAYBOOK.md), the [Coding Standards Index](INDEX.md), and any stack overlay in [`../stacks/`](../stacks/).

## 1. Style and Naming
- Follow repo-configured ESLint and formatting rules.
- Match existing naming conventions before applying these defaults.
- Use `camelCase` for variables and functions.
- Use `PascalCase` for classes, types, and components.
- Avoid one-letter identifiers except for loop indices.
- Prefer named exports for shared utilities.

## 2. Modules and Dependencies
- Use the existing module system (ESM/CJS) in the file you edit.
- Do not introduce new package managers, bundlers, or build tools without approval.
- Avoid adding new dependencies unless explicitly required and approved.
- Keep public exports minimal and intentional.

## 3. State and Side Effects
- Avoid hidden global state; keep state scoped to modules or functions.
- Avoid side effects in module scope; initialize in explicit entry points.
- Do not mutate shared data unless the project explicitly uses mutation.

## 4. Data Boundaries
- Validate external data at module boundaries and API edges.
- Sanitize any data that reaches HTML, the DOM, or templates.
- Document the shape of data passed between layers.
