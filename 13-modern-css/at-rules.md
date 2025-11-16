---
title: CSS At-Rules
category: Modern CSS
order: 3
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS At-Rules

> **Quick Summary:** At-rules are CSS statements starting with `@` that control CSS behavior. Common examples: `@media` (responsive design), `@import` (load stylesheets), `@keyframes` (animations), `@font-face` (custom fonts), `@supports` (feature detection).

## Table of Contents
- [Introduction](#introduction)
- [@media](#media)
- [@import](#import)
- [@keyframes](#keyframes)
- [@font-face](#font-face)
- [@supports](#supports)
- [@layer](#layer)
- [@container](#container)
- [Other At-Rules](#other-at-rules)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**At-rules** are special CSS instructions that control how CSS behaves. They all start with `@` followed by a keyword.

**Common at-rules:**
- `@media` - Responsive breakpoints
- `@import` - Load external stylesheets
- `@keyframes` - Define animations
- `@font-face` - Import custom fonts
- `@supports` - Feature detection
- `@layer` - Cascade layers
- `@container` - Container queries

**Syntax:**
```css
@rule-name (parameters) {
  /* CSS rules */
}
```

---

## @media

**Applies styles based on device characteristics** (screen size, orientation, etc.).

### Basic Usage

```css
/* Mobile styles (default) */
body {
  font-size: 14px;
}

/* Tablet and larger */
@media (min-width: 768px) {
  body {
    font-size: 16px;
  }
}

/* Desktop and larger */
@media (min-width: 1024px) {
  body {
    font-size: 18px;
  }
}
```

---

### Media Features

```css
/* Screen width */
@media (min-width: 768px) { }
@media (max-width: 1024px) { }

/* Screen height */
@media (min-height: 600px) { }

/* Orientation */
@media (orientation: portrait) { }
@media (orientation: landscape) { }

/* Resolution (Retina displays) */
@media (min-resolution: 2dppx) { }

/* Hover capability */
@media (hover: hover) {
  .button:hover {
    background: blue;
  }
}

/* Pointer precision */
@media (pointer: coarse) {
  /* Touch devices: Larger buttons */
  button {
    min-height: 44px;
  }
}

/* Preferred color scheme */
@media (prefers-color-scheme: dark) {
  body {
    background: #1a1a1a;
    color: white;
  }
}

/* Reduced motion */
@media (prefers-reduced-motion: reduce) {
  * {
    animation: none !important;
    transition: none !important;
  }
}
```

---

### Logical Operators

```css
/* AND */
@media (min-width: 768px) and (max-width: 1024px) {
  /* Tablet only */
}

/* OR (comma) */
@media (orientation: portrait), (max-width: 600px) {
  /* Portrait OR narrow screen */
}

/* NOT */
@media not screen and (color) {
  /* Non-color screens */
}

/* ONLY (legacy) */
@media only screen and (min-width: 768px) {
  /* Modern screens only */
}
```

---

## @import

**Loads external stylesheets** into your CSS.

### Basic Usage

```css
@import url('normalize.css');
@import url('typography.css');
@import url('components.css');

body {
  /* Your styles */
}
```

---

### With Media Queries

```css
/* Import only for print */
@import url('print.css') print;

/* Import for large screens */
@import url('desktop.css') screen and (min-width: 1024px);
```

---

### Performance Warning

```css
/* ⚠️ SLOW: Each @import is a separate HTTP request */
@import url('style1.css');
@import url('style2.css');
@import url('style3.css');

/* ✅ BETTER: Use <link> in HTML */
```

**HTML:**
```html
<link rel="stylesheet" href="style1.css">
<link rel="stylesheet" href="style2.css">
<link rel="stylesheet" href="style3.css">
```

**Why?** Browsers can download `<link>` files in parallel. `@import` must wait for each file sequentially.

---

## @keyframes

**Defines animation sequences.**

### Basic Animation

```css
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.element {
  animation: fadeIn 1s ease-in;
}
```

---

### Multi-Step Animation

```css
@keyframes slideInBounce {
  0% {
    transform: translateX(-100%);
    opacity: 0;
  }
  60% {
    transform: translateX(10px);
  }
  80% {
    transform: translateX(-5px);
  }
  100% {
    transform: translateX(0);
    opacity: 1;
  }
}

.element {
  animation: slideInBounce 0.8s ease-out;
}
```

---

### Multiple Properties

```css
@keyframes pulse {
  0%, 100% {
    transform: scale(1);
    opacity: 1;
  }
  50% {
    transform: scale(1.1);
    opacity: 0.8;
  }
}

.button {
  animation: pulse 2s infinite;
}
```

---

## @font-face

**Import custom fonts.**

### Basic Usage

```css
@font-face {
  font-family: 'MyCustomFont';
  src: url('MyCustomFont.woff2') format('woff2'),
       url('MyCustomFont.woff') format('woff');
  font-weight: normal;
  font-style: normal;
  font-display: swap; /* Prevent FOIT */
}

body {
  font-family: 'MyCustomFont', sans-serif;
}
```

---

### Multiple Weights

```css
/* Regular */
@font-face {
  font-family: 'Inter';
  src: url('Inter-Regular.woff2') format('woff2');
  font-weight: 400;
  font-style: normal;
}

/* Bold */
@font-face {
  font-family: 'Inter';
  src: url('Inter-Bold.woff2') format('woff2');
  font-weight: 700;
  font-style: normal;
}

/* Italic */
@font-face {
  font-family: 'Inter';
  src: url('Inter-Italic.woff2') format('woff2');
  font-weight: 400;
  font-style: italic;
}
```

---

### font-display Values

```css
@font-face {
  font-family: 'MyFont';
  src: url('MyFont.woff2') format('woff2');
  font-display: swap; /* Most common */
}
```

**Options:**
- `auto`: Browser decides (default)
- `block`: Hide text until font loads (Flash of Invisible Text - FOIT)
- `swap`: Show fallback immediately, swap when font loads (Flash of Unstyled Text - FOUT) ← **Recommended**
- `fallback`: Brief block period, then swap (compromise)
- `optional`: Use font only if cached (best performance)

---

## @supports

**Feature detection** - apply styles only if browser supports a CSS feature.

### Basic Usage

```css
/* Use Grid if supported */
@supports (display: grid) {
  .container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
  }
}

/* Fallback for old browsers */
@supports not (display: grid) {
  .container {
    display: flex;
    flex-wrap: wrap;
  }
}
```

---

### Multiple Conditions

```css
/* AND */
@supports (display: grid) and (gap: 20px) {
  .grid {
    display: grid;
    gap: 20px;
  }
}

/* OR */
@supports (display: flex) or (display: grid) {
  .container {
    /* Modern layout */
  }
}

/* NOT */
@supports not (aspect-ratio: 16 / 9) {
  /* Fallback for old browsers */
  .video-wrapper {
    padding-top: 56.25%; /* Old technique */
  }
}
```

---

### Real-World Example

```css
/* Modern: Use aspect-ratio */
.video-container {
  width: 100%;
}

@supports (aspect-ratio: 16 / 9) {
  .video-container {
    aspect-ratio: 16 / 9;
  }
}

/* Fallback: Padding-top technique */
@supports not (aspect-ratio: 16 / 9) {
  .video-container {
    position: relative;
    padding-top: 56.25%;
    height: 0;
  }

  .video-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
}
```

---

## @layer

**Cascade layers** for managing CSS specificity (new in 2022).

### Basic Usage

```css
/* Define layer order (highest priority last) */
@layer reset, base, components, utilities;

/* Add styles to layers */
@layer reset {
  * {
    margin: 0;
    padding: 0;
  }
}

@layer base {
  body {
    font-family: sans-serif;
    line-height: 1.6;
  }
}

@layer components {
  .button {
    padding: 10px 20px;
    background: blue;
  }
}

@layer utilities {
  .text-center {
    text-align: center;
  }
}
```

**Benefits:**
- Control specificity without `!important`
- Utilities can override components (even with lower specificity)
- Better organization

---

## @container

**Container queries** - responsive based on parent size, not viewport (new in 2023).

### Basic Usage

```css
/* Define container */
.card-grid {
  container-type: inline-size;
  container-name: card-container;
}

/* Query based on container width */
@container card-container (min-width: 400px) {
  .card {
    display: grid;
    grid-template-columns: 150px 1fr;
  }
}

@container card-container (min-width: 600px) {
  .card {
    grid-template-columns: 200px 1fr;
  }
}
```

**Difference from @media:**
- `@media`: Queries viewport size
- `@container`: Queries parent container size

**Use case:** Reusable components that adapt to their container, not screen size.

---

## Other At-Rules

### @charset

```css
/* Define character encoding (must be first line) */
@charset "UTF-8";
```

---

### @namespace

```css
/* For XML/SVG */
@namespace svg "http://www.w3.org/2000/svg";

svg|a {
  /* Styles for SVG <a> elements */
}
```

---

### @page

```css
/* Print styles */
@page {
  margin: 1in;
  size: A4;
}

@page :first {
  margin-top: 2in; /* First page */
}
```

---

### @property

```css
/* Register custom property (experimental) */
@property --gradient-angle {
  syntax: '<angle>';
  inherits: false;
  initial-value: 0deg;
}

.element {
  background: linear-gradient(var(--gradient-angle), blue, red);
  transition: --gradient-angle 1s;
}
```

---

## Best Practices

### ✅ Do This

1. **Use @media for responsive design**
   ```css
   @media (min-width: 768px) {
     /* Tablet styles */
   }
   ```

2. **Prefer <link> over @import**
   ```html
   <!-- Faster -->
   <link rel="stylesheet" href="style.css">
   ```

3. **Use @supports for progressive enhancement**
   ```css
   @supports (display: grid) {
     .grid {
       display: grid;
     }
   }
   ```

4. **Use font-display: swap**
   ```css
   @font-face {
     font-display: swap;
   }
   ```

5. **Group @media queries**
   ```css
   /* Good: All mobile styles together */
   @media (max-width: 768px) {
     .header { }
     .nav { }
     .footer { }
   }
   ```

---

### ❌ Avoid This

1. **Don't use @import in production**
   ```css
   /* Slow: Blocks rendering */
   @import url('style.css');
   ```

2. **Don't nest @media too deep**
   ```css
   /* Hard to maintain */
   @media (min-width: 768px) {
     @media (max-width: 1024px) {
       @media (orientation: portrait) {
         /* Too nested */
       }
     }
   }
   ```

3. **Don't forget @keyframes browser prefixes** (if supporting old browsers)
   ```css
   @-webkit-keyframes slide { }
   @keyframes slide { }
   ```

4. **Don't overuse @layer**
   ```css
   /* Overkill */
   @layer layer1, layer2, layer3, layer4, layer5;
   ```

---

## Browser Support

| At-Rule | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `@media` | All | All | All | All |
| `@import` | All | All | All | All |
| `@keyframes` | 43+ | 16+ | 9+ | 12+ |
| `@font-face` | 4+ | 3.5+ | 3.1+ | 12+ |
| `@supports` | 28+ | 22+ | 9+ | 12+ |
| `@layer` | 99+ | 97+ | 15.4+ | 99+ |
| `@container` | 105+ | 110+ | 16+ | 105+ |

**Support:**
- Core at-rules: Universal (100%)
- `@layer`: Modern browsers (90%+)
- `@container`: Cutting edge (85%+)

---

## Related Topics

**Prerequisites:**
- [CSS Fundamentals](../01-fundamentals/syntax.md)
- [Media Queries](../12-responsive-design/media-queries.md)

**Next Steps:**
- [Custom Properties](custom-properties.md)
- [Animations](../08-animations/keyframes.md)

---

## Practice Exercise

Create a responsive layout using at-rules:
- Use `@media` for 3 breakpoints
- Define `@keyframes` fade-in animation
- Import custom font with `@font-face`
- Use `@supports` to provide Grid fallback
- Test in browser DevTools

---

## Navigation

**Previous:** [← Custom Properties](custom-properties.md)
**Next:** [Optimization →](optimization.md)
**Up:** [↑ Back to Modern CSS](../README.md#1️⃣3️⃣-modern-css-5-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Modern CSS
**Difficulty:** Intermediate
