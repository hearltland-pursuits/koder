---
title: CSS Functions
category: Modern CSS
order: 2
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Functions

> **Quick Summary:** CSS functions perform calculations and transformations in stylesheets. Essential functions: `calc()` for math, `clamp()` for responsive sizing, `min()`/`max()` for constraints, `var()` for custom properties, and color functions like `rgb()` and `hsl()`.

## Table of Contents
- [Introduction](#introduction)
- [calc()](#calc)
- [min() and max()](#min-and-max)
- [clamp()](#clamp)
- [var()](#var)
- [Color Functions](#color-functions)
- [Transform Functions](#transform-functions)
- [Filter Functions](#filter-functions)
- [Other Useful Functions](#other-useful-functions)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**CSS functions** are built-in operations that perform calculations, transformations, or return values. They make CSS more dynamic and reduce the need for hardcoded values.

**Common categories:**
- **Math:** `calc()`, `min()`, `max()`, `clamp()`
- **Custom Properties:** `var()`
- **Colors:** `rgb()`, `hsl()`, `color-mix()`
- **Transforms:** `translate()`, `rotate()`, `scale()`
- **Filters:** `blur()`, `brightness()`, `contrast()`

---

## calc()

**Perform mathematical calculations** mixing different units.

### Syntax

```css
property: calc(expression);
```

### Basic Operations

```css
/* Addition */
width: calc(100% - 80px);

/* Subtraction */
width: calc(100vw - 40px);

/* Multiplication */
width: calc(100% * 0.5);

/* Division */
width: calc(100% / 3);

/* Complex expression */
width: calc((100% - 60px) / 4);
```

### Common Use Cases

```css
/* Perfect centering with offset */
.sidebar {
  width: 250px;
  margin-left: calc(50% - 125px);
}

/* Full width minus padding */
.container {
  width: calc(100% - 40px);
  padding: 20px;
}

/* Column gaps in percentage layouts */
.col {
  width: calc(33.333% - 20px); /* 1/3 width minus gap */
}

/* Responsive font size */
font-size: calc(16px + 0.5vw);

/* Dynamic spacing */
margin-top: calc(var(--base-spacing) * 2);
```

### Rules

- **Spaces required** around `+` and `-`:
  ```css
  calc(100% - 20px)  /* Correct */
  calc(100%-20px)    /* X Invalid */
  ```

- **Spaces optional** for `*` and `/`:
  ```css
  calc(100%/2)  /* Valid */
  calc(100% / 2)  /* Also valid */
  ```

- **Can nest** calc expressions:
  ```css
  width: calc(calc(100% / 3) - 20px);
  ```

---

## min() and max()

**Choose smallest or largest value** from a list.

### min()

**Returns the smallest value.**

```css
/* Never exceeds 600px */
width: min(100%, 600px);

/* Responsive with max constraint */
font-size: min(5vw, 32px);

/* Multiple values */
width: min(50%, 300px, 100vw - 40px);
```

**Use case:** Setting maximum limits.

### max()

**Returns the largest value.**

```css
/* Never goes below 16px */
font-size: max(16px, 1vw);

/* Minimum width */
width: max(200px, 20%);

/* Multiple values */
padding: max(20px, 2vw, 1rem);
```

**Use case:** Setting minimum limits.

### Practical Examples

```css
/* Responsive padding (min 20px, max 5% of width) */
padding: min(5%, 20px);

/* Container width (min 300px, max 90% of viewport) */
.container {
  width: min(90%, 1200px);
  margin: 0 auto;
}

/* Font size (min 14px, responsive with max 24px) */
h1 {
  font-size: max(14px, min(5vw, 24px));
}
```

---

## clamp()

**Constrains value between minimum and maximum.**

### Syntax

```css
property: clamp(minimum, preferred, maximum);
```

### Fluid Typography

```css
/* Font size between 16px and 48px, scales with viewport */
h1 {
  font-size: clamp(16px, 5vw, 48px);
}

/* Explanation:
   - Mobile (small viewport): stays at 16px
   - Grows with viewport: uses 5vw
   - Large screens: caps at 48px
*/
```

### Responsive Spacing

```css
/* Padding scales from 10px to 40px */
.container {
  padding: clamp(10px, 3vw, 40px);
}

/* Gap scales from 15px to 60px */
.grid {
  gap: clamp(15px, 4vw, 60px);
}
```

### Width Constraints

```css
/* Container between 320px and 1200px */
.wrapper {
  width: clamp(320px, 90%, 1200px);
  margin: 0 auto;
}
```

### vs min/max Comparison

```css
/* These are equivalent: */
clamp(16px, 5vw, 48px)
max(16px, min(5vw, 48px))

/* But clamp() is more readable */
```

---

## var()

**Use CSS custom properties (variables).**

### Basic Usage

```css
:root {
  --primary-color: #007bff;
  --spacing: 20px;
}

.button {
  background: var(--primary-color);
  padding: var(--spacing);
}
```

### Fallback Values

```css
/* Use fallback if variable not defined */
color: var(--text-color, #333);

/* Nested fallbacks */
color: var(--custom-color, var(--default-color, black));
```

### Calculations with Variables

```css
:root {
  --base-size: 16px;
}

h1 {
  font-size: calc(var(--base-size) * 2); /* 32px */
}

h2 {
  font-size: calc(var(--base-size) * 1.5); /* 24px */
}
```

### Dynamic Variables

```css
:root {
  --spacing: 10px;
}

@media (min-width: 768px) {
  :root {
    --spacing: 20px;
  }
}

.container {
  padding: var(--spacing); /* Changes at breakpoint */
}
```

---

## Color Functions

### rgb() and rgba()

```css
/* RGB (Red, Green, Blue) */
color: rgb(255, 0, 0); /* Red */

/* RGBA (with alpha/transparency) */
background: rgba(0, 0, 0, 0.5); /* 50% transparent black */

/* Modern syntax (supports alpha in rgb) */
color: rgb(255 0 0 / 0.5); /* Red at 50% opacity */
```

### hsl() and hsla()

```css
/* HSL (Hue, Saturation, Lightness) */
color: hsl(210, 100%, 50%); /* Blue */

/* HSLA (with alpha) */
background: hsla(210, 100%, 50%, 0.5);

/* Modern syntax */
color: hsl(210 100% 50% / 0.5);
```

### color-mix() (New)

```css
/* Mix two colors */
background: color-mix(in srgb, red, blue);

/* With percentage */
background: color-mix(in srgb, red 75%, blue 25%);
```

---

## Transform Functions

```css
/* Translate (move) */
transform: translate(50px, 100px);
transform: translateX(50px);
transform: translateY(100px);

/* Rotate */
transform: rotate(45deg);

/* Scale */
transform: scale(1.5);
transform: scale(2, 1); /* x, y */

/* Skew */
transform: skew(10deg, 20deg);

/* Multiple transforms */
transform: translate(50px, 0) rotate(45deg) scale(1.2);
```

---

## Filter Functions

```css
/* Blur */
filter: blur(5px);

/* Brightness */
filter: brightness(1.2);

/* Contrast */
filter: contrast(1.5);

/* Grayscale */
filter: grayscale(100%);

/* Hue rotation */
filter: hue-rotate(90deg);

/* Invert */
filter: invert(100%);

/* Saturation */
filter: saturate(1.5);

/* Sepia */
filter: sepia(80%);

/* Drop shadow */
filter: drop-shadow(2px 2px 4px rgba(0,0,0,0.3));

/* Combine multiple */
filter: brightness(1.1) contrast(1.2) saturate(1.3);
```

---

## Other Useful Functions

### url()

```css
background-image: url('photo.jpg');
cursor: url('custom-cursor.png'), pointer;
```

### attr()

```css
/* Use HTML attribute value */
.tooltip::after {
  content: attr(data-tooltip);
}
```

**HTML:**
```html
<span class="tooltip" data-tooltip="Helpful info">Hover me</span>
```

### linear-gradient()

```css
background: linear-gradient(to right, red, blue);
background: linear-gradient(135deg, #667eea, #764ba2);
```

### radial-gradient()

```css
background: radial-gradient(circle, red, blue);
```

---

## Examples

### Example 1: Fluid Typography System

```css
:root {
  --font-size-min: 16px;
  --font-size-max: 24px;
  --font-size-viewport: 2vw;
}

body {
  font-size: clamp(
    var(--font-size-min),
    var(--font-size-viewport),
    var(--font-size-max)
  );
}

h1 {
  font-size: clamp(2rem, 5vw, 4rem);
}

h2 {
  font-size: clamp(1.5rem, 3vw, 2.5rem);
}
```

---

### Example 2: Responsive Spacing System

```css
:root {
  --space-xs: clamp(0.5rem, 1vw, 1rem);
  --space-sm: clamp(1rem, 2vw, 1.5rem);
  --space-md: clamp(1.5rem, 3vw, 2.5rem);
  --space-lg: clamp(2rem, 4vw, 4rem);
  --space-xl: clamp(3rem, 6vw, 6rem);
}

.section {
  padding: var(--space-lg);
}

.card {
  padding: var(--space-md);
  margin-bottom: var(--space-sm);
}
```

---

### Example 3: Dynamic Grid Gaps

```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(300px, 100%), 1fr));
  gap: clamp(1rem, 3vw, 3rem);
}
```

---

### Example 4: Responsive Container

```css
.container {
  width: min(90%, 1200px);
  margin: 0 auto;
  padding: clamp(1rem, 2vw, 2rem);
}
```

---

## Browser Support

| Function | Chrome | Firefox | Safari | Edge |
|----------|--------|---------|--------|------|
| `calc()` | 26+ | 16+ | 7+ | 12+ |
| `min()/max()` | 79+ | 75+ | 11.1+ | 79+ |
| `clamp()` | 79+ | 75+ | 13.1+ | 79+ |
| `var()` | 49+ | 31+ | 9.1+ | 15+ |
| Color functions | All | All | All | All |

**Support:** Excellent (90%+ for modern functions).

---

## Best Practices

### Do This

1. **Use clamp() for fluid sizing**
   ```css
   font-size: clamp(1rem, 2vw, 2rem);
   ```

2. **Combine with CSS variables**
   ```css
   padding: calc(var(--base-spacing) * 2);
   ```

3. **Use min/max for constraints**
   ```css
   width: min(90%, 1200px);
   ```

4. **Add fallbacks for older browsers**
   ```css
   font-size: 24px; /* Fallback */
   font-size: clamp(16px, 3vw, 48px);
   ```

### Avoid This

1. **Don't forget spaces in calc()**
   ```css
   calc(100%-20px)  /* Invalid */
   calc(100% - 20px)  /* Valid */
   ```

2. **Don't overcomplicate expressions**
   ```css
   /* Too complex */
   width: calc(calc(calc(100% / 3) - 10px) * 2);

   /* Simpler */
   width: calc((100% / 3 - 10px) * 2);
   ```

3. **Don't use calc() for simple values**
   ```css
   width: calc(50%);  /* Unnecessary */
   width: 50%;        /* Better */
   ```

---

## Related Topics

**Prerequisites:**
- [CSS Variables](css-variables.md)
- [Units](../03-box-model/units.md)

**Next Steps:**
- [Custom Properties](custom-properties.md)
- [At-Rules](at-rules.md)

---

## Practice Exercise

Create a responsive card component where:
- Font size scales from 14px to 24px
- Padding scales from 1rem to 3rem
- Width is constrained between 300px and 600px
- All values use CSS functions (calc, clamp, min/max)

---

## Navigation

**Previous:** [← CSS Variables](css-variables.md)
**Next:** [Custom Properties →](custom-properties.md)
**Up:** [↑ Back to Modern CSS](../README.md#1️⃣3️⃣-modern-css-6-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Modern CSS
**Difficulty:** Intermediate
