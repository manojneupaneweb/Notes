# 09 — Advanced HTML: Meta Tags, SEO & Accessibility

---

## 📌 Part 1: Meta Tags

Meta tags live inside `<head>` and provide information **about** the page. They are invisible to users but read by browsers and search engines.

### Essential Meta Tags:
```html
<head>
    <!-- Character encoding — always include this first! -->
    <meta charset="UTF-8">

    <!-- Responsive design on mobile -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- Page description (shown in search engine results) -->
    <meta name="description" content="Learn HTML and CSS from scratch with practical examples.">

    <!-- Keywords (less important now, but still used) -->
    <meta name="keywords" content="HTML tutorial, learn HTML, CSS basics, web development">

    <!-- Author of the page -->
    <meta name="author" content="Manoj Neupane">

    <!-- Prevent robots from indexing (useful for dev environments) -->
    <meta name="robots" content="noindex, nofollow">

    <!-- Control link preview (Open Graph — for social media) -->
    <meta property="og:title" content="Learn HTML from Scratch">
    <meta property="og:description" content="A complete guide to HTML for beginners.">
    <meta property="og:image" content="https://example.com/thumbnail.jpg">
    <meta property="og:url" content="https://example.com/html-guide">

    <!-- Twitter Card (for Twitter previews) -->
    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:title" content="Learn HTML from Scratch">
    <meta name="twitter:image" content="https://example.com/thumbnail.jpg">

    <!-- Refresh page after N seconds -->
    <meta http-equiv="refresh" content="30">

    <title>Page Title — Site Name</title>
</head>
```

---

## 🔍 Part 2: SEO Basics

**SEO** (Search Engine Optimization) is the practice of making your page rank higher on Google and other search engines.

### HTML SEO Best Practices:

#### 1. Use a Good `<title>` Tag
```html
<!-- Bad: Too generic -->
<title>Home</title>

<!-- Good: Descriptive and includes keyword -->
<title>HTML Tutorial for Beginners — Learn Web Development | MyBlog</title>
```
- Should be **50-60 characters** max.
- Include the **primary keyword**.

#### 2. Write a Compelling Meta Description
```html
<meta name="description" content="Learn HTML from scratch with this beginner-friendly tutorial. Covers all essential tags, forms, and semantic HTML with real examples.">
```
- Should be **150-160 characters** max.
- Should encourage users to click.

#### 3. Use One `<h1>` Per Page
```html
<!-- Only one h1 per page — it's the main topic -->
<h1>HTML Tutorial: The Complete Beginner's Guide</h1>

<!-- Then use h2 for sections, h3 for subsections -->
<h2>Basic HTML Tags</h2>
<h3>Heading Tags</h3>
```

#### 4. Use Descriptive `alt` on Images
```html
<!-- Bad: No information -->
<img src="photo.jpg" alt="image">

<!-- Good: Describes the content and includes a keyword -->
<img src="html-tutorial.jpg" alt="HTML code displayed on a laptop screen showing a web tutorial">
```

#### 5. Use Clean URLs and Internal Links
```html
<!-- Link to related pages on your site -->
<a href="/css-tutorial">Next: Learn CSS →</a>
```

#### 6. Structured Data (Schema.org)
```html
<script type="application/ld+json">
{
    "@context": "https://schema.org",
    "@type": "Article",
    "headline": "HTML Tutorial for Beginners",
    "author": { "@type": "Person", "name": "Manoj Neupane" },
    "datePublished": "2025-04-29"
}
</script>
```

---

## ♿ Part 3: Accessibility (a11y) Basics

**Accessibility** means making websites usable for everyone, including people with disabilities (visual, hearing, motor).

> 💡 **Quick Fact:** Over 1 billion people worldwide have some form of disability. Good accessibility helps everyone!

### ARIA (Accessible Rich Internet Applications)

ARIA attributes give extra meaning to HTML for screen readers.

#### `aria-label` — Names an element
```html
<!-- Without label text, screen readers don't know what this button does -->
<button aria-label="Close dialog">✕</button>

<!-- For an icon-only link -->
<a href="https://twitter.com" aria-label="Follow us on Twitter">
    <img src="twitter-icon.svg" alt="">
</a>
```

#### `aria-hidden` — Hides from screen readers
```html
<!-- Decorative icons should be hidden from screen readers -->
<span aria-hidden="true">🎉</span>
<span>Congratulations!</span>
```

#### `aria-describedby` — Links to a description
```html
<input type="password" id="pass" aria-describedby="pass-hint">
<p id="pass-hint">Password must be at least 8 characters long.</p>
```

#### `role` — Defines the type of element
```html
<!-- When not using semantic tags (avoid if possible) -->
<div role="navigation"> ... </div>
<div role="main"> ... </div>
<div role="button" tabindex="0"> Click Me </div>
```

### Accessibility Checklist:
```html
<!-- ✅ Always use labels with inputs -->
<label for="email">Email:</label>
<input type="email" id="email">

<!-- ✅ Always use alt text on images -->
<img src="team.jpg" alt="Our team of 5 developers at our office">

<!-- ✅ Use semantic HTML (header, nav, main, footer) -->

<!-- ✅ Ensure links make sense out of context -->
<!-- Bad: -->
<a href="/products">Click here</a>
<!-- Good: -->
<a href="/products">View all products</a>

<!-- ✅ Make sure all interactive elements are keyboard accessible -->
<button>Submit</button> <!-- buttons are keyboard accessible by default -->

<!-- ✅ Use sufficient color contrast (not your job in HTML, but CSS) -->

<!-- ✅ Add skip navigation link for keyboard users -->
<a href="#main-content" class="skip-link">Skip to main content</a>
<main id="main-content"> ... </main>
```

---

## 🏗️ Full Example: SEO & Accessible Page

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="A free HTML and CSS tutorial for beginners. Learn web development step by step.">
    <meta name="author" content="Manoj Neupane">
    <meta property="og:title" content="HTML & CSS Tutorial — Learn Web Dev">
    <meta property="og:image" content="thumbnail.jpg">
    <title>HTML & CSS Tutorial — LearnWeb.com</title>
</head>
<body>

    <!-- Skip link for screen readers/keyboard navigation -->
    <a href="#main" style="position:absolute;left:-9999px">Skip to main content</a>

    <header>
        <h1>LearnWeb — Your Web Dev Guide</h1>
        <nav aria-label="Main navigation">
            <ul>
                <li><a href="/">Home</a></li>
                <li><a href="/html">HTML Tutorial</a></li>
                <li><a href="/css">CSS Tutorial</a></li>
            </ul>
        </nav>
    </header>

    <main id="main">
        <article>
            <h2>What is HTML?</h2>
            <p>HTML stands for HyperText Markup Language and is the backbone of every website.</p>

            <figure>
                <img src="html-code.jpg" alt="Screenshot of HTML code in a text editor showing basic page structure">
                <figcaption>Example of HTML code structure in VS Code.</figcaption>
            </figure>
        </article>
    </main>

    <footer>
        <p>&copy; 2025 LearnWeb. All rights reserved.</p>
    </footer>

</body>
</html>
```

---

## ✅ Key Takeaways

- **Meta tags** provide page info to browsers and search engines.
- **SEO** = Good title, description, one `<h1>`, descriptive `alt` text.
- **Accessibility** = Use semantic tags, `alt` on images, `aria-label` on icon buttons, good link text.
- Test accessibility with keyboard navigation (Tab key) and a screen reader.

---

> 🎉 **You've completed all HTML Notes!**
> ➡️ **Next:** Open `css-notes/01-introduction.md` to start learning CSS!
