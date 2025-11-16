---
title: Grid Container Properties
category: CSS Grid
order: 2
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Grid Container Properties

> **Quick Summary:** Grid container properties define the structure of a CSS Grid layout. Key properties: `display: grid`, `grid-template-columns`, `grid-template-rows`, `grid-template-areas`, `grid-auto-flow`, and spacing properties.

## Table of Contents
- [Introduction](#introduction)
- [display: grid](#display-grid)
- [grid-template-columns](#grid-template-columns)
- [grid-template-rows](#grid-template-rows)
- [grid-template-areas](#grid-template-areas)
- [grid-auto-flow](#grid-auto-flow)
- [justify-items](#justify-items)
- [align-items](#align-items)
- [place-items](#place-items)
- [justify-content](#justify-content)
- [align-content](#align-content)
- [place-content](#place-content)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The **grid container** is the parent element with `display: grid`. It establishes a grid formatting context for its children (grid items) and controls the overall structure, sizing, and alignment of the grid.

**Grid containers control:**
- Number and size of columns/rows
- Spacing between grid cells (gaps)
- Alignment of items within cells
- Alignment of the entire grid within container
- Automatic placement of items

---

## display: grid

**Activates CSS Grid** on an element.

```css
.container {
  display: grid; /* Block-level grid container */
}

.inline-container {
  display: inline-grid; /* Inline-level grid container */
}
```

**Effect:**
- Direct children become grid items
- Grid items participate in grid layout
- Content is arranged in rows and columns

---

## grid-template-columns

**Defines column structure** of the grid.

```css
/* Fixed widths */
grid-template-columns: 200px 200px 200px;

/* Flexible with fr units */
grid-template-columns: 1fr 2fr 1fr; /* 25% 50% 25% */

/* Mix fixed and flexible */
grid-template-columns: 250px 1fr 250px; /* Sidebar, content, sidebar */

/* Auto sizing */
grid-template-columns: auto 1fr auto;

/* Repeat notation */
grid-template-columns: repeat(3, 1fr); /* 3 equal columns */
grid-template-columns: repeat(4, 200px); /* 4 fixed columns */

/* Auto-fit (responsive) */
grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));

/* Auto-fill (fills with empty tracks) */
grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));

/* Named lines */
grid-template-columns: [start] 1fr [middle] 1fr [end];
```

**Visual:**
```
1fr 2fr 1fr
[___][______][___]
25%    50%    25%
```

---

## grid-template-rows

**Defines row structure** of the grid.

```css
/* Fixed heights */
grid-template-rows: 100px 200px 100px;

/* Flexible with fr units */
grid-template-rows: 1fr 2fr 1fr;

/* Auto height based on content */
grid-template-rows: auto auto auto;

/* Mix approaches */
grid-template-rows: 80px 1fr 60px; /* Header, content, footer */

/* Repeat notation */
grid-template-rows: repeat(3, 200px);

/* Min/max sizing */
grid-template-rows: repeat(3, minmax(100px, auto));

/* Named lines */
grid-template-rows: [header-start] 80px [header-end content-start] 1fr [content-end footer-start] 60px [footer-end];
```

**Common Pattern (Full-Height Layout):**
```css
.container {
  display: grid;
  grid-template-rows: 80px 1fr 60px; /* Header, main, footer */
  min-height: 100vh;
}
```

---

## grid-template-areas

**Creates named grid areas** for semantic layout.

```css
/* Define areas */
grid-template-areas:
  "header header header"
  "sidebar content content"
  "footer footer footer";

/* Items reference these areas */
.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.content { grid-area: content; }
.footer { grid-area: footer; }
```

**Visual:**
```
┌─────────────────────┐
│      header         │
├──────┬──────────────┤
│side  │   content    │
│bar   │              │
├──────┴──────────────┤
│      footer         │
└─────────────────────┘
```

**Empty cells** with dot notation:
```css
grid-template-areas:
  "logo nav nav"
  ". content content"
  ". content content";
```

---

## grid-auto-flow

**Controls automatic placement** of grid items.

```css
/* Row by row (default) */
grid-auto-flow: row;

/* Column by column */
grid-auto-flow: column;

/* Dense packing (fills gaps) */
grid-auto-flow: row dense;
grid-auto-flow: column dense;
```

**Example:**
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-flow: row; /* Items fill rows left-to-right */
}
```

**Visual (row vs column):**
```
row:          column:
[1][2][3]     [1][4][7]
[4][5][6]     [2][5][8]
[7][8][9]     [3][6][9]
```

**Dense Packing:**
```css
/* Without dense - leaves gaps */
grid-auto-flow: row;
/*
[1][2][gap]
[3][4][5]
*/

/* With dense - fills gaps */
grid-auto-flow: row dense;
/*
[1][2][3]
[4][5][ ]
*/
```

---

## justify-items

**Aligns items horizontally** (inline axis) within their grid cells.

```css
/* Stretch (default) */
justify-items: stretch; /* Items fill cell width */

/* Start */
justify-items: start; /* Align to left */

/* Center */
justify-items: center; /* Center horizontally */

/* End */
justify-items: end; /* Align to right */
```

**Visual:**
```
stretch:    start:      center:     end:
[████████]  [██      ]  [   ██   ]  [      ██]
[████████]  [███     ]  [   ███  ]  [     ███]
```

---

## align-items

**Aligns items vertically** (block axis) within their grid cells.

```css
/* Stretch (default) */
align-items: stretch; /* Items fill cell height */

/* Start */
align-items: start; /* Align to top */

/* Center */
align-items: center; /* Center vertically */

/* End */
align-items: end; /* Align to bottom */

/* Baseline */
align-items: baseline; /* Align text baselines */
```

**Common Pattern (Perfect Centering):**
```css
.container {
  display: grid;
  justify-items: center; /* Horizontal center */
  align-items: center;   /* Vertical center */
}
```

---

## place-items

**Shorthand** for justify-items + align-items.

```css
/* Syntax: align-items justify-items */
place-items: center center;

/* One value applies to both */
place-items: center; /* Same as: center center */

/* Different values */
place-items: start end; /* Top-right alignment */
```

**Example:**
```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(3, 200px);
  place-items: center; /* Center all cards in cells */
}
```

---

## justify-content

**Aligns entire grid horizontally** within container (when grid is smaller than container).

```css
/* Start (default) */
justify-content: start;

/* Center */
justify-content: center;

/* End */
justify-content: end;

/* Space between */
justify-content: space-between;

/* Space around */
justify-content: space-around;

/* Space evenly */
justify-content: space-evenly;
```

**Visual:**
```
start:    [grid]-------------
center:   ------[grid]-------
end:      -------------[grid]
space-between: [col]---[col]---[col]
space-evenly:  --[col]--[col]--[col]--
```

---

## align-content

**Aligns entire grid vertically** within container (when grid is smaller than container).

```css
/* Start (default) */
align-content: start;

/* Center */
align-content: center;

/* End */
align-content: end;

/* Space between */
align-content: space-between;

/* Space around */
align-content: space-around;

/* Space evenly */
align-content: space-evenly;

/* Stretch */
align-content: stretch;
```

**Example:**
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 200px);
  height: 600px;
  align-content: center; /* Center grid vertically */
}
```

---

## place-content

**Shorthand** for align-content + justify-content.

```css
/* Syntax: align-content justify-content */
place-content: center center;

/* One value applies to both */
place-content: center; /* Same as: center center */

/* Different values */
place-content: space-between center;
```

---

## Examples

### Example 1: Responsive Card Grid

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  padding: 20px;
}

.card {
  background: white;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}
```

**Result:** Cards automatically wrap to new rows when screen gets smaller.

---

### Example 2: Dashboard Layout

```css
.dashboard {
  display: grid;
  grid-template-columns: 250px 1fr;
  grid-template-rows: 80px 1fr 60px;
  grid-template-areas:
    "header header"
    "sidebar content"
    "footer footer";
  min-height: 100vh;
  gap: 20px;
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.content { grid-area: content; }
.footer { grid-area: footer; }
```

**Visual:**
```
┌────────────────────────┐
│       header (80px)    │
├──────┬─────────────────┤
│side  │   content       │
│bar   │   (1fr)         │
│250px │                 │
├──────┴─────────────────┤
│       footer (60px)    │
└────────────────────────┘
```

---

### Example 3: Image Gallery

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  grid-auto-rows: 200px;
  gap: 10px;
}

.gallery-item {
  overflow: hidden;
  border-radius: 8px;
}

.gallery-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```

**Result:** Auto-responsive gallery that fills available width.

---

### Example 4: Holy Grail Layout

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
}

@media (max-width: 768px) {
  .holy-grail {
    grid-template-columns: 1fr;
    grid-template-areas:
      "header"
      "content"
      "left-sidebar"
      "right-sidebar"
      "footer";
  }
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge |
|----------|--------|---------|--------|------|
| `display: grid` | 57+ | 52+ | 10.1+ | 16+ |
| `grid-template-columns/rows` | 57+ | 52+ | 10.1+ | 16+ |
| `grid-template-areas` | 57+ | 52+ | 10.1+ | 16+ |
| `gap` (replaces grid-gap) | 84+ | 63+ | 14.1+ | 84+ |
| `auto-fit/auto-fill` | 57+ | 52+ | 10.1+ | 16+ |
| `place-items/place-content` | 59+ | 45+ | 11+ | 79+ |

**Note:** Grid support is excellent in all modern browsers (95%+ global support).

---

## Best Practices

### Do This

1. **Use fr units for flexible layouts**
   ```css
   grid-template-columns: 1fr 2fr 1fr;
   ```

2. **Use repeat() for repetition**
   ```css
   grid-template-columns: repeat(3, 1fr);
   ```

3. **Use auto-fit/auto-fill for responsive grids**
   ```css
   grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
   ```

4. **Use named areas for semantic layouts**
   ```css
   grid-template-areas:
     "header header"
     "sidebar content"
     "footer footer";
   ```

5. **Combine with gap property**
   ```css
   display: grid;
   gap: 20px;
   ```

### Avoid This

1. **Too many explicit rows/columns**
   ```css
   /* Hard to maintain */
   grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr;

   /* Better */
   grid-template-columns: repeat(6, 1fr);
   ```

2. **Fixed widths without minmax**
   ```css
   /* Breaks on mobile */
   grid-template-columns: 300px 300px 300px;

   /* Better */
   grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
   ```

3. **Forgetting min-height for full-height layouts**
   ```css
   /* Grid might not fill viewport */
   grid-template-rows: 80px 1fr 60px;

   /* Better */
   grid-template-rows: 80px 1fr 60px;
   min-height: 100vh;
   ```

---

## Related Topics

**Prerequisites:**
- [Grid Introduction](grid-intro.md)

**Next Steps:**
- [Grid Tracks](grid-tracks.md)
- [Grid Gaps](grid-gaps.md)
- [Grid Alignment](grid-alignment.md)
- [Grid Items](grid-items.md)

**Compare with:**
- [Flex Container](../06-flexbox/flex-container.md) - 1D layout alternative

---

## Practice Exercise

Create a responsive blog layout with:
- Header (full width)
- Sidebar (250px on desktop, full width on mobile)
- Main content (flexible)
- Footer (full width)

**Hint:** Use `grid-template-areas` and media queries.

---

## Navigation

**Previous:** [← Grid Introduction](grid-intro.md)
**Next:** [Grid Tracks →](grid-tracks.md)
**Up:** [↑ Back to Grid](../README.md#7️⃣-grid-8-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** CSS Grid
**Difficulty:** Intermediate
