---
title: Dropdown Menus
category: Components
order: 4
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Dropdown Menus

> **Quick Summary:** Dropdown menus reveal additional content on hover or click. Built with CSS positioning, transitions, and the `:hover` pseudo-class. Often enhanced with JavaScript for mobile support.

## Table of Contents
- [Introduction](#introduction)
- [Basic Dropdown Structure](#basic-dropdown-structure)
- [Pure CSS Dropdowns](#pure-css-dropdowns)
- [Hover-Based Dropdowns](#hover-based-dropdowns)
- [Click-Based Dropdowns](#click-based-dropdowns)
- [Mega Menus](#mega-menus)
- [Mobile Considerations](#mobile-considerations)
- [Accessibility](#accessibility)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**Dropdown menus** (also called **drop-down menus** or **pulldown menus**) are navigation components that reveal hidden options when triggered.

**Common uses:**
- Navigation menus
- Settings menus
- User profile menus
- Filter/sort options
- Action menus

**Trigger methods:**
- `:hover` (desktop)
- `:focus-within` (keyboard accessible)
- JavaScript click handlers (mobile-friendly)

---

## Basic Dropdown Structure

**HTML structure:**
```html
<div class="dropdown">
  <button class="dropdown-toggle">Menu ▾</button>
  <div class="dropdown-menu">
    <a href="#" class="dropdown-item">Option 1</a>
    <a href="#" class="dropdown-item">Option 2</a>
    <a href="#" class="dropdown-item">Option 3</a>
  </div>
</div>
```

**Key elements:**
- **Container** (`.dropdown`): Wrapper with `position: relative`
- **Toggle** (`.dropdown-toggle`): Button or link that triggers menu
- **Menu** (`.dropdown-menu`): Hidden container with `position: absolute`
- **Items** (`.dropdown-item`): Individual menu options

---

## Pure CSS Dropdowns

**Basic implementation using CSS only.**

```css
/* Container */
.dropdown {
  position: relative;
  display: inline-block;
}

/* Toggle button */
.dropdown-toggle {
  background: #007bff;
  color: white;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  border-radius: 4px;
}

/* Dropdown menu (hidden by default) */
.dropdown-menu {
  display: none; /* Hidden initially */
  position: absolute;
  top: 100%; /* Below toggle */
  left: 0;
  background: white;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  min-width: 200px;
  z-index: 1000;
}

/* Show menu on hover */
.dropdown:hover .dropdown-menu {
  display: block;
}

/* Menu items */
.dropdown-item {
  display: block;
  padding: 10px 20px;
  color: #333;
  text-decoration: none;
  transition: background 0.2s;
}

.dropdown-item:hover {
  background: #f8f9fa;
}
```

---

## Hover-Based Dropdowns

**Opens on hover** (desktop-friendly).

```css
.dropdown {
  position: relative;
}

.dropdown-menu {
  opacity: 0;
  visibility: hidden;
  position: absolute;
  top: 100%;
  left: 0;
  transform: translateY(-10px);
  transition: all 0.3s ease;
}

/* Show on hover */
.dropdown:hover .dropdown-menu {
  opacity: 1;
  visibility: visible;
  transform: translateY(0);
}
```

**Visual transition:**
```
Before hover:    After hover:
[Button ▾]       [Button ▾]
                 ┌─────────┐
                 │ Option 1│
                 │ Option 2│
                 │ Option 3│
                 └─────────┘
```

---

## Click-Based Dropdowns

**Opens on click** (requires JavaScript).

**JavaScript:**
```javascript
document.querySelectorAll('.dropdown-toggle').forEach(toggle => {
  toggle.addEventListener('click', function(e) {
    e.stopPropagation();
    const dropdown = this.closest('.dropdown');
    dropdown.classList.toggle('is-open');
  });
});

// Close when clicking outside
document.addEventListener('click', function() {
  document.querySelectorAll('.dropdown.is-open').forEach(dropdown => {
    dropdown.classList.remove('is-open');
  });
});
```

**CSS:**
```css
.dropdown-menu {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
}

.dropdown.is-open .dropdown-menu {
  display: block;
}
```

---

## Mega Menus

**Large dropdowns** with multiple columns and rich content.

```css
.mega-menu {
  position: static; /* Important for full-width */
}

.mega-menu-content {
  display: none;
  position: absolute;
  left: 0;
  right: 0;
  background: white;
  border-top: 3px solid #007bff;
  box-shadow: 0 8px 16px rgba(0,0,0,0.1);
  padding: 40px;
}

.mega-menu:hover .mega-menu-content {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 30px;
}

.mega-menu-section h3 {
  font-size: 1.1rem;
  margin-bottom: 15px;
  color: #333;
}

.mega-menu-section a {
  display: block;
  padding: 8px 0;
  color: #666;
  text-decoration: none;
  transition: color 0.2s;
}

.mega-menu-section a:hover {
  color: #007bff;
}
```

**HTML:**
```html
<nav class="main-nav">
  <div class="mega-menu">
    <a href="#" class="nav-link">Products ▾</a>
    <div class="mega-menu-content">
      <div class="mega-menu-section">
        <h3>Category 1</h3>
        <a href="#">Product A</a>
        <a href="#">Product B</a>
        <a href="#">Product C</a>
      </div>
      <div class="mega-menu-section">
        <h3>Category 2</h3>
        <a href="#">Product D</a>
        <a href="#">Product E</a>
      </div>
    </div>
  </div>
</nav>
```

---

## Mobile Considerations

**Hover doesn't work on mobile** - use click/touch instead.

```css
/* Desktop: hover */
@media (min-width: 768px) {
  .dropdown:hover .dropdown-menu {
    display: block;
  }
}

/* Mobile: click (requires JS) */
@media (max-width: 767px) {
  .dropdown.is-open .dropdown-menu {
    display: block;
    position: static; /* Stack instead of absolute */
    box-shadow: none;
    border: none;
    border-top: 1px solid #ddd;
  }
}
```

**Mobile-friendly pattern:**
```css
/* Mobile accordion-style */
@media (max-width: 767px) {
  .dropdown {
    display: block;
  }

  .dropdown-toggle {
    width: 100%;
    text-align: left;
  }

  .dropdown-menu {
    position: static;
    display: none;
    background: #f8f9fa;
    padding: 10px;
  }

  .dropdown.is-open .dropdown-menu {
    display: block;
  }
}
```

---

## Accessibility

**Make dropdowns accessible** for keyboard and screen readers.

```html
<!-- Accessible dropdown -->
<div class="dropdown">
  <button
    class="dropdown-toggle"
    aria-haspopup="true"
    aria-expanded="false"
    id="dropdown-1">
    Menu ▾
  </button>
  <div
    class="dropdown-menu"
    role="menu"
    aria-labelledby="dropdown-1">
    <a href="#" class="dropdown-item" role="menuitem">Option 1</a>
    <a href="#" class="dropdown-item" role="menuitem">Option 2</a>
  </div>
</div>
```

**Keyboard navigation:**
```javascript
// Arrow keys to navigate
dropdown.addEventListener('keydown', function(e) {
  if (e.key === 'ArrowDown') {
    // Move to next item
  } else if (e.key === 'ArrowUp') {
    // Move to previous item
  } else if (e.key === 'Escape') {
    // Close menu
  }
});
```

**CSS for focus-within:**
```css
/* Show dropdown when focused (keyboard accessible) */
.dropdown:focus-within .dropdown-menu {
  display: block;
}
```

---

## Examples

### Example 1: User Menu

```css
.user-menu {
  position: relative;
}

.user-avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  cursor: pointer;
}

.user-dropdown {
  display: none;
  position: absolute;
  top: 100%;
  right: 0;
  margin-top: 10px;
  background: white;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
  min-width: 200px;
}

.user-menu:hover .user-dropdown {
  display: block;
}

.user-dropdown-header {
  padding: 15px;
  border-bottom: 1px solid #eee;
  font-weight: 600;
}

.user-dropdown-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 12px 15px;
  color: #333;
  text-decoration: none;
  transition: background 0.2s;
}

.user-dropdown-item:hover {
  background: #f8f9fa;
}

.user-dropdown-divider {
  height: 1px;
  background: #eee;
  margin: 5px 0;
}
```

---

### Example 2: Navbar Dropdown

```css
.navbar {
  display: flex;
  background: #333;
  padding: 0 20px;
}

.nav-item {
  position: relative;
}

.nav-link {
  display: block;
  padding: 20px;
  color: white;
  text-decoration: none;
  transition: background 0.2s;
}

.nav-link:hover {
  background: rgba(255,255,255,0.1);
}

.nav-dropdown {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
  background: white;
  border-radius: 0 0 4px 4px;
  box-shadow: 0 8px 16px rgba(0,0,0,0.1);
  min-width: 200px;
}

.nav-item:hover .nav-dropdown {
  display: block;
}

.nav-dropdown-item {
  display: block;
  padding: 12px 20px;
  color: #333;
  text-decoration: none;
  transition: all 0.2s;
}

.nav-dropdown-item:hover {
  background: #007bff;
  color: white;
}
```

---

### Example 3: Animated Dropdown

```css
.dropdown-menu {
  opacity: 0;
  visibility: hidden;
  position: absolute;
  top: calc(100% + 10px);
  left: 0;
  transform: translateY(-20px) scale(0.95);
  transform-origin: top left;
  transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.dropdown:hover .dropdown-menu {
  opacity: 1;
  visibility: visible;
  transform: translateY(0) scale(1);
}
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `:hover` | All | All | All | All |
| `:focus-within` | 60+ | 52+ | 10.1+ | 79+ |
| `position: absolute` | All | All | All | All |

**Support:** Excellent (99%+ with fallbacks).

---

## Best Practices

### Do This

1. **Use `position: relative` on container**
   ```css
   .dropdown { position: relative; }
   ```

2. **Add smooth transitions**
   ```css
   .dropdown-menu {
     transition: opacity 0.3s, transform 0.3s;
   }
   ```

3. **Include z-index for stacking**
   ```css
   .dropdown-menu { z-index: 1000; }
   ```

4. **Support keyboard navigation**
   ```css
   .dropdown:focus-within .dropdown-menu { display: block; }
   ```

5. **Use ARIA attributes**
   ```html
   <button aria-haspopup="true" aria-expanded="false">
   ```

### Avoid This

1. **Hover-only on mobile**
   ```css
   /* Doesn't work on touch devices */
   .dropdown:hover .dropdown-menu { display: block; }
   ```

2. **Missing z-index**
   ```css
   /* Dropdown might appear behind other elements */
   ```

3. **No transition delay on hover out**
   ```css
   /* Menu disappears immediately if mouse leaves */
   ```

---

## Related Topics

**Prerequisites:**
- [Position](../05-layout-basics/position.md)
- [Z-Index](../05-layout-basics/z-index.md)
- [Pseudo-Classes](../08-selectors-advanced/pseudo-classes.md)

**Next Steps:**
- [Tooltips](tooltips.md)
- [Navigation Bars](navigation-bars.md)

---

## Practice Exercise

Create a dropdown menu that:
- Opens on hover (desktop) and click (mobile)
- Has smooth slide-down animation
- Closes when clicking outside
- Works with keyboard (Tab, Escape)

---

## Navigation

**Previous:** [← Buttons](buttons.md)
**Next:** [Tooltips →](tooltips.md)
**Up:** [↑ Back to Components](../README.md#1️⃣1️⃣-components-7-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Components
**Difficulty:** Intermediate
