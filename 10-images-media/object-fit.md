---
title: Object-Fit Property
category: Images & Media
order: 4
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Object-Fit Property

> **Quick Summary:** `object-fit` controls how images and videos fit within their containers, similar to `background-size` but for `<img>` and `<video>` elements. Values: `cover`, `contain`, `fill`, `none`, `scale-down`.

## Table of Contents
- [Introduction](#introduction)
- [object-fit Values](#object-fit-values)
- [object-position](#object-position)
- [Common Use Cases](#common-use-cases)
- [Aspect Ratio Control](#aspect-ratio-control)
- [Browser Support](#browser-support)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**`object-fit`** controls how replaced elements (`<img>`, `<video>`, `<iframe>`) resize to fit their container. Without it, images stretch or distort when given explicit dimensions.

**Problem:**
```css
img {
  width: 300px;
  height: 300px;
  /* Image distorts if not naturally square! */
}
```

**Solution:**
```css
img {
  width: 300px;
  height: 300px;
  object-fit: cover; /* Crops to fill, maintains aspect ratio */
}
```

---

## object-fit Values

### cover (Most Common)

**Fills container completely**, cropping excess.

```css
img {
  width: 400px;
  height: 300px;
  object-fit: cover;
}
```

**Visual:**
```
Original image:        Result (cover):
┌──────────────┐      ┌──────────┐
│              │      │  cropped │
│    Photo     │  →   │   photo  │
│  (portrait)  │      │          │
│              │      └──────────┘
└──────────────┘      (fills box, crops top/bottom)
```

**Use when:** Images must fill a specific area (product cards, hero images, avatars).

---

### contain

**Fits entire image** inside container, may leave gaps.

```css
img {
  width: 400px;
  height: 300px;
  object-fit: contain;
}
```

**Visual:**
```
Original image:        Result (contain):
┌──────────────┐      ┌──────────┐
│              │      │          │
│    Photo     │  →   │  [photo] │
│  (portrait)  │      │          │
│              │      └──────────┘
└──────────────┘      (gaps on sides)
```

**Use when:** Full image must be visible (logos, diagrams, product images where details matter).

---

### fill (Default)

**Stretches to fill** container (may distort).

```css
img {
  width: 400px;
  height: 300px;
  object-fit: fill; /* Default behavior */
}
```

**Visual:**
```
Original image:        Result (fill):
┌──────────────┐      ┌──────────┐
│              │      │          │
│    Photo     │  →   │ STRETCHED│
│  (portrait)  │      │  PHOTO   │
│              │      └──────────┘
└──────────────┘      (distorted)
```

**Use when:** Rarely (causes distortion). Only if aspect ratio doesn't matter.

---

### none

**Original size**, may overflow or leave gaps.

```css
img {
  width: 400px;
  height: 300px;
  object-fit: none;
}
```

**Visual:**
```
Original image (large):    Result (none):
┌────────────────────┐    ┌──────────┐
│                    │    │[cropped] │
│      Photo         │ →  │  center  │
│   (very large)     │    │          │
│                    │    └──────────┘
└────────────────────┘    (shows center portion)
```

**Use when:** Cropping to show specific portion at original resolution.

---

### scale-down

**Chooses smaller of `none` or `contain`**.

```css
img {
  width: 400px;
  height: 300px;
  object-fit: scale-down;
}
```

**Behavior:**
- If image is smaller than container → acts like `none`
- If image is larger than container → acts like `contain`

**Use when:** Ensuring small images don't upscale (pixelate), but large images fit.

---

## object-position

**Controls which part** of the image is visible when cropped.

```css
img {
  width: 300px;
  height: 300px;
  object-fit: cover;
  object-position: center; /* Default */
}
```

### Position Keywords

```css
/* Horizontal */
object-position: left;
object-position: center; /* Default */
object-position: right;

/* Vertical */
object-position: top;
object-position: center; /* Default */
object-position: bottom;

/* Combined */
object-position: top left;
object-position: center right;
object-position: bottom center;
```

### Precise Positioning

```css
/* Percentage */
object-position: 75% 50%; /* 75% from left, 50% from top */

/* Pixels */
object-position: 20px 30px;

/* Mix */
object-position: right 20px; /* 20px from right edge */
object-position: center bottom 10px; /* 10px from bottom, centered horizontally */
```

---

## Common Use Cases

### Product Card Images

```css
.product-image {
  width: 100%;
  aspect-ratio: 1 / 1; /* Square */
  object-fit: cover;
  object-position: center;
}
```

### Profile Avatars

```css
.avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  object-fit: cover;
  object-position: center top; /* Focus on face */
}
```

### Hero Images

```css
.hero-image {
  width: 100%;
  height: 500px;
  object-fit: cover;
  object-position: center 30%; /* Focus on upper-center */
}
```

### Video Backgrounds

```css
.video-background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: -1;
}
```

---

## Aspect Ratio Control

**Combine with `aspect-ratio` for responsive containers:**

```css
/* 16:9 video thumbnails */
.video-thumb {
  width: 100%;
  aspect-ratio: 16 / 9;
  object-fit: cover;
}

/* Square Instagram posts */
.insta-post {
  width: 100%;
  aspect-ratio: 1 / 1;
  object-fit: cover;
}

/* 4:5 Pinterest cards */
.pin-card {
  width: 100%;
  aspect-ratio: 4 / 5;
  object-fit: cover;
}
```

**Legacy fallback (padding-bottom hack):**

```css
.aspect-box {
  position: relative;
  width: 100%;
  padding-bottom: 56.25%; /* 16:9 (9/16 = 0.5625) */
  overflow: hidden;
}

.aspect-box img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```

---

## Examples

### Example 1: Responsive Grid with Fixed Aspect Ratio

```css
.image-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
}

.grid-item img {
  width: 100%;
  aspect-ratio: 4 / 3;
  object-fit: cover;
  border-radius: 8px;
}
```

---

### Example 2: Portrait/Landscape Mixed Gallery

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  grid-auto-rows: 300px;
  gap: 15px;
}

.gallery img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  /* Each image fills its cell regardless of original dimensions */
}
```

---

### Example 3: Logo Container (Contain)

```css
.logo-container {
  width: 200px;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f8f9fa;
  padding: 20px;
}

.logo-container img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain; /* Never crops logo */
}
```

---

### Example 4: Full-Screen Hero with Focus Point

```css
.hero {
  width: 100%;
  height: 100vh;
}

.hero img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: 70% 40%; /* Custom focus point */
}
```

---

### Example 5: Responsive Card with Fallback

```css
.card-image {
  width: 100%;
  height: 250px;
  object-fit: cover;
  background-color: #e0e0e0; /* Fallback color */
}

/* For browsers without object-fit support */
@supports not (object-fit: cover) {
  .card-image {
    width: auto;
    height: 250px;
  }
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge |
|----------|--------|---------|--------|------|
| `object-fit` | 32+ | 36+ | 10+ | 79+ |
| `object-position` | 32+ | 36+ | 10+ | 79+ |

**Support:** Excellent (95%+ global).

**IE11 Fallback:**
```css
/* IE11 doesn't support object-fit */
img {
  width: 100%;
  height: 300px;
  object-fit: cover; /* Modern browsers */
}

/* IE11 hack using background-image instead */
@media all and (-ms-high-contrast: none), (-ms-high-contrast: active) {
  .ie-fix {
    background-size: cover;
    background-position: center;
  }
  .ie-fix img {
    opacity: 0; /* Hide img, show background instead */
  }
}
```

---

## Best Practices

### Do This

1. **Use `cover` for cards and thumbnails**
   ```css
   .card-img { object-fit: cover; }
   ```

2. **Use `contain` for logos**
   ```css
   .logo { object-fit: contain; }
   ```

3. **Combine with aspect-ratio**
   ```css
   img { aspect-ratio: 16/9; object-fit: cover; }
   ```

4. **Set both width AND height for object-fit to work**
   ```css
   /* Won't work (no height) */
   img { width: 300px; object-fit: cover; }

   /* Works */
   img { width: 300px; height: 300px; object-fit: cover; }
   ```

### Avoid This

1. **Don't use object-fit without explicit dimensions**
   ```css
   /* Doesn't work */
   img { object-fit: cover; }

   /* Need dimensions */
   img { width: 100%; height: 300px; object-fit: cover; }
   ```

2. **Don't use `fill` (causes distortion)**
   ```css
   /* Usually undesirable */
   object-fit: fill;
   ```

3. **Don't forget fallbacks for older browsers**
   ```css
   /* Add background-color for loading state */
   img {
     object-fit: cover;
     background-color: #f0f0f0;
   }
   ```

---

## Related Topics

**Prerequisites:**
- [Image Styling](image-styling.md)
- [Box Model](../03-box-model/box-model-concept.md)

**Next Steps:**
- [Responsive Images](../12-responsive-design/responsive-images.md)
- [Aspect Ratio](#)

---

## Practice Exercise

Create a responsive image grid where:
- 4 columns on desktop, 2 on tablet, 1 on mobile
- All images are square (1:1 aspect ratio)
- Images crop to fill (no stretching)
- Gaps of 15px between images

**Hint:** Use Grid + `aspect-ratio` + `object-fit: cover`

---

## Navigation

**Previous:** [← Image Sprites](image-sprites.md)
**Next:** [Masking →](masking.md)
**Up:** [↑ Back to Images & Media](../README.md#1️⃣0️⃣-images--media-6-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Images & Media
**Difficulty:** Beginner
