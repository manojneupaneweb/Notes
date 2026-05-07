# 02 — Basic HTML Tags

---

## 🏷️ What are Tags?

Tags are the building blocks of HTML. They tell the browser what kind of content to display.

```html
<tagname>Content here</tagname>
```

---

## 📦 The Three Core Tags

### `<html>` — The Root Element
Everything on a web page lives inside `<html>`.

```html
<html lang="en">
  <!-- Everything goes in here -->
</html>
```

### `<head>` — Metadata Container
Contains information **about** the page (not visible to users).

```html
<head>
  <meta charset="UTF-8" />
  <title>Page Title</title>
  <link rel="stylesheet" href="style.css" />  <!-- link CSS here -->
</head>
```

### `<body>` — Visible Content
Everything the **user sees** on the page goes here.

```html
<body>
  <h1>Welcome!</h1>
  <p>This is visible.</p>
</body>
```

---

## 🔤 Headings: `<h1>` to `<h6>`

Headings define the importance/hierarchy of text. `<h1>` is the most important.

```html
<h1>Heading 1 — Main Title (Biggest)</h1>
<h2>Heading 2 — Section Title</h2>
<h3>Heading 3 — Sub-section</h3>
<h4>Heading 4</h4>
<h5>Heading 5</h5>
<h6>Heading 6 — Smallest Heading</h6>
```

> ⚠️ **SEO Rule:** Only use **one `<h1>` per page**. It tells search engines the main topic.

> 💡 **Tip:** Use headings for structure, not just to make text big. Use CSS to change font size.

---

## 📝 Paragraph: `<p>`

Used for blocks of text content.

```html
<p>This is a paragraph. It creates a block of text with spacing above and below.</p>

<p>This is a second paragraph. Each paragraph starts on a new line automatically.</p>
```

---

## ↩️ Line Break: `<br>`

Forces text onto the next line **within** the same paragraph. It's self-closing.

```html
<p>
  Line one of this poem.<br />
  Line two continues here.<br />
  And this is line three.
</p>
```

> ⚠️ **Don't overuse `<br>`!** Use CSS margins/padding for spacing instead.

---

## ➖ Horizontal Rule: `<hr>`

Creates a horizontal dividing line. Useful for separating sections.

```html
<h2>Section One</h2>
<p>Content of section one.</p>

<hr />  <!-- This draws a line -->

<h2>Section Two</h2>
<p>Content of section two.</p>
```

---

## 🧪 Full Example — Putting It Together

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Basic HTML Tags Demo</title>
</head>
<body>

    <h1>My Personal Blog</h1>

    <h2>About Me</h2>
    <p>Hello! My name is Alex. I am a web developer from Nepal.</p>

    <h2>My Skills</h2>
    <p>
        I know HTML, CSS, and JavaScript.<br />
        I am currently learning Tailwind CSS.
    </p>

    <hr />

    <h2>Contact</h2>
    <p>Feel free to reach out to me anytime.</p>

</body>
</html>
```

---

## ✅ Key Takeaways

| Tag | Purpose |
|-----|---------|
| `<html>` | Root of the page |
| `<head>` | Meta info (not visible) |
| `<body>` | Visible content |
| `<h1>` to `<h6>` | Headings — 1 is biggest, 6 is smallest |
| `<p>` | Paragraph of text |
| `<br>` | Line break (self-closing) |
| `<hr>` | Horizontal divider (self-closing) |

---

> ➡️ **Next:** `03-text-formatting.md` — Bold, italic, highlight, and more text formatting tags.
