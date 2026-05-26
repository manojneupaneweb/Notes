# 01 — Introduction to CSS

---

## 📌 What is CSS?

**CSS** stands for **Cascading Style Sheets**.

- CSS is the **design/styling language** of the web.
- It controls the **look and feel** of HTML elements: colors, fonts, spacing, layout, animations.
- Without CSS, websites would look like plain black-and-white text documents.

> 💡 **Analogy:** If HTML is the skeleton of a house, CSS is the paint, wallpaper, furniture, and decoration.

---

## 🔗 How CSS Works with HTML

CSS **selects** HTML elements and applies **rules** to them.

```css
/* selector { property: value; } */

h1 {
    color: blue;
    font-size: 36px;
}
```

This says: "Find all `<h1>` elements and make them blue, 36px."

---

## 📦 Three Types of CSS

### 1. Inline CSS
Written directly inside the HTML tag using the `style` attribute.

```html
<p style="color: red; font-size: 20px;">This is red text.</p>
```

✅ Quick for testing  
❌ Hard to maintain — not recommended for real projects

---

### 2. Internal CSS
Written inside a `<style>` tag in the `<head>` of the HTML file.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Internal CSS</title>

    <!-- Internal CSS lives here -->
    <style>
        body {
            background-color: #f0f0f0;
            font-family: Arial, sans-serif;
        }
        h1 {
            color: #333;
        }
        p {
            color: #666;
        }
    </style>

</head>
<body>
    <h1>Hello!</h1>
    <p>This text is styled with internal CSS.</p>
</body>
</html>
```

✅ Good for single-page demos and small projects  
❌ Doesn't scale well for large projects

---

### 3. External CSS ✅ (Best Practice)
CSS written in a **separate file** (`.css`) and linked to the HTML file.

**style.css:**
```css
/* This is an external stylesheet */

body {
    background-color: #f9f9f9;
    font-family: 'Arial', sans-serif;
    margin: 0;
    padding: 0;
}

h1 {
    color: #2c3e50;
    text-align: center;
}

p {
    color: #7f8c8d;
    line-height: 1.6;
}
```

**index.html:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>External CSS</title>

    <!-- Link to external CSS file -->
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Hello!</h1>
    <p>This is styled by an external CSS file.</p>
</body>
</html>
```

✅ Best for real projects  
✅ One CSS file can style many HTML pages  
✅ Easy to maintain and update  

---

## ⚡ CSS Cascade: Which Style Wins?

When two CSS rules target the same element, CSS has a simple pecking order:

```
More specific = Wins!

Inline style  >  #id  >  .class  >  element tag
   (1000)        (100)    (10)          (1)
```

**Simple example:**
```css
p { color: blue; }       /* loses */
.text { color: green; }  /* wins over element */
#para { color: red; }    /* wins over class */
```

> 💡 **Beginner tip:** When your style isn't working, check if something more specific is overriding it. Open **DevTools → Inspect** to see which rule wins.

**Rule of thumb for beginners:**
- Use **element selectors** for general styles (all `p`, all `h1`)
- Use **class selectors** for specific components (`.btn`, `.card`)
- Avoid `!important` — it causes confusion later

---

## 📊 Summary Table

| Type | Where Written | Best For |
|------|--------------|---------| 
| Inline | Inside the HTML tag | Quick testing only |
| Internal | `<style>` in `<head>` | Small, single pages |
| External | Separate `.css` file | All real projects ✅ |

---

## ✅ Key Takeaways

- CSS = style and design of HTML pages.
- A CSS rule = `selector { property: value; }`
- Always use **external CSS** for real projects (separate `.css` file).
- When styles conflict, the more **specific** rule wins.

---

## 🏋️ Practice Tasks

### Task 1 — Your First Stylesheet
1. Create `index.html` with an `<h1>`, a `<p>`, and a `<button>`
2. Create `style.css` and link it with `<link rel="stylesheet" href="style.css">`
3. In `style.css`, give the `<h1>` a color, the `<p>` a font-size, and the `<button>` a background color
4. Open in browser — confirm styles are working ✅

---

### Task 2 — Three Types of CSS
On the same page, apply the same style (`color: red`) using all 3 methods:
- **Inline:** directly on an `<h2>` tag
- **Internal:** inside a `<style>` tag in `<head>`
- **External:** in your `style.css` file

Then **remove inline and internal CSS** — use external only from now on!

---

### Task 3 — See the Cascade in Action
Write these rules in order and observe which color wins on a `<p>` tag:
```css
p { color: blue; }
p { color: red; }   /* Does this override blue? */
```
Then add a class `.special` with `color: green` to the `<p>`. Does green win?
Write your conclusion as a comment in the CSS file.

---

> ➡️ **Next:** `02-selectors.md` — How to target specific elements.
