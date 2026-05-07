# 01 — Introduction to HTML

---

## 📌 What is HTML?

**HTML** stands for **HyperText Markup Language**.

- It is the **skeleton/structure** of every web page.
- HTML is **NOT** a programming language — it is a **markup language**.
- It uses **tags** to define elements like headings, paragraphs, images, links, etc.
- Every webpage you visit is built with HTML at its core.

> 💡 **Simple Analogy:** Think of HTML as the **blueprint of a house**. It defines what rooms (sections) exist, but not how they are decorated. CSS does the decoration.

---

## 🌐 How the Web Works (Simplified)

When you type a URL in your browser, here's what happens:

```
You type: https://google.com
         ↓
Browser sends a request to Google's server
         ↓
Server sends back an HTML file
         ↓
Browser reads the HTML and displays the page
```

**Key Terms:**
| Term | Meaning |
|------|---------|
| **Browser** | Chrome, Firefox, Edge — it reads and renders HTML |
| **Server** | A computer that stores and sends web files |
| **URL** | The address of a web page (e.g., `https://google.com`) |
| **HTML File** | A `.html` file that contains the structure of the page |

---

## 🏗️ Basic Structure of an HTML Document

Every HTML file follows this exact structure:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>My First Web Page</title>
  </head>
  <body>
    <h1>Hello, World!</h1>
    <p>This is my first web page.</p>
  </body>
</html>
```

### Breaking It Down:

| Tag / Part | Purpose |
|-----------|---------|
| `<!DOCTYPE html>` | Tells the browser this is an HTML5 document. Always write this first! |
| `<html lang="en">` | The root element. Everything lives inside here. `lang="en"` sets the language to English. |
| `<head>` | Contains **meta information** — not visible on the page, but important for the browser and SEO. |
| `<meta charset="UTF-8">` | Sets the character encoding. Ensures special characters display correctly. |
| `<meta name="viewport">` | Makes the page responsive on mobile devices. |
| `<title>` | The text shown in the browser tab. |
| `<body>` | Everything **visible** on the page goes here. |

---

## 🔑 How HTML Tags Work

```
Opening Tag    Content     Closing Tag
    ↓              ↓             ↓
  <h1>    Hello, World!    </h1>
```

- **Opening tag:** `<tagname>`
- **Closing tag:** `</tagname>` (notice the forward slash `/`)
- **Content:** What appears between the tags
- **Self-closing tags:** Some tags don't have content and close themselves: `<br />`, `<img />`, `<hr />`

---

## 📝 Your First HTML File — Step by Step

**Step 1:** Open any text editor (VS Code, Notepad, etc.)

**Step 2:** Type the basic structure above.

**Step 3:** Save the file as `index.html`

> ⚠️ **Important:** Always name your main file `index.html`. Servers look for this file by default.

**Step 4:** Open the file in your browser by double-clicking it.

---

## ✅ Key Takeaways

- HTML defines the **structure** of a web page.
- A web page = HTML (structure) + CSS (style) + JavaScript (behavior).
- Every HTML file must have: `<!DOCTYPE html>`, `<html>`, `<head>`, and `<body>`.
- Save files as `.html` and open them in a browser to see results.

---

> ➡️ **Next:** `02-basic-tags.md` — Learn the most commonly used HTML tags.
