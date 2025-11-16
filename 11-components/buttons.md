---
title: CSS Buttons
category: Components
order: 5
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Buttons

> **Quick Summary:** CSS transforms basic `<button>` and `<a>` elements into interactive, accessible UI components with hover effects, multiple states, sizes, and styles.

## Table of Contents
- [Introduction](#introduction)
- [Basic Button Styling](#basic-button-styling)
- [Button States](#button-states)
- [Button Variants](#button-variants)
- [Button Sizes](#button-sizes)
- [Icon Buttons](#icon-buttons)
- [Button Groups](#button-groups)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

Buttons are the primary call-to-action elements. Good button design improves usability and conversions.

---

## Basic Button Styling

```css
.btn {
  display: inline-block;
  padding: 12px 24px;
  background: #007bff;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  font-weight: 600;
  text-align: center;
  text-decoration: none;
  cursor: pointer;
  transition: all 0.3s ease;
}
```

---

## Button States

### Hover

```css
.btn:hover {
  background: #0056b3;
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0,0,0,0.2);
}
```

### Active (Pressed)

```css
.btn:active {
  transform: translateY(0);
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
```

### Focus

```css
.btn:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(0,123,255,0.25);
}
```

### Disabled

```css
.btn:disabled {
  background: #ccc;
  color: #666;
  cursor: not-allowed;
  opacity: 0.6;
  transform: none;
}
```

---

## Button Variants

### Primary

```css
.btn-primary {
  background: #007bff;
  color: white;
}

.btn-primary:hover {
  background: #0056b3;
}
```

### Secondary

```css
.btn-secondary {
  background: #6c757d;
  color: white;
}
```

### Outline

```css
.btn-outline {
  background: transparent;
  border: 2px solid #007bff;
  color: #007bff;
}

.btn-outline:hover {
  background: #007bff;
  color: white;
}
```

### Ghost

```css
.btn-ghost {
  background: transparent;
  border: none;
  color: #007bff;
}

.btn-ghost:hover {
  background: rgba(0,123,255,0.1);
}
```

---

## Button Sizes

```css
.btn-sm {
  padding: 8px 16px;
  font-size: 0.875rem;
}

.btn-md {
  padding: 12px 24px;
  font-size: 1rem;
}

.btn-lg {
  padding: 16px 32px;
  font-size: 1.25rem;
}
```

---

## Icon Buttons

```css
.btn-icon {
  display: inline-flex;
  align-items: center;
  gap: 10px;
}

.btn-icon::before {
  content: "→";
  font-size: 1.2rem;
}

/* Icon only */
.btn-circle {
  width: 48px;
  height: 48px;
  padding: 0;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}
```

---

## Button Groups

```css
.btn-group {
  display: inline-flex;
}

.btn-group .btn {
  border-radius: 0;
  border-right: 1px solid rgba(255,255,255,0.3);
}

.btn-group .btn:first-child {
  border-radius: 6px 0 0 6px;
}

.btn-group .btn:last-child {
  border-radius: 0 6px 6px 0;
  border-right: none;
}
```

---

## Examples

### Example 1: Modern Button Set

```css
.btn {
  padding: 14px 28px;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.btn-primary {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
}

.btn-primary:hover {
  transform: scale(1.05);
  box-shadow: 0 8px 16px rgba(102,126,234,0.4);
}

.btn-primary:active {
  transform: scale(0.98);
}
```

---

### Example 2: Pill Button

```css
.btn-pill {
  padding: 12px 32px;
  border-radius: 50px;
  background: #007bff;
  color: white;
  border: none;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s;
}

.btn-pill:hover {
  background: #0056b3;
  box-shadow: 0 6px 12px rgba(0,123,255,0.3);
}
```

---

### Example 3: Animated Button

```css
.btn-animated {
  position: relative;
  overflow: hidden;
}

.btn-animated::before {
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  width: 0;
  height: 0;
  border-radius: 50%;
  background: rgba(255,255,255,0.3);
  transform: translate(-50%, -50%);
  transition: width 0.6s, height 0.6s;
}

.btn-animated:hover::before {
  width: 300px;
  height: 300px;
}
```

---

## Best Practices

### ✅ Do This

1. **Minimum size 44x44px (touch target)**
   ```css
   .btn { min-height: 44px; min-width: 44px; }
   ```

2. **Clear hover/focus states**
   ```css
   .btn:hover { background: #0056b3; }
   .btn:focus { box-shadow: 0 0 0 3px rgba(0,123,255,0.25); }
   ```

3. **Use semantic HTML**
   ```html
   <button type="submit">Submit</button>
   <a href="/page" class="btn">Link Button</a>
   ```

### ❌ Avoid This

1. **Too many button styles on one page**
2. **Missing disabled state**
3. **No focus indicator**

---

## Related Topics

**Prerequisites:**
- [Transitions](../09-visual-effects/transitions.md)

**Next Steps:**
- [Navigation Bars](navigation-bars.md)

---

## Navigation

**Previous:** [← Forms](forms.md)
**Next:** [Navigation Bars →](navigation-bars.md)
**Up:** [↑ Back to Components](../README.md#1️⃣1️⃣-components-7-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Components
**Difficulty:** Beginner
