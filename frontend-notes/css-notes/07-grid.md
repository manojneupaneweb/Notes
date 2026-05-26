# 07 — CSS Grid Layout

---

## 📌 What is CSS Grid?

**CSS Grid** is a two-dimensional layout system — it handles both **rows AND columns** at the same time.

> 💡 **Flexbox vs Grid:**
> - **Flexbox** = one-dimensional (row OR column at a time)
> - **Grid** = two-dimensional (rows AND columns simultaneously)
> - Use Flexbox for components, use Grid for full page layouts.

---

## 🏗️ Setup: Container and Items

```html
<div class="grid-container">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
    <div class="item">5</div>
    <div class="item">6</div>
</div>
```

```css
.grid-container {
    display: grid; /* Activates Grid! */
}
```

---

## 📐 Defining Columns: `grid-template-columns`

```css
.container {
    /* 3 equal columns */
    grid-template-columns: 200px 200px 200px;

    /* Using repeat() shorthand */
    grid-template-columns: repeat(3, 200px);

    /* 3 equal flexible columns (fr = fraction unit) */
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-columns: repeat(3, 1fr);  /* Same thing! */

    /* Sidebar layout: 250px sidebar + flexible main */
    grid-template-columns: 250px 1fr;

    /* 3 unequal columns */
    grid-template-columns: 1fr 2fr 1fr; /* Middle is twice as wide */

    /* 4 columns with minimum and maximum size */
    grid-template-columns: repeat(4, minmax(200px, 1fr));
}
```

---

## 📐 Defining Rows: `grid-template-rows`

```css
.container {
    grid-template-rows: 100px 200px 100px; /* 3 rows with specific heights */
    grid-template-rows: repeat(3, 1fr);    /* 3 equal rows */
    grid-template-rows: auto;              /* Rows size to content (default) */
}
```

---

## 📐 Gap Between Items

```css
.container {
    gap: 20px;             /* Equal gap on both axes */
    row-gap: 20px;         /* Gap between rows only */
    column-gap: 30px;      /* Gap between columns only */
    gap: 20px 30px;        /* Row gap, Column gap */
}
```

---

## 🎨 The `fr` Unit (Fraction)

`fr` divides available space into fractions — it's the most powerful Grid unit.

```css
/* The remaining space after fixed columns is divided */
.container {
    grid-template-columns: 200px 1fr 2fr;
    /* 200px fixed, then remaining space split 1:2 */
}
```

---

## 🔀 Auto-Responsive Grid: `auto-fill` vs `auto-fit`

These automatically determine how many columns fit based on screen size — **no media queries needed!**

```css
.container {
    /* auto-fill: creates columns as needed, may leave empty columns */
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));

    /* auto-fit: stretches columns to fill space, no empty columns */
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}
```

> 💡 Use `auto-fit` with `minmax` for automatically responsive card grids. No media queries!

---

## 🖊️ Placing Items: Span Rows/Columns

Items can span multiple rows and columns.

```css
/* Span 2 columns */
.wide-item {
    grid-column: span 2;
}

/* Span 2 rows */
.tall-item {
    grid-row: span 2;
}

/* Specific placement: start line / end line */
.hero {
    grid-column: 1 / 3;  /* Start at line 1, end at line 3 (spans 2 cols) */
    grid-row: 1 / 2;     /* First row only */
}

/* Using -1 to reach the last line */
.full-width {
    grid-column: 1 / -1; /* Spans ALL columns */
}
```

---

## 🗺️ Grid Template Areas — Visual Layout

This is the most intuitive way to define a full-page layout!

```css
.container {
    display: grid;
    grid-template-columns: 200px 1fr;
    grid-template-rows: 60px 1fr 50px;
    grid-template-areas:
        "header  header"    /* Row 1: header spans both columns */
        "sidebar main  "    /* Row 2: sidebar left, main right */
        "footer  footer";   /* Row 3: footer spans both columns */
    min-height: 100vh;
}

/* Assign elements to areas */
.header  { grid-area: header; background: #2c3e50; color: white; }
.sidebar { grid-area: sidebar; background: #ecf0f1; }
.main    { grid-area: main; padding: 20px; }
.footer  { grid-area: footer; background: #2c3e50; color: white; }
```

---

## 📌 Alignment in Grid

```css
/* Align items within their cell */
.container {
    justify-items: start | center | end | stretch; /* Horizontal */
    align-items: start | center | end | stretch;   /* Vertical */
    place-items: center; /* Shorthand: vertical horizontal */
}

/* Align the ENTIRE grid within the container */
.container {
    justify-content: start | center | end | space-between;
    align-content: start | center | end;
}

/* Align a single item */
.special-item {
    justify-self: center;
    align-self: end;
    place-self: center end; /* Shorthand */
}
```

---

## 🧪 Full Page Layout Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS Grid Layout Demo</title>
    <style>
        *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: Arial, sans-serif; }

        /* Full Page Grid Layout */
        .page {
            display: grid;
            grid-template-columns: 240px 1fr;
            grid-template-rows: 60px 1fr 50px;
            grid-template-areas:
                "header  header"
                "sidebar main  "
                "footer  footer";
            min-height: 100vh;
        }

        header {
            grid-area: header;
            background: #2c3e50;
            color: white;
            display: flex;
            align-items: center;
            padding: 0 30px;
            font-size: 1.4rem;
            font-weight: bold;
        }

        .sidebar {
            grid-area: sidebar;
            background: #f4f4f4;
            padding: 20px;
            border-right: 1px solid #ddd;
        }

        main {
            grid-area: main;
            padding: 30px;
        }

        footer {
            grid-area: footer;
            background: #2c3e50;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.85rem;
        }

        /* Auto-responsive Card Grid inside main */
        .card-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .card {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.08);
        }
    </style>
</head>
<body>

    <div class="page">

        <header>📐 CSS Grid Dashboard</header>

        <aside class="sidebar">
            <h3>Navigation</h3>
            <ul style="margin-top:10px; list-style:none; line-height:2.5;">
                <li>📊 Dashboard</li>
                <li>👤 Users</li>
                <li>📦 Products</li>
                <li>⚙️ Settings</li>
            </ul>
        </aside>

        <main>
            <h1>Dashboard Overview</h1>
            <div class="card-grid">
                <div class="card"><h3>Total Users</h3><p style="font-size:2rem;margin-top:8px">1,240</p></div>
                <div class="card"><h3>Revenue</h3><p style="font-size:2rem;margin-top:8px">$8,400</p></div>
                <div class="card"><h3>Orders</h3><p style="font-size:2rem;margin-top:8px">382</p></div>
                <div class="card"><h3>Products</h3><p style="font-size:2rem;margin-top:8px">56</p></div>
            </div>
        </main>

        <footer>&copy; 2025 CSS Grid Demo. All rights reserved.</footer>

    </div>

</body>
</html>
```

---

## 📊 Grid Quick Reference

| Property | Purpose |
|---------|---------|
| `display: grid` | Enable grid |
| `grid-template-columns` | Define column sizes |
| `grid-template-rows` | Define row sizes |
| `gap` | Space between cells |
| `grid-column: span 2` | Item spans 2 columns |
| `repeat(3, 1fr)` | 3 equal columns |

---

## 🏋️ Practice Tasks

### Task 1 — The 3-Column Layout
Create a `.container` with 6 `.box` divs inside.
Make it a grid with 3 equal columns using `repeat(3, 1fr)` and a `gap: 20px`.
Notice how the items automatically wrap to the next row!

### Task 2 — The Classic Sidebar Layout
Create a layout with a sidebar on the left and main content on the right.
Use `grid-template-columns: 250px 1fr;`.
Watch how the sidebar stays 250px wide, but the main content stretches to fill the rest of the screen.

### Task 3 — Spanning Columns
In your 3-column layout from Task 1, select the first `.box` and add `grid-column: span 3;`.
Watch how the first box now takes up the entire first row!

---

> ➡️ **Next:** `08-responsive-design.md` — Making sites work on all screen sizes.
