---
title: 2D Transforms
category: Visual Effects
order: 3
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS 2D Transforms

> **Quick Summary:** The `transform` property lets you rotate, scale, skew, and translate (move) elements in 2D space without affecting document flow. Transforms are hardware-accelerated, making them perfect for smooth animations.

## Table of Contents
- [Introduction](#introduction)
- [Why Transforms Matter](#why-transforms-matter)
- [Transform Functions](#transform-functions)
- [Translate (Move)](#translate-move)
- [Rotate](#rotate)
- [Scale](#scale)
- [Skew](#skew)
- [Transform Origin](#transform-origin)
- [Multiple Transforms](#multiple-transforms)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

Before CSS transforms, moving or rotating elements required:
- **JavaScript** (position calculations, performance issues)
- **Image files** (pre-rotated graphics, not scalable)
- **Flash/Canvas** (complex, not accessible)

**CSS Transforms** changed everything by enabling visual transformations with:
- **Hardware acceleration** (GPU-powered, 60fps animations)
- **No layout reflow** (transforms don't affect document flow)
- **Simple syntax** (one-line CSS)

**Key Concept:** Transforms are **visual only**—they don't change an element's actual position in the DOM or affect surrounding elements.

---

## Why Transforms Matter

### 1. **Performance (Hardware Accelerated)**

```css
/* Slow (causes reflow) */
.move-with-position {
  position: relative;
  left: 100px; /* Browser recalculates layout */
}

/* Fast (GPU accelerated) */
.move-with-transform {
  transform: translateX(100px); /* No layout recalculation */
}
```

### 2. **Smooth Animations**

```css
.button {
  transition: transform 0.3s ease;
}

.button:hover {
  transform: scale(1.1) rotate(2deg);
}
```

### 3. **Modern UI Patterns**

```css
/* Card flip */
.card:hover .card-front {
  transform: rotateY(180deg);
}

/* Bounce effect */
@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-20px); }
}
```

### 4. **Career Relevance**
- **Interview question:** "How do you create performant animations?"
- **Common task:** "Add hover effects to cards/buttons"
- **Framework skill:** React Spring, Framer Motion use transforms

---

## Transform Functions

### Basic Syntax

```css
transform: function(value);
```

**Available 2D Functions:**
- `translate()` - Move element
- `rotate()` - Rotate element
- `scale()` - Resize element
- `skew()` - Slant element

---

## Translate (Move)

**Moves element** along X (horizontal) and/or Y (vertical) axes.

### Syntax

```css
/* Move right 50px */
transform: translateX(50px);

/* Move down 30px */
transform: translateY(30px);

/* Move right 50px, down 30px */
transform: translate(50px, 30px);
```

### Examples

```css
/* Center element absolutely positioned */
.centered {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/* Slide in from left */
.slide-in {
  transform: translateX(-100%);
  transition: transform 0.5s;
}

.slide-in.active {
  transform: translateX(0);
}
```

**Why use translate over `position`?**
- GPU accelerated (smoother)
- Doesn't trigger layout reflow
- Works with `transition` for animations

---

## Rotate

**Rotates element** around a point (default: center).

### Syntax

```css
/* Rotate 45 degrees clockwise */
transform: rotate(45deg);

/* Rotate counter-clockwise */
transform: rotate(-45deg);

/* Full rotation */
transform: rotate(360deg);
```

### Examples

```css
/* Rotating arrow icon */
.arrow {
  transition: transform 0.3s;
}

.dropdown.open .arrow {
  transform: rotate(180deg);
}

/* Spinning loader */
@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.loader {
  animation: spin 1s linear infinite;
}
```

---

## Scale

**Resizes element** (enlarges or shrinks).

### Syntax

```css
/* Scale to 150% size */
transform: scale(1.5);

/* Scale width only */
transform: scaleX(2);

/* Scale height only */
transform: scaleY(0.5);

/* Scale width and height separately */
transform: scale(1.5, 0.8);
```

### Examples

```css
/* Button hover grow */
button {
  transition: transform 0.3s ease;
}

button:hover {
  transform: scale(1.1);
}

/* Image zoom on hover */
.image-container {
  overflow: hidden;
}

.image-container img {
  transition: transform 0.5s;
}

.image-container:hover img {
  transform: scale(1.2);
}
```

**Note:** `scale(1)` = original size, `scale(2)` = 2x size, `scale(0.5)` = 50% size

---

## Skew

**Slants element** along X and/or Y axes (creates parallelogram effect).

### Syntax

```css
/* Skew horizontally */
transform: skewX(20deg);

/* Skew vertically */
transform: skewY(10deg);

/* Skew both axes */
transform: skew(20deg, 10deg);
```

### Examples

```css
/* Diagonal banner */
.banner {
  transform: skewY(-3deg);
  background: linear-gradient(to right, #667eea, #764ba2);
}

/* Italic-style effect */
.slanted {
  transform: skewX(-10deg);
}
```

---

## Transform Origin

**Changes the pivot point** for transformations (default: center).

### Syntax

```css
transform-origin: x-position y-position;
```

### Examples

```css
/* Rotate from top-left corner */
.card {
  transform-origin: top left;
  transform: rotate(45deg);
}

/* Scale from bottom center */
.popup {
  transform-origin: bottom center;
  transform: scale(0);
  transition: transform 0.3s;
}

.popup.show {
  transform: scale(1);
}

/* Common values */
transform-origin: center;        /* Default */
transform-origin: top left;
transform-origin: 50% 50%;       /* Same as center */
transform-origin: 100px 50px;    /* Pixel positioning */
```

---

## Multiple Transforms

**Combine multiple transform functions** (space-separated).

### Syntax

```css
transform: rotate(45deg) scale(1.5) translate(50px, 20px);
```

**Order matters!** Transforms apply **right to left**:
```css
/* First translate, then rotate */
transform: rotate(45deg) translate(50px, 0);

/* First rotate, then translate (different result) */
transform: translate(50px, 0) rotate(45deg);
```

### Examples

```css
/* Hover effect: grow and lift */
.card {
  transition: transform 0.3s ease;
}

.card:hover {
  transform: translateY(-10px) scale(1.05);
}

/* Rotating and pulsing loader */
.loader {
  animation: rotateAndPulse 2s ease-in-out infinite;
}

@keyframes rotateAndPulse {
  0%, 100% { transform: rotate(0deg) scale(1); }
  50% { transform: rotate(180deg) scale(1.2); }
}
```

---

## Examples

### Example 1: Card Hover Effect

**HTML:**
```html
<div class="card">
  <img src="image.jpg" alt="Card image">
  <h3>Card Title</h3>
  <p>Card description</p>
</div>
```

**CSS:**
```css
.card {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
  transform: translateY(-10px) scale(1.02);
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}

.card img {
  transition: transform 0.5s ease;
}

.card:hover img {
  transform: scale(1.1);
}
```

---

### Example 2: Rotating Icon Button

**HTML:**
```html
<button class="icon-button">
  <span class="icon">+</span>
  Add Item
</button>
```

**CSS:**
```css
.icon-button .icon {
  display: inline-block;
  transition: transform 0.3s ease;
}

.icon-button:hover .icon {
  transform: rotate(90deg);
}
```

---

### Example 3: Parallax Skew Effect

**CSS:**
```css
.section-1 {
  transform: skewY(-3deg);
  transform-origin: top left;
  background: linear-gradient(135deg, #667eea, #764ba2);
  padding: 100px 0;
  margin-top: -50px;
}

.section-1 .content {
  transform: skewY(3deg); /* Unskew content */
}
```

---

## Common Use Cases

### Use Case 1: Center Element Absolutely
```css
.centered {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

### Use Case 2: Button Hover Grow
```css
button:hover {
  transform: scale(1.05);
}
```

### Use Case 3: Image Zoom Container
```css
.image-container {
  overflow: hidden;
}

.image-container:hover img {
  transform: scale(1.2);
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE 11 |
|----------|--------|---------|--------|------|-------|
| `transform` (2D) | 36+ | 16+ | 9+ | 12+ | 10+ (prefix) |
| `transform-origin` | 36+ | 16+ | 9+ | 12+ | 10+ |

**IE 9-10 Prefix:**
```css
-ms-transform: rotate(45deg);
```

**Can I Use:** [https://caniuse.com/transforms2d](https://caniuse.com/transforms2d)

---

## Best Practices

### Do This

1. **Use for Animations (Performance)**
   ```css
   transform: translateX(100px); /* Fast */
   ```

2. **Combine with Transitions**
   ```css
   transition: transform 0.3s ease;
   ```

3. **Use `translate()` for Centering**
   ```css
   transform: translate(-50%, -50%);
   ```

---

### Avoid This

1. **Animating `position` Properties**
   ```css
   /* Slow */
   transition: left 0.3s;
   ```

2. **Too Many Simultaneous Transforms**
   ```css
   /* Overkill */
   transform: rotate(45deg) scale(1.5) skew(20deg) translate(100px, 50px);
   ```

---

## Video Tutorial

**Watch:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=3400s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=3400s)

**Additional Resources:**
- [MDN - CSS Transforms](https://developer.mozilla.org/en-US/docs/Web/CSS/transform)

---

## Related Topics

**Prerequisites:**
- [Position Property](../05-layout-basics/position.md)

**Next Steps:**
- [3D Transforms](transforms-3d.md)
- [Transitions](transitions.md)

---

## Practice Exercise

### Challenge: Create an Interactive Photo Gallery

**Requirements:**
- [ ] Images scale up on hover
- [ ] Container has slight rotation effect
- [ ] Add shadow that grows on hover
- [ ] Use `transform-origin` for corner rotation

**Starter Code:**
```html
<div class="gallery">
  <div class="photo-card">
    <img src="photo1.jpg" alt="Photo 1">
  </div>
</div>
```

---

## Navigation

**Previous:** [← Shadows](shadows.md)
**Next:** [3D Transforms →](transforms-3d.md)
**Up:** [↑ Back to Visual Effects](../README.md#9️⃣-visual-effects-8-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Visual Effects
**Difficulty:** Intermediate
