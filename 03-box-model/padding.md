---
title: CSS Padding
category: Box Model
order: 5
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Padding

> **Quick Summary:** Padding creates space INSIDE elements, between content and border. Background colors extend through padding. Padding never collapses and cannot be negative.

## Key Properties

**Syntax:**
```css
.element {
  padding: [all];
  padding: [vertical] [horizontal];
  padding: [top] [horizontal] [bottom];
  padding: [top] [right] [bottom] [left];
}
```

**Individual sides:**
```css
.element {
  padding-top: 20px;
  padding-right: 15px;
  padding-bottom: 20px;
  padding-left: 15px;
}
```

## Common Patterns

**Equal padding all sides:**
```css
.button {
  padding: 15px;
}
```

**Horizontal and vertical:**
```css
.button {
  padding: 10px 20px; /* vertical: 10px, horizontal: 20px */
}
```

**Container with breathing room:**
```css
.container {
  padding: 40px 20px; /* More vertical, less horizontal */
}
```

## Padding vs Margin

| Padding | Margin |
|---------|--------|
| Inside element | Outside element |
| Background visible | Transparent |
| Can't be negative | Can be negative |
| Never collapses | Vertical margins collapse |
| Increases click area | Doesn't increase click area |

## Examples

**Button with padding:**
```css
.button {
  padding: 12px 24px;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 5px;
}
```

**Card with internal spacing:**
```css
.card {
  padding: 20px;
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 8px;
}
```

**Responsive padding:**
```css
.container {
  padding: 20px;
}

@media (min-width: 768px) {
  .container {
    padding: 40px;
  }
}
```

## Browser Support

Universal support across all browsers.

## Best Practices

✅ **Use padding for internal spacing**
```css
.box {
  padding: 20px; /* Space inside element */
}
```

✅ **Use padding to increase click area**
```css
.button {
  padding: 15px 30px; /* Larger, easier to click */
}
```

❌ **Don't forget `box-sizing: border-box`**
```css
* {
  box-sizing: border-box; /* Includes padding in width */
}
```

---

**Last Updated:** November 15, 2025
**Category:** Box Model
**Difficulty:** Beginner
