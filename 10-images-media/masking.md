---
title: CSS Masking
category: Images & Media
order: 5
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Masking

> **Quick Summary:** CSS masking hides portions of elements using images, gradients, or shapes. Use `mask-image`, `mask-mode`, and `clip-path` to create creative visual effects without editing images.

## Table of Contents
- [Introduction](#introduction)
- [clip-path](#clip-path)
- [mask-image](#mask-image)
- [mask-mode](#mask-mode)
- [mask-size and mask-position](#mask-size-and-mask-position)
- [Gradient Masks](#gradient-masks)
- [SVG Masks](#svg-masks)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**CSS masking** controls element visibility using shapes, images, or gradients. Unlike `clip-path` which crops, masking uses alpha channels to show/hide portions.

**Two main techniques:**
1. **clip-path:** Geometric shapes (polygons, circles, ellipses)
2. **mask-image:** Images, gradients, SVGs with transparency

---

## clip-path

**Crops elements to specific shapes.**

### Basic Shapes

```css
/* Circle */
.circle {
  clip-path: circle(50%);
}

/* Ellipse */
.ellipse {
  clip-path: ellipse(40% 50%);
}

/* Triangle */
.triangle {
  clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
}

/* Hexagon */
.hexagon {
  clip-path: polygon(25% 0%, 75% 0%, 100% 50%, 75% 100%, 25% 100%, 0% 50%);
}

/* Star */
.star {
  clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
}
```

### Custom Polygons

```css
/* Diagonal cut */
.diagonal {
  clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
}

/* Speech bubble */
.speech-bubble {
  clip-path: polygon(0% 0%, 100% 0%, 100% 75%, 75% 75%, 75% 100%, 50% 75%, 0% 75%);
}

/* Notch (phone screen) */
.notch {
  clip-path: polygon(
    0% 0%, 30% 0%, 30% 5%, 70% 5%, 70% 0%, 100% 0%,
    100% 100%, 0% 100%
  );
}
```

### circle() and ellipse()

```css
/* Syntax */
clip-path: circle(radius at x y);
clip-path: ellipse(x-radius y-radius at x y);

/* Examples */
clip-path: circle(100px);                /* Center, 100px radius */
clip-path: circle(50% at 100% 0);        /* Top-right corner */
clip-path: ellipse(50% 30%);             /* Center ellipse */
clip-path: ellipse(40% 50% at 25% 50%);  /* Off-center */
```

---

## mask-image

**Uses image transparency to mask elements.**

### Image Masks

```css
.masked {
  mask-image: url('mask.png');
  mask-size: cover;
  mask-repeat: no-repeat;
}
```

**How it works:**
- **Black** in mask = transparent
- **White** in mask = visible
- **Gray** in mask = partially transparent

### Linear Gradient Masks

```css
/* Fade to transparent (top to bottom) */
.fade-bottom {
  mask-image: linear-gradient(to bottom, black, transparent);
}

/* Fade from both sides */
.fade-edges {
  mask-image: linear-gradient(to right, transparent, black 20%, black 80%, transparent);
}
```

### Radial Gradient Masks

```css
/* Vignette effect */
.vignette {
  mask-image: radial-gradient(circle, black 50%, transparent 100%);
}

/* Spotlight */
.spotlight {
  mask-image: radial-gradient(circle at 30% 30%, black 20%, transparent 50%);
}
```

---

## mask-mode

**Controls how mask is applied.**

```css
/* Luminance (uses brightness) */
.mask-luminance {
  mask-image: url('mask.png');
  mask-mode: luminance; /* Default */
}

/* Alpha (uses transparency) */
.mask-alpha {
  mask-image: url('mask.png');
  mask-mode: alpha;
}

/* Match source (preserves original) */
.mask-match {
  mask-image: url('mask.svg');
  mask-mode: match-source;
}
```

---

## mask-size and mask-position

**Control mask scaling and positioning.**

```css
.masked {
  mask-image: url('mask.png');
  mask-size: cover;         /* Scale to cover element */
  mask-size: contain;       /* Fit inside element */
  mask-size: 50% 50%;       /* Specific size */
  mask-position: center;    /* Center mask */
  mask-position: top left;  /* Position mask */
  mask-repeat: no-repeat;   /* Don't repeat */
}
```

---

## Gradient Masks

### Fade Effects

```css
/* Fade out bottom */
.fade-text {
  mask-image: linear-gradient(to bottom, black 80%, transparent 100%);
}

/* Fade from center */
.fade-center {
  mask-image: radial-gradient(circle, black 40%, transparent 70%);
}

/* Horizontal scroll fade */
.scroll-fade {
  mask-image: linear-gradient(90deg, transparent, black 10%, black 90%, transparent);
}
```

### Text Masks

```css
/* Text reveals background */
.text-mask {
  background: url('background.jpg');
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

---

## SVG Masks

**More control with SVG.**

```html
<svg width="0" height="0">
  <defs>
    <mask id="custom-mask">
      <circle cx="50%" cy="50%" r="40%" fill="white"/>
    </mask>
  </defs>
</svg>
```

```css
.element {
  mask: url(#custom-mask);
}
```

---

## Examples

### Example 1: Image Gallery with Shapes

```css
.gallery-item img {
  width: 100%;
  aspect-ratio: 1 / 1;
  object-fit: cover;
}

.gallery-item:nth-child(1) img {
  clip-path: circle(50%);
}

.gallery-item:nth-child(2) img {
  clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); /* Diamond */
}

.gallery-item:nth-child(3) img {
  clip-path: polygon(25% 0%, 75% 0%, 100% 50%, 75% 100%, 25% 100%, 0% 50%); /* Hexagon */
}
```

---

### Example 2: Fade Overlay

```css
.hero {
  position: relative;
  height: 500px;
  background: url('hero.jpg') center/cover;
}

.hero::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 200px;
  background: linear-gradient(to bottom, transparent, rgba(0,0,0,0.9));
}

/* Or with mask */
.hero-masked {
  mask-image: linear-gradient(to bottom, black 60%, transparent 100%);
}
```

---

### Example 3: Diagonal Section Divider

```css
section {
  clip-path: polygon(0 0, 100% 0, 100% calc(100% - 50px), 0 100%);
  margin-bottom: -50px; /* Overlap next section */
}
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `clip-path` | 55+ | 54+ | 9.1+ | 79+ |
| `mask-image` | 120+ | 53+ | 15.4+ | 120+ |
| `-webkit-mask-image` | 4+ | N/A | 4+ | 79+ |

**Support:** `clip-path` excellent (95%+), `mask-image` improving (85%+).

**Vendor Prefixes:**
```css
.masked {
  -webkit-mask-image: linear-gradient(to bottom, black, transparent);
  mask-image: linear-gradient(to bottom, black, transparent);
}
```

---

## Best Practices

### Do This

1. **Use clip-path for geometric shapes**
   ```css
   clip-path: circle(50%);
   ```

2. **Use mask-image for complex effects**
   ```css
   mask-image: linear-gradient(to bottom, black, transparent);
   ```

3. **Add vendor prefixes for mask**
   ```css
   -webkit-mask-image: url('mask.png');
   mask-image: url('mask.png');
   ```

4. **Provide fallbacks**
   ```css
   border-radius: 50%; /* Fallback */
   clip-path: circle(50%);
   ```

### Avoid This

1. **Don't use for essential content visibility**
   ```css
   /* Inaccessible if mask fails to load */
   mask-image: url('mask.png');
   ```

2. **Don't forget vendor prefixes**
   ```css
   /* Won't work in Safari without -webkit- */
   mask-image: linear-gradient(...);
   ```

3. **Don't overuse complex shapes**
   ```css
   /* Performance impact */
   clip-path: polygon(/* 100 points */);
   ```

---

## Related Topics

**Prerequisites:**
- [Image Styling](image-styling.md)
- [Gradients](../09-visual-effects/gradients.md)

**Next Steps:**
- [Filters](../09-visual-effects/filters.md)
- [Transforms](../09-visual-effects/transforms-2d.md)

---

## Practice Exercise

Create three image cards with different shapes:
- First: Circle
- Second: Hexagon
- Third: Triangle
Use `clip-path` for all three.

---

## Navigation

**Previous:** [← Object-Fit](object-fit.md)
**Next:** [Responsive Images →](responsive-images.md)
**Up:** [↑ Back to Images & Media](../README.md#1️⃣0️⃣-images--media-6-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Images & Media
**Difficulty:** Advanced
