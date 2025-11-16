---
title: CSS Z-Index
category: Layout Basics
order: 3
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Z-Index

> **Quick Summary:** The `z-index` property controls the stacking order of positioned elements (relative, absolute, fixed, sticky). Higher values appear in front of lower values, creating layered layouts like modals, dropdowns, and overlays.

## Table of Contents
- [Introduction](#introduction)
- [How Z-Index Works](#how-z-index-works)
- [Stacking Contexts](#stacking-contexts)
- [Z-Index Values](#z-index-values)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

`z-index` controls the **third dimension** (depth/layering) of elements on a webpage. It determines which elements appear "above" or "below" others when they overlap.

**Key Concept:** `z-index` **only works on positioned elements** (`position: relative`, `absolute`, `fixed`, or `sticky`). It has **no effect** on `position: static` (default).

---

## How Z-Index Works

### Basic Syntax

```css
.element {
  position: relative; /* Required */
  z-index: 10;        /* Stacking order */
}
```

### Default Stacking Order (Without Z-Index)

When elements overlap, browsers use this order (back to front):
1. Background/borders of root element
2. Non-positioned blocks (in HTML order)
3. Positioned elements (in HTML order)

**Example:**
```html
<div class="box1">Box 1 (static)</div>
<div class="box2">Box 2 (absolute)</div>
```

```css
.box1 { background: red; }
.box2 {
  position: absolute;
  top: 20px;
  left: 20px;
  background: blue;
}
```

**Result:** Box 2 (absolute) appears above Box 1 (static) because positioned elements stack above non-positioned ones.

---

## Stacking Contexts

A **stacking context** is a group of elements that share the same layering hierarchy. Key rules:

1. **Root element** (`<html>`) creates a stacking context
2. Elements with `position` + `z-index` create new stacking contexts
3. **Children can't escape** their parent's stacking context

### Example: Parent-Child Constraint

```html
<div class="parent" style="position: relative; z-index: 1;">
  <div class="child" style="position: absolute; z-index: 9999;">
    I can't go above elements outside parent!
  </div>
</div>
<div class="sibling" style="position: relative; z-index: 2;">
  I'm above the child (despite child having z-index: 9999)
</div>
```

**Why:** Parent has `z-index: 1`, sibling has `z-index: 2`. Child is constrained to parent's stacking context.

---

## Z-Index Values

```css
/* Positive integers (higher = front) */
z-index: 1;
z-index: 100;
z-index: 9999;

/* Negative integers (behind parent) */
z-index: -1;

/* Auto (default - uses DOM order) */
z-index: auto;
```

### Common Conventions

```css
/* Layering system */
.background { z-index: -1; }
.content { z-index: 1; }
.dropdown { z-index: 100; }
.modal { z-index: 1000; }
.tooltip { z-index: 2000; }
.notification { z-index: 3000; }
```

---

## Examples

### Example 1: Modal Overlay

```css
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  z-index: 1000;
}

.modal-content {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: white;
  padding: 20px;
  z-index: 1001; /* Above overlay */
}
```

---

### Example 2: Dropdown Menu

```css
.dropdown-container {
  position: relative;
}

.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  background: white;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  z-index: 100; /* Above page content */
}
```

---

### Example 3: Sticky Header Above Content

```css
.header {
  position: sticky;
  top: 0;
  background: white;
  z-index: 50; /* Above scrolling content */
}
```

---

## Common Use Cases

### Use Case 1: Modal/Dialog
```css
.modal {
  position: fixed;
  z-index: 1000;
}
```

### Use Case 2: Dropdown/Tooltip
```css
.dropdown {
  position: absolute;
  z-index: 100;
}
```

### Use Case 3: Fixed Navigation
```css
.navbar {
  position: fixed;
  z-index: 50;
}
```

### Use Case 4: Background Decoration
```css
.bg-decoration {
  position: absolute;
  z-index: -1;
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE 11 |
|----------|--------|---------|--------|------|-------|
| `z-index` | All | All | All | All | Full |

---

## Best Practices

### Do This

1. **Use position property with z-index**
   ```css
   .element {
     position: relative;
     z-index: 10;
   }
   ```

2. **Create a z-index scale**
   ```css
   /* CSS variables for consistency */
   :root {
     --z-background: -1;
     --z-default: 1;
     --z-dropdown: 100;
     --z-sticky: 500;
     --z-modal: 1000;
     --z-tooltip: 2000;
   }
   ```

3. **Use meaningful increments (10, 100, 1000)**
   ```css
   .content { z-index: 10; }
   .dropdown { z-index: 100; }
   .modal { z-index: 1000; }
   ```

### Avoid This

1. **Forgetting position property**
   ```css
   /* Won't work */
   .element { z-index: 10; } /* No position */
   ```

2. **Z-index wars (arbitrarily high values)**
   ```css
   /* Bad */
   .element { z-index: 999999999; }
   ```

3. **Not understanding stacking contexts**

---

## Related Topics

**Prerequisites:**
- [Position Property](position.md)

**Next Steps:**
- [Components](../11-components/navigation-bars.md)

---

## Navigation

**Previous:** [← Alignment](alignment.md)
**Next:** [Filters →](../09-visual-effects/filters.md)
**Up:** [↑ Back to Layout Basics](../README.md#5️⃣-layout-basics-7-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Layout Basics
**Difficulty:** Intermediate
