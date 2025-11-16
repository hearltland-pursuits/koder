---
title: Display Inline-Block
category: Layout Basics
order: 5
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Display: Inline-Block

> **Quick Summary:** `display: inline-block` combines inline (flows horizontally) with block (accepts width/height, respects all margins/padding). Perfect for navigation menus, button groups, and horizontal lists. Beware of whitespace between elements.

## Table of Contents
- [Introduction](#introduction)
- [Inline vs Inline-Block vs Block](#inline-vs-inline-block-vs-block)
- [Use Cases](#use-cases)
- [Whitespace Issue](#whitespace-issue)
- [Vertical Alignment](#vertical-alignment)
- [Examples](#examples)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)

---

## Introduction

**Inline-block:** The hybrid display value that gets the best of both inline and block.

**Characteristics:**
- ✅ Flows horizontally (like inline)
- ✅ Accepts width/height (like block)
- ✅ Respects all margins/padding (like block)
- ❌ Creates whitespace gaps (annoying quirk)

**Common uses:**
- Navigation menus
- Button groups
- Image galleries
- Tags/badges
- Card layouts (before Flexbox)

---

## Inline vs Inline-Block vs Block

### Comparison Table

| Feature | Inline | Inline-Block | Block |
|---------|--------|--------------|-------|
| **Flows horizontally** | ✅ Yes | ✅ Yes | ❌ No (stacks vertically) |
| **Can set width/height** | ❌ No | ✅ Yes | ✅ Yes |
| **Respects vertical margins** | ❌ No | ✅ Yes | ✅ Yes |
| **Respects padding (all sides)** | ⚠️ Partially | ✅ Yes | ✅ Yes |
| **Takes full width** | ❌ No | ❌ No | ✅ Yes (default) |
| **Default for** | `<span>`, `<a>` | None | `<div>`, `<p>` |

### Visual Comparison

```css
/* INLINE - no width/height */
.inline {
  display: inline;
  width: 100px; /* Ignored */
  height: 100px; /* Ignored */
  margin: 20px 10px; /* Vertical margins don't push */
}

/* INLINE-BLOCK - best of both */
.inline-block {
  display: inline-block;
  width: 100px; /* Works! */
  height: 100px; /* Works! */
  margin: 20px 10px; /* All work! */
}

/* BLOCK - full width by default */
.block {
  display: block;
  width: 100px; /* Works, but element is on own line */
  margin: 20px 10px;
}
```

---

## Use Cases

### 1. Navigation Menus

```css
.nav {
  list-style: none;
  padding: 0;
  background: #333;
}

.nav li {
  display: inline-block; /* Horizontal menu */
}

.nav a {
  display: inline-block;
  padding: 15px 20px;
  color: white;
  text-decoration: none;
}

.nav a:hover {
  background: #555;
}
```

### 2. Button Groups

```css
.btn {
  display: inline-block;
  padding: 10px 20px;
  background: #3498db;
  color: white;
  text-decoration: none;
  border-radius: 5px;
  margin-right: 10px;
}
```

### 3. Tag List

```css
.tag {
  display: inline-block;
  padding: 5px 10px;
  background: #ecf0f1;
  border-radius: 3px;
  font-size: 0.875rem;
  margin: 5px 5px 5px 0;
}
```

### 4. Image Gallery (Legacy)

```css
.gallery {
  text-align: center;
}

.gallery img {
  display: inline-block;
  width: 200px;
  height: 200px;
  object-fit: cover;
  margin: 10px;
  border-radius: 8px;
}
```

---

## Whitespace Issue

**Problem:** HTML whitespace (spaces, newlines) between `inline-block` elements renders as visible gaps.

### The Problem

```html
<div>
  <div class="box">1</div>
  <div class="box">2</div>
  <div class="box">3</div>
</div>
```

```css
.box {
  display: inline-block;
  width: 100px;
  height: 100px;
  background: #3498db;
}
```

**Result:** ~4px gap between boxes (browser renders whitespace)

### Solution 1: Remove Whitespace in HTML

```html
<!-- Remove spaces/newlines -->
<div><div class="box">1</div><div class="box">2</div><div class="box">3</div></div>

<!-- Or use comments -->
<div>
  <div class="box">1</div><!--
  --><div class="box">2</div><!--
  --><div class="box">3</div>
</div>
```

**Downside:** Ugly, hard to read

### Solution 2: font-size: 0 on Parent

```css
.container {
  font-size: 0; /* Removes whitespace */
}

.box {
  display: inline-block;
  font-size: 16px; /* Reset for children */
}
```

**Downside:** Must remember to reset font-size

### Solution 3: Negative Margin

```css
.box {
  display: inline-block;
  margin-right: -4px; /* Compensate for whitespace */
}
```

**Downside:** Fragile, depends on font-size

### Solution 4: Use Flexbox Instead (Modern)

```css
/* ✅ Best solution - no whitespace issues */
.container {
  display: flex;
  gap: 10px;
}
```

---

## Vertical Alignment

**Inline-block elements respect `vertical-align`:**

```css
.container {
  font-size: 0; /* Remove whitespace */
}

.box {
  display: inline-block;
  width: 100px;
  height: 100px;
  font-size: 16px;
  vertical-align: top; /* Align to top */
}
```

**vertical-align values:**
```css
.align-top { vertical-align: top; }
.align-middle { vertical-align: middle; }
.align-bottom { vertical-align: bottom; }
.align-baseline { vertical-align: baseline; } /* Default */
```

**Example:**
```html
<div>
  <div class="box" style="height: 50px; vertical-align: top;">Top</div>
  <div class="box" style="height: 100px; vertical-align: middle;">Middle</div>
  <div class="box" style="height: 75px; vertical-align: bottom;">Bottom</div>
</div>
```

---

## Examples

### Example 1: Horizontal Navigation

```html
<nav class="nav">
  <a href="/">Home</a>
  <a href="/about">About</a>
  <a href="/services">Services</a>
  <a href="/contact">Contact</a>
</nav>
```

```css
.nav {
  background: #333;
  font-size: 0; /* Remove whitespace */
}

.nav a {
  display: inline-block;
  padding: 15px 20px;
  color: white;
  text-decoration: none;
  font-size: 16px; /* Reset */
  transition: background 0.3s;
}

.nav a:hover {
  background: #555;
}
```

---

### Example 2: Card Grid (Legacy Method)

```html
<div class="grid">
  <div class="card">Card 1</div>
  <div class="card">Card 2</div>
  <div class="card">Card 3</div>
</div>
```

```css
.grid {
  font-size: 0;
  text-align: center;
}

.card {
  display: inline-block;
  width: 30%;
  margin: 1.5%;
  padding: 20px;
  background: white;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 16px;
  vertical-align: top; /* Align tops if heights differ */
}
```

---

### Example 3: Badge/Tag List

```html
<div class="tags">
  <span class="tag">HTML</span>
  <span class="tag">CSS</span>
  <span class="tag">JavaScript</span>
  <span class="tag">React</span>
</div>
```

```css
.tags {
  font-size: 0;
}

.tag {
  display: inline-block;
  padding: 6px 12px;
  background: #3498db;
  color: white;
  border-radius: 4px;
  font-size: 14px;
  margin: 5px 5px 5px 0;
}
```

---

### Example 4: Social Media Icons

```html
<div class="social">
  <a href="#" class="social-icon">FB</a>
  <a href="#" class="social-icon">TW</a>
  <a href="#" class="social-icon">IG</a>
</div>
```

```css
.social {
  font-size: 0;
}

.social-icon {
  display: inline-block;
  width: 40px;
  height: 40px;
  line-height: 40px;
  text-align: center;
  background: #3498db;
  color: white;
  text-decoration: none;
  border-radius: 50%;
  font-size: 14px;
  margin: 0 5px;
  transition: background 0.3s;
}

.social-icon:hover {
  background: #2980b9;
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE |
|----------|--------|---------|--------|------|-----|
| `display: inline-block` | 1+ | 3+ | 1+ | 12+ | 8+ |

**Universal support** - Works in all modern browsers.

---

## Best Practices

### ✅ Do This

**1. Use font-size: 0 to remove whitespace**
```css
.container {
  font-size: 0;
}

.item {
  display: inline-block;
  font-size: 16px;
}
```

**2. Set vertical-align: top for consistent alignment**
```css
.item {
  display: inline-block;
  vertical-align: top;
}
```

**3. Use for navigation and small components**
```css
.nav a {
  display: inline-block;
  padding: 10px 15px;
}
```

**4. Consider Flexbox for modern projects**
```css
/* ✅ Better than inline-block for grids */
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}
```

### ❌ Avoid This

**1. Don't forget about whitespace gaps**
```css
/* ❌ Will have gaps */
.box {
  display: inline-block;
}

/* ✅ Remove gaps */
.container { font-size: 0; }
.box { font-size: 16px; }
```

**2. Don't use for complex layouts**
```css
/* ❌ Bad - use Grid instead */
.complex-layout .col {
  display: inline-block;
  width: 25%;
}

/* ✅ Good - use Grid */
.complex-layout {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
}
```

**3. Don't forget vertical-align**
```css
/* ❌ Elements may not align as expected */
.item {
  display: inline-block;
}

/* ✅ Explicitly set alignment */
.item {
  display: inline-block;
  vertical-align: top;
}
```

---

**Last Updated:** November 15, 2025
**Category:** Layout Basics
**Difficulty:** Beginner

**Related Topics:**
- [Display Property](display.md) - All display values
- [Flexbox](../06-flexbox/flexbox-intro.md) - Modern alternative for horizontal layouts
- [Float](float.md) - Another legacy layout method
