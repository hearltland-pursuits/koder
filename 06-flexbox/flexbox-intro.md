---
title: Flexbox Introduction
category: Flexbox
order: 1
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Flexbox Introduction

> **Quick Summary:** Flexbox (Flexible Box Layout) is a modern CSS layout system that makes it easy to align, distribute, and resize elements in one dimension (row or column). It solves common layout problems like centering, equal-height columns, and responsive spacing.

## Table of Contents
- [Introduction](#introduction)
- [Why Flexbox Matters](#why-flexbox-matters)
- [Flex Container vs Flex Items](#flex-container-vs-flex-items)
- [Basic Flexbox Syntax](#basic-flexbox-syntax)
- [Main Axis vs Cross Axis](#main-axis-vs-cross-axis)
- [Core Container Properties](#core-container-properties)
- [Core Item Properties](#core-item-properties)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

Before Flexbox, creating layouts required CSS hacks: floats for columns, tables for alignment, absolute positioning for centering. Simple tasks like "create three equal-width columns" or "vertically center this div" required complex, fragile code. Flexbox changed everything.

**Flexbox is a layout mode designed for one-dimensional layouts**—either rows or columns. Need a horizontal navigation bar? Flexbox. Need vertically stacked cards that distribute space evenly? Flexbox. Need an image gallery that wraps to multiple lines? Flexbox. It excels at distributing space and aligning items, even when their sizes are unknown or dynamic.

The magic of Flexbox lies in its **flexibility**. Items can grow to fill available space, shrink to prevent overflow, or maintain their size. You can align items at the start, center, end, or distribute them evenly. You can reverse order, wrap to multiple lines, or even change visual order without touching HTML. Flexbox makes responsive design intuitive—columns on desktop become stacked rows on mobile with minimal code.

**Key Concept:** Flexbox has two parts: the **flex container** (parent) and **flex items** (children). Container properties control overall layout; item properties control individual element behavior.

---

## Why Flexbox Matters

### 1. **Solves Common Layout Problems**

**Before Flexbox (complex):**
```css
/* Centering with absolute positioning */
.centered {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

**With Flexbox (simple):**
```css
.container {
  display: flex;
  justify-content: center; /* Horizontal center */
  align-items: center;     /* Vertical center */
}
```

### 2. **Responsive by Default**
Flexbox adapts to content size and viewport width automatically:
```css
.container {
  display: flex;
  flex-wrap: wrap; /* Wraps to multiple rows on small screens */
}

.item {
  flex: 1 1 300px; /* Grows/shrinks, minimum 300px */
}
```

### 3. **Equal-Height Columns (No JavaScript)**
```css
.container {
  display: flex; /* All children automatically same height */
}
```

### 4. **Career Relevance**
Flexbox is standard in modern web development:
- **95%+ of job postings** require Flexbox knowledge
- **Interview question:** "How do you center a div?" → Flexbox
- **Common task:** "Build a responsive navigation bar" → Flexbox
- **Framework foundation:** Bootstrap, Tailwind, Material-UI all use Flexbox

---

## Flex Container vs Flex Items

Flexbox operates on a **parent-child relationship**:

```html
<div class="flex-container">  <!-- Parent -->
  <div class="flex-item">1</div>  <!-- Child -->
  <div class="flex-item">2</div>  <!-- Child -->
  <div class="flex-item">3</div>  <!-- Child -->
</div>
```

### Flex Container (Parent)
**Created by:** `display: flex;` or `display: inline-flex;`

**Controls:**
- Direction (row vs column)
- Wrapping (single vs multiple lines)
- Alignment of all items
- Space distribution

### Flex Items (Children)
**Automatically:** Direct children of flex container become flex items

**Controls:**
- Individual item size
- Individual item order
- Individual item alignment

---

## Basic Flexbox Syntax

### Step 1: Create Flex Container

```css
.container {
  display: flex; /* Activates Flexbox */
}
```

**What happens:**
- Children become flex items
- Items line up in a row (default direction)
- Items size to fit their content

### Step 2: Add Container Properties (Optional)

```css
.container {
  display: flex;
  flex-direction: row;        /* Direction: row or column */
  justify-content: center;    /* Main axis alignment */
  align-items: center;        /* Cross axis alignment */
  gap: 20px;                  /* Space between items */
}
```

### Step 3: Add Item Properties (Optional)

```css
.item {
  flex: 1;           /* Grow to fill space equally */
  align-self: flex-start; /* Override container alignment */
}
```

---

## Main Axis vs Cross Axis

Flexbox uses two axes:

### Main Axis
- **Direction:** Defined by `flex-direction`
- **`row`:** Main axis = horizontal (left → right)
- **`column`:** Main axis = vertical (top → bottom)
- **Controlled by:** `justify-content`

### Cross Axis
- **Direction:** Perpendicular to main axis
- **`row`:** Cross axis = vertical (top → bottom)
- **`column`:** Cross axis = horizontal (left → right)
- **Controlled by:** `align-items`

### Visual Diagram

```
flex-direction: row
┌──────────────────────────────────────┐
│                                      │ ↕️ Cross Axis
│  [Item 1] [Item 2] [Item 3]        │ (align-items)
│                                      │
└──────────────────────────────────────┘
  ↔️ Main Axis (justify-content)


flex-direction: column
┌─────────────┐
│  [Item 1]   │  ↕️ Main Axis
│  [Item 2]   │  (justify-content)
│  [Item 3]   │
└─────────────┘
  ↔️ Cross Axis
  (align-items)
```

---

## Core Container Properties

### 1. `flex-direction`
**Controls:** Main axis direction

**Values:**
```css
.container {
  flex-direction: row;            /* Default: left to right */
  flex-direction: row-reverse;    /* Right to left */
  flex-direction: column;         /* Top to bottom */
  flex-direction: column-reverse; /* Bottom to top */
}
```

---

### 2. `justify-content`
**Controls:** Alignment along **main axis**

**Values:**
```css
.container {
  justify-content: flex-start;    /* Default: start of axis */
  justify-content: flex-end;      /* End of axis */
  justify-content: center;        /* Center of axis */
  justify-content: space-between; /* Items spread: first/last at edges */
  justify-content: space-around;  /* Items spread: equal space around each */
  justify-content: space-evenly;  /* Items spread: equal space between all */
}
```

**Visual:**
```
flex-start:    [1][2][3]________
center:        ____[1][2][3]____
flex-end:      ________[1][2][3]
space-between: [1]____[2]____[3]
space-around:  __[1]____[2]____[3]__
space-evenly:  __[1]__[2]__[3]__
```

---

### 3. `align-items`
**Controls:** Alignment along **cross axis**

**Values:**
```css
.container {
  align-items: stretch;     /* Default: fill container height */
  align-items: flex-start;  /* Align to start of cross axis */
  align-items: flex-end;    /* Align to end of cross axis */
  align-items: center;      /* Center on cross axis */
  align-items: baseline;    /* Align by text baseline */
}
```

---

### 4. `flex-wrap`
**Controls:** Whether items wrap to multiple lines

**Values:**
```css
.container {
  flex-wrap: nowrap;       /* Default: single line (may overflow) */
  flex-wrap: wrap;         /* Wrap to multiple rows/columns */
  flex-wrap: wrap-reverse; /* Wrap in reverse order */
}
```

---

### 5. `gap`
**Controls:** Space between flex items

**Values:**
```css
.container {
  gap: 20px;           /* 20px between all items */
  gap: 10px 20px;      /* 10px row gap, 20px column gap */
  row-gap: 10px;       /* Only vertical gap */
  column-gap: 20px;    /* Only horizontal gap */
}
```

**Modern alternative to margins** — cleaner and more flexible.

---

## Core Item Properties

### 1. `flex-grow`
**Controls:** How much an item grows relative to siblings

**Values:** Number (default: `0`)

```css
.item1 { flex-grow: 1; } /* Takes 1 part of available space */
.item2 { flex-grow: 2; } /* Takes 2 parts (twice as much as item1) */
.item3 { flex-grow: 1; } /* Takes 1 part */
```

**Result:** Available space is divided: 25% / 50% / 25%

---

### 2. `flex-shrink`
**Controls:** How much an item shrinks when space is limited

**Values:** Number (default: `1`)

```css
.item {
  flex-shrink: 0; /* Never shrink (may overflow container) */
  flex-shrink: 1; /* Default: shrink equally */
  flex-shrink: 2; /* Shrink twice as much as siblings */
}
```

---

### 3. `flex-basis`
**Controls:** Initial size of item before growing/shrinking

**Values:** Length or `auto`

```css
.item {
  flex-basis: 200px;  /* Start at 200px width (for row) */
  flex-basis: auto;   /* Size based on content (default) */
  flex-basis: 0;      /* Ignore content size, only use grow/shrink */
}
```

---

### 4. `flex` (Shorthand)
**Combines:** `flex-grow flex-shrink flex-basis`

**Common patterns:**
```css
.item {
  flex: 1;           /* flex: 1 1 0 (equal widths) */
  flex: 0 0 200px;   /* Fixed 200px width, no grow/shrink */
  flex: 1 0 auto;    /* Grow, don't shrink, size from content */
}
```

---

### 5. `align-self`
**Controls:** Individual item's cross-axis alignment (overrides container's `align-items`)

**Values:**
```css
.item {
  align-self: auto;       /* Inherit from container */
  align-self: flex-start;
  align-self: flex-end;
  align-self: center;
  align-self: baseline;
  align-self: stretch;
}
```

---

## Examples

### Example 1: Horizontal Navigation Bar

```html
<nav class="navbar">
  <div class="logo">Logo</div>
  <ul class="nav-links">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Services</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

```css
.navbar {
  display: flex;
  justify-content: space-between; /* Logo left, links right */
  align-items: center;            /* Vertically centered */
  background-color: #2c3e50;
  padding: 1rem 2rem;
}

.logo {
  font-size: 24px;
  font-weight: bold;
  color: white;
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 2rem; /* Space between links */
}

.nav-links a {
  color: white;
  text-decoration: none;
}
```

**Result:** Logo on left, navigation links on right, all vertically centered.

---

### Example 2: Equal-Width Cards

```html
<div class="card-container">
  <div class="card">Card 1</div>
  <div class="card">Card 2 with more content that makes it taller</div>
  <div class="card">Card 3</div>
</div>
```

```css
.card-container {
  display: flex;
  gap: 20px;
}

.card {
  flex: 1; /* Equal width, same height automatically */
  padding: 20px;
  background-color: #ecf0f1;
  border-radius: 8px;
}
```

**Result:** Three equal-width cards with equal heights (tallest card determines height).

---

### Example 3: Centered Content

```html
<div class="hero">
  <div class="hero-content">
    <h1>Welcome</h1>
    <p>This content is perfectly centered</p>
  </div>
</div>
```

```css
.hero {
  display: flex;
  justify-content: center; /* Horizontal center */
  align-items: center;     /* Vertical center */
  height: 100vh;           /* Full viewport height */
  background-color: #3498db;
  color: white;
  text-align: center;
}
```

**Result:** Content is perfectly centered both horizontally and vertically.

---

### Example 4: Responsive Grid (Wrapping)

```html
<div class="grid">
  <div class="grid-item">1</div>
  <div class="grid-item">2</div>
  <div class="grid-item">3</div>
  <div class="grid-item">4</div>
  <div class="grid-item">5</div>
  <div class="grid-item">6</div>
</div>
```

```css
.grid {
  display: flex;
  flex-wrap: wrap; /* Wrap to multiple rows */
  gap: 20px;
}

.grid-item {
  flex: 1 1 250px; /* Grow/shrink, minimum 250px */
  height: 150px;
  background-color: #3498db;
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 24px;
  border-radius: 8px;
}
```

**Result:** Items wrap to multiple rows when viewport is narrow, creating a responsive grid.

---

## Common Use Cases

### Use Case 1: Sticky Footer

```css
body {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

main {
  flex: 1; /* Grows to fill available space */
}

footer {
  /* Naturally sticks to bottom */
}
```

---

### Use Case 2: Form Layout

```css
.form-row {
  display: flex;
  gap: 20px;
}

.form-row input {
  flex: 1; /* Equal width inputs */
}
```

---

### Use Case 3: Media Object

```css
.media {
  display: flex;
  gap: 20px;
}

.media-image {
  flex: 0 0 100px; /* Fixed 100px width */
}

.media-content {
  flex: 1; /* Takes remaining space */
}
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|----|
| Basic Flexbox | 29+ | 28+ | 9+ | 12+ | 11 |
| `gap` | 84+ | 63+ | 14.1+ | 84+ | ❌ |

**Note:** Flexbox is safe to use. `gap` is modern but has fallbacks (use margins).

---

## Best Practices

### ✅ Do This

1. **Use Flexbox for One-Dimensional Layouts**
   ```css
   /* Good - horizontal or vertical */
   .navbar { display: flex; }
   .sidebar { display: flex; flex-direction: column; }
   ```

2. **Use `gap` for Spacing (Modern)**
   ```css
   /* Good - clean */
   .container {
     display: flex;
     gap: 20px;
   }

   /* Old way - verbose */
   .item {
     margin-right: 20px;
   }
   .item:last-child {
     margin-right: 0;
   }
   ```

3. **Use `flex` Shorthand**
   ```css
   /* Good */
   .item { flex: 1 0 200px; }

   /* Avoid - verbose */
   .item {
     flex-grow: 1;
     flex-shrink: 0;
     flex-basis: 200px;
   }
   ```

---

### ❌ Avoid This

1. **Don't Use Flexbox for Two-Dimensional Layouts**
   ```css
   /* Bad - use CSS Grid instead */
   .complex-grid { display: flex; flex-wrap: wrap; }

   /* Good */
   .complex-grid { display: grid; }
   ```

2. **Don't Forget `flex-wrap` for Responsive**
   ```css
   /* Bad - items may overflow */
   .container { display: flex; }

   /* Good - wraps on small screens */
   .container { display: flex; flex-wrap: wrap; }
   ```

---

## Video Tutorial

**Watch Flexbox:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=7200s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=7200s)

**Timestamps:**
- `2:00:00` - Flexbox introduction
- `2:05:00` - Container properties
- `2:15:00` - Item properties
- `2:25:00` - Practical layouts
- `2:35:00` - Responsive Flexbox

**Resources:**
- [W3Schools - Flexbox](https://www.w3schools.com/css/css3_flexbox.asp)
- [CSS-Tricks - Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [Flexbox Froggy](https://flexboxfroggy.com/) - Interactive game

---

## Related Topics

**Prerequisites:**
- [CSS Box Model](../03-box-model/box-model-concept.md)
- [CSS Display](../05-layout-basics/display.md)

**Related:**
- [Flex Container](flex-container.md)
- [Flex Items](flex-items.md)
- [CSS Grid](../07-grid/grid-intro.md)

---

## Practice Exercise

### 🎯 Challenge: Build a Responsive Card Layout

**Requirements:**
- [ ] 3 equal-width cards in a row
- [ ] Cards wrap to column on mobile
- [ ] Cards have equal height
- [ ] Centered content within cards

<details>
<summary>Click to reveal solution</summary>

**CSS:**
```css
.card-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  padding: 20px;
}

.card {
  flex: 1 1 300px; /* Grow, shrink, min 300px */
  padding: 30px;
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.card h3 {
  margin-bottom: 16px;
  color: #2c3e50;
}

.card p {
  color: #555;
  flex: 1; /* Push button to bottom */
}

.card button {
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 5px;
}
```

</details>

---

**Last Updated:** November 15, 2025
**Category:** Flexbox
**Difficulty:** Intermediate
