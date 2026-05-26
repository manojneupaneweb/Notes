# 02 — CSS Selectors

---

## 📌 What are Selectors?

Selectors tell CSS **which HTML elements to style**. They are the part before the curly braces `{}`.

```css
/* selector { declarations } */
h1 { color: blue; }
```

---

## 1. Element Selector

Targets **all** elements of that type.

```css
/* Styles ALL <p> tags on the page */
p {
    font-size: 16px;
    color: #333;
}

/* Styles ALL <h1> tags */
h1 {
    font-size: 36px;
}
```

---

## 2. Class Selector `.`

Targets elements with a specific `class` attribute. Classes can be reused on many elements.

```html
<!-- HTML -->
<p class="highlight">This text is highlighted.</p>
<span class="highlight">This too!</span>
<p>This is NOT highlighted.</p>
```

```css
/* CSS — targets all elements with class="highlight" */
.highlight {
    background-color: yellow;
    font-weight: bold;
}
```

> 💡 **Tip:** Use classes when you want to style **multiple elements** with the same style.

---

## 3. ID Selector `#`

Targets a **single, unique** element with a specific `id`. IDs must be unique on a page.

```html
<!-- HTML -->
<div id="hero">This is the hero section.</div>
```

```css
/* CSS — targets ONLY the element with id="hero" */
#hero {
    background-color: #1a1a2e;
    color: white;
    padding: 80px;
    text-align: center;
}
```

> ⚠️ **Rule:** Each `id` should only be used **once per page**. Use classes for reusable styles.

---

## 4. Universal Selector `*`

Targets **every single element** on the page.

```css
/* Remove margin and padding from everything */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box; /* Very commonly used in resets */
}
```

---

## 5. Grouping Selector `,`

Apply the same styles to multiple selectors at once.

```css
/* Style h1, h2, and h3 the same way */
h1, h2, h3 {
    font-family: 'Georgia', serif;
    color: #2c3e50;
}

/* Style both paragraphs and list items */
p, li {
    line-height: 1.8;
    font-size: 16px;
}
```

---

## 6. Descendant Selector (space)

Targets elements **nested inside** another element.

```html
<!-- HTML -->
<nav>
    <a href="/">Home</a>
    <a href="/about">About</a>
</nav>

<p>
    Visit <a href="#">our website</a>.
</p>
```

```css
/* Targets ONLY <a> tags inside <nav> */
nav a {
    color: white;
    text-decoration: none;
}

/* Does NOT affect the <a> inside <p> */
```

---

## 7. Child Selector `>`

Targets **direct children** only (not deeper nested elements).

```html
<!-- HTML -->
<ul>
    <li>Item 1  <!-- direct child of ul: SELECTED -->
        <ul>
            <li>Nested Item</li>  <!-- NOT direct child: NOT selected -->
        </ul>
    </li>
    <li>Item 2</li>  <!-- direct child of ul: SELECTED -->
</ul>
```

```css
/* Only direct <li> children of <ul> */
ul > li {
    font-weight: bold;
    list-style-type: square;
}
```

---

## 8. Pseudo-Classes (`:`)

Style elements based on their **state** or **position**.

```css
/* Link states */
a:link    { color: blue; }        /* Unvisited link */
a:visited { color: purple; }      /* Visited link */
a:hover   { color: red; }         /* Mouse hovering over it */
a:active  { color: orange; }      /* Being clicked */

/* First and last children */
li:first-child { font-weight: bold; }
li:last-child  { color: gray; }

/* Every Nth child */
li:nth-child(2)    { color: red; }    /* 2nd item */
li:nth-child(even) { background: #f0f0f0; } /* Even items */
li:nth-child(odd)  { background: #fff; }    /* Odd items */

/* Input states */
input:focus    { border-color: blue; outline: none; }  /* When focused */
input:disabled { background: #eee; cursor: not-allowed; }
input:checked  { accent-color: green; }

/* Negation */
p:not(.special) { color: gray; } /* All p EXCEPT .special */
```

---

## 9. Pseudo-Elements (`::`)

Style **specific parts** of an element.

```css
/* First letter of a paragraph */
p::first-letter {
    font-size: 2em;
    font-weight: bold;
    color: #e74c3c;
    float: left;
    margin-right: 5px;
}

/* First line of a paragraph */
p::first-line {
    font-variant: small-caps;
}

/* Add content BEFORE an element */
.warning::before {
    content: "⚠️ ";
}

/* Add content AFTER an element */
.required::after {
    content: " *";
    color: red;
}

/* Selected text styling */
::selection {
    background: #4a90d9;
    color: white;
}
```

---

## 10. Attribute Selector `[]`

Select elements based on their attributes.

```css
/* All inputs */
input[type="text"] { border: 1px solid blue; }
input[type="email"] { border: 1px solid green; }

/* Links that open in new tab */
a[target="_blank"] { color: orange; }

/* Links starting with https */
a[href^="https"] { font-weight: bold; }

/* Links ending in .pdf */
a[href$=".pdf"] { color: red; }
```

---

## 📊 Selector Specificity — Simple Version

Think of specificity like **points**. The rule with the most points wins:

| Selector | Points | Example |
|---------|--------|---------|
| Inline style | 1000 | `style="color:red"` |
| `#id` | 100 | `#header` |
| `.class` | 10 | `.btn` |
| `element` | 1 | `p`, `h1` |

```css
/* Which wins? */
p            { color: blue; }   /* 1 point  — loses */
.text        { color: green; }  /* 10 points — beats element */
#paragraph   { color: red; }    /* 100 points — wins! */
```

> 💡 **Beginner tip:** Stick to **classes** for most styling. They're flexible and easy to understand.

---

## ✅ Key Takeaways

| Selector | Syntax | Use When |
|---------|--------|---------|
| Element | `p` | Style ALL tags of that type |
| Class | `.card` | Style specific components (reusable) |
| ID | `#hero` | Style ONE unique element |
| Grouping | `h1, h2` | Same style, multiple elements |
| Descendant | `nav a` | Target elements inside another |
| `:hover` | `a:hover` | Style on mouse hover |

---

## 🏋️ Practice Tasks

### Task 1 — Selector Practice Page
Create a page with:
- An `<h1>` (element selector → make it dark blue)
- Two `<p>` tags — give them both a class `"text"` (class selector → `color: #555; line-height: 1.6`)
- One special `<p>` with `id="intro"` (ID selector → `font-size: 20px; font-weight: bold`)

Verify each selector works correctly in the browser.

---

### Task 2 — Hover Effects
Create 3 buttons with class `"btn"`. Write CSS so:
- Default state: `background: #4a90d9; color: white; padding: 10px 20px`
- On hover (`:hover`): `background: #2c70b9; cursor: pointer`
- On click (`:active`): `background: #1a5090`

Observe the smooth state changes when you hover and click!

---

### Task 3 — Striped Table
Create an HTML table with at least 5 rows. Use `nth-child` to:
- Make **even rows** have a light gray background (`#f5f5f5`)
- Make **odd rows** have a white background
- Make the **first row** (header) have a blue background with white text

```css
tr:nth-child(even) { background: #f5f5f5; }
tr:nth-child(odd)  { background: white; }
tr:first-child     { background: #4a90d9; color: white; }
```

---

> ➡️ **Next:** `03-colors-and-units.md` — CSS colors and measurement units.
