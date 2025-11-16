---
title: Image Sprites
category: Images & Media
order: 3
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Image Sprites

> **Quick Summary:** Image sprites combine multiple images into one file, reducing HTTP requests and improving performance. Use `background-position` to display specific portions. Useful for icons, buttons, and repeated graphics.

## Table of Contents
- [Introduction](#introduction)
- [How Sprites Work](#how-sprites-work)
- [Creating a Sprite](#creating-a-sprite)
- [CSS Implementation](#css-implementation)
- [Icon Sprites](#icon-sprites)
- [Hover States](#hover-states)
- [Modern Alternatives](#modern-alternatives)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**Image sprites** are single image files containing multiple smaller images. Instead of loading 20 separate icon files, you load one sprite sheet and display portions using CSS.

**Benefits:**
- Fewer HTTP requests (faster page load)
- Smaller total file size (compression efficiency)
- No flicker on hover states (image already loaded)
- Easier cache management (one file to cache)

**Use cases:**
- Icon sets
- Button states (normal, hover, active)
- UI elements
- Small repeated graphics

---

## How Sprites Work

**Concept:** Show only a portion of the sprite image using `background-position`.

```css
/* Sprite contains 4 icons in a row */
.icon {
  width: 32px;
  height: 32px;
  background-image: url('sprite.png');
  background-repeat: no-repeat;
}

.icon-home {
  background-position: 0 0; /* First icon */
}

.icon-user {
  background-position: -32px 0; /* Second icon (shift left 32px) */
}

.icon-settings {
  background-position: -64px 0; /* Third icon (shift left 64px) */
}

.icon-search {
  background-position: -96px 0; /* Fourth icon (shift left 96px) */
}
```

**Visual:**
```
Sprite file (128px × 32px):
[Home][User][Settings][Search]
  ↑    ↑      ↑         ↑
 0px  32px   64px      96px

background-position values:
- Home:     0 0
- User:     -32px 0
- Settings: -64px 0
- Search:   -96px 0
```

---

## Creating a Sprite

### Manual Creation

1. **Arrange images** in a grid (Photoshop, GIMP, etc.)
2. **Note positions** of each image
3. **Export as single file** (PNG for transparency, JPG for photos)
4. **Write CSS** with background-position values

### Grid Layout (Recommended)

```
32px × 32px icons, 10px spacing:

[Icon1][Icon2][Icon3]
[Icon4][Icon5][Icon6]
[Icon7][Icon8][Icon9]

Total size: (32+10)×3 - 10 = 116px wide
```

### Online Tools

- **CSS Sprite Generator:** cssspritestool.com
- **Sprite Cow:** spritecow.com (visual position picker)
- **TexturePacker:** codeandweb.com/texturepacker

---

## CSS Implementation

### Basic Sprite

```css
.sprite {
  background-image: url('sprites.png');
  background-repeat: no-repeat;
  display: inline-block;
}

.icon-home {
  width: 32px;
  height: 32px;
  background-position: 0 0;
}

.icon-user {
  width: 32px;
  height: 32px;
  background-position: -32px 0;
}
```

### With Spacing Between Icons

```css
/* Sprite has 10px spacing between icons */
.icon-home {
  background-position: 0 0;
}

.icon-user {
  background-position: -42px 0; /* 32px icon + 10px spacing */
}

.icon-settings {
  background-position: -84px 0; /* (32px + 10px) × 2 */
}
```

### 2D Grid Sprites

```css
/* Icons arranged in 3×3 grid */
.sprite {
  width: 32px;
  height: 32px;
  background-image: url('icon-sprite.png');
  background-repeat: no-repeat;
}

/* First row */
.icon-1 { background-position: 0 0; }
.icon-2 { background-position: -42px 0; }
.icon-3 { background-position: -84px 0; }

/* Second row */
.icon-4 { background-position: 0 -42px; }
.icon-5 { background-position: -42px -42px; }
.icon-6 { background-position: -84px -42px; }

/* Third row */
.icon-7 { background-position: 0 -84px; }
.icon-8 { background-position: -42px -84px; }
.icon-9 { background-position: -84px -84px; }
```

---

## Icon Sprites

### Social Media Icons

```css
.social-icon {
  width: 40px;
  height: 40px;
  background-image: url('social-sprites.png');
  background-repeat: no-repeat;
  display: inline-block;
}

.icon-facebook { background-position: 0 0; }
.icon-twitter { background-position: -40px 0; }
.icon-instagram { background-position: -80px 0; }
.icon-linkedin { background-position: -120px 0; }
```

**HTML:**
```html
<a href="#" class="social-icon icon-facebook"></a>
<a href="#" class="social-icon icon-twitter"></a>
<a href="#" class="social-icon icon-instagram"></a>
```

---

## Hover States

**Include normal and hover states** in one sprite.

```css
.button {
  width: 150px;
  height: 40px;
  background-image: url('button-sprite.png');
  background-repeat: no-repeat;
  background-position: 0 0; /* Normal state */
  transition: background-position 0.2s;
}

.button:hover {
  background-position: 0 -40px; /* Hover state (shift up) */
}

.button:active {
  background-position: 0 -80px; /* Active state */
}
```

**Sprite layout:**
```
[Normal button ]  ← 0px
[Hover button  ]  ← 40px
[Active button ]  ← 80px
```

---

## Modern Alternatives

**Image sprites are legacy technique.** Modern alternatives often better:

### 1. Icon Fonts

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
<i class="fas fa-home"></i>
```

**Pros:** Scalable, color-changeable
**Cons:** Font file to load, accessibility issues

### 2. SVG Sprites

```html
<svg class="icon">
  <use xlink:href="sprite.svg#icon-home"></use>
</svg>
```

**Pros:** Scalable, accessible, styleable
**Cons:** More complex setup

### 3. Inline SVG

```html
<svg width="24" height="24" viewBox="0 0 24 24">
  <path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z"/>
</svg>
```

**Pros:** Full CSS control, no HTTP request
**Cons:** Larger HTML file

### 4. HTTP/2

With HTTP/2, multiple file requests are less expensive, reducing sprite benefits.

---

## Examples

### Example 1: Navigation Icons

```css
.nav-icon {
  width: 24px;
  height: 24px;
  background-image: url('nav-sprites.png');
  background-repeat: no-repeat;
  display: inline-block;
  vertical-align: middle;
  margin-right: 8px;
}

.icon-home { background-position: 0 0; }
.icon-about { background-position: -24px 0; }
.icon-services { background-position: -48px 0; }
.icon-contact { background-position: -72px 0; }
```

---

### Example 2: Flag Sprites

```css
.flag {
  width: 32px;
  height: 24px;
  background-image: url('flags-sprite.png');
  background-repeat: no-repeat;
  display: inline-block;
}

.flag-us { background-position: 0 0; }
.flag-uk { background-position: -32px 0; }
.flag-fr { background-position: -64px 0; }
.flag-de { background-position: -96px 0; }
.flag-es { background-position: -128px 0; }
```

---

### Example 3: Game Sprites

```css
.game-sprite {
  width: 64px;
  height: 64px;
  background-image: url('character-sprite.png');
  background-repeat: no-repeat;
}

/* Character animations */
.char-idle { background-position: 0 0; }
.char-walk-1 { background-position: -64px 0; }
.char-walk-2 { background-position: -128px 0; }
.char-jump { background-position: -192px 0; }
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `background-position` | All | All | All | All |
| `background-image` | All | All | All | All |

**Support:** Universal (100%).

---

## Best Practices

### Do This

1. **Use PNG for icons with transparency**
   ```css
   background-image: url('icons-sprite.png');
   ```

2. **Group related images**
   - All navigation icons in one sprite
   - All social icons in another sprite

3. **Document sprite positions**
   ```css
   /* Icon positions (32px × 32px + 10px spacing):
      home: 0 0
      user: -42px 0
      settings: -84px 0
   */
   ```

4. **Consider modern alternatives first**
   - SVG sprites for icons
   - Icon fonts for scalability
   - Individual files with HTTP/2

### Avoid This

1. **Don't put unrelated images together**
   ```css
   /* Bad: icons, photos, and backgrounds mixed */
   ```

2. **Don't make sprites too large**
   ```css
   /* Bad: 5000px × 5000px sprite */
   /* Better: Multiple smaller sprites */
   ```

3. **Don't use sprites for large images**
   ```css
   /* Bad: Hero images in sprites */
   /* Better: Separate files */
   ```

4. **Don't forget retina displays**
   ```css
   /* Include @2x version for high-DPI screens */
   @media (-webkit-min-device-pixel-ratio: 2) {
     .sprite {
       background-image: url('sprite@2x.png');
       background-size: 200px 200px; /* Half of 2x dimensions */
     }
   }
   ```

---

## Related Topics

**Prerequisites:**
- [Image Styling](image-styling.md)
- [Backgrounds](../03-box-model/backgrounds.md)

**Next Steps:**
- [Object-Fit](object-fit.md)

**Modern Alternatives:**
- SVG implementation
- Icon fonts
- Web components

---

## Practice Exercise

Create a sprite sheet with 6 social media icons:
- Arrange in 2 rows × 3 columns
- Each icon 40px × 40px
- 10px spacing between icons
- Write CSS classes for each icon

---

## Navigation

**Previous:** [← Image Gallery](image-gallery.md)
**Next:** [Object-Fit →](object-fit.md)
**Up:** [↑ Back to Images & Media](../README.md#1️⃣0️⃣-images--media-6-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Images & Media
**Difficulty:** Intermediate
