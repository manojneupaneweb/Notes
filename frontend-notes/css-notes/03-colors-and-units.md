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

### CSS Custom Properties (Variables) — Best Practice
```css
/* Define your color palette once */
:root {
    --primary: hsl(220, 80%, 55%);
    --primary-dark: hsl(220, 80%, 40%);
    --text: hsl(0, 0%, 15%);
    --bg: hsl(0, 0%, 98%);
    --danger: hsl(0, 75%, 55%);
    --success: hsl(140, 60%, 45%);
}

/* Use them everywhere */
button { background: var(--primary); }
button:hover { background: var(--primary-dark); }
body { color: var(--text); background: var(--bg); }
```

---

## 📏 Part 2: CSS Units

Units define the **size** of properties like `font-size`, `width`, `margin`, `padding`.

---

### Absolute Units

Fixed sizes — don't change based on screen or parent.

| Unit | Full Name | Example | Use Case |
|------|-----------|---------|----------|
| `px` | Pixels | `font-size: 16px` | Most common — precise sizing |
| `pt` | Points | `font-size: 12pt` | Print stylesheets |
| `cm` / `mm` | Centimeters / Millimeters | `width: 10cm` | Print layouts only |

```css
/* px is the most common absolute unit */
h1 { font-size: 48px; }
.btn { padding: 12px 24px; border-radius: 6px; }
```

---

### Relative Units ✅ (Preferred for Responsive Design)

Sizes that change relative to something else.

#### `%` — Percentage
Relative to the **parent element's** size.

```css
.container { width: 80%; }        /* 80% of parent width */
.sidebar   { width: 25%; }        /* 25% of parent */
.img       { max-width: 100%; }   /* Never wider than its container */
```

#### `em` — Relative to parent font-size
`1em` = the current element's font-size. Compounding can be tricky!

```css
body { font-size: 16px; }

/* 2em = 2 × 16px = 32px */
h1 { font-size: 2em; }

/* Padding of 1em on h1 = 1 × 32px = 32px (uses h1's font-size!) */
h1 { padding: 1em; }
```

> ⚠️ **Warning:** `em` compounds! A nested element with `font-size: 1.2em` inside another `font-size: 1.2em` = `1.2 × 1.2 = 1.44em` of the root.

#### `rem` — Relative to root font-size ✅ (Recommended)
`1rem` = the `<html>` element's font-size (usually 16px). Does NOT compound.

```css
html { font-size: 16px; } /* root = 16px */

h1 { font-size: 3rem; }   /* 3 × 16px = 48px */
h2 { font-size: 2rem; }   /* 2 × 16px = 32px */
p  { font-size: 1rem; }   /* 1 × 16px = 16px */

/* Pro tip: Set html to 62.5% to make 1rem = 10px */
html { font-size: 62.5%; }
h1   { font-size: 4.8rem; }  /* 4.8 × 10px = 48px — easy math! */
```

#### `vw` / `vh` — Viewport Width / Height
`1vw` = 1% of the browser window width. `1vh` = 1% of the browser window height.

```css
/* Full-screen hero section */
.hero {
    width: 100vw;
    height: 100vh;
    background: #1a1a2e;
}

/* Text that scales with screen width */
h1 { font-size: 5vw; }

/* Viewport minimum/maximum */
.box { width: 50vmin; } /* 50% of whichever is smaller: vw or vh */
```

#### `ch` — Width of the "0" character
Useful for text content width.

```css
/* Readable text — limit line length to ~65 characters */
p { max-width: 65ch; }
```

---

## 📊 Units Quick Reference

| Unit | Relative to | Best Use |
|------|------------|---------|
| `px` | Fixed | Precise spacing, borders |
| `%` | Parent element | Flexible widths and heights |
| `em` | Current font-size | Padding/margin relative to font |
| `rem` | Root font-size | Font sizes, consistent spacing |
| `vw` | Viewport width | Full-width layouts |
| `vh` | Viewport height | Full-screen sections |
| `ch` | Character width | Text container widths |

---

## ✅ Key Takeaways

- Use **HEX** for fixed brand colors.
- Use **HSL** when designing custom color palettes — easiest to reason about.
- Use **rgba/hsla** for transparency effects.
- Use **CSS variables** (`--color`) for a maintainable color system.
- Use **rem** for font sizes and most spacing.
- Use **%** and **vw/vh** for responsive layouts.
- Avoid hardcoding `px` for font sizes — use `rem` for accessibility.

---

> ➡️ **Next:** `04-box-model.md` — Understanding the CSS Box Model.
