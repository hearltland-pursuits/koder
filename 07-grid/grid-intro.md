---
title: CSS Grid Introduction
category: Grid
order: 1
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Grid Introduction

> **Quick Summary:** CSS Grid is a two-dimensional layout system that lets you create complex layouts with rows AND columns simultaneously. It's the most powerful layout tool in CSS, perfect for page layouts, image galleries, dashboards, and any design requiring precise control over both dimensions.

## Table of Contents
- [Introduction](#introduction)
- [Why CSS Grid Matters](#why-css-grid-matters)
- [Grid vs Flexbox](#grid-vs-flexbox)
- [Basic Grid Syntax](#basic-grid-syntax)
- [Grid Container Properties](#grid-container-properties)
- [Grid Item Properties](#grid-item-properties)
- [Grid Template Areas](#grid-template-areas)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

CSS Grid is the **Swiss Army knife of CSS layout**. Before Grid, creating complex layouts required a patchwork of floats, positioning, and Flexbox. Want a sidebar, main content, and footer? Float the sidebar, position the footer, pray nothing breaks. Want a 12-column magazine layout? Write hundreds of lines of CSS or use a framework like Bootstrap.

CSS Grid changed everything. **It's a true 2D layout system**—you can control rows and columns simultaneously. Define a grid template, place items in cells, span across multiple rows/columns, create gaps, align content—all with intuitive CSS. Grid makes complex layouts simple and responsive layouts effortless.

The magic is in the control. You can create magazine layouts, Pinterest-style masonry grids, dashboard interfaces, card collections, image galleries—anything that needs precise positioning in two dimensions. Grid handles responsive design brilliantly with `auto-fit`, `minmax()`, and fractional units (`fr`). Mobile-first? Desktop-first? Grid adapts. Need to completely restructure layout for different screen sizes? Change the grid template, not the HTML.

**Key Concept:** Grid divides space into rows and columns, creating "cells." You place items into these cells using line numbers, area names, or automatic placement. Think Excel spreadsheet, but for web layout.

---

## Why CSS Grid Matters

### 1. **Two-Dimensional Control**
Flexbox handles one dimension (row OR column). Grid handles both simultaneously.

**Flexbox:**
```css
.container { display: flex; } /* Row OR column, not both */
```

**Grid:**
```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr; /* 3 columns */
  grid-template-rows: 100px 200px;    /* 2 rows */
}
/* Creates 6 cells (3 columns × 2 rows) */
```

### 2. **Complex Layouts Made Simple**

**Common 3-column layout:**

**Before Grid (complex):**
```css
.sidebar { float: left; width: 25%; }
.main { float: left; width: 50%; }
.aside { float: left; width: 25%; }
.clearfix::after { content: ""; display: table; clear: both; }
```

**With Grid (simple):**
```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr; /* 25% 50% 25% */
}
```

### 3. **Responsive Without Media Queries**

**Auto-responsive grid:**
```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}
```

**Result:** Items automatically wrap to fit screen width. No media queries needed!

### 4. **Career Relevance**
- **90%+ of modern projects** use Grid for page layouts
- **Interview question:** "Build a responsive dashboard" → Grid
- **Framework knowledge:** Understanding Grid helps learn Bootstrap Grid, Material-UI Grid
- **Portfolio projects:** Showcase advanced layout skills

---

## Grid vs Flexbox

**When to use each:**

| Layout Need | Use This |
|-------------|----------|
| **Navigation bar** (horizontal items) | Flexbox |
| **Card stack** (vertical items) | Flexbox |
| **Page layout** (header, sidebar, main, footer) | **Grid** |
| **Image gallery** (rows AND columns) | **Grid** |
| **Dashboard** (complex 2D layout) | **Grid** |
| **Centering one item** | Flexbox |
| **Magazine layout** (varied row/column spans) | **Grid** |

**Key difference:**
- **Flexbox:** Content-first (items determine layout)
- **Grid:** Layout-first (grid determines item placement)

**Best practice:** Use both! Grid for overall page structure, Flexbox within grid items.

---

## Basic Grid Syntax

### Step 1: Create Grid Container

```css
.container {
  display: grid; /* Activates Grid */
}
```

**What happens:**
- Direct children become grid items
- Items stack vertically by default (single column)

### Step 2: Define Grid Structure

```css
.container {
  display: grid;
  grid-template-columns: 200px 200px 200px; /* 3 columns, 200px each */
  grid-template-rows: 100px 100px;          /* 2 rows, 100px each */
  gap: 20px;                                /* Space between cells */
}
```

**Result:** Creates a 3×2 grid (6 cells) with 20px gaps.

### Step 3: Place Items (Optional)

```css
.item1 {
  grid-column: 1 / 3; /* Span from column line 1 to 3 (2 columns) */
  grid-row: 1;        /* Row 1 */
}
```

---

## Grid Container Properties

### 1. `grid-template-columns`
**Defines:** Column sizes

**Syntax:**
```css
.grid {
  /* Fixed widths */
  grid-template-columns: 200px 300px 200px;

  /* Fractional units (proportional) */
  grid-template-columns: 1fr 2fr 1fr; /* 25% 50% 25% */

  /* Mixed units */
  grid-template-columns: 200px 1fr 200px; /* Fixed, flexible, fixed */

  /* repeat() function */
  grid-template-columns: repeat(3, 1fr); /* Same as: 1fr 1fr 1fr */

  /* Auto columns */
  grid-template-columns: repeat(auto-fill, 200px); /* As many 200px columns as fit */

  /* Responsive (magic!) */
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  /* Minimum 250px, maximum 1fr, auto-fits to screen */
}
```

---

### 2. `grid-template-rows`
**Defines:** Row sizes (syntax same as columns)

```css
.grid {
  grid-template-rows: 100px 200px 100px;
  grid-template-rows: auto 1fr auto; /* Header, content, footer */
}
```

---

### 3. `gap` (or `grid-gap`)
**Defines:** Space between grid cells

```css
.grid {
  gap: 20px;           /* 20px between all cells */
  gap: 20px 40px;      /* 20px row gap, 40px column gap */
  row-gap: 20px;       /* Only row gap */
  column-gap: 40px;    /* Only column gap */
}
```

---

### 4. `justify-items` and `align-items`
**Controls:** Item alignment within cells

**Horizontal (justify-items):**
```css
.grid {
  justify-items: start;   /* Align left */
  justify-items: center;  /* Align center */
  justify-items: end;     /* Align right */
  justify-items: stretch; /* Default: fill cell width */
}
```

**Vertical (align-items):**
```css
.grid {
  align-items: start;   /* Align top */
  align-items: center;  /* Align middle */
  align-items: end;     /* Align bottom */
  align-items: stretch; /* Default: fill cell height */
}
```

**Shorthand:**
```css
.grid {
  place-items: center; /* justify-items + align-items */
}
```

---

### 5. `justify-content` and `align-content`
**Controls:** Entire grid alignment within container

**Horizontal (justify-content):**
```css
.grid {
  justify-content: start;        /* Align grid left */
  justify-content: center;       /* Center grid */
  justify-content: space-between;
  justify-content: space-around;
  justify-content: space-evenly;
}
```

**Vertical (align-content):**
```css
.grid {
  align-content: start;   /* Align grid top */
  align-content: center;  /* Center grid vertically */
  align-content: end;     /* Align grid bottom */
}
```

---

## Grid Item Properties

### 1. `grid-column` and `grid-row`
**Controls:** Item placement and spanning

**Line-based placement:**
```css
.item {
  grid-column: 1 / 3;   /* Start at line 1, end before line 3 (span 2 columns) */
  grid-row: 1 / 2;      /* Occupy row 1 */
}
```

**Visual:**
```
Column Lines:  1    2    3    4
              ├────┼────┼────┤
Row Line 1 ─  │ A  │ A  │ B  │
              ├────┼────┼────┤
Row Line 2 ─  │ C  │ D  │ E  │
              ├────┼────┼────┤

Item A: grid-column: 1 / 3, grid-row: 1 / 2 (spans 2 columns)
Item B: grid-column: 3 / 4, grid-row: 1 / 2
Item C: grid-column: 1 / 2, grid-row: 2 / 3
```

**Span syntax (alternative):**
```css
.item {
  grid-column: span 2;   /* Span 2 columns from current position */
  grid-row: span 1;      /* Span 1 row */
}
```

**Shorthand:**
```css
.item {
  grid-column: 1 / 3;  /* columns */
  grid-row: 1 / 2;     /* rows */

  /* Or even shorter: */
  grid-area: 1 / 1 / 2 / 3; /* row-start / column-start / row-end / column-end */
}
```

---

### 2. `justify-self` and `align-self`
**Controls:** Individual item alignment (overrides container's `justify-items`/`align-items`)

```css
.item {
  justify-self: center; /* Horizontal alignment */
  align-self: center;   /* Vertical alignment */
}
```

---

## Grid Template Areas

**Semantic grid layout using named areas:**

### Example: Page Layout

```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header  header  header"
    "sidebar main    aside"
    "footer  footer  footer";
  gap: 20px;
  height: 100vh;
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.aside   { grid-area: aside; }
.footer  { grid-area: footer; }
```

**Visual:**
```
┌────────────────────────────┐
│         HEADER             │
├───────┬──────────┬─────────┤
│ SIDE  │   MAIN   │  ASIDE  │
│ BAR   │ CONTENT  │         │
├───────┴──────────┴─────────┤
│         FOOTER             │
└────────────────────────────┘
```

**Responsive with areas:**
```css
@media (max-width: 768px) {
  .container {
    grid-template-columns: 1fr;
    grid-template-areas:
      "header"
      "main"
      "sidebar"
      "aside"
      "footer";
  }
}
```

---

## Examples

### Example 1: Simple 3-Column Layout

```html
<div class="grid">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
  <div class="item">4</div>
  <div class="item">5</div>
  <div class="item">6</div>
</div>
```

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* 3 equal columns */
  gap: 20px;
}

.item {
  background-color: #3498db;
  color: white;
  padding: 40px;
  text-align: center;
  border-radius: 8px;
}
```

---

### Example 2: Responsive Image Gallery

```html
<div class="gallery">
  <img src="1.jpg" alt="Image 1">
  <img src="2.jpg" alt="Image 2">
  <img src="3.jpg" alt="Image 3">
  <!-- More images -->
</div>
```

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
  padding: 20px;
}

.gallery img {
  width: 100%;
  height: 250px;
  object-fit: cover;
  border-radius: 8px;
}
```

**Result:** Images automatically wrap to fit screen width. Minimum 250px per image.

---

### Example 3: Dashboard Layout

```html
<div class="dashboard">
  <header class="header">Header</header>
  <aside class="sidebar">Sidebar</aside>
  <main class="main">Main Content</main>
  <footer class="footer">Footer</footer>
</div>
```

```css
.dashboard {
  display: grid;
  grid-template-columns: 250px 1fr;
  grid-template-rows: 60px 1fr 40px;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
  gap: 20px;
  height: 100vh;
}

.header  { grid-area: header; background: #2c3e50; }
.sidebar { grid-area: sidebar; background: #34495e; }
.main    { grid-area: main; background: #ecf0f1; }
.footer  { grid-area: footer; background: #2c3e50; }
```

---

## Common Use Cases

### Use Case 1: Holy Grail Layout

**Header, footer, sidebar, main, aside:**

```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header header header"
    "nav    main   aside"
    "footer footer footer";
  min-height: 100vh;
}
```

---

### Use Case 2: Card Grid with Featured Item

```css
.grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
}

.featured {
  grid-column: span 2; /* Span 2 columns */
  grid-row: span 2;    /* Span 2 rows */
}
```

---

### Use Case 3: Form Layout

```css
.form {
  display: grid;
  grid-template-columns: 150px 1fr;
  gap: 20px;
  align-items: center;
}

.form label {
  text-align: right;
}

.form input,
.form textarea {
  width: 100%;
}

.form .full-width {
  grid-column: 1 / -1; /* Span all columns */
}
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|----|
| Basic Grid | 57+ | 52+ | 10.1+ | 16+ | ❌ |
| `gap` | 66+ | 61+ | 12+ | 16+ | ❌ |
| `grid-template-areas` | 57+ | 52+ | 10.1+ | 16+ | ❌ |

**Note:** Grid is modern (2017+). IE11 has partial support with `-ms-` prefix (not recommended).

---

## Best Practices

### ✅ Do This

1. **Use Grid for Page Layouts**
   ```css
   .page {
     display: grid;
     grid-template-areas: "header header" "sidebar main" "footer footer";
   }
   ```

2. **Use Fractional Units (`fr`)**
   ```css
   /* Good - flexible */
   grid-template-columns: 1fr 2fr 1fr;

   /* Avoid - fixed */
   grid-template-columns: 25% 50% 25%; /* Doesn't account for gap */
   ```

3. **Use `minmax()` for Responsive**
   ```css
   grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
   ```

4. **Combine Grid + Flexbox**
   ```css
   .page { display: grid; } /* Overall structure */
   .card { display: flex; } /* Card internals */
   ```

---

### ❌ Avoid This

1. **Don't Use Grid for Simple One-Dimensional Layouts**
   ```css
   /* Bad - overkill */
   .navbar { display: grid; grid-auto-flow: column; }

   /* Good - simpler */
   .navbar { display: flex; }
   ```

2. **Don't Forget Fallbacks for Old Browsers (If Needed)**
   ```css
   .grid {
     display: flex; /* Fallback */
     flex-wrap: wrap;
   }

   @supports (display: grid) {
     .grid { display: grid; }
   }
   ```

---

## Video Tutorial

**Watch Grid:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=8400s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=8400s)

**Timestamps:**
- `2:20:00` - Grid introduction
- `2:28:00` - Grid template columns/rows
- `2:38:00` - Grid areas
- `2:48:00` - Responsive Grid
- `2:58:00` - Grid + Flexbox

**Resources:**
- [W3Schools - CSS Grid](https://www.w3schools.com/css/css_grid.asp)
- [CSS-Tricks - Grid Guide](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [Grid Garden](https://cssgridgarden.com/) - Interactive game

---

## Related Topics

**Prerequisites:**
- [CSS Box Model](../03-box-model/box-model-concept.md)
- [Flexbox](../06-flexbox/flexbox-intro.md)

**Related:**
- [Grid Container](grid-container.md)
- [Grid Items](grid-items.md)
- [Responsive Design](../12-responsive-design/media-queries.md)

---

## Practice Exercise

### 🎯 Challenge: Build a Responsive Dashboard

**Requirements:**
- [ ] Header spanning full width
- [ ] Sidebar (fixed 250px)
- [ ] Main content area
- [ ] Footer spanning full width
- [ ] Mobile: Stack vertically

<details>
<summary>Click to reveal solution</summary>

**CSS:**
```css
.dashboard {
  display: grid;
  grid-template-columns: 250px 1fr;
  grid-template-rows: 60px 1fr 40px;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
  gap: 20px;
  min-height: 100vh;
}

.header  { grid-area: header; background: #2c3e50; }
.sidebar { grid-area: sidebar; background: #34495e; }
.main    { grid-area: main; background: #ecf0f1; padding: 20px; }
.footer  { grid-area: footer; background: #2c3e50; }

/* Mobile */
@media (max-width: 768px) {
  .dashboard {
    grid-template-columns: 1fr;
    grid-template-areas:
      "header"
      "main"
      "sidebar"
      "footer";
  }
}
```

</details>

---

**Last Updated:** November 15, 2025
**Category:** Grid
**Difficulty:** Intermediate
