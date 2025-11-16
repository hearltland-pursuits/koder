---
title: Image Gallery
category: Images & Media
order: 2
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Image Gallery

> **Quick Summary:** Create responsive image galleries using CSS Grid or Flexbox. Common patterns: equal-height rows, masonry layouts, lightbox overlays, and hover effects. No JavaScript required for basic galleries.

## Table of Contents
- [Introduction](#introduction)
- [Grid-Based Gallery](#grid-based-gallery)
- [Flexbox Gallery](#flexbox-gallery)
- [Masonry Layout](#masonry-layout)
- [Hover Effects](#hover-effects)
- [Lightbox Overlay](#lightbox-overlay)
- [Responsive Galleries](#responsive-galleries)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**Image galleries** display collections of images in organized, visually appealing layouts. CSS Grid and Flexbox make creating responsive galleries straightforward without frameworks.

**Common gallery types:**
- **Grid gallery:** Equal-sized images in rows/columns
- **Masonry:** Pinterest-style staggered layout
- **Justified:** Images scaled to fit rows perfectly
- **Carousel:** Horizontal scrolling (requires JS)

---

## Grid-Based Gallery

**CSS Grid** is ideal for equal-sized image grids.

### Basic Grid Gallery

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 15px;
}

.gallery img {
  width: 100%;
  height: 250px;
  object-fit: cover;
  border-radius: 8px;
}
```

**Result:** Responsive grid that shows as many columns as fit, minimum 250px each.

### Fixed Column Grid

```css
/* Desktop: 4 columns */
.gallery {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
}

/* Tablet: 3 columns */
@media (max-width: 1024px) {
  .gallery {
    grid-template-columns: repeat(3, 1fr);
  }
}

/* Mobile: 2 columns */
@media (max-width: 768px) {
  .gallery {
    grid-template-columns: repeat(2, 1fr);
  }
}

.gallery img {
  width: 100%;
  aspect-ratio: 1 / 1;
  object-fit: cover;
}
```

---

## Flexbox Gallery

**Flexbox** offers more flexibility for variable-sized images.

```css
.gallery {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
}

.gallery-item {
  flex: 1 1 calc(25% - 15px); /* 4 columns */
  min-width: 200px;
}

.gallery-item img {
  width: 100%;
  height: 250px;
  object-fit: cover;
  border-radius: 8px;
}

@media (max-width: 768px) {
  .gallery-item {
    flex: 1 1 calc(50% - 15px); /* 2 columns */
  }
}
```

---

## Masonry Layout

**Pinterest-style** staggered layout with variable heights.

### Using CSS Columns

```css
.masonry {
  column-count: 4;
  column-gap: 15px;
}

.masonry-item {
  break-inside: avoid;
  margin-bottom: 15px;
}

.masonry-item img {
  width: 100%;
  border-radius: 8px;
}

@media (max-width: 1024px) {
  .masonry {
    column-count: 3;
  }
}

@media (max-width: 768px) {
  .masonry {
    column-count: 2;
  }
}
```

### Using Grid (Auto-Flow Dense)

```css
.masonry-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  grid-auto-rows: 50px; /* Small row units */
  gap: 15px;
}

.masonry-item {
  /* Span rows based on image height */
}

.masonry-item.tall {
  grid-row: span 6; /* 6 × 50px = 300px */
}

.masonry-item.short {
  grid-row: span 4; /* 4 × 50px = 200px */
}

.masonry-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```

---

## Hover Effects

### Zoom on Hover

```css
.gallery-item {
  overflow: hidden;
  border-radius: 8px;
}

.gallery-item img {
  transition: transform 0.5s ease;
}

.gallery-item:hover img {
  transform: scale(1.1);
}
```

### Overlay on Hover

```css
.gallery-item {
  position: relative;
  overflow: hidden;
}

.gallery-item::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  opacity: 0;
  transition: opacity 0.3s;
}

.gallery-item:hover::before {
  opacity: 1;
}

.gallery-caption {
  position: absolute;
  bottom: 20px;
  left: 20px;
  color: white;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.3s;
}

.gallery-item:hover .gallery-caption {
  opacity: 1;
  transform: translateY(0);
}
```

### Grayscale to Color

```css
.gallery img {
  filter: grayscale(100%);
  transition: filter 0.3s;
}

.gallery-item:hover img {
  filter: grayscale(0%);
}
```

---

## Lightbox Overlay

**Pure CSS lightbox** using `:target` pseudo-class.

```css
/* Thumbnail in gallery */
.gallery a {
  display: block;
}

/* Lightbox overlay (hidden by default) */
.lightbox {
  display: none;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.9);
  z-index: 1000;
  justify-content: center;
  align-items: center;
}

/* Show when targeted */
.lightbox:target {
  display: flex;
}

.lightbox img {
  max-width: 90%;
  max-height: 90%;
}

.lightbox-close {
  position: absolute;
  top: 20px;
  right: 30px;
  color: white;
  font-size: 40px;
  text-decoration: none;
}
```

**HTML:**
```html
<div class="gallery">
  <a href="#img1">
    <img src="thumb1.jpg" alt="Photo 1">
  </a>
</div>

<div id="img1" class="lightbox">
  <a href="#" class="lightbox-close">×</a>
  <img src="full1.jpg" alt="Photo 1">
</div>
```

---

## Responsive Galleries

### Mobile-Optimized

```css
/* Desktop: 4 columns, small gaps */
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
  padding: 20px;
}

/* Tablet: 3 columns */
@media (max-width: 1024px) {
  .gallery {
    gap: 15px;
    padding: 15px;
  }
}

/* Mobile: 2 columns, minimal gaps */
@media (max-width: 768px) {
  .gallery {
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
    padding: 10px;
  }
}

/* Small mobile: 1 column */
@media (max-width: 480px) {
  .gallery {
    grid-template-columns: 1fr;
  }
}
```

---

## Examples

### Example 1: Photography Portfolio

```css
.portfolio-gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 30px;
  padding: 40px;
}

.portfolio-item {
  position: relative;
  overflow: hidden;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

.portfolio-item img {
  width: 100%;
  aspect-ratio: 4 / 3;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.portfolio-item:hover img {
  transform: scale(1.05);
}

.portfolio-info {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 20px;
  background: linear-gradient(to top, rgba(0,0,0,0.8), transparent);
  color: white;
  transform: translateY(100%);
  transition: transform 0.3s;
}

.portfolio-item:hover .portfolio-info {
  transform: translateY(0);
}
```

---

### Example 2: Product Grid

```css
.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 25px;
}

.product-card {
  background: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: transform 0.3s, box-shadow 0.3s;
}

.product-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 16px rgba(0,0,0,0.2);
}

.product-image {
  width: 100%;
  aspect-ratio: 1 / 1;
  object-fit: cover;
}

.product-info {
  padding: 15px;
}
```

---

### Example 3: Instagram-Style Square Grid

```css
.instagram-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 3px; /* Minimal gaps like Instagram */
}

.instagram-item {
  aspect-ratio: 1 / 1;
  position: relative;
  overflow: hidden;
}

.instagram-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Overlay on hover */
.instagram-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  opacity: 0;
  transition: opacity 0.3s;
}

.instagram-item:hover .instagram-overlay {
  opacity: 1;
}
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| CSS Grid | 57+ | 52+ | 10.1+ | 16+ |
| Flexbox | 29+ | 28+ | 9+ | 12+ |
| `object-fit` | 32+ | 36+ | 10+ | 79+ |
| `aspect-ratio` | 88+ | 89+ | 15+ | 88+ |
| `:target` | All | All | All | All |

**Support:** Excellent (95%+).

---

## Best Practices

### ✅ Do This

1. **Use `object-fit: cover` for consistent sizing**
   ```css
   img { object-fit: cover; }
   ```

2. **Add loading="lazy" for performance**
   ```html
   <img src="photo.jpg" loading="lazy" alt="Photo">
   ```

3. **Provide alt text for accessibility**
   ```html
   <img src="photo.jpg" alt="Sunset over mountains">
   ```

4. **Use responsive images**
   ```html
   <img srcset="thumb.jpg 480w, medium.jpg 800w, large.jpg 1200w"
        sizes="(max-width: 600px) 480px, 800px"
        src="medium.jpg" alt="Photo">
   ```

### ❌ Avoid This

1. **Don't load full-size images for thumbnails**
   ```html
   <!-- Bad: 4MB image for 200px thumbnail -->
   <img src="full-resolution.jpg" width="200">
   ```

2. **Don't forget mobile optimization**
   ```css
   /* Too many columns on mobile */
   grid-template-columns: repeat(6, 1fr);
   ```

3. **Don't use tables for galleries**
   ```html
   <!-- Old approach, don't use -->
   <table><tr><td><img></td></tr></table>
   ```

---

## Related Topics

**Prerequisites:**
- [Image Styling](image-styling.md)
- [Grid Container](../07-grid/grid-container.md)
- [Flexbox](../06-flexbox/flexbox-intro.md)

**Next Steps:**
- [Object-Fit](object-fit.md)
- [Responsive Images](responsive-images.md)

---

## Practice Exercise

Create a responsive photo gallery with:
- 4 columns on desktop, 2 on mobile
- Square aspect ratio (1:1)
- Zoom hover effect
- 15px gaps
- Rounded corners (8px)

---

## Navigation

**Previous:** [← Image Styling](image-styling.md)
**Next:** [Image Sprites →](image-sprites.md)
**Up:** [↑ Back to Images & Media](../README.md#1️⃣0️⃣-images--media-6-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Images & Media
**Difficulty:** Intermediate
