---
title: CSS Overflow
category: Layout Basics
order: 3
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Overflow

> **Quick Summary:** The `overflow` property controls what happens when content exceeds element's box. Options: clip it, scroll it, or let it overflow.

## Property

**Syntax:**
```css
.element {
  overflow: visible | hidden | scroll | auto;
}
```

## Values

### `visible` (default)

Content overflows, nothing is clipped.

```css
.visible {
  overflow: visible;
}
```

**Use when:** You want overflow to show (dropdowns, tooltips)

### `hidden`

Content is clipped, no scrollbars.

```css
.hidden {
  overflow: hidden;
}
```

**Use when:**
- Hiding overflow intentionally
- Creating image crops
- Clearing floats

### `scroll`

Always shows scrollbars (even if no overflow).

```css
.scroll {
  overflow: scroll;
}
```

**Rarely used** - `auto` is better

### `auto`

Scrollbars appear only when needed.

```css
.auto {
  height: 300px;
  overflow: auto;
}
```

**Most common** - smart scrolling

## Directional Overflow

**Control X and Y separately:**

```css
.element {
  overflow-x: hidden;  /* No horizontal scroll */
  overflow-y: auto;    /* Vertical scroll if needed */
}
```

**Common pattern:**
```css
.sidebar {
  height: 100vh;
  overflow-y: auto; /* Scroll vertically if content exceeds */
  overflow-x: hidden; /* Never scroll horizontally */
}
```

## Examples

**Scrollable container:**
```css
.chat-box {
  height: 400px;
  overflow-y: auto;
  border: 1px solid #ddd;
  padding: 10px;
}
```

**Image crop:**
```css
.avatar {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  overflow: hidden; /* Crops image to circle */
}

.avatar img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```

**Clearfix (old technique):**
```css
.clearfix {
  overflow: hidden; /* Contains floated children */
}
```

## Browser Support

Universal support across all browsers.

## Best Practices

**Use `overflow: auto` for scrolling**
```css
.scrollable {
  max-height: 500px;
  overflow: auto;
}
```

**Use `overflow: hidden` to crop content**
```css
.image-container {
  overflow: hidden;
  border-radius: 8px;
}
```

**Don't use `overflow: scroll`**
```css
/* Bad - always shows scrollbars */
.element { overflow: scroll; }

/* Good - shows only when needed */
.element { overflow: auto; }
```

---

**Last Updated:** November 15, 2025
**Category:** Layout Basics
**Difficulty:** Beginner
