# Changelog 📝

All notable changes to **`nnp-shared-styles`** will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.1.6] - 2026-09-01

### Added
- Standardized open-source build scripts in `package.json` (`build`, `build:min`, `build:all`, `watch`, `prepare`).
- Comprehensive open-source documentation:
  - `README.md`: Modernized with design token quick tables, installation commands, and usage recipes.
  - `USER_MANUAL_AND_DEPLOYMENT_GUIDE.md`: Deep-dive component recipes, CSS variable dictionary, theme toggle hooks, and automated CI/CD release pipelines.
  - `DEVELOPER_GUIDELINES.md`: Local setup guide, architecture walkthrough, Sass `@use` conventions, token creation how-tos, and QA testing checklist.
  - `LICENSE`: MIT License.
  - `CONTRIBUTING.md`: GitHub contribution flow and PR process.
  - `SECURITY.md`: Security vulnerability reporting policy.

### Security
- Scrubbed all internal GitLab URLs and private tokens across the codebase.
- Standardized sensitive endpoint configurations using generic environment placeholders.

### Changed
- Refactored `package.json` entry points for modern build tooling (`main`, `style`, `sass`, `repository`, `bugs`, `homepage`).
