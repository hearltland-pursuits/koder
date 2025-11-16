---
title: CSS Tables
category: Components
order: 1
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Tables

> **Quick Summary:** CSS transforms basic HTML tables into professional, readable data displays with borders, spacing, zebra striping, hover effects, and responsive layouts.

## Table of Contents
- [Introduction](#introduction)
- [Table Structure](#table-structure)
- [Basic Table Styling](#basic-table-styling)
- [Table Borders](#table-borders)
- [Table Spacing](#table-spacing)
- [Zebra Striping](#zebra-striping)
- [Hover Effects](#hover-effects)
- [Responsive Tables](#responsive-tables)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

HTML tables display tabular data. CSS makes them readable, accessible, and visually appealing.

---

## Table Structure

```html
<table>
  <thead>
    <tr>
      <th>Header 1</th>
      <th>Header 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Data 1</td>
      <td>Data 2</td>
    </tr>
  </tbody>
</table>
```

---

## Basic Table Styling

```css
table {
  width: 100%;
  border-collapse: collapse; /* Removes double borders */
  font-family: Arial, sans-serif;
}

th, td {
  padding: 12px 15px;
  text-align: left;
}

th {
  background: #007bff;
  color: white;
  font-weight: bold;
}
```

---

## Table Borders

### Border-Collapse

```css
/* Collapsed borders (cleaner) */
table {
  border-collapse: collapse;
}

/* Separate borders (spaced) */
table {
  border-collapse: separate;
  border-spacing: 10px;
}
```

### Border Styles

```css
/* All-around borders */
table, th, td {
  border: 1px solid #ddd;
}

/* Bottom borders only */
th, td {
  border-bottom: 1px solid #ddd;
}

/* No borders */
table {
  border: none;
}
```

---

## Table Spacing

```css
/* Cell padding */
th, td {
  padding: 12px 15px;
}

/* Row height */
tr {
  height: 50px;
}

/* Column width */
th:first-child,
td:first-child {
  width: 30%;
}
```

---

## Zebra Striping

```css
/* Alternate row colors */
tbody tr:nth-child(even) {
  background: #f9f9f9;
}

tbody tr:nth-child(odd) {
  background: white;
}
```

---

## Hover Effects

```css
tbody tr:hover {
  background: #e3f2fd;
  cursor: pointer;
}
```

---

## Responsive Tables

### Horizontal Scroll

```css
.table-container {
  overflow-x: auto;
}

table {
  min-width: 600px;
}
```

### Stacked Mobile Layout

```css
@media (max-width: 768px) {
  table, thead, tbody, th, td, tr {
    display: block;
  }

  thead tr {
    position: absolute;
    top: -9999px;
    left: -9999px;
  }

  tr {
    margin-bottom: 15px;
    border: 1px solid #ddd;
  }

  td {
    border: none;
    position: relative;
    padding-left: 50%;
  }

  td::before {
    content: attr(data-label);
    position: absolute;
    left: 10px;
    font-weight: bold;
  }
}
```

**HTML:**
```html
<td data-label="Name">John Doe</td>
```

---

## Examples

### Example 1: Modern Data Table

```css
table {
  width: 100%;
  border-collapse: collapse;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

thead {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
}

th {
  padding: 15px;
  text-align: left;
  font-weight: 600;
}

tbody tr {
  border-bottom: 1px solid #eee;
  transition: background 0.3s;
}

tbody tr:hover {
  background: #f8f9fa;
}

td {
  padding: 12px 15px;
}
```

---

### Example 2: Pricing Table

```css
.pricing-table {
  display: flex;
  gap: 20px;
}

.price-column {
  flex: 1;
  border: 2px solid #ddd;
  border-radius: 8px;
  text-align: center;
  padding: 30px;
}

.price-column.featured {
  border-color: #007bff;
  transform: scale(1.05);
  box-shadow: 0 8px 16px rgba(0,123,255,0.3);
}

.price {
  font-size: 3rem;
  font-weight: bold;
  color: #007bff;
}
```

---

## Best Practices

### Do This

1. **Use border-collapse**
   ```css
   table { border-collapse: collapse; }
   ```

2. **Add hover states**
   ```css
   tr:hover { background: #f0f0f0; }
   ```

3. **Make responsive**
   ```css
   .table-container { overflow-x: auto; }
   ```

### Avoid This

1. **Fixed widths on mobile**
2. **Missing thead/tbody**
3. **Inline styles**

---

## Related Topics

**Next Steps:**
- [Forms](forms.md)
- [Buttons](buttons.md)

---

## Navigation

**Previous:** [← Opacity](../09-visual-effects/opacity.md)
**Next:** [Forms →](forms.md)
**Up:** [↑ Back to Components](../README.md#1️⃣1️⃣-components-7-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Components
**Difficulty:** Beginner
