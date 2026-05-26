# 01 — Introduction to JavaScript

---

## 📌 What is JavaScript?

**JavaScript** (JS) is the **programming language of the web**.

- It makes web pages **interactive and dynamic**.
- While HTML gives structure and CSS gives style, **JavaScript gives behavior**.
- JavaScript can update content, respond to clicks, validate forms, fetch data, animate elements, and much more.
- It runs directly in the **browser** (no installation needed).

> 💡 **Analogy:** If HTML is the skeleton and CSS is the clothing, JavaScript is the **muscles and brain** — it makes things move and respond.

---

## 🌐 Where Does JavaScript Run?

JavaScript runs in **two environments**:

| Environment | Examples | Used For |
|-------------|---------|---------|
| **Browser** (Client-side) | Chrome, Firefox, Edge | DOM manipulation, UI, animations |
| **Server** (Node.js) | Node.js, Deno | Backend APIs, databases, file systems |

> In this course, we focus on **browser JavaScript** (front-end).

---

## 📄 How to Add JavaScript to a Web Page

### 1. Inline JavaScript (Not Recommended)

Written directly inside an HTML tag's event attribute.

```html
<button onclick="alert('Hello!')">Click Me</button>
```

❌ Hard to maintain — avoid for real projects.

---

### 2. Internal JavaScript

Written inside a `<script>` tag in the HTML file.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>My Page</title>
</head>
<body>
  <h1>Hello!</h1>

  <script>
    // JavaScript goes here
    console.log("Page loaded!");
  </script>
</body>
</html>
```

✅ Good for small demos and practice.

> ⚠️ **Place `<script>` before the closing `</body>` tag** — this ensures the HTML loads before JavaScript runs.

---

### 3. External JavaScript ✅ (Best Practice)

JavaScript written in a separate `.js` file and linked to the HTML.

**script.js:**
```javascript
console.log("Hello from external JS!");
```

**index.html:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>My Page</title>
</head>
<body>
  <h1>Hello!</h1>

  <!-- Link to external JS file — always before </body> -->
  <script src="script.js"></script>
</body>
</html>
```

✅ Best for real projects  
✅ Keeps HTML and JS separate  
✅ One JS file can be reused across many pages  

---

## 🖥️ Your First JavaScript Program

Open the browser Console and type:

```javascript
console.log("Hello, World!");
```

`console.log()` is your most important debugging tool — it prints messages to the **browser console**.

### How to Open the Console:
- **Chrome/Edge:** Press `F12` → Click "Console" tab
- **Firefox:** Press `F12` → Click "Console" tab
- **Mac:** `Cmd + Option + J`

---

## 📊 JavaScript vs HTML vs CSS

| Language | Role | Example |
|----------|------|---------|
| **HTML** | Structure | `<h1>Hello</h1>` |
| **CSS** | Style | `color: blue;` |
| **JavaScript** | Behavior | `document.getElementById("btn").onclick = ...` |

---

## ✅ Key Takeaways

- JavaScript = the programming language that makes web pages interactive.
- Always use **external JS files** for real projects (link with `<script src="...">`).
- Place `<script>` tags **before `</body>`**, not in `<head>`.
- `console.log()` is your best friend for testing and debugging.
- JavaScript runs in the **browser** without any special software.

---

> ➡️ **Next:** `02-variables-and-data-types.md` — Learn how to store and work with data.
