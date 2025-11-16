---
title: CSS Float
category: Layout Basics
order: 4
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Float

> **Quick Summary:** Float removes elements from normal document flow, moving them left or right while allowing text to wrap. Originally for magazine-style layouts, now largely replaced by Flexbox/Grid. Still useful for wrapping text around images.

## Table of Contents
- [Introduction](#introduction)
- [Float Property](#float-property)
- [Clearing Floats](#clearing-floats)
- [Clearfix Technique](#clearfix-technique)
- [Float-Based Layouts (Legacy)](#float-based-layouts-legacy)
- [Modern Alternatives](#modern-alternatives)
- [Use Cases Today](#use-cases-today)
- [Examples](#examples)
- [Best Practices](#best-practices)

---

## Introduction

**Float:** Originally designed for magazine-style text wrapping around images.

**What float does:**
1. Removes element from normal flow
2. Shifts element left or right
3. Allows text/inline elements to wrap around it

**Historical use:** Before Flexbox/Grid, float was THE way to create multi-column layouts.

**Modern use:** Primarily for text wrapping around images.

---

## Float Property

**Syntax:**
```css
.element {
  float: left | right | none;
}
```

### float: left

```css
.image {
  float: left;
  margin-right: 20px;
}
```

**Result:** Element shifts to left, content wraps on right

### float: right

```css
.sidebar {
  float: right;
  margin-left: 20px;
}
```

**Result:** Element shifts to right, content wraps on left

### float: none (default)

```css
.element {
  float: none; /* Normal document flow */
}
```

---

## Clearing Floats

**Problem:** Parent containers don't wrap around floated children (height collapses)

### Method 1: Clear Property

```css
.clear {
  clear: left;   /* No floated elements on left */
  clear: right;  /* No floated elements on right */
  clear: both;   /* No floated elements on either side */
}
```

**Example:**
```html
<div class="container">
  <div class="float-left">Float</div>
  <div class="clear">This starts below float</div>
</div>
```

```css
.float-left {
  float: left;
}

.clear {
  clear: both; /* Starts below floated element */
}
```

### Method 2: Overflow

```css
.container {
  overflow: hidden; /* or auto */
}

.child {
  float: left;
}
```

**How it works:** Creates new Block Formatting Context (BFC)

---

## Clearfix Technique

**Problem:** Parent container collapses when all children are floated

**Solution:** Clearfix hack (still widely used)

### Modern Clearfix

```css
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}
```

**Usage:**
```html
<div class="container clearfix">
  <div class="float-left">Float</div>
  <div class="float-right">Float</div>
</div>
<!-- Container now has height -->
```

### Legacy Clearfix (IE Support)

```css
.clearfix::before,
.clearfix::after {
  content: "";
  display: table;
}

.clearfix::after {
  clear: both;
}

.clearfix {
  *zoom: 1; /* IE6-7 */
}
```

---

## Float-Based Layouts (Legacy)

**Before Flexbox/Grid, floats created layouts:**

### Two-Column Layout

```html
<div class="container clearfix">
  <aside class="sidebar">Sidebar</aside>
  <main class="content">Main Content</main>
</div>
```

```css
.container {
  max-width: 1200px;
}

.sidebar {
  float: left;
  width: 25%;
}

.content {
  float: right;
  width: 70%;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}
```

### Three-Column Layout

```css
.left {
  float: left;
  width: 20%;
}

.center {
  float: left;
  width: 60%;
}

.right {
  float: left;
  width: 20%;
}
```

**Issues with float layouts:**
- Height collapse
- Source order restrictions
- Requires clearfix everywhere
- Math doesn't always add up (rounding errors)

---

## Modern Alternatives

### Flexbox (Preferred for 1D layouts)

```css
/* OLD: Float-based */
.container::after {
  content: "";
  display: table;
  clear: both;
}

.sidebar { float: left; width: 25%; }
.content { float: left; width: 75%; }

/* NEW: Flexbox */
.container {
  display: flex;
}

.sidebar {
  flex: 0 0 25%;
}

.content {
  flex: 1;
}
```

### Grid (Preferred for 2D layouts)

```css
/* OLD: Float-based */
.col { float: left; width: 33.333%; }

/* NEW: Grid */
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
```

---

## Use Cases Today

### Still Use Float For:

**1. Text wrapping around images**
```css
.article-image {
  float: left;
  margin: 0 20px 10px 0;
  max-width: 300px;
}
```

**2. Magazine-style layouts**
```css
.pull-quote {
  float: right;
  width: 30%;
  margin: 0 0 10px 20px;
  font-size: 1.5em;
  border-left: 4px solid #3498db;
  padding-left: 20px;
}
```

### Don't Use Float For:

- Page layouts (use Grid)
- Navigation menus (use Flexbox)
- Card grids (use Grid or Flexbox)
- Centering elements (use Flexbox/Grid)

---

## Examples

### Example 1: Text Wrapping Image

```html
<article>
  <img src="image.jpg" class="float-image">
  <p>Lorem ipsum dolor sit amet...</p>
  <p>Consectetur adipiscing elit...</p>
</article>
```

```css
.float-image {
  float: left;
  margin: 0 20px 10px 0;
  width: 300px;
  border-radius: 8px;
}

article {
  max-width: 800px;
}
```

---

### Example 2: Pull Quote

```html
<article>
  <p>Regular paragraph text...</p>
  <blockquote class="pull-quote">
    "This is a highlighted quote"
  </blockquote>
  <p>More paragraph text wraps around the quote...</p>
</article>
```

```css
.pull-quote {
  float: right;
  width: 40%;
  margin: 10px 0 10px 20px;
  padding: 20px;
  background: #f9f9f9;
  border-left: 4px solid #3498db;
  font-style: italic;
  font-size: 1.2em;
}
```

---

### Example 3: Legacy Two-Column Layout

```html
<div class="container clearfix">
  <aside class="sidebar">
    <h3>Sidebar</h3>
    <nav>...</nav>
  </aside>
  <main class="main">
    <h1>Main Content</h1>
    <p>...</p>
  </main>
</div>
```

```css
.container {
  max-width: 1200px;
  margin: 0 auto;
}

.sidebar {
  float: left;
  width: 250px;
  background: #f0f0f0;
  padding: 20px;
}

.main {
  margin-left: 290px; /* sidebar width + spacing */
  padding: 20px;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}
```

---

### Example 4: Floated Navigation (Legacy)

```html
<nav class="nav clearfix">
  <a href="/">Home</a>
  <a href="/about">About</a>
  <a href="/contact">Contact</a>
</nav>
```

```css
.nav a {
  float: left;
  padding: 10px 15px;
  text-decoration: none;
  color: #333;
}

.nav a:hover {
  background: #f0f0f0;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}
```

**Modern alternative:**
```css
.nav {
  display: flex;
  gap: 10px;
}

.nav a {
  padding: 10px 15px;
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE |
|----------|--------|---------|--------|------|-----|
| `float` | 1+ | 1+ | 1+ | 12+ | 4+ |
| `clear` | 1+ | 1+ | 1+ | 12+ | 4+ |

**Universal support** - Float works everywhere.

---

## Best Practices

### Do This

**1. Use float for text wrapping**
```css
.article-image {
  float: left;
  margin-right: 20px;
}
```

**2. Always clear floats**
```css
.container::after {
  content: "";
  display: table;
  clear: both;
}
```

**3. Add margins for spacing**
```css
.float-left {
  float: left;
  margin-right: 20px; /* Prevents text touching */
}
```

**4. Use modern layouts for grids**
```css
/* Good - use Grid/Flexbox for layouts */
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```

### Avoid This

**1. Don't use float for page layouts**
```css
/* Bad - use Grid instead */
.col {
  float: left;
  width: 33.333%;
}

/* Good */
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```

**2. Don't forget to clear**
```css
/* Bad - parent collapses */
.parent {
  /* No clearfix */
}

.child {
  float: left;
}

/* Good */
.parent::after {
  content: "";
  display: table;
  clear: both;
}
```

**3. Don't nest too many floats**
```css
/* Bad - complex, error-prone */
.outer { float: left; }
.inner { float: left; }
.nested { float: left; }

/* Good - use Flexbox */
.container {
  display: flex;
  flex-wrap: wrap;
}
```

---

**Last Updated:** November 15, 2025
**Category:** Layout Basics
**Difficulty:** Beginner

**Related Topics:**
- [Display Property](display.md) - Display values
- [Flexbox](../06-flexbox/flexbox-intro.md) - Modern 1D layouts
- [CSS Grid](../07-grid/grid-intro.md) - Modern 2D layouts
- [Position](position.md) - Positioning systems
