---
title: Grid Named Areas
category: CSS Grid
order: 7
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Grid Named Areas

> **Quick Summary:** Named grid areas create semantic, readable layouts using `grid-template-areas` and `grid-area`. Perfect for defining page layouts like headers, sidebars, and footers with intuitive ASCII-art syntax.

## Table of Contents
- [Introduction](#introduction)
- [Defining Named Areas](#defining-named-areas)
- [Assigning Items to Areas](#assigning-items-to-areas)
- [Creating Layouts](#creating-layouts)
- [Empty Cells](#empty-cells)
- [Responsive Layouts](#responsive-layouts)
- [Complex Patterns](#complex-patterns)
- [Advantages](#advantages)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**Named grid areas** provide a visual, semantic way to define grid layouts using ASCII-art style syntax. Instead of using line numbers, you name regions of your grid and assign items to those regions.

**Why use named areas?**
- **Readable**: Layout structure is visible in CSS
- **Semantic**: Names describe content purpose
- **Maintainable**: Easy to restructure layouts
- **Responsive**: Simple to reorganize for different screen sizes

---

## Defining Named Areas

**Use `grid-template-areas`** on the container to define named regions.

```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: 80px 1fr 60px;
  grid-template-areas:
    "header header header"
    "sidebar content ads"
    "footer footer footer";
}
```

**Visual representation:**
```
┌──────────────────────────┐
│        header            │ 80px
├──────┬───────────┬───────┤
│side  │  content  │  ads  │ 1fr
│bar   │           │       │
├──────┴───────────┴───────┤
│        footer            │ 60px
└──────────────────────────┘
 200px      1fr      200px
```

**Rules:**
- Each row is a string
- Area names separated by spaces
- Same name creates merged cells
- Each row must have same number of cells
- Rectangle shapes only (no L-shapes)

---

## Assigning Items to Areas

**Use `grid-area` property** on items to assign them to named areas.

```css
.header {
  grid-area: header;
}

.sidebar {
  grid-area: sidebar;
}

.content {
  grid-area: content;
}

.ads {
  grid-area: ads;
}

.footer {
  grid-area: footer;
}
```

**HTML:**
```html
<div class="container">
  <header class="header">Header</header>
  <aside class="sidebar">Sidebar</aside>
  <main class="content">Content</main>
  <aside class="ads">Ads</aside>
  <footer class="footer">Footer</footer>
</div>
```

**Note:** HTML order doesn't matter! Grid places items visually based on area names.

---

## Creating Layouts

### Holy Grail Layout

```css
.holy-grail {
  display: grid;
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header header header"
    "left-sidebar content right-sidebar"
    "footer footer footer";
  min-height: 100vh;
  gap: 20px;
}

.header { grid-area: header; }
.left-sidebar { grid-area: left-sidebar; }
.content { grid-area: content; }
.right-sidebar { grid-area: right-sidebar; }
.footer { grid-area: footer; }
```

### App Layout (Header + Nav + Main)

```css
.app {
  display: grid;
  grid-template-columns: 250px 1fr;
  grid-template-rows: 60px 1fr;
  grid-template-areas:
    "header header"
    "sidebar main";
  height: 100vh;
}

.app-header { grid-area: header; }
.app-sidebar { grid-area: sidebar; }
.app-main { grid-area: main; }
```

### Blog Layout

```css
.blog {
  display: grid;
  grid-template-columns: 1fr 300px;
  grid-template-rows: auto auto 1fr auto;
  grid-template-areas:
    "header header"
    "featured featured"
    "posts sidebar"
    "footer footer";
  gap: 30px;
}

.blog-header { grid-area: header; }
.blog-featured { grid-area: featured; }
.blog-posts { grid-area: posts; }
.blog-sidebar { grid-area: sidebar; }
.blog-footer { grid-area: footer; }
```

---

## Empty Cells

**Use dot (`.`) for empty cells.**

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-areas:
    "logo . nav"
    "content content content"
    ". . footer";
}
```

**Visual:**
```
┌──────┬──────┬──────┐
│ logo │ empty│ nav  │
├──────┴──────┴──────┤
│     content        │
├──────┬──────┬──────┤
│ empty│ empty│footer│
└──────┴──────┴──────┘
```

**Multiple dots create multiple empty cells:**
```css
grid-template-areas:
  "header header header"
  ". content ."      /* Content centered with empty sides */
  "footer footer footer";
```

---

## Responsive Layouts

**Reorganize layouts with media queries.**

```css
/* Desktop */
.page {
  display: grid;
  grid-template-columns: 250px 1fr 200px;
  grid-template-areas:
    "header header header"
    "sidebar content ads"
    "footer footer footer";
}

/* Tablet */
@media (max-width: 1024px) {
  .page {
    grid-template-columns: 1fr 250px;
    grid-template-areas:
      "header header"
      "content sidebar"
      "ads ads"
      "footer footer";
  }
}

/* Mobile */
@media (max-width: 768px) {
  .page {
    grid-template-columns: 1fr;
    grid-template-areas:
      "header"
      "content"
      "sidebar"
      "ads"
      "footer";
  }
}
```

**Result:**
- **Desktop**: Traditional 3-column layout
- **Tablet**: 2-column with ads below
- **Mobile**: Single stacked column

---

## Complex Patterns

### Magazine Layout

```css
.magazine {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(4, 200px);
  grid-template-areas:
    "hero hero feature1 feature1"
    "hero hero feature1 feature1"
    "article1 article2 feature2 ad1"
    "article3 article4 feature2 ad2";
  gap: 15px;
}

.hero { grid-area: hero; }
.feature1 { grid-area: feature1; }
.feature2 { grid-area: feature2; }
.article1 { grid-area: article1; }
.article2 { grid-area: article2; }
.article3 { grid-area: article3; }
.article4 { grid-area: article4; }
.ad1 { grid-area: ad1; }
.ad2 { grid-area: ad2; }
```

**Visual:**
```
┌─────────────┬─────────────┐
│             │             │
│    hero     │  feature1   │
│             │             │
├──────┬──────┼──────┬──────┤
│art 1 │art 2 │      │ ad1  │
├──────┼──────┤feat2 ├──────┤
│art 3 │art 4 │      │ ad2  │
└──────┴──────┴──────┴──────┘
```

### Dashboard Grid

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-template-rows: auto auto 1fr;
  grid-template-areas:
    "header header header header header header"
    "stats stats stats stats stats stats"
    "chart1 chart1 chart1 chart2 chart2 chart2"
    "table table table table table table";
  gap: 20px;
}
```

---

## Advantages

### 1. Visual Understanding

```css
/* Clear visual layout in code */
grid-template-areas:
  "header header header"
  "nav content aside"
  "footer footer footer";

/* vs line-based (harder to visualize) */
.header { grid-column: 1 / 4; grid-row: 1; }
.nav { grid-column: 1; grid-row: 2; }
.content { grid-column: 2; grid-row: 2; }
```

### 2. Easy Reorganization

```css
/* Swap sidebar positions by changing one line */
/* Before */
grid-template-areas: "sidebar content";

/* After */
grid-template-areas: "content sidebar";
```

### 3. Semantic Naming

```css
/* Self-documenting */
grid-area: featured-product;  /* Clear purpose */

/* vs */
grid-column: 2 / 4;  /* What is this? */
```

### 4. HTML Order Independence

```html
<!-- HTML order doesn't affect visual layout -->
<div class="container">
  <footer>Footer</footer>  <!-- Appears last visually -->
  <header>Header</header>  <!-- Appears first visually -->
  <main>Content</main>     <!-- Appears middle visually -->
</div>
```

---

## Examples

### Example 1: Landing Page

```css
.landing {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: auto 1fr auto auto auto;
  grid-template-areas:
    "header"
    "hero"
    "features"
    "testimonials"
    "footer";
}

@media (min-width: 768px) {
  .landing {
    grid-template-columns: 1fr 1fr;
    grid-template-areas:
      "header header"
      "hero hero"
      "features features"
      "testimonials testimonials"
      "footer footer";
  }
}
```

---

### Example 2: E-commerce Product Page

```css
.product-page {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: auto 1fr auto auto;
  grid-template-areas:
    "breadcrumb breadcrumb"
    "gallery details"
    "description description"
    "reviews reviews";
  gap: 30px;
}

.breadcrumb { grid-area: breadcrumb; }
.gallery { grid-area: gallery; }
.details { grid-area: details; }
.description { grid-area: description; }
.reviews { grid-area: reviews; }

@media (max-width: 768px) {
  .product-page {
    grid-template-columns: 1fr;
    grid-template-areas:
      "breadcrumb"
      "gallery"
      "details"
      "description"
      "reviews";
  }
}
```

---

### Example 3: Email Client Interface

```css
.email-app {
  display: grid;
  grid-template-columns: 80px 250px 1fr 300px;
  grid-template-rows: 60px 1fr;
  grid-template-areas:
    "icons folders toolbar toolbar"
    "icons folders inbox preview";
  height: 100vh;
  gap: 0;
}

.app-icons { grid-area: icons; background: #2c3e50; }
.folders { grid-area: folders; background: #34495e; }
.toolbar { grid-area: toolbar; background: #ecf0f1; }
.inbox { grid-area: inbox; background: white; }
.preview { grid-area: preview; background: #f8f9fa; }
```

**Visual:**
```
┌────┬────────┬──────────────────────┐
│    │        │      toolbar         │ 60px
│icon│ folder ├──────────┬───────────┤
│s   │  list  │  inbox   │  preview  │ 1fr
│    │        │  list    │  pane     │
└────┴────────┴──────────┴───────────┘
 80px  250px      1fr        300px
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `grid-template-areas` | 57+ | 52+ | 10.1+ | 16+ |
| `grid-area` | 57+ | 52+ | 10.1+ | 16+ |

**Support:** Excellent (95%+ global).

---

## Best Practices

### ✅ Do This

1. **Use semantic area names**
   ```css
   grid-area: main-content; /* Clear */
   /* Not: grid-area: area1; */
   ```

2. **Keep template-areas readable**
   ```css
   grid-template-areas:
     "header header header"
     "nav    main   aside"
     "footer footer footer";
   /* Aligned for visual clarity */
   ```

3. **Match columns/rows to areas**
   ```css
   grid-template-columns: 200px 1fr 200px; /* 3 columns */
   grid-template-areas: "a b c";           /* 3 areas ✓ */
   ```

4. **Use dots for intentional gaps**
   ```css
   grid-template-areas:
     "logo . . . nav";  /* Centered spacing */
   ```

### ❌ Avoid This

1. **Non-rectangular shapes**
   ```css
   /* Invalid - creates L-shape */
   grid-template-areas:
     "header header"
     "sidebar content"
     "sidebar .";  /* sidebar not rectangular! */
   ```

2. **Inconsistent column counts**
   ```css
   /* Invalid */
   grid-template-areas:
     "a b c"    /* 3 cells */
     "d e";     /* 2 cells - ERROR! */
   ```

3. **Vague names**
   ```css
   grid-area: box1;  /* What is this? */
   /* Better: grid-area: product-card; */
   ```

---

## Related Topics

**Prerequisites:**
- [Grid Container](grid-container.md)
- [Grid Items](grid-items.md)

**Next Steps:**
- [12-Column Grid](grid-12-column.md)
- [Responsive Grid](../12-responsive-design/responsive-grid.md)

---

## Practice Exercise

Create a responsive dashboard with:
- Header (full width)
- Sidebar (fixed 250px on desktop, full width on mobile)
- Main content area (flexible)
- Stats panel (300px on desktop, full width on mobile)
- Footer (full width)

Use `grid-template-areas` and reorganize for mobile.

---

## Navigation

**Previous:** [← Grid Items](grid-items.md)
**Next:** [12-Column Grid →](grid-12-column.md)
**Up:** [↑ Back to Grid](../README.md#7️⃣-grid-8-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** CSS Grid
**Difficulty:** Intermediate
