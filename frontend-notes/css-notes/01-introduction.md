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

The word "Cascading" means styles are applied in a specific order. When styles conflict, the browser follows these rules:

### 1. Specificity (Most Important)
More specific selectors beat less specific ones:
```
Inline style > ID (#id) > Class (.class) > Element (h1, p)
```

### 2. Order
Later rules override earlier ones (when specificity is equal):
```css
p { color: red; }   /* This is overridden */
p { color: blue; }  /* This wins */
```

### 3. `!important` (Use Sparingly!)
Forces a rule to take priority. Avoid using this.
```css
p { color: red !important; } /* This beats everything */
```

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
- Always use **external CSS** for real projects.
- CSS rule: `selector { property: value; }`
- Styles cascade — more specific rules and later rules win conflicts.

---

> ➡️ **Next:** `02-selectors.md` — How to target specific elements.
