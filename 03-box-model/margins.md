---
title: CSS Margins
category: Box Model
order: 4
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Margins

> **Quick Summary:** Margins create space OUTSIDE elements, between them and their neighbors. They're transparent, can collapse (vertical margins combine), and can be negative (for overlapping effects).

## Key Properties

**Syntax:**
```css
.element {
  margin: [all];
  margin: [vertical] [horizontal];
  margin: [top] [horizontal] [bottom];
  margin: [top] [right] [bottom] [left];
}
```

**Individual sides:**
```css
.element {
  margin-top: 20px;
  margin-right: 15px;
  margin-bottom: 20px;
  margin-left: 15px;
}
```

## Common Patterns

**Center block element:**
```css
.container {
  width: 800px;
  margin: 0 auto; /* Centers horizontally */
}
```

**Equal margins all sides:**
```css
.box {
  margin: 20px;
}
```

**Vertical margins only:**
```css
.section {
  margin: 40px 0; /* top/bottom: 40px, left/right: 0 */
}
```

## Margin Collapse

**Vertical margins between siblings collapse** (use larger value):

```css
.box1 { margin-bottom: 30px; }
.box2 { margin-top: 20px; }
/* Actual space between: 30px (not 50px) */
```

**Prevent collapse:**
- Use padding instead
- Add border or `overflow: hidden`
- Use Flexbox or Grid (they don't collapse)

## Negative Margins

```css
.overlap {
  margin-top: -20px; /* Pulls element up 20px */
}

.pull-left {
  margin-left: -10px; /* Pulls element left 10px */
}
```

## Auto Margins

```css
/* Center horizontally */
.centered {
  width: 600px;
  margin-left: auto;
  margin-right: auto;
}

/* Push to right */
.right-aligned {
  margin-left: auto;
}
```

## Browser Support

Universal support across all browsers.

## Best Practices

✅ **Use margins for spacing between elements**
```css
.card {
  margin-bottom: 20px; /* Space between cards */
}
```

✅ **Use `auto` for centering**
```css
.container {
  max-width: 1200px;
  margin: 0 auto;
}
```

❌ **Don't use margins for internal spacing** (use padding)
```css
/* Bad */
.box { margin: 20px; } /* Inside element? Use padding */

/* Good */
.box { padding: 20px; }
```

---

**Last Updated:** November 15, 2025
**Category:** Box Model
**Difficulty:** Beginner
