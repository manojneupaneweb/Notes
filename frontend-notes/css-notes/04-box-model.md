# 04 — The CSS Box Model

---

## 📌 What is the Box Model?

In CSS, **every HTML element is a rectangular box**. The Box Model describes how that box is structured with four layers:

```
┌─────────────────────────────────────┐
│             MARGIN                  │  ← Outermost: space outside the border
│   ┌─────────────────────────────┐   │
│   │           BORDER            │   │  ← The visible edge
│   │   ┌─────────────────────┐   │   │
│   │   │       PADDING       │   │   │  ← Space between border and content
│   │   │   ┌─────────────┐   │   │   │
│   │   │   │   CONTENT   │   │   │   │  ← Your actual text/image
│   │   │   └─────────────┘   │   │   │
│   │   └─────────────────────┘   │   │
│   └─────────────────────────────┘   │
└─────────────────────────────────────┘
```

---

## 📦 The Four Parts Explained

### 1. Content
The actual content (text, image, etc.).

```css
.box {
    width: 300px;   /* Content width */
    height: 150px;  /* Content height */
}
```

### 2. Padding
Space **inside** the border, between content and the edge.

```css
.card {
    padding: 20px;           /* All four sides: 20px */
    padding-top: 10px;       /* Top only */
    padding-right: 20px;     /* Right only */
    padding-bottom: 10px;    /* Bottom only */
    padding-left: 20px;      /* Left only */

    /* Shorthand: Top Right Bottom Left (TRBL — clockwise) */
    padding: 10px 20px 10px 20px;

    /* Shorthand: Vertical Horizontal */
    padding: 10px 20px;

    /* All sides equal */
    padding: 15px;
}
```

### 3. Border
The visible line around the element.

```css
.card {
    border: 2px solid #333;       /* Width Style Color */
    border-radius: 8px;           /* Rounded corners */

    /* Individual sides */
    border-top: 4px solid blue;
    border-right: 1px dashed gray;
    border-bottom: 2px dotted red;
    border-left: none;

    /* Border styles */
    border-style: solid;    /* ──────── */
    border-style: dashed;   /* -------- */
    border-style: dotted;   /* ........ */
    border-style: double;   /* ════════ */
    border-style: groove;   /* 3D groove */
    border-style: none;     /* No border */
}
```

### 4. Margin
Space **outside** the border, pushing other elements away.

```css
.section {
    margin: 20px;            /* All sides */
    margin-top: 40px;        /* Top only */
    margin-bottom: 40px;     /* Bottom only */
    margin-left: auto;       /* Auto (useful for centering!) */
    margin-right: auto;

    /* Center a block element horizontally */
    margin: 0 auto;

    /* Negative margin (pulls elements closer) */
    margin-top: -10px;
}
```

---

## 🔑 The `box-sizing` Property (Critical!)

By default, `width` only applies to the **content area**. Padding and border are added ON TOP.

### Default behavior (`box-sizing: content-box`):
```css
.box {
    width: 200px;
    padding: 20px;
    border: 2px solid;
    /* ACTUAL SIZE = 200 + 20+20 (padding) + 2+2 (border) = 244px */
}
```

This is confusing! When you set `width: 200px`, you don't get a 200px box.

### Fix: Use `box-sizing: border-box` ✅
```css
/* Apply to EVERYTHING — this is a standard reset */
*, *::before, *::after {
    box-sizing: border-box;
}

/* Now width INCLUDES padding and border */
.box {
    width: 200px;
    padding: 20px;
    border: 2px solid;
    /* ACTUAL SIZE = 200px exactly! */
}
```

> ⚠️ **Always include `box-sizing: border-box` in your CSS reset!**

---

## 🧪 Full Box Model Demo

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Box Model Demo</title>
    <style>
        /* Reset */
        *, *::before, *::after { box-sizing: border-box; }
        body { font-family: Arial, sans-serif; padding: 40px; background: #f0f0f0; }

        /* Card Component */
        .card {
            width: 350px;
            background: white;

            /* Content: defined by width/height */

            /* Padding: inside space */
            padding: 24px;

            /* Border */
            border: 2px solid #e0e0e0;
            border-radius: 12px;
            border-top: 4px solid #4a90d9; /* Accent border */

            /* Margin: outside space */
            margin: 20px auto;

            /* Shadow for depth */
            box-shadow: 0 4px 15px rgba(0,0,0,0.08);
        }

        .card h2 {
            margin: 0 0 8px 0;  /* Remove top margin, add bottom */
            color: #2c3e50;
        }

        .card p {
            margin: 0;
            color: #7f8c8d;
            line-height: 1.6;
        }

        .card .btn {
            display: inline-block;
            margin-top: 16px;
            padding: 10px 20px;
            background: #4a90d9;
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <div class="card">
        <h2>CSS Box Model</h2>
        <p>Every element is a box. This card demonstrates how margin, border, padding, and content work together.</p>
        <button class="btn">Learn More</button>
    </div>

</body>
</html>
```

---

## 📊 Box Model Summary

| Layer | Location | Affects |
|-------|----------|---------|
| **Content** | Innermost | Where text/images appear |
| **Padding** | Inside border | Space around content |
| **Border** | Around padding | Visible edge |
| **Margin** | Outside border | Space between elements |

### Shorthand Reference:
```css
/* 4 values: Top Right Bottom Left */
margin: 10px 20px 10px 20px;

/* 2 values: Top/Bottom  Left/Right */
margin: 10px 20px;

/* 1 value: All sides */
margin: 10px;

/* 3 values: Top  Left/Right  Bottom */
margin: 10px 20px 30px;
```

---

## ✅ Key Takeaways

- Every element is a box with: **Content → Padding → Border → Margin**.
- **Padding** = inside space (pushes content inward).
- **Margin** = outside space (pushes other elements away).
- **Border** = the line between them.
- **Always** use `box-sizing: border-box` so width includes padding/borders.

---

## 🏋️ Practice Tasks

### Task 1 — The Button
Create a `<button>` element. Style it using the Box Model:
- Give it `padding` (e.g., `10px` top/bottom, `20px` left/right)
- Give it a `border` (e.g., `2px solid blue`)
- Give it some `margin` to separate it from surrounding text
- Give it a background color

Notice how padding makes the button bigger from the inside, while margin pushes things away on the outside.

### Task 2 — The Card Component
Create a `<div>` with a class of `.card`.
- Set `width: 300px`
- Add a border and some padding inside.
- Add `margin: 0 auto;` — watch how it perfectly centers itself horizontally!

### Task 3 — The box-sizing Fix
Create two `<div>` elements side by side. Give them both `width: 200px`.
- Give the second one `padding: 40px` and a thick `border: 10px solid black`.
- Notice how the second box is much wider than the first one.
- Now add `box-sizing: border-box;` to the second box. Watch it shrink back to exactly 200px wide!

---

> ➡️ **Next:** `05-display-and-positioning.md` — Controlling how elements display and position themselves.
