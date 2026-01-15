# AI Coding Standards (JS/TS)

## Index
- [0. Purpose and Scope](#0-purpose-and-scope)
- [1. Style and Naming](#1-style-and-naming)
- [2. Build Tooling](#2-build-tooling)
- [3. React and Blocks](#3-react-and-blocks)
- [4. PHP ↔ JS Interop](#4-php--js-interop)

## 0. Purpose and Scope
### Purpose
- Define JS/TS coding standards for WordPress editor and frontend code.
- Keep AI-assisted JS changes consistent and maintainable.

### Scope
- Applies to block editor code, build scripts, and frontend JS.
- Supplements [AI Playbook](../AI_PLAYBOOK.md), the [WordPress overlay](../WORDPRESS.md), and the [Coding Standards Index](../CODING_STANDARDS.md).

## 1. Style and Naming
- Follow repo-configured ESLint and formatting rules.
- Use `camelCase` for variables and functions.
- Use `PascalCase` for React components and classes.
- Prefer named exports for shared utilities.
- Avoid mutating props or state directly.

## 2. Build Tooling
- Use project-defined npm scripts and build pipelines.
- Prefer `@wordpress/scripts` conventions when present.
- Keep build configuration in the repo standard location.
- Avoid introducing new bundlers without explicit approval.

## 3. React and Blocks
- Use `block.json` for block registration where possible.
- Keep block edit and save logic in focused, testable components.
- Use `@wordpress/data`, `@wordpress/element`, and `@wordpress/components`.
- Avoid direct DOM manipulation in editor contexts.
- Keep editor-only and frontend-only logic separated.

## 4. PHP ↔ JS Interop
- Localize data with `wp_localize_script` or `wp_add_inline_script`.
- Use REST endpoints with explicit permissions and nonces.
- Document contract shape for data passed across boundaries.
- Keep shared constants in a single source of truth.
