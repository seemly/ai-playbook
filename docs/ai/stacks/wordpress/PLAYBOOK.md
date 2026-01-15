# AI WordPress Playbook (Overlay)

## Index
- [0. Purpose and Scope](#0-purpose-and-scope)
- [1. How to Use](#1-how-to-use)
- [2. Decision Tree](#2-decision-tree)
- [3. Project Types](#3-project-types)
- [4. Environment and Tooling](#4-environment-and-tooling)
- [5. Project Structure](#5-project-structure)
- [6. Security and Data Handling](#6-security-and-data-handling)
- [7. Database and Queries](#7-database-and-queries)
- [8. REST API](#8-rest-api)
- [9. Hooks and Lifecycle](#9-hooks-and-lifecycle)
- [10. Admin UI and Settings](#10-admin-ui-and-settings)
- [11. Blocks and Editor](#11-blocks-and-editor)
- [12. Internationalization](#12-internationalization)
- [13. Testing and QA](#13-testing-and-qa)
- [14. Performance](#14-performance)
- [15. Release and Deployment](#15-release-and-deployment)
- [16. Data Migrations and Versioning](#16-data-migrations-and-versioning)
- [17. Logging and Error Handling](#17-logging-and-error-handling)
- [18. Deprecation and Backwards Compatibility](#18-deprecation-and-backwards-compatibility)
- [19. Coding Standards References](#19-coding-standards-references)
- [20. References and Links](#20-references-and-links)

## 0. Purpose and Scope
### Purpose
- Define WordPress-specific rules that overlay the baseline [AI Playbook](../../AI_PLAYBOOK.md).
- Keep guidance thin and focused on WordPress-only requirements.

### Scope
- Applies to WordPress themes, plugins, mu-plugins, and block projects.
- Applies to AI-assisted changes touching WordPress runtime behaviour.
- If this overlay is stricter than the base playbook, follow the stricter rule.

## 1. How to Use
- Read [AI Playbook](../../AI_PLAYBOOK.md) first for baseline rules.
- Use this overlay for WordPress-specific decisions and workflows.
- Use the [Coding Standards Index](../../standards/INDEX.md) for language rules.
- If a rule is missing or unclear, stop and request guidance.

## 2. Decision Tree
- If building a theme or block theme, focus on Sections 5, 10, and 11.
- If building a plugin or mu-plugin, focus on Sections 6, 7, 8, and 9.
- If working on editor UI, prioritize Sections 10 and 15.
- If working on shared styling, prioritize Sections 15 and the CSS standards.

## 3. Project Types
- **Theme**: presentation layer using templates, `functions.php`, and theme assets.
- **Block theme**: theme with `theme.json` and block templates.
- **Plugin**: feature logic that is portable across themes.
- **MU plugin**: must-use plugin loaded automatically for all sites.

## 4. Environment and Tooling
- Align WordPress and PHP versions with the project runtime requirements.
- Use `wp-cli` for local management and scripted tasks.
- Use `composer` for PHP dependencies where configured.
- Use `npm`/`pnpm` tooling for assets where configured.
- Record tool version requirements in the repo when they change.

## 5. Project Structure
- Themes should follow the WordPress template hierarchy and keep assets alongside templates.
- Plugins should keep a small bootstrap file and route logic into `includes/` or `src/`.
- Use `includes/` for procedural helpers, hooks registration, and WordPress integrations.
- Use `src/` for class-based code, services, and PSR-4 autoloaded namespaces.
- Keep assets organized by build target (editor vs frontend).
- Use `block.json` to declare block metadata and assets.
- Use Composer with PSR-4 autoloading for plugin class loading.
- Commit `vendor/` and `composer.lock` so dependencies stay deterministic.

## 6. Security and Data Handling
- Sanitize input with `sanitize_text_field`, `sanitize_email`, `sanitize_textarea_field`, `absint`.
- Escape output with `esc_html`, `esc_attr`, `esc_url`, `wp_kses_post`.
- Require nonces for state-changing actions (`wp_nonce_field`, `check_admin_referer`).
- Enforce capability checks before privileged actions (`current_user_can`).
- Validate file uploads and restrict MIME types (`wp_check_filetype_and_ext`).
- Review REST endpoints for permissions and data exposure.
- Reference WordPress security guidance: https://developer.wordpress.org/plugins/security/

## 7. Database and Queries
- Prefer WordPress APIs over custom SQL.
- If `$wpdb` is required, use prepared statements.
- Prefer options, post meta, term meta, and transients where appropriate.
- Document data storage and migration expectations.

## 8. REST API
- Require `permission_callback` for all routes.
- Enforce authentication and authorization in REST handlers.
- Return `WP_Error` for failure cases with clear error codes.
- Validate and sanitize request arguments with schemas.

## 9. Hooks and Lifecycle
- Register hooks on the appropriate lifecycle action (`init`, `admin_init`, `enqueue`).
- Keep action and filter handlers focused and testable.
- Avoid adding global side effects on load.
- Document hook priorities when order matters.

## 10. Admin UI and Settings
- Use the Settings API for configuration screens.
- Gate settings screens behind capability checks.
- Ensure admin UX is consistent with WordPress patterns.
- Keep admin assets scoped to the relevant screens.

## 11. Blocks and Editor
- Use `block.json` for block registration when possible.
- Separate editor-only logic from frontend rendering.
- Use `theme.json` for shared design tokens.
- Keep editor styles and frontend styles isolated.

## 12. Internationalization
- Use a single text domain per theme or plugin.
- Wrap user-facing strings in i18n functions.
- Ensure translation files are loaded correctly.

## 13. Testing and QA
- Prefer automated tests where project tooling exists.
- Validate behaviour in both editor and frontend contexts.
- Record manual checks when automated tests are not available.

## 14. Performance
- Avoid unnecessary queries in loops and templates.
- Use caching or transients for expensive operations.
- Optimize asset loading and avoid duplicate enqueues.

## 15. Release and Deployment
- Keep version numbers consistent across plugin headers and assets.
- Document build steps required for release artifacts.
- Confirm upgrade and rollback steps for data changes.

## 16. Data Migrations and Versioning
- Track data schema or option changes with explicit versions.
- Provide upgrade routines for new data structures.
- Ensure migrations are idempotent and safe to re-run.
- Document rollback considerations for destructive changes.

## 17. Logging and Error Handling
- Use structured error messages and consistent error codes.
- Avoid logging sensitive data or secrets.
- Prefer WordPress logging or established project logging utilities.
- Capture failure paths in admin notices or REST responses.

## 18. Deprecation and Backwards Compatibility
- Deprecate hooks and filters with clear alternatives.
- Maintain backwards compatibility for public APIs when possible.
- Document version cutoffs for removals.
- Provide migration notes for consumers.

## 19. Coding Standards References
- [Coding Standards Index](../../standards/INDEX.md)
- [AI Coding Standards (PHP)](../../standards/php.md)
- [AI Coding Standards (JS/TS)](../../standards/js.md)
- [AI Coding Standards (CSS)](../../standards/css.md)
- [AI Coding Standards (WordPress)](../../standards/wordpress.md)

## 20. References and Links
- Add WordPress official docs links as needed.
- Add project-specific architecture docs as needed.
