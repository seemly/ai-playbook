# AGENTS.md

## Purpose
- This repository is a playbook and standards reference.
- Use this file to orient agentic tools working in the repo.
- The canonical guidance lives in `ai/` documents listed below.

## Source Documents (Authoritative)
- `ai/PLAYBOOK.md` (baseline workflow + AI rules)
- `ai/stacks/wordpress/PLAYBOOK.md` (WordPress overlay)
- `ai/standards/INDEX.md` (language standards index)
- `ai/standards/php.md` (PHP guardrails)
- `ai/standards/js.md` (JS/TS guardrails)
- `ai/standards/css.md` (CSS guardrails)
- `ai/standards/wordpress.md` (WordPress guardrails)

## Repository Structure
- `ai/` contains the core playbook and standards.
- `templates/git/` contains reusable templates.
- `planning/` holds forward-looking notes and proposals.

## Cursor/Copilot Rules
- No `.cursor/rules`, `.cursorrules`, or `.github/copilot-instructions.md` found.

## Build, Lint, Test Commands
- No build system or test harness is defined in this repo.
- No `package.json`, `composer.json`, `Makefile`, or CI config exists here.
- Do not assume any command names or test runners.
- If you need to add automation to this repo, document it here and in the playbook.
- For single-test execution, follow the tooling conventions of the target project:
  - PHPUnit: `vendor/bin/phpunit --filter "TestName"`
  - Jest: `npm test -- --testNamePattern "name"`
  - Vitest: `npx vitest -t "name"`
  - Playwright: `npx playwright test path/to/spec`

## Workflow Expectations (from AI Playbook)
- Follow the mandatory workflow order; do not skip steps.
- Classify change size and risk before editing.
- Stop when rules are missing or conflicting and request guidance.
- Keep changes small, reversible, and evidence-backed.
- Provide verification evidence for any change.

## Documentation Style
- Use clear, declarative headings and short paragraphs.
- Keep lists concise and ordered by importance.
- Use consistent terminology across documents.
- Avoid duplicating rules across documents; link instead.
- Match the existing formatting in each document.

## General Coding Guardrails
- Follow the most specific standard for the file you edit.
- Prefer small, reversible changes over broad refactors.
- Do not add inline comments unless explicitly requested.
- Avoid introducing new tooling or dependencies without approval.
- Avoid one-letter identifiers except for loop indices.

## Imports and Dependencies
- Group imports by standard library, third-party, and local modules.
- Keep import lists alphabetized within each group when the project does so.
- Remove unused imports and avoid circular dependencies.
- Prefer explicit imports over wildcard imports.
- Do not introduce new dependencies without approval.

## Formatting and Linting
- Use project-configured formatters and linters when available.
- Do not reformat unrelated code.
- Do not disable lint rules without explicit approval.
- Keep whitespace, indentation, and ordering consistent with the file.

## Types and Data Boundaries
- Validate external data at module boundaries and API edges.
- Document the shape of data passed between layers.
- Avoid implicit type coercion when it affects correctness.

## Error Handling
- Surface errors explicitly; avoid swallowing exceptions.
- Return structured errors and consistent error codes.
- Do not log or expose sensitive data.

## PHP Guardrails (Summary)
- Match project-specific conventions before applying defaults.
- Use `snake_case` for functions/variables when no project rule exists.
- Use `StudlyCaps` for classes and namespaces.
- Use `UPPER_SNAKE_CASE` for constants.
- Sanitize input, escape output, and enforce authorization checks.
- Use prepared statements for any dynamic SQL.

## JS/TS Guardrails (Summary)
- Match project naming conventions before applying defaults.
- Use `camelCase` for variables/functions and `PascalCase` for classes/components.
- Avoid hidden global state; keep side effects explicit.
- Do not introduce new package managers or bundlers without approval.
- Validate data at boundaries before using it in DOM/templates.

## CSS Guardrails (Summary)
- Use one naming methodology per project and avoid mixing.
- Keep selectors shallow and avoid `!important` unless required.
- Avoid inline styles except for runtime needs.
- Use CSS variables or design tokens when available.
- Validate styles across supported breakpoints and themes.

## WordPress Guardrails (Summary)
- Prefer core APIs over custom implementations.
- Enforce nonces and capability checks for privileged actions.
- Require `permission_callback` for all REST routes.
- Scope admin assets to the screens that need them.
- Separate editor assets from frontend assets.

## Stop Conditions
- If a rule is missing or unclear, stop and request guidance.
- If a change alters scope or risk, reclassify before proceeding.
- If verification evidence is missing, do not proceed.
- If a change touches security-sensitive logic, request review.
