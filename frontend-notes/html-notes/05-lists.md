# 05 — Lists

---

## 📌 Why Lists?

Lists help organize related items in a structured way. HTML has **three types** of lists, each for a different purpose.

---

## 1️⃣ Unordered List: `<ul>`

Items have no order — they display with bullet points.

```html
<ul>
    <li>HTML</li>
    <li>CSS</li>
    <li>JavaScript</li>
</ul>
```

**Output:**
- HTML
- CSS
- JavaScript

### When to use:
- Navigation menus
- Features/benefits lists
- Any list where order doesn't matter

---

## 2️⃣ Ordered List: `<ol>`

Items are numbered — the order matters.

```html
<ol>
    <li>Open VS Code</li>
    <li>Create a new file</li>
    <li>Type your HTML code</li>
    <li>Save as index.html</li>
    <li>Open in browser</li>
</ol>
```

**Output:**
1. Open VS Code
2. Create a new file
3. Type your HTML code
4. Save as index.html
5. Open in browser

### `type` Attribute for `<ol>`:
```html
<!-- Numbers (default) -->
<ol type="1"> ... </ol>

<!-- Uppercase Letters -->
<ol type="A"> ... </ol>

<!-- Lowercase Letters -->
<ol type="a"> ... </ol>

<!-- Uppercase Roman Numerals -->
<ol type="I"> ... </ol>

<!-- Lowercase Roman Numerals -->
<ol type="i"> ... </ol>

<!-- Start from a custom number -->
<ol start="5"> ... </ol>
```

---

## 3️⃣ Description List: `<dl>`

A list of terms and their definitions. Used for glossaries or key-value pairs.

```html
<dl>
    <dt>HTML</dt>
    <dd>HyperText Markup Language — the structure of web pages.</dd>

    <dt>CSS</dt>
    <dd>Cascading Style Sheets — the styling of web pages.</dd>

    <dt>JavaScript</dt>
    <dd>A programming language that adds interactivity to web pages.</dd>
</dl>
```

**Tags:**
| Tag | Meaning |
|-----|---------|
| `<dl>` | Description List (the container) |
| `<dt>` | Description Term (the word/key) |
| `<dd>` | Description Definition (the explanation, indented) |

---

## 🪆 Nested Lists

You can put lists inside lists to create sub-items.

```html
<ul>
    <li>Frontend Development
        <ul>
            <li>HTML</li>
            <li>CSS</li>
            <li>JavaScript</li>
        </ul>
    </li>
    <li>Backend Development
        <ul>
            <li>Node.js</li>
            <li>PHP</li>
            <li>Python</li>
        </ul>
    </li>
</ul>
```

> 💡 **Tip:** You can also nest `<ol>` inside `<ul>` and vice versa.

---

## 🧪 Full Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>HTML Lists Demo</title>
</head>
<body>

    <h1>Learning Roadmap</h1>

    <!-- Ordered: Step by step -->
    <h2>Step-by-Step Learning Path:</h2>
    <ol>
        <li>Learn HTML basics</li>
        <li>Learn CSS fundamentals</li>
        <li>Learn JavaScript</li>
        <li>Learn a framework (React, Vue, etc.)</li>
    </ol>

    <!-- Unordered: Tools to install -->
    <h2>Tools You Need:</h2>
    <ul>
        <li>VS Code (Code Editor)</li>
        <li>Google Chrome (Browser)</li>
        <li>Git (Version Control)</li>
    </ul>

    <!-- Nested: Technologies by category -->
    <h2>Web Technologies:</h2>
    <ul>
        <li>Frontend
            <ul>
                <li>HTML</li>
                <li>CSS / Tailwind</li>
                <li>JavaScript / React</li>
            </ul>
        </li>
        <li>Backend
            <ul>
                <li>Node.js / PHP / Python</li>
                <li>Databases (MySQL, MongoDB)</li>
            </ul>
        </li>
    </ul>

    <!-- Description: Glossary -->
    <h2>Glossary:</h2>
    <dl>
        <dt>API</dt>
        <dd>Application Programming Interface — a way for two programs to communicate.</dd>

        <dt>DOM</dt>
        <dd>Document Object Model — the live tree structure of an HTML document.</dd>

        <dt>CDN</dt>
        <dd>Content Delivery Network — servers that deliver files quickly from nearby locations.</dd>
    </dl>

</body>
</html>
```

---

## ✅ Key Takeaways

| Tag | Type | Use |
|-----|------|-----|
| `<ul>` | Unordered | Bullet points; order doesn't matter |
| `<ol>` | Ordered | Numbered; order matters |
| `<dl>` | Description | Terms and their definitions |
| `<li>` | List Item | Used inside `<ul>` and `<ol>` |
| `<dt>` | Description Term | The word in a `<dl>` |
| `<dd>` | Description Detail | The explanation in a `<dl>` |

---

> ➡️ **Next:** `06-tables.md` — Displaying tabular data with HTML tables.
