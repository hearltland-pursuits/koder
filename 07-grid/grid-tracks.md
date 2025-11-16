---
title: Grid Tracks (Sizing)
category: CSS Grid
order: 3
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Grid Tracks (Sizing)

> **Quick Summary:** Grid tracks are the rows and columns of your grid. Master sizing with `fr` units, `minmax()`, `auto-fit`, `auto-fill`, and `repeat()` for flexible, responsive layouts without media queries.

## Table of Contents
- [Introduction](#introduction)
- [What are Grid Tracks?](#what-are-grid-tracks)
- [fr Units](#fr-units)
- [minmax() Function](#minmax-function)
- [repeat() Function](#repeat-function)
- [auto-fit vs auto-fill](#auto-fit-vs-auto-fill)
- [Implicit vs Explicit Tracks](#implicit-vs-explicit-tracks)
- [grid-auto-columns & grid-auto-rows](#grid-auto-columns--grid-auto-rows)
- [Track Sizing Keywords](#track-sizing-keywords)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**Grid tracks** are the spaces between grid lines. They define the **size** of rows and columns in your grid layout. Mastering track sizing is essential for creating flexible, responsive designs.

**Two types of tracks:**
1. **Explicit tracks:** Defined by `grid-template-columns` and `grid-template-rows`
2. **Implicit tracks:** Auto-generated when items exceed defined grid

---

## What are Grid Tracks?

A **grid track** is the space between two adjacent grid lines.

```
Grid Lines:     |    |    |    |
                ↓    ↓    ↓    ↓
Grid Tracks:    [T1] [T2] [T3]
                └─┘  └─┘  └─┘
                Col1 Col2 Col3
```

**Example:**
```css
.container {
  display: grid;
  grid-template-columns: 200px 400px 200px; /* 3 column tracks */
  grid-template-rows: 100px 300px;          /* 2 row tracks */
}
```

Creates **3 columns × 2 rows = 6 grid cells**.

---

## fr Units

**Fraction units (`fr`)** distribute available space proportionally.

```css
/* Equal columns */
grid-template-columns: 1fr 1fr 1fr; /* Each gets 33.33% */

/* Unequal distribution */
grid-template-columns: 1fr 2fr 1fr; /* 25% 50% 25% */

/* Mix with fixed widths */
grid-template-columns: 200px 1fr 200px; /* Sidebars + flexible content */
```

**Visual:**
```
1fr 2fr 1fr
[___][______][___]
 25%    50%    25%
```

**How `fr` works:**
1. Fixed sizes are allocated first (`px`, `auto`)
2. Remaining space is divided by total `fr` units
3. Each `fr` gets its proportional share

**Example:**
```css
/* Container is 1000px wide */
grid-template-columns: 200px 1fr 2fr;

/* Calculation:
   200px (fixed) = 200px
   Remaining: 1000px - 200px = 800px
   Total fr units: 1 + 2 = 3
   1fr = 800px / 3 = 266.67px
   2fr = 533.33px
*/
```

---

## minmax() Function

**Sets minimum and maximum track size.**

```css
/* Syntax */
minmax(min, max)

/* Examples */
grid-template-columns: minmax(200px, 1fr); /* Min 200px, max 1fr */
grid-template-columns: minmax(100px, 500px); /* Range */
grid-template-columns: minmax(0, 1fr); /* Allows shrinking to 0 */
grid-template-columns: minmax(auto, 1fr); /* Content-based min */
```

**Common Patterns:**

```css
/* Responsive cards (min 300px, max flexible) */
grid-template-columns: repeat(3, minmax(300px, 1fr));

/* Sidebar (min 200px, max 250px) */
grid-template-columns: minmax(200px, 250px) 1fr;

/* Content-based min, flexible max */
grid-template-columns: minmax(auto, 1fr) minmax(auto, 1fr);
```

**Visual:**
```
minmax(300px, 1fr)

Wide screen:    [___flexible___]
Narrow screen:  [300px minimum]
```

---

## repeat() Function

**Repeats track definitions** without rewriting.

```css
/* Syntax */
repeat(count, track-list)

/* Instead of this: */
grid-template-columns: 1fr 1fr 1fr 1fr;

/* Write this: */
grid-template-columns: repeat(4, 1fr);

/* Complex patterns */
grid-template-columns: repeat(3, 100px 200px); /* 100px 200px 100px 200px 100px 200px */

/* With minmax */
grid-template-columns: repeat(4, minmax(200px, 1fr));
```

**Named lines with repeat:**
```css
grid-template-columns: repeat(3, [col-start] 1fr [col-end]);
```

---

## auto-fit vs auto-fill

**Creates responsive grids** that adapt to container width.

### auto-fill

**Fills row with as many tracks as possible** (even empty ones).

```css
grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
```

**Behavior:**
- Creates as many 200px columns as fit
- Keeps empty tracks if items don't fill all columns
- Items stay at min-width (200px)

**Visual (container 1000px, 4 items):**
```
auto-fill:
[200px][200px][200px][200px][empty]
   1      2      3      4
```

### auto-fit

**Fits tracks to container** by expanding items.

```css
grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
```

**Behavior:**
- Creates tracks as needed
- Collapses empty tracks (0px width)
- Items expand to fill available space (up to 1fr max)

**Visual (container 1000px, 4 items):**
```
auto-fit:
[250px][250px][250px][250px]
   1      2      3      4    (expanded to fill)
```

### When to Use Which?

| Use Case | Choice |
|----------|--------|
| Items should grow to fill space | `auto-fit` |
| Items should stay minimum size | `auto-fill` |
| Gallery with consistent sizing | `auto-fill` |
| Cards that expand on wide screens | `auto-fit` |

**Example:**
```css
/* Cards expand on wide screens */
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
}

/* Images stay consistent size */
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 10px;
}
```

---

## Implicit vs Explicit Tracks

### Explicit Tracks

**Defined explicitly** in CSS.

```css
grid-template-columns: 1fr 1fr 1fr; /* 3 explicit columns */
grid-template-rows: 100px 200px;    /* 2 explicit rows */
```

### Implicit Tracks

**Auto-generated** when items exceed defined grid.

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr; /* Only 2 columns defined */
  /* But if you have 7 items: */
}
```

**Visual:**
```
[1][2]  ← Explicit row 1
[3][4]  ← Implicit row 2 (auto-generated)
[5][6]  ← Implicit row 3 (auto-generated)
[7][ ]  ← Implicit row 4 (auto-generated)
```

---

## grid-auto-columns & grid-auto-rows

**Controls size of implicit tracks.**

```css
/* Default (auto) */
grid-auto-rows: auto; /* Height based on content */

/* Fixed size */
grid-auto-rows: 200px; /* All implicit rows are 200px */

/* Flexible size */
grid-auto-rows: 1fr; /* Equal height rows */

/* With minmax */
grid-auto-rows: minmax(100px, auto); /* Min 100px, max content */
```

**Example:**
```css
.masonry {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 150px; /* Each row is 150px */
  gap: 10px;
}
```

**With grid-auto-flow:**
```css
.horizontal-scroll {
  display: grid;
  grid-template-rows: 200px; /* Only 1 row */
  grid-auto-flow: column;    /* Items flow into columns */
  grid-auto-columns: 300px;  /* Each column is 300px */
  overflow-x: auto;
}
```

---

## Track Sizing Keywords

```css
/* auto - Size based on content */
grid-template-columns: auto 1fr auto;

/* min-content - Smallest size without overflow */
grid-template-columns: min-content 1fr;

/* max-content - Largest size based on content */
grid-template-columns: max-content 1fr;

/* fit-content() - Clamps to max size */
grid-template-columns: fit-content(500px) 1fr;
```

**Visual Examples:**

```css
/* min-content */
grid-template-columns: min-content 1fr;
/*
[Hello]  [Remaining space...........]
└─ Wraps at narrowest word
*/

/* max-content */
grid-template-columns: max-content 1fr;
/*
[Hello World This Is Long Text]  [Rest]
└─ No wrapping, full width
*/

/* auto */
grid-template-columns: auto 1fr;
/*
[Content fits]  [Remaining space.....]
└─ Natural size based on content
*/
```

---

## Examples

### Example 1: Responsive Card Grid (No Media Queries)

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
}
```

**Result:**
- Wide screen (1200px+): 4 cards per row
- Medium screen (900px): 3 cards per row
- Tablet (600px): 2 cards per row
- Mobile (400px): 1 card per row

---

### Example 2: Holy Grail Layout

```css
.holy-grail {
  display: grid;
  grid-template-columns: minmax(200px, 250px) 1fr minmax(200px, 250px);
  grid-template-rows: auto 1fr auto;
  min-height: 100vh;
}
```

**Result:**
- Left sidebar: 200px min, 250px max
- Content: Flexible (takes remaining space)
- Right sidebar: 200px min, 250px max

---

### Example 3: Masonry-Style Grid

```css
.masonry {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  grid-auto-rows: 150px;
  gap: 15px;
}

.item-tall {
  grid-row: span 2; /* Spans 2 rows */
}

.item-wide {
  grid-column: span 2; /* Spans 2 columns */
}
```

---

### Example 4: Dashboard Grid

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(12, 1fr); /* 12-column system */
  gap: 20px;
}

.widget-small { grid-column: span 3; } /* 25% width */
.widget-medium { grid-column: span 6; } /* 50% width */
.widget-large { grid-column: span 12; } /* 100% width */
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `fr` units | 57+ | 52+ | 10.1+ | 16+ |
| `minmax()` | 57+ | 52+ | 10.1+ | 16+ |
| `repeat()` | 57+ | 52+ | 10.1+ | 16+ |
| `auto-fit/auto-fill` | 57+ | 52+ | 10.1+ | 16+ |
| `grid-auto-rows/columns` | 57+ | 52+ | 10.1+ | 16+ |
| `min-content/max-content` | 57+ | 52+ | 10.1+ | 16+ |

**Support:** Excellent (95%+ global).

---

## Best Practices

### ✅ Do This

1. **Use `fr` for flexible layouts**
   ```css
   grid-template-columns: 1fr 2fr 1fr;
   ```

2. **Combine `repeat()` with `minmax()`**
   ```css
   grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
   ```

3. **Set reasonable min/max values**
   ```css
   minmax(250px, 1fr) /* Content won't break on mobile */
   ```

4. **Use `grid-auto-rows` for consistent implicit sizing**
   ```css
   grid-auto-rows: minmax(100px, auto);
   ```

### ❌ Avoid This

1. **Too-small minimum sizes**
   ```css
   /* Breaks on mobile */
   minmax(50px, 1fr)

   /* Better */
   minmax(300px, 1fr)
   ```

2. **Fixed widths without flexibility**
   ```css
   /* Not responsive */
   grid-template-columns: 300px 300px 300px;

   /* Better */
   grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
   ```

3. **Forgetting `minmax()` with `auto-fit/auto-fill`**
   ```css
   /* Won't work as expected */
   repeat(auto-fit, 1fr)

   /* Correct */
   repeat(auto-fit, minmax(300px, 1fr))
   ```

---

## Related Topics

**Prerequisites:**
- [Grid Container](grid-container.md)

**Next Steps:**
- [Grid Gaps](grid-gaps.md)
- [Grid Alignment](grid-alignment.md)

**Deep Dive:**
- [12-Column Grid](grid-12-column.md) - Bootstrap-style system

---

## Practice Exercise

Create a responsive product grid that:
- Shows 4 products per row on desktop
- Automatically adjusts to 3, 2, or 1 column on smaller screens
- Each product card is minimum 280px wide
- Uses no media queries

**Hint:** `repeat(auto-fit, minmax(280px, 1fr))`

---

## Navigation

**Previous:** [← Grid Container](grid-container.md)
**Next:** [Grid Gaps →](grid-gaps.md)
**Up:** [↑ Back to Grid](../README.md#7️⃣-grid-8-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** CSS Grid
**Difficulty:** Intermediate
