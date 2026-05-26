# 06 — CSS Flexbox

---

## 📌 What is Flexbox?

**Flexbox** (Flexible Box Layout) is a CSS layout system designed to arrange items in a **row or column**, distribute space, and align them easily.

> 💡 **Before Flexbox:** Developers used floats, tables, and hacks for layout. Flexbox changed everything!

---

## 🏗️ Setup: Container and Items

Flexbox works on two levels:
1. **Flex Container** — The parent element with `display: flex`
2. **Flex Items** — The direct children of the container

```html
<div class="container">    <!-- Flex Container -->
    <div class="item">A</div>   <!-- Flex Item -->
    <div class="item">B</div>   <!-- Flex Item -->
    <div class="item">C</div>   <!-- Flex Item -->
</div>
```

```css
.container {
    display: flex; /* This turns the container into a flex container */
}
```

---

## 📦 Container Properties

### `flex-direction` — Which direction do items go?

```css
.container {
    /* Row (default) — items go left to right */
    flex-direction: row;

    /* Row reversed — items go right to left */
    flex-direction: row-reverse;

    /* Column — items go top to bottom */
    flex-direction: column;

    /* Column reversed — items go bottom to top */
    flex-direction: column-reverse;
}
```

---

### `justify-content` — Align items along the MAIN axis

The main axis is horizontal when `flex-direction: row`.

```css
.container {
    justify-content: flex-start;    /* [A B C          ] — default */
    justify-content: flex-end;      /* [          A B C ] */
    justify-content: center;        /* [    A B C       ] */
    justify-content: space-between; /* [A     B     C   ] — even gaps, no edge space */
    justify-content: space-around;  /* [ A   B   C  ] — gaps around each item */
    justify-content: space-evenly;  /* [  A  B  C  ] — perfectly equal gaps */
}
```

---

### `align-items` — Align items along the CROSS axis

The cross axis is vertical when `flex-direction: row`.

```css
.container {
    height: 200px; /* Need height to see vertical alignment */

    align-items: stretch;      /* Items stretch to full height (default) */
    align-items: flex-start;   /* Align to top */
    align-items: flex-end;     /* Align to bottom */
    align-items: center;       /* Align to middle ← Most commonly used! */
    align-items: baseline;     /* Align by text baseline */
}
```

---

### `flex-wrap` — What happens when items don't fit?

```css
.container {
    flex-wrap: nowrap;   /* Default — items shrink to fit on one line */
    flex-wrap: wrap;     /* Items wrap onto multiple lines */
    flex-wrap: wrap-reverse; /* Wrap in reverse order */
}
```

---

### `gap` — Space between items

```css
.container {
    gap: 20px;            /* Equal gap on both axes */
    gap: 10px 20px;       /* Row gap, Column gap */
    row-gap: 10px;
    column-gap: 20px;
}
```

---

### `align-content` — Align wrapped rows

Only works when `flex-wrap: wrap` and there are multiple rows.

```css
.container {
    flex-wrap: wrap;
    align-content: flex-start;    /* Rows at top */
    align-content: flex-end;      /* Rows at bottom */
    align-content: center;        /* Rows in middle */
    align-content: space-between; /* Rows spread out */
    align-content: space-around;  /* Space around rows */
}
```

---

## 📦 Item Properties

### `flex-grow` — How much should an item grow?

```css
/* By default, flex-grow: 0 (don't grow) */

/* Take all available space */
.item { flex-grow: 1; }

/* This item grows TWICE as fast as others */
.item.big { flex-grow: 2; }

/* Sidebar layout: 1:3 ratio */
.sidebar { flex-grow: 1; }
.main    { flex-grow: 3; }
```

---

### `flex-shrink` — How much can an item shrink?

```css
/* Default: flex-shrink: 1 (can shrink) */

/* This item won't shrink */
.logo { flex-shrink: 0; }
```

---

### `flex-basis` — Starting size before growing/shrinking

```css
/* Start at 200px, then grow/shrink as needed */
.item { flex-basis: 200px; }

/* Start at 33.33% width */
.item { flex-basis: 33.33%; }
```

---

### `flex` Shorthand — grow shrink basis

```css
/* flex: grow shrink basis */
.item { flex: 1 1 0; }    /* Can grow and shrink, starts at 0 */
.item { flex: 1; }        /* Shorthand for: 1 1 0 — most common! */
.item { flex: 0 0 200px;} /* Fixed at 200px, won't grow or shrink */
```

---

### `align-self` — Override alignment for one item

```css
.container { align-items: flex-start; }

.item.special {
    align-self: flex-end; /* This item aligns to bottom while others are at top */
}
```

---

### `order` — Change display order without changing HTML

```css
/* Default order is 0 */
.item-a { order: 1; }  /* Appears LAST */
.item-b { order: -1; } /* Appears FIRST */
```

---

## 🧪 Real-World Examples

### Centered Content (The Most Common Use!)
```css
.hero {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}
```

### Navigation Bar
```css
.navbar {
    display: flex;
    justify-content: space-between; /* Logo left, links right */
    align-items: center;
    padding: 0 30px;
    height: 60px;
}
```

### Card Grid with Equal-Width Cards
```css
.card-container {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}
.card {
    flex: 1 1 300px; /* Grow, shrink, min-width of 300px */
    /* Cards fill the row, wrapping when they can't fit */
}
```

### Sidebar Layout
```css
.page {
    display: flex;
}
.sidebar { flex: 0 0 250px; } /* Fixed 250px, doesn't grow */
.main    { flex: 1; }         /* Takes all remaining space */
```

---

## 🧪 Full Flexbox Demo

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Flexbox Demo</title>
    <style>
        *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: Arial, sans-serif; }

        /* Navbar */
        .navbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #2c3e50;
            color: white;
            padding: 0 30px;
            height: 60px;
        }
        .nav-links { display: flex; gap: 20px; list-style: none; }
        .nav-links a { color: white; text-decoration: none; }

        /* Hero */
        .hero {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            text-align: center;
            height: 300px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            gap: 16px;
        }

        /* Cards */
        .cards {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            padding: 40px;
            justify-content: center;
        }
        .card {
            flex: 1 1 200px;
            max-width: 280px;
            background: white;
            border-radius: 12px;
            padding: 24px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.08);
        }
    </style>
</head>
<body>

    <!-- Flexbox Navbar -->
    <nav class="navbar">
        <strong>FlexDemo</strong>
        <ul class="nav-links">
            <li><a href="#">Home</a></li>
            <li><a href="#">About</a></li>
            <li><a href="#">Contact</a></li>
        </ul>
    </nav>

    <!-- Flexbox Hero: centered content -->
    <div class="hero">
        <h1>Master CSS Flexbox</h1>
        <p>Build any layout with ease.</p>
        <button>Get Started</button>
    </div>

    <!-- Flexbox Card Grid -->
    <div class="cards">
        <div class="card"><h3>🚀 Fast</h3><p>Flexbox makes layout effortless.</p></div>
        <div class="card"><h3>🎨 Flexible</h3><p>Works for any screen size.</p></div>
        <div class="card"><h3>💪 Powerful</h3><p>Complex layouts made simple.</p></div>
    </div>

</body>
</html>
```

---

## 📊 Flexbox Quick Reference

- **Container:** `display: flex;`
- **Direction:** `flex-direction: row` (horizontal) or `column` (vertical)
- **Align Main Axis:** `justify-content`
- **Align Cross Axis:** `align-items`
- **Wrapping:** `flex-wrap: wrap`
- **Spacing:** `gap`

---

## 🏋️ Practice Tasks

### Task 1 — The Perfect Center
Create a `.container` `<div>` with a fixed height (e.g., `400px`) and a border. Inside it, place a single `.box` `<div>`.
Use Flexbox on the container to perfectly center the box both vertically and horizontally.
*(Hint: You only need 3 lines of CSS on the container!)*

### Task 2 — The Navigation Bar
Create a `<nav>` element containing a logo `<h1>` and a `<ul>` with 3 links.
Use Flexbox on the `<nav>` to push the logo to the far left, and the links to the far right. Use `align-items` to make sure they are vertically centered.
*(Hint: Use `justify-content: space-between`)*

### Task 3 — The Responsive Card Grid
Create a `.grid` container with 5 `.card` elements inside.
- Set the container to `display: flex` and enable wrapping.
- Add a `gap: 20px` to space them out.
- Give each card a `flex-basis: 200px` and `flex-grow: 1`.
- Resize your browser window and watch the cards automatically rearrange and resize themselves!

---

> ➡️ **Next:** `07-grid.md` — CSS Grid Layout for two-dimensional designs.
