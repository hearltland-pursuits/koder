---
title: Responsive Videos
category: Responsive Design
order: 4
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Responsive Videos

> **Quick Summary:** Make videos scale responsively using aspect-ratio, padding-top technique, or container wrappers. Works for YouTube embeds, Vimeo, and native HTML5 video. Maintains correct proportions across all screen sizes.

## Table of Contents
- [Introduction](#introduction)
- [aspect-ratio Property](#aspect-ratio-property)
- [Padding-Top Technique](#padding-top-technique)
- [YouTube and Vimeo Embeds](#youtube-and-vimeo-embeds)
- [HTML5 Video](#html5-video)
- [Multiple Aspect Ratios](#multiple-aspect-ratios)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**Responsive videos** scale proportionally to fit their container while maintaining aspect ratio (usually 16:9). Without proper CSS, videos either overflow on small screens or become distorted.

**Problem without responsive styling:**
```html
<iframe width="560" height="315" src="..."></iframe>
```
→ Fixed 560×315px on all devices (too wide for mobile)

**Solution:**
- Modern: `aspect-ratio` property
- Legacy: Padding-top technique

---

## aspect-ratio Property

### Basic Usage (Modern Browsers)

```css
.video-container {
  width: 100%;
  aspect-ratio: 16 / 9;
}

.video-container iframe,
.video-container video {
  width: 100%;
  height: 100%;
}
```

**HTML:**
```html
<div class="video-container">
  <iframe src="https://www.youtube.com/embed/VIDEO_ID"></iframe>
</div>
```

**How it works:**
- `width: 100%`: Video fills container width
- `aspect-ratio: 16 / 9`: Automatically calculates height
- Result: Perfect 16:9 ratio at any size

---

### Different Aspect Ratios

```css
/* Widescreen (16:9) */
.video-16-9 {
  aspect-ratio: 16 / 9;
}

/* Standard (4:3) */
.video-4-3 {
  aspect-ratio: 4 / 3;
}

/* Ultra-wide (21:9) */
.video-21-9 {
  aspect-ratio: 21 / 9;
}

/* Vertical video (9:16, TikTok/Stories) */
.video-9-16 {
  aspect-ratio: 9 / 16;
}

/* Square (1:1) */
.video-1-1 {
  aspect-ratio: 1 / 1;
}
```

---

## Padding-Top Technique

### Legacy Method (Works in All Browsers)

```css
.video-wrapper {
  position: relative;
  padding-top: 56.25%; /* 16:9 aspect ratio (9 / 16 = 0.5625) */
  width: 100%;
  height: 0;
}

.video-wrapper iframe,
.video-wrapper video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
```

**Why padding-top: 56.25%?**
```
Aspect ratio calculation:
16:9 → 9 ÷ 16 = 0.5625 → 56.25%
4:3  → 3 ÷ 4  = 0.75   → 75%
21:9 → 9 ÷ 21 = 0.4286 → 42.86%
```

**HTML:**
```html
<div class="video-wrapper">
  <iframe src="https://www.youtube.com/embed/VIDEO_ID"></iframe>
</div>
```

---

### Common Aspect Ratio Percentages

```css
/* 16:9 (Widescreen) */
.ratio-16-9 { padding-top: 56.25%; }

/* 4:3 (Standard) */
.ratio-4-3 { padding-top: 75%; }

/* 21:9 (Ultra-wide) */
.ratio-21-9 { padding-top: 42.86%; }

/* 1:1 (Square) */
.ratio-1-1 { padding-top: 100%; }

/* 9:16 (Vertical) */
.ratio-9-16 { padding-top: 177.78%; }
```

---

## YouTube and Vimeo Embeds

### YouTube Responsive Embed

**Modern (aspect-ratio):**
```html
<div class="youtube-container">
  <iframe
    src="https://www.youtube.com/embed/dQw4w9WgXcQ"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen>
  </iframe>
</div>
```

```css
.youtube-container {
  width: 100%;
  aspect-ratio: 16 / 9;
}

.youtube-container iframe {
  width: 100%;
  height: 100%;
  border: none;
}
```

---

**Legacy (padding-top):**
```css
.youtube-wrapper {
  position: relative;
  padding-top: 56.25%;
  width: 100%;
  height: 0;
}

.youtube-wrapper iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: none;
}
```

---

### Vimeo Responsive Embed

```html
<div class="vimeo-container">
  <iframe
    src="https://player.vimeo.com/video/VIDEO_ID"
    frameborder="0"
    allow="autoplay; fullscreen; picture-in-picture"
    allowfullscreen>
  </iframe>
</div>
```

```css
.vimeo-container {
  width: 100%;
  aspect-ratio: 16 / 9;
}

.vimeo-container iframe {
  width: 100%;
  height: 100%;
}
```

---

## HTML5 Video

### Native Video Element

```html
<div class="video-container">
  <video controls>
    <source src="video.mp4" type="video/mp4">
    <source src="video.webm" type="video/webm">
    Your browser does not support the video tag.
  </video>
</div>
```

```css
.video-container {
  width: 100%;
  aspect-ratio: 16 / 9;
}

.video-container video {
  width: 100%;
  height: 100%;
  object-fit: cover; /* or 'contain' */
}
```

---

### object-fit for Videos

```css
/* Cover: Fill container, crop if needed */
video {
  object-fit: cover;
}

/* Contain: Fit inside, may have letterboxing */
video {
  object-fit: contain;
}

/* Fill: Stretch to fill (may distort) */
video {
  object-fit: fill;
}
```

**Use cases:**
- `cover`: Background videos, hero sections
- `contain`: Video players (preserve full frame)
- `fill`: Avoid (causes distortion)

---

## Multiple Aspect Ratios

### Responsive Breakpoints

```css
.video-container {
  width: 100%;
}

/* Mobile: 4:3 (more vertical space) */
.video-container {
  aspect-ratio: 4 / 3;
}

/* Desktop: 16:9 (widescreen) */
@media (min-width: 768px) {
  .video-container {
    aspect-ratio: 16 / 9;
  }
}
```

---

### Max Width for Large Screens

```css
.video-container {
  width: 100%;
  max-width: 1200px; /* Don't get too wide */
  margin: 0 auto; /* Center */
  aspect-ratio: 16 / 9;
}
```

---

## Examples

### Example 1: Full-Width YouTube Embed

```html
<article class="blog-post">
  <h2>Watch This Tutorial</h2>
  <div class="video-embed">
    <iframe
      src="https://www.youtube.com/embed/VIDEO_ID"
      allowfullscreen>
    </iframe>
  </div>
  <p>Video description...</p>
</article>
```

```css
.video-embed {
  width: 100%;
  aspect-ratio: 16 / 9;
  margin: 30px 0;
}

.video-embed iframe {
  width: 100%;
  height: 100%;
  border: none;
  border-radius: 8px;
}
```

---

### Example 2: Grid of Video Thumbnails

```html
<div class="video-grid">
  <div class="video-item">
    <div class="video-thumbnail">
      <img src="thumb1.jpg" alt="Video 1">
      <button class="play-button">▶</button>
    </div>
    <h3>Video Title</h3>
  </div>
  <!-- More videos... -->
</div>
```

```css
.video-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
}

.video-thumbnail {
  position: relative;
  width: 100%;
  aspect-ratio: 16 / 9;
  overflow: hidden;
  border-radius: 8px;
}

.video-thumbnail img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.play-button {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 48px;
  color: white;
  background: rgba(0, 0, 0, 0.7);
  border: none;
  border-radius: 50%;
  width: 80px;
  height: 80px;
  cursor: pointer;
}
```

---

### Example 3: Background Video

```html
<section class="hero">
  <div class="video-background">
    <video autoplay muted loop playsinline>
      <source src="hero.mp4" type="video/mp4">
    </video>
  </div>
  <div class="hero-content">
    <h1>Welcome</h1>
    <p>Amazing content here</p>
  </div>
</section>
```

```css
.hero {
  position: relative;
  height: 100vh;
  overflow: hidden;
}

.video-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
}

.video-background video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.hero-content {
  position: relative;
  z-index: 1;
  color: white;
  text-align: center;
  padding: 50px;
}
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `aspect-ratio` | 88+ | 89+ | 15+ | 88+ |
| Padding-top technique | All | All | All | All |
| `<video>` element | 4+ | 3.5+ | 3.1+ | 12+ |
| `object-fit` | 32+ | 36+ | 10+ | 79+ |

**Support:**
- `aspect-ratio`: Excellent modern support (90%+)
- Padding-top: Universal fallback (100%)

---

## Best Practices

### ✅ Do This

1. **Use aspect-ratio for modern browsers**
   ```css
   .video {
     aspect-ratio: 16 / 9;
   }
   ```

2. **Provide fallback for older browsers**
   ```css
   .video {
     padding-top: 56.25%; /* Fallback */
     aspect-ratio: 16 / 9; /* Modern */
   }
   ```

3. **Remove default iframe borders**
   ```css
   iframe {
     border: none;
   }
   ```

4. **Add max-width for large screens**
   ```css
   .video-container {
     max-width: 1200px;
     margin: 0 auto;
   }
   ```

5. **Use playsinline for iOS autoplay**
   ```html
   <video autoplay muted loop playsinline>
   ```

---

### ❌ Avoid This

1. **Don't use fixed dimensions**
   ```html
   <!-- Bad: Fixed size doesn't scale -->
   <iframe width="560" height="315" src="..."></iframe>
   ```

2. **Don't forget height: 100% on video**
   ```css
   /* Missing height causes problems */
   .video-container video {
     width: 100%;
     /* height: 100%; ← Need this */
   }
   ```

3. **Don't skip the wrapper div**
   ```html
   <!-- Bad: No container for aspect ratio -->
   <iframe class="responsive-video" src="..."></iframe>
   ```

4. **Don't use object-fit: fill (distorts)**
   ```css
   /* Bad: Stretches video */
   video {
     object-fit: fill;
   }
   ```

---

## Related Topics

**Prerequisites:**
- [Responsive Design Intro](rwd-intro.md)
- [Object-Fit](../10-images-media/object-fit.md)

**Next Steps:**
- [Responsive Images](../10-images-media/responsive-images.md)
- [Media Queries](media-queries.md)

---

## Practice Exercise

Create a responsive video page with:
- YouTube embed using aspect-ratio
- 16:9 aspect ratio
- Max-width 900px, centered
- Rounded corners (12px)
- Responsive on mobile (full-width)

---

## Navigation

**Previous:** [← Responsive Grid](responsive-grid.md)
**Next:** [Mobile-First Design →](mobile-first.md)
**Up:** [↑ Back to Responsive Design](../README.md#1️⃣2️⃣-responsive-design-5-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Responsive Design
**Difficulty:** Intermediate
