---
title: Tooltips
category: Components
order: 5
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Tooltips

> **Quick Summary:** Tooltips provide contextual information on hover or focus. Built with CSS pseudo-elements (`::before`, `::after`), positioning, and transitions. Pure CSS solution for simple tooltips, JavaScript for complex needs.

## Table of Contents
- [Introduction](#introduction)
- [Basic Tooltip Structure](#basic-tooltip-structure)
- [Pure CSS Tooltips](#pure-css-tooltips)
- [Tooltip Positions](#tooltip-positions)
- [Tooltip Arrows](#tooltip-arrows)
- [Animated Tooltips](#animated-tooltips)
- [Multi-line Tooltips](#multi-line-tooltips)
- [Accessibility](#accessibility)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**Tooltips** are small popups that appear when hovering over or focusing on an element, providing additional context or information.

**Common uses:**
- Icon explanations
- Button descriptions
- Form field hints
- Abbreviation expansions
- Additional context for truncated text

**Trigger methods:**
- `:hover` (mouse)
- `:focus` (keyboard)
- JavaScript click (mobile)

---

## Basic Tooltip Structure

**HTML:**
```html
<span class="tooltip" data-tooltip="This is a tooltip">
  Hover me
</span>
```

**CSS (using `::before` and `::after`):**
```css
.tooltip {
  position: relative;
  cursor: help;
  border-bottom: 1px dotted #333;
}

/* Tooltip box */
.tooltip::before {
  content: attr(data-tooltip);
  position: absolute;
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  background: #333;
  color: white;
  padding: 8px 12px;
  border-radius: 4px;
  font-size: 14px;
  white-space: nowrap;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.3s, visibility 0.3s;
  z-index: 1000;
}

/* Show on hover */
.tooltip:hover::before {
  opacity: 1;
  visibility: visible;
}
```

**Visual:**
```
Before hover:    After hover:
[Hover me]       ┌─────────────────┐
                 │ This is a tooltip│
                 └─────────────────┘
                      [Hover me]
```

---

## Pure CSS Tooltips

**Complete implementation with arrow.**

```css
.tooltip {
  position: relative;
  display: inline-block;
  cursor: help;
}

/* Tooltip box */
.tooltip::before {
  content: attr(data-tooltip);
  position: absolute;
  bottom: calc(100% + 10px); /* 10px gap */
  left: 50%;
  transform: translateX(-50%);
  background: #333;
  color: white;
  padding: 8px 12px;
  border-radius: 4px;
  font-size: 14px;
  white-space: nowrap;
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease;
  z-index: 1000;
}

/* Arrow */
.tooltip::after {
  content: '';
  position: absolute;
  bottom: calc(100% + 2px); /* Arrow tip position */
  left: 50%;
  transform: translateX(-50%);
  border: 8px solid transparent;
  border-top-color: #333;
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease;
  z-index: 1001;
}

/* Show on hover/focus */
.tooltip:hover::before,
.tooltip:hover::after,
.tooltip:focus::before,
.tooltip:focus::after {
  opacity: 1;
  visibility: visible;
}
```

---

## Tooltip Positions

**Top, bottom, left, right positions.**

### Top (Default)

```css
.tooltip-top::before {
  bottom: calc(100% + 10px);
  left: 50%;
  transform: translateX(-50%);
}

.tooltip-top::after {
  bottom: calc(100% + 2px);
  left: 50%;
  transform: translateX(-50%);
  border-top-color: #333;
}
```

### Bottom

```css
.tooltip-bottom::before {
  top: calc(100% + 10px);
  left: 50%;
  transform: translateX(-50%);
}

.tooltip-bottom::after {
  top: calc(100% + 2px);
  left: 50%;
  transform: translateX(-50%);
  border-bottom-color: #333;
}
```

### Left

```css
.tooltip-left::before {
  top: 50%;
  right: calc(100% + 10px);
  transform: translateY(-50%);
}

.tooltip-left::after {
  top: 50%;
  right: calc(100% + 2px);
  transform: translateY(-50%);
  border-left-color: #333;
}
```

### Right

```css
.tooltip-right::before {
  top: 50%;
  left: calc(100% + 10px);
  transform: translateY(-50%);
}

.tooltip-right::after {
  top: 50%;
  left: calc(100% + 2px);
  transform: translateY(-50%);
  border-right-color: #333;
}
```

**Visual:**
```
Top:           ┌──────┐
               │Tooltip│
               └───▼──┘
               [Element]

Bottom:        [Element]
               ┌───▲──┐
               │Tooltip│
               └──────┘

Left:     ┌──────┐
          │Tooltip│◄── [Element]
          └──────┘

Right:    [Element] ──►┌──────┐
                       │Tooltip│
                       └──────┘
```

---

## Tooltip Arrows

**Creating the arrow using CSS borders.**

```css
/* Arrow pointing down (for top tooltip) */
.tooltip::after {
  content: '';
  position: absolute;
  border: 8px solid transparent;
  border-top-color: #333; /* Arrow color matches tooltip */
}

/* Arrow pointing up (for bottom tooltip) */
.tooltip::after {
  border-bottom-color: #333;
}

/* Arrow pointing right (for left tooltip) */
.tooltip::after {
  border-left-color: #333;
}

/* Arrow pointing left (for right tooltip) */
.tooltip::after {
  border-right-color: #333;
}
```

**How CSS border arrows work:**
```css
/* Border trick visualization */
.arrow {
  width: 0;
  height: 0;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-top: 10px solid #333;
}
/* Creates: ▼ */
```

---

## Animated Tooltips

**Smooth animations on show/hide.**

### Fade + Slide

```css
.tooltip::before {
  opacity: 0;
  visibility: hidden;
  transform: translateX(-50%) translateY(10px);
  transition: all 0.3s ease;
}

.tooltip:hover::before {
  opacity: 1;
  visibility: visible;
  transform: translateX(-50%) translateY(0);
}
```

### Scale + Fade

```css
.tooltip::before {
  opacity: 0;
  visibility: hidden;
  transform: translateX(-50%) scale(0.8);
  transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.tooltip:hover::before {
  opacity: 1;
  visibility: visible;
  transform: translateX(-50%) scale(1);
}
```

### Delayed Show

```css
.tooltip::before,
.tooltip::after {
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.3s ease, visibility 0.3s ease;
  transition-delay: 0s; /* No delay on hide */
}

.tooltip:hover::before,
.tooltip:hover::after {
  opacity: 1;
  visibility: visible;
  transition-delay: 0.5s; /* 0.5s delay on show */
}
```

---

## Multi-line Tooltips

**Tooltips with wrapping text.**

```css
.tooltip-multiline::before {
  content: attr(data-tooltip);
  white-space: normal; /* Allow wrapping */
  max-width: 200px; /* Limit width */
  text-align: center;
}
```

**HTML:**
```html
<span class="tooltip tooltip-multiline" data-tooltip="This is a longer tooltip that wraps to multiple lines">
  Hover for info
</span>
```

---

## Accessibility

**Making tooltips accessible for keyboard and screen readers.**

### ARIA Attributes

```html
<!-- Accessible tooltip -->
<button
  class="tooltip"
  data-tooltip="Save your changes"
  aria-label="Save your changes">
  💾
</button>
```

### Focus Support

```css
/* Show on both hover AND focus */
.tooltip:hover::before,
.tooltip:focus::before {
  opacity: 1;
  visibility: visible;
}
```

### Keyboard-Friendly

```html
<!-- Make non-interactive elements focusable -->
<span class="tooltip" tabindex="0" data-tooltip="Information">
  ℹ️
</span>
```

### Screen Reader Consideration

```html
<!-- Option 1: Use aria-label (hides tooltip from screen readers) -->
<button aria-label="Delete item">
  🗑️
</button>

<!-- Option 2: Use title attribute (screen readers announce it) -->
<button title="Delete item">
  🗑️
</button>

<!-- Option 3: Visually hidden text -->
<button>
  🗑️
  <span class="sr-only">Delete item</span>
</button>
```

---

## Examples

### Example 1: Icon Tooltips

```css
.icon-tooltip {
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 24px;
  height: 24px;
  background: #007bff;
  color: white;
  border-radius: 50%;
  font-size: 14px;
  cursor: help;
}

.icon-tooltip::before {
  content: attr(data-tooltip);
  position: absolute;
  bottom: calc(100% + 8px);
  left: 50%;
  transform: translateX(-50%);
  background: #333;
  color: white;
  padding: 6px 10px;
  border-radius: 4px;
  font-size: 12px;
  white-space: nowrap;
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease;
  z-index: 1000;
}

.icon-tooltip:hover::before {
  opacity: 1;
  visibility: visible;
}
```

**HTML:**
```html
<span class="icon-tooltip" data-tooltip="Click for more information">ℹ️</span>
```

---

### Example 2: Form Field Hints

```css
.form-field {
  position: relative;
  margin-bottom: 20px;
}

.form-hint {
  position: absolute;
  top: 50%;
  right: 10px;
  transform: translateY(-50%);
  width: 20px;
  height: 20px;
  background: #6c757d;
  color: white;
  border-radius: 50%;
  text-align: center;
  line-height: 20px;
  font-size: 12px;
  cursor: help;
}

.form-hint::before {
  content: attr(data-tooltip);
  position: absolute;
  bottom: calc(100% + 10px);
  right: 0;
  background: #333;
  color: white;
  padding: 8px 12px;
  border-radius: 4px;
  font-size: 13px;
  white-space: nowrap;
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease;
  z-index: 1000;
}

.form-hint:hover::before {
  opacity: 1;
  visibility: visible;
}
```

**HTML:**
```html
<div class="form-field">
  <input type="password" placeholder="Password">
  <span class="form-hint" data-tooltip="Min 8 characters, 1 number, 1 special character">?</span>
</div>
```

---

### Example 3: Colored Tooltips

```css
/* Success tooltip */
.tooltip-success::before {
  background: #28a745;
}

.tooltip-success::after {
  border-top-color: #28a745;
}

/* Warning tooltip */
.tooltip-warning::before {
  background: #ffc107;
  color: #333;
}

.tooltip-warning::after {
  border-top-color: #ffc107;
}

/* Error tooltip */
.tooltip-error::before {
  background: #dc3545;
}

.tooltip-error::after {
  border-top-color: #dc3545;
}
```

---

### Example 4: Truncated Text Tooltips

```css
.truncate-text {
  position: relative;
  max-width: 200px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  cursor: help;
}

.truncate-text:hover::before {
  content: attr(data-full-text);
  position: absolute;
  bottom: calc(100% + 8px);
  left: 0;
  background: #333;
  color: white;
  padding: 8px 12px;
  border-radius: 4px;
  white-space: normal;
  max-width: 300px;
  opacity: 1;
  visibility: visible;
  z-index: 1000;
}
```

**HTML:**
```html
<p class="truncate-text" data-full-text="This is a very long text that gets truncated">
  This is a very long text that gets truncated
</p>
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `::before/::after` | All | All | All | All |
| `attr()` | All | All | All | All |
| `:hover` | All | All | All | All |
| `:focus` | All | All | All | All |

**Support:** Excellent (99%+ global).

---

## Best Practices

### ✅ Do This

1. **Use `attr(data-tooltip)` for content**
   ```css
   content: attr(data-tooltip);
   ```

2. **Support both hover and focus**
   ```css
   .tooltip:hover::before,
   .tooltip:focus::before { opacity: 1; }
   ```

3. **Add transitions for smooth appearance**
   ```css
   transition: opacity 0.3s, visibility 0.3s;
   ```

4. **Use high z-index**
   ```css
   z-index: 1000;
   ```

5. **Include ARIA attributes**
   ```html
   <span aria-label="Description">ℹ️</span>
   ```

### ❌ Avoid This

1. **Tooltips on mobile (hover doesn't work)**
   ```css
   /* Consider click-based alternatives for mobile */
   ```

2. **Too much text**
   ```html
   <!-- Keep tooltips concise (1-2 lines max) -->
   <span data-tooltip="This is way too much text for a tooltip...">
   ```

3. **Missing arrow positioning**
   ```css
   /* Arrow might not align with tooltip */
   ```

4. **Blocking important content**
   ```css
   /* Tooltip shouldn't cover critical UI elements */
   ```

---

## Related Topics

**Prerequisites:**
- [Pseudo-Elements](../08-selectors-advanced/pseudo-elements.md)
- [Position](../05-layout-basics/position.md)
- [Transitions](../09-visual-effects/transitions.md)

**Next Steps:**
- [Dropdowns](dropdowns.md)
- [Modals (Advanced topic)](#)

---

## Practice Exercise

Create a tooltip system that:
- Supports top, bottom, left, right positions
- Has smooth fade + slide animation
- Shows arrow pointing to element
- Works with keyboard (Tab + hover)
- Changes color based on tooltip type (info, success, warning, error)

---

## Navigation

**Previous:** [← Dropdowns](dropdowns.md)
**Next:** [Pagination →](pagination.md)
**Up:** [↑ Back to Components](../README.md#1️⃣1️⃣-components-7-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Components
**Difficulty:** Intermediate
