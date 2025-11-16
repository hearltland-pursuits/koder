---
title: Flex Container Properties
category: Flexbox
order: 2
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Flex Container Properties

> **Quick Summary:** Flex container properties control how flex items are arranged, aligned, and spaced within the parent element. Key properties: `flex-direction`, `flex-wrap`, `justify-content`, `align-items`, and `align-content`.

## Table of Contents
- [Introduction](#introduction)
- [display: flex](#display-flex)
- [flex-direction](#flex-direction)
- [flex-wrap](#flex-wrap)
- [justify-content](#justify-content)
- [align-items](#align-items)
- [align-content](#align-content)
- [gap](#gap)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The **flex container** is the parent element with `display: flex`. It controls the overall layout of its children (flex items).

---

## display: flex

**Activates flexbox** on an element.

```css
.container {
  display: flex; /* Block-level flex container */
}

.inline-container {
  display: inline-flex; /* Inline-level flex container */
}
```

---

## flex-direction

**Controls main axis direction** (row or column).

```css
/* Horizontal (default) */
flex-direction: row; /* Left to right → */

/* Horizontal reversed */
flex-direction: row-reverse; /* Right to left ← */

/* Vertical */
flex-direction: column; /* Top to bottom ↓ */

/* Vertical reversed */
flex-direction: column-reverse; /* Bottom to top ↑ */
```

**Example:**
```css
.container {
  display: flex;
  flex-direction: column; /* Stack items vertically */
}
```

---

## flex-wrap

**Controls wrapping** when items overflow container.

```css
/* No wrap (default) - items shrink to fit */
flex-wrap: nowrap;

/* Wrap to next line */
flex-wrap: wrap;

/* Wrap in reverse direction */
flex-wrap: wrap-reverse;
```

**Example:**
```css
.container {
  display: flex;
  flex-wrap: wrap; /* Items wrap to multiple rows */
}

.item {
  flex: 0 0 300px; /* Min width 300px, will wrap */
}
```

---

## justify-content

**Aligns items along main axis** (horizontal in row, vertical in column).

```css
/* Start (default) */
justify-content: flex-start;

/* End */
justify-content: flex-end;

/* Center */
justify-content: center;

/* Space between (first/last at edges) */
justify-content: space-between;

/* Space around (equal space around each) */
justify-content: space-around;

/* Space evenly (equal space everywhere) */
justify-content: space-evenly;
```

**Visual:**
```
flex-start:   [1][2][3]--------
center:       ----[1][2][3]----
flex-end:     --------[1][2][3]
space-between:[1]----[2]----[3]
space-around: -[1]--[2]--[3]-
space-evenly: --[1]--[2]--[3]--
```

---

## align-items

**Aligns items along cross axis** (vertical in row, horizontal in column).

```css
/* Stretch (default) */
align-items: stretch; /* Items fill container height */

/* Start */
align-items: flex-start;

/* Center */
align-items: center;

/* End */
align-items: flex-end;

/* Baseline (align text baselines) */
align-items: baseline;
```

**Common Pattern (Perfect Centering):**
```css
.container {
  display: flex;
  justify-content: center; /* Horizontal center */
  align-items: center;     /* Vertical center */
  height: 100vh;
}
```

---

## align-content

**Aligns multiple rows/columns** (only works with `flex-wrap: wrap`).

```css
/* Stretch (default) */
align-content: stretch;

/* Start */
align-content: flex-start;

/* Center */
align-content: center;

/* Space between rows */
align-content: space-between;

/* Space around rows */
align-content: space-around;
```

**Note:** No effect unless items wrap to multiple lines.

---

## gap

**Spacing between flex items** (modern property).

```css
/* Both row and column gap */
gap: 20px;

/* Separate row/column gaps */
row-gap: 20px;
column-gap: 30px;

/* Shorthand */
gap: 20px 30px; /* row column */
```

**Example:**
```css
.container {
  display: flex;
  gap: 20px; /* 20px space between all items */
}
```

**Older Alternative (if gap not supported):**
```css
.container {
  display: flex;
  margin: -10px; /* Negative margin */
}

.item {
  margin: 10px; /* Positive margin */
}
```

---

## Examples

### Example 1: Navigation Bar

```css
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background: #333;
}

nav .logo {
  font-size: 1.5rem;
  color: white;
}

nav ul {
  display: flex;
  gap: 30px;
  list-style: none;
}
```

---

### Example 2: Card Grid

```css
.card-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}

.card {
  flex: 0 0 calc(33.333% - 20px); /* 3 columns */
  min-width: 300px; /* Responsive breakpoint */
}
```

---

### Example 3: Hero Section

```css
.hero {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  text-align: center;
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
}
```

---

## Best Practices

### ✅ Do This

1. **Use gap for spacing**
   ```css
   .container { display: flex; gap: 20px; }
   ```

2. **Combine justify-content and align-items for centering**
   ```css
   display: flex;
   justify-content: center;
   align-items: center;
   ```

3. **Use flex-wrap for responsive layouts**
   ```css
   flex-wrap: wrap;
   ```

### ❌ Avoid This

1. **Forgetting display: flex**
2. **Using align-content without flex-wrap**
3. **Confusing main/cross axis**

---

## Related Topics

**Prerequisites:**
- [Flexbox Introduction](flexbox-intro.md)

**Next Steps:**
- [Flex Items](flex-items.md)
- [Flex Responsive](flex-responsive.md)

---

## Navigation

**Previous:** [← Flexbox Introduction](flexbox-intro.md)
**Next:** [Flex Items →](flex-items.md)
**Up:** [↑ Back to Flexbox](../README.md#6️⃣-flexbox-4-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Flexbox
**Difficulty:** Intermediate
