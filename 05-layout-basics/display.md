---
title: CSS Display Property
category: Layout Basics
order: 1
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Display Property

> **Quick Summary:** The `display` property controls how elements are laid out. Block elements stack vertically, inline elements flow horizontally, and modern values like `flex` and `grid` enable advanced layouts.

## Display Values

| Value | Behavior | Use Case |
|-------|----------|----------|
| `block` | Full width, new line | Headings, divs, sections |
| `inline` | Flows with text | Links, spans, emphasis |
| `inline-block` | Inline + block properties | Buttons, badges |
| `none` | Hidden (not rendered) | Hide elements |
| `flex` | Flexbox container | 1D layouts |
| `grid` | Grid container | 2D layouts |

## Block

**Default for:** `<div>`, `<p>`, `<h1>`-`<h6>`, `<section>`, `<article>`

```css
.block {
  display: block;
}
```

**Characteristics:**
- Takes full width available
- Starts on new line
- Can set width/height
- Respects all margins/padding

## Inline

**Default for:** `<span>`, `<a>`, `<strong>`, `<em>`

```css
.inline {
  display: inline;
}
```

**Characteristics:**
- Flows with text
- Width determined by content
- Cannot set width/height
- Vertical margins/padding don't push other elements

## Inline-Block

**Best of both worlds:**

```css
.inline-block {
  display: inline-block;
}
```

**Characteristics:**
- Flows horizontally (like inline)
- Can set width/height (like block)
- Respects all margins/padding

**Common use:** Navigation links, buttons

```css
.nav a {
  display: inline-block;
  padding: 10px 20px;
  margin: 0 5px;
}
```

## None

**Hides element completely:**

```css
.hidden {
  display: none; /* Element doesn't exist in layout */
}
```

**vs `visibility: hidden`:**
```css
.invisible {
  visibility: hidden; /* Hidden but space reserved */
}
```

## Flex

**Creates flexbox container:**

```css
.flex-container {
  display: flex;
}
```

[See Flexbox guide for details](../06-flexbox/flexbox-intro.md)

## Grid

**Creates grid container:**

```css
.grid-container {
  display: grid;
}
```

[See Grid guide for details](../07-grid/grid-intro.md)

## Examples

**Horizontal navigation:**
```css
.nav {
  display: flex;
  gap: 20px;
}

.nav a {
  display: inline-block;
  padding: 10px 15px;
}
```

**Card grid:**
```css
.card-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
```

**Toggle visibility:**
```css
.mobile-menu {
  display: none;
}

@media (max-width: 768px) {
  .mobile-menu {
    display: block;
  }
}
```

## Browser Support

Universal support across all browsers.

## Best Practices

✅ **Use semantic HTML first**
```html
<!-- Already block by default -->
<div>, <section>, <header>

<!-- Already inline by default -->
<a>, <span>, <strong>
```

✅ **Use flex/grid for layouts**
```css
.container {
  display: grid; /* Modern layout */
}
```

❌ **Don't overuse `display: none`**
```css
/* Bad for accessibility */
.element { display: none; }

/* Better - screen readers can still access */
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  overflow: hidden;
}
```

---

**Last Updated:** November 15, 2025
**Category:** Layout Basics
**Difficulty:** Beginner
