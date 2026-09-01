# User Manual & Deployment Guidelines

This guide provides end-to-end documentation for consumers and operations teams utilizing **`nnp-shared-styles`**. It is split into two major sections:
1. **[Part 1: User Manual](#part-1-user-manual)** -- Integrating, consuming, theming, and building interfaces with the design system.
2. **[Part 2: Deployment Guidelines](#part-2-deployment-guidelines)** -- Packaging, publishing, CI/CD pipeline automation, and release management.

---

# Part 1: User Manual

## 1. Overview & Architectural Philosophy

`nnp-shared-styles` is a zero-dependency SCSS/CSS styling foundation engineered for modern web applications. The library is built around three core pillars:
- **CSS Custom Properties (Variables)**: Allows dynamic, real-time styling updates and theme switching without re-compiling SCSS or running JavaScript runtime style calculations.
- **Utility & Layout Abstractions**: Standardizes navigation bars, side drawers, modals, accordions, and flexbox alignments.
- **Cross-Framework Compatibility**: Directly usable in React, Angular, Vue, Svelte, or vanilla HTML/CSS.

---

## 2. Installation & Setup

### Package Installation

```bash
# Using npm
npm install nnp-shared-styles

# Using yarn
yarn add nnp-shared-styles

# Using pnpm
pnpm add nnp-shared-styles
```

---

## 3. Importing Styles into Your Project

### Option A: SCSS Pipeline (Recommended for customization)
If your project uses Sass/SCSS, import the root SCSS file in your top-level stylesheet (e.g. `src/styles.scss` or `src/App.scss`):

```scss
// Import everything (tokens, mixins, layouts, components)
@use 'nnp-shared-styles/src/index.scss';

// Or selectively import individual modules
@use 'nnp-shared-styles/src/shared/nnp-variables.scss';
@use 'nnp-shared-styles/src/shared/nnp-mixins.scss' as mixins;
@use 'nnp-shared-styles/src/shared/nnp-base-styles.scss';
@use 'nnp-shared-styles/src/shared/nnp-component-styles.scss';
```

### Option B: Pre-Compiled CSS (Zero build step)
If you don't use Sass, import the compiled CSS directly:

```javascript
// In React / Next.js / Vite entrypoint (e.g. main.tsx or index.js)
import 'nnp-shared-styles/dist/index.min.css';
```

```html
<!-- In HTML header -->
<link rel="stylesheet" href="node_modules/nnp-shared-styles/dist/index.min.css" />
```

---

## 4. Design Tokens & CSS Custom Properties Reference

All design tokens are declared as CSS custom properties under `:root` and automatically adapt when switching between light and dark themes.

### 4.1 Typography Tokens
| CSS Variable | Default Value | Description |
| :--- | :--- | :--- |
| `--font-family-special` | `Verdana, sans-serif` | Special font for navigation and headers |
| `--font-family-header` | `"Helvetica"` | Main font for headings |
| `--font-family-body` | `"Helvetica"` | Default body copy font |
| `--font-size-xs` | `0.70rem` | Extra small text |
| `--font-size-sm` | `0.78rem` | Small text / secondary labels |
| `--font-size-nm` | `0.85rem` | Normal text |
| `--font-size-md` | `0.98rem` | Medium text / default body |
| `--font-size-lg` | `1.115rem` | Large text / sub-headings |
| `--font-size-xl` | `1.25rem` | Extra large text |
| `--font-size-xxl` | `2.00rem` | Display / hero headings |
| `--font-light` | `200` | Light font weight |
| `--font-normal` | `400` | Normal font weight |
| `--font-bold` | `600` | Bold font weight |
| `--fold-bolder` | `800` | Extra bold font weight |

### 4.2 Sizing, Spacing & Border Radii
| CSS Variable | Default Value | Description |
| :--- | :--- | :--- |
| `--nnp-padding-small` | `0.5rem` | Small padding unit (8px equivalent) |
| `--nnp-padding-medium` | `1rem` | Medium padding unit (16px equivalent) |
| `--nnp-padding-large` | `2rem` | Large padding unit (32px equivalent) |
| `--radius-small` | `0.15rem` | Minor rounded corners |
| `--radius-medium` | `0.25rem` | Standard component corner radius |
| `--radius-large` | `0.75rem` | Card / modal container corner radius |
| `--component-height-small` | `30px` | Small button/input height |
| `--component-height-medium` | `50px` | Header/primary component height |
| `--component-height-large` | `150px` | Logo panel/footer height |
| `--nav-width` | `260px` | Sidebar navigation expanded width |

### 4.3 Color Tokens (Light vs. Dark Theme)

| Token Name | Light Theme Value | Dark Theme Value | Purpose |
| :--- | :--- | :--- | :--- |
| `--base-color-primary` | `#E8E8E8` | `#3D3D3D` | Primary page background surface |
| `--base-color-secondary` | `#000000` | `#1E1E1E` | Inverted surface / deep background |
| `--base-color-tertiary` | `#444444` | `#444444` | Subtle container background |
| `--component-color-primary` | `#666666` | `#666666` | Neutral component accents |
| `--component-color-secondary` | `#FFFBFB` | `#1E1E1E` | Light component background surface |
| `--component-color-tertiary` | `#CCCCCC` | `#2F2F2F` | Border / divider / hover accent |
| `--component-color-highlight` | `#0099CC` | `#0099CC` | Primary brand action color |
| `--text-color-primary` | `#000000` | `#FFFFFF` | Primary body typography |
| `--text-color-secondary` | `#FFFFFF` | `#FFFFFF` | Inverted text color (on dark backgrounds) |
| `--text-color-tertiary` | `#0099CC` | `#B0BEC5` | Accent text color |
| `--text-color-quaternary` | `#7E7E7E` | `#A6A6A6` | Muted / secondary caption text |
| `--text-color-link` | `#0099CC` | `#84DEF1` | Hyperlink color |
| `--text-color-disabled` | `#F44336` | `#F44336` | Warning / error / disabled state |
| `--top-header-background-color`| `#000000` | `#121212` | Main top navigation background |
| `--bottom-footer-background-color`| `#000000` | `#1E1E1E` | Footer background |

---

## 5. Light / Dark Theme Switching

To switch themes, toggle the CSS class `dark` on `<html>` or `dark-theme` on `<body>`.

### 5.1 Pure JavaScript Implementation
```javascript
// Set Dark Mode
document.documentElement.classList.add('dark');

// Set Light Mode
document.documentElement.classList.remove('dark');

// Toggle
function toggleTheme() {
  const isDark = document.documentElement.classList.toggle('dark');
  localStorage.setItem('app-theme', isDark ? 'dark' : 'light');
}

// Restore saved preference on load
const savedTheme = localStorage.getItem('app-theme') || 'light';
if (savedTheme === 'dark') {
  document.documentElement.classList.add('dark');
}
```

### 5.2 React Hook Implementation
```tsx
import { useState, useEffect } from 'react';

export function useTheme() {
  const [theme, setTheme] = useState<'light' | 'dark'>(() => {
    return (localStorage.getItem('theme') as 'light' | 'dark') || 'light';
  });

  useEffect(() => {
    const root = document.documentElement;
    if (theme === 'dark') {
      root.classList.add('dark');
    } else {
      root.classList.remove('dark');
    }
    localStorage.setItem('theme', theme);
  }, [theme]);

  const toggleTheme = () => setTheme(prev => (prev === 'light' ? 'dark' : 'light'));

  return { theme, toggleTheme };
}
```

---

## 6. Layout & Component Usage Recipes

### 6.1 Standard Application Layout
```html
<div class="nnp-layout-container">
  <!-- Top Navigation Header -->
  <header class="nnp-top-header">
    <div class="nnp-menu-item">Dashboard</div>
    <div class="nnp-menu-item active">Analytics</div>
    <div class="nnp-menu-item">Settings</div>
  </header>

  <!-- Main Body Content -->
  <main class="nnp-main-container">
    <div class="nnp-main-content page-padding-medium">
      <h1 class="nnp-title">Welcome to the Portal</h1>
      <p class="body-font">Standardized layout with consistent header height.</p>
    </div>
  </main>

  <!-- Bottom Footer -->
  <footer class="nnp-bottom-footer">
    <p>(c) Nubo Native Platform. All rights reserved.</p>
  </footer>
</div>
```

### 6.2 Side-Navigation Layout
```html
<div class="nnp-side-layout-container">
  <div class="nnp-side-main-container">
    <!-- Sidebar Navigation -->
    <aside class="nnp-side-nav">
      <div class="nnp-side-menu-item">
        <div class="nnp-side-menu-header active">
          <span>Overview</span>
          <span class="nnp-side-menu-arrow">&gt;</span>
        </div>
      </div>
      <div class="nnp-side-menu-item">
        <div class="nnp-side-menu-header">
          <span>Reports</span>
          <span class="nnp-side-menu-arrow">&gt;</span>
        </div>
      </div>
    </aside>

    <!-- Side Main Content Area -->
    <section class="nnp-side-main-content">
      <h2>Main Content View</h2>
    </section>
  </div>
</div>
```

### 6.3 Buttons
```html
<!-- Primary action button -->
<button class="nnp-btn nnp-btn-primary">Submit</button>

<!-- Secondary neutral button -->
<button class="nnp-btn nnp-btn-secondary">Cancel</button>

<!-- Tertiary background-toned button -->
<button class="nnp-btn nnp-btn-tertiary">Details</button>

<!-- Disabled button -->
<button class="nnp-btn nnp-btn-disabled" disabled>Unavailable</button>
```

### 6.4 Modals & Popups
```html
<div class="nnp-modal-container">
  <div class="nnp-modal-content">
    <div class="nnp-header nnp-header-primary flex-space-center">
      <span>Confirm Action</span>
      <span class="cursor-pointer">&times;</span>
    </div>
    <div class="nnp-modal-body">
      <p>Are you sure you want to proceed with this operation?</p>
    </div>
  </div>
</div>
```

### 6.5 Material UI DataGrid Theming
When using MUI DataGrid in your application, `nnp-shared-styles` automatically adjusts grid rows, cells, and header colors for dark mode:
```tsx
import { DataGrid } from '@mui/x-data-grid';

export function UserGrid({ rows, columns }: any) {
  return (
    <div style={{ height: 400, width: '100%' }}>
      <DataGrid rows={rows} columns={columns} />
    </div>
  );
}
```

---

# Part 2: Deployment Guidelines

This section provides complete operational guidelines for packaging, versioning, publishing, and automating CI/CD releases of `nnp-shared-styles`.

---

## 1. Release Architecture & Assets

When publishing `nnp-shared-styles`, two deliverables are distributed:
1. **SCSS Sources (`src/`)**: For consumers who build styles using Sass and override variables.
2. **Pre-compiled CSS (`dist/index.css` & `dist/index.min.css`)**: For consumers who prefer standalone CSS imports.

The `package.json` manifest includes the `prepare` lifecycle hook to automatically compile CSS bundles before any `npm publish` or `npm pack` command:
```json
"scripts": {
  "build": "sass src/index.scss dist/index.css --no-source-map",
  "build:min": "sass src/index.scss dist/index.min.css --style=compressed --no-source-map",
  "build:all": "npm run build && npm run build:min",
  "prepare": "npm run build:all"
}
```

---

## 2. Publishing to Registries

### 2.1 Public NPM Registry (`registry.npmjs.org`)

1. Authenticate with npm:
   ```bash
   npm login
   ```
2. Verify you have appropriate maintainer rights:
   ```bash
   npm whoami
   ```
3. Test package packaging locally:
   ```bash
   npm pack --dry-run
   ```
4. Publish the package:
   ```bash
   npm publish --access public
   ```

### 2.2 GitHub Packages (`npm.pkg.github.com`)

To publish to GitHub Packages:

1. Update package scope in `package.json`:
   ```json
   {
     "name": "@nubo-native-platform/picc-pc-nnp-shared-styles",
     "publishConfig": {
       "registry": "https://npm.pkg.github.com"
     }
   }
   ```
2. Configure `.npmrc` with a generic token placeholder:
   ```ini
   @Nubo-Native-Platform:registry=https://npm.pkg.github.com
   //npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}
   ```
3. Publish:
   ```bash
   npm publish
   ```

### 2.3 Private Registry (Artifactory / Nexus / Verdaccio)

1. Configure `.npmrc`:
   ```ini
   registry=https://<YOUR_PRIVATE_REGISTRY_URL>/repository/npm-hosted/
   //<YOUR_PRIVATE_REGISTRY_URL>/repository/npm-hosted/:_authToken=${NPM_AUTH_TOKEN}
   always-auth=true
   ```
2. Run publish:
   ```bash
   npm publish
   ```

---

## 3. Automated CI/CD Pipelines

### 3.1 GitHub Actions Release Workflow

Create `.github/workflows/release.yml`:

```yaml
name: Build & Release Package

on:
  push:
    tags:
      - 'v*.*.*'
  workflow_dispatch:

jobs:
  build-and-publish:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          registry-url: 'https://registry.npmjs.org'

      - name: Install Dependencies
        run: npm ci

      - name: Build CSS Bundles
        run: npm run build:all

      - name: Publish to NPM
        run: npm publish --access public
        env:
          NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}
```

### 3.2 GitLab CI/CD Pipeline

Create `.gitlab-ci.yml`:

```yaml
stages:
  - test
  - build
  - publish

default:
  image: node:20-alpine

cache:
  paths:
    - node_modules/

install_dependencies:
  stage: test
  script:
    - npm ci

build_artifacts:
  stage: build
  script:
    - npm run build:all
  artifacts:
    paths:
      - dist/
    expire_in: 1 week

publish_package:
  stage: publish
  rules:
    - if: '$CI_COMMIT_TAG =~ /^v\d+\.\d+\.\d+$/'
  script:
    - echo "//${CI_SERVER_HOST}/api/v4/projects/${CI_PROJECT_ID}/packages/npm/:_authToken=${CI_JOB_TOKEN}">.npmrc
    - npm publish
```

---

## 4. Semantic Versioning (SemVer) Guidelines

Follow [Semantic Versioning 2.0.0](https://semver.org/) when incrementing package versions:

| Version Increment | Rule | Example Trigger |
| :--- | :--- | :--- |
| **PATCH (`x.x.+1`)** | Backward-compatible bug fixes or minor CSS tweaks. | Adjusting a hover color, fixing a padding quirk, or correcting a typo. |
| **MINOR (`x.+1.0`)** | Backward-compatible new features or new tokens. | Adding a new component style (e.g. `.nnp-card`), introducing new CSS variables, or adding a new client theme. |
| **MAJOR (`+1.0.0`)** | Breaking structural changes. | Renaming or deleting CSS classes, removing core CSS custom properties, or changing structural layout dependencies. |

---

## 5. Security, Secret Management & Placeholders

To maintain open-source hygiene:
1. **Never commit `.npmrc` files containing raw authentication tokens.**
2. Always use environment variable expansion (e.g., `${NPM_TOKEN}` or `${GITHUB_TOKEN}`).
3. Ensure `.gitignore` ignores `node_modules/`, `*.local`, `logs`, and temporary auth files.
4. If setting up staging/production deployment endpoints, replace internal URLs with placeholders:
   - Private registry URL: `https://<YOUR_REGISTRY_DOMAIN>/repository/npm-releases/`
   - Git repository URL: `https://github.com/Nubo-Native-Platform/PICC-PC-NNP-Shared-Styles.git`
   - Support contact: `<maintainer-email@example.com>`
