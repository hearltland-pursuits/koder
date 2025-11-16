---
title: Responsive Grid
category: Responsive Design
order: 3
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Responsive Grid

> **Quick Summary:** Create responsive grid layouts that adapt to different screen sizes using CSS Grid's `auto-fit`, `auto-fill`, `minmax()`, and media queries. Modern alternative to Bootstrap's grid system.

## Table of Contents
- [Introduction](#introduction)
- [Auto-Responsive Grids](#auto-responsive-grids)
- [auto-fit vs auto-fill](#auto-fit-vs-auto-fill)
- [Responsive Breakpoints](#responsive-breakpoints)
- [Grid Template Areas](#grid-template-areas)
- [Mobile-First Grid](#mobile-first-grid)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**Responsive grids** automatically adjust column counts and layouts based on available space. CSS Grid makes this simpler than traditional frameworks like Bootstrap.

**Key techniques:**
- `auto-fit` / `auto-fill` with `repeat()`
- `minmax()` for flexible sizing
- Media queries for breakpoint changes
- Grid template areas for layout switching

---

## Auto-Responsive Grids

### Basic Auto-Responsive Grid

```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}
```

**How it works:**
- `repeat()`: Repeat column definition
- `auto-fit`: Fit as many columns as possible
- `minmax(250px, 1fr)`: Minimum 250px, maximum equal distribution
- Result: Automatically shows 4 columns on desktop, 2 on tablet, 1 on mobile

**Visual example:**
```
Desktop (1200px):
[Item] [Item] [Item] [Item]  ← 4 columns (300px each)

Tablet (768px):
[Item] [Item]                 ← 2 columns (384px each)
[Item] [Item]

Mobile (375px):
[Item]                        ← 1 column (375px)
[Item]
[Item]
```

---

### Responsive Product Grid

```css
.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 30px;
  padding: 20px;
}

.product-card {
  background: white;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}
```

**Result:** Cards automatically reflow as viewport changes.

---

## auto-fit vs auto-fill

### auto-fit

```css
.grid-fit {
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}
```

**Behavior:** Collapses empty columns, stretches existing items to fill space.

**Example:**
```
3 items, 1200px container:
[Item 1 - 400px] [Item 2 - 400px] [Item 3 - 400px]
↑ Each item stretches to fill space
```

---

### auto-fill

```css
.grid-fill {
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
}
```

**Behavior:** Creates empty columns, items don't stretch beyond 1fr.

**Example:**
```
3 items, 1200px container:
[Item 1 - 200px] [Item 2 - 200px] [Item 3 - 200px] [Empty] [Empty] [Empty]
↑ Items stay minimum size, empty columns created
```

---

### When to Use Each

| Use Case | Choice | Why |
|----------|--------|-----|
| Product cards | `auto-fit` | Want cards to expand to fill space |
| Image gallery | `auto-fill` | Want consistent sizing, allow gaps |
| Blog posts | `auto-fit` | Better use of space |
| Icon grid | `auto-fill` | Keep icons same size |

---

## Responsive Breakpoints

### Using Media Queries

```css
.grid {
  display: grid;
  gap: 20px;
}

/* Mobile: 1 column */
.grid {
  grid-template-columns: 1fr;
}

/* Tablet: 2 columns */
@media (min-width: 768px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* Desktop: 3 columns */
@media (min-width: 1024px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

/* Large desktop: 4 columns */
@media (min-width: 1280px) {
  .grid {
    grid-template-columns: repeat(4, 1fr);
  }
}
```

---

### Adjusting Gap Sizes

```css
.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 10px; /* Mobile: Small gap */
}

@media (min-width: 768px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 20px; /* Tablet: Medium gap */
  }
}

@media (min-width: 1024px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
    gap: 30px; /* Desktop: Large gap */
  }
}
```

---

## Grid Template Areas

### Responsive Layout Switching

```css
.page-layout {
  display: grid;
  gap: 20px;
}

/* Mobile: Stacked layout */
.page-layout {
  grid-template-areas:
    "header"
    "content"
    "sidebar"
    "footer";
  grid-template-columns: 1fr;
}

/* Desktop: Sidebar layout */
@media (min-width: 1024px) {
  .page-layout {
    grid-template-areas:
      "header header header"
      "sidebar content content"
      "footer footer footer";
    grid-template-columns: 250px 1fr 1fr;
  }
}

.header { grid-area: header; }
.content { grid-area: content; }
.sidebar { grid-area: sidebar; }
.footer { grid-area: footer; }
```

**Mobile:**
```
[Header  ]
[Content ]
[Sidebar ]
[Footer  ]
```

**Desktop:**
```
[Header    Header    Header  ]
[Sidebar   Content   Content ]
[Footer    Footer    Footer  ]
```

---

## Mobile-First Grid

### Start Small, Add Complexity

```css
/* Mobile-first: Start with 1 column */
.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 15px;
  padding: 15px;
}

/* Add columns as space allows */
@media (min-width: 480px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 768px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    padding: 20px;
  }
}

@media (min-width: 1024px) {
  .grid {
    grid-template-columns: repeat(4, 1fr);
    gap: 30px;
    padding: 30px;
  }
}
```

**Benefits:**
- ✅ Simpler code (add complexity incrementally)
- ✅ Better mobile performance (less CSS to parse)
- ✅ Easier to maintain

---

## Examples

### Example 1: Dashboard Layout

```css
.dashboard {
  display: grid;
  gap: 20px;
  padding: 20px;
}

/* Mobile: Stack all widgets */
.dashboard {
  grid-template-columns: 1fr;
}

/* Tablet: 2 columns */
@media (min-width: 768px) {
  .dashboard {
    grid-template-columns: repeat(2, 1fr);
  }

  /* Make featured widget span 2 columns */
  .widget-featured {
    grid-column: span 2;
  }
}

/* Desktop: 3 columns with sidebar */
@media (min-width: 1024px) {
  .dashboard {
    grid-template-areas:
      "sidebar main main"
      "sidebar stats stats"
      "sidebar activity activity";
    grid-template-columns: 250px 1fr 1fr;
  }

  .sidebar { grid-area: sidebar; }
  .main { grid-area: main; }
  .stats { grid-area: stats; }
  .activity { grid-area: activity; }
}
```

---

### Example 2: Photo Gallery

```css
.gallery {
  display: grid;
  gap: 10px;
}

/* Mobile: 2 columns, tight spacing */
.gallery {
  grid-template-columns: repeat(2, 1fr);
  gap: 5px;
}

/* Tablet: 3 columns */
@media (min-width: 768px) {
  .gallery {
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
  }
}

/* Desktop: Auto-fit with min 250px */
@media (min-width: 1024px) {
  .gallery {
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 15px;
  }
}

.gallery img {
  width: 100%;
  aspect-ratio: 1 / 1;
  object-fit: cover;
  border-radius: 8px;
}
```

---

### Example 3: Article Grid

```css
.articles {
  display: grid;
  gap: 30px;
}

/* Mobile: 1 column */
.articles {
  grid-template-columns: 1fr;
}

/* Tablet: Featured article + 2 columns */
@media (min-width: 768px) {
  .articles {
    grid-template-columns: repeat(2, 1fr);
  }

  .article-featured {
    grid-column: span 2;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
  }
}

/* Desktop: 3 columns with varying sizes */
@media (min-width: 1024px) {
  .articles {
    grid-template-columns: 2fr 1fr 1fr;
  }
}
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| CSS Grid | 57+ | 52+ | 10.1+ | 16+ |
| `auto-fit` / `auto-fill` | 57+ | 52+ | 10.1+ | 16+ |
| `minmax()` | 57+ | 52+ | 10.1+ | 16+ |
| Grid template areas | 57+ | 52+ | 10.1+ | 16+ |

**Support:** Excellent (95%+).

---

## Best Practices

### ✅ Do This

1. **Use auto-fit for flexible grids**
   ```css
   grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
   ```

2. **Start mobile-first**
   ```css
   /* Mobile first */
   grid-template-columns: 1fr;

   @media (min-width: 768px) {
     grid-template-columns: repeat(3, 1fr);
   }
   ```

3. **Adjust gaps for screen size**
   ```css
   gap: 10px; /* Mobile */

   @media (min-width: 768px) {
     gap: 20px; /* Tablet */
   }
   ```

4. **Use named areas for complex layouts**
   ```css
   grid-template-areas:
     "header header"
     "sidebar content"
     "footer footer";
   ```

---

### ❌ Avoid This

1. **Don't use too many columns on mobile**
   ```css
   /* Bad: 4 columns on 375px screen */
   grid-template-columns: repeat(4, 1fr);
   ```

2. **Don't set minimum sizes too large**
   ```css
   /* Bad: Forces 1 column on 768px tablet */
   minmax(800px, 1fr)
   ```

3. **Don't forget gap adjustments**
   ```css
   /* Bad: Same 30px gap on mobile and desktop */
   gap: 30px;
   ```

4. **Don't use desktop-first approach**
   ```css
   /* Harder to maintain */
   grid-template-columns: repeat(4, 1fr);

   @media (max-width: 768px) {
     grid-template-columns: 1fr;
   }
   ```

---

## Related Topics

**Prerequisites:**
- [CSS Grid Basics](../07-grid/grid-container.md)
- [Media Queries](media-queries.md)

**Next Steps:**
- [Responsive Images](../10-images-media/responsive-images.md)
- [Mobile-First Design](mobile-first.md)

---

## Practice Exercise

Create a responsive card grid:
- Mobile: 1 column, 10px gap
- Tablet: 2 columns, 20px gap
- Desktop: auto-fit with 280px minimum, 30px gap
- Cards have 1:1 aspect ratio
- Includes hover effects

---

## Navigation

**Previous:** [← Viewport](viewport.md)
**Next:** [Media Queries →](media-queries.md)
**Up:** [↑ Back to Responsive Design](../README.md#1️⃣2️⃣-responsive-design-5-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Responsive Design
**Difficulty:** Intermediate
