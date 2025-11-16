---
title: Grid Item Properties
category: CSS Grid
order: 6
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Grid Item Properties

> **Quick Summary:** Grid item properties control how individual elements position themselves within the grid. Key properties: `grid-column`, `grid-row`, `grid-area`, and `span` keyword for sizing.

## Table of Contents
- [Introduction](#introduction)
- [grid-column](#grid-column)
- [grid-row](#grid-row)
- [grid-area](#grid-area)
- [Spanning Cells](#spanning-cells)
- [Line-Based Placement](#line-based-placement)
- [Named Lines](#named-lines)
- [Named Areas](#named-areas)
- [Stacking Items](#stacking-items)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**Grid item properties** control **where** and **how much space** items occupy in the grid. Unlike container properties, these are applied to **grid children**.

**Grid items can:**
- Span multiple columns/rows
- Position themselves at specific grid lines
- Overlap other items (with z-index)
- Reference named grid areas

---

## grid-column

**Controls horizontal position and span** of item.

```css
/* Syntax */
grid-column: start / end;

/* Examples */
grid-column: 1 / 3; /* Start at line 1, end before line 3 (spans 2 columns) */
grid-column: 2 / 4; /* Columns 2-3 */
grid-column: 1 / -1; /* Span all columns (start to end) */
grid-column: span 2; /* Span 2 columns from auto placement */
```

**Visual:**
```
Grid Lines:  1    2    3    4
             |    |    |    |
grid-column: 1 / 3
             [____]
             Spans columns 1-2
```

**Longhand properties:**
```css
/* Instead of shorthand */
grid-column: 2 / 4;

/* You can use longhand */
grid-column-start: 2;
grid-column-end: 4;
```

---

## grid-row

**Controls vertical position and span** of item.

```css
/* Syntax */
grid-row: start / end;

/* Examples */
grid-row: 1 / 3; /* Rows 1-2 */
grid-row: 2 / 5; /* Rows 2-4 */
grid-row: 1 / -1; /* Span all rows */
grid-row: span 3; /* Span 3 rows */
```

**Visual:**
```
Grid Lines:
1 ──────────
  |        |
2 ──────────
  |        | grid-row: 1 / 3
3 ──────────  (Spans rows 1-2)
  |        |
4 ──────────
```

**Longhand properties:**
```css
/* Instead of shorthand */
grid-row: 2 / 5;

/* You can use longhand */
grid-row-start: 2;
grid-row-end: 5;
```

---

## grid-area

**Shorthand** for grid-row-start + grid-column-start + grid-row-end + grid-column-end.

```css
/* Syntax: row-start / column-start / row-end / column-end */
grid-area: 1 / 1 / 3 / 3;

/* Or reference named area */
grid-area: header;
```

**Visual:**
```
grid-area: 1 / 1 / 3 / 3

  1    2    3
1 [________]
2 [________]
3
```

**Example:**
```css
.item {
  grid-area: 1 / 2 / 3 / 4;
  /* Rows 1-2, Columns 2-3 */
}
```

---

## Spanning Cells

**Use `span` keyword** to span multiple columns/rows without knowing exact line numbers.

```css
/* Span specific number of columns */
grid-column: span 2; /* Spans 2 columns */
grid-column: span 3; /* Spans 3 columns */

/* Span specific number of rows */
grid-row: span 2; /* Spans 2 rows */

/* Combine with explicit start */
grid-column: 2 / span 3; /* Start at column 2, span 3 columns */
grid-row: 1 / span 2; /* Start at row 1, span 2 rows */
```

**Example (12-column grid):**
```css
.col-6 {
  grid-column: span 6; /* Half width (6 of 12 columns) */
}

.col-4 {
  grid-column: span 4; /* Third width (4 of 12 columns) */
}

.col-12 {
  grid-column: span 12; /* Full width */
}
```

---

## Line-Based Placement

**Position items using grid line numbers.**

```css
/* Grid with 4 columns has 5 lines:
   1    2    3    4    5
   |    |    |    |    |
*/

.item {
  grid-column: 2 / 4; /* Columns 2-3 */
}
```

**Negative numbers** count from the end:
```css
grid-column: 1 / -1; /* First line to last line (full width) */
grid-column: -3 / -1; /* Last 2 columns */
```

**Visual:**
```
Positive lines:  1    2    3    4    5
                 |    |    |    |    |
Negative lines: -5   -4   -3   -2   -1

grid-column: 1 / -1  spans entire width
grid-column: -3 / -1 spans last 2 columns
```

---

## Named Lines

**Name grid lines** for semantic placement.

```css
/* Define named lines */
.container {
  grid-template-columns: [main-start] 1fr [content-start] 3fr [content-end] 1fr [main-end];
}

/* Use named lines */
.item {
  grid-column: content-start / content-end;
}
```

**Multiple names per line:**
```css
.container {
  grid-template-columns: [sidebar-start] 250px [sidebar-end main-start] 1fr [main-end];
}

.sidebar {
  grid-column: sidebar-start / sidebar-end;
}

.main {
  grid-column: main-start / main-end;
}
```

---

## Named Areas

**Assign items to named grid areas.**

**Container defines areas:**
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

**Items reference areas:**
```css
.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.content { grid-area: content; }
.ads { grid-area: ads; }
.footer { grid-area: footer; }
```

**Visual:**
```
┌──────────────────────────┐
│        header            │
├──────┬───────────┬───────┤
│side  │  content  │  ads  │
│bar   │           │       │
├──────┴───────────┴───────┤
│        footer            │
└──────────────────────────┘
```

---

## Stacking Items

**Grid items can overlap** using same grid cells.

```css
.item1 {
  grid-area: 1 / 1 / 3 / 3;
  z-index: 1; /* Behind */
}

.item2 {
  grid-area: 2 / 2 / 4 / 4;
  z-index: 2; /* In front */
}
```

**Visual:**
```
┌─────────┐
│ Item 1  │
│    ┌────┼─────┐
│    │Item│2    │
└────┼────┘     │
     │          │
     └──────────┘
```

**Use cases:**
- Image overlays
- Badge notifications
- Decorative elements
- Hero sections with text over images

**Example:**
```css
.hero {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 1fr;
}

.hero-image {
  grid-area: 1 / 1 / 2 / 2;
  z-index: 1;
}

.hero-text {
  grid-area: 1 / 1 / 2 / 2;
  z-index: 2;
  place-self: center; /* Center text over image */
}
```

---

## Examples

### Example 1: Magazine Layout

```css
.magazine {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-auto-rows: 150px;
  gap: 15px;
}

.featured {
  grid-column: span 4; /* Wide feature */
  grid-row: span 2;    /* Tall */
}

.article {
  grid-column: span 2; /* Standard article */
}

.sidebar-ad {
  grid-column: span 2; /* Sidebar width */
  grid-row: span 3;    /* Tall ad */
}
```

---

### Example 2: Dashboard Widgets

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 20px;
}

.widget-small {
  grid-column: span 3; /* 25% width */
}

.widget-medium {
  grid-column: span 6; /* 50% width */
}

.widget-large {
  grid-column: span 12; /* Full width */
}

.widget-tall {
  grid-row: span 2; /* Double height */
}
```

**HTML:**
```html
<div class="dashboard">
  <div class="widget-large">Chart</div>
  <div class="widget-medium">Stats</div>
  <div class="widget-medium">Activity</div>
  <div class="widget-small">Stat 1</div>
  <div class="widget-small">Stat 2</div>
  <div class="widget-small">Stat 3</div>
  <div class="widget-small">Stat 4</div>
</div>
```

---

### Example 3: Holy Grail Layout

```css
.holy-grail {
  display: grid;
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header header header"
    "left content right"
    "footer footer footer";
  min-height: 100vh;
}

.header { grid-area: header; }
.left-sidebar { grid-area: left; }
.content { grid-area: content; }
.right-sidebar { grid-area: right; }
.footer { grid-area: footer; }

/* Mobile */
@media (max-width: 768px) {
  .holy-grail {
    grid-template-columns: 1fr;
    grid-template-areas:
      "header"
      "content"
      "left"
      "right"
      "footer";
  }
}
```

---

### Example 4: Image Gallery with Feature

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 200px;
  gap: 10px;
}

.gallery-item:first-child {
  grid-column: span 2; /* First item is featured */
  grid-row: span 2;
}
```

---

### Example 5: Card with Overlapping Badge

```css
.card {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 200px 1fr;
}

.card-image {
  grid-area: 1 / 1 / 2 / 2;
}

.card-badge {
  grid-area: 1 / 1 / 2 / 2;
  place-self: start end; /* Top-right corner */
  z-index: 2;
  background: red;
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
  margin: 10px;
}

.card-content {
  grid-area: 2 / 1 / 3 / 2;
}
```

---

### Example 6: Asymmetric Layout

```css
.asymmetric {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-auto-rows: 200px;
  gap: 15px;
}

.item:nth-child(1) { grid-column: span 4; grid-row: span 2; }
.item:nth-child(2) { grid-column: span 2; }
.item:nth-child(3) { grid-column: span 2; }
.item:nth-child(4) { grid-column: span 3; }
.item:nth-child(5) { grid-column: span 3; }
.item:nth-child(6) { grid-column: span 6; }
```

**Result:** Pinterest/Masonry-style asymmetric layout.

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge |
|----------|--------|---------|--------|------|
| `grid-column/grid-row` | 57+ | 52+ | 10.1+ | 16+ |
| `grid-area` | 57+ | 52+ | 10.1+ | 16+ |
| `span` keyword | 57+ | 52+ | 10.1+ | 16+ |
| Named lines | 57+ | 52+ | 10.1+ | 16+ |
| Named areas | 57+ | 52+ | 10.1+ | 16+ |

**Support:** Excellent (95%+ global).

---

## Best Practices

### Do This

1. **Use `span` for flexible sizing**
   ```css
   grid-column: span 6; /* Better than hardcoded 1 / 7 */
   ```

2. **Use `1 / -1` for full width**
   ```css
   grid-column: 1 / -1; /* Works regardless of column count */
   ```

3. **Use named areas for semantic layouts**
   ```css
   grid-template-areas:
     "header header"
     "sidebar content";
   ```

4. **Use z-index when stacking**
   ```css
   .overlay {
     grid-area: 1 / 1;
     z-index: 2;
   }
   ```

### Avoid This

1. **Hardcoding line numbers unnecessarily**
   ```css
   /* Fragile */
   grid-column: 3 / 7;

   /* Better (if you want to span 4 columns) */
   grid-column: span 4;
   ```

2. **Forgetting z-index when stacking**
   ```css
   /* Items overlap but stacking order is unpredictable */
   .item1 { grid-area: 1 / 1; }
   .item2 { grid-area: 1 / 1; }

   /* Better */
   .item1 { grid-area: 1 / 1; z-index: 1; }
   .item2 { grid-area: 1 / 1; z-index: 2; }
   ```

3. **Overusing explicit placement**
   ```css
   /* Too rigid */
   .item1 { grid-column: 1 / 2; }
   .item2 { grid-column: 2 / 3; }
   .item3 { grid-column: 3 / 4; }

   /* Better: let auto-placement work */
   /* Just define column size if needed */
   ```

---

## Related Topics

**Prerequisites:**
- [Grid Container](grid-container.md)
- [Grid Tracks](grid-tracks.md)
- [Grid Alignment](grid-alignment.md)

**Next Steps:**
- [Grid Named Areas](grid-named-areas.md)
- [12-Column Grid](grid-12-column.md)

**Compare with:**
- [Flex Items](../06-flexbox/flex-items.md)

---

## Practice Exercise

Create a blog post layout with:
- Full-width header
- Main content (2/3 width on desktop)
- Sidebar (1/3 width on desktop)
- Full-width footer
- On mobile: Stack header, content, sidebar, footer

**Hint:** Use `grid-template-areas` and media queries.

---

## Navigation

**Previous:** [← Grid Alignment](grid-alignment.md)
**Next:** [Grid Named Areas →](grid-named-areas.md)
**Up:** [↑ Back to Grid](../README.md#7️⃣-grid-8-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** CSS Grid
**Difficulty:** Intermediate
