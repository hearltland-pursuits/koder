---
title: CSS Height & Width
category: Box Model
order: 6
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Height & Width

> **Quick Summary:** Width and height properties control element dimensions. Use `max-width`, `min-width`, `max-height`, `min-height` for responsive, flexible sizing.

## Properties

**Basic sizing:**
```css
.element {
  width: 300px;
  height: 200px;
}
```

**Responsive sizing:**
```css
.container {
  width: 100%;          /* Full width of parent */
  max-width: 1200px;    /* Never wider than 1200px */
  min-width: 320px;     /* Never narrower than 320px */
}
```

## Width

**Values:** `auto`, length, `%`, `vw`, `vh`

```css
/* Fixed width */
.fixed { width: 500px; }

/* Percentage (of parent) */
.half { width: 50%; }

/* Viewport width */
.full-screen { width: 100vw; }

/* Auto (default - fits content) */
.auto { width: auto; }
```

## Max-Width

**Most important for responsive design:**

```css
.container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto; /* Center */
}
```

**Why this pattern works:**
- Mobile: `width: 100%` fills screen
- Desktop: `max-width: 1200px` prevents excessive width
- Always centered with `margin: 0 auto`

## Height

**Values:** `auto`, length, `%`, `vh`

```css
/* Fixed height */
.box { height: 300px; }

/* Percentage (parent must have defined height) */
.half-height { height: 50%; }

/* Viewport height */
.hero { height: 100vh; } /* Full screen height */

/* Auto (default - fits content) */
.auto { height: auto; }
```

## Min/Max Height

```css
/* Flexible height with constraints */
.flexible {
  min-height: 200px;  /* At least 200px tall */
  max-height: 600px;  /* Never taller than 600px */
}

/* Common: full viewport, minimum content */
.full-page {
  min-height: 100vh; /* At least full screen */
}
```

## Common Patterns

**Responsive container:**
```css
.container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}
```

**Full-screen hero:**
```css
.hero {
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
```

**Flexible sidebar:**
```css
.sidebar {
  width: 250px;
  min-height: 100vh; /* Full height minimum */
}
```

## Box-Sizing Impact

```css
/* content-box (default) */
.box {
  width: 300px;
  padding: 20px;
  border: 5px solid;
  /* Actual width: 300 + 40 (padding) + 10 (border) = 350px */
}

/* border-box (recommended) */
.box {
  box-sizing: border-box;
  width: 300px;
  padding: 20px;
  border: 5px solid;
  /* Actual width: 300px (padding/border included) */
}
```

## Browser Support

Universal support across all browsers.

## Best Practices

**Use `max-width` for responsive containers**
```css
.container {
  width: 100%;
  max-width: 1200px;
}
```

**Use `min-height` instead of `height` for flexibility**
```css
.section {
  min-height: 100vh; /* Can grow if content exceeds */
}
```

**Avoid fixed heights** (content may overflow)
```css
/* Bad - content might overflow */
.box { height: 200px; }

/* Good - flexible */
.box { min-height: 200px; }
```

---

**Last Updated:** November 15, 2025
**Category:** Box Model
**Difficulty:** Beginner
