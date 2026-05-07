# 08 — Semantic HTML

---

## 📌 What is Semantic HTML?

**Semantic HTML** uses tags that describe the **meaning and purpose** of the content, not just how it looks.

### Non-Semantic (Bad Practice):
```html
<div id="header"> ... </div>
<div id="nav"> ... </div>
<div id="content"> ... </div>
<div id="footer"> ... </div>
```

### Semantic (Good Practice ✅):
```html
<header> ... </header>
<nav> ... </nav>
<main> ... </main>
<footer> ... </footer>
```

### Why Does It Matter?
1. **SEO:** Search engines understand your page structure better.
2. **Accessibility:** Screen readers can navigate the page properly.
3. **Readability:** Your code is easier to understand and maintain.

---

## 🏷️ Semantic Tags Reference

### `<header>`
The top section of the page or a content section. Usually contains the logo, site title, and navigation.

```html
<header>
    <h1>My Website</h1>
    <nav> ... </nav>
</header>
```

### `<nav>`
Contains navigation links. Helps screen readers find the site menu.

```html
<nav>
    <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About</a></li>
        <li><a href="/contact">Contact</a></li>
    </ul>
</nav>
```

### `<main>`
The main, unique content of the page. There should be **only one** `<main>` per page.

```html
<main>
    <h1>Welcome to My Blog</h1>
    <!-- Page articles go here -->
</main>
```

### `<article>`
A self-contained piece of content that could stand on its own (like a blog post, news article, or product card).

```html
<article>
    <h2>How to Learn HTML in 30 Days</h2>
    <p>Published: April 29, 2025</p>
    <p>Learning HTML is easier than most people think...</p>
</article>
```

### `<section>`
A thematic grouping of content, usually with a heading. Groups related content together.

```html
<section>
    <h2>Our Services</h2>
    <p>We offer web design, development, and SEO.</p>
</section>

<section>
    <h2>Testimonials</h2>
    <p>"Great team to work with!" — Client</p>
</section>
```

### `<aside>`
Content that is related to, but separate from, the main content. Used for sidebars, ads, or related links.

```html
<aside>
    <h3>Related Articles</h3>
    <ul>
        <li><a href="#">CSS Grid Tutorial</a></li>
        <li><a href="#">Flexbox Guide</a></li>
    </ul>
</aside>
```

### `<footer>`
The bottom section of the page. Usually contains copyright info, links, and contact details.

```html
<footer>
    <p>&copy; 2025 My Website. All rights reserved.</p>
    <nav>
        <a href="/privacy">Privacy Policy</a>
        <a href="/terms">Terms of Service</a>
    </nav>
</footer>
```

### Other Semantic Tags:
| Tag | Meaning |
|-----|---------|
| `<figure>` | Self-contained content like images or code |
| `<figcaption>` | Caption for a `<figure>` |
| `<time>` | Represents a date/time |
| `<address>` | Contact information |
| `<details>` | Disclosure widget (expandable) |
| `<summary>` | Summary/heading for `<details>` |

---

## 🌐 Full Page Structure Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Blog - Semantic HTML Demo</title>
</head>
<body>

    <!-- HEADER: Logo and navigation -->
    <header>
        <h1>📝 My Blog</h1>
        <nav>
            <a href="/">Home</a>
            <a href="/about">About</a>
            <a href="/contact">Contact</a>
        </nav>
    </header>

    <!-- MAIN: Primary content -->
    <main>

        <!-- SECTION: Blog posts section -->
        <section>
            <h2>Latest Articles</h2>

            <!-- ARTICLE: Individual blog post -->
            <article>
                <h3>Getting Started with HTML</h3>
                <time datetime="2025-04-29">April 29, 2025</time>
                <p>HTML is the foundation of every website. In this article, we'll cover the basics...</p>
                <a href="/posts/html-basics">Read More →</a>
            </article>

            <article>
                <h3>Why CSS is Important</h3>
                <time datetime="2025-04-28">April 28, 2025</time>
                <p>CSS transforms plain HTML into beautiful, styled pages. Let's explore how...</p>
                <a href="/posts/css-intro">Read More →</a>
            </article>
        </section>

        <!-- FIGURE: Image with caption -->
        <figure>
            <img src="https://picsum.photos/800/300" alt="A web developer at work">
            <figcaption>A developer building a modern web application.</figcaption>
        </figure>

    </main>

    <!-- ASIDE: Sidebar -->
    <aside>
        <h3>Categories</h3>
        <ul>
            <li><a href="#">HTML (5)</a></li>
            <li><a href="#">CSS (8)</a></li>
            <li><a href="#">JavaScript (12)</a></li>
        </ul>
    </aside>

    <!-- FOOTER: Copyright and links -->
    <footer>
        <address>
            Contact: <a href="mailto:hello@myblog.com">hello@myblog.com</a>
        </address>
        <p>&copy; 2025 My Blog. All rights reserved.</p>
    </footer>

</body>
</html>
```

---

## ✅ Key Takeaways

- Use semantic tags instead of `<div>` everywhere.
- Page structure: `<header>` → `<nav>` → `<main>` → `<footer>`.
- Use `<article>` for self-contained content (blog posts).
- Use `<section>` to group related content with a heading.
- Use `<aside>` for sidebars and related links.
- Semantic HTML helps **SEO**, **accessibility**, and **code readability**.

---

> ➡️ **Next:** `09-advanced-html.md` — Meta tags, SEO, and accessibility.
