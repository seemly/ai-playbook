# AI Coding Standards (CSS)

## Index
- [0. Purpose and Scope](#0-purpose-and-scope)
- [1. Naming and Structure](#1-naming-and-structure)
- [2. Formatting and Linting](#2-formatting-and-linting)
- [3. Runtime Safety](#3-runtime-safety)

## 0. Purpose and Scope
### Purpose
- Define framework-agnostic CSS guardrails.
- Keep AI-assisted styling changes predictable and reviewable.

### Scope
- Applies to CSS, SCSS, and committed build outputs.
- Follow existing project conventions before using these defaults.
- Supplements [AI Playbook](../PLAYBOOK.md), the [Coding Standards Index](INDEX.md), and any stack overlay in [`../stacks/`](../stacks/).

## 1. Naming and Structure
- Follow project naming conventions for classes and utilities.
- Use one naming methodology per project (BEM, utility, etc.) and avoid mixing.
- Keep selectors shallow to avoid specificity conflicts.
- Avoid `!important` unless explicitly required.
- Group styles by component or module, not by property.

## 2. Formatting and Linting
- Use project-configured stylelint rules when available.
- Keep indentation consistent with the rest of the CSS codebase.
- Avoid inline styles except for dynamic runtime needs.
- Use CSS variables or design tokens when the project provides them.
- Do not reformat unrelated code.

## 3. Runtime Safety
- Avoid expensive selectors that target large DOM surfaces.
- Keep animations and transitions respectful of user preferences.
- Validate styles across the project’s supported breakpoints and themes.
