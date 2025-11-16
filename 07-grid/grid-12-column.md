---
title: 12-Column Grid System
category: CSS Grid
order: 8
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# 12-Column Grid System

> **Quick Summary:** Build a Bootstrap-style 12-column grid system using CSS Grid. Use `grid-template-columns: repeat(12, 1fr)` and span utilities for flexible, responsive layouts without a framework.

## Table of Contents
- [Introduction](#introduction)
- [Basic 12-Column Setup](#basic-12-column-setup)
- [Column Spanning](#column-spanning)
- [Utility Classes](#utility-classes)
- [Responsive Columns](#responsive-columns)
- [Offset Columns](#offset-columns)
- [Nested Grids](#nested-grids)
- [Gap (Gutters)](#gap-gutters)
- [Bootstrap Comparison](#bootstrap-comparison)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The **12-column grid** is a popular layout system used by frameworks like Bootstrap, Foundation, and Material Design. It divides the page width into 12 equal columns, allowing flexible layouts with fractions like 1/2 (6 columns), 1/3 (4 columns), 1/4 (3 columns), etc.

**Why 12 columns?**
- **Divisible by:** 1, 2, 3, 4, 6, 12
- **Flexible fractions:** halves, thirds, quarters, sixths
- **Industry standard:** Familiar to most developers

**CSS Grid advantages over Bootstrap:**
- No external framework needed
- Cleaner HTML (no `.row` wrappers)
- More flexible (not limited to 12 columns)
- Better performance (less CSS)

---

## Basic 12-Column Setup

**Container:**
```css
.container {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 20px; /* Gutter spacing */
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 15px;
}
```

**Visual:**
```
┌─┬─┬─┬─┬─┬─┬─┬─┬─┬─┬─┬─┐
│1│2│3│4│5│6│7│8│9│10│11│12│
└─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┴─┘
```

Each column is `1fr` (equal width).

---

## Column Spanning

**Use `grid-column: span N`** to span multiple columns.

```css
/* Full width (12 columns) */
.col-12 { grid-column: span 12; }

/* Half width (6 columns) */
.col-6 { grid-column: span 6; }

/* Third width (4 columns) */
.col-4 { grid-column: span 4; }

/* Quarter width (3 columns) */
.col-3 { grid-column: span 3; }

/* Sixth width (2 columns) */
.col-2 { grid-column: span 2; }

/* Twelfth width (1 column) */
.col-1 { grid-column: span 1; }
```

**HTML:**
```html
<div class="container">
  <div class="col-12">Full width</div>
  <div class="col-6">Half</div>
  <div class="col-6">Half</div>
  <div class="col-4">Third</div>
  <div class="col-4">Third</div>
  <div class="col-4">Third</div>
  <div class="col-3">Quarter</div>
  <div class="col-3">Quarter</div>
  <div class="col-3">Quarter</div>
  <div class="col-3">Quarter</div>
</div>
```

**Visual:**
```
┌────────────────────────────┐
│          col-12            │
├──────────────┬─────────────┤
│    col-6     │   col-6     │
├─────────┬────┴────┬────────┤
│  col-4  │  col-4  │ col-4  │
├────┬────┼────┬────┼───┬────┤
│col3│col3│col3│col3│c3 │ c3 │
└────┴────┴────┴────┴───┴────┘
```

---

## Utility Classes

**Complete utility class system:**

```css
/* Container */
.container {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 20px;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 15px;
}

/* Full-width container */
.container-fluid {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 20px;
  padding: 0 15px;
}

/* Column spans */
.col-1 { grid-column: span 1; }
.col-2 { grid-column: span 2; }
.col-3 { grid-column: span 3; }
.col-4 { grid-column: span 4; }
.col-5 { grid-column: span 5; }
.col-6 { grid-column: span 6; }
.col-7 { grid-column: span 7; }
.col-8 { grid-column: span 8; }
.col-9 { grid-column: span 9; }
.col-10 { grid-column: span 10; }
.col-11 { grid-column: span 11; }
.col-12 { grid-column: span 12; }

/* Auto (natural width) */
.col-auto { grid-column: auto; }
```

---

## Responsive Columns

**Breakpoint-based column classes:**

```css
/* Mobile-first approach */

/* Mobile (default) */
.col-1 { grid-column: span 1; }
.col-2 { grid-column: span 2; }
.col-3 { grid-column: span 3; }
.col-4 { grid-column: span 4; }
.col-5 { grid-column: span 5; }
.col-6 { grid-column: span 6; }
.col-7 { grid-column: span 7; }
.col-8 { grid-column: span 8; }
.col-9 { grid-column: span 9; }
.col-10 { grid-column: span 10; }
.col-11 { grid-column: span 11; }
.col-12 { grid-column: span 12; }

/* Tablet (768px+) */
@media (min-width: 768px) {
  .col-md-1 { grid-column: span 1; }
  .col-md-2 { grid-column: span 2; }
  .col-md-3 { grid-column: span 3; }
  .col-md-4 { grid-column: span 4; }
  .col-md-5 { grid-column: span 5; }
  .col-md-6 { grid-column: span 6; }
  .col-md-7 { grid-column: span 7; }
  .col-md-8 { grid-column: span 8; }
  .col-md-9 { grid-column: span 9; }
  .col-md-10 { grid-column: span 10; }
  .col-md-11 { grid-column: span 11; }
  .col-md-12 { grid-column: span 12; }
}

/* Desktop (1024px+) */
@media (min-width: 1024px) {
  .col-lg-1 { grid-column: span 1; }
  .col-lg-2 { grid-column: span 2; }
  .col-lg-3 { grid-column: span 3; }
  .col-lg-4 { grid-column: span 4; }
  .col-lg-5 { grid-column: span 5; }
  .col-lg-6 { grid-column: span 6; }
  .col-lg-7 { grid-column: span 7; }
  .col-lg-8 { grid-column: span 8; }
  .col-lg-9 { grid-column: span 9; }
  .col-lg-10 { grid-column: span 10; }
  .col-lg-11 { grid-column: span 11; }
  .col-lg-12 { grid-column: span 12; }
}
```

**Usage:**
```html
<div class="container">
  <div class="col-12 col-md-6 col-lg-4">
    <!-- Mobile: 12 cols (100%) -->
    <!-- Tablet: 6 cols (50%) -->
    <!-- Desktop: 4 cols (33%) -->
  </div>
</div>
```

---

## Offset Columns

**Push columns with `grid-column-start`:**

```css
/* Offset utilities */
.offset-1 { grid-column-start: 2; }
.offset-2 { grid-column-start: 3; }
.offset-3 { grid-column-start: 4; }
.offset-4 { grid-column-start: 5; }
.offset-5 { grid-column-start: 6; }
.offset-6 { grid-column-start: 7; }
.offset-7 { grid-column-start: 8; }
.offset-8 { grid-column-start: 9; }
.offset-9 { grid-column-start: 10; }
.offset-10 { grid-column-start: 11; }
.offset-11 { grid-column-start: 12; }
```

**Example:**
```html
<div class="container">
  <div class="col-6 offset-3">
    <!-- Centered 6-column div with 3-column margins -->
  </div>
</div>
```

**Visual:**
```
┌───┬───┬───┬───────────────┬───┬───┐
│ 1 │ 2 │ 3 │   col-6       │11 │12 │
│   │   │   │  (offset-3)   │   │   │
└───┴───┴───┴───────────────┴───┴───┘
    ↑
   offset
```

---

## Nested Grids

**Grids inside grids:**

```html
<div class="container">
  <div class="col-8">
    <div class="container"> <!-- Nested grid -->
      <div class="col-6">Nested Half</div>
      <div class="col-6">Nested Half</div>
    </div>
  </div>
  <div class="col-4">Sidebar</div>
</div>
```

**CSS:**
```css
/* Parent grid */
.container {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 20px;
}

/* Nested grids also use 12 columns */
.col-8 > .container {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 15px; /* Smaller gap for nested */
}
```

---

## Gap (Gutters)

**Customize spacing:**

```css
/* Default gap */
.container {
  gap: 20px;
}

/* No gap */
.no-gutters {
  gap: 0;
}

/* Custom gaps */
.gap-sm { gap: 10px; }
.gap-md { gap: 20px; }
.gap-lg { gap: 30px; }
.gap-xl { gap: 40px; }

/* Responsive gaps */
@media (max-width: 768px) {
  .container { gap: 10px; }
}
```

---

## Bootstrap Comparison

### Bootstrap (HTML-heavy)

```html
<div class="container">
  <div class="row">
    <div class="col-md-6">Column 1</div>
    <div class="col-md-6">Column 2</div>
  </div>
  <div class="row">
    <div class="col-md-4">Column 1</div>
    <div class="col-md-4">Column 2</div>
    <div class="col-md-4">Column 3</div>
  </div>
</div>
```

### CSS Grid (Cleaner)

```html
<div class="container">
  <div class="col-md-6">Column 1</div>
  <div class="col-md-6">Column 2</div>
  <div class="col-md-4">Column 1</div>
  <div class="col-md-4">Column 2</div>
  <div class="col-md-4">Column 3</div>
</div>
```

**Advantages:**
- No `.row` wrappers needed
- Less markup
- Automatic wrapping
- Easier to maintain

---

## Examples

### Example 1: Landing Page Hero

```html
<div class="container">
  <div class="col-12 col-lg-6">
    <h1>Welcome to Our Product</h1>
    <p>Amazing features await...</p>
    <button>Get Started</button>
  </div>
  <div class="col-12 col-lg-6">
    <img src="hero.jpg" alt="Hero Image">
  </div>
</div>
```

**Result:**
- **Mobile:** Stacked (12 columns each)
- **Desktop:** Side-by-side (6 columns each)

---

### Example 2: Product Grid

```html
<div class="container">
  <h2 class="col-12">Our Products</h2>
  <div class="col-6 col-md-4 col-lg-3">
    <div class="product-card">Product 1</div>
  </div>
  <div class="col-6 col-md-4 col-lg-3">
    <div class="product-card">Product 2</div>
  </div>
  <div class="col-6 col-md-4 col-lg-3">
    <div class="product-card">Product 3</div>
  </div>
  <div class="col-6 col-md-4 col-lg-3">
    <div class="product-card">Product 4</div>
  </div>
</div>
```

**Result:**
- **Mobile:** 2 per row (6 cols each)
- **Tablet:** 3 per row (4 cols each)
- **Desktop:** 4 per row (3 cols each)

---

### Example 3: Blog Layout

```html
<div class="container">
  <header class="col-12">Header</header>

  <main class="col-12 col-lg-8">
    <article class="col-12">Article 1</article>
    <article class="col-12">Article 2</article>
  </main>

  <aside class="col-12 col-lg-4">
    <div class="widget">Widget 1</div>
    <div class="widget">Widget 2</div>
  </aside>

  <footer class="col-12">Footer</footer>
</div>
```

---

### Example 4: Dashboard Cards

```html
<div class="container">
  <div class="col-12 col-md-6 col-lg-3">
    <div class="stat-card">Total Users</div>
  </div>
  <div class="col-12 col-md-6 col-lg-3">
    <div class="stat-card">Revenue</div>
  </div>
  <div class="col-12 col-md-6 col-lg-3">
    <div class="stat-card">Orders</div>
  </div>
  <div class="col-12 col-md-6 col-lg-3">
    <div class="stat-card">Growth</div>
  </div>

  <div class="col-12 col-lg-8">
    <div class="chart">Sales Chart</div>
  </div>
  <div class="col-12 col-lg-4">
    <div class="recent-activity">Recent Activity</div>
  </div>
</div>
```

**Result:**
- **Mobile:** 1 card per row
- **Tablet:** 2 cards per row
- **Desktop:** 4 cards per row, then 8/4 split for chart/activity

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| CSS Grid | 57+ | 52+ | 10.1+ | 16+ |
| `repeat()` | 57+ | 52+ | 10.1+ | 16+ |
| `gap` | 84+ | 63+ | 14.1+ | 84+ |

**Support:** Excellent (95%+ with fallbacks).

**Fallback for older browsers:**
```css
/* Fallback using grid-gap (older syntax) */
.container {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-gap: 20px; /* Old syntax */
  gap: 20px;      /* Modern syntax */
}
```

---

## Best Practices

### Do This

1. **Use semantic HTML**
   ```html
   <main class="col-8">Content</main>
   <aside class="col-4">Sidebar</aside>
   ```

2. **Mobile-first responsive classes**
   ```html
   <div class="col-12 col-md-6 col-lg-4">
   ```

3. **Use CSS custom properties**
   ```css
   :root {
     --grid-gap: 20px;
     --grid-columns: 12;
   }
   .container { gap: var(--grid-gap); }
   ```

4. **Keep max-width for large screens**
   ```css
   .container { max-width: 1200px; }
   ```

### Avoid This

1. **Don't exceed 12 columns**
   ```html
   <!-- Total > 12, will wrap unexpectedly -->
   <div class="col-8"></div>
   <div class="col-6"></div> <!-- Wraps! -->
   ```

2. **Don't forget gap on mobile**
   ```css
   /* Cramped on mobile */
   gap: 0;

   /* Better */
   gap: 10px;
   @media (min-width: 768px) { gap: 20px; }
   ```

3. **Don't use fixed px widths**
   ```css
   /* Not responsive */
   grid-template-columns: repeat(12, 100px);

   /* Better */
   grid-template-columns: repeat(12, 1fr);
   ```

---

## Related Topics

**Prerequisites:**
- [Grid Container](grid-container.md)
- [Grid Tracks](grid-tracks.md)

**Next Steps:**
- [Responsive Grid](../12-responsive-design/responsive-grid.md)
- [Mobile-First Design](../12-responsive-design/mobile-first.md)

**Compare with:**
- [Flexbox Responsive](../06-flexbox/flex-responsive.md)

---

## Practice Exercise

Create a responsive pricing page with:
- Header (full width)
- 3 pricing cards (stacked on mobile, side-by-side on desktop)
- Features section (2 columns on tablet, 4 columns on desktop)
- Footer (full width)

Use the 12-column grid system with responsive classes.

---

## Navigation

**Previous:** [← Grid Named Areas](grid-named-areas.md)
**Next:** [Components →](../11-components/tables.md)
**Up:** [↑ Back to Grid](../README.md#7️⃣-grid-8-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** CSS Grid
**Difficulty:** Intermediate
