# nnp-shared-styles 🎨

> A modular, lightweight SCSS/CSS design system and styling foundation providing design tokens, CSS custom properties, light/dark themes, responsive layout utilities, and reusable component styles.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![NPM Version](https://img.shields.io/badge/npm-v1.1.6-orange.svg)](https://www.npmjs.com/)
[![SCSS](https://img.shields.io/badge/style-SCSS-CC6699.svg)](https://sass-lang.com/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](DEVELOPER_GUIDELINES.md)

---

## 📖 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Quick Start & Usage](#quick-start--usage)
  - [1. Using SCSS (@use)](#1-using-scss-use)
  - [2. Using Pre-compiled CSS](#2-using-pre-compiled-css)
  - [3. Integration by Framework](#3-integration-by-framework)
- [Theming (Light & Dark Mode)](#theming-light--dark-mode)
- [Core Design Tokens](#core-design-tokens)
- [Component & Utility Classes](#component--utility-classes)
- [NPM Scripts](#npm-scripts)
- [Documentation & Guidelines](#documentation--guidelines)
- [Contributing](#contributing)
- [Security & Credentials](#security--credentials)
- [License](#license)

---

## 🌟 Overview

`nnp-shared-styles` is an open-source styling library engineered to deliver a consistent look-and-feel across multi-project ecosystems. It provides:
- **Design Tokens**: Standardized CSS custom properties for colors, typography, spacing, border radii, and component dimensions.
- **Dynamic Theming**: Seamless runtime switching between Light and Dark modes.
- **Layout Engines**: Flexbox helper classes, sticky headers, collapsible side navigation, and responsive content wrappers.
- **Component Foundations**: Built-in styling for buttons, modals, accordions, cards, and third-party UI overrides (e.g., Material UI DataGrid).
- **Client Themes**: Extensible folder structure for white-label and multi-tenant customization.

---

## ✨ Key Features

- **⚡ Zero JS Dependencies**: Pure SCSS and CSS with zero JavaScript overhead.
- **🌓 Instant Dark Mode**: Toggle between themes effortlessly by switching the `.dark` or `.dark-theme` class.
- **🧩 Modular Architecture**: Import only what you need, or include the full compiled stylesheet.
- **📱 Responsive & Cross-Browser**: Standardized scrollbar styling, modern autofill overrides, and flexible layouts.
- **🎯 Component Agnostic**: Works seamlessly with React, Angular, Vue, Svelte, or vanilla HTML/CSS.

---

## 📁 Project Structure

```text
nnp-shared-styles/
├── dist/                                # Compiled CSS production bundles
│   ├── index.css                        # Expanded compiled CSS
│   └── index.min.css                    # Minified compiled CSS
├── src/                                 # SCSS source files
│   ├── index.scss                       # Main entry point importing all shared modules
│   ├── clients/                         # Client-specific / white-label themes
│   │   ├── clientA-theme/               # Client A customization overrides
│   │   └── clientB-theme/               # Client B customization overrides
│   └── shared/                          # Core design system modules
│       ├── common-styles.scss           # Common style definitions
│       ├── nnp-base-styles.scss         # Typography, sizing, borders, and layout helpers
│       ├── nnp-component-styles.scss    # UI components (buttons, nav, modals, tables)
│       ├── nnp-mixins.scss              # Reusable Sass mixins (flex, dimensions)
│       └── nnp-variables.scss           # CSS custom properties (colors, fonts, tokens)
├── package.json                         # Package manifest & build scripts
├── USER_MANUAL_AND_DEPLOYMENT_GUIDE.md  # Detailed user manual & deployment pipelines
└── DEVELOPER_GUIDELINES.md              # Developer setup, build, and contribution guide
```

---

## 📦 Installation

Install the package via your preferred package manager:

```bash
# Using npm
npm install nnp-shared-styles

# Using yarn
yarn add nnp-shared-styles

# Using pnpm
pnpm add nnp-shared-styles
```

Or install directly from the GitHub repository:

```bash
npm install git+https://github.com/Nubo-Native-Platform/PICC-PC-NNP-Shared-Styles.git#v1.1.6
```

---

## 🚀 Quick Start & Usage

### 1. Using SCSS (@use)

Import the master SCSS stylesheet directly in your project's main stylesheet (e.g., `styles.scss` or `App.scss`):

```scss
// Import the entire design system
@use 'nnp-shared-styles/src/index.scss';

// Or import specific modules individually
@use 'nnp-shared-styles/src/shared/nnp-variables.scss';
@use 'nnp-shared-styles/src/shared/nnp-mixins.scss' as mixins;
@use 'nnp-shared-styles/src/shared/nnp-base-styles.scss';
@use 'nnp-shared-styles/src/shared/nnp-component-styles.scss';
```

### 2. Using Pre-compiled CSS

If your project does not use a Sass compiler, import the pre-compiled CSS bundle:

```javascript
// In your application root file (e.g., main.js, index.tsx, App.jsx)
import 'nnp-shared-styles/dist/index.min.css';
```

Or link it directly in your HTML `<head>`:

```html
<link rel="stylesheet" href="node_modules/nnp-shared-styles/dist/index.min.css" />
```

---

### 3. Integration by Framework

#### React / Next.js / Vite
```tsx
// src/index.tsx or src/main.tsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import 'nnp-shared-styles/dist/index.min.css';
import App from './App';

ReactDOM.createRoot(document.getElementById('root')!).render(<App />);
```

#### Angular
```json
// angular.json
"styles": [
  "node_modules/nnp-shared-styles/dist/index.min.css",
  "src/styles.scss"
]
```

#### Vue.js
```vue
<!-- src/App.vue -->
<style>
@import 'nnp-shared-styles/dist/index.min.css';
</style>
```

---

## 🌓 Theming (Light & Dark Mode)

All color tokens are bound to CSS custom properties. By default, the root variables apply the **Light Theme**.

To switch to **Dark Theme**, add either the `dark` class to `<html>` or `dark-theme` to `<body>`:

```html
<!-- Enable Dark Theme via HTML class -->
<html class="dark">
  ...
</html>

<!-- Or enable Dark Theme via Body class -->
<body class="dark-theme">
  ...
</body>
```

### Dynamic Theme Toggle Example (JavaScript)

```typescript
function toggleDarkMode(isDark: boolean) {
  const root = document.documentElement;
  if (isDark) {
    root.classList.add('dark');
  } else {
    root.classList.remove('dark');
  }
}
```

---

## 🎨 Core Design Tokens

A snapshot of the key CSS variables available in your stylesheets:

| Variable Category | CSS Variable Names | Example Default Value |
| :--- | :--- | :--- |
| **Typography** | `--font-family-special`, `--font-family-header`, `--font-family-body` | `Verdana, sans-serif`, `"Helvetica"` |
| **Font Sizes** | `--font-size-xs`, `--font-size-sm`, `--font-size-nm`, `--font-size-md`, `--font-size-lg`, `--font-size-xl`, `--font-size-xxl` | `0.70rem` to `2.0rem` |
| **Border Radii** | `--radius-small`, `--radius-medium`, `--radius-large` | `0.15rem`, `0.25rem`, `0.75rem` |
| **Padding** | `--nnp-padding-small`, `--nnp-padding-medium`, `--nnp-padding-large` | `0.5rem`, `1rem`, `2rem` |
| **Component Heights**| `--component-height-small`, `--component-height-medium`, `--component-height-large` | `30px`, `50px`, `150px` |
| **Light Theme Colors** | `--base-color-primary`, `--component-color-highlight`, `--text-color-primary` | `#E8E8E8`, `#0099cc`, `#000000` |
| **Dark Theme Colors** | `--base-color-primary`, `--component-color-highlight`, `--text-color-primary` | `#3D3D3D`, `#0099cc`, `#ffffff` |

For the complete list of tokens and their values, refer to the [User Manual](USER_MANUAL_AND_DEPLOYMENT_GUIDE.md).

---

## 🧩 Component & Utility Classes

### Layout
- `.nnp-layout-container`: Base full-height column layout.
- `.nnp-top-header`: Standardized sticky application top navigation bar.
- `.nnp-side-layout-container`: Flex container for side-nav + main workspace.
- `.nnp-side-nav`: Collapsible vertical navigation sidebar with smooth animation.

### Buttons
```html
<button class="nnp-btn nnp-btn-primary">Primary Button</button>
<button class="nnp-btn nnp-btn-secondary">Secondary Button</button>
<button class="nnp-btn nnp-btn-tertiary">Tertiary Button</button>
<button class="nnp-btn nnp-btn-disabled" disabled>Disabled Button</button>
```

### Modals & Dialogs
```html
<div class="nnp-modal-container">
  <div class="nnp-modal-content">
    <div class="nnp-header nnp-header-primary">Modal Title</div>
    <div class="nnp-modal-body">Modal Content Goes Here...</div>
  </div>
</div>
```

---

## 🛠 NPM Scripts

| Command | Description |
| :--- | :--- |
| `npm run build` | Compiles SCSS sources to uncompressed `dist/index.css`. |
| `npm run build:min` | Compiles and compresses SCSS to `dist/index.min.css`. |
| `npm run build:all` | Compiles both expanded and minified production bundles. |
| `npm run watch` | Watches SCSS source files for changes and re-compiles automatically. |

---

## 📚 Documentation & Guidelines

- 📘 **[User Manual & Deployment Guide](USER_MANUAL_AND_DEPLOYMENT_GUIDE.md)**:
  - Deep-dive component integration recipes.
  - Complete CSS variable and theme catalog.
  - Step-by-step CI/CD pipeline automation (GitHub Actions & GitLab CI).
  - Package publishing workflows (Public npm, Private Registries, GitHub Packages).
- 🛠 **[Developer Guidelines](DEVELOPER_GUIDELINES.md)**:
  - Developer workstation setup.
  - SCSS coding standards, token architecture, and mixin conventions.
  - Guide to adding new components and client themes.
  - Contribution and pull request workflows.
- 🤝 **[Contributing Guide](CONTRIBUTING.md)**: Quick contribution workflow and checklist.
- 🔒 **[Security Policy](SECURITY.md)**: Vulnerability disclosure and reporting procedure.
- 📝 **[Changelog](CHANGELOG.md)**: Version release notes and change history.

---

## 🤝 Contributing

We welcome contributions from the community! Please check our [Contributing Guide](CONTRIBUTING.md) and [Developer Guidelines](DEVELOPER_GUIDELINES.md) before submitting a Pull Request.

1. Fork the repository on [GitHub](https://github.com/Nubo-Native-Platform/PICC-PC-NNP-Shared-Styles).
2. Create your feature branch (`git checkout -b feature/amazing-feature`).
3. Commit your changes (`git commit -m 'feat: add amazing feature'`).
4. Push to the branch (`git push origin feature/amazing-feature`).
5. Open a Pull Request.

---

## 🔒 Security & Credentials Policy

This project strictly adheres to open-source security standards:
- **No hardcoded secrets or credentials**: All internal URLs, tokens, passwords, and private registry endpoints have been scrubbed.
- Use environment variables (e.g., `NPM_TOKEN`, `GITHUB_TOKEN`) when deploying or publishing packages.
- Placeholders such as `<YOUR_ORGANIZATION>`, `<YOUR_REGISTRY_URL>`, and `<AUTH_TOKEN>` are used throughout configuration templates and documentation.

---

## 📄 License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.
