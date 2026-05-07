# 03 — Text Formatting Tags

---

## 📌 What is Text Formatting?

HTML provides special tags to style text with **semantic meaning**. This is different from CSS — these tags tell the browser (and screen readers) that the text has special importance.

> 💡 **Semantic vs Visual:** `<b>` makes text bold visually, but `<strong>` makes text bold AND tells the browser this text is **important**.

---

## 💪 Bold Text

### `<b>` — Bold (Visual Only)
Makes text **bold** but has no extra meaning.

```html
<p>My favorite language is <b>HTML</b>.</p>
```

### `<strong>` — Bold with Importance ✅ (Preferred)
Makes text bold AND indicates it is **important**. Screen readers will emphasize it.

```html
<p><strong>Warning:</strong> Do not delete this file!</p>
```

> 🔑 **Best Practice:** Use `<strong>` instead of `<b>` in most cases.

---

## 🔤 Italic Text

### `<i>` — Italic (Visual Only)
Makes text *italic* but has no extra meaning. Used for technical terms, foreign words.

```html
<p>The word <i>Bonjour</i> means "hello" in French.</p>
```

### `<em>` — Italic with Emphasis ✅ (Preferred)
Makes text italic AND tells the browser this text needs **emphasis** in speech.

```html
<p>I <em>really</em> want to learn CSS!</p>
```

---

## 🖌️ Other Formatting Tags

### `<mark>` — Highlighted Text
Highlights text with a yellow background (like a highlighter pen).

```html
<p>The exam is on <mark>Friday, May 10th</mark>. Don't miss it!</p>
```

### `<small>` — Smaller Text
Makes text smaller than the surrounding text. Used for fine print.

```html
<p>Buy now for just $9.99 <small>(taxes not included)</small></p>
```

### `<del>` — Deleted/Strikethrough Text
Shows text that has been ~~removed~~ (crossed out). Used for corrections or price reductions.

```html
<p>Original price: <del>$50.00</del> Now only $25.00!</p>
```

### `<ins>` — Inserted Text
Shows text that has been added (usually underlined). Works as the opposite of `<del>`.

```html
<p>The meeting is on <del>Monday</del> <ins>Tuesday</ins>.</p>
```

---

## 🧪 Full Example — All Together

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Text Formatting Demo</title>
</head>
<body>

    <h1>Product Review</h1>

    <!-- Strong and Em for emphasis -->
    <p>This is <strong>the best laptop</strong> I have ever used.</p>
    <p>I was <em>completely amazed</em> by the battery life.</p>

    <!-- Mark to highlight important info -->
    <p>Sale ends on <mark>December 31st</mark>. Don't miss out!</p>

    <!-- Del and Ins for showing changes -->
    <p>Old price: <del>$1500</del> New price: <ins>$999</ins></p>

    <!-- b and i for stylistic use -->
    <p>Model: <b>ProBook X500</b></p>
    <p>Category: <i>Electronics / Laptops</i></p>

    <!-- Small for fine print -->
    <p>
      All prices in USD.
      <small>*Prices may vary by region.</small>
    </p>

</body>
</html>
```

---

## 📊 Quick Reference Table

| Tag | Effect | Use Case |
|-----|--------|----------|
| `<b>` | **Bold** (visual) | Style without importance |
| `<strong>` | **Bold** (important) | Warnings, key points |
| `<i>` | *Italic* (visual) | Foreign words, technical terms |
| `<em>` | *Italic* (emphasis) | Stressed words in sentences |
| `<mark>` | Highlighted | Key dates, search results |
| `<small>` | Smaller text | Fine print, disclaimers |
| `<del>` | ~~Strikethrough~~ | Removed/old content, price cuts |
| `<ins>` | Underlined insert | Corrections, added content |

---

## ✅ Key Takeaways

- Use **semantic tags** (`<strong>`, `<em>`) over visual-only tags (`<b>`, `<i>`).
- These tags help **accessibility** — screen readers use them to understand the page.
- Combine multiple formatting tags carefully: `<strong><em>Very Important!</em></strong>`

---

> ➡️ **Next:** `04-links-and-media.md` — Links, images, audio, and video.
