---
title: CSS Variables (Custom Properties)
category: Modern CSS
order: 1
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Variables (Custom Properties)

> **Quick Summary:** CSS Variables (officially called Custom Properties) let you store values that can be reused throughout your stylesheets. They make theming, maintenance, and dynamic styling simple—change one variable, update the entire site.

## Table of Contents
- [Introduction](#introduction)
- [Why CSS Variables Matter](#why-css-variables-matter)
- [Basic Syntax](#basic-syntax)
- [Scope and Inheritance](#scope-and-inheritance)
- [Fallback Values](#fallback-values)
- [JavaScript Integration](#javascript-integration)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

Before CSS Variables, managing consistent values across a stylesheet was painful. Change your brand color from blue to green? Find and replace dozens (or hundreds) of instances. Create a dark mode? Duplicate your entire stylesheet. Dynamic styling? Use JavaScript to inject inline styles (messy).

CSS Variables revolutionized this. **They're reusable values stored once and referenced many times.** Define `--brand-primary: #3498db` in one place, use it everywhere. Update it once, see changes site-wide. They're inheritance-aware (children inherit parent variables), JavaScript-accessible (change values dynamically), and scoped (global or local).

CSS Variables enable powerful patterns: **theming** (light/dark modes with one toggle), **design systems** (consistent spacing, colors, typography), **dynamic styling** (change values with JavaScript), and **maintainability** (centralized values). They're the bridge between static CSS and dynamic applications, bringing programming-like variable power to stylesheets.

**Key Concept:** CSS Variables are not like Sass/Less variables. CSS Variables are **live**—change them at runtime, they update immediately. Sass variables are compiled away; CSS variables persist in the browser.

---

## Why CSS Variables Matter

### 1. **Maintainability**

**Without variables:**
```css
.header { background-color: #3498db; }
.button { background-color: #3498db; }
.link { color: #3498db; }
.card-border { border-color: #3498db; }
/* ...200 more instances */

/* Change brand color? Edit 200+ places  */
```

**With variables:**
```css
:root {
  --brand-primary: #3498db;
}

.header { background-color: var(--brand-primary); }
.button { background-color: var(--brand-primary); }
.link { color: var(--brand-primary); }
.card-border { border-color: var(--brand-primary); }
/* ...200 more instances */

/* Change brand color? Edit 1 place */
:root {
  --brand-primary: #2ecc71; /* Everything updates */
}
```

---

### 2. **Theming (Light/Dark Modes)**

```css
/* Light mode */
:root {
  --bg-color: #ffffff;
  --text-color: #333333;
}

/* Dark mode */
.dark-mode {
  --bg-color: #1a1a1a;
  --text-color: #e0e0e0;
}

/* Everything uses variables */
body {
  background-color: var(--bg-color);
  color: var(--text-color);
}
```

**Toggle dark mode with JavaScript:**
```javascript
document.body.classList.toggle('dark-mode'); /* That's it! */
```

---

### 3. **JavaScript Integration**

**Get variable value:**
```javascript
const root = document.documentElement;
const primaryColor = getComputedStyle(root).getPropertyValue('--brand-primary');
console.log(primaryColor); // "#3498db"
```

**Set variable value:**
```javascript
root.style.setProperty('--brand-primary', '#e74c3c');
/* Entire site updates instantly */
```

---

### 4. **Responsive Design**

**Change variables at different breakpoints:**
```css
:root {
  --spacing: 10px;
  --font-size: 14px;
}

@media (min-width: 768px) {
  :root {
    --spacing: 20px;
    --font-size: 16px;
  }
}

@media (min-width: 1024px) {
  :root {
    --spacing: 30px;
    --font-size: 18px;
  }
}

/* Use variables everywhere */
.container {
  padding: var(--spacing);
}

body {
  font-size: var(--font-size);
}
```

---

### 5. **Career Relevance**
- **Modern standard:** All new projects use CSS Variables
- **Framework requirement:** React, Vue, Angular integrate with CSS Variables
- **Interview question:** "How would you implement theming?" → CSS Variables
- **Portfolio showcase:** Demonstrates modern CSS knowledge

---

## Basic Syntax

### Declaring Variables

**Global scope (`:root`):**
```css
:root {
  --variable-name: value;
}
```

**Local scope (any selector):**
```css
.component {
  --local-variable: value;
}
```

### Using Variables

**Syntax:** `var(--variable-name)`

```css
:root {
  --brand-primary: #3498db;
  --spacing-large: 40px;
}

.button {
  background-color: var(--brand-primary);
  padding: var(--spacing-large);
}
```

---

### Naming Conventions

**Best practices:**
```css
:root {
  /* Colors */
  --color-primary: #3498db;
  --color-secondary: #2ecc71;
  --color-danger: #e74c3c;

  /* Spacing */
  --spacing-xs: 5px;
  --spacing-sm: 10px;
  --spacing-md: 20px;
  --spacing-lg: 40px;

  /* Typography */
  --font-family-sans: 'Helvetica Neue', Arial, sans-serif;
  --font-size-base: 16px;
  --font-size-large: 20px;

  /* Breakpoints */
  --breakpoint-tablet: 768px;
  --breakpoint-desktop: 1024px;
}
```

**Rules:**
- Start with `--` (required)
- Use kebab-case (`--my-variable`, not `--myVariable`)
- Be descriptive (`--color-primary`, not `--c1`)
- Group by category (colors, spacing, typography)

---

## Scope and Inheritance

### Global Scope (`:root`)

Variables defined on `:root` are available everywhere.

```css
:root {
  --brand-primary: #3498db;
}

/* Available anywhere */
.header { background-color: var(--brand-primary); }
.footer { background-color: var(--brand-primary); }
```

**Note:** `:root` is the `<html>` element with higher specificity.

---

### Local Scope

Variables defined on a selector are available only to that selector and its children.

```css
.card {
  --card-bg: #f5f5f5;
}

.card {
  background-color: var(--card-bg); /* Works */
}

.card-header {
  background-color: var(--card-bg); /* Works (inherited from parent) */
}

.footer {
  background-color: var(--card-bg); /* Doesn't work (not a child of .card) */
}
```

---

### Inheritance

**Children inherit parent variables:**

```css
.parent {
  --text-color: blue;
}

.child {
  color: var(--text-color); /* Inherits blue from .parent */
}
```

**Override in children:**

```css
.parent {
  --text-color: blue;
}

.child {
  --text-color: red; /* Override for this child only */
  color: var(--text-color); /* Uses red */
}
```

---

## Fallback Values

**Syntax:** `var(--variable-name, fallback-value)`

```css
.element {
  /* If --brand-primary doesn't exist, use #3498db */
  color: var(--brand-primary, #3498db);
}
```

### Nested Fallbacks

```css
.element {
  /* Try --primary, then --secondary, then #000 */
  color: var(--primary, var(--secondary, #000));
}
```

### Use Cases

**Providing defaults:**
```css
:root {
  --spacing: 20px;
}

.element {
  /* Use custom spacing if set, otherwise default to 20px */
  padding: var(--custom-spacing, var(--spacing));
}
```

---

## JavaScript Integration

### Reading Variables

```javascript
// Get :root (html element)
const root = document.documentElement;

// Read variable value
const primaryColor = getComputedStyle(root).getPropertyValue('--brand-primary');
console.log(primaryColor); // " #3498db" (note: may have leading space)

// Clean up value
const cleanColor = primaryColor.trim();
```

---

### Setting Variables

```javascript
// Set global variable
document.documentElement.style.setProperty('--brand-primary', '#e74c3c');

// Set variable on specific element
const card = document.querySelector('.card');
card.style.setProperty('--card-bg', '#ffffff');
```

---

### Dynamic Theming

```javascript
// Toggle dark mode
const toggleTheme = () => {
  const root = document.documentElement;
  const isDark = root.classList.contains('dark-mode');

  if (isDark) {
    root.style.setProperty('--bg-color', '#ffffff');
    root.style.setProperty('--text-color', '#333333');
    root.classList.remove('dark-mode');
  } else {
    root.style.setProperty('--bg-color', '#1a1a1a');
    root.style.setProperty('--text-color', '#e0e0e0');
    root.classList.add('dark-mode');
  }
};
```

---

### User Customization

```javascript
// Let users choose accent color
const colorPicker = document.querySelector('#color-picker');

colorPicker.addEventListener('change', (e) => {
  document.documentElement.style.setProperty('--accent-color', e.target.value);
});
```

```html
<input type="color" id="color-picker" value="#3498db">
```

---

## Examples

### Example 1: Color System

```css
:root {
  /* Brand colors */
  --color-primary: #3498db;
  --color-secondary: #2ecc71;
  --color-danger: #e74c3c;
  --color-warning: #f39c12;
  --color-info: #3498db;
  --color-success: #2ecc71;

  /* Neutral colors */
  --color-black: #000000;
  --color-white: #ffffff;
  --color-gray-100: #f5f5f5;
  --color-gray-300: #d1d1d1;
  --color-gray-500: #9e9e9e;
  --color-gray-700: #616161;
  --color-gray-900: #212121;

  /* Semantic colors */
  --color-text: var(--color-gray-900);
  --color-bg: var(--color-white);
  --color-border: var(--color-gray-300);
}

/* Usage */
body {
  color: var(--color-text);
  background-color: var(--color-bg);
}

.button-primary {
  background-color: var(--color-primary);
  color: var(--color-white);
}

.alert-danger {
  background-color: var(--color-danger);
  color: var(--color-white);
}
```

---

### Example 2: Spacing System

```css
:root {
  /* Spacing scale */
  --spacing-xs: 4px;
  --spacing-sm: 8px;
  --spacing-md: 16px;
  --spacing-lg: 24px;
  --spacing-xl: 32px;
  --spacing-xxl: 48px;
}

/* Usage */
.container {
  padding: var(--spacing-lg);
}

.button {
  padding: var(--spacing-sm) var(--spacing-md);
}

.section {
  margin-bottom: var(--spacing-xxl);
}
```

---

### Example 3: Dark Mode Theme

```css
/* Light mode (default) */
:root {
  --bg-primary: #ffffff;
  --bg-secondary: #f5f5f5;
  --text-primary: #333333;
  --text-secondary: #666666;
  --border-color: #e0e0e0;
}

/* Dark mode */
.dark-mode {
  --bg-primary: #1a1a1a;
  --bg-secondary: #2a2a2a;
  --text-primary: #e0e0e0;
  --text-secondary: #b0b0b0;
  --border-color: #404040;
}

/* Components use variables */
body {
  background-color: var(--bg-primary);
  color: var(--text-primary);
}

.card {
  background-color: var(--bg-secondary);
  border: 1px solid var(--border-color);
}

.card-text {
  color: var(--text-secondary);
}
```

```javascript
// Toggle with button
document.querySelector('#theme-toggle').addEventListener('click', () => {
  document.body.classList.toggle('dark-mode');
});
```

---

### Example 4: Component Variants

```css
:root {
  --button-bg: #3498db;
  --button-text: #ffffff;
  --button-padding: 12px 24px;
}

.button {
  background-color: var(--button-bg);
  color: var(--button-text);
  padding: var(--button-padding);
  border: none;
  border-radius: 4px;
}

/* Large variant */
.button-large {
  --button-padding: 16px 32px;
  font-size: 18px;
}

/* Danger variant */
.button-danger {
  --button-bg: #e74c3c;
}

/* Success variant */
.button-success {
  --button-bg: #2ecc71;
}
```

---

## Common Use Cases

### Use Case 1: Design System

```css
:root {
  /* Colors */
  --color-primary: #3498db;
  --color-secondary: #2ecc71;

  /* Typography */
  --font-family-base: 'Inter', sans-serif;
  --font-size-base: 16px;
  --line-height-base: 1.5;

  /* Spacing */
  --spacing-unit: 8px;

  /* Borders */
  --border-radius: 4px;
  --border-width: 1px;

  /* Shadows */
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.1);
  --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);

  /* Transitions */
  --transition-speed: 0.3s;
  --transition-easing: ease-in-out;
}
```

---

### Use Case 2: Responsive Sizing

```css
:root {
  --container-width: 100%;
  --font-size: 14px;
  --spacing: 10px;
}

@media (min-width: 768px) {
  :root {
    --container-width: 750px;
    --font-size: 16px;
    --spacing: 20px;
  }
}

@media (min-width: 1024px) {
  :root {
    --container-width: 1000px;
    --font-size: 18px;
    --spacing: 30px;
  }
}

.container {
  max-width: var(--container-width);
  padding: var(--spacing);
}

body {
  font-size: var(--font-size);
}
```

---

### Use Case 3: Component Theming

```css
.card {
  --card-bg: #ffffff;
  --card-text: #333333;
  --card-border: #e0e0e0;

  background-color: var(--card-bg);
  color: var(--card-text);
  border: 1px solid var(--card-border);
}

/* Themed variants */
.card-primary {
  --card-bg: #3498db;
  --card-text: #ffffff;
  --card-border: #2980b9;
}

.card-danger {
  --card-bg: #e74c3c;
  --card-text: #ffffff;
  --card-border: #c0392b;
}
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|----|
| CSS Variables | 49+ | 31+ | 9.1+ | 15+ | |
| `var()` | 49+ | 31+ | 9.1+ | 15+ | |
| JavaScript access | 49+ | 31+ | 9.1+ | 15+ | |

**Key Takeaway:** CSS Variables work in all modern browsers. IE11 doesn't support them (use fallbacks or Sass variables for legacy support).

---

## Best Practices

### Do This

1. **Define Variables Globally in `:root`**
   ```css
   :root {
     --brand-primary: #3498db;
     --spacing-md: 20px;
   }
   ```

2. **Use Semantic Names**
   ```css
   /* Good - describes purpose */
   --color-primary: #3498db;
   --spacing-large: 40px;

   /* Bad - describes value */
   --blue: #3498db;
   --forty-pixels: 40px;
   ```

3. **Group Related Variables**
   ```css
   :root {
     /* Colors */
     --color-primary: #3498db;
     --color-secondary: #2ecc71;

     /* Spacing */
     --spacing-sm: 10px;
     --spacing-md: 20px;
   }
   ```

4. **Provide Fallbacks**
   ```css
   .element {
     color: var(--text-color, #333); /* Fallback to #333 */
   }
   ```

5. **Use Variables for Repeated Values**
   ```css
   /* If a value appears 3+ times, make it a variable */
   :root {
     --transition-speed: 0.3s;
   }

   .button,
   .link,
   .card {
     transition: all var(--transition-speed);
   }
   ```

---

### Avoid This

1. **Don't Hardcode Values That Could Be Variables**
   ```css
   /* Bad */
   .button { background-color: #3498db; }
   .link { color: #3498db; }

   /* Good */
   :root { --color-primary: #3498db; }
   .button { background-color: var(--color-primary); }
   .link { color: var(--color-primary); }
   ```

2. **Don't Name Variables After Their Values**
   ```css
   /* Bad */
   --blue-500: #3498db;

   /* Good */
   --color-primary: #3498db;
   ```

3. **Don't Overuse Variables**
   ```css
   /* Bad - overkill */
   --button-border-top-left-radius: 4px;

   /* Good - reasonable */
   --border-radius: 4px;
   ```

---

## Video Tutorial

**Watch CSS Variables:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=12000s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=12000s)

**Timestamps:**
- `3:20:00` - Introduction to CSS Variables
- `3:28:00` - Variable syntax and usage
- `3:38:00` - Scope and inheritance
- `3:48:00` - JavaScript integration
- `3:58:00` - Building a theme switcher

**Resources:**
- [W3Schools - CSS Variables](https://www.w3schools.com/css/css3_variables.asp)
- [MDN - CSS Variables](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- [CSS Variables Guide](https://css-tricks.com/a-complete-guide-to-custom-properties/)

---

## Related Topics

**Prerequisites:**
- [CSS Introduction](../01-fundamentals/introduction.md)
- [CSS Colors](../02-colors/colors-overview.md)

**Related:**
- [CSS Functions](css-functions.md)
- [Media Queries](../12-responsive-design/media-queries.md)
- [Responsive Design](../12-responsive-design/rwd-intro.md)

---

## Practice Exercise

### Challenge: Build a Theme Switcher

**Objective:** Create a website with light/dark mode toggle using CSS Variables.

**Requirements:**
- [ ] Define color variables for light mode
- [ ] Create dark mode with overridden variables
- [ ] Add toggle button with JavaScript
- [ ] Use variables for spacing and typography
- [ ] **Bonus:** Save theme preference to localStorage

---

### Starter Code

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Theme Switcher</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header>
    <h1>Theme Switcher Demo</h1>
    <button id="theme-toggle">Toggle Dark Mode</button>
  </header>

  <main>
    <section class="card">
      <h2>Card Title</h2>
      <p>This card adapts to light and dark themes using CSS Variables.</p>
    </section>
  </main>

  <script src="script.js"></script>
</body>
</html>
```

**CSS (Complete this):**
```css
/* Your CSS Variables here */
```

**JavaScript (Complete this):**
```javascript
/* Your theme toggle logic here */
```

---

### Solution

<details>
<summary>Click to reveal solution</summary>

**CSS:**
```css
/* Light mode (default) */
:root {
  --bg-primary: #ffffff;
  --bg-secondary: #f5f5f5;
  --text-primary: #333333;
  --text-secondary: #666666;
  --border-color: #e0e0e0;
  --button-bg: #3498db;
  --button-text: #ffffff;

  --spacing-sm: 10px;
  --spacing-md: 20px;
  --spacing-lg: 40px;

  --border-radius: 8px;
  --transition-speed: 0.3s;
}

/* Dark mode */
.dark-mode {
  --bg-primary: #1a1a1a;
  --bg-secondary: #2a2a2a;
  --text-primary: #e0e0e0;
  --text-secondary: #b0b0b0;
  --border-color: #404040;
  --button-bg: #2980b9;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: var(--bg-primary);
  color: var(--text-primary);
  font-family: Arial, sans-serif;
  transition: background-color var(--transition-speed),
              color var(--transition-speed);
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: var(--spacing-md) var(--spacing-lg);
  background-color: var(--bg-secondary);
  border-bottom: 1px solid var(--border-color);
}

#theme-toggle {
  background-color: var(--button-bg);
  color: var(--button-text);
  border: none;
  padding: var(--spacing-sm) var(--spacing-md);
  border-radius: var(--border-radius);
  cursor: pointer;
  transition: opacity var(--transition-speed);
}

#theme-toggle:hover {
  opacity: 0.8;
}

main {
  padding: var(--spacing-lg);
}

.card {
  background-color: var(--bg-secondary);
  padding: var(--spacing-md);
  border-radius: var(--border-radius);
  border: 1px solid var(--border-color);
  transition: background-color var(--transition-speed),
              border-color var(--transition-speed);
}

.card h2 {
  margin-bottom: var(--spacing-sm);
}

.card p {
  color: var(--text-secondary);
  line-height: 1.6;
}
```

**JavaScript:**
```javascript
const themeToggle = document.getElementById('theme-toggle');
const body = document.body;

// Check for saved theme preference or default to light mode
const currentTheme = localStorage.getItem('theme') || 'light';
if (currentTheme === 'dark') {
  body.classList.add('dark-mode');
  themeToggle.textContent = 'Toggle Light Mode';
}

// Toggle theme
themeToggle.addEventListener('click', () => {
  body.classList.toggle('dark-mode');

  // Update button text
  if (body.classList.contains('dark-mode')) {
    themeToggle.textContent = 'Toggle Light Mode';
    localStorage.setItem('theme', 'dark');
  } else {
    themeToggle.textContent = 'Toggle Dark Mode';
    localStorage.setItem('theme', 'light');
  }
});
```

**How it works:**
1. **CSS Variables** define colors for light mode in `:root`
2. **`.dark-mode` class** overrides variables for dark theme
3. **JavaScript** toggles the `dark-mode` class on `<body>`
4. **localStorage** persists user's theme choice
5. **CSS transitions** create smooth theme switching

</details>

---

**Last Updated:** November 15, 2025
**Category:** Modern CSS
**Difficulty:** Intermediate
