---
title: CSS Opacity
category: Visual Effects
order: 8
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Opacity

> **Quick Summary:** The `opacity` property controls the transparency level of an element and its children. Values range from `0` (fully transparent) to `1` (fully opaque). Unlike `rgba()`, opacity affects the entire element including text and children.

## Table of Contents
- [Introduction](#introduction)
- [Opacity vs RGBA](#opacity-vs-rgba)
- [Syntax and Values](#syntax-and-values)
- [Opacity and Children](#opacity-and-children)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

`opacity` makes elements transparent, creating layering effects, overlays, and fade animations. It's **hardware-accelerated** and works with **transitions/animations**.

**Key Difference from RGBA:**
- `opacity`: Affects **entire element** and children
- `rgba()`: Affects only **that specific property** (background, color, border)

---

## Opacity vs RGBA

### opacity Property

```css
.element {
  background: blue;
  opacity: 0.5; /* Element + text + children all 50% transparent */
}
```

### RGBA Color

```css
.element {
  background: rgba(0, 0, 255, 0.5); /* Only background is 50% transparent */
  /* Text remains fully opaque */
}
```

**Visual Comparison:**

```html
<div class="opacity-example">Text</div>
<div class="rgba-example">Text</div>
```

```css
.opacity-example {
  background: blue;
  opacity: 0.5;
  /* Text is also 50% transparent */
}

.rgba-example {
  background: rgba(0, 0, 255, 0.5);
  /* Text is fully opaque */
}
```

---

## Syntax and Values

```css
opacity: 1;    /* Fully opaque (default) */
opacity: 0.5;  /* 50% transparent */
opacity: 0;    /* Fully transparent (invisible) */
```

**Values:** `0` to `1` (decimals) or `0%` to `100%` (percentages)

```css
opacity: 0.75; /* Same as 75% */
opacity: 75%;  /* Same as 0.75 */
```

---

## Opacity and Children

**Important:** Opacity affects **all descendants**.

```html
<div class="parent" style="opacity: 0.5;">
  <p>This text is also 50% transparent</p>
  <button>This button is also 50% transparent</button>
</div>
```

**Solution:** Use `rgba()` for background only:

```css
.parent {
  background: rgba(0, 0, 0, 0.5); /* Only background transparent */
  /* Children remain fully opaque */
}
```

---

## Examples

### Example 1: Fade In Animation

```css
.fade-in {
  opacity: 0;
  animation: fadeIn 1s ease-out forwards;
}

@keyframes fadeIn {
  to {
    opacity: 1;
  }
}
```

---

### Example 2: Hover Effect

```css
.image {
  opacity: 1;
  transition: opacity 0.3s ease;
}

.image:hover {
  opacity: 0.7;
}
```

---

### Example 3: Modal Overlay

```css
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: black;
  opacity: 0.8;
}
```

---

### Example 4: Loading State

```css
.loading {
  opacity: 0.3;
  pointer-events: none; /* Disable interactions */
}
```

---

## Common Use Cases

### Use Case 1: Disabled State
```css
button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

### Use Case 2: Overlay
```css
.overlay {
  opacity: 0.8;
  background: black;
}
```

### Use Case 3: Fade Transition
```css
.element {
  transition: opacity 0.3s;
}
.element.hidden {
  opacity: 0;
}
```

### Use Case 4: Watermark
```css
.watermark {
  opacity: 0.1;
  position: absolute;
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE 11 |
|----------|--------|---------|--------|------|-------|
| `opacity` | All | All | All | All | Full |

---

## Best Practices

### Do This

1. **Combine with transitions**
   ```css
   .element {
     transition: opacity 0.3s ease;
   }
   ```

2. **Use rgba() when only background needs transparency**
   ```css
   background: rgba(0, 0, 0, 0.5);
   ```

3. **Disable pointer events when fully transparent**
   ```css
   .hidden {
     opacity: 0;
     pointer-events: none;
   }
   ```

### Avoid This

1. **Using opacity when rgba() would work better**
   ```css
   /* Avoid */
   .element {
     opacity: 0.5; /* Makes text transparent too */
   }

   /* Better */
   .element {
     background: rgba(0, 0, 0, 0.5);
   }
   ```

2. **Forgetting accessibility (invisible text)**
   ```css
   /* Bad for screen readers */
   .element {
     opacity: 0; /* Still in DOM, confusing */
   }

   /* Better */
   .element {
     display: none; /* Or visibility: hidden */
   }
   ```

---

## Related Topics

**Prerequisites:**
- [Colors Overview](../02-colors/colors-overview.md)

**Next Steps:**
- [Transitions](transitions.md)
- [Animations](animations.md)

---

## Navigation

**Previous:** [← Filters](filters.md)
**Next:** [Tables →](../11-components/tables.md)
**Up:** [↑ Back to Visual Effects](../README.md#9️⃣-visual-effects-8-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Visual Effects
**Difficulty:** Beginner
