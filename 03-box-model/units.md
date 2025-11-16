---
title: CSS Units
category: Box Model
order: 9
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Units

> **Quick Summary:** CSS supports absolute units (px, pt) and relative units (em, rem, %, vw, vh). Use `rem` for font sizes, `%` or viewport units for layouts, and `px` for borders. Relative units create responsive, accessible designs.

## Table of Contents
- [Introduction](#introduction)
- [Absolute Units](#absolute-units)
- [Relative Units](#relative-units)
- [Viewport Units](#viewport-units)
- [Font-Relative Units](#font-relative-units)
- [When to Use Each Unit](#when-to-use-each-unit)
- [Examples](#examples)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)

---

## Introduction

**CSS units** define measurements for sizes, spacing, and positioning.

**Two categories:**
1. **Absolute:** Fixed sizes (px, cm, in)
2. **Relative:** Scale based on context (em, rem, %, vw)

**Modern best practice:** Use relative units for scalability and accessibility.

---

## Absolute Units

### Pixels (px)

**Most common absolute unit**

```css
.box {
  width: 300px;
  height: 200px;
  font-size: 16px;
}
```

**Characteristics:**
- Fixed size across all screens
- Not affected by parent/root font size
- Good for: borders, box shadows, small details

**1px ≠ 1 physical pixel on high-DPI screens**

### Other Absolute Units

```css
/* Rarely used in web design */
.print {
  width: 8.5in;  /* Inches */
  height: 11in;
  margin: 0.5cm; /* Centimeters */
  font-size: 12pt; /* Points (print typography) */
}
```

**Use cases:** Print stylesheets only

---

## Relative Units

### Percentage (%)

**Relative to parent element**

```css
.parent {
  width: 1000px;
}

.child {
  width: 50%; /* 500px (50% of parent) */
}
```

**Property-specific:**
- `width/height %` = parent's width/height
- `padding/margin %` = parent's **width** (even for vertical!)
- `font-size %` = parent's font-size

**Example:**
```css
.container {
  width: 800px;
  font-size: 16px;
}

.child {
  width: 50%; /* 400px */
  padding: 10%; /* 80px (10% of parent width!) */
  font-size: 150%; /* 24px (150% of 16px) */
}
```

---

## Viewport Units

**Relative to browser viewport (visible area)**

### Viewport Width (vw)

```css
.full-width {
  width: 100vw; /* 100% of viewport width */
}

.half-width {
  width: 50vw; /* 50% of viewport width */
}
```

**1vw** = 1% of viewport width

### Viewport Height (vh)

```css
.full-height {
  height: 100vh; /* 100% of viewport height */
}

.hero {
  min-height: 80vh; /* At least 80% of viewport */
}
```

**1vh** = 1% of viewport height

### Viewport Minimum (vmin)

```css
.square {
  width: 50vmin; /* 50% of smaller dimension */
  height: 50vmin;
}
```

**1vmin** = 1% of viewport's smaller dimension (width or height)

### Viewport Maximum (vmax)

```css
.element {
  font-size: 5vmax; /* 5% of larger dimension */
}
```

**1vmax** = 1% of viewport's larger dimension

---

## Font-Relative Units

### EM (em)

**Relative to parent element's font-size**

```css
.parent {
  font-size: 16px;
}

.child {
  font-size: 2em; /* 32px (2 × 16px) */
  padding: 1em; /* 32px (1 × own font-size!) */
}
```

**Caution:** Compounds (nesting multiplies)

```css
.parent {
  font-size: 16px;
}

.child {
  font-size: 1.5em; /* 24px */
}

.grandchild {
  font-size: 1.5em; /* 36px (1.5 × 24px) = compounding! */
}
```

### REM (rem)

**Relative to root element's font-size**

```css
html {
  font-size: 16px; /* Root */
}

.element {
  font-size: 1.5rem; /* 24px (1.5 × 16px) */
  padding: 2rem; /* 32px (2 × 16px) */
}

.nested .deeply .element {
  font-size: 1.5rem; /* Still 24px (no compounding!) */
}
```

**Benefits:**
- Predictable (always relative to root)
- No compounding issues
- Scalable (change root = everything scales)

**Modern best practice:** Use `rem` for font sizes

### CH (character width)

```css
.monospace {
  width: 80ch; /* Width of 80 "0" characters */
}
```

**Use case:** Limiting line length for readability

### EX (x-height)

```css
.element {
  height: 5ex; /* 5× height of lowercase "x" */
}
```

**Rarely used**

---

## When to Use Each Unit

### Pixels (px)

```css
/* Use for: */
.element {
  border: 1px solid black; /* Borders */
  box-shadow: 0 2px 4px rgba(0,0,0,0.1); /* Shadows */
  border-radius: 4px; /* Small radii */
}
```

### REM

```css
/* Use for: */
.element {
  font-size: 1.5rem; /* Font sizes */
  padding: 2rem; /* Spacing (scales with font) */
  margin: 1.5rem; /* Margins */
}
```

### Percentage (%)

```css
/* Use for: */
.element {
  width: 50%; /* Fluid widths */
  padding: 5%; /* Relative spacing */
}
```

### Viewport Units (vw, vh)

```css
/* Use for: */
.hero {
  height: 100vh; /* Full-screen sections */
  width: 100vw; /* Full-width backgrounds */
}

.responsive-text {
  font-size: 5vw; /* Responsive typography (with limits!) */
}
```

---

## Examples

### Example 1: Responsive Font Sizes

```css
html {
  font-size: 16px; /* Base size */
}

body {
  font-size: 1rem; /* 16px */
}

h1 {
  font-size: 2.5rem; /* 40px */
}

h2 {
  font-size: 2rem; /* 32px */
}

small {
  font-size: 0.875rem; /* 14px */
}
```

---

### Example 2: Fluid Typography

```css
html {
  /* Scales from 14px to 18px based on viewport */
  font-size: calc(14px + (18 - 14) * ((100vw - 320px) / (1200 - 320)));
}

@media (max-width: 320px) {
  html {
    font-size: 14px;
  }
}

@media (min-width: 1200px) {
  html {
    font-size: 18px;
  }
}
```

---

### Example 3: Responsive Padding

```css
.container {
  padding: 1rem; /* 16px on mobile */
}

@media (min-width: 768px) {
  .container {
    padding: 2rem; /* 32px on tablet+ */
  }
}

@media (min-width: 1200px) {
  .container {
    padding: 3rem; /* 48px on desktop+ */
  }
}
```

---

### Example 4: Full-Screen Hero

```css
.hero {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.hero-title {
  font-size: 5vw; /* Scales with viewport */
  max-font-size: 4rem; /* Cap at 64px */
  min-font-size: 2rem; /* Minimum 32px */
}
```

---

## Browser Support

| Unit | Chrome | Firefox | Safari | Edge | IE |
|------|--------|---------|--------|------|-----|
| `px` | 1+ | 1+ | 1+ | 12+ | 3+ |
| `em`, `rem` | 1+ | 1+ | 1+ | 12+ | 9+ |
| `%` | 1+ | 1+ | 1+ | 12+ | 3+ |
| `vw`, `vh` | 26+ | 19+ | 6.1+ | 12+ | 9+ |
| `vmin`, `vmax` | 26+ | 19+ | 6.1+ | 12+ | (vmax) |
| `ch` | 27+ | 1+ | 7+ | 12+ | 9+ |

**Excellent support** for most units in modern browsers.

---

## Best Practices

### Do This

**1. Use rem for font sizes**
```css
html {
  font-size: 16px;
}

body {
  font-size: 1rem;
}

h1 {
  font-size: 2.5rem;
}
```

**2. Use percentages for widths**
```css
.container {
  width: 100%;
  max-width: 1200px;
}

.col-half {
  width: 50%;
}
```

**3. Use viewport units for full-screen sections**
```css
.hero {
  min-height: 100vh;
}
```

**4. Use px for borders and small details**
```css
.card {
  border: 1px solid #ddd;
  border-radius: 4px;
}
```

### Avoid This

**1. Don't use px for font sizes**
```css
/* Bad - not accessible */
body {
  font-size: 16px;
}

/* Good - scales with user preferences */
body {
  font-size: 1rem;
}
```

**2. Don't use em for font sizes (compounding issues)**
```css
/* Bad - compounds in nested elements */
.parent {
  font-size: 1.5em;
}

.child {
  font-size: 1.5em; /* 1.5 × 1.5 = 2.25× root! */
}

/* Good - use rem */
.parent {
  font-size: 1.5rem;
}

.child {
  font-size: 1.5rem; /* Always 1.5× root */
}
```

**3. Don't use viewport units without limits**
```css
/* Bad - too small on mobile, too large on desktop */
.text {
  font-size: 5vw;
}

/* Good - add min/max */
.text {
  font-size: clamp(1rem, 5vw, 3rem);
}
```

---

## Unit Conversion Cheat Sheet

**Assuming root font-size: 16px**

| rem | px | em (if parent=16px) |
|-----|----|--------------------|
| 0.5rem | 8px | 0.5em |
| 0.75rem | 12px | 0.75em |
| 1rem | 16px | 1em |
| 1.25rem | 20px | 1.25em |
| 1.5rem | 24px | 1.5em |
| 2rem | 32px | 2em |
| 3rem | 48px | 3em |
| 4rem | 64px | 4em |

---

**Last Updated:** November 15, 2025
**Category:** Box Model
**Difficulty:** Beginner

**Related Topics:**
- [Height & Width](height-width.md) - Element sizing
- [Fonts](../04-typography/fonts.md) - Font sizing
- [Responsive Design](../12-responsive-design/media-queries.md) - Responsive layouts
