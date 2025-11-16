---
title: Grid Alignment
category: CSS Grid
order: 5
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Grid Alignment

> **Quick Summary:** CSS Grid provides powerful alignment controls for both individual items and the entire grid. Master `justify-items`, `align-items`, `justify-content`, `align-content`, and their item-level overrides.

## Table of Contents
- [Introduction](#introduction)
- [Alignment Axes](#alignment-axes)
- [Container-Level Alignment](#container-level-alignment)
- [justify-items (Horizontal)](#justify-items-horizontal)
- [align-items (Vertical)](#align-items-vertical)
- [place-items (Shorthand)](#place-items-shorthand)
- [justify-content (Grid Horizontal)](#justify-content-grid-horizontal)
- [align-content (Grid Vertical)](#align-content-grid-vertical)
- [place-content (Shorthand)](#place-content-shorthand)
- [Item-Level Alignment](#item-level-alignment)
- [justify-self](#justify-self)
- [align-self](#align-self)
- [place-self (Shorthand)](#place-self-shorthand)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

CSS Grid offers **two levels of alignment**:

1. **Container-level:** Aligns items within grid cells and the grid within the container
2. **Item-level:** Overrides alignment for individual items

**Alignment is critical for:**
- Centering content
- Creating consistent layouts
- Controlling whitespace distribution
- Responsive design patterns

---

## Alignment Axes

Grid has **two axes** for alignment:

```
Block Axis (Vertical)
    ↓
┌─────────────┐
│ ←───────→   │ Inline Axis (Horizontal)
│             │
└─────────────┘
```

**Properties by axis:**
- **Inline (Horizontal):** `justify-*` properties
- **Block (Vertical):** `align-*` properties
- **Both:** `place-*` shorthands

---

## Container-Level Alignment

**Two types of container alignment:**

1. **Items within cells:** How items sit inside their grid areas
   - `justify-items` (horizontal)
   - `align-items` (vertical)
   - `place-items` (shorthand)

2. **Grid within container:** How entire grid sits in container
   - `justify-content` (horizontal)
   - `align-content` (vertical)
   - `place-content` (shorthand)

---

## justify-items (Horizontal)

**Aligns all items horizontally** within their grid cells.

```css
/* Stretch (default) - items fill cell width */
justify-items: stretch;

/* Start - align to left */
justify-items: start;

/* Center - center horizontally */
justify-items: center;

/* End - align to right */
justify-items: end;
```

**Visual:**
```
stretch:    start:      center:     end:
[████████]  [██      ]  [   ██   ]  [      ██]
[████████]  [███     ]  [   ███  ]  [     ███]
```

**Example:**
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 200px);
  justify-items: center; /* All items centered in cells */
}
```

---

## align-items (Vertical)

**Aligns all items vertically** within their grid cells.

```css
/* Stretch (default) - items fill cell height */
align-items: stretch;

/* Start - align to top */
align-items: start;

/* Center - center vertically */
align-items: center;

/* End - align to bottom */
align-items: end;

/* Baseline - align text baselines */
align-items: baseline;
```

**Visual:**
```
stretch:    start:      center:     end:
┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐
│████████│  │██      │  │        │  │        │
│████████│  │        │  │   ██   │  │        │
│████████│  │        │  │        │  │      ██│
└────────┘  └────────┘  └────────┘  └────────┘
```

**Example:**
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 200px;
  align-items: center; /* All items vertically centered */
}
```

---

## place-items (Shorthand)

**Shorthand** for `align-items` + `justify-items`.

```css
/* Syntax: align-items justify-items */
place-items: center center;

/* One value applies to both */
place-items: center; /* Same as: center center */

/* Different values */
place-items: start end; /* Top-right alignment */
```

**Perfect centering:**
```css
.container {
  display: grid;
  place-items: center; /* Center all items vertically & horizontally */
}
```

**Visual:**
```
place-items: center

┌──────────────┐
│              │
│     ██       │
│              │
└──────────────┘
```

---

## justify-content (Grid Horizontal)

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

/* Stretch */
justify-content: stretch;
```

**Visual:**
```
start:     [grid]-------------------
center:    --------[grid]-----------
end:       -------------------[grid]

space-between: [col]-----[col]-----[col]
space-around:  --[col]--[col]--[col]--
space-evenly:  ---[col]---[col]---[col]---
```

**Example:**
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 200px); /* Total 600px */
  width: 1000px; /* Container wider than grid */
  justify-content: center; /* Center grid horizontally */
}
```

---

## align-content (Grid Vertical)

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
  grid-template-rows: repeat(3, 100px); /* Total 300px */
  height: 600px; /* Container taller than grid */
  align-content: center; /* Center grid vertically */
}
```

---

## place-content (Shorthand)

**Shorthand** for `align-content` + `justify-content`.

```css
/* Syntax: align-content justify-content */
place-content: center center;

/* One value applies to both */
place-content: center; /* Same as: center center */

/* Different values */
place-content: space-between center;
```

**Example:**
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 200px);
  grid-template-rows: repeat(2, 150px);
  width: 1000px;
  height: 600px;
  place-content: center; /* Center entire grid in container */
}
```

---

## Item-Level Alignment

**Override container alignment** for individual items using:
- `justify-self` (horizontal)
- `align-self` (vertical)
- `place-self` (shorthand)

---

## justify-self

**Aligns individual item horizontally** within its grid cell.

```css
/* Use container's justify-items (default) */
justify-self: auto;

/* Start */
justify-self: start;

/* Center */
justify-self: center;

/* End */
justify-self: end;

/* Stretch */
justify-self: stretch;
```

**Example:**
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  justify-items: start; /* All items left-aligned */
}

.item-special {
  justify-self: end; /* This item right-aligned */
}
```

---

## align-self

**Aligns individual item vertically** within its grid cell.

```css
/* Use container's align-items (default) */
align-self: auto;

/* Start */
align-self: start;

/* Center */
align-self: center;

/* End */
align-self: end;

/* Stretch */
align-self: stretch;

/* Baseline */
align-self: baseline;
```

**Example:**
```css
.container {
  display: grid;
  grid-auto-rows: 200px;
  align-items: start; /* All items top-aligned */
}

.item-featured {
  align-self: center; /* This item vertically centered */
}
```

---

## place-self (Shorthand)

**Shorthand** for `align-self` + `justify-self`.

```css
/* Syntax: align-self justify-self */
place-self: center center;

/* One value applies to both */
place-self: center; /* Same as: center center */

/* Different values */
place-self: start end; /* Top-right in cell */
```

**Example:**
```css
.item-centered {
  place-self: center; /* Center this item in its cell */
}
```

---

## Examples

### Example 1: Perfect Centering

```css
/* Center single element on page */
body {
  display: grid;
  place-items: center;
  min-height: 100vh;
}

.modal {
  /* Automatically centered */
}
```

---

### Example 2: Card Grid with Centered Content

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  place-items: center; /* Center all cards in cells */
}

.card {
  width: 100%;
  max-width: 350px;
  /* Card content centered in cell */
}
```

---

### Example 3: Dashboard with Mixed Alignment

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 20px;
  align-items: start; /* Default: top-align all widgets */
}

.widget-stat {
  place-self: center; /* Center stat widgets */
}

.widget-chart {
  align-self: stretch; /* Charts fill height */
}
```

---

### Example 4: Form with Label Alignment

```css
.form-row {
  display: grid;
  grid-template-columns: 150px 1fr;
  gap: 15px;
  align-items: center; /* Align labels with inputs */
}

.form-row.textarea {
  align-items: start; /* Textarea labels at top */
}
```

**HTML:**
```html
<div class="form-row">
  <label>Name:</label>
  <input type="text">
</div>

<div class="form-row textarea">
  <label>Message:</label>
  <textarea></textarea>
</div>
```

---

### Example 5: Pricing Cards

```css
.pricing-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
  align-items: end; /* Bottom-align cards (puts CTA buttons at same level) */
}

.pricing-card {
  display: grid;
  grid-template-rows: auto auto 1fr auto;
  /* Header, price, features, CTA button */
}

.pricing-card.featured {
  align-self: center; /* Featured card vertically centered */
}
```

---

### Example 6: Navigation with Logo and Menu

```css
nav {
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: center; /* Vertically center all nav items */
  padding: 20px;
}

.logo {
  justify-self: start; /* Left-align logo */
}

.nav-menu {
  justify-self: center; /* Center menu */
}

.nav-actions {
  justify-self: end; /* Right-align actions */
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge |
|----------|--------|---------|--------|------|
| `justify-items/align-items` | 57+ | 52+ | 10.1+ | 16+ |
| `justify-content/align-content` | 57+ | 52+ | 10.1+ | 16+ |
| `justify-self/align-self` | 57+ | 52+ | 10.1+ | 16+ |
| `place-items/place-content/place-self` | 59+ | 45+ | 11+ | 79+ |

**Support:** Excellent (95%+ global).

---

## Best Practices

### ✅ Do This

1. **Use `place-*` shorthands for brevity**
   ```css
   place-items: center; /* Instead of justify-items + align-items */
   ```

2. **Center elements with Grid (simpler than Flexbox)**
   ```css
   display: grid;
   place-items: center;
   ```

3. **Use `*-self` for exceptions**
   ```css
   .container { align-items: start; }
   .featured { align-self: center; }
   ```

4. **Align baselines for text-heavy layouts**
   ```css
   align-items: baseline; /* Aligns text baselines */
   ```

### ❌ Avoid This

1. **Don't confuse items vs content**
   ```css
   /* Items = align children in cells */
   place-items: center;

   /* Content = align grid in container */
   place-content: center;
   ```

2. **Don't use alignment when stretching is needed**
   ```css
   /* Cards won't fill height */
   align-items: start;

   /* Better for equal-height cards */
   align-items: stretch;
   ```

3. **Don't forget `min-height` for vertical centering**
   ```css
   /* Won't center if no height */
   place-content: center;

   /* Better */
   min-height: 100vh;
   place-content: center;
   ```

---

## Related Topics

**Prerequisites:**
- [Grid Container](grid-container.md)
- [Grid Tracks](grid-tracks.md)

**Next Steps:**
- [Grid Items](grid-items.md)

**Compare with:**
- [Flex Container - Alignment](../06-flexbox/flex-container.md)

---

## Practice Exercise

Create a modal dialog that:
- Centers on the screen
- Has a header (top-aligned)
- Has content (centered)
- Has action buttons (bottom-aligned)

**Hint:** Use nested grids - outer grid centers modal, inner grid aligns sections.

---

## Navigation

**Previous:** [← Grid Gaps](grid-gaps.md)
**Next:** [Grid Items →](grid-items.md)
**Up:** [↑ Back to Grid](../README.md#7️⃣-grid-8-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** CSS Grid
**Difficulty:** Intermediate
