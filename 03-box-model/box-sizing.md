---
title: CSS Box Sizing
category: Box Model
order: 8
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Box Sizing

> **Quick Summary:** `box-sizing` controls how width and height are calculated. `content-box` (default) adds padding/border to dimensions. `border-box` includes padding/border in dimensions. Almost all modern sites use `border-box` globally.

## Table of Contents
- [Introduction](#introduction)
- [Content-Box (Default)](#content-box-default)
- [Border-Box](#border-box)
- [Global Box-Sizing Reset](#global-box-sizing-reset)
- [Use Cases](#use-cases)
- [Examples](#examples)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)

---

## Introduction

**Problem:** By default, padding and border ADD to element dimensions, making sizing unpredictable.

**Example of the problem:**
```css
.box {
  width: 300px;
  padding: 20px;
  border: 5px solid black;
  /* Actual width: 300 + 40 (padding) + 10 (border) = 350px */
}
```

**Solution:** Use `box-sizing: border-box` to include padding/border in width.

---

## Content-Box (Default)

**Default behavior:** Width/height apply ONLY to content

```css
.content-box {
  box-sizing: content-box; /* Default */
  width: 300px;
  padding: 20px;
  border: 5px solid black;
}
```

**Calculation:**
```
Total width = width + padding-left + padding-right + border-left + border-right
            = 300 + 20 + 20 + 5 + 5
            = 350px
```

**Visual:**
```
┌─────────────────────────────────────┐
│ Border (5px each side)              │
│  ┌─────────────────────────────┐    │
│  │ Padding (20px each side)    │    │
│  │  ┌───────────────────────┐  │    │
│  │  │ Content (300px)       │  │    │
│  │  └───────────────────────┘  │    │
│  └─────────────────────────────┘    │
└─────────────────────────────────────┘
          Total: 350px
```

---

## Border-Box

**Modern approach:** Width/height include padding and border

```css
.border-box {
  box-sizing: border-box;
  width: 300px;
  padding: 20px;
  border: 5px solid black;
}
```

**Calculation:**
```
Total width = width (padding and border included)
            = 300px (exactly what you set!)
```

**Visual:**
```
┌─────────────────────────────────────┐
│ Border (5px)     (300px total)      │
│  ┌─────────────────────────────┐    │
│  │ Padding (20px)              │    │
│  │  ┌───────────────────────┐  │    │
│  │  │ Content (250px)       │  │    │
│  │  └───────────────────────┘  │    │
│  └─────────────────────────────┘    │
└─────────────────────────────────────┘
          Total: 300px
```

**Content width:** `300 - 40 (padding) - 10 (border) = 250px`

---

## Global Box-Sizing Reset

**Industry standard:** Apply `border-box` to everything

### Recommended Method

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

**Why this works:**
- Applies to all elements
- Includes pseudo-elements (::before, ::after)
- Predictable sizing everywhere

### Alternative (Inheritable)

```css
html {
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}
```

**Benefit:** Allows components to opt out by changing parent's box-sizing

---

## Use Cases

### Use Border-Box When:

**1. Building layouts**
```css
.container {
  box-sizing: border-box;
  width: 100%;
  padding: 20px; /* Padding doesn't break layout */
}
```

**2. Creating grids**
```css
.col {
  box-sizing: border-box;
  width: 33.333%;
  padding: 15px; /* Still 33.333% total */
}
```

**3. Responsive design**
```css
.card {
  box-sizing: border-box;
  width: 100%;
  padding: 20px;
  /* Always 100%, regardless of padding */
}
```

### Keep Content-Box When:

**Rare:** Almost never. Legacy code only.

---

## Examples

### Example 1: Problem Without Border-Box

```css
/* Problem: Columns overflow container */
.container {
  width: 900px;
}

.col {
  float: left;
  width: 300px;
  padding: 20px; /* Actual width: 340px! */
  border: 5px solid black; /* Total: 350px */
}

/* Result: 3 columns × 350px = 1050px > 900px = overflow! */
```

### Example 2: Solution With Border-Box

```css
/* Solution: Perfect fit */
.container {
  width: 900px;
}

.col {
  box-sizing: border-box; /* Include padding in width */
  float: left;
  width: 300px;
  padding: 20px; /* Still 300px total */
  border: 5px solid black; /* Still 300px total */
}

/* Result: 3 columns × 300px = 900px = perfect fit! */
```

---

### Example 3: Responsive Card

```css
.card {
  box-sizing: border-box;
  width: 100%;
  padding: 20px;
  border: 1px solid #ddd;
}

/* Always 100% width, regardless of padding/border */
```

---

### Example 4: Form Inputs

```css
input,
textarea,
select {
  box-sizing: border-box;
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
}

/* All inputs are exactly 100% wide */
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE |
|----------|--------|---------|--------|------|-----|
| `box-sizing: border-box` | 10+ | 29+ | 5.1+ | 12+ | 8+ |
| `box-sizing: content-box` | 1+ | 1+ | 3+ | 12+ | 8+ |

**Excellent support** - Works in all modern browsers.

---

## Best Practices

### Do This

**1. Use global border-box reset**
```css
/* ALWAYS include this in your CSS */
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

**2. Set widths confidently**
```css
.sidebar {
  box-sizing: border-box;
  width: 300px;
  padding: 20px; /* Still 300px! */
}
```

**3. Use percentages safely**
```css
.col-half {
  box-sizing: border-box;
  width: 50%;
  padding: 15px; /* Still exactly 50% */
}
```

### Avoid This

**1. Don't forget the reset**
```css
/* Without box-sizing reset */
.element {
  width: 300px;
  padding: 20px; /* Surprise! Actually 340px */
}

/* With box-sizing reset */
*,
*::before,
*::after {
  box-sizing: border-box;
}

.element {
  width: 300px;
  padding: 20px; /* Exactly 300px */
}
```

**2. Don't use content-box intentionally**
```css
/* Rarely needed */
.element {
  box-sizing: content-box;
}

/* Just use border-box */
.element {
  box-sizing: border-box;
}
```

**3. Don't calculate widths manually**
```css
/* Error-prone */
.col {
  width: calc(33.333% - 40px); /* Accounting for padding */
  padding: 20px;
}

/* Let border-box handle it */
.col {
  box-sizing: border-box;
  width: 33.333%;
  padding: 20px;
}
```

---

## Why Border-Box is Better

### Benefits of `border-box`:

1. **Predictable sizing:** Width = actual width
2. **Easier math:** No mental calculations
3. **Flexible padding:** Add padding without breaking layout
4. **Responsive-friendly:** Percentages work as expected
5. **Industry standard:** Used in Bootstrap, Tailwind, etc.

### Comparison Table

| Scenario | Content-Box | Border-Box |
|----------|-------------|------------|
| Set width: 300px, padding: 20px | Total: 340px | Total: 300px |
| Set width: 50%, padding: 15px | May overflow | Exactly 50% |
| Adding border later | Breaks layout | Still works |
| Responsive grid | Manual calc needed | Just works |

---

## Visual Comparison

```css
/* CONTENT-BOX (Default) */
.content-box {
  width: 200px;
  padding: 20px;
  border: 5px solid black;
  /* Visual width: 250px */
  /* Content width: 200px */
}

/* BORDER-BOX (Recommended) */
.border-box {
  box-sizing: border-box;
  width: 200px;
  padding: 20px;
  border: 5px solid black;
  /* Visual width: 200px */
  /* Content width: 150px */
}
```

---

**Last Updated:** November 15, 2025
**Category:** Box Model
**Difficulty:** Beginner

**Related Topics:**
- [Box Model Concept](box-model-concept.md) - Box model fundamentals
- [Padding](padding.md) - Internal spacing
- [Borders](borders.md) - Border properties
- [Height & Width](height-width.md) - Element sizing
