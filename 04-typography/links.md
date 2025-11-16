---
title: Styling Links
category: Typography
order: 5
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Styling Links

> **Quick Summary:** CSS provides four link pseudo-classes: `:link` (unvisited), `:visited` (previously clicked), `:hover` (mouse over), `:active` (being clicked), and `:focus` (keyboard focus). Style in LVHFA order to avoid specificity issues. Always provide visual feedback for accessibility.

## Table of Contents
- [Introduction](#introduction)
- [Link Pseudo-Classes](#link-pseudo-classes)
- [LVHFA Order](#lvhfa-order)
- [Common Link Styles](#common-link-styles)
- [Removing Underlines](#removing-underlines)
- [Button-Style Links](#button-style-links)
- [Accessibility](#accessibility)
- [Examples](#examples)
- [Best Practices](#best-practices)

---

## Introduction

**Links (`<a>` tags)** are interactive elements that need visual feedback to show their state.

**Default browser styles:**
```css
a:link { color: blue; text-decoration: underline; }
a:visited { color: purple; }
a:hover { cursor: pointer; }
```

**Why custom styling matters:**
- Brand consistency
- Better user experience
- Accessibility (clear interactive elements)
- Visual hierarchy

---

## Link Pseudo-Classes

### :link (Unvisited Links)

**Targets links NOT yet visited:**
```css
a:link {
  color: #3498db;
}
```

### :visited (Visited Links)

**Targets links previously clicked:**
```css
a:visited {
  color: #9b59b6; /* Different color shows visited */
}
```

**Security note:** Browsers limit what you can style on `:visited` (prevents tracking)

### :hover (Mouse Over)

**Targets links when mouse hovers:**
```css
a:hover {
  color: #2980b9;
  text-decoration: underline;
}
```

### :active (Being Clicked)

**Targets links while mouse button is pressed:**
```css
a:active {
  color: #1a5276;
}
```

### :focus (Keyboard Focus)

**Targets links when focused (Tab key):**
```css
a:focus {
  outline: 2px solid #3498db;
  outline-offset: 2px;
}
```

---

## LVHFA Order

**CRITICAL:** Style link pseudo-classes in this order:

```css
a:link { } /* L - Link */
a:visited { } /* V - Visited */
a:hover { } /* H - Hover */
a:focus { } /* F - Focus */
a:active { } /* A - Active */
```

**Mnemonic:** **L**o**V**e **H****A**te or **L**o**V**e, **H**ate, **F**ear, **A**nger

**Why this order matters:**
- Specificity: All have same specificity (0-0-1-1)
- Cascade: Later rules override earlier ones
- Wrong order breaks hover/active states

**Example of broken order:**
```css
/* BAD - hover won't work on visited links */
a:visited { color: purple; }
a:hover { color: red; } /* Visited links stay purple! */

/* GOOD - hover works */
a:visited { color: purple; }
a:hover { color: red; } /* All links turn red on hover */
```

---

## Common Link Styles

### Basic Link Styling

```css
a {
  color: #3498db;
  text-decoration: none;
  transition: color 0.3s;
}

a:hover {
  color: #2980b9;
  text-decoration: underline;
}

a:focus {
  outline: 2px solid #3498db;
  outline-offset: 2px;
}
```

### Underline Styles

```css
/* No underline by default, underline on hover */
a {
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

/* Dotted underline */
a {
  text-decoration: underline dotted;
}

/* Custom underline with border */
a {
  text-decoration: none;
  border-bottom: 1px solid #3498db;
}

a:hover {
  border-bottom-color: #2980b9;
}
```

### Animated Underline

```css
a {
  position: relative;
  text-decoration: none;
  color: #3498db;
}

a::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: #3498db;
  transition: width 0.3s;
}

a:hover::after {
  width: 100%;
}
```

---

## Removing Underlines

### Method 1: text-decoration

```css
a {
  text-decoration: none; /* Removes underline */
}
```

### Method 2: Maintain Accessibility

```css
/* Remove underline but keep on hover/focus */
a {
  text-decoration: none;
}

a:hover,
a:focus {
  text-decoration: underline; /* Feedback for interaction */
}
```

**IMPORTANT:** Always provide visual feedback (color change, underline on hover, outline on focus)

---

## Button-Style Links

### Basic Button Link

```css
.btn-link {
  display: inline-block;
  padding: 10px 20px;
  background: #3498db;
  color: white;
  text-decoration: none;
  border-radius: 5px;
  transition: background 0.3s;
}

.btn-link:hover {
  background: #2980b9;
}

.btn-link:active {
  background: #1a5276;
}
```

### Outline Button Link

```css
.btn-outline {
  display: inline-block;
  padding: 10px 20px;
  border: 2px solid #3498db;
  color: #3498db;
  text-decoration: none;
  border-radius: 5px;
  transition: all 0.3s;
}

.btn-outline:hover {
  background: #3498db;
  color: white;
}
```

---

## Accessibility

### Requirements

1. **Visual distinction:** Links must be visually different from text
2. **Focus indicators:** Clear outline for keyboard users
3. **Color contrast:** Meet WCAG AA (4.5:1 for normal text)
4. **Don't rely on color alone:** Use underlines or other indicators

### Accessible Link Styles

```css
/* Clear distinction from body text */
body {
  color: #333;
}

a {
  color: #0066cc; /* Blue, sufficient contrast */
  text-decoration: underline; /* Visual indicator */
}

a:hover {
  color: #004499;
  text-decoration: none;
}

/* Strong focus indicator */
a:focus {
  outline: 3px solid #0066cc;
  outline-offset: 2px;
}
```

### Inaccessible Link Styles

```css
/* BAD - no visual distinction */
a {
  color: inherit; /* Same as body text */
  text-decoration: none; /* No underline */
}

/* BAD - removed focus outline */
a:focus {
  outline: none; /* Keyboard users can't see focus */
}
```

---

## Examples

### Example 1: Navigation Links

```html
<nav>
  <a href="/">Home</a>
  <a href="/about">About</a>
  <a href="/services">Services</a>
  <a href="/contact">Contact</a>
</nav>
```

```css
nav a {
  color: #333;
  text-decoration: none;
  padding: 10px 15px;
  display: inline-block;
  transition: background 0.3s;
}

nav a:hover {
  background: #f0f0f0;
  color: #3498db;
}

nav a:focus {
  outline: 2px solid #3498db;
  outline-offset: -2px;
}
```

---

### Example 2: Text Links with Underline Animation

```css
.text-link {
  color: #3498db;
  text-decoration: none;
  position: relative;
  display: inline-block;
}

.text-link::after {
  content: '';
  position: absolute;
  width: 100%;
  height: 2px;
  bottom: 0;
  left: 0;
  background-color: #3498db;
  transform: scaleX(0);
  transform-origin: bottom right;
  transition: transform 0.3s;
}

.text-link:hover::after {
  transform: scaleX(1);
  transform-origin: bottom left;
}
```

---

### Example 3: Card Links

```html
<a href="/article" class="card-link">
  <div class="card">
    <h3>Article Title</h3>
    <p>Article description...</p>
  </div>
</a>
```

```css
.card-link {
  text-decoration: none;
  color: inherit;
  display: block;
}

.card {
  padding: 20px;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  transition: all 0.3s;
}

.card-link:hover .card {
  border-color: #3498db;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  transform: translateY(-4px);
}

.card-link:focus {
  outline: 3px solid #3498db;
  outline-offset: 4px;
}
```

---

### Example 4: Social Media Links

```css
.social-link {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  background: #3498db;
  color: white;
  border-radius: 50%;
  text-decoration: none;
  transition: background 0.3s;
}

.social-link:hover {
  background: #2980b9;
}

.social-link:focus {
  outline: 3px solid #3498db;
  outline-offset: 2px;
}
```

---

## Best Practices

### Do This

**1. Use LVHFA order**
```css
a:link { }
a:visited { }
a:hover { }
a:focus { }
a:active { }
```

**2. Provide visual feedback**
```css
a {
  text-decoration: underline; /* Or color change */
}

a:hover {
  color: #2980b9; /* Visual change */
}
```

**3. Keep focus outlines**
```css
a:focus {
  outline: 2px solid #3498db;
  outline-offset: 2px;
}
```

**4. Use transitions for smooth effects**
```css
a {
  transition: color 0.3s, background 0.3s;
}
```

### Avoid This

**1. Don't remove all visual indicators**
```css
/* BAD */
a {
  color: inherit;
  text-decoration: none;
}
```

**2. Don't remove focus outlines**
```css
/* BAD - keyboard users can't navigate */
a:focus {
  outline: none;
}
```

**3. Don't style :visited radically different**
```css
/* BAD - privacy/security issue */
a:visited {
  background: red; /* Browsers may block this */
}
```

**4. Don't use wrong order**
```css
/* BAD - hover won't work properly */
a:hover { }
a:visited { }
```

---

## Browser Support

**Universal support** - All link pseudo-classes work in all browsers.

---

**Last Updated:** November 15, 2025
**Category:** Typography
**Difficulty:** Beginner

**Related Topics:**
- [Text Styling](text-styling.md) - Text formatting
- [Pseudo-Classes](../08-selectors-advanced/pseudo-classes.md) - Advanced selectors
- [Accessibility](../13-modern-css/accessibility.md) - Accessible CSS
