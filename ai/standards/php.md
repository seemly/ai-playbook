# AI Coding Standards (PHP)

## Index
- [0. Purpose and Scope](#0-purpose-and-scope)
- [1. Style and Naming](#1-style-and-naming)
- [2. Formatting and Linting](#2-formatting-and-linting)
- [3. Security Patterns](#3-security-patterns)

## 0. Purpose and Scope
### Purpose
- Define framework-agnostic PHP guardrails.
- Keep AI-assisted PHP changes predictable, reviewable, and secure.

### Scope
- Applies to any PHP you touch in a project.
- Follow existing project conventions before using these defaults.
- Supplements [AI Playbook](../PLAYBOOK.md), the [Coding Standards Index](INDEX.md), and any stack overlay in [`../stacks/`](../stacks/).

## 1. Style and Naming
- Follow repo-configured PHP coding standards when available.
- Match existing naming conventions before applying these defaults.
- Use `snake_case` for functions and variables unless the project standard says otherwise.
- Use `StudlyCaps` for class names and namespaces.
- Use `UPPER_SNAKE_CASE` for constants.
- Avoid one-letter identifiers except for loop indices.
- Prefer descriptive names over abbreviations.
- Keep functions focused and aligned with a single responsibility.

## 2. Formatting and Linting
- Use project-configured PHP linting and formatting tools when available.
- Run `php -l` for syntax validation when no lint tooling exists.
- Keep indentation consistent with the existing codebase.
- Avoid trailing whitespace and align array formatting with project rules.
- Do not reformat unrelated code.
- Do not disable lint rules without explicit approval.

## 3. Security Patterns
- Sanitize and validate all untrusted input before use.
- Escape output based on target context (HTML, attributes, JSON).
- Enforce authorization checks before privileged actions.
- Use CSRF protections for state-changing requests.
- Never interpolate untrusted input into SQL or HTML.
- Use prepared statements for any dynamic SQL.
