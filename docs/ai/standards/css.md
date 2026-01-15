# AI Coding Standards (CSS)

## Index
- [0. Purpose and Scope](#0-purpose-and-scope)
- [1. Naming and Structure](#1-naming-and-structure)
- [2. Formatting and Linting](#2-formatting-and-linting)
- [3. Editor vs Frontend](#3-editor-vs-frontend)

## 0. Purpose and Scope
### Purpose
- Define CSS standards for WordPress themes, blocks, and editor styles.
- Keep AI-assisted styling changes predictable and reviewable.

### Scope
- Applies to CSS, SCSS, and build outputs committed to the repo.
- Supplements [AI Playbook](../AI_PLAYBOOK.md), the [WordPress overlay](../stacks/wordpress/PLAYBOOK.md), and the [Coding Standards Index](INDEX.md).

## 1. Naming and Structure
- Follow project naming conventions for classes and utilities.
- Align custom block styles with `wp-block-*` naming.
- Prefer BEM-style naming for custom components where appropriate.
- Keep selectors shallow to avoid specificity conflicts.
- Group styles by component or block, not by property.

## 2. Formatting and Linting
- Use project-configured stylelint rules when available.
- Keep indentation consistent with the rest of the CSS codebase.
- Avoid inline styles except for dynamic runtime needs.
- Use CSS variables for shared values when the project supports them.

## 3. Editor vs Frontend
- Separate editor-only styles from frontend styles.
- Ensure editor styles do not leak into frontend bundles.
- Test block styles in both editor and frontend contexts.
- Use `theme.json` settings when available for shared design tokens.
