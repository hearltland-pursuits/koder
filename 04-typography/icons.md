---
title: Icon Fonts
category: Typography
order: 4
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Icon Fonts

> **Quick Summary:** Icon fonts render icons as scalable text characters. Font Awesome and Material Icons are popular libraries. Use `<i>` tags with classes, style like text (color, size). Modern alternative: SVG icons for better accessibility and performance.

## Table of Contents
- [Introduction](#introduction)
- [Font Awesome](#font-awesome)
- [Material Icons](#material-icons)
- [Icon Fonts vs SVG](#icon-fonts-vs-svg)
- [Styling Icon Fonts](#styling-icon-fonts)
- [Accessibility](#accessibility)
- [Examples](#examples)
- [Best Practices](#best-practices)

---

## Introduction

**Icon fonts:** Icons rendered as font characters, scalable and styleable like text.

**Popular libraries:**
- Font Awesome (7000+ icons)
- Material Icons (Google, 2000+ icons)
- Bootstrap Icons
- Ionicons

**Benefits:**
- ✅ Scalable (vector-based)
- ✅ Style with CSS (color, size, shadow)
- ✅ One HTTP request (all icons in font file)
- ✅ Easy to implement

**Drawbacks:**
- ❌ Accessibility challenges
- ❌ Limited multi-color support
- ❌ Can't animate individual parts
- ❌ May fail if custom fonts blocked

---

## Font Awesome

### Setup (CDN)

**Add to HTML `<head>`:**
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
```

### Basic Usage

```html
<!-- Solid style (default) -->
<i class="fa-solid fa-heart"></i>

<!-- Regular style -->
<i class="fa-regular fa-heart"></i>

<!-- Brands -->
<i class="fa-brands fa-github"></i>
```

### Sizing

```html
<!-- Size classes -->
<i class="fa-solid fa-heart fa-xs"></i>  <!-- Extra small -->
<i class="fa-solid fa-heart fa-sm"></i>  <!-- Small -->
<i class="fa-solid fa-heart fa-lg"></i>  <!-- Large -->
<i class="fa-solid fa-heart fa-2x"></i>  <!-- 2× -->
<i class="fa-solid fa-heart fa-3x"></i>  <!-- 3× -->
<i class="fa-solid fa-heart fa-10x"></i> <!-- 10× -->
```

### Common Icons

```html
<!-- UI Icons -->
<i class="fa-solid fa-bars"></i>          <!-- Menu -->
<i class="fa-solid fa-search"></i>        <!-- Search -->
<i class="fa-solid fa-user"></i>          <!-- User -->
<i class="fa-solid fa-envelope"></i>      <!-- Email -->
<i class="fa-solid fa-phone"></i>         <!-- Phone -->
<i class="fa-solid fa-shopping-cart"></i> <!-- Cart -->
<i class="fa-solid fa-heart"></i>         <!-- Like -->
<i class="fa-solid fa-star"></i>          <!-- Star -->
<i class="fa-solid fa-times"></i>         <!-- Close -->
<i class="fa-solid fa-check"></i>         <!-- Checkmark -->
```

---

## Material Icons

### Setup (CDN)

**Add to HTML `<head>`:**
```html
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
```

### Basic Usage

```html
<span class="material-icons">home</span>
<span class="material-icons">search</span>
<span class="material-icons">favorite</span>
```

### Sizing

```css
/* Default size: 24px */
.material-icons { font-size: 24px; }

/* Custom sizes */
.material-icons.md-18 { font-size: 18px; }
.material-icons.md-24 { font-size: 24px; }
.material-icons.md-36 { font-size: 36px; }
.material-icons.md-48 { font-size: 48px; }
```

```html
<span class="material-icons md-18">home</span>
<span class="material-icons md-48">home</span>
```

### Styles

```html
<!-- Filled (default) -->
<span class="material-icons">favorite</span>

<!-- Outlined -->
<span class="material-icons-outlined">favorite</span>

<!-- Rounded -->
<span class="material-icons-round">favorite</span>

<!-- Sharp -->
<span class="material-icons-sharp">favorite</span>
```

---

## Icon Fonts vs SVG

### Icon Fonts

**Pros:**
- Easy to implement
- One file for all icons
- Style with CSS

**Cons:**
- Accessibility issues
- Can fail if fonts blocked
- Limited to single color (usually)
- Screen readers may read icon codes

### SVG Icons

**Pros:**
- Better accessibility (semantic HTML)
- Multi-color support
- Animatable (individual parts)
- Always renders (no font dependency)

**Cons:**
- More complex implementation
- Multiple HTTP requests (without sprite)

**Modern recommendation:** Use SVG when possible, icon fonts for quick prototypes.

---

## Styling Icon Fonts

### Color

```css
.icon {
  color: #3498db; /* Icon color */
}

.icon-red {
  color: #e74c3c;
}
```

### Size

```css
.icon-small {
  font-size: 14px;
}

.icon-large {
  font-size: 48px;
}
```

### Rotation

```html
<!-- Font Awesome rotation -->
<i class="fa-solid fa-sync fa-spin"></i> <!-- Spinning -->
<i class="fa-solid fa-arrow-right fa-rotate-90"></i> <!-- 90° -->
<i class="fa-solid fa-arrow-right fa-flip-horizontal"></i> <!-- Flipped -->
```

### Shadow & Effects

```css
.icon-shadow {
  text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
}

.icon-glow {
  color: #3498db;
  text-shadow: 0 0 10px rgba(52, 152, 219, 0.8);
}
```

---

## Accessibility

### ❌ Bad: No Accessibility

```html
<!-- Screen readers don't understand this -->
<i class="fa-solid fa-heart"></i>
```

### ✅ Good: With aria-label

```html
<!-- Decorative icon (purely visual) -->
<i class="fa-solid fa-heart" aria-hidden="true"></i>

<!-- Meaningful icon (conveys information) -->
<i class="fa-solid fa-envelope" aria-label="Email"></i>

<!-- Icon with text (hide from screen readers) -->
<button>
  <i class="fa-solid fa-trash" aria-hidden="true"></i>
  Delete
</button>
```

### Screen Reader Text

```html
<button>
  <i class="fa-solid fa-search" aria-hidden="true"></i>
  <span class="sr-only">Search</span>
</button>
```

```css
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0,0,0,0);
  border: 0;
}
```

---

## Examples

### Example 1: Button with Icon

```html
<button class="btn-primary">
  <i class="fa-solid fa-download" aria-hidden="true"></i>
  Download
</button>
```

```css
.btn-primary {
  padding: 10px 20px;
  background: #3498db;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.btn-primary i {
  margin-right: 8px;
}
```

---

### Example 2: Social Media Icons

```html
<div class="social-icons">
  <a href="#" aria-label="Facebook">
    <i class="fa-brands fa-facebook" aria-hidden="true"></i>
  </a>
  <a href="#" aria-label="Twitter">
    <i class="fa-brands fa-twitter" aria-hidden="true"></i>
  </a>
  <a href="#" aria-label="Instagram">
    <i class="fa-brands fa-instagram" aria-hidden="true"></i>
  </a>
</div>
```

```css
.social-icons a {
  display: inline-block;
  width: 40px;
  height: 40px;
  line-height: 40px;
  text-align: center;
  background: #3498db;
  color: white;
  border-radius: 50%;
  margin: 0 5px;
  transition: background 0.3s;
}

.social-icons a:hover {
  background: #2980b9;
}

.social-icons i {
  font-size: 18px;
}
```

---

### Example 3: Navigation Icons

```html
<nav>
  <a href="/home">
    <i class="material-icons" aria-hidden="true">home</i>
    <span>Home</span>
  </a>
  <a href="/search">
    <i class="material-icons" aria-hidden="true">search</i>
    <span>Search</span>
  </a>
  <a href="/profile">
    <i class="material-icons" aria-hidden="true">person</i>
    <span>Profile</span>
  </a>
</nav>
```

```css
nav a {
  display: flex;
  align-items: center;
  padding: 10px 15px;
  color: #333;
  text-decoration: none;
  transition: background 0.3s;
}

nav a:hover {
  background: #f0f0f0;
}

nav i {
  margin-right: 10px;
  color: #3498db;
}
```

---

### Example 4: Loading Spinner

```html
<div class="loading">
  <i class="fa-solid fa-spinner fa-spin fa-3x"></i>
  <p>Loading...</p>
</div>
```

```css
.loading {
  text-align: center;
  padding: 50px;
}

.loading i {
  color: #3498db;
}
```

---

## Best Practices

### ✅ Do This

**1. Use aria-hidden for decorative icons**
```html
<button>
  <i class="fa-solid fa-save" aria-hidden="true"></i>
  Save
</button>
```

**2. Add aria-label for standalone icons**
```html
<button aria-label="Close">
  <i class="fa-solid fa-times" aria-hidden="true"></i>
</button>
```

**3. Use semantic HTML**
```html
<!-- Good - semantic button -->
<button type="button">
  <i class="fa-solid fa-heart"></i>
  Like
</button>

<!-- Bad - div pretending to be button -->
<div onclick="like()">
  <i class="fa-solid fa-heart"></i>
</div>
```

**4. Include fallback text**
```html
<a href="/search" aria-label="Search">
  <i class="fa-solid fa-search" aria-hidden="true"></i>
  <span class="sr-only">Search</span>
</a>
```

### ❌ Avoid This

**1. Don't use icons without context**
```html
<!-- Bad - no label -->
<button>
  <i class="fa-solid fa-save"></i>
</button>

<!-- Good - has label -->
<button aria-label="Save">
  <i class="fa-solid fa-save" aria-hidden="true"></i>
</button>
```

**2. Don't rely solely on color**
```html
<!-- Bad - color alone -->
<i class="fa-solid fa-exclamation" style="color: red;"></i>

<!-- Good - icon + text -->
<span class="error">
  <i class="fa-solid fa-exclamation" aria-hidden="true"></i>
  Error: Invalid input
</span>
```

---

## Browser Support

**Universal support** - Icon fonts work in all modern browsers (IE8+).

---

**Last Updated:** November 15, 2025
**Category:** Typography
**Difficulty:** Beginner

**Related Topics:**
- [Fonts](fonts.md) - Font properties
- [Google Fonts](google-fonts.md) - Custom web fonts
- [Accessibility](../13-modern-css/accessibility.md) - Accessible CSS
