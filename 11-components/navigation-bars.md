---
title: CSS Navigation Bars
category: Components
order: 3
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Navigation Bars

> **Quick Summary:** CSS transforms basic lists into professional navigation bars with horizontal/vertical layouts, dropdowns, mobile menus, sticky headers, and active states.

## Table of Contents
- [Introduction](#introduction)
- [Horizontal Navigation](#horizontal-navigation)
- [Vertical Navigation](#vertical-navigation)
- [Sticky Navigation](#sticky-navigation)
- [Dropdown Menus](#dropdown-menus)
- [Mobile Navigation](#mobile-navigation)
- [Active States](#active-states)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

Navigation bars guide users through websites. Good nav design improves usability and accessibility.

---

## Horizontal Navigation

### Basic Horizontal Nav

```css
nav {
  background: #333;
}

nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
}

nav li {
  flex: 1;
}

nav a {
  display: block;
  padding: 15px 20px;
  color: white;
  text-decoration: none;
  text-align: center;
  transition: background 0.3s;
}

nav a:hover {
  background: #555;
}
```

---

### Flexbox Navigation

```css
nav ul {
  display: flex;
  gap: 20px;
  justify-content: space-between; /* Or center, flex-end */
  align-items: center;
}
```

---

## Vertical Navigation

```css
nav {
  width: 250px;
  background: #f8f9fa;
}

nav ul {
  list-style: none;
  padding: 0;
}

nav a {
  display: block;
  padding: 15px 20px;
  color: #333;
  text-decoration: none;
  border-left: 4px solid transparent;
  transition: all 0.3s;
}

nav a:hover {
  background: #e9ecef;
  border-left-color: #007bff;
}
```

---

## Sticky Navigation

```css
nav {
  position: sticky;
  top: 0;
  z-index: 100;
  background: white;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}
```

---

## Dropdown Menus

```css
/* Parent item */
.has-dropdown {
  position: relative;
}

/* Dropdown menu */
.dropdown {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
  background: white;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  min-width: 200px;
}

/* Show on hover */
.has-dropdown:hover .dropdown {
  display: block;
}

/* Dropdown links */
.dropdown a {
  padding: 12px 20px;
  color: #333;
  border-bottom: 1px solid #eee;
}

.dropdown a:hover {
  background: #f8f9fa;
}
```

---

## Mobile Navigation

### Hamburger Menu

```css
/* Hide menu by default on mobile */
@media (max-width: 768px) {
  nav ul {
    display: none;
    flex-direction: column;
  }

  nav ul.open {
    display: flex;
  }

  .hamburger {
    display: block;
    background: none;
    border: none;
    font-size: 2rem;
    cursor: pointer;
  }
}

/* Show menu on desktop */
@media (min-width: 769px) {
  .hamburger {
    display: none;
  }

  nav ul {
    display: flex !important;
  }
}
```

### Hamburger Icon

```css
.hamburger {
  width: 30px;
  height: 24px;
  position: relative;
}

.hamburger span {
  display: block;
  height: 3px;
  background: #333;
  margin-bottom: 6px;
  transition: all 0.3s;
}

.hamburger.open span:nth-child(1) {
  transform: rotate(45deg) translateY(12px);
}

.hamburger.open span:nth-child(2) {
  opacity: 0;
}

.hamburger.open span:nth-child(3) {
  transform: rotate(-45deg) translateY(-12px);
}
```

---

## Active States

```css
/* Current page */
nav a.active {
  background: #007bff;
  color: white;
}

/* Visited link */
nav a:visited {
  color: white;
}

/* Focus (keyboard navigation) */
nav a:focus {
  outline: 2px solid #007bff;
  outline-offset: 2px;
}
```

---

## Examples

### Example 1: Modern Top Nav

```css
nav {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

nav ul {
  display: flex;
  justify-content: center;
  gap: 30px;
  list-style: none;
  margin: 0;
  padding: 0;
}

nav a {
  display: block;
  padding: 20px 25px;
  color: white;
  text-decoration: none;
  font-weight: 600;
  position: relative;
  transition: all 0.3s;
}

nav a::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 50%;
  width: 0;
  height: 3px;
  background: white;
  transform: translateX(-50%);
  transition: width 0.3s;
}

nav a:hover::after {
  width: 80%;
}
```

---

### Example 2: Sidebar Navigation

```css
.sidebar {
  width: 280px;
  height: 100vh;
  background: #2c3e50;
  padding: 20px 0;
  position: fixed;
}

.sidebar ul {
  list-style: none;
  padding: 0;
}

.sidebar a {
  display: flex;
  align-items: center;
  gap: 15px;
  padding: 15px 30px;
  color: #ecf0f1;
  text-decoration: none;
  transition: all 0.3s;
}

.sidebar a:hover {
  background: #34495e;
  padding-left: 40px;
}

.sidebar a.active {
  background: #007bff;
  border-left: 4px solid #0056b3;
}
```

---

### Example 3: Responsive Nav with Dropdown

```css
nav {
  background: white;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
}

.nav-menu {
  display: flex;
  gap: 30px;
  list-style: none;
}

.nav-menu a {
  padding: 25px 0;
  color: #333;
  text-decoration: none;
  font-weight: 600;
}

/* Dropdown */
.dropdown {
  position: relative;
}

.dropdown-menu {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
  background: white;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  min-width: 220px;
}

.dropdown:hover .dropdown-menu {
  display: block;
}

/* Mobile */
@media (max-width: 768px) {
  .nav-menu {
    flex-direction: column;
    position: fixed;
    top: 70px;
    right: -100%;
    width: 100%;
    background: white;
    transition: right 0.3s;
  }

  .nav-menu.active {
    right: 0;
  }
}
```

---

## Best Practices

### ✅ Do This

1. **Use semantic HTML**
   ```html
   <nav>
     <ul>
       <li><a href="/">Home</a></li>
     </ul>
   </nav>
   ```

2. **Add focus states**
   ```css
   nav a:focus { outline: 2px solid #007bff; }
   ```

3. **Make keyboard accessible**
   ```css
   nav a:focus-visible { outline: 2px solid #007bff; }
   ```

4. **Indicate current page**
   ```css
   nav a.active { background: #007bff; }
   ```

### ❌ Avoid This

1. **No mobile menu**
2. **Missing focus indicators**
3. **Dropdown hover-only (inaccessible)**

---

## Related Topics

**Prerequisites:**
- [Flexbox](../06-flexbox/flexbox-intro.md)
- [Position](../05-layout-basics/position.md)

**Next Steps:**
- [Dropdowns](dropdowns.md)

---

## Navigation

**Previous:** [← Buttons](buttons.md)
**Next:** [Dropdowns →](dropdowns.md)
**Up:** [↑ Back to Components](../README.md#1️⃣1️⃣-components-7-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Components
**Difficulty:** Intermediate
