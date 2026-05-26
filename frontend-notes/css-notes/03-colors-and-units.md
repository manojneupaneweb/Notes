# 03 — CSS Colors and Units

---

## 🎨 Part 1: Colors

CSS offers multiple ways to define colors. Each method has its use case.

---

### 1. Named Colors
CSS has 140+ predefined color names.

```css
h1 { color: red; }
p  { color: steelblue; }
body { background-color: whitesmoke; }
```

> 💡 Good for quick prototypes, but use HEX/HSL for professional work.

---

### 2. HEX Colors `#RRGGBB`

Hexadecimal colors mix **Red, Green, Blue** values from 00 (none) to FF (max).

```css
/* Format: #RRGGBB */
h1 { color: #ff0000; }     /* Pure red */
h1 { color: #00ff00; }     /* Pure green */
h1 { color: #0000ff; }     /* Pure blue */
h1 { color: #ffffff; }     /* White */
h1 { color: #000000; }     /* Black */
h1 { color: #2c3e50; }     /* Dark blue-gray */

/* Shorthand: #RGB (when both digits are the same) */
h1 { color: #f00; }        /* Same as #ff0000 */
h1 { color: #333; }        /* Same as #333333 (dark gray) */

/* With transparency: #RRGGBBAA */
div { background: #2c3e5080; }  /* 50% transparent */
```

---

### 3. RGB `rgb(r, g, b)`

Mix Red, Green, Blue values from **0 to 255**.

```css
h1 { color: rgb(255, 0, 0); }       /* Red */
h1 { color: rgb(0, 128, 0); }       /* Green */
h1 { color: rgb(44, 62, 80); }      /* Dark blue-gray */
h1 { color: rgb(200, 200, 200); }   /* Light gray */
```

### RGBA `rgba(r, g, b, alpha)` — With Transparency

Alpha is from **0** (transparent) to **1** (opaque).

```css
/* Semi-transparent backgrounds — very useful! */
.overlay { background: rgba(0, 0, 0, 0.5); }   /* 50% black */
.card    { background: rgba(255, 255, 255, 0.9); } /* 90% white */
.tip     { background: rgba(74, 144, 217, 0.2); }  /* Light blue tint */
```

---

### 4. HSL `hsl(hue, saturation%, lightness%)` ✅ Recommended for Design

HSL is the most **intuitive** way to work with colors for designers.

- **Hue (0-360):** The color wheel position (0=red, 120=green, 240=blue)
- **Saturation (0-100%):** How vivid? 0% = gray, 100% = full color
- **Lightness (0-100%):** How bright? 0% = black, 100% = white, 50% = normal

```css
/* Red */
h1 { color: hsl(0, 100%, 50%); }

/* Green */
h1 { color: hsl(120, 100%, 40%); }

/* Blue */
h1 { color: hsl(240, 100%, 60%); }

/* Creating a consistent color palette — just change lightness! */
.primary        { color: hsl(220, 80%, 50%); }  /* Normal */
.primary-light  { color: hsl(220, 80%, 70%); }  /* Lighter */
.primary-dark   { color: hsl(220, 80%, 30%); }  /* Darker */
.primary-faint  { color: hsl(220, 80%, 95%); }  /* Very light for backgrounds */
```

### HSLA — With Transparency
```css
.modal-bg { background: hsla(0, 0%, 0%, 0.5); } /* Semi-transparent black */
```

---

### CSS Variables — Save Colors for Easy Reuse (Optional for Beginners)
```css
/* Define your colors once at the top */
:root {
    --blue:  #4a90d9;
    --dark:  #2c3e50;
    --light: #f9f9f9;
}

/* Use them anywhere */
h1     { color: var(--dark); }
button { background: var(--blue); }
body   { background: var(--light); }
```
> 💡 If you change `--blue` in one place, it updates everywhere!

---

## 📏 Part 2: CSS Units

Units define the **size** of things like width, font-size, spacing.

---

### The Main Units Beginners Need

| Unit | What it means | Example |
|------|--------------|---------|
| `px` | Pixels — fixed size | `font-size: 16px` |
| `%` | Percentage of parent | `width: 50%` |
| `rem` | Based on root font size (usually 16px) | `font-size: 1.5rem` = 24px |
| `vw` | % of screen width | `width: 100vw` |
| `vh` | % of screen height | `height: 100vh` |

```css
/* px — precise, fixed */
.border { border: 2px solid black; }

/* % — flexible, relative to parent */
.container { width: 80%; margin: 0 auto; }

/* rem — great for font sizes (1rem = 16px by default) */
h1 { font-size: 2rem; }    /* 32px */
h2 { font-size: 1.5rem; }  /* 24px */
p  { font-size: 1rem; }    /* 16px */

/* vw/vh — full screen layouts */
.hero { width: 100vw; height: 100vh; }
```

> 💡 **Beginner tip:** Use `px` for borders/spacing. Use `rem` for font sizes. Use `%` or `vw/vh` for widths.

---

## 📊 Units Quick Reference

| Unit | Relative to | Best Use |
|------|------------|---------| 
| `px` | Fixed | Borders, precise spacing |
| `%` | Parent element | Flexible widths |
| `rem` | Root font-size (16px) | Font sizes |
| `vw` | Screen width | Full-width layouts |
| `vh` | Screen height | Full-screen sections |

---

## ✅ Key Takeaways

- Use **named colors** for quick tests, **HEX or HSL** for real projects.
- `rgba(r, g, b, 0.5)` gives you a **semi-transparent** color.
- Use `px` for small fixed sizes, `rem` for fonts, `%` for flexible widths.
- `100vw` / `100vh` = full screen width/height.

---

## 🏋️ Practice Tasks

### Task 1 — Color Palette Card
Create a page with 5 `<div>` boxes side by side (use `display: inline-block`). Give each a different background color using:
- A **named color** (e.g., `tomato`)
- A **HEX** color (e.g., `#4a90d9`)
- An **RGB** color (e.g., `rgb(44, 62, 80)`)
- An **RGBA** color (e.g., `rgba(255, 165, 0, 0.7)`)
- An **HSL** color (e.g., `hsl(140, 60%, 45%)`)

Each box should be `100px × 100px` with the color name written inside.

---

### Task 2 — Font Size Scale
Create an `<h1>` through `<h4>` and a `<p>`. Set font sizes using `rem`:
```css
h1 { font-size: 2.5rem; }  /* 40px */
h2 { font-size: 2rem; }    /* 32px */
h3 { font-size: 1.5rem; }  /* 24px */
h4 { font-size: 1.25rem; } /* 20px */
p  { font-size: 1rem; }    /* 16px */
```
Open the browser and confirm you can see the clear size difference.

---

### Task 3 — Hero Section
Create a full-screen hero section using `vw` and `vh`:
```css
.hero {
    width: 100vw;
    height: 100vh;
    background-color: #2c3e50;
    color: white;
    /* center the text — we'll learn flexbox soon! */
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2rem;
}
```
Put an `<h1>` inside with text like "Welcome to My Page".

---

> ➡️ **Next:** `04-box-model.md` — Understanding the CSS Box Model.
