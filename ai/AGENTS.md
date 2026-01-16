# AGENTS.md

## Purpose
- This repository is a playbook and standards reference.
- Use this file to orient agentic tools working in the repo.
- Follow the canonical documents listed below for detailed rules.

## Source Documents (Authoritative)
- `PLAYBOOK.md` (baseline workflow + AI rules)
- `stacks/wordpress/PLAYBOOK.md` (WordPress overlay)
- `standards/INDEX.md` (language standards index)
- `standards/php.md` (PHP standards)
- `standards/js.md` (JS/TS standards)
- `standards/css.md` (CSS standards)
- `standards/wordpress.md` (WordPress standards)

## Cursor/Copilot Rules
- No `.cursor/rules`, `.cursorrules`, or `.github/copilot-instructions.md` found.

## Build, Lint, Test Commands
- No build system or test harness is defined in this repo.
- No `package.json`, `composer.json`, `Makefile`, or CI config exists here.
- Do not assume any command names or test runners.
- If you need to add automation to this repo, document it here and in the playbook.
- For single-test execution, follow the tooling conventions of the target project.
- Common single-test patterns (use only if the target repo supports them):
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

## General Style Rules
- Keep changes minimal and scoped to intent.
- Match the existing formatting in each document.
- Prefer clarity over cleverness; avoid abbreviations.
- Use descriptive names for files, headings, and identifiers.
- Avoid introducing new tooling without explicit approval.
- Do not add inline comments unless explicitly requested.
- Avoid one-letter identifiers except in tight loops.

## Imports and Dependencies
- Group imports by standard library, third-party, and local modules.
- Keep import lists alphabetized within each group when a project does so.
- Remove unused imports and avoid circular dependencies.
- Prefer explicit imports over wildcard imports.
- Do not introduce new dependencies without approval.
## Documentation Style
- Use clear, declarative headings and short paragraphs.
- Keep lists concise and ordered by importance.
- Use consistent terminology across documents.
- Avoid duplicating rules across documents; link instead.

## PHP Standards
- Follow repo-configured PHP standards when present.
- Use `snake_case` for functions and variables unless a project dictates otherwise.
- Use `StudlyCaps` for classes and namespaces.
- Use `UPPER_SNAKE_CASE` for constants.
- Prefer descriptive names and single-responsibility functions.

### PHP Formatting & Linting
- Use project-configured linters/formatters when available.
- If no tooling exists, validate syntax with `php -l`.
- Keep indentation consistent with existing files.
- Avoid trailing whitespace and keep arrays consistent.

### PHP Security & Error Handling
- Sanitize and validate all untrusted input.
- Escape output by context (HTML, attributes, URLs, JSON).
- Enforce capability checks before privileged actions.
- Use nonces for state-changing requests.
- Avoid dynamic SQL; use prepared statements.
- Return `WP_Error` or structured responses for failures.
- Do not swallow exceptions or errors; surface them consistently.
## JS/TS Standards
- Follow repo-configured ESLint/Prettier rules.
- Use `camelCase` for variables and functions.
- Use `PascalCase` for React components and classes.
- Prefer named exports for shared utilities.
- Avoid mutating props or state directly.

### JS/TS Tooling & Architecture
- Use project-defined npm scripts and build pipelines.
- Prefer `@wordpress/scripts` conventions when present.
- Avoid introducing new bundlers without approval.

### Types and Data
- Use TypeScript types at module boundaries and public APIs.
- Avoid `any`; prefer unions or `unknown` with narrowing.
- Keep types close to where they are used; avoid giant global types.
- Model external data explicitly (REST responses, localized data).

### React and Blocks
- Use `block.json` for block registration where possible.
- Keep edit/save logic in focused, testable components.
- Prefer `@wordpress/data`, `@wordpress/element`, `@wordpress/components`.
- Avoid direct DOM manipulation in editor contexts.
- Keep editor-only and frontend-only logic separated.

### PHP ↔ JS Interop
- Localize data with `wp_localize_script` or `wp_add_inline_script`.
- Use REST endpoints with explicit permissions and nonces.
- Document data contracts and keep constants centralized.

## CSS Standards
- Follow project naming conventions for classes/utilities.
- Align custom block styles with `wp-block-*` naming.
- Prefer BEM-style naming for custom components where appropriate.
- Keep selectors shallow to avoid specificity conflicts.
- Group styles by component or block, not by property.

### CSS Formatting
- Use project-configured stylelint rules when available.
- Keep indentation consistent with existing CSS.
- Avoid inline styles unless required for runtime behavior.
- Use CSS variables for shared values when supported.
- Keep ordering consistent (e.g., layout → spacing → typography).
### Editor vs Frontend
- Separate editor-only styles from frontend styles.
- Ensure editor styles do not leak into frontend bundles.
- Test block styles in both editor and frontend contexts.
- Use `theme.json` for shared design tokens when available.

## WordPress Standards
- Prefer core APIs over custom implementations.
- Use Settings API for admin configuration.
- Use Options, Post Meta, Term Meta, and Transients APIs for storage.
- Use `register_post_type` and `register_taxonomy` helpers.
- Use `wp_enqueue_script` and `wp_enqueue_style` for assets.

### Hooks and Lifecycle
- Register hooks on correct lifecycle actions (`init`, `admin_init`, `wp_enqueue_scripts`).
- Keep hook callbacks focused and testable.
- Document hook priorities when order matters.
- Avoid global side effects on load.

### Assets and Builds
- Separate editor assets from frontend assets.
- Use versioned asset handles and cache busting.
- Keep build artifacts in repo-approved locations.
- Avoid introducing new tooling without approval.

### REST API & Error Handling
- Require `permission_callback` for all REST routes.
- Enforce authentication and authorization in handlers.
- Return `WP_Error` with clear error codes on failures.
- Validate and sanitize request arguments with schemas.
- Use consistent error codes and messages across endpoints.
- Avoid leaking sensitive data in error responses.
### Security & Data Handling
- Sanitize input with WordPress helpers (e.g., `sanitize_text_field`).
- Escape output with context-specific helpers (e.g., `esc_html`, `esc_attr`).
- Require nonces for state changes (`wp_nonce_field`, `check_admin_referer`).
- Enforce capability checks (`current_user_can`).
- Validate file uploads (`wp_check_filetype_and_ext`).

### Admin UI
- Scope admin assets to the screens that need them.
- Align admin UX with WordPress UI patterns.
- Keep settings pages consistent with core conventions.

### Interop & Compatibility
- Avoid conflicts via namespacing and scoped behavior.
- Load integrations only when required for relevant contexts.
- Define a compatibility matrix for WordPress and PHP versions.
- Record manual compatibility checks when automated tests are unavailable.

## Stop Conditions
- If a rule is missing or unclear, stop and request guidance.
- If a change alters scope or risk, reclassify before proceeding.
- If verification evidence is missing, do not proceed.
- If a change touches security-sensitive logic, request review.