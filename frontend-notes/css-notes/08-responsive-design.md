# 08 — Responsive Design

---

## 📌 What is Responsive Design?

A **responsive website** looks and works great on **any screen size** — from a small phone to a large desktop monitor.

> 💡 **Why it matters:** Over 60% of web traffic is from mobile devices. Your site MUST work on phones!

---

## 📱 Mobile-First Design (Best Practice)

**Mobile-first** means you write CSS for the **smallest screen first**, then add styles for larger screens.

### Why Mobile-First?
1. Forces you to prioritize content (phones have limited space).
2. Easier to add complexity than to remove it.
3. Better performance — mobile devices download less CSS.

```css
/* Mobile-first approach */

/* Base styles — for all screens (including mobile) */
.card {
    width: 100%;
    padding: 16px;
}

/* Tablet and up — add more styling */
@media (min-width: 768px) {
    .card { width: 50%; }
}

/* Desktop and up — add even more */
@media (min-width: 1024px) {
    .card { width: 33.33%; }
}
```

---

## 📐 Media Queries

Media queries apply CSS rules **only** when certain conditions are met (like screen width).

### Basic Syntax:
```css
@media (condition) {
    /* CSS rules applied when condition is true */
}
```

### Common Breakpoints:

```css
/* Mobile (default — no media query needed) */
/* < 640px */

/* Small tablets and up */
@media (min-width: 640px) {
    /* sm: small phones in landscape, small tablets */
}

/* Tablets and up */
@media (min-width: 768px) {
    /* md: iPads, tablets */
}

/* Laptops and up */
@media (min-width: 1024px) {
    /* lg: small laptops */
}

/* Desktops and up */
@media (min-width: 1280px) {
    /* xl: standard desktops */
}

/* Large desktops */
@media (min-width: 1536px) {
    /* 2xl: wide screens */
}
```

---

### Media Query Features:

```css
/* Width conditions */
@media (min-width: 768px) { ... }     /* Screen >= 768px */
@media (max-width: 767px) { ... }     /* Screen <= 767px */
@media (min-width: 768px) and (max-width: 1023px) { ... } /* Between */

/* Device orientation */
@media (orientation: portrait) { ... }    /* Phone upright */
@media (orientation: landscape) { ... }   /* Phone sideways */

/* Dark mode support */
@media (prefers-color-scheme: dark) {
    body { background: #1a1a2e; color: #eee; }
}

/* Reduced motion (accessibility!) */
@media (prefers-reduced-motion: reduce) {
    * { animation: none !important; transition: none !important; }
}

/* Hover capability (touch devices can't hover) */
@media (hover: hover) {
    .btn:hover { background: darkblue; }
}

/* High-resolution screens (Retina) */
@media (-webkit-min-device-pixel-ratio: 2) {
    /* Use higher-res images for Retina displays */
}
```

---

## 📏 Fluid Layouts: Flexible Widths

Instead of fixed pixels, use relative units to create naturally responsive layouts.

```css
/* Fixed (not responsive) ❌ */
.container { width: 960px; }

/* Fluid (responsive ✅) */
.container {
    width: 90%;           /* 90% of viewport */
    max-width: 1200px;    /* But never wider than 1200px */
    margin: 0 auto;       /* Center it */
}

/* Fluid images */
img {
    max-width: 100%;      /* Never wider than its container */
    height: auto;         /* Maintain aspect ratio */
    display: block;
}
```

---

## 🔤 Responsive Typography

```css
/* Approach 1: Fluid font sizes with clamp() */
h1 {
    /* clamp(minimum, preferred, maximum) */
    font-size: clamp(1.5rem, 5vw, 3rem);
    /* Minimum: 1.5rem, scales with viewport, max: 3rem */
}

p {
    font-size: clamp(1rem, 2.5vw, 1.2rem);
}

/* Approach 2: Viewport units */
h1 { font-size: 5vw; } /* 5% of viewport width */

/* Approach 3: Media queries */
h1 { font-size: 1.8rem; }
@media (min-width: 768px) { h1 { font-size: 2.5rem; } }
@media (min-width: 1024px) { h1 { font-size: 3.5rem; } }
```

---

## 📱 Common Responsive Patterns

### 1. Column to Row
```css
/* Mobile: Stack vertically */
.container {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

/* Desktop: Side by side */
@media (min-width: 768px) {
    .container { flex-direction: row; }
}
```

### 2. Hide on Mobile, Show on Desktop
```css
.desktop-only { display: none; }

@media (min-width: 1024px) {
    .desktop-only { display: block; }
}
```

### 3. Hamburger Menu (mobile) to Full Nav (desktop)
```css
/* Mobile: hide nav links, show hamburger */
.nav-links { display: none; }
.hamburger { display: block; }

/* Desktop: show nav links, hide hamburger */
@media (min-width: 768px) {
    .nav-links { display: flex; gap: 20px; }
    .hamburger { display: none; }
}
```

### 4. Responsive Card Grid
```css
.grid {
    display: grid;
    /* Automatically responsive — no media queries! */
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 24px;
}
```

---

## 🧪 Full Responsive Page Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <!-- THIS IS ESSENTIAL FOR RESPONSIVE DESIGN -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Responsive Design Demo</title>
    <style>
        *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

        body { font-family: Arial, sans-serif; color: #333; }

        /* Container */
        .container { width: 90%; max-width: 1100px; margin: 0 auto; }

        /* Navbar */
        .navbar {
            background: #2c3e50;
            padding: 15px 0;
        }
        .navbar .container {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .logo { color: white; font-size: 1.4rem; font-weight: bold; }
        .nav-links { display: none; gap: 20px; list-style: none; }
        .nav-links a { color: rgba(255,255,255,0.8); text-decoration: none; }

        /* Show nav links on tablet+ */
        @media (min-width: 768px) {
            .nav-links { display: flex; }
        }

        /* Hero */
        .hero {
            padding: 60px 0;
            text-align: center;
        }
        .hero h1 {
            font-size: clamp(1.8rem, 5vw, 3.5rem);
            color: #2c3e50;
            margin-bottom: 16px;
        }
        .hero p {
            font-size: clamp(1rem, 2.5vw, 1.2rem);
            color: #7f8c8d;
            max-width: 60ch;
            margin: 0 auto 24px;
        }
        .btn {
            padding: 12px 28px;
            background: #4a90d9;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            cursor: pointer;
        }

        /* Card Grid */
        .cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 24px;
            padding: 60px 0;
        }
        .card {
            background: white;
            padding: 24px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.08);
        }
        .card h3 { margin-bottom: 8px; color: #2c3e50; }
        .card p { color: #7f8c8d; line-height: 1.6; }

        /* Dark mode */
        @media (prefers-color-scheme: dark) {
            body { background: #1a1a2e; color: #eee; }
            .card { background: #2d2d44; }
            .card h3 { color: #eee; }
        }
    </style>
</head>
<body>

    <nav class="navbar">
        <div class="container">
            <div class="logo">ResponsiveDemo</div>
            <ul class="nav-links">
                <li><a href="#">Home</a></li>
                <li><a href="#">Features</a></li>
                <li><a href="#">Contact</a></li>
            </ul>
        </div>
    </nav>

    <section class="hero">
        <div class="container">
            <h1>Responsive Web Design</h1>
            <p>Build websites that look great on every device, from mobile phones to large desktop monitors.</p>
            <button class="btn">Get Started</button>
        </div>
    </section>

    <section class="container">
        <div class="cards">
            <div class="card"><h3>📱 Mobile First</h3><p>Design for the smallest screen first, then enhance for larger screens.</p></div>
            <div class="card"><h3>📐 Fluid Grids</h3><p>Use flexible units and CSS Grid to create layouts that adapt automatically.</p></div>
            <div class="card"><h3>🖼️ Flexible Images</h3><p>Set max-width: 100% on images so they never overflow their container.</p></div>
        </div>
    </section>

</body>
</html>
```

---

## ✅ Key Takeaways

- Always add the `<meta name="viewport">` tag — without it, responsive CSS won't work on mobile!
- Write **mobile-first** CSS, then use `min-width` media queries for larger screens.
- Use **relative units** (`%`, `rem`, `vw`) instead of fixed `px` for flexible layouts.
- Use `clamp()` for fluid typography that scales with the viewport.
- Use `repeat(auto-fit, minmax())` for automatically responsive grids.
- Support **dark mode** and **reduced motion** with media queries for better accessibility.

---

> ➡️ **Next:** `09-animations.md` — CSS transitions, animations, and transforms.
