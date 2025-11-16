---
title: Responsive Images
category: Images & Media
order: 6
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Responsive Images

> **Quick Summary:** Responsive images adapt to different screen sizes using `srcset`, `sizes`, and `<picture>` elements. Serve appropriate image sizes for each device, reducing bandwidth and improving performance.

## Table of Contents
- [Introduction](#introduction)
- [srcset Attribute](#srcset-attribute)
- [sizes Attribute](#sizes-attribute)
- [picture Element](#picture-element)
- [Art Direction](#art-direction)
- [Image Formats](#image-formats)
- [Performance Optimization](#performance-optimization)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**Responsive images** serve different image files based on screen size, resolution, and viewport. This prevents loading massive desktop images on mobile devices.

**Goals:**
- Faster page loads (smaller file sizes)
- Better user experience
- Bandwidth savings
- Sharp images on all devices

---

## srcset Attribute

**Provides multiple image sources** for the browser to choose from.

### Resolution Switching

```html
<img src="photo.jpg"
     srcset="photo-480w.jpg 480w,
             photo-800w.jpg 800w,
             photo-1200w.jpg 1200w"
     alt="Photo">
```

**How it works:**
- Browser chooses based on viewport width
- `480w` = image is 480px wide
- `800w` = image is 800px wide
- `1200w` = image is 1200px wide

### Pixel Density Switching

```html
<img src="photo.jpg"
     srcset="photo@1x.jpg 1x,
             photo@2x.jpg 2x,
             photo@3x.jpg 3x"
     alt="Photo">
```

**Use cases:**
- `1x`: Standard displays
- `2x`: Retina/high-DPI (most modern phones)
- `3x`: Ultra high-DPI (newest phones)

---

## sizes Attribute

**Tells browser how much space image will occupy** at different breakpoints.

```html
<img src="photo.jpg"
     srcset="photo-480w.jpg 480w,
             photo-800w.jpg 800w,
             photo-1200w.jpg 1200w"
     sizes="(max-width: 600px) 100vw,
            (max-width: 900px) 50vw,
            33vw"
     alt="Photo">
```

**Explanation:**
- `(max-width: 600px) 100vw`: On small screens, image is 100% of viewport
- `(max-width: 900px) 50vw`: On medium screens, image is 50% of viewport
- `33vw`: On large screens, image is 33% of viewport (default)

---

## picture Element

**Most flexible** approach for responsive images.

### Basic Usage

```html
<picture>
  <source media="(min-width: 1024px)" srcset="large.jpg">
  <source media="(min-width: 768px)" srcset="medium.jpg">
  <img src="small.jpg" alt="Photo">
</picture>
```

**How it works:**
- Browser evaluates `<source>` elements top-to-bottom
- Uses first match
- Falls back to `<img>` if no match

### With srcset

```html
<picture>
  <source media="(min-width: 1024px)"
          srcset="large-1x.jpg 1x, large-2x.jpg 2x">
  <source media="(min-width: 768px)"
          srcset="medium-1x.jpg 1x, medium-2x.jpg 2x">
  <img src="small.jpg"
       srcset="small-1x.jpg 1x, small-2x.jpg 2x"
       alt="Photo">
</picture>
```

---

## Art Direction

**Different crops/compositions** for different screen sizes.

```html
<picture>
  <!-- Desktop: Wide landscape -->
  <source media="(min-width: 1024px)" srcset="landscape-wide.jpg">

  <!-- Tablet: Standard landscape -->
  <source media="(min-width: 768px)" srcset="landscape.jpg">

  <!-- Mobile: Portrait crop focusing on subject -->
  <img src="portrait-crop.jpg" alt="Photo">
</picture>
```

**Use case:** Hero images where you want to show different portions of the image on different devices.

---

## Image Formats

**Modern formats** for better compression.

### WebP Support

```html
<picture>
  <source type="image/webp" srcset="photo.webp">
  <img src="photo.jpg" alt="Photo">
</picture>
```

### AVIF Support

```html
<picture>
  <source type="image/avif" srcset="photo.avif">
  <source type="image/webp" srcset="photo.webp">
  <img src="photo.jpg" alt="Photo">
</picture>
```

**File size comparison** (same visual quality):
- AVIF: ~30KB (smallest)
- WebP: ~45KB
- JPEG: ~100KB
- PNG: ~150KB (lossless)

---

## Performance Optimization

### Loading Attribute

```html
<img src="photo.jpg" loading="lazy" alt="Photo">
```

**Values:**
- `lazy`: Load when near viewport (default for offscreen images)
- `eager`: Load immediately
- `auto`: Browser decides

### Decoding Attribute

```html
<img src="photo.jpg" decoding="async" alt="Photo">
```

**Values:**
- `async`: Decode in parallel with other content
- `sync`: Decode before showing other content
- `auto`: Browser decides

### Fetch Priority

```html
<img src="hero.jpg" fetchpriority="high" alt="Hero">
```

**Use for:** Above-the-fold images that should load first.

---

## Examples

### Example 1: Product Card Image

```html
<picture>
  <!-- WebP for modern browsers -->
  <source type="image/webp"
          srcset="product-480w.webp 480w,
                  product-800w.webp 800w,
                  product-1200w.webp 1200w"
          sizes="(max-width: 768px) 100vw,
                 (max-width: 1200px) 50vw,
                 33vw">

  <!-- JPEG fallback -->
  <img src="product-800w.jpg"
       srcset="product-480w.jpg 480w,
               product-800w.jpg 800w,
               product-1200w.jpg 1200w"
       sizes="(max-width: 768px) 100vw,
              (max-width: 1200px) 50vw,
              33vw"
       loading="lazy"
       alt="Product name">
</picture>
```

---

### Example 2: Hero Image with Art Direction

```html
<picture>
  <!-- Desktop: Wide landscape, focus on full scene -->
  <source media="(min-width: 1024px)" srcset="hero-desktop.jpg">

  <!-- Tablet: Medium crop -->
  <source media="(min-width: 768px)" srcset="hero-tablet.jpg">

  <!-- Mobile: Tight crop on main subject -->
  <img src="hero-mobile.jpg"
       alt="Company office"
       fetchpriority="high">
</picture>
```

---

### Example 3: Retina Images

```html
<img src="logo.png"
     srcset="logo@1x.png 1x,
             logo@2x.png 2x,
             logo@3x.png 3x"
     alt="Company Logo"
     width="200"
     height="50">
```

---

### Example 4: Complete Responsive Image

```html
<picture>
  <!-- AVIF (newest, best compression) -->
  <source type="image/avif"
          srcset="photo-480w.avif 480w,
                  photo-800w.avif 800w,
                  photo-1200w.avif 1200w"
          sizes="(max-width: 600px) 100vw, 50vw">

  <!-- WebP (good compression, wide support) -->
  <source type="image/webp"
          srcset="photo-480w.webp 480w,
                  photo-800w.webp 800w,
                  photo-1200w.webp 1200w"
          sizes="(max-width: 600px) 100vw, 50vw">

  <!-- JPEG (universal fallback) -->
  <img src="photo-800w.jpg"
       srcset="photo-480w.jpg 480w,
               photo-800w.jpg 800w,
               photo-1200w.jpg 1200w"
       sizes="(max-width: 600px) 100vw, 50vw"
       loading="lazy"
       decoding="async"
       alt="Descriptive alt text">
</picture>
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `srcset` | 38+ | 38+ | 9+ | 13+ |
| `sizes` | 38+ | 38+ | 9+ | 13+ |
| `<picture>` | 38+ | 38+ | 9.1+ | 13+ |
| `loading="lazy"` | 77+ | 75+ | 15.4+ | 79+ |
| `fetchpriority` | 102+ | N/A | 17+ | 102+ |

**Support:** Excellent (95%+). Always include fallback `<img>`.

---

## Best Practices

### ✅ Do This

1. **Always provide fallback src**
   ```html
   <img src="fallback.jpg" srcset="...">
   ```

2. **Use WebP/AVIF for modern browsers**
   ```html
   <picture>
     <source type="image/webp" srcset="photo.webp">
     <img src="photo.jpg" alt="Photo">
   </picture>
   ```

3. **Add loading="lazy" for below-fold images**
   ```html
   <img src="photo.jpg" loading="lazy" alt="Photo">
   ```

4. **Include width/height to prevent layout shift**
   ```html
   <img src="photo.jpg" width="800" height="600" alt="Photo">
   ```

5. **Use descriptive alt text**
   ```html
   <img src="photo.jpg" alt="Sunset over mountains">
   ```

### ❌ Avoid This

1. **Don't load full-size images for thumbnails**
   ```html
   <!-- Bad: 4MB image for 200px thumbnail -->
   <img src="full-size.jpg" width="200">
   ```

2. **Don't skip srcset for large images**
   ```html
   <!-- Missing opportunity to save bandwidth -->
   <img src="huge-image.jpg">
   ```

3. **Don't use fetchpriority="high" on all images**
   ```html
   <!-- Defeats the purpose -->
   <img fetchpriority="high"> <!-- everywhere -->
   ```

4. **Don't forget alt text**
   ```html
   <!-- Inaccessible -->
   <img src="photo.jpg">
   ```

---

## Related Topics

**Prerequisites:**
- [Image Styling](image-styling.md)
- [Object-Fit](object-fit.md)

**Next Steps:**
- [Responsive Design](../12-responsive-design/rwd-intro.md)
- [Performance Optimization](../13-modern-css/optimization.md)

---

## Practice Exercise

Create a responsive product image with:
- 3 sizes (480w, 800w, 1200w)
- WebP and JPEG formats
- Lazy loading
- Proper alt text
- Width/height attributes

---

## Navigation

**Previous:** [← Masking](masking.md)
**Next:** [Components →](../11-components/tables.md)
**Up:** [↑ Back to Images & Media](../README.md#1️⃣0️⃣-images--media-6-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Images & Media
**Difficulty:** Intermediate
