---
title: CSS Custom Properties (Variables)
category: Modern CSS
order: 2
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Custom Properties (Variables)

> **Quick Summary:** CSS custom properties (variables) let you store and reuse values throughout your stylesheet. Defined with `--variable-name` and accessed with `var(--variable-name)`. Perfect for theming, consistent spacing, and dynamic updates via JavaScript.

## Table of Contents
- [Introduction](#introduction)
- [Defining Variables](#defining-variables)
- [Using Variables](#using-variables)
- [Scope and Inheritance](#scope-and-inheritance)
- [Fallback Values](#fallback-values)
- [Common Use Cases](#common-use-cases)
- [Theming with Variables](#theming-with-variables)
- [JavaScript Integration](#javascript-integration)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**CSS custom properties** (also called CSS variables) allow you to define reusable values that can be referenced throughout your stylesheet.

**Benefits:**
- ✅ **DRY principle:** Define once, use everywhere
- ✅ **Easy maintenance:** Change one value, updates everywhere
- ✅ **Dynamic:** Can be changed via JavaScript
- ✅ **Scoped:** Can have different values in different contexts
- ✅ **Inheritance:** Child elements inherit parent variables

**Syntax:**
```css
/* Define */
--variable-name: value;

/* Use */
property: var(--variable-name);
```

---

## Defining Variables

### Global Variables (:root)

```css
:root {
  --primary-color: #007bff;
  --secondary-color: #6c757d;
  --font-size-base: 16px;
  --spacing-unit: 8px;
}
```

**`:root` = global scope.** Variables defined here are available everywhere.

---

### Local Variables (Scoped)

```css
.card {
  --card-bg: white;
  --card-padding: 20px;
  background: var(--card-bg);
  padding: var(--card-padding);
}

.card-dark {
  --card-bg: #333;
  --card-color: white;
}
```

**Scope:** Variables are only available within the element (and its children) where they're defined.

---

### Naming Convention

```css
:root {
  /* Colors */
  --color-primary: #007bff;
  --color-secondary: #6c757d;
  --color-success: #28a745;
  --color-danger: #dc3545;

  /* Spacing */
  --spacing-xs: 4px;
  --spacing-sm: 8px;
  --spacing-md: 16px;
  --spacing-lg: 24px;
  --spacing-xl: 32px;

  /* Typography */
  --font-family-base: 'Helvetica Neue', Arial, sans-serif;
  --font-size-sm: 14px;
  --font-size-base: 16px;
  --font-size-lg: 18px;

  /* Shadows */
  --shadow-sm: 0 1px 3px rgba(0,0,0,0.1);
  --shadow-md: 0 4px 6px rgba(0,0,0,0.1);
  --shadow-lg: 0 10px 15px rgba(0,0,0,0.2);
}
```

**Best practice:** Use descriptive, hierarchical names with `--` prefix.

---

## Using Variables

### Basic Usage

```css
:root {
  --primary-color: #007bff;
}

button {
  background: var(--primary-color);
  color: white;
}

a {
  color: var(--primary-color);
}
```

---

### Multiple Variables

```css
:root {
  --spacing: 16px;
  --border-radius: 8px;
  --transition-speed: 0.3s;
}

.card {
  padding: var(--spacing);
  border-radius: var(--border-radius);
  transition: all var(--transition-speed);
}
```

---

### Calculated Values

```css
:root {
  --spacing-unit: 8px;
}

.container {
  padding: calc(var(--spacing-unit) * 2); /* 16px */
  margin: calc(var(--spacing-unit) * 4); /* 32px */
}
```

---

## Scope and Inheritance

### How Inheritance Works

```css
:root {
  --color: blue;
}

.parent {
  --color: red;
}

.child {
  color: var(--color); /* Inherits from .parent = red */
}
```

**HTML:**
```html
<div class="parent">
  <div class="child">This text is red</div>
</div>

<div class="child">This text is blue (from :root)</div>
```

---

### Overriding Variables

```css
:root {
  --button-bg: #007bff;
}

.button {
  background: var(--button-bg);
}

/* Override for specific context */
.dark-theme {
  --button-bg: #0056b3;
}
```

**HTML:**
```html
<button class="button">Blue button</button>

<div class="dark-theme">
  <button class="button">Darker blue button</button>
</div>
```

---

## Fallback Values

### Default Fallback

```css
.element {
  /* If --custom-color is undefined, use blue */
  color: var(--custom-color, blue);
}
```

---

### Nested Fallbacks

```css
.element {
  /* Try --color-primary, then --color-default, then blue */
  color: var(--color-primary, var(--color-default, blue));
}
```

---

### Fallback for Calculations

```css
:root {
  --spacing: 16px;
}

.element {
  padding: var(--spacing, 20px); /* Fallback to 20px if undefined */
  margin: calc(var(--spacing, 10px) * 2); /* Fallback in calc() */
}
```

---

## Common Use Cases

### 1. Color Schemes

```css
:root {
  --color-primary: #007bff;
  --color-primary-light: #4da3ff;
  --color-primary-dark: #0056b3;

  --color-gray-100: #f8f9fa;
  --color-gray-200: #e9ecef;
  --color-gray-300: #dee2e6;
  --color-gray-400: #ced4da;
  --color-gray-500: #adb5bd;

  --color-text: #212529;
  --color-text-muted: #6c757d;
}

body {
  color: var(--color-text);
}

.muted {
  color: var(--color-text-muted);
}
```

---

### 2. Consistent Spacing

```css
:root {
  --spacing-1: 4px;
  --spacing-2: 8px;
  --spacing-3: 12px;
  --spacing-4: 16px;
  --spacing-5: 20px;
}

.card {
  padding: var(--spacing-4);
  margin-bottom: var(--spacing-3);
}

.button {
  padding: var(--spacing-2) var(--spacing-4);
}
```

---

### 3. Typography Scale

```css
:root {
  --font-size-xs: 12px;
  --font-size-sm: 14px;
  --font-size-base: 16px;
  --font-size-lg: 18px;
  --font-size-xl: 20px;
  --font-size-2xl: 24px;
  --font-size-3xl: 30px;

  --line-height-tight: 1.25;
  --line-height-normal: 1.5;
  --line-height-loose: 1.75;
}

body {
  font-size: var(--font-size-base);
  line-height: var(--line-height-normal);
}

h1 {
  font-size: var(--font-size-3xl);
  line-height: var(--line-height-tight);
}
```

---

### 4. Component Variants

```css
.button {
  --button-bg: var(--color-primary);
  --button-color: white;
  --button-padding: 10px 20px;

  background: var(--button-bg);
  color: var(--button-color);
  padding: var(--button-padding);
}

.button-large {
  --button-padding: 15px 30px;
  --button-font-size: 18px;
}

.button-danger {
  --button-bg: var(--color-danger);
}
```

---

## Theming with Variables

### Light/Dark Theme

```css
/* Default: Light theme */
:root {
  --bg-color: white;
  --text-color: #333;
  --border-color: #ddd;
}

/* Dark theme */
[data-theme="dark"] {
  --bg-color: #1a1a1a;
  --text-color: #f0f0f0;
  --border-color: #444;
}

body {
  background: var(--bg-color);
  color: var(--text-color);
}

.card {
  border: 1px solid var(--border-color);
}
```

**HTML:**
```html
<body data-theme="dark">
  <div class="card">Dark themed card</div>
</body>
```

---

### Multiple Theme Support

```css
:root {
  --theme-bg: white;
  --theme-text: black;
}

[data-theme="ocean"] {
  --theme-bg: #006994;
  --theme-text: #e0f7fa;
}

[data-theme="forest"] {
  --theme-bg: #2d5016;
  --theme-text: #c8e6c9;
}

[data-theme="sunset"] {
  --theme-bg: #ff6f00;
  --theme-text: #fff3e0;
}

body {
  background: var(--theme-bg);
  color: var(--theme-text);
}
```

---

## JavaScript Integration

### Reading Variables

```javascript
// Get computed value of a variable
const root = document.documentElement;
const primaryColor = getComputedStyle(root)
  .getPropertyValue('--primary-color');

console.log(primaryColor); // "#007bff"
```

---

### Setting Variables

```javascript
// Set a variable value
const root = document.documentElement;
root.style.setProperty('--primary-color', '#ff0000');
```

---

### Theme Switcher

```javascript
// Toggle between light and dark theme
const themeToggle = document.getElementById('theme-toggle');

themeToggle.addEventListener('click', () => {
  const currentTheme = document.body.dataset.theme;
  const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
  document.body.dataset.theme = newTheme;
});
```

**CSS:**
```css
:root {
  --bg: white;
  --text: black;
}

[data-theme="dark"] {
  --bg: #1a1a1a;
  --text: white;
}

body {
  background: var(--bg);
  color: var(--text);
  transition: background 0.3s, color 0.3s;
}
```

---

## Examples

### Example 1: Design System

```css
:root {
  /* Colors */
  --primary-50: #e3f2fd;
  --primary-100: #bbdefb;
  --primary-500: #2196f3;
  --primary-700: #1976d2;
  --primary-900: #0d47a1;

  /* Spacing scale (8px base) */
  --space-1: 8px;
  --space-2: 16px;
  --space-3: 24px;
  --space-4: 32px;
  --space-5: 40px;

  /* Typography */
  --font-sans: 'Inter', system-ui, sans-serif;
  --font-mono: 'Fira Code', monospace;

  --text-xs: 0.75rem;
  --text-sm: 0.875rem;
  --text-base: 1rem;
  --text-lg: 1.125rem;
  --text-xl: 1.25rem;

  /* Borders */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-full: 9999px;

  /* Shadows */
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
  --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
}

/* Usage */
.button {
  background: var(--primary-500);
  padding: var(--space-2) var(--space-3);
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-sm);
  font-family: var(--font-sans);
  font-size: var(--text-base);
}
```

---

### Example 2: Responsive Spacing

```css
:root {
  --container-padding: 16px;
}

@media (min-width: 768px) {
  :root {
    --container-padding: 32px;
  }
}

@media (min-width: 1024px) {
  :root {
    --container-padding: 48px;
  }
}

.container {
  padding: var(--container-padding);
}
```

---

### Example 3: Component Library

```css
:root {
  --button-primary-bg: #007bff;
  --button-primary-hover: #0056b3;
  --button-primary-active: #004085;

  --button-secondary-bg: #6c757d;
  --button-secondary-hover: #5a6268;

  --button-padding-sm: 6px 12px;
  --button-padding-md: 10px 20px;
  --button-padding-lg: 14px 28px;
}

.btn {
  padding: var(--button-padding-md);
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background 0.2s;
}

.btn-primary {
  background: var(--button-primary-bg);
  color: white;
}

.btn-primary:hover {
  background: var(--button-primary-hover);
}

.btn-primary:active {
  background: var(--button-primary-active);
}

.btn-sm {
  padding: var(--button-padding-sm);
}

.btn-lg {
  padding: var(--button-padding-lg);
}
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| Custom properties | 49+ | 31+ | 9.1+ | 15+ |
| `var()` function | 49+ | 31+ | 9.1+ | 15+ |

**Support:** Excellent (95%+).

---

## Best Practices

### ✅ Do This

1. **Use :root for global variables**
   ```css
   :root {
     --primary-color: #007bff;
   }
   ```

2. **Name variables descriptively**
   ```css
   /* Good */
   --color-primary: blue;
   --spacing-large: 32px;

   /* Bad */
   --c1: blue;
   --x: 32px;
   ```

3. **Provide fallback values**
   ```css
   color: var(--custom-color, #333);
   ```

4. **Group related variables**
   ```css
   :root {
     /* Colors */
     --color-primary: #007bff;
     --color-secondary: #6c757d;

     /* Spacing */
     --spacing-sm: 8px;
     --spacing-md: 16px;
   }
   ```

5. **Use for theming**
   ```css
   [data-theme="dark"] {
     --bg: #1a1a1a;
     --text: white;
   }
   ```

---

### ❌ Avoid This

1. **Don't use variables for everything**
   ```css
   /* Overkill */
   --display-block: block;
   div { display: var(--display-block); }
   ```

2. **Don't mix naming conventions**
   ```css
   /* Inconsistent */
   --primaryColor: blue;
   --secondary_color: red;
   --TertiaryColor: green;
   ```

3. **Don't forget browser support**
   ```css
   /* No fallback for old browsers */
   color: var(--color); /* IE11 gets nothing */

   /* Better */
   color: #007bff; /* Fallback */
   color: var(--color, #007bff);
   ```

4. **Don't redefine too many variables**
   ```css
   /* Hard to track */
   :root { --color: blue; }
   .section1 { --color: red; }
   .section2 { --color: green; }
   .section3 { --color: yellow; }
   ```

---

## Related Topics

**Prerequisites:**
- [CSS Fundamentals](../01-fundamentals/syntax.md)

**Next Steps:**
- [At-Rules](at-rules.md)
- [CSS Functions](css-functions.md)

**Related:**
- [Theming Strategies](../09-visual-effects/filters.md)

---

## Practice Exercise

Create a theme switcher with variables:
- Define light/dark theme color palettes
- Create toggle button
- Use JavaScript to switch `data-theme` attribute
- Apply smooth transitions between themes
- Include at least 5 variables (bg, text, border, button-bg, link)

---

## Navigation

**Previous:** [← CSS Functions](css-functions.md)
**Next:** [At-Rules →](at-rules.md)
**Up:** [↑ Back to Modern CSS](../README.md#1️⃣3️⃣-modern-css-5-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Modern CSS
**Difficulty:** Intermediate
