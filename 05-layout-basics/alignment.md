---
title: CSS Alignment Techniques
category: Layout Basics
order: 6
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Alignment Techniques

> **Quick Summary:** CSS offers multiple centering methods: `margin: auto` for horizontal block centering, Flexbox for both axes, Grid for grid items, and absolute positioning for legacy support. Modern best practice: use Flexbox or Grid for reliable, responsive centering.

## Table of Contents
- [Introduction](#introduction)
- [Horizontal Centering](#horizontal-centering)
- [Vertical Centering](#vertical-centering)
- [Flexbox Centering](#flexbox-centering)
- [Grid Centering](#grid-centering)
- [Absolute Positioning](#absolute-positioning)
- [Text Alignment](#text-alignment)
- [Examples](#examples)
- [Best Practices](#best-practices)

---

## Introduction

**Centering in CSS:** Historically challenging, now simple with modern layout methods.

**Methods:**
1. **text-align** - Inline/inline-block elements
2. **margin: auto** - Block elements (horizontal only)
3. **Flexbox** - Modern, both axes
4. **Grid** - Modern, both axes
5. **Absolute positioning** - Legacy fallback

---

## Horizontal Centering

### Method 1: Text-Align (Inline Elements)

```css
.container {
  text-align: center; /* Centers inline/inline-block children */
}
```

**Works on:**
- Text
- Inline elements (`<span>`, `<a>`)
- Inline-block elements
- Images (if default display: inline)

**Example:**
```html
<div class="container">
  <span>Centered text</span>
  <a href="#">Centered link</a>
</div>
```

### Method 2: Margin Auto (Block Elements)

```css
.block {
  width: 500px; /* Must have width */
  margin-left: auto;
  margin-right: auto;
  /* or shorthand: margin: 0 auto; */
}
```

**Requirements:**
- Element must be `display: block`
- Must have explicit width (not 100%)

**Example:**
```css
.container {
  width: 800px;
  max-width: 90%; /* Responsive */
  margin: 0 auto; /* Centered */
}
```

### Method 3: Flexbox (Modern)

```css
.container {
  display: flex;
  justify-content: center; /* Horizontal centering */
}
```

---

## Vertical Centering

### Method 1: Line-Height (Single Line Text)

```css
.box {
  height: 100px;
  line-height: 100px; /* Match height */
  text-align: center;
}
```

**Limitation:** Only works for single-line text

### Method 2: Flexbox (Modern, Recommended)

```css
.container {
  display: flex;
  align-items: center; /* Vertical centering */
  min-height: 400px;
}
```

### Method 3: Grid (Modern)

```css
.container {
  display: grid;
  place-items: center; /* Both axes */
  min-height: 400px;
}
```

### Method 4: Absolute Positioning + Transform (Legacy)

```css
.parent {
  position: relative;
  height: 400px;
}

.child {
  position: absolute;
  top: 50%;
  transform: translateY(-50%); /* Pull up by half own height */
}
```

---

## Flexbox Centering

**Best modern method** for most centering needs.

### Horizontal Only

```css
.container {
  display: flex;
  justify-content: center;
}
```

### Vertical Only

```css
.container {
  display: flex;
  align-items: center;
  min-height: 100vh;
}
```

### Both Axes (Perfectly Centered)

```css
.container {
  display: flex;
  justify-content: center; /* Horizontal */
  align-items: center; /* Vertical */
  min-height: 100vh;
}
```

**Example:**
```html
<div class="hero">
  <div class="content">
    <h1>Perfectly Centered</h1>
    <p>Both horizontally and vertically</p>
  </div>
</div>
```

```css
.hero {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: #3498db;
  color: white;
}

.content {
  text-align: center;
}
```

---

## Grid Centering

**Alternative modern method:**

### Method 1: place-items

```css
.container {
  display: grid;
  place-items: center; /* Both axes */
  min-height: 100vh;
}
```

**Shorthand for:**
```css
.container {
  display: grid;
  align-items: center; /* Vertical */
  justify-items: center; /* Horizontal */
}
```

### Method 2: place-content

```css
.container {
  display: grid;
  place-content: center;
  min-height: 100vh;
}
```

**Difference:**
- `place-items` - Centers individual grid items
- `place-content` - Centers the entire grid

---

## Absolute Positioning

**Legacy method** (use when Flexbox/Grid unavailable)

### Horizontal Centering

```css
.parent {
  position: relative;
}

.child {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}
```

### Vertical Centering

```css
.parent {
  position: relative;
  height: 400px;
}

.child {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
```

### Both Axes

```css
.parent {
  position: relative;
  height: 100vh;
}

.child {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

**Alternative (known dimensions):**
```css
.child {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  margin: auto;
  width: 300px; /* Must have dimensions */
  height: 200px;
}
```

---

## Text Alignment

### Horizontal Text Alignment

```css
.left { text-align: left; }
.center { text-align: center; }
.right { text-align: right; }
.justify { text-align: justify; }
```

### Vertical Text Alignment (Table Cells)

```css
.cell {
  display: table-cell;
  vertical-align: middle;
  height: 200px;
}
```

---

## Examples

### Example 1: Centered Hero Section

```html
<section class="hero">
  <div class="hero-content">
    <h1>Welcome</h1>
    <p>Perfectly centered content</p>
    <button>Get Started</button>
  </div>
</section>
```

```css
.hero {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  text-align: center;
}

.hero-content h1 {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.hero-content p {
  font-size: 1.25rem;
  margin-bottom: 2rem;
}
```

---

### Example 2: Centered Card

```html
<div class="container">
  <div class="card">
    <h2>Centered Card</h2>
    <p>This card is centered on the page</p>
  </div>
</div>
```

```css
/* Method 1: Flexbox */
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: #ecf0f1;
}

.card {
  background: white;
  padding: 40px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  max-width: 500px;
}

/* Method 2: Grid */
.container {
  display: grid;
  place-items: center;
  min-height: 100vh;
  background: #ecf0f1;
}
```

---

### Example 3: Centered Navigation

```html
<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/about">About</a></li>
    <li><a href="/contact">Contact</a></li>
  </ul>
</nav>
```

```css
nav {
  background: #333;
}

nav ul {
  display: flex;
  justify-content: center; /* Center nav items */
  list-style: none;
  margin: 0;
  padding: 0;
}

nav a {
  display: block;
  padding: 15px 20px;
  color: white;
  text-decoration: none;
}

nav a:hover {
  background: #555;
}
```

---

### Example 4: Multiple Centering Methods Comparison

```html
<div class="grid">
  <div class="method method-flexbox">
    <div class="box">Flexbox</div>
  </div>
  <div class="method method-grid">
    <div class="box">Grid</div>
  </div>
  <div class="method method-absolute">
    <div class="box">Absolute</div>
  </div>
</div>
```

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}

.method {
  height: 200px;
  border: 2px solid #ddd;
}

.box {
  padding: 20px;
  background: #3498db;
  color: white;
  border-radius: 8px;
}

/* Method 1: Flexbox */
.method-flexbox {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Method 2: Grid */
.method-grid {
  display: grid;
  place-items: center;
}

/* Method 3: Absolute */
.method-absolute {
  position: relative;
}

.method-absolute .box {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

---

## Browser Support

| Method | Chrome | Firefox | Safari | Edge | IE |
|--------|--------|---------|--------|------|-----|
| `text-align` | 1+ | 1+ | 1+ | 12+ | 3+ |
| `margin: auto` | 1+ | 1+ | 1+ | 12+ | 6+ |
| Flexbox | 29+ | 28+ | 9+ | 12+ | 11+ |
| Grid | 57+ | 52+ | 10.1+ | 16+ | ❌ |
| Absolute + transform | 36+ | 16+ | 9+ | 12+ | 9+ |

---

## Best Practices

### ✅ Do This

**1. Use Flexbox for most centering**
```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

**2. Use Grid for grid-based centering**
```css
.grid {
  display: grid;
  place-items: center;
}
```

**3. Use margin: auto for simple horizontal centering**
```css
.container {
  width: 800px;
  margin: 0 auto;
}
```

**4. Combine text-align with Flexbox**
```css
.hero {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center; /* Center text inside */
}
```

### ❌ Avoid This

**1. Don't use absolute positioning as first choice**
```css
/* ❌ Old-school, fragile */
.center {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/* ✅ Modern, robust */
.center {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

**2. Don't use line-height for multi-line text**
```css
/* ❌ Breaks with multiple lines */
.box {
  height: 100px;
  line-height: 100px;
}

/* ✅ Works for any content */
.box {
  display: flex;
  align-items: center;
  min-height: 100px;
}
```

**3. Don't forget to set parent height**
```css
/* ❌ Vertical centering won't work */
.container {
  display: flex;
  align-items: center;
  /* No height! */
}

/* ✅ Set min-height */
.container {
  display: flex;
  align-items: center;
  min-height: 100vh;
}
```

---

## Centering Cheat Sheet

**Horizontal centering:**
- Inline elements: `text-align: center`
- Block elements: `margin: 0 auto` (with width)
- Flexbox: `justify-content: center`
- Grid: `place-items: center`

**Vertical centering:**
- Flexbox: `align-items: center`
- Grid: `place-items: center`
- Absolute: `top: 50%; transform: translateY(-50%)`

**Both axes:**
- Flexbox: `justify-content: center; align-items: center`
- Grid: `place-items: center`
- Absolute: `top/left: 50%; transform: translate(-50%, -50%)`

---

**Last Updated:** November 15, 2025
**Category:** Layout Basics
**Difficulty:** Beginner

**Related Topics:**
- [Flexbox](../06-flexbox/flexbox-intro.md) - Modern 1D layouts
- [CSS Grid](../07-grid/grid-intro.md) - Modern 2D layouts
- [Display Property](display.md) - Display values
- [Position](position.md) - Positioning systems
