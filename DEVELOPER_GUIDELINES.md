# Developer Guidelines 🛠️👨‍💻

Welcome to the **`nnp-shared-styles`** developer guidelines! This document outlines architecture, local setup, build workflows, coding standards, and step-by-step instructions for extending the library.

---

## 📖 Table of Contents

- [1. Architectural Overview](#1-architectural-overview)
- [2. Development Environment Setup](#2-development-environment-setup)
- [3. Build & Compilation Workflows](#3-build--compilation-workflows)
- [4. SCSS & CSS Coding Standards](#4-scss--css-coding-standards)
- [5. How-To: Common Development Tasks](#5-how-to-common-development-tasks)
  - [5.1 Adding a New Design Token](#51-adding-a-new-design-token)
  - [5.2 Creating a New UI Component Style](#52-creating-a-new-ui-component-style)
  - [5.3 Adding a New Mixin](#53-adding-a-new-mixin)
  - [5.4 Creating a New Client / Multi-Tenant Theme](#54-creating-a-new-client--multi-tenant-theme)
- [6. Quality Assurance & Verification](#6-quality-assurance--verification)
- [7. Git & Contribution Workflow](#7-git--contribution-workflow)
- [8. Release & Publishing Checklist](#8-release--publishing-checklist)

---

## 1. Architectural Overview

`nnp-shared-styles` is designed around modern Dart Sass module mechanics (`@use`) and CSS custom properties (CSS variables). 

### File Hierarchy

```text
src/
├── index.scss                    # Main root stylesheet that aggregates shared modules
├── shared/                       # Global core style definitions
│   ├── nnp-variables.scss        # CSS Custom Properties (:root & dark theme overrides)
│   ├── nnp-mixins.scss           # Sass helper mixins (flexbox, component heights)
│   ├── nnp-base-styles.scss      # Typography, font weights, layout helpers, sizing
│   ├── nnp-component-styles.scss # Pre-built component classes (buttons, headers, nav, modals)
│   └── common-styles.scss        # Shared common overrides
└── clients/                      # Client-specific / white-label style extensions
    ├── clientA-theme/            # Client A styles and variables
    └── clientB-theme/            # Client B styles and variables
```

### Key Principles
1. **Zero Runtime JavaScript**: All theme adaptations, layout dimensions, and typography variations are implemented using CSS custom properties.
2. **Modern Sass Module System**: We exclusively use `@use` (not the deprecated `@import`).
3. **Namespacing**: Core classes use the `.nnp-*` prefix to prevent collision with application styles.

---

## 2. Development Environment Setup

### Prerequisites
- **Node.js**: `v18.0.0` or higher (Node 20+ recommended)
- **Package Manager**: `npm` (bundled with Node) or `yarn` / `pnpm`
- **Git**: `2.30+`

### Initial Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/Nubo-Native-Platform/PICC-PC-NNP-Shared-Styles.git
   cd PICC-PC-NNP-Shared-Styles
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

---

## 3. Build & Compilation Workflows

We use the official Dart Sass compiler (`sass`) to compile SCSS to production-ready CSS bundles in `dist/`.

| Command | Purpose |
| :--- | :--- |
| `npm run build` | Compiles `src/index.scss` into `dist/index.css` (expanded, no sourcemap). |
| `npm run build:min` | Compiles `src/index.scss` into `dist/index.min.css` (compressed production build). |
| `npm run build:all` | Compiles both expanded and minified bundles simultaneously. |
| `npm run watch` | Watches `src/` directory and recompiles `dist/index.css` on every file save. |

### Developing with File Watcher
During local development, keep the watcher running in your terminal:
```bash
npm run watch
```

---

## 4. SCSS & CSS Coding Standards

### 4.1 Module Importing
- Always import dependencies using `@use`:
  ```scss
  // Correct
  @use './nnp-mixins.scss' as mixins;
  @use './nnp-base-styles.scss';

  // Do NOT use deprecated @import
  // @import './nnp-mixins.scss';
  ```

### 4.2 CSS Custom Properties (Variables)
- Declare default light theme variables under `:root` in `src/shared/nnp-variables.scss`.
- Declare dark theme overrides under `html.dark, body.dark-theme`.
- Use descriptive, hierarchical variable names:
  `--[category]-[type]-[variant]`
  - Examples:
    - `--base-color-primary`
    - `--component-color-highlight`
    - `--font-size-md`
    - `--radius-medium`

### 4.3 Class Naming & Namespacing
- Use the `.nnp-` prefix for component classes:
  - Layout: `.nnp-layout-container`, `.nnp-side-nav`
  - Components: `.nnp-btn`, `.nnp-btn-primary`, `.nnp-modal-content`
  - Utility: `.flex-center-center`, `.font-bold`, `.page-padding-medium`

### 4.4 Specificity & Overrides
- Avoid heavy selector nesting (maximum 2-3 levels deep).
- Avoid `!important` in core classes unless overriding aggressive third-party UI framework styles (e.g. Material UI / browser autofill).

---

## 5. How-To: Common Development Tasks

### 5.1 Adding a New Design Token

1. Open `src/shared/nnp-variables.scss`.
2. Add the light theme value inside `:root`:
   ```scss
   :root {
     /* ...existing tokens... */
     --component-badge-bg: #e0f2fe;
     --component-badge-text: #0369a1;
   }
   ```
3. Add the dark theme override inside `html.dark, body.dark-theme`:
   ```scss
   html.dark,
   body.dark-theme {
     /* ...existing tokens... */
     --component-badge-bg: #075985;
     --component-badge-text: #e0f2fe;
   }
   ```
4. Run `npm run build:all` to verify that compilation succeeds without errors.

---

### 5.2 Creating a New UI Component Style

1. Open `src/shared/nnp-component-styles.scss`.
2. Reference necessary mixins or base styles:
   ```scss
   @use './nnp-mixins.scss' as mixins;
   ```
3. Author your component class using CSS custom properties:
   ```scss
   .nnp-badge {
     display: inline-flex;
     align-items: center;
     padding: 0.25rem 0.5rem;
     font-size: var(--font-size-xs);
     border-radius: var(--radius-small);
     background-color: var(--component-badge-bg);
     color: var(--component-badge-text);
   }
   ```
4. If your component requires responsive layout or dark mode specific tweaks, use the established theme selectors.

---

### 5.3 Adding a New Mixin

1. Open `src/shared/nnp-mixins.scss`.
2. Add your mixin with descriptive argument names:
   ```scss
   @mixin truncate-text {
     white-space: nowrap;
     overflow: hidden;
     text-overflow: ellipsis;
   }
   ```
3. Use the mixin in component or base style files:
   ```scss
   @use './nnp-mixins.scss' as mixins;

   .nnp-text-ellipsis {
     @include mixins.truncate-text;
   }
   ```

---

### 5.4 Creating a New Client / Multi-Tenant Theme

To add custom styling for a specific tenant or white-label client:

1. Create a new directory under `src/clients/`:
   ```text
   src/clients/clientC-theme/
   ├── clientC-theme-variables.scss
   └── clientC-theme-styles.scss
   ```
2. Define tenant variable overrides in `clientC-theme-variables.scss`:
   ```scss
   :root[data-client="clientC"] {
     --component-color-highlight: #ff6600;
     --base-color-secondary: #222222;
   }
   ```
3. Define custom layout or component rules in `clientC-theme-styles.scss`.
4. Import your client theme into your client-facing build or document it for tenant integration.

---

## 6. Quality Assurance & Verification

Before submitting changes, run these verification steps:

1. **SCSS Compilation Test**:
   ```bash
   npm run build:all
   ```
   Ensure no Sass warnings or errors are reported.

2. **Verify Output Artifacts**:
   - Check `dist/index.css` to ensure new rules and tokens are rendered properly.
   - Check `dist/index.min.css` to verify file size and minification.

3. **Check for Hardcoded Values**:
   - Ensure color hex values are not hardcoded inside component styles where tokens should be used (`var(--...)`).

---

## 7. Git & Contribution Workflow

We adhere to a standard GitHub Flow branching strategy and Conventional Commits.

### 7.1 Branch Naming Convention
- `feature/<short-description>`: New tokens, components, or mixins.
- `fix/<short-description>`: Bug fixes in existing styles.
- `docs/<short-description>`: Documentation improvements.
- `refactor/<short-description>`: Code cleanup without functional change.

### 7.2 Commit Message Format
Follow [Conventional Commits](https://www.conventionalcommits.org/):
```text
feat(components): add .nnp-badge component styling
fix(variables): correct dark mode contrast for muted text
docs(readme): update integration example for React 18
style(mixins): format flex mixin indentation
```

### 7.3 Pull Request Checklist
Before creating a PR, verify:
- [ ] `npm run build:all` executes cleanly.
- [ ] No private or company-internal credentials, endpoints, or emails are included.
- [ ] Documentation (`README.md`, `USER_MANUAL_AND_DEPLOYMENT_GUIDE.md`) is updated if new components/tokens were added.
- [ ] Commits are well-structured and descriptive.

---

## 8. Release & Publishing Checklist

For maintainers publishing a new version:

1. **Check Working Tree**:
   ```bash
   git status
   ```
2. **Bump Version in `package.json`**:
   ```bash
   # For patch fix: 1.1.6 -> 1.1.7
   npm version patch

   # For new feature: 1.1.6 -> 1.2.0
   npm version minor

   # For breaking change: 1.1.6 -> 2.0.0
   npm version major
   ```
3. **Build Bundles**:
   ```bash
   npm run build:all
   ```
4. **Push Git Tag**:
   ```bash
   git push origin main --tags
   ```
5. **Publish to NPM Registry**:
   ```bash
   npm publish --access public
   ```
