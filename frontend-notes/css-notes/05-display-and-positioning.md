# 05 — Display and Positioning

---

## 📌 Part 1: The `display` Property

The `display` property determines **how an element behaves** in the page flow.

---

### `display: block`
- Takes up the **full width** of its parent.
- Starts on a **new line**.
- Respects `width`, `height`, `margin`, `padding`.

```css
div, p, h1, section { display: block; } /* These are block by default */
```

```html
<div>Block 1 — full width</div>
<div>Block 2 — starts on new line</div>
```

---

### `display: inline`
- Only takes up **as much width as its content**.
- Does **NOT** start on a new line — flows with text.
- Does NOT respect `width` or `height`.

```css
span, a, strong, em { display: inline; } /* These are inline by default */
```

```html
<p>This is <span style="color:red">red text</span> within a paragraph.</p>
```

---

### `display: inline-block` ✅ Very Useful
The **best of both worlds**:
- Flows inline (doesn't start a new line).
- Respects `width`, `height`, `margin`, `padding`.

```css
.btn {
    display: inline-block;
    width: 150px;
    padding: 10px 20px;
    background: blue;
    color: white;
    text-align: center;
}
```

---

### `display: none`
Completely **removes the element** from the page. It takes up no space.

```css
.hidden { display: none; }     /* Element is gone */
.visible { display: block; }   /* Show it again */
```

> 💡 **vs `visibility: hidden`:** `visibility: hidden` hides the element but **keeps its space**. `display: none` removes it entirely.

---

### `display: flex` and `display: grid`
These are covered in their own dedicated notes (06 and 07).

---

## 📌 Part 2: The `position` Property

`position` controls how an element is **placed on the page**.

---

### `position: static` (Default)
The element follows normal document flow. `top`, `right`, `bottom`, `left` have NO effect.

```css
div { position: static; } /* This is the default — you rarely need to write this */
```

---

### `position: relative`
Positioned **relative to its own normal position**. Other elements are NOT affected.

```css
.box {
    position: relative;
    top: 20px;    /* Move 20px DOWN from where it normally sits */
    left: 30px;   /* Move 30px RIGHT from where it normally sits */
}
```

```html
<p>Normal text.</p>
<div class="box">I moved down 20px and right 30px from my normal position.</div>
<p>This text is NOT affected by the box's position.</p>
```

> 💡 **Common Use:** Set `position: relative` on a parent to anchor absolute children inside it.

---

### `position: absolute`
Positioned relative to the **nearest positioned ancestor** (any ancestor with position other than `static`).
Removed from the normal document flow (other elements ignore it).

```css
.parent {
    position: relative;  /* The anchor for absolute children */
    width: 400px;
    height: 300px;
    background: #eee;
}

.badge {
    position: absolute;
    top: 10px;    /* 10px from the TOP of .parent */
    right: 10px;  /* 10px from the RIGHT of .parent */
    background: red;
    color: white;
    padding: 5px 10px;
    border-radius: 20px;
}
```

```html
<div class="parent">
    <img src="product.jpg" alt="Product">
    <span class="badge">SALE</span>  <!-- Positioned in top-right corner of parent -->
</div>
```

---

### `position: fixed`
Positioned relative to the **browser viewport**. Stays in place when you scroll.

```css
/* Sticky navigation bar */
.navbar {
    position: fixed;
    top: 0;        /* Stuck to the top */
    left: 0;
    right: 0;
    height: 60px;
    background: white;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    z-index: 1000;  /* Above everything */
}

body {
    padding-top: 60px; /* Prevent content hiding behind navbar */
}
```

---

### `position: sticky`
Acts like `relative` until it hits a scroll threshold, then acts like `fixed`.

```css
/* Section header that sticks while in view */
.section-header {
    position: sticky;
    top: 60px;  /* Stick 60px from top */
    background: white;
    z-index: 10;
    padding: 10px 0;
    border-bottom: 1px solid #eee;
}

/* Sticky table header — very useful! */
th {
    position: sticky;
    top: 0;
    background: #4a90d9;
    color: white;
}
```

---

## 🔢 `z-index` — Stack Order

When elements overlap, `z-index` controls which one appears on top.

```css
.modal    { position: fixed; z-index: 1000; }  /* On top of everything */
.navbar   { position: fixed; z-index: 100; }   /* Above content */
.card     { position: relative; z-index: 10; } /* Normal stacking */
.bg-image { position: absolute; z-index: -1; } /* Behind everything */
```

> ⚠️ `z-index` only works on **positioned elements** (not `position: static`).

---

## 🧪 Practical Example — Product Card with Badge

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Display & Position Demo</title>
    <style>
        *, *::before, *::after { box-sizing: border-box; }
        body { font-family: Arial, sans-serif; padding: 40px; background: #f5f5f5; }

        /* Flexbox row for cards */
        .card-row {
            display: flex;
            gap: 20px;
        }

        /* Card */
        .card {
            position: relative;  /* Anchor for .badge */
            display: inline-block;
            width: 200px;
            background: white;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }

        .card img { width: 100%; display: block; }

        .card-body { padding: 16px; }

        /* Absolute positioned badge */
        .badge {
            position: absolute;
            top: 12px;
            left: 12px;
            background: #e74c3c;
            color: white;
            font-size: 12px;
            font-weight: bold;
            padding: 4px 10px;
            border-radius: 20px;
            text-transform: uppercase;
        }

        /* Fixed button — stays on screen */
        .back-to-top {
            position: fixed;
            bottom: 30px;
            right: 30px;
            background: #4a90d9;
            color: white;
            border: none;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            font-size: 20px;
            cursor: pointer;
            z-index: 999;
        }
    </style>
</head>
<body>

    <div class="card-row">
        <div class="card">
            <img src="https://picsum.photos/200/150" alt="Product">
            <span class="badge">Sale</span>
            <div class="card-body">
                <strong>Product Name</strong>
                <p>$29.99</p>
            </div>
        </div>
        <div class="card">
            <img src="https://picsum.photos/201/150" alt="Product">
            <span class="badge" style="background:#27ae60;">New</span>
            <div class="card-body">
                <strong>Another Product</strong>
                <p>$49.99</p>
            </div>
        </div>
    </div>

    <button class="back-to-top">↑</button>

</body>
</html>
```

---

## 📊 Position Quick Reference

| Value | Relative To | Stays in Flow? | Use Case |
|-------|------------|---------------|---------|
| `static` | Normal flow | ✅ Yes | Default (no positioning) |
| `relative` | Its own position | ✅ Yes | Slight offsets, anchoring children |
| `absolute` | Nearest positioned ancestor | ❌ No | Badges, dropdowns, tooltips |
| `fixed` | Viewport | ❌ No | Navbars, chat buttons, back-to-top |
| `sticky` | Viewport (after scroll) | ✅ Yes | Sticky headers, table headers |

---

> ➡️ **Next:** `06-flexbox.md` — The most powerful layout tool in CSS.
