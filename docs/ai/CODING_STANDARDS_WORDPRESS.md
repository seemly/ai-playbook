# AI Coding Standards (WordPress)

## Index
- [0. Purpose and Scope](#0-purpose-and-scope)
- [1. Data Handling and Security](#1-data-handling-and-security)
- [2. WordPress APIs](#2-wordpress-apis)
- [3. Hooks and Lifecycle](#3-hooks-and-lifecycle)
- [4. Assets and Builds](#4-assets-and-builds)
- [5. Admin UI Standards](#5-admin-ui-standards)
- [6. Editor and Blocks](#6-editor-and-blocks)
- [7. Interop and Boundaries](#7-interop-and-boundaries)
- [8. Compatibility Testing](#8-compatibility-testing)

## 0. Purpose and Scope
### Purpose
- Define WordPress-specific coding expectations that overlay the language standards.
- Keep guidance thin and scoped to WordPress-only behaviour.

### Scope
- Applies to themes, plugins, mu-plugins, and block projects.
- Supplements the [Coding Standards Index](CODING_STANDARDS.md) and the [WordPress Playbook](WORDPRESS.md).

## 1. Data Handling and Security
- Sanitize and validate all untrusted input.
- Escape output based on context (HTML, attributes, URLs, JSON).
- Require nonces for state-changing actions.
- Enforce capability checks before privileged actions.
- Review REST endpoints for permission callbacks and data exposure.

## 2. WordPress APIs
- Prefer core APIs over custom implementations.
- Use Settings API for admin configuration.
- Use Options, Post Meta, Term Meta, and Transients APIs for storage.
- Use `register_post_type` and `register_taxonomy` helpers.
- Use `wp_enqueue_script` and `wp_enqueue_style` for assets.

## 3. Hooks and Lifecycle
- Register hooks on the correct lifecycle actions (`init`, `admin_init`, `wp_enqueue_scripts`).
- Keep hook callbacks focused and testable.
- Document hook priorities when order matters.
- Avoid global side effects on load.

## 4. Assets and Builds
- Separate editor assets from frontend assets.
- Use versioned asset handles and cache busting for enqueued assets.
- Keep build artifacts in repo-approved locations.
- Avoid introducing new tooling without approval.

## 5. Admin UI Standards
- Scope admin assets to the screens that need them.
- Align admin UX with WordPress UI patterns.
- Keep settings pages consistent with core conventions.

## 6. Editor and Blocks
- Use `block.json` for block registration when possible.
- Keep editor-only logic separate from frontend rendering.
- Use `theme.json` for shared tokens when available.
- Avoid direct DOM manipulation in editor contexts.

## 7. Interop and Boundaries
- Localize data with `wp_localize_script` or `wp_add_inline_script`.
- Keep shared data contracts documented and versioned.
- Use REST endpoints with explicit permissions and nonces.
- Avoid conflicts with third-party plugins by namespacing and scoping behaviour.
- Load integrations only when required and for the relevant screens or contexts.

## 8. Compatibility Testing
- Define a target matrix for WordPress core and PHP versions.
- Validate critical paths against the supported plugin ecosystem.
- Record compatibility checks when tests are manual or tool-driven.
