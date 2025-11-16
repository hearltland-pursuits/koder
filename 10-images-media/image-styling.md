---
title: Image Styling
category: Images & Media
order: 1
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Image Styling

> **Quick Summary:** CSS provides extensive control over image appearance through borders, shadows, filters, shapes, and sizing. Master responsive images, aspect ratios, and visual effects for professional-looking galleries and content.

## Table of Contents
- [Introduction](#introduction)
- [Basic Image Properties](#basic-image-properties)
- [Borders and Shapes](#borders-and-shapes)
- [Shadows and Effects](#shadows-and-effects)
- [Filters](#filters)
- [Responsive Sizing](#responsive-sizing)
- [Aspect Ratio](#aspect-ratio)
- [Hover Effects](#hover-effects)
- [Image Overlays](#image-overlays)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**Image styling** transforms plain images into polished, professional visuals using CSS. Common techniques include responsive sizing, borders, shadows, filters, and hover effects.

**Key styling areas:**
- Size and aspect ratio control
- Borders, shapes, and rounded corners
- Shadows and depth effects
- Color filters and adjustments
- Hover and transition effects
- Overlays and captions

---

## Basic Image Properties

```css
img {
  /* Sizing */
  width: 100%;
  height: auto; /* Maintains aspect ratio */
  max-width: 100%; /* Prevents overflow */

  /* Display */
  display: block; /* Removes inline spacing */

  /* Spacing */
  margin: 0 auto; /* Center image */
  padding: 10px;
}
```

**Common patterns:**

```css
/* Responsive image (scales with container) */
.responsive-img {
  width: 100%;
  height: auto;
  display: block;
}

/* Fixed size */
.avatar {
  width: 100px;
  height: 100px;
}

/* Constrained maximum */
.hero-image {
  max-width: 1200px;
  width: 100%;
  height: auto;
}
```

---

## Borders and Shapes

### Rounded Corners

```css
/* Slightly rounded */
img {
  border-radius: 8px;
}

/* Pill shape */
.pill-image {
  border-radius: 50px;
}

/* Circle (requires square aspect ratio) */
.circle-image {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  object-fit: cover; /* Crop to fit */
}
```

### Borders

```css
/* Simple border */
img {
  border: 2px solid #ddd;
}

/* Gradient border (using background trick) */
.gradient-border {
  padding: 3px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  border-radius: 8px;
}

.gradient-border img {
  border-radius: 5px;
  display: block;
}

/* Photo frame effect */
.frame {
  border: 15px solid white;
  box-shadow: 0 4px 8px rgba(0,0,0,0.2);
}
```

### Custom Shapes

```css
/* Hexagon (using clip-path) */
.hexagon {
  clip-path: polygon(25% 0%, 75% 0%, 100% 50%, 75% 100%, 25% 100%, 0% 50%);
}

/* Triangle */
.triangle {
  clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
}

/* Star */
.star {
  clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
}
```

---

## Shadows and Effects

### Box Shadows

```css
/* Subtle shadow */
img {
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

/* Material Design elevation */
.elevated {
  box-shadow:
    0 2px 4px rgba(0,0,0,0.07),
    0 4px 8px rgba(0,0,0,0.07);
}

/* Dramatic shadow */
.dramatic {
  box-shadow: 0 10px 40px rgba(0,0,0,0.3);
}

/* Colored shadow */
.colored-shadow {
  box-shadow: 0 8px 16px rgba(102, 126, 234, 0.4);
}
```

### Neumorphism

```css
.neumorphic-image {
  border-radius: 20px;
  background: #e0e5ec;
  box-shadow:
    9px 9px 16px rgba(163,177,198,0.6),
    -9px -9px 16px rgba(255,255,255,0.5);
  padding: 20px;
}
```

---

## Filters

```css
/* Grayscale */
.grayscale {
  filter: grayscale(100%);
}

/* Sepia tone */
.sepia {
  filter: sepia(80%);
}

/* Blur */
.blur {
  filter: blur(5px);
}

/* Brightness adjustment */
.bright {
  filter: brightness(1.3);
}

.dark {
  filter: brightness(0.7);
}

/* Contrast */
.high-contrast {
  filter: contrast(1.5);
}

/* Saturation */
.vibrant {
  filter: saturate(1.5);
}

.desaturate {
  filter: saturate(0.5);
}

/* Hue rotation */
.hue-shift {
  filter: hue-rotate(90deg);
}

/* Combine multiple filters */
.vintage {
  filter: sepia(40%) contrast(1.2) brightness(0.9);
}

.instagram {
  filter: saturate(1.3) contrast(1.1) brightness(1.05);
}
```

---

## Responsive Sizing

### Percentage-based

```css
/* Full width of container */
img {
  width: 100%;
  height: auto;
}

/* Half width */
.half-width {
  width: 50%;
  height: auto;
}
```

### Max-width constraint

```css
/* Never exceeds natural size */
img {
  max-width: 100%;
  height: auto;
}

/* Set maximum */
.constrained {
  max-width: 800px;
  width: 100%;
  height: auto;
}
```

### Object-fit

```css
/* Cover (crop to fill) */
.cover {
  width: 300px;
  height: 300px;
  object-fit: cover; /* Crops to fill square */
}

/* Contain (fit inside, may have gaps) */
.contain {
  width: 300px;
  height: 300px;
  object-fit: contain; /* Fits inside, maintains ratio */
}

/* Fill (stretch to fit) */
.fill {
  object-fit: fill; /* Stretches, may distort */
}
```

---

## Aspect Ratio

**Modern `aspect-ratio` property:**

```css
/* 16:9 aspect ratio */
.video-thumbnail {
  width: 100%;
  aspect-ratio: 16 / 9;
  object-fit: cover;
}

/* Square (1:1) */
.square {
  width: 100%;
  aspect-ratio: 1 / 1;
  object-fit: cover;
}

/* Portrait (4:5 - Instagram) */
.portrait {
  aspect-ratio: 4 / 5;
}
```

**Legacy technique (padding-bottom hack):**

```css
.aspect-ratio-box {
  position: relative;
  width: 100%;
  padding-bottom: 56.25%; /* 16:9 ratio (9/16 = 0.5625) */
}

.aspect-ratio-box img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```

---

## Hover Effects

### Zoom on Hover

```css
.zoom-container {
  overflow: hidden;
  border-radius: 8px;
}

.zoom-container img {
  transition: transform 0.5s ease;
  display: block;
}

.zoom-container:hover img {
  transform: scale(1.1);
}
```

### Grayscale to Color

```css
img {
  filter: grayscale(100%);
  transition: filter 0.3s ease;
}

img:hover {
  filter: grayscale(0%);
}
```

### Lift Effect

```css
img {
  transition: all 0.3s ease;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

img:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 16px rgba(0,0,0,0.2);
}
```

### Brightness Change

```css
img {
  transition: filter 0.3s ease;
}

img:hover {
  filter: brightness(1.2);
}
```

---

## Image Overlays

### Dark Overlay with Text

```css
.image-overlay {
  position: relative;
  display: inline-block;
}

.image-overlay img {
  display: block;
  width: 100%;
}

.image-overlay::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0,0,0,0.5);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.image-overlay:hover::before {
  opacity: 1;
}

.image-overlay .caption {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: white;
  font-size: 1.5rem;
  opacity: 0;
  transition: opacity 0.3s ease;
  z-index: 2;
}

.image-overlay:hover .caption {
  opacity: 1;
}
```

**HTML:**
```html
<div class="image-overlay">
  <img src="photo.jpg" alt="Photo">
  <div class="caption">View Details</div>
</div>
```

---

## Examples

### Example 1: Profile Avatar

```css
.avatar {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  border: 4px solid white;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  object-fit: cover;
}
```

---

### Example 2: Product Card Image

```css
.product-image {
  width: 100%;
  aspect-ratio: 1 / 1;
  object-fit: cover;
  border-radius: 8px 8px 0 0;
  transition: transform 0.3s ease;
}

.product-card:hover .product-image {
  transform: scale(1.05);
}
```

---

### Example 3: Hero Image with Gradient Overlay

```css
.hero {
  position: relative;
  height: 500px;
  overflow: hidden;
}

.hero img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.hero::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(to bottom, transparent, rgba(0,0,0,0.7));
  z-index: 1;
}

.hero-content {
  position: absolute;
  bottom: 40px;
  left: 40px;
  color: white;
  z-index: 2;
}
```

---

### Example 4: Instagram-Style Filter Gallery

```css
.filter-gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 15px;
}

.filter-normal { filter: none; }
.filter-clarendon { filter: contrast(1.2) saturate(1.35); }
.filter-gingham { filter: brightness(1.05) hue-rotate(350deg); }
.filter-moon { filter: grayscale(1) contrast(1.1) brightness(1.1); }
.filter-lark { filter: contrast(0.9) sepia(0.25) saturate(1.2); }
.filter-reyes { filter: sepia(0.22) brightness(1.1) contrast(0.85); }
.filter-juno { filter: contrast(1.2) brightness(1.1) saturate(1.4); }
.filter-slumber { filter: saturate(0.66) brightness(1.05); }
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `border-radius` | All | All | All | All |
| `box-shadow` | All | All | All | All |
| `filter` | 53+ | 35+ | 9.1+ | 13+ |
| `object-fit` | 32+ | 36+ | 10+ | 79+ |
| `aspect-ratio` | 88+ | 89+ | 15+ | 88+ |
| `clip-path` | 55+ | 54+ | 9.1+ | 79+ |

**Support:** Modern features excellent (90%+), with fallbacks available.

---

## Best Practices

### ✅ Do This

1. **Always set height: auto for responsive images**
   ```css
   img { width: 100%; height: auto; }
   ```

2. **Use object-fit for fixed dimensions**
   ```css
   img { width: 300px; height: 300px; object-fit: cover; }
   ```

3. **Add alt attributes for accessibility**
   ```html
   <img src="photo.jpg" alt="Description of photo">
   ```

4. **Use transitions for smooth effects**
   ```css
   img { transition: transform 0.3s ease; }
   ```

5. **Optimize images before uploading**
   - Use proper file formats (JPG for photos, PNG for graphics, WebP for best compression)
   - Compress images (aim for <200KB for web)
   - Use appropriate dimensions (don't upload 4K for a 400px display)

### ❌ Avoid This

1. **Don't set both width and height without object-fit**
   ```css
   /* May distort image */
   img { width: 300px; height: 200px; }

   /* Better */
   img { width: 300px; height: 200px; object-fit: cover; }
   ```

2. **Don't forget display: block for full-width images**
   ```css
   /* May have inline spacing issues */
   img { width: 100%; }

   /* Better */
   img { width: 100%; display: block; }
   ```

3. **Don't overuse filters**
   ```css
   /* Too many filters = slow performance */
   img { filter: blur(2px) brightness(1.1) contrast(1.2) saturate(1.3) sepia(0.2); }
   ```

---

## Related Topics

**Prerequisites:**
- [Box Model](../03-box-model/box-model-concept.md)
- [Filters](../09-visual-effects/filters.md)
- [Shadows](../09-visual-effects/shadows.md)

**Next Steps:**
- [Image Gallery](image-gallery.md)
- [Object-Fit](object-fit.md)
- [Responsive Images](../12-responsive-design/responsive-images.md)

---

## Practice Exercise

Create a photo card component with:
- Rounded corners (12px)
- Subtle shadow
- Zoom effect on hover (scale 1.1)
- Grayscale by default, color on hover
- Smooth transitions (0.3s)

---

## Navigation

**Previous:** [← Visual Effects](../09-visual-effects/opacity.md)
**Next:** [Image Gallery →](image-gallery.md)
**Up:** [↑ Back to Images & Media](../README.md#1️⃣0️⃣-images--media-6-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Images & Media
**Difficulty:** Beginner
