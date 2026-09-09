# Changelog

All notable changes to **`@nubo-native-platform/nnp-shared-styles`** will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.1.7] - 2026-09-09

### Changed
- **Package Scope**: Renamed package from `nnp-shared-styles` to `@nubo-native-platform/nnp-shared-styles` for organization namespace.
- Updated all documentation examples to use scoped package name.
- NPM publishing now publishes under organization account.

### Fixed
- Resolved npm registry configuration to publish to public npm registry instead of GitHub Packages.
- Fixed npm install failures by properly configuring registry for public dependencies.

---

## [1.1.6] - 2026-09-01

### Added
- Standardized open-source build scripts in `package.json` (`build`, `build:min`, `build:all`, `watch`, `prepare`).
- Comprehensive open-source documentation:
  - `README.md`: Modernized with design token quick tables, installation commands, and usage recipes.
  - `USER_MANUAL_AND_DEPLOYMENT_GUIDE.md`: Deep-dive component recipes, CSS variable dictionary, theme toggle hooks, and automated CI/CD release pipelines.
  - `DEVELOPER_GUIDELINES.md`: Local setup guide, architecture walkthrough, Sass `@use` conventions, token creation how-tos, and QA testing checklist.
  - `LICENSE`: MIT License.
  - `CHANGELOG.md`: Release notes and change history.

### Security
- Scrubbed all internal GitLab URLs and private tokens across the codebase.
- Standardized sensitive endpoint configurations using generic environment placeholders.

### Changed
- Refactored `package.json` entry points for modern build tooling (`main`, `style`, `sass`, `repository`, `bugs`, `homepage`).
