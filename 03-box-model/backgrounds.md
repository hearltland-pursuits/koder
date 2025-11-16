---
title: CSS Backgrounds
category: Box Model
order: 2
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Backgrounds

> **Quick Summary:** CSS background properties control the background of elements—colors, images, gradients, positioning, sizing, and layering. Backgrounds add visual interest without affecting layout or content.

## Table of Contents
- [Introduction](#introduction)
- [Background Color](#background-color)
- [Background Image](#background-image)
- [Background Repeat](#background-repeat)
- [Background Position](#background-position)
- [Background Size](#background-size)
- [Background Attachment](#background-attachment)
- [Multiple Backgrounds](#multiple-backgrounds)
- [Background Shorthand](#background-shorthand)
- [Examples](#examples)
- [Browser Support](#browser-support)
- [Best Practices](#best-practices)

---

## Introduction

Backgrounds transform plain boxes into visually rich elements. A solid color creates mood. An image tells a story. A gradient adds depth. CSS backgrounds are powerful because they're **non-destructive**—they sit behind content without affecting layout, padding, or margins.

**Key Concept:** Backgrounds fill the content + padding area, extending under borders (unless `background-clip` changes this).

---

## Background Color

**Property:** `background-color`

**Syntax:**
```css
.element {
  background-color: value;
}
```

**Values:** Any CSS color (named, HEX, RGB, HSL, transparent)

### Examples

```css
/* Named color */
.box1 { background-color: red; }

/* HEX */
.box2 { background-color: #3498db; }

/* RGB */
.box3 { background-color: rgb(52, 152, 219); }

/* RGBA (transparent) */
.box4 { background-color: rgba(52, 152, 219, 0.5); }

/* HSL */
.box5 { background-color: hsl(210, 80%, 53%); }

/* Transparent (default) */
.box6 { background-color: transparent; }
```

---

## Background Image

**Property:** `background-image`

**Syntax:**
```css
.element {
  background-image: url('path/to/image.jpg');
}
```

### Examples

```css
/* Relative path */
.hero {
  background-image: url('images/hero.jpg');
}

/* Absolute URL */
.banner {
  background-image: url('https://example.com/image.jpg');
}

/* Gradient (linear) */
.gradient-box {
  background-image: linear-gradient(to right, #3498db, #2ecc71);
}

/* Gradient (radial) */
.radial {
  background-image: radial-gradient(circle, #3498db, #2c3e50);
}

/* No background */
.plain {
  background-image: none;
}
```

---

## Background Repeat

**Property:** `background-repeat`

**Controls:** How background images tile

**Values:** `repeat`, `repeat-x`, `repeat-y`, `no-repeat`, `space`, `round`

```css
/* Repeat both directions (default) */
.tile {
  background-image: url('pattern.png');
  background-repeat: repeat;
}

/* No repeat */
.hero {
  background-image: url('hero.jpg');
  background-repeat: no-repeat;
}

/* Repeat horizontally only */
.horizontal {
  background-repeat: repeat-x;
}

/* Repeat vertically only */
.vertical {
  background-repeat: repeat-y;
}

/* Space (distribute evenly) */
.spaced {
  background-repeat: space;
}

/* Round (scale to fit) */
.rounded {
  background-repeat: round;
}
```

---

## Background Position

**Property:** `background-position`

**Controls:** Where the background image starts

**Values:** Keywords, percentages, lengths

### Examples

```css
/* Keywords */
.top-left { background-position: top left; }
.center { background-position: center; }
.bottom-right { background-position: bottom right; }

/* Percentages */
.percent { background-position: 50% 50%; } /* Center */

/* Lengths */
.exact { background-position: 20px 40px; }

/* Mixed */
.mixed { background-position: center 20px; }

/* Multiple values (X Y) */
.hero {
  background-image: url('hero.jpg');
  background-position: center top;
  background-repeat: no-repeat;
}
```

**Common positions:**
- `top left` = `0% 0%` = `0 0`
- `center` = `50% 50%`
- `bottom right` = `100% 100%`

---

## Background Size

**Property:** `background-size`

**Controls:** Size of background image

**Values:** `auto`, `cover`, `contain`, lengths, percentages

### Examples

```css
/* Auto (original size) */
.auto {
  background-size: auto;
}

/* Cover (fill container, may crop) */
.cover {
  background-image: url('hero.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}

/* Contain (fit inside, may show empty space) */
.contain {
  background-size: contain;
}

/* Specific dimensions */
.fixed {
  background-size: 300px 200px;
}

/* Percentage */
.percent {
  background-size: 50% 50%;
}

/* Width auto-height */
.width-only {
  background-size: 100% auto;
}
```

**Most common: `cover`** for hero sections (fills container, crops excess)

---

## Background Attachment

**Property:** `background-attachment`

**Controls:** Whether background scrolls with content

**Values:** `scroll` (default), `fixed`, `local`

### Examples

```css
/* Scroll with page (default) */
.normal {
  background-attachment: scroll;
}

/* Fixed (parallax effect) */
.parallax {
  background-image: url('mountains.jpg');
  background-attachment: fixed;
  background-size: cover;
  background-position: center;
}

/* Scroll with element content */
.local {
  background-attachment: local;
}
```

**Parallax effect:**
```css
.hero {
  height: 100vh;
  background-image: url('parallax.jpg');
  background-attachment: fixed;
  background-size: cover;
  background-position: center;
}
```

---

## Multiple Backgrounds

**Layer multiple backgrounds** (comma-separated, first = top layer)

```css
.layered {
  background-image:
    url('overlay.png'),
    linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
    url('photo.jpg');
  background-position:
    center,
    center,
    center;
  background-size:
    auto,
    cover,
    cover;
  background-repeat:
    no-repeat,
    no-repeat,
    no-repeat;
}
```

**Result:** Overlay PNG on top, semi-transparent gradient, photo on bottom.

---

## Background Shorthand

**Combine all properties:**

```css
.element {
  background: [color] [image] [repeat] [attachment] [position] / [size];
}
```

### Examples

```css
/* Full shorthand */
.hero {
  background: #3498db url('hero.jpg') no-repeat center / cover;
}

/* Equivalent longhand */
.hero {
  background-color: #3498db;
  background-image: url('hero.jpg');
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}

/* Common pattern: Hero section */
.hero {
  background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
              url('hero.jpg') no-repeat center / cover;
  height: 100vh;
}
```

**Note:** `background-size` must come **after** `background-position` with `/` separator.

---

## Examples

### Example 1: Hero Section

```css
.hero {
  background: linear-gradient(rgba(0,0,0,0.4), rgba(0,0,0,0.4)),
              url('hero.jpg') no-repeat center / cover;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
}
```

**Result:** Full-screen hero with darkened background image.

---

### Example 2: Gradient Button

```css
.button {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 15px 30px;
  border: none;
  border-radius: 5px;
  transition: transform 0.3s;
}

.button:hover {
  transform: translateY(-2px);
}
```

---

### Example 3: Pattern Background

```css
.pattern {
  background: url('pattern.png') repeat;
  background-size: 50px 50px;
}
```

---

## Browser Support

| Property | Chrome | Firefox | Safari | Edge | IE |
|----------|--------|---------|--------|------|----|
| `background-color` | 1+ | 1+ | 1+ | 12+ | 4+ |
| `background-image` | 1+ | 1+ | 1+ | 12+ | 4+ |
| `background-size` | 4+ | 4+ | 5+ | 12+ | 9+ |
| `background-position` | 1+ | 1+ | 1+ | 12+ | 4+ |
| Multiple backgrounds | 4+ | 3.6+ | 1.3+ | 12+ | 9+ |

---

## Best Practices

### ✅ Do This

1. **Use `cover` for Hero Sections**
   ```css
   .hero {
     background: url('hero.jpg') no-repeat center / cover;
     height: 100vh;
   }
   ```

2. **Provide Fallback Colors**
   ```css
   .element {
     background-color: #3498db; /* Fallback */
     background-image: url('image.jpg');
   }
   ```

3. **Optimize Images**
   - Use WebP format when possible
   - Compress images (aim for <200KB for backgrounds)
   - Use appropriate dimensions (don't use 4K image for 500px div)

### ❌ Avoid This

1. **Don't Forget `no-repeat` for Photos**
   ```css
   /* Bad - image tiles */
   .hero { background-image: url('hero.jpg'); }

   /* Good */
   .hero {
     background: url('hero.jpg') no-repeat center / cover;
   }
   ```

2. **Don't Use Huge Images**
   ```css
   /* Bad - slow load */
   background-image: url('8000x6000.jpg'); /* 5MB */

   /* Good - optimized */
   background-image: url('1920x1080-optimized.webp'); /* 150KB */
   ```

---

**Last Updated:** November 15, 2025
**Category:** Box Model
**Difficulty:** Beginner
