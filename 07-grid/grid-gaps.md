---
title: Grid Gaps (Spacing)
category: CSS Grid
order: 4
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Grid Gaps (Spacing)

> **Quick Summary:** Grid gaps create spacing between grid cells without using margins. Use `gap`, `row-gap`, and `column-gap` to control spacing. Modern property that replaced `grid-gap`.

## Table of Contents
- [Introduction](#introduction)
- [gap Property](#gap-property)
- [row-gap](#row-gap)
- [column-gap](#column-gap)
- [Gap vs Margin](#gap-vs-margin)
- [Legacy: grid-gap](#legacy-grid-gap)
- [Responsive Gaps](#responsive-gaps)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**Grid gaps** (also called **gutters**) are the spaces between grid cells. They provide clean spacing without adding margins to individual grid items.

**Benefits:**
- No margin collapse issues
- Simpler than margin management
- No math for negative margins
- Consistent spacing across entire grid

**Visual:**
```
Without gap:          With gap:
[Item][Item][Item]   [Item] [Item] [Item]
[Item][Item][Item]   [Item] [Item] [Item]
```

---

## gap Property

**Shorthand** for row-gap and column-gap.

```css
/* Same gap for rows and columns */
gap: 20px;

/* Different gaps: row column */
gap: 20px 30px; /* 20px between rows, 30px between columns */
```

**Example:**
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px; /* 20px spacing between all cells */
}
```

**Visual:**
```
gap: 20px

[Item] 20px [Item] 20px [Item]
  ↓ 20px
[Item] 20px [Item] 20px [Item]
```

---

## row-gap

**Spacing between rows** only.

```css
/* Fixed spacing */
row-gap: 20px;

/* Relative spacing */
row-gap: 1rem;
row-gap: 2em;

/* Percentage (of container height) */
row-gap: 5%;
```

**Example:**
```css
.list {
  display: grid;
  grid-template-columns: 1fr;
  row-gap: 15px; /* Spacing between list items */
}
```

**Visual:**
```
row-gap: 20px

[Item Item Item]
     ↓ 20px
[Item Item Item]
     ↓ 20px
[Item Item Item]
```

---

## column-gap

**Spacing between columns** only.

```css
/* Fixed spacing */
column-gap: 30px;

/* Relative spacing */
column-gap: 2rem;

/* Percentage (of container width) */
column-gap: 3%;
```

**Example:**
```css
.columns {
  display: grid;
  grid-template-columns: 1fr 1fr;
  column-gap: 40px; /* Space between columns */
}
```

**Visual:**
```
column-gap: 30px

[Item] 30px [Item] 30px [Item]
[Item] 30px [Item] 30px [Item]
```

---

## Gap vs Margin

### Using Gap (Recommended)

```css
.container {
  display: grid;
  gap: 20px;
}

.item {
  /* No margins needed! */
}
```

**Benefits:**
- ✅ No margin on outer edges
- ✅ No need for `:last-child` or `:nth-child` selectors
- ✅ Cleaner, simpler code
- ✅ Works with wrapping grids

### Using Margin (Old Way)

```css
.container {
  display: grid;
  /* Need negative margin to offset item margins */
  margin: -10px;
}

.item {
  margin: 10px;
}
```

**Problems:**
- ❌ Margins on outer edges
- ❌ Complex calculations
- ❌ Negative margin on container required
- ❌ Harder to maintain

**Visual Comparison:**
```
gap:                    margin:
┌────────────────────┐  ┌────────────────────┐
│ [Item] [Item]      │  │→[Item] [Item]←     │
│ [Item] [Item]      │  │→[Item] [Item]←     │
└────────────────────┘  └────────────────────┘
  No outer spacing       Unwanted outer margin
```

---

## Legacy: grid-gap

**Old property name** (deprecated but still works).

```css
/* Old (still works) */
grid-gap: 20px;
grid-row-gap: 20px;
grid-column-gap: 30px;

/* Modern (preferred) */
gap: 20px;
row-gap: 20px;
column-gap: 30px;
```

**Why the change?**
- `gap` works in both Grid AND Flexbox
- Shorter, cleaner syntax
- Consistent across layout methods

**Recommendation:** Use `gap`, `row-gap`, `column-gap` (modern syntax).

---

## Responsive Gaps

**Adjust gaps based on screen size.**

### Using Relative Units

```css
.container {
  display: grid;
  gap: clamp(10px, 2vw, 30px); /* Fluid gap */
}
```

### Using Media Queries

```css
.container {
  display: grid;
  gap: 30px; /* Desktop */
}

@media (max-width: 768px) {
  .container {
    gap: 20px; /* Tablet */
  }
}

@media (max-width: 480px) {
  .container {
    gap: 10px; /* Mobile */
  }
}
```

### Using CSS Variables

```css
:root {
  --gap-desktop: 30px;
  --gap-tablet: 20px;
  --gap-mobile: 10px;
}

.container {
  display: grid;
  gap: var(--gap-desktop);
}

@media (max-width: 768px) {
  :root {
    --gap-desktop: var(--gap-tablet);
  }
}

@media (max-width: 480px) {
  :root {
    --gap-desktop: var(--gap-mobile);
  }
}
```

---

## Examples

### Example 1: Card Grid with Consistent Spacing

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px; /* Simple, consistent spacing */
  padding: 20px;
}

.card {
  background: white;
  border-radius: 8px;
  padding: 20px;
  /* No margins needed! */
}
```

---

### Example 2: Different Row/Column Gaps

```css
.masonry {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  row-gap: 30px;    /* Vertical spacing */
  column-gap: 15px; /* Horizontal spacing */
}
```

**Use case:** Pinterest-style layouts where vertical spacing is typically larger.

---

### Example 3: Dashboard with Section Spacing

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 20px;
}

.widget {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.widget-small { grid-column: span 3; }
.widget-medium { grid-column: span 6; }
.widget-large { grid-column: span 12; }
```

---

### Example 4: Form Layout with Gaps

```css
.form-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px 15px; /* 20px rows, 15px columns */
}

.form-field {
  display: flex;
  flex-direction: column;
}

.form-field.full-width {
  grid-column: 1 / -1; /* Span all columns */
}
```

**HTML:**
```html
<form class="form-grid">
  <div class="form-field">
    <label>First Name</label>
    <input type="text">
  </div>
  <div class="form-field">
    <label>Last Name</label>
    <input type="text">
  </div>
  <div class="form-field full-width">
    <label>Email</label>
    <input type="email">
  </div>
  <div class="form-field full-width">
    <label>Message</label>
    <textarea></textarea>
  </div>
</form>
```

---

### Example 5: Image Gallery with Minimal Gaps

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 5px; /* Minimal spacing for tight gallery */
}

.gallery img {
  width: 100%;
  height: 200px;
  object-fit: cover;
}
```

---

### Example 6: Responsive Gap Scaling

```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));

  /* Fluid gap using clamp */
  gap: clamp(
    10px,  /* Minimum (mobile) */
    3vw,   /* Preferred (scales with viewport) */
    40px   /* Maximum (large screens) */
  );
}
```

**Result:** Gap smoothly scales from 10px on mobile to 40px on desktop.

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge |
|----------|--------|---------|--------|------|
| `gap` (Grid) | 84+ | 63+ | 14.1+ | 84+ |
| `row-gap` (Grid) | 84+ | 63+ | 14.1+ | 84+ |
| `column-gap` (Grid) | 84+ | 63+ | 14.1+ | 84+ |
| `grid-gap` (legacy) | 57+ | 52+ | 10.1+ | 16+ |

**Note:** For older browsers, use `grid-gap` instead of `gap`.

**Fallback:**
```css
.container {
  display: grid;
  grid-gap: 20px; /* Fallback for older browsers */
  gap: 20px;      /* Modern syntax */
}
```

---

## Best Practices

### ✅ Do This

1. **Use modern `gap` syntax**
   ```css
   gap: 20px; /* Not grid-gap */
   ```

2. **Use relative units for scalability**
   ```css
   gap: 1.5rem; /* Scales with base font size */
   ```

3. **Keep gaps consistent across similar layouts**
   ```css
   :root {
     --card-gap: 20px;
   }
   .card-grid { gap: var(--card-gap); }
   ```

4. **Use clamp() for fluid spacing**
   ```css
   gap: clamp(10px, 2vw, 30px);
   ```

### ❌ Avoid This

1. **Don't use margins on grid items for spacing**
   ```css
   /* Bad */
   .item { margin: 10px; }

   /* Good */
   .container { gap: 20px; }
   ```

2. **Don't use excessive gaps**
   ```css
   /* Too much whitespace */
   gap: 100px;

   /* Better */
   gap: 30px;
   ```

3. **Don't forget mobile adjustments**
   ```css
   /* Same 40px gap on mobile can waste space */
   gap: 40px;

   /* Better: responsive */
   gap: clamp(15px, 3vw, 40px);
   ```

---

## Related Topics

**Prerequisites:**
- [Grid Container](grid-container.md)
- [Grid Tracks](grid-tracks.md)

**Next Steps:**
- [Grid Alignment](grid-alignment.md)
- [Grid Items](grid-items.md)

**Compare with:**
- [Box Model - Margins](../03-box-model/margins.md)

---

## Practice Exercise

Create a responsive photo gallery with:
- 4 columns on desktop (>1200px)
- 3 columns on tablet (768px-1199px)
- 2 columns on mobile (480px-767px)
- 1 column on small mobile (<480px)
- Spacing that scales: 30px desktop → 20px tablet → 10px mobile

**Hint:** Use `repeat(auto-fit, minmax(...))` and `clamp()` for gap.

---

## Navigation

**Previous:** [← Grid Tracks](grid-tracks.md)
**Next:** [Grid Alignment →](grid-alignment.md)
**Up:** [↑ Back to Grid](../README.md#7️⃣-grid-8-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** CSS Grid
**Difficulty:** Beginner
