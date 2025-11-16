---
title: Responsive Flexbox Layouts
category: Flexbox
order: 4
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Responsive Flexbox Layouts

> **Quick Summary:** Flexbox naturally adapts to screen sizes with `flex-wrap`, media queries, and responsive `flex` values. Common patterns: responsive grids, navigation menus, and mobile-first layouts.

## Table of Contents
- [Introduction](#introduction)
- [Mobile-First Approach](#mobile-first-approach)
- [Responsive Grid Pattern](#responsive-grid-pattern)
- [Navigation Patterns](#navigation-patterns)
- [Column to Stack](#column-to-stack)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

Flexbox excels at responsive design through:
- Automatic wrapping (`flex-wrap`)
- Flexible sizing (`flex: 1`)
- Direction switching (`flex-direction`)
- Order changes (`order`)

---

## Mobile-First Approach

**Start with mobile layout, enhance for larger screens.**

```css
/* Mobile (default) */
.container {
  display: flex;
  flex-direction: column; /* Stack on mobile */
  gap: 20px;
}

/* Tablet and up */
@media (min-width: 768px) {
  .container {
    flex-direction: row; /* Side-by-side */
  }
}
```

---

## Responsive Grid Pattern

**Auto-fitting cards** that wrap naturally.

```css
.grid {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.card {
  flex: 1 1 300px; /* Min 300px, grows to fill */
  max-width: calc(33.333% - 20px); /* Max 3 columns */
}

@media (max-width: 768px) {
  .card {
    flex: 1 1 100%; /* Full width on mobile */
  }
}
```

**Result:** 3 columns → 2 columns → 1 column automatically.

---

## Navigation Patterns

### Mobile: Hamburger Menu

```css
/* Mobile */
nav {
  display: flex;
  flex-direction: column;
}

.nav-menu {
  display: none; /* Hidden by default */
  flex-direction: column;
}

.nav-menu.open {
  display: flex;
}

/* Desktop */
@media (min-width: 768px) {
  nav {
    flex-direction: row;
    justify-content: space-between;
  }

  .nav-menu {
    display: flex !important;
    flex-direction: row;
    gap: 30px;
  }

  .hamburger {
    display: none;
  }
}
```

---

## Column to Stack

**Common pattern:** Side-by-side → stacked.

```css
.layout {
  display: flex;
  gap: 30px;
}

.sidebar {
  flex: 0 0 250px; /* Fixed width */
}

.main {
  flex: 1; /* Fills space */
}

/* Mobile: Stack */
@media (max-width: 768px) {
  .layout {
    flex-direction: column;
  }

  .sidebar {
    flex: 0 0 auto; /* Full width */
    order: 2; /* Move below content */
  }
}
```

---

## Examples

### Example 1: Responsive Card Grid

```css
.cards {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  padding: 20px;
}

.card {
  flex: 1 1 calc(25% - 20px); /* 4 columns */
  min-width: 250px;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

@media (max-width: 1200px) {
  .card {
    flex: 1 1 calc(33.333% - 20px); /* 3 columns */
  }
}

@media (max-width: 768px) {
  .card {
    flex: 1 1 calc(50% - 20px); /* 2 columns */
  }
}

@media (max-width: 480px) {
  .card {
    flex: 1 1 100%; /* 1 column */
  }
}
```

---

### Example 2: App Layout (Header, Sidebar, Content)

```css
.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

header {
  flex: 0 0 auto;
  padding: 20px;
  background: #333;
  color: white;
}

.main-wrapper {
  display: flex;
  flex: 1;
}

.sidebar {
  flex: 0 0 250px;
  background: #f8f9fa;
}

.content {
  flex: 1;
  padding: 20px;
}

/* Mobile */
@media (max-width: 768px) {
  .main-wrapper {
    flex-direction: column;
  }

  .sidebar {
    flex: 0 0 auto;
  }
}
```

---

### Example 3: Feature Sections

```css
.feature-section {
  display: flex;
  align-items: center;
  gap: 40px;
  margin-bottom: 60px;
}

.feature-image {
  flex: 0 0 50%;
}

.feature-text {
  flex: 1;
}

/* Alternate sides */
.feature-section:nth-child(even) {
  flex-direction: row-reverse;
}

/* Mobile: Stack */
@media (max-width: 768px) {
  .feature-section,
  .feature-section:nth-child(even) {
    flex-direction: column;
  }

  .feature-image {
    flex: 0 0 auto;
    max-width: 100%;
  }
}
```

---

## Best Practices

### ✅ Do This

1. **Use flex-wrap for automatic responsiveness**
   ```css
   display: flex;
   flex-wrap: wrap;
   ```

2. **Combine flex with min-width**
   ```css
   flex: 1 1 300px;
   min-width: 250px;
   ```

3. **Use order for mobile reordering**
   ```css
   @media (max-width: 768px) {
     .sidebar { order: 2; }
   }
   ```

4. **Mobile-first approach**
   ```css
   /* Default: Mobile */
   flex-direction: column;

   /* Desktop */
   @media (min-width: 768px) {
     flex-direction: row;
   }
   ```

### ❌ Avoid This

1. **Fixed widths without flex-wrap**
2. **Too many breakpoints**
3. **Forgetting gap property**

---

## Related Topics

**Prerequisites:**
- [Flex Container](flex-container.md)
- [Flex Items](flex-items.md)

**Next Steps:**
- [Media Queries](../12-responsive-design/media-queries.md)
- [Mobile-First Design](../12-responsive-design/mobile-first.md)

---

## Navigation

**Previous:** [← Flex Items](flex-items.md)
**Next:** [Grid Introduction →](../07-grid/grid-intro.md)
**Up:** [↑ Back to Flexbox](../README.md#6️⃣-flexbox-4-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Flexbox
**Difficulty:** Intermediate
