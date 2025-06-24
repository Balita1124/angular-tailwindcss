# Angular material(SCSS) with TailwindCSS

## Installation
### Create angular project 
```sh
npx @angular/cli@20 new angular-tailwindcss
```
### Add angular material
```sh
npx ng add @angular/material
```
### Add Tailwind
```sh
npm install tailwindcss @tailwindcss/postcss autoprefixer postcss-import postcss-preset-env
```
## Configuration

### .postcssrc.json
```json
{
  "plugins": {
    "@tailwindcss/postcss": {
      "optimize": {
        "minify": true
      }
    },
    "postcss-import": {},
    "autoprefixer": {},
    "postcss-preset-env": {}
  }
}
```
### .vscode/extensions.json
```json
{
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=827846
  "recommendations": ["angular.ng-template", "csstools.postcss"]
}
```

### .vscode/settings.json
```json
{
  "css.customData": [".vscode/tailwind.json"]
}
```
### .vscode/tailwind.json
```json
{
  "version": 1.1,
  "atDirectives": [
    {
      "name": "@tailwind",
      "description": "Use the `@tailwind` directive to insert Tailwind's `base`, `components`, `utilities` and `screens` styles into your CSS.",
      "references": [
        {
          "name": "Tailwind Documentation",
          "url": "https://tailwindcss.com/docs/functions-and-directives#tailwind"
        }
      ]
    },
    {
      "name": "@apply",
      "description": "Use the `@apply` directive to inline any existing utility classes into your own custom CSS. This is useful when you find a common utility pattern in your HTML that you’d like to extract to a new component.",
      "references": [
        {
          "name": "Tailwind Documentation",
          "url": "https://tailwindcss.com/docs/functions-and-directives#apply"
        }
      ]
    },
    {
      "name": "@responsive",
      "description": "You can generate responsive variants of your own classes by wrapping their definitions in the `@responsive` directive:\n```css\n@responsive {\n  .alert {\n    background-color: #E53E3E;\n  }\n}\n```\n",
      "references": [
        {
          "name": "Tailwind Documentation",
          "url": "https://tailwindcss.com/docs/functions-and-directives#responsive"
        }
      ]
    },
    {
      "name": "@screen",
      "description": "The `@screen` directive allows you to create media queries that reference your breakpoints by **name** instead of duplicating their values in your own CSS:\n```css\n@screen sm {\n  /* ... */\n}\n```\n…gets transformed into this:\n```css\n@media (min-width: 640px) {\n  /* ... */\n}\n```\n",
      "references": [
        {
          "name": "Tailwind Documentation",
          "url": "https://tailwindcss.com/docs/functions-and-directives#screen"
        }
      ]
    },
    {
      "name": "@variants",
      "description": "Generate `hover`, `focus`, `active` and other **variants** of your own utilities by wrapping their definitions in the `@variants` directive:\n```css\n@variants hover, focus {\n   .btn-brand {\n    background-color: #3182CE;\n  }\n}\n```\n",
      "references": [
        {
          "name": "Tailwind Documentation",
          "url": "https://tailwindcss.com/docs/functions-and-directives#variants"
        }
      ]
    }
  ]
}
```

### styles.scss

```scss
@use "sass:meta";
@use '@angular/material' as mat;
@use 'tailwindcss';


@use './styles/tailwind';

// Defining default font

$heading-font-family: Poppins, sans-serif;
$regular-font-family: Inter, sans-serif;

@include sizes.sizes();

// #region: Setting @angular/material custom theme
html {
  color-scheme: light;
  @include mat.theme((
    color: (
      primary: mat.$azure-palette,
      tertiary: mat.$blue-palette,
    ),
    // typography: Roboto,
    typography: (
      plain-family: #{meta.inspect($regular-font-family)},
      brand-family: #{meta.inspect($heading-font-family)},
    ),
    density: 0
  ));
}
// #endregion

// #region: Setting @angular/material dark theme
.dark-theme {
  color-scheme: dark;
}
```

### styles/_tailwind.scss
```scss
@use "tailwindcss";

// base for setting the font-families
@layer base {
  body {
    // same as `plain-family` in angular material
    font-family: var(--mat-sys-body-large-font), sans-serif;
  }
  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    // same as `brand-family` in angular material
    font-family: var(--mat-sys-display-large-font), sans-serif;
  }
}

@utility form-field-error-icon {
  vertical-align: bottom;
  font-variation-settings: "FILL" 1;
  height: 16px !important;
  width: 16px !important;
  font-size: 16px !important;
}

@utility icon-filled {
  font-variation-settings: "FILL" 1;
}

// `.dark-theme` is the class name to enable dark mode in our application
@custom-variant dark (&:where(.dark-theme, .dark-theme *));

// `inline` is needed to use the CSS variables in tailwind's @theme
@theme inline {
  --color-primary: var(--mat-sys-primary);
  --color-on-primary: var(--mat-sys-on-primary);
  --color-primary-container: var(--mat-sys-primary-container);
  --color-on-primary-container: var(--mat-sys-on-primary-container);
  --color-secondary: var(--mat-sys-secondary);
  --color-on-secondary: var(--mat-sys-on-secondary);
  --color-secondary-container: var(--mat-sys-secondary-container);
  --color-on-secondary-container: var(--mat-sys-on-secondary-container);
  --color-tertiary: var(--mat-sys-tertiary);
  --color-on-tertiary: var(--mat-sys-on-tertiary);
  --color-tertiary-container: var(--mat-sys-tertiary-container);
  --color-on-tertiary-container: var(--mat-sys-on-tertiary-container);
  --color-error: var(--mat-sys-error);
  --color-on-error: var(--mat-sys-on-error);
  --color-error-container: var(--mat-sys-error-container);
  --color-on-error-container: var(--mat-sys-on-error-container);
  --color-outline: var(--mat-sys-outline);
  --color-outline-variant: var(--mat-sys-outline-variant);
  --color-surface: var(--mat-sys-surface);
  --color-surface-container-highest: var(--mat-sys-surface-container-highest);
  --color-surface-container-high: var(--mat-sys-surface-container-high);
  --color-surface-container-medium: var(--mat-sys-surface-container-medium);
  --color-surface-container-low: var(--mat-sys-surface-container-low);
  --color-surface-container-lowest: var(--mat-sys-surface-container-lowest);
  --color-surface-container: var(--mat-sys-surface-container);
  --color-surface-variant: var(--mat-sys-surface-variant);
  --color-on-surface-variant: var(--mat-sys-on-surface-variant);
  --color-on-surface: var(--mat-sys-on-surface);

  // same as `plain-family` in angular material
  --font-sans: var(--mat-sys-body-large-font), sans-serif;
}

// #region: Tailwind X Angular Material fix
.mdc-notched-outline__notch {
  border-style: none;
}
.mat-mdc-icon-button {
  line-height: 1;
}
// #endregion
```
