---
title: CSS Filters
category: Visual Effects
order: 7
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Filters

> **Quick Summary:** The `filter` property applies visual effects like blur, brightness, contrast, grayscale, and more to elements without requiring image editing software. Filters are hardware-accelerated and work on images, backgrounds, and entire elements.

## Table of Contents
- [Introduction](#introduction)
- [Filter Functions](#filter-functions)
- [Combining Filters](#combining-filters)
- [Backdrop Filter](#backdrop-filter)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

CSS filters let you apply **Photoshop-style effects** directly in the browser: blur, sepia, brightness adjustments, and more—all without image editing.

**Key Benefits:**
- No image editing required
- Real-time, dynamic effects
- Works on images, videos, and elements
- Hardware-accelerated (GPU)

---

## Filter Functions

### blur()

```css
filter: blur(5px); /* Gaussian blur */
```

**Values:** Length (px, rem, em)
**Use Case:** Background blur for overlays, loading states

---

### brightness()

```css
filter: brightness(1.5); /* 150% brighter */
filter: brightness(0.5); /* 50% darker */
```

**Values:** Number or percentage
- `0` = completely black
- `1` = original (100%)
- `>1` = brighter

---

### contrast()

```css
filter: contrast(2); /* Double contrast */
filter: contrast(50%); /* Half contrast */
```

**Values:** Number or percentage
**Use Case:** Make images pop or create washed-out effects

---

### grayscale()

```css
filter: grayscale(100%); /* Full black & white */
filter: grayscale(0%);   /* Original colors */
```

**Values:** 0% to 100%
**Use Case:** Inactive/disabled state images

---

### sepia()

```css
filter: sepia(100%); /* Full vintage effect */
```

**Values:** 0% to 100%
**Use Case:** Old photograph effect

---

### saturate()

```css
filter: saturate(2);   /* Double saturation */
filter: saturate(0%);  /* Completely desaturated */
```

**Values:** Number or percentage
**Use Case:** Vibrant colors or muted tones

---

### hue-rotate()

```css
filter: hue-rotate(90deg);  /* Shift colors */
filter: hue-rotate(180deg); /* Invert colors */
```

**Values:** Angle (deg)
**Use Case:** Color theme variations

---

### invert()

```css
filter: invert(100%); /* Full color inversion */
```

**Values:** 0% to 100%
**Use Case:** Dark mode transformations

---

### opacity()

```css
filter: opacity(50%); /* Same as opacity property */
```

**Values:** 0% to 100%
**Note:** Use `opacity` property instead (better performance)

---

### drop-shadow()

```css
filter: drop-shadow(5px 5px 10px rgba(0,0,0,0.5));
```

**Syntax:** `drop-shadow(offset-x offset-y blur-radius color)`
**Difference from box-shadow:** Follows element's shape (including transparent areas)

---

## Combining Filters

**Space-separate** multiple filters:

```css
.image {
  filter: brightness(1.2) contrast(1.1) saturate(1.3);
}
```

### Example: Instagram-Style Filters

```css
/* Sepia vintage effect */
.vintage {
  filter: sepia(50%) brightness(1.1) contrast(0.9);
}

/* High-contrast B&W */
.dramatic {
  filter: grayscale(100%) contrast(1.5);
}

/* Vibrant colors */
.vibrant {
  filter: saturate(1.8) brightness(1.1);
}
```

---

## Backdrop Filter

**Blurs background behind element** (glass morphism effect).

```css
.glass-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
}
```

**Use Case:** Modern frosted glass UI

---

## Examples

### Example 1: Image Hover Effects

```css
.image-container img {
  transition: filter 0.3s ease;
  filter: grayscale(0%);
}

.image-container:hover img {
  filter: grayscale(100%) brightness(0.8);
}
```

---

### Example 2: Disabled State

```css
button:disabled {
  filter: grayscale(100%) opacity(50%);
  cursor: not-allowed;
}
```

---

### Example 3: Dark Mode Image Adjustment

```css
@media (prefers-color-scheme: dark) {
  img {
    filter: brightness(0.8) contrast(1.2);
  }
}
```

---

### Example 4: Loading Blur Effect

```css
.loading {
  filter: blur(5px);
  pointer-events: none;
}

.loaded {
  filter: blur(0);
  transition: filter 0.5s ease-out;
}
```

---

## Common Use Cases

### Use Case 1: Hover Brightness
```css
img:hover {
  filter: brightness(1.2);
}
```

### Use Case 2: Inactive/Disabled
```css
.inactive {
  filter: grayscale(100%) opacity(50%);
}
```

### Use Case 3: Glassmorphism
```css
.card {
  backdrop-filter: blur(10px);
}
```

### Use Case 4: Dynamic Theming
```css
.dark-theme img {
  filter: invert(1) hue-rotate(180deg);
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE 11 |
|----------|--------|---------|--------|------|-------|
| `filter` | ✅ 53+ | ✅ 35+ | ✅ 9.1+ | ✅ 79+ | ❌ None |
| `backdrop-filter` | ✅ 76+ | ✅ 103+ | ✅ 9+ | ✅ 79+ | ❌ None |

**Fallback:**
```css
.element {
  background: rgba(255, 255, 255, 0.9); /* Fallback */
  backdrop-filter: blur(10px); /* Enhanced */
}
```

---

## Best Practices

### ✅ Do This

1. **Combine with transitions**
   ```css
   img {
     transition: filter 0.3s ease;
   }
   img:hover {
     filter: brightness(1.2);
   }
   ```

2. **Use for interactive states**
   ```css
   button:disabled {
     filter: grayscale(100%);
   }
   ```

3. **Subtle effects (avoid overuse)**
   ```css
   /* Good */
   filter: brightness(1.1);

   /* Too much */
   filter: brightness(2) saturate(5);
   ```

### ❌ Avoid This

1. **Too many filters (performance)**
2. **Extreme values (unreadable)**
3. **Using for layout (use transforms instead)**

---

## Related Topics

**Prerequisites:**
- [Transitions](transitions.md)

**Next Steps:**
- [Opacity](opacity.md)

---

## Navigation

**Previous:** [← Animations](animations.md)
**Next:** [Opacity →](opacity.md)
**Up:** [↑ Back to Visual Effects](../README.md#9️⃣-visual-effects-8-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Visual Effects
**Difficulty:** Intermediate
