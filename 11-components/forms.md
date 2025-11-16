---
title: CSS Forms
category: Components
order: 2
youtube_video: https://www.youtube.com/watch?v=OXGznpKZ_sA
---

# CSS Forms

> **Quick Summary:** CSS transforms basic HTML forms into professional, user-friendly interfaces with proper spacing, focus states, validation styling, and accessibility features.

## Table of Contents
- [Introduction](#introduction)
- [Form Layout](#form-layout)
- [Input Styling](#input-styling)
- [Focus States](#focus-states)
- [Validation States](#validation-states)
- [Buttons](#buttons)
- [Checkboxes and Radios](#checkboxes-and-radios)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

Well-styled forms improve user experience, reduce errors, and increase conversions.

---

## Form Layout

### Vertical Layout (Default)

```css
form {
  max-width: 500px;
  margin: 0 auto;
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: 600;
}

input, textarea, select {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 1rem;
}
```

---

### Horizontal Layout

```css
.form-group {
  display: flex;
  align-items: center;
  margin-bottom: 15px;
}

label {
  width: 150px;
  margin-right: 20px;
}

input {
  flex: 1;
}
```

---

## Input Styling

```css
/* Base input */
input[type="text"],
input[type="email"],
input[type="password"],
textarea {
  width: 100%;
  padding: 12px;
  border: 2px solid #e0e0e0;
  border-radius: 6px;
  font-size: 1rem;
  transition: border-color 0.3s, box-shadow 0.3s;
}

/* Placeholder */
input::placeholder {
  color: #999;
  font-style: italic;
}

/* Textarea */
textarea {
  min-height: 120px;
  resize: vertical;
}
```

---

## Focus States

```css
input:focus,
textarea:focus,
select:focus {
  outline: none;
  border-color: #007bff;
  box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.1);
}
```

---

## Validation States

### Valid State

```css
input:valid {
  border-color: #28a745;
}

input:valid:focus {
  box-shadow: 0 0 0 3px rgba(40, 167, 69, 0.1);
}
```

### Invalid State

```css
/* Only show after interaction */
input:not(:placeholder-shown):invalid {
  border-color: #dc3545;
}

input:invalid:focus {
  box-shadow: 0 0 0 3px rgba(220, 53, 69, 0.1);
}
```

### Required Fields

```css
input:required {
  border-left: 4px solid #ffc107;
}

/* Add asterisk to label */
label[for]:has(+ input:required)::after,
input:required + label::before {
  content: " *";
  color: red;
}
```

---

## Buttons

```css
button,
input[type="submit"] {
  padding: 12px 24px;
  background: #007bff;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  cursor: pointer;
  transition: background 0.3s, transform 0.1s;
}

button:hover {
  background: #0056b3;
}

button:active {
  transform: scale(0.98);
}

button:disabled {
  background: #ccc;
  cursor: not-allowed;
  opacity: 0.6;
}
```

---

## Checkboxes and Radios

### Custom Checkbox

```css
/* Hide default */
input[type="checkbox"] {
  appearance: none;
  width: 20px;
  height: 20px;
  border: 2px solid #007bff;
  border-radius: 4px;
  cursor: pointer;
  position: relative;
}

input[type="checkbox"]:checked {
  background: #007bff;
}

input[type="checkbox"]:checked::before {
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: white;
  font-size: 14px;
}
```

### Custom Radio

```css
input[type="radio"] {
  appearance: none;
  width: 20px;
  height: 20px;
  border: 2px solid #007bff;
  border-radius: 50%;
  cursor: pointer;
  position: relative;
}

input[type="radio"]:checked::before {
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 10px;
  height: 10px;
  background: #007bff;
  border-radius: 50%;
}
```

---

## Examples

### Example 1: Contact Form

```css
.contact-form {
  max-width: 600px;
  margin: 0 auto;
  padding: 30px;
  background: white;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 8px;
  font-weight: 600;
  color: #333;
}

input,
textarea {
  width: 100%;
  padding: 12px;
  border: 2px solid #e0e0e0;
  border-radius: 6px;
  font-size: 1rem;
  transition: all 0.3s;
}

input:focus,
textarea:focus {
  border-color: #007bff;
  box-shadow: 0 0 0 3px rgba(0,123,255,0.1);
  outline: none;
}

button {
  width: 100%;
  padding: 14px;
  background: #007bff;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1.1rem;
  cursor: pointer;
  transition: background 0.3s;
}

button:hover {
  background: #0056b3;
}
```

---

### Example 2: Login Form

```css
.login-form {
  max-width: 400px;
  margin: 50px auto;
  padding: 40px;
  background: #f8f9fa;
  border-radius: 12px;
}

.form-group {
  position: relative;
  margin-bottom: 25px;
}

input {
  width: 100%;
  padding: 12px 40px 12px 12px;
  border: 1px solid #ddd;
  border-radius: 8px;
}

/* Icon inside input */
.form-group::after {
  content: "";
  position: absolute;
  right: 15px;
  top: 50%;
  transform: translateY(-50%);
}

.remember {
  display: flex;
  align-items: center;
  gap: 10px;
}
```

---

## Best Practices

### Do This

1. **Provide clear focus states**
   ```css
   input:focus { border-color: #007bff; }
   ```

2. **Use proper input types**
   ```html
   <input type="email"> <!-- Built-in validation -->
   ```

3. **Add placeholder text**
   ```html
   <input placeholder="Enter email...">
   ```

4. **Make accessible**
   ```html
   <label for="email">Email</label>
   <input id="email" type="email">
   ```

### Avoid This

1. **Missing labels**
2. **No focus indicators**
3. **Tiny click targets (<44px)**

---

## Related Topics

**Prerequisites:**
- [Box Model](../03-box-model/box-model-concept.md)

**Next Steps:**
- [Buttons](buttons.md)

---

## Navigation

**Previous:** [← Tables](tables.md)
**Next:** [Buttons →](buttons.md)
**Up:** [↑ Back to Components](../README.md#1️⃣1️⃣-components-7-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 15, 2025
**Category:** Components
**Difficulty:** Intermediate
