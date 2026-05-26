# 09 — Animations & Transitions

---

## 📌 Why Animations?

Animations and transitions make interfaces feel **alive, responsive, and premium**. They:
- Give **feedback** when users interact (hover, click)
- Guide the **user's attention**
- Make transitions between states feel natural

---

## ⚡ Part 1: CSS Transitions

A **transition** smoothly animates a property change from one state to another.

### Syntax:
```css
element {
    transition: property duration timing-function delay;
}
```

### Basic Example:
```css
.btn {
    background: blue;
    /* When any property changes, animate it over 0.3s */
    transition: background 0.3s ease;
}

.btn:hover {
    background: darkblue; /* This change will be animated! */
}
```

### All Transition Properties:
```css
.box {
    /* Transition a specific property */
    transition: background-color 0.3s ease;

    /* Transition multiple properties */
    transition: background-color 0.3s ease, transform 0.2s ease, box-shadow 0.3s ease;

    /* Transition ALL changed properties */
    transition: all 0.3s ease;

    /* With a delay */
    transition: opacity 0.5s ease 0.2s; /* Starts after 0.2s delay */
}
```

### Timing Functions:
```css
.box {
    transition: all 0.3s linear;     /* Constant speed */
    transition: all 0.3s ease;       /* Slow start, fast middle, slow end (default) */
    transition: all 0.3s ease-in;    /* Slow start, fast end */
    transition: all 0.3s ease-out;   /* Fast start, slow end */
    transition: all 0.3s ease-in-out;/* Slow start and end */
    transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55); /* Custom bounce! */
}
```

### Practical Transition Examples:
```css
/* Smooth hover effect on cards */
.card {
    transform: translateY(0);
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.card:hover {
    transform: translateY(-5px);   /* Float up */
    box-shadow: 0 12px 30px rgba(0,0,0,0.15); /* Deeper shadow */
}

/* Button click effect */
.btn {
    transform: scale(1);
    transition: transform 0.1s ease, background 0.2s ease;
}
.btn:hover  { background: darkblue; }
.btn:active { transform: scale(0.97); } /* Shrink slightly when clicked */

/* Smooth link underline */
.nav-link {
    text-decoration: none;
    position: relative;
}
.nav-link::after {
    content: '';
    position: absolute;
    bottom: -2px;
    left: 0;
    width: 0%;
    height: 2px;
    background: blue;
    transition: width 0.3s ease;
}
.nav-link:hover::after { width: 100%; } /* Underline slides in! */
```

---

## 🔄 Part 2: CSS Transform

`transform` moves, scales, rotates, or skews an element **without affecting the layout**.

```css
/* Translate (move) */
transform: translateX(50px);        /* Move 50px right */
transform: translateY(-20px);       /* Move 20px up */
transform: translate(50px, -20px);  /* Move right AND up */
transform: translateX(50%);         /* Move 50% of its OWN width */

/* Scale (resize) */
transform: scale(1.2);     /* 20% bigger */
transform: scale(0.9);     /* 10% smaller */
transform: scaleX(1.5);    /* Wide only */
transform: scaleY(0.5);    /* Short only */

/* Rotate */
transform: rotate(45deg);  /* 45 degrees clockwise */
transform: rotate(-90deg); /* 90 degrees counter-clockwise */

/* Skew */
transform: skewX(15deg);   /* Slant horizontally */
transform: skewY(10deg);   /* Slant vertically */

/* Combining transforms */
transform: translateY(-5px) scale(1.05) rotate(2deg);

/* 3D transforms */
transform: perspective(500px) rotateY(30deg);
```

---

## 🎬 Part 3: CSS Keyframe Animations

For **more complex animations** with multiple steps, use `@keyframes`.

### Syntax:
```css
/* 1. Define the animation */
@keyframes animation-name {
    from { /* starting state */ }
    to   { /* ending state */ }
}

/* Or with percentage steps */
@keyframes animation-name {
    0%   { /* start */ }
    50%  { /* middle */ }
    100% { /* end */ }
}

/* 2. Apply the animation */
.element {
    animation: animation-name duration timing-function delay iteration-count direction;
}
```

### Animation Properties:
```css
.element {
    animation-name: slideIn;       /* Name of @keyframes */
    animation-duration: 1s;        /* How long one cycle takes */
    animation-timing-function: ease;
    animation-delay: 0.5s;         /* Wait before starting */
    animation-iteration-count: 1;  /* How many times to run (or 'infinite') */
    animation-direction: normal;   /* normal, reverse, alternate, alternate-reverse */
    animation-fill-mode: forwards; /* Keep final state after animation ends */
    animation-play-state: running; /* running or paused */

    /* Shorthand */
    animation: slideIn 1s ease 0.5s 1 normal forwards;
}
```

### Real-World Keyframe Examples:

```css
/* Fade In */
@keyframes fadeIn {
    from { opacity: 0; }
    to   { opacity: 1; }
}
.page-load { animation: fadeIn 0.5s ease forwards; }

/* Slide Up */
@keyframes slideUp {
    from { opacity: 0; transform: translateY(30px); }
    to   { opacity: 1; transform: translateY(0); }
}
.hero-text { animation: slideUp 0.8s ease-out forwards; }

/* Pulse (for notifications/badges) */
@keyframes pulse {
    0%, 100% { transform: scale(1); }
    50%       { transform: scale(1.1); }
}
.badge { animation: pulse 2s ease-in-out infinite; }

/* Spinning Loader */
@keyframes spin {
    from { transform: rotate(0deg); }
    to   { transform: rotate(360deg); }
}
.spinner {
    width: 40px;
    height: 40px;
    border: 4px solid #eee;
    border-top-color: #4a90d9;
    border-radius: 50%;
    animation: spin 1s linear infinite;
}

/* Bounce */
@keyframes bounce {
    0%, 100% { transform: translateY(0); animation-timing-function: ease-in; }
    50%       { transform: translateY(-30px); animation-timing-function: ease-out; }
}
.ball { animation: bounce 1s infinite; }

/* Shake (for form errors) */
@keyframes shake {
    0%, 100% { transform: translateX(0); }
    20%       { transform: translateX(-10px); }
    40%       { transform: translateX(10px); }
    60%       { transform: translateX(-6px); }
    80%       { transform: translateX(6px); }
}
.error { animation: shake 0.5s ease; }

/* Gradient shimmer (skeleton loader) */
@keyframes shimmer {
    0%   { background-position: -200% 0; }
    100% { background-position: 200% 0; }
}
.skeleton {
    background: linear-gradient(90deg, #eee 25%, #f5f5f5 50%, #eee 75%);
    background-size: 200% 100%;
    animation: shimmer 1.5s infinite;
}
```

---

## 🧪 Full Animation Demo

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS Animations Demo</title>
    <style>
        *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: Arial, sans-serif; background: #f9f9f9; padding: 40px; }

        /* Fade-in on load */
        @keyframes fadeUp {
            from { opacity: 0; transform: translateY(20px); }
            to   { opacity: 1; transform: translateY(0); }
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        @keyframes pulse {
            0%, 100% { box-shadow: 0 0 0 0 rgba(74,144,217,0.5); }
            50%       { box-shadow: 0 0 0 12px rgba(74,144,217,0); }
        }

        h1 { animation: fadeUp 0.8s ease forwards; text-align: center; margin-bottom: 40px; }

        /* Spinner */
        .spinner {
            width: 50px; height: 50px;
            border: 5px solid #eee;
            border-top-color: #4a90d9;
            border-radius: 50%;
            animation: spin 0.8s linear infinite;
            margin: 20px auto;
        }

        /* Animated button */
        .btn {
            display: block;
            width: 200px;
            margin: 20px auto;
            padding: 14px 28px;
            background: #4a90d9;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            cursor: pointer;
            transition: transform 0.2s ease, background 0.2s ease;
            animation: pulse 2s ease-in-out infinite;
        }
        .btn:hover  { background: #357abd; transform: translateY(-3px); }
        .btn:active { transform: scale(0.97); }

        /* Hover card */
        .card {
            width: 250px;
            margin: 20px auto;
            padding: 24px;
            background: white;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.08);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            animation: fadeUp 1s ease 0.3s forwards;
            opacity: 0;
        }
        .card:hover {
            transform: translateY(-8px);
            box-shadow: 0 20px 40px rgba(0,0,0,0.12);
        }
    </style>
</head>
<body>

    <h1>CSS Animations</h1>

    <div class="spinner"></div>
    <button class="btn">Hover Me ✨</button>
    <div class="card">
        <h3>Animated Card</h3>
        <p>Hover over me to see the lift effect!</p>
    </div>

</body>
</html>
```

---

## 📊 Quick Reference

| Property | What it does |
|---------|-------------|
| `transition` | Animate property changes on state change |
| `transform` | Move, scale, rotate elements |
| `animation` | Apply keyframe animations |
| `@keyframes` | Define animation steps |

| Transform | Effect |
|-----------|--------|
| `translateX/Y(n)` | Move horizontally/vertically |
| `scale(n)` | Grow/shrink |
| `rotate(deg)` | Spin |
| `skewX/Y(deg)` | Slant |

---

## ✅ Key Takeaways

- **Transitions** = smooth changes between two states (e.g., when you hover over a button).
- **Transform** = move/scale/rotate an element without breaking the page layout.
- **Keyframes** = multi-step, continuous animations (like a loading spinner).

---

## 🏋️ Practice Tasks

### Task 1 — The Growing Button
Create a `<button>` with a background color and some padding.
- Add a transition: `transition: transform 0.3s ease;`
- On hover (`:hover`), add `transform: scale(1.1);`
Watch the button smoothly grow when you mouse over it!

### Task 2 — The Rotating Card
Create a square `.card` div.
- Give it a transition for `transform`.
- On hover, rotate it slightly: `transform: rotate(5deg);`

### Task 3 — The Loading Spinner
Create a circular `<div>` (use `border-radius: 50%` and a border with one colored side).
- Define a `@keyframes` animation named `spin` that goes from `rotate(0deg)` to `rotate(360deg)`.
- Apply it to your circle: `animation: spin 1s linear infinite;`
Congratulations, you just made a loading spinner!

---

> 🎉 **CSS Basics to Advanced Complete!**
> ➡️ **Next:** `10-tailwind-css.md` — Master utility-first CSS with Tailwind!
