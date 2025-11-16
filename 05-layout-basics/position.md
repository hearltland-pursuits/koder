---
title: CSS Position Property
category: Layout Basics
order: 2
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Position Property

> **Quick Summary:** The `position` property controls how elements are placed on the page. It offers five positioning methods: static (default), relative (offset from normal position), absolute (positioned relative to parent), fixed (positioned relative to viewport), and sticky (hybrid of relative and fixed).

## Table of Contents
- [Introduction](#introduction)
- [Why Positioning Matters](#why-positioning-matters)
- [Position Values](#position-values)
- [Static Positioning (Default)](#static-positioning-default)
- [Relative Positioning](#relative-positioning)
- [Absolute Positioning](#absolute-positioning)
- [Fixed Positioning](#fixed-positioning)
- [Sticky Positioning](#sticky-positioning)
- [Z-Index and Stacking](#z-index-and-stacking)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

Imagine building with LEGO blocks. **Static positioning** is like stacking blocks in order—each piece sits where you place it in the sequence. **Relative positioning** is like nudging a block slightly left or right while keeping its spot in the stack. **Absolute positioning** is like lifting a block out of the stack entirely and placing it anywhere on the baseplate. **Fixed positioning** is like attaching a block to your hand—it stays in place even as you move the baseplate. **Sticky positioning** is a block that acts normal until you scroll, then "sticks" to a spot.

The `position` property breaks elements out of the normal document flow, giving you surgical control over layout. Want a navigation bar that stays visible while scrolling? `position: fixed`. Want a badge overlay on a product image? `position: absolute`. Want a table header that sticks when scrolling? `position: sticky`.

Understanding positioning is essential for modern layouts: modals, dropdowns, tooltips, sticky headers, overlays, and complex UI components all depend on strategic use of positioning. Master these five values, and you can build any layout imaginable.

**Key Concept:** Position changes how an element is placed, and how it interacts with other elements. It works with four offset properties: `top`, `right`, `bottom`, `left`.

---

## Why Positioning Matters

### 1. **Layout Control**
Positioning lets you place elements precisely:
- **Fixed headers/footers** that stay visible while scrolling
- **Centered modals** overlaying the page
- **Tooltips** appearing next to UI elements
- **Badges** overlaying images

### 2. **Breaking Normal Flow**
The normal flow stacks elements vertically (block) or horizontally (inline). Positioning lets you break this flow and place elements anywhere.

### 3. **Layering (Z-Index)**
Positioned elements can be layered on top of each other using `z-index`. This creates depth and hierarchy.

### 4. **Career Relevance**
Positioning appears in every front-end interview:
- "Explain the difference between relative and absolute positioning"
- "How would you create a sticky header?"
- "What is z-index and when do you use it?"

---

## Position Values

| Value | Behavior | Use Case |
|-------|----------|----------|
| `static` | Default; follows normal flow | Regular content |
| `relative` | Offset from normal position, maintains space | Nudging elements, positioning context |
| `absolute` | Removed from flow, positioned relative to nearest positioned ancestor | Overlays, badges, dropdowns |
| `fixed` | Removed from flow, positioned relative to viewport | Sticky headers, floating buttons |
| `sticky` | Toggles between relative and fixed based on scroll | Table headers, sticky nav |

---

## Static Positioning (Default)

**Value:** `position: static;`

**Behavior:**
- Elements follow the normal document flow
- `top`, `right`, `bottom`, `left` properties have **no effect**
- This is the default—you rarely need to explicitly set it

### Example

```css
.static-box {
  position: static; /* Default (unnecessary to specify) */
  background-color: #3498db;
  padding: 20px;
}
```

**When to use:** You don't—elements are static by default. You might use it to override another position value.

---

## Relative Positioning

**Value:** `position: relative;`

**Behavior:**
- Element remains in normal flow (space is reserved)
- Can be offset from its normal position using `top`, `right`, `bottom`, `left`
- Other elements are NOT affected by the offset

### Example

```html
<div class="box box1">Box 1</div>
<div class="box box2">Box 2 (Relative)</div>
<div class="box box3">Box 3</div>
```

```css
.box {
  padding: 20px;
  background-color: #3498db;
  margin-bottom: 10px;
}

.box2 {
  position: relative;
  left: 50px;  /* Move 50px to the right */
  top: 20px;   /* Move 20px down */
  background-color: #e74c3c;
}
```

**Result:**
- Box 2 is visually shifted 50px right and 20px down
- The space where Box 2 *would* have been is still reserved
- Box 3 doesn't move—it sits in its normal position

### Common Uses

1. **Nudging elements slightly**
   ```css
   .icon {
     position: relative;
     top: 2px; /* Align icon with text baseline */
   }
   ```

2. **Creating a positioning context for absolute children**
   ```css
   .card {
     position: relative; /* Now absolute children position relative to this */
   }

   .badge {
     position: absolute;
     top: 10px;
     right: 10px;
   }
   ```

---

## Absolute Positioning

**Value:** `position: absolute;`

**Behavior:**
- Element is **removed from normal flow** (no space reserved)
- Positioned relative to the nearest **positioned ancestor** (any ancestor with `position` other than `static`)
- If no positioned ancestor exists, positioned relative to the `<html>` element
- Uses `top`, `right`, `bottom`, `left` for placement

### Example

```html
<div class="container">
  <div class="box absolute-box">Absolutely Positioned</div>
</div>
```

```css
.container {
  position: relative; /* Positioning context */
  width: 400px;
  height: 300px;
  background-color: #ecf0f1;
  border: 2px solid #333;
}

.absolute-box {
  position: absolute;
  top: 20px;    /* 20px from top of .container */
  right: 20px;  /* 20px from right of .container */
  background-color: #e74c3c;
  padding: 20px;
}
```

**Result:** The box is positioned 20px from the top-right corner of `.container`.

### Key Rules

1. **Finds nearest positioned ancestor**
   ```css
   /* absolute-box positions relative to .parent */
   .parent {
     position: relative;
   }

   .absolute-box {
     position: absolute;
     top: 0;
     left: 0;
   }
   ```

2. **If no positioned ancestor, uses viewport**
   ```css
   /* No parent has position set */
   .absolute-box {
     position: absolute;
     top: 0;  /* Top of the entire page */
     left: 0; /* Left of the entire page */
   }
   ```

### Common Uses

**Badge on image:**
```css
.product-card {
  position: relative;
}

.sale-badge {
  position: absolute;
  top: 10px;
  left: 10px;
  background-color: red;
  color: white;
  padding: 5px 10px;
}
```

**Centered modal:**
```css
.modal {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%); /* Center perfectly */
}
```

---

## Fixed Positioning

**Value:** `position: fixed;`

**Behavior:**
- Element is **removed from normal flow**
- Positioned relative to the **viewport** (browser window)
- Stays in place when scrolling
- Uses `top`, `right`, `bottom`, `left` for placement

### Example

```html
<header class="fixed-header">
  <nav>Navigation Bar</nav>
</header>
```

```css
.fixed-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: #2c3e50;
  color: white;
  padding: 20px;
  z-index: 1000; /* Ensure it's on top */
}

/* Add padding to body so content isn't hidden under header */
body {
  padding-top: 70px; /* Height of fixed header */
}
```

**Result:** The header stays at the top of the viewport, even when scrolling.

### Common Uses

**Sticky navigation:**
```css
.nav {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 100;
}
```

**Floating action button:**
```css
.fab {
  position: fixed;
  bottom: 20px;
  right: 20px;
  width: 60px;
  height: 60px;
  border-radius: 50%;
  background-color: #3498db;
}
```

**Modal overlay:**
```css
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7);
}
```

---

## Sticky Positioning

**Value:** `position: sticky;`

**Behavior:**
- Acts like `relative` until the user scrolls to a threshold
- Then acts like `fixed` (sticks to the specified position)
- Requires at least one of: `top`, `right`, `bottom`, `left`
- Only sticks within its parent container

### Example

```html
<table>
  <thead>
    <tr class="sticky-header">
      <th>Name</th>
      <th>Email</th>
      <th>Status</th>
    </tr>
  </thead>
  <tbody>
    <!-- Many rows -->
  </tbody>
</table>
```

```css
.sticky-header {
  position: sticky;
  top: 0; /* Stick to top of viewport when scrolling */
  background-color: #2c3e50;
  color: white;
}
```

**Result:** As you scroll the table, the header row sticks to the top of the viewport.

### Common Uses

**Sticky section headers:**
```css
.section-header {
  position: sticky;
  top: 60px; /* Stick 60px from top (below main nav) */
  background-color: white;
  z-index: 10;
}
```

**Sidebar that follows scroll:**
```css
.sidebar {
  position: sticky;
  top: 20px; /* Stick 20px from top */
  height: fit-content;
}
```

---

## Z-Index and Stacking

**Property:** `z-index`

**Purpose:** Controls the stacking order of positioned elements (which element appears on top).

**Rules:**
- Only works on **positioned elements** (`position` other than `static`)
- Higher `z-index` values appear on top
- Default `z-index` is `auto` (effectively `0`)

### Example

```html
<div class="box red">Z-Index: 1</div>
<div class="box blue">Z-Index: 2</div>
<div class="box green">Z-Index: 3</div>
```

```css
.box {
  position: absolute;
  width: 200px;
  height: 200px;
  padding: 20px;
  color: white;
}

.red {
  background-color: red;
  top: 0;
  left: 0;
  z-index: 1;
}

.blue {
  background-color: blue;
  top: 50px;
  left: 50px;
  z-index: 2; /* Appears above red */
}

.green {
  background-color: green;
  top: 100px;
  left: 100px;
  z-index: 3; /* Appears above blue */
}
```

**Result:** Green box appears on top, then blue, then red.

### Common Z-Index Values

```css
/* Standard layering hierarchy */
.page-content     { z-index: 1; }
.dropdown-menu    { z-index: 100; }
.modal-overlay    { z-index: 1000; }
.modal-content    { z-index: 1001; }
.tooltip          { z-index: 2000; }
.notification     { z-index: 3000; }
```

---

## Examples

### Example 1: Image Card with Badge

```html
<div class="card">
  <img src="product.jpg" alt="Product">
  <span class="badge">NEW</span>
  <h3>Product Name</h3>
</div>
```

```css
.card {
  position: relative; /* Positioning context */
  width: 300px;
  border: 1px solid #ddd;
  border-radius: 8px;
  overflow: hidden;
}

.card img {
  width: 100%;
  display: block;
}

.badge {
  position: absolute;
  top: 10px;
  right: 10px;
  background-color: #e74c3c;
  color: white;
  padding: 5px 12px;
  border-radius: 4px;
  font-weight: bold;
  z-index: 10;
}
```

---

### Example 2: Fixed Navigation + Sticky Sidebar

```html
<header class="main-nav">Navigation</header>
<div class="content-wrapper">
  <aside class="sidebar">Sidebar (Sticky)</aside>
  <main class="content">Main Content</main>
</div>
```

```css
.main-nav {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 60px;
  background-color: #2c3e50;
  z-index: 1000;
}

.content-wrapper {
  margin-top: 60px; /* Account for fixed nav */
  display: flex;
}

.sidebar {
  position: sticky;
  top: 80px; /* Stick below nav (60px + 20px gap) */
  width: 250px;
  height: fit-content;
  padding: 20px;
  background-color: #ecf0f1;
}

.content {
  flex: 1;
  padding: 20px;
}
```

---

## Common Use Cases

### Use Case 1: Centered Modal

```css
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 2000;
}

.modal-content {
  position: relative; /* For close button */
  background-color: white;
  padding: 40px;
  border-radius: 8px;
  max-width: 500px;
}

.close-button {
  position: absolute;
  top: 10px;
  right: 10px;
  cursor: pointer;
}
```

---

### Use Case 2: Tooltip

```css
.tooltip-container {
  position: relative;
  display: inline-block;
}

.tooltip {
  position: absolute;
  bottom: 100%; /* Above the element */
  left: 50%;
  transform: translateX(-50%); /* Center horizontally */
  background-color: #333;
  color: white;
  padding: 8px 12px;
  border-radius: 4px;
  white-space: nowrap;
  opacity: 0;
  transition: opacity 0.3s;
  z-index: 1000;
}

.tooltip-container:hover .tooltip {
  opacity: 1;
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE |
|----------|--------|---------|--------|------|----|
| `static`, `relative`, `absolute`, `fixed` | 1+ | 1+ | 1+ | 12+ | 4+ |
| `sticky` | 56+ | 32+ | 13+ | 16+ | ❌ No |
| `z-index` | 1+ | 1+ | 1+ | 12+ | 4+ |

**Note:** `position: sticky` is modern. Use fallbacks for older browsers.

---

## Best Practices

### ✅ Do This

1. **Use Relative Parent for Absolute Children**
   ```css
   .parent {
     position: relative; /* Positioning context */
   }

   .child {
     position: absolute;
     top: 0;
     right: 0;
   }
   ```

2. **Account for Fixed Element Height**
   ```css
   .fixed-header {
     position: fixed;
     height: 60px;
   }

   body {
     padding-top: 60px; /* Prevent content hiding */
   }
   ```

3. **Use Z-Index Hierarchies**
   ```css
   /* Define clear z-index scale */
   :root {
     --z-dropdown: 100;
     --z-modal: 1000;
     --z-tooltip: 2000;
   }
   ```

---

### ❌ Avoid This

1. **Don't Forget Positioning Context**
   ```css
   /* Bad - absolute positions relative to viewport */
   .card { /* No position set */ }
   .badge { position: absolute; }

   /* Good - positions relative to .card */
   .card { position: relative; }
   .badge { position: absolute; }
   ```

2. **Don't Use Excessive Z-Index**
   ```css
   /* Bad - z-index arms race */
   .modal { z-index: 999999; }

   /* Good - reasonable hierarchy */
   .modal { z-index: 1000; }
   ```

---

## Video Tutorial

**Watch Positioning:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=5400s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=5400s)

**Timestamps:**
- `1:30:00` - Position property overview
- `1:35:00` - Relative vs Absolute
- `1:42:00` - Fixed positioning
- `1:48:00` - Sticky positioning
- `1:55:00` - Z-index stacking

**Resources:**
- [W3Schools - Position](https://www.w3schools.com/css/css_positioning.asp)
- [MDN - Position](https://developer.mozilla.org/en-US/docs/Web/CSS/position)

---

## Related Topics

**Prerequisites:**
- [CSS Box Model](../03-box-model/box-model-concept.md)

**Related:**
- [Z-Index](z-index.md)
- [Flexbox](../06-flexbox/flexbox-intro.md)
- [Grid](../07-grid/grid-intro.md)

---

## Practice Exercise

### 🎯 Challenge: Build a Fixed Header with Sticky Sidebar

**Requirements:**
- [ ] Fixed navigation bar at top
- [ ] Sticky sidebar that follows scroll
- [ ] Absolute-positioned badge on card
- [ ] Proper z-index layering

<details>
<summary>Click to reveal solution</summary>

**CSS:**
```css
.nav {
  position: fixed;
  top: 0;
  width: 100%;
  height: 60px;
  background: #2c3e50;
  z-index: 100;
}

body {
  padding-top: 60px;
}

.sidebar {
  position: sticky;
  top: 80px;
  width: 250px;
}

.card {
  position: relative;
}

.badge {
  position: absolute;
  top: 10px;
  right: 10px;
  z-index: 10;
}
```

</details>

---

**Last Updated:** November 15, 2025
**Category:** Layout Basics
**Difficulty:** Intermediate
