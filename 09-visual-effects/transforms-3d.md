---
title: 3D Transforms
category: Visual Effects
order: 4
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS 3D Transforms

> **Quick Summary:** 3D transforms extend 2D transforms by adding a Z-axis (depth), enabling effects like card flips, rotating cubes, and perspective-based animations. They require `perspective` to create realistic 3D space.

## Table of Contents
- [Introduction](#introduction)
- [Perspective](#perspective)
- [3D Transform Functions](#3d-transform-functions)
- [Preserve-3D](#preserve-3d)
- [Backface Visibility](#backface-visibility)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)
- [Video Tutorial](#video-tutorial)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

While **2D transforms** move elements in a flat plane (X and Y axes), **3D transforms** add **depth** (Z-axis), creating realistic spatial effects. Combined with `perspective`, 3D transforms simulate how objects appear in real-world 3D space.

**Key Concept:** Without `perspective`, 3D transforms appear flat. Perspective defines the "viewing distance" from the user to the 3D scene.

---

## Perspective

**Defines the depth of 3D space** (how "far away" elements appear).

### Syntax

```css
/* On parent container */
.container {
  perspective: 1000px; /* Viewing distance */
}

/* On element itself */
.element {
  transform: perspective(1000px) rotateY(45deg);
}
```

**Lower values** = more dramatic distortion
**Higher values** = more subtle, realistic perspective

### Example: Perspective Comparison

```css
/* Dramatic perspective (close viewing distance) */
.close {
  perspective: 300px;
}

/* Subtle perspective (far viewing distance) */
.far {
  perspective: 1500px;
}
```

---

## 3D Transform Functions

### translateZ() - Move Along Z-Axis

```css
/* Move toward viewer */
transform: translateZ(50px);

/* Move away from viewer */
transform: translateZ(-50px);

/* Combined 3D translation */
transform: translate3d(50px, 30px, 20px);
```

---

### rotateX() - Flip Vertically

```css
/* Rotate around horizontal axis */
transform: rotateX(45deg);

/* Flip card vertically */
transform: rotateX(180deg);
```

**Visual:**
```
    Before          rotateX(90deg)
    ┌─────┐              │
    │     │         ─────┴─────
    └─────┘         (edge view)
```

---

### rotateY() - Flip Horizontally

```css
/* Rotate around vertical axis */
transform: rotateY(45deg);

/* Card flip effect */
transform: rotateY(180deg);
```

**Visual:**
```
Before      rotateY(90deg)
┌─────┐          ─
│     │          │ (edge)
└─────┘          ─
```

---

### rotateZ() - Spin (Same as 2D rotate)

```css
/* Rotate around Z-axis (depth) */
transform: rotateZ(45deg);

/* Equivalent to 2D rotate */
transform: rotate(45deg);
```

---

### rotate3d() - Rotate Around Custom Axis

```css
/* rotate3d(x, y, z, angle) */
transform: rotate3d(1, 1, 0, 45deg);
```

---

## Preserve-3D

**Maintains 3D space** for nested elements.

```css
.parent {
  transform-style: preserve-3d;
}

.child {
  transform: rotateY(45deg);
}
```

**Without `preserve-3d`:** Children are flattened to parent's plane.
**With `preserve-3d`:** Children maintain 3D positioning.

---

## Backface Visibility

**Controls visibility** of element's back side when rotated.

```css
/* Hide back face (default for card flips) */
.card-front,
.card-back {
  backface-visibility: hidden;
}

/* Show back face (default) */
.element {
  backface-visibility: visible;
}
```

**Use Case:** Card flip effects (prevents seeing reversed text).

---

## Examples

### Example 1: Card Flip on Hover

**HTML:**
```html
<div class="flip-container">
  <div class="flipper">
    <div class="front">Front Side</div>
    <div class="back">Back Side</div>
  </div>
</div>
```

**CSS:**
```css
.flip-container {
  perspective: 1000px;
  width: 300px;
  height: 200px;
}

.flipper {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.6s;
  transform-style: preserve-3d;
}

.flip-container:hover .flipper {
  transform: rotateY(180deg);
}

.front, .back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 10px;
}

.front {
  background: #007bff;
  color: white;
}

.back {
  background: #28a745;
  color: white;
  transform: rotateY(180deg);
}
```

---

### Example 2: Rotating 3D Cube

**CSS:**
```css
.cube-container {
  perspective: 1000px;
}

.cube {
  width: 200px;
  height: 200px;
  position: relative;
  transform-style: preserve-3d;
  animation: rotateCube 10s infinite linear;
}

.cube-face {
  position: absolute;
  width: 200px;
  height: 200px;
  border: 2px solid #007bff;
  background: rgba(0, 123, 255, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  color: white;
}

.front  { transform: rotateY(0deg) translateZ(100px); }
.back   { transform: rotateY(180deg) translateZ(100px); }
.right  { transform: rotateY(90deg) translateZ(100px); }
.left   { transform: rotateY(-90deg) translateZ(100px); }
.top    { transform: rotateX(90deg) translateZ(100px); }
.bottom { transform: rotateX(-90deg) translateZ(100px); }

@keyframes rotateCube {
  from { transform: rotateX(0) rotateY(0); }
  to { transform: rotateX(360deg) rotateY(360deg); }
}
```

---

### Example 3: Parallax Depth Effect

**CSS:**
```css
.scene {
  perspective: 600px;
}

.layer {
  transition: transform 0.3s;
}

.layer-1 { transform: translateZ(-100px); }
.layer-2 { transform: translateZ(0px); }
.layer-3 { transform: translateZ(100px); }

.scene:hover .layer-1 { transform: translateZ(-150px); }
.scene:hover .layer-3 { transform: translateZ(150px); }
```

---

## Common Use Cases

### Use Case 1: Product Showcase (360° Rotation)
```css
.product {
  animation: rotate360 5s infinite linear;
}

@keyframes rotate360 {
  from { transform: rotateY(0deg); }
  to { transform: rotateY(360deg); }
}
```

### Use Case 2: Info Card Flip
```css
.card-container:hover .card {
  transform: rotateY(180deg);
}
```

### Use Case 3: Book Page Turn
```css
.page {
  transform-origin: left center;
  transform: rotateY(-90deg);
}

.page.open {
  transform: rotateY(0deg);
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE 11 |
|----------|--------|---------|--------|------|-------|
| 3D Transforms | ✅ 36+ | ✅ 16+ | ✅ 9+ | ✅ 12+ | ✅ 10+ (prefix) |
| `perspective` | ✅ 36+ | ✅ 16+ | ✅ 9+ | ✅ 12+ | ✅ 10+ |
| `transform-style` | ✅ 36+ | ✅ 16+ | ✅ 9+ | ✅ 12+ | ✅ 11+ |

**Can I Use:** [https://caniuse.com/transforms3d](https://caniuse.com/transforms3d)

---

## Best Practices

### ✅ Do This

1. **Always Set Perspective on Parent**
   ```css
   .container { perspective: 1000px; }
   ```

2. **Use `backface-visibility: hidden` for Flips**
   ```css
   .card-face { backface-visibility: hidden; }
   ```

3. **Combine with Transitions for Smooth Effects**
   ```css
   transition: transform 0.6s;
   ```

---

### ❌ Avoid This

1. **Forgetting `transform-style: preserve-3d`**
2. **Using Too Low Perspective Values (distorted)**
3. **Not Testing on Mobile (performance)**

---

## Video Tutorial

**Watch:** [https://www.youtube.com/watch?v=OXGznpKZ_sA&t=3600s](https://www.youtube.com/watch?v=OXGznpKZ_sA&t=3600s)

---

## Related Topics

**Prerequisites:**
- [2D Transforms](transforms-2d.md)

**Next Steps:**
- [Transitions](transitions.md)
- [Animations](animations.md)

---

## Practice Exercise

### 🎯 Challenge: Create a Flip Card Component

**Requirements:**
- [ ] Card flips on hover
- [ ] Front and back sides with different content
- [ ] Smooth transition (0.6s)
- [ ] Hidden backfaces

---

## Navigation

**Previous:** [← 2D Transforms](transforms-2d.md)
**Next:** [Transitions →](transitions.md)
**Up:** [↑ Back to Visual Effects](../README.md#9️⃣-visual-effects-8-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Visual Effects
**Difficulty:** Advanced
