---
title: Flex Item Properties
category: Flexbox
order: 3
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Flex Item Properties

> **Quick Summary:** Flex item properties control individual child elements within a flex container. Key properties: `flex-grow`, `flex-shrink`, `flex-basis`, `flex` (shorthand), `order`, and `align-self`.

## Table of Contents
- [Introduction](#introduction)
- [flex-grow](#flex-grow)
- [flex-shrink](#flex-shrink)
- [flex-basis](#flex-basis)
- [flex (Shorthand)](#flex-shorthand)
- [order](#order)
- [align-self](#align-self)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

Flex item properties apply to **children** of flex containers, controlling individual sizing, ordering, and alignment.

---

## flex-grow

**How much item grows** relative to siblings when extra space exists.

```css
/* Don't grow (default) */
flex-grow: 0;

/* Grow equally */
flex-grow: 1;

/* Grow twice as much as siblings */
flex-grow: 2;
```

**Example:**
```css
.item-1 { flex-grow: 1; } /* Takes 1 part */
.item-2 { flex-grow: 2; } /* Takes 2 parts (double) */
.item-3 { flex-grow: 1; } /* Takes 1 part */
/* Total: 4 parts (1+2+1) */
```

**Visual:**
```
[Item1: 25%][Item2: 50%][Item3: 25%]
```

---

## flex-shrink

**How much item shrinks** when space is limited.

```css
/* Shrink equally (default) */
flex-shrink: 1;

/* Don't shrink */
flex-shrink: 0;

/* Shrink twice as much */
flex-shrink: 2;
```

**Example:**
```css
.sidebar {
  flex-shrink: 0; /* Sidebar maintains width */
}

.main-content {
  flex-shrink: 1; /* Content shrinks if needed */
}
```

---

## flex-basis

**Initial size** before growing/shrinking (replaces width/height).

```css
/* Auto (default - use content size) */
flex-basis: auto;

/* Fixed size */
flex-basis: 200px;

/* Percentage */
flex-basis: 33.333%;

/* Zero (for pure flex-grow distribution) */
flex-basis: 0;
```

**Example:**
```css
.item {
  flex-basis: 300px; /* Starts at 300px, then grows/shrinks */
}
```

---

## flex (Shorthand)

**Combines grow, shrink, basis** in one property.

```css
/* Syntax */
flex: grow shrink basis;

/* Common patterns */
flex: 1;              /* flex: 1 1 0% */
flex: 0 0 auto;       /* Don't grow/shrink */
flex: 1 0 300px;      /* Grow, don't shrink, start at 300px */
flex: initial;        /* flex: 0 1 auto (default) */
flex: auto;           /* flex: 1 1 auto */
flex: none;           /* flex: 0 0 auto */
```

**Most Common:**
```css
/* Equal width items that fill container */
.item {
  flex: 1; /* Shorthand for flex: 1 1 0% */
}

/* Fixed width, no grow/shrink */
.sidebar {
  flex: 0 0 250px;
}
```

---

## order

**Visual order** of items (doesn't change HTML).

```css
/* Default order */
order: 0;

/* Move to end */
order: 1;

/* Move to start */
order: -1;
```

**Example:**
```css
.item-1 { order: 2; } /* Shows third */
.item-2 { order: 1; } /* Shows second */
.item-3 { order: 0; } /* Shows first */
```

**Result:** Items display as: item-3, item-2, item-1

**Use Case:** Reorder items on mobile without changing HTML.

```css
@media (max-width: 768px) {
  .sidebar { order: 2; } /* Move sidebar below content */
  .main { order: 1; }
}
```

---

## align-self

**Overrides** container's `align-items` for individual item.

```css
/* Use container's align-items (default) */
align-self: auto;

/* Override with specific alignment */
align-self: flex-start;
align-self: center;
align-self: flex-end;
align-self: stretch;
align-self: baseline;
```

**Example:**
```css
.container {
  display: flex;
  align-items: flex-start; /* All items at top */
}

.item-special {
  align-self: center; /* This item centered */
}
```

---

## Examples

### Example 1: Holy Grail Layout

```css
.container {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}

header, footer {
  flex: 0 0 auto; /* Don't grow/shrink */
}

.content-wrapper {
  display: flex;
  flex: 1; /* Takes remaining space */
}

.sidebar {
  flex: 0 0 250px; /* Fixed width */
}

.main-content {
  flex: 1; /* Fills remaining space */
}
```

---

### Example 2: Responsive Card Grid

```css
.card-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.card {
  flex: 1 1 300px; /* Grow, shrink, min 300px */
  max-width: calc(33.333% - 20px); /* Max 3 columns */
}

@media (max-width: 768px) {
  .card {
    flex: 1 1 100%; /* Full width on mobile */
  }
}
```

---

### Example 3: Navigation with Featured Item

```css
nav {
  display: flex;
  gap: 20px;
}

.nav-item {
  flex: 0 0 auto; /* Natural width */
}

.nav-featured {
  flex: 1; /* Takes remaining space */
  margin-left: auto; /* Push to right */
}
```

---

## Best Practices

### ✅ Do This

1. **Use flex shorthand**
   ```css
   .item { flex: 1; }
   ```

2. **Combine with min-width/max-width**
   ```css
   .item {
     flex: 1 1 300px;
     max-width: 500px;
   }
   ```

3. **Use order for mobile reordering**
   ```css
   @media (max-width: 768px) {
     .sidebar { order: 2; }
   }
   ```

### ❌ Avoid This

1. **Using width with flex-basis**
   ```css
   /* Redundant */
   .item {
     flex-basis: 300px;
     width: 300px; /* Remove this */
   }
   ```

2. **Forgetting flex-shrink: 0 for fixed items**
   ```css
   /* Item might shrink unexpectedly */
   .sidebar { width: 250px; }

   /* Better */
   .sidebar { flex: 0 0 250px; }
   ```

---

## Related Topics

**Prerequisites:**
- [Flex Container](flex-container.md)

**Next Steps:**
- [Flex Responsive](flex-responsive.md)

---

## Navigation

**Previous:** [← Flex Container](flex-container.md)
**Next:** [Flex Responsive →](flex-responsive.md)
**Up:** [↑ Back to Flexbox](../README.md#6️⃣-flexbox-4-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Flexbox
**Difficulty:** Intermediate
