---
title: Pagination
category: Components
order: 7
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# Pagination

> **Quick Summary:** Pagination components split content across multiple pages. Styled with buttons, numbers, and navigation controls. Use Flexbox for layout, hover states for interactivity, and ARIA attributes for accessibility.

## Table of Contents
- [Introduction](#introduction)
- [Basic Pagination](#basic-pagination)
- [Number Buttons](#number-buttons)
- [Active State](#active-state)
- [Disabled State](#disabled-state)
- [Ellipsis for Long Lists](#ellipsis-for-long-lists)
- [Responsive Pagination](#responsive-pagination)
- [Accessibility](#accessibility)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

**Pagination** divides content into discrete pages, allowing users to navigate through large datasets without overwhelming the interface.

**Common patterns:**
- Numbered pages (1, 2, 3...)
- Previous/Next buttons
- First/Last page links
- Ellipsis (...) for large page counts

---

## Basic Pagination

```css
.pagination {
  display: flex;
  list-style: none;
  gap: 5px;
  padding: 0;
  margin: 20px 0;
}

.page-link {
  display: block;
  padding: 8px 12px;
  background: white;
  border: 1px solid #ddd;
  border-radius: 4px;
  text-decoration: none;
  color: #007bff;
  transition: all 0.2s;
}

.page-link:hover {
  background: #007bff;
  color: white;
  border-color: #007bff;
}
```

**HTML:**
```html
<ul class="pagination">
  <li><a href="#" class="page-link">Previous</a></li>
  <li><a href="#" class="page-link">1</a></li>
  <li><a href="#" class="page-link">2</a></li>
  <li><a href="#" class="page-link">3</a></li>
  <li><a href="#" class="page-link">Next</a></li>
</ul>
```

---

## Number Buttons

```css
.pagination {
  display: flex;
  gap: 5px;
  list-style: none;
  padding: 0;
}

.page-item {
  min-width: 40px;
}

.page-link {
  display: flex;
  align-items: center;
  justify-content: center;
  min-width: 40px;
  height: 40px;
  padding: 0 12px;
  background: white;
  border: 1px solid #dee2e6;
  color: #007bff;
  text-decoration: none;
  border-radius: 4px;
  font-weight: 500;
  transition: all 0.2s;
}

.page-link:hover {
  background: #e9ecef;
  border-color: #dee2e6;
}
```

---

## Active State

```css
.page-item.active .page-link {
  background: #007bff;
  border-color: #007bff;
  color: white;
  cursor: default;
  pointer-events: none; /* Prevent clicking active page */
}
```

**HTML:**
```html
<ul class="pagination">
  <li class="page-item"><a href="#" class="page-link">1</a></li>
  <li class="page-item active"><a href="#" class="page-link">2</a></li>
  <li class="page-item"><a href="#" class="page-link">3</a></li>
</ul>
```

---

## Disabled State

```css
.page-item.disabled .page-link {
  color: #6c757d;
  background: #fff;
  border-color: #dee2e6;
  cursor: not-allowed;
  opacity: 0.5;
  pointer-events: none;
}
```

**Use case:** Disable "Previous" on first page, "Next" on last page.

```html
<ul class="pagination">
  <li class="page-item disabled">
    <a href="#" class="page-link">Previous</a>
  </li>
  <li class="page-item"><a href="#" class="page-link">1</a></li>
  <li class="page-item"><a href="#" class="page-link">Next</a></li>
</ul>
```

---

## Ellipsis for Long Lists

```css
.page-ellipsis {
  display: flex;
  align-items: center;
  padding: 0 12px;
  color: #6c757d;
}
```

**HTML:**
```html
<ul class="pagination">
  <li class="page-item"><a href="#" class="page-link">1</a></li>
  <li class="page-item"><a href="#" class="page-link">2</a></li>
  <li class="page-ellipsis">...</li>
  <li class="page-item"><a href="#" class="page-link">9</a></li>
  <li class="page-item"><a href="#" class="page-link">10</a></li>
</ul>
```

**Smart pagination pattern:**
```
[Prev] [1] ... [4] [5] [6] ... [20] [Next]
              ↑  ↑  ↑
          Current page (5)
```

---

## Responsive Pagination

### Hide Numbers on Mobile

```css
.pagination {
  display: flex;
  gap: 5px;
}

/* Desktop: Show all */
.page-number {
  display: block;
}

/* Mobile: Hide numbers, keep Prev/Next */
@media (max-width: 576px) {
  .page-number {
    display: none;
  }

  .page-prev,
  .page-next {
    display: block;
  }
}
```

### Compact Mobile View

```css
@media (max-width: 576px) {
  .page-link {
    min-width: 36px;
    height: 36px;
    padding: 0 8px;
    font-size: 14px;
  }

  .pagination {
    gap: 3px;
  }
}
```

---

## Accessibility

**ARIA attributes** for screen readers:

```html
<nav aria-label="Page navigation">
  <ul class="pagination">
    <li class="page-item disabled">
      <a href="#" class="page-link" aria-disabled="true" tabindex="-1">
        Previous
      </a>
    </li>

    <li class="page-item">
      <a href="#" class="page-link" aria-label="Page 1">1</a>
    </li>

    <li class="page-item active" aria-current="page">
      <a href="#" class="page-link" aria-label="Page 2 (current)">2</a>
    </li>

    <li class="page-item">
      <a href="#" class="page-link" aria-label="Page 3">3</a>
    </li>

    <li class="page-item">
      <a href="#" class="page-link" aria-label="Next page">Next</a>
    </li>
  </ul>
</nav>
```

**Keyboard navigation:**
- Tab to navigate between page links
- Enter to activate link
- Disabled links should have `tabindex="-1"`

---

## Examples

### Example 1: Material Design Style

```css
.pagination-material {
  display: flex;
  gap: 8px;
  list-style: none;
  padding: 0;
}

.pagination-material .page-link {
  display: flex;
  align-items: center;
  justify-content: center;
  min-width: 48px;
  height: 48px;
  border-radius: 50%;
  background: transparent;
  border: none;
  color: rgba(0, 0, 0, 0.87);
  font-weight: 500;
  transition: background 0.2s;
}

.pagination-material .page-link:hover {
  background: rgba(0, 0, 0, 0.04);
}

.pagination-material .page-item.active .page-link {
  background: #1976d2;
  color: white;
}
```

---

### Example 2: Minimal Style

```css
.pagination-minimal {
  display: flex;
  gap: 10px;
  list-style: none;
  padding: 0;
}

.pagination-minimal .page-link {
  padding: 8px 12px;
  background: transparent;
  border: none;
  color: #333;
  text-decoration: underline;
  text-decoration-color: transparent;
  transition: text-decoration-color 0.2s;
}

.pagination-minimal .page-link:hover {
  text-decoration-color: #333;
}

.pagination-minimal .page-item.active .page-link {
  color: #007bff;
  text-decoration-color: #007bff;
  font-weight: 600;
}
```

---

### Example 3: Pills Style

```css
.pagination-pills {
  display: flex;
  gap: 8px;
  list-style: none;
  padding: 0;
}

.pagination-pills .page-link {
  display: block;
  padding: 6px 16px;
  border-radius: 20px;
  background: #f8f9fa;
  border: 1px solid transparent;
  color: #495057;
  text-decoration: none;
  transition: all 0.2s;
}

.pagination-pills .page-link:hover {
  background: #e9ecef;
}

.pagination-pills .page-item.active .page-link {
  background: #007bff;
  color: white;
}
```

---

### Example 4: Large Pagination

```css
.pagination-lg .page-link {
  min-width: 48px;
  height: 48px;
  padding: 0 16px;
  font-size: 18px;
}
```

### Example 5: Small Pagination

```css
.pagination-sm .page-link {
  min-width: 32px;
  height: 32px;
  padding: 0 8px;
  font-size: 14px;
}
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| Flexbox | 29+ | 28+ | 9+ | 12+ |
| ARIA attributes | All | All | All | All |

**Support:** Universal (99%+).

---

## Best Practices

### ✅ Do This

1. **Use semantic HTML (nav and ul)**
   ```html
   <nav aria-label="Pagination">
     <ul class="pagination">
   ```

2. **Disable current page and unavailable actions**
   ```css
   .page-item.active .page-link { pointer-events: none; }
   ```

3. **Add ARIA labels**
   ```html
   <a aria-label="Next page" href="#">Next</a>
   ```

4. **Use consistent sizing (min 44×44px for touch)**
   ```css
   .page-link { min-width: 44px; height: 44px; }
   ```

5. **Show ellipsis for long lists**
   ```html
   <li class="page-ellipsis">...</li>
   ```

### ❌ Avoid This

1. **Don't make page numbers too small**
   ```css
   /* Too small for touch */
   .page-link { width: 20px; height: 20px; }
   ```

2. **Don't skip keyboard accessibility**
   ```html
   <!-- Missing tabindex for disabled -->
   <a class="disabled">Previous</a>
   ```

3. **Don't show too many page numbers**
   ```html
   <!-- Bad: Shows 1-100 -->
   <!-- Good: Shows 1...48, 49, 50...100 -->
   ```

---

## Related Topics

**Prerequisites:**
- [Buttons](buttons.md)
- [Flexbox](../06-flexbox/flexbox-intro.md)

**Next Steps:**
- [Navigation Bars](navigation-bars.md)
- [Tables](tables.md)

---

## Practice Exercise

Create a pagination component with:
- Previous/Next buttons
- 5 numbered pages
- Active state styling
- Disabled state for Previous (first page)
- Hover effects
- ARIA labels

---

## Navigation

**Previous:** [← Tooltips](tooltips.md)
**Next:** [Responsive Design →](../12-responsive-design/rwd-intro.md)
**Up:** [↑ Back to Components](../README.md#1️⃣1️⃣-components-7-topics)
**Home:** [🏠 Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Components
**Difficulty:** Intermediate
