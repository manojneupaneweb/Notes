# 📚 HTML & CSS — Complete Reference Notes
### Frontend Development · Beginner to Advanced

> **Author:** Manoj Neupane  
> **Last Updated:** May 2026  
> **Goal:** A complete, detailed reference for HTML and CSS — from basics to advanced techniques.

---

## 📑 Table of Contents

### 🧱 HTML
- [01 — Introduction to HTML](#01--introduction-to-html)
- [02 — Basic HTML Tags](#02--basic-html-tags)
- [03 — Text Formatting Tags](#03--text-formatting-tags)
- [04 — Links and Media](#04--links-and-media)
- [05 — Lists](#05--lists)
- [06 — Tables](#06--tables)
- [07 — Forms](#07--forms-the-most-important-html-topic)
- [08 — Semantic HTML](#08--semantic-html)
- [09 — Advanced HTML: Meta Tags, SEO & Accessibility](#09--advanced-html-meta-tags-seo--accessibility)

### 🎨 CSS
- [CSS 01 — Introduction to CSS](#css-01--introduction-to-css)
- [CSS 02 — CSS Selectors](#css-02--css-selectors)
- [CSS 03 — Colors and Units](#css-03--colors-and-units)
- [CSS 04 — The Box Model](#css-04--the-css-box-model)
- [CSS 05 — Display and Positioning](#css-05--display-and-positioning)
- [CSS 06 — Flexbox](#css-06--flexbox)
- [CSS 07 — Grid Layout](#css-07--grid-layout)
- [CSS 08 — Responsive Design](#css-08--responsive-design)
- [CSS 09 — Animations & Transitions](#css-09--animations--transitions)

---

# 🧱 HTML Notes

---

## 01 — Introduction to HTML

### 📌 What is HTML?

**HTML** stands for **HyperText Markup Language**.

- It is the **skeleton/structure** of every web page.
- HTML is **NOT** a programming language — it is a **markup language**.
- It uses **tags** to define elements like headings, paragraphs, images, links, etc.
- Every webpage you visit is built with HTML at its core.

> 💡 **Simple Analogy:** Think of HTML as the **blueprint of a house**. It defines what rooms (sections) exist, but not how they are decorated. CSS does the decoration.

---

### 🌐 How the Web Works (Simplified)

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

| Term | Meaning |
|------|---------|
| **Browser** | Chrome, Firefox, Edge — it reads and renders HTML |
| **Server** | A computer that stores and sends web files |
| **URL** | The address of a web page (e.g., `https://google.com`) |
| **HTML File** | A `.html` file that contains the structure of the page |

---

### 🏗️ Basic Structure of an HTML Document

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

| Tag / Part | Purpose |
|-----------|---------|
| `<!DOCTYPE html>` | Tells the browser this is an HTML5 document. Always write this first! |
| `<html lang="en">` | The root element. Everything lives inside here. `lang="en"` sets the language. |
| `<head>` | Contains **meta information** — not visible on the page. |
| `<meta charset="UTF-8">` | Sets the character encoding. Ensures special characters display correctly. |
| `<meta name="viewport">` | Makes the page responsive on mobile devices. |
| `<title>` | The text shown in the browser tab. |
| `<body>` | Everything **visible** on the page goes here. |

---

### 🔑 How HTML Tags Work

```
Opening Tag    Content     Closing Tag
    ↓              ↓             ↓
  <h1>    Hello, World!    </h1>
```

- **Opening tag:** `<tagname>`
- **Closing tag:** `</tagname>` (notice the forward slash `/`)
- **Content:** What appears between the tags
- **Self-closing tags:** Some tags don't have content and close themselves: `<br />`, `<img />`, `<hr />`

### ✅ Key Takeaways

- HTML defines the **structure** of a web page.
- A web page = HTML (structure) + CSS (style) + JavaScript (behavior).
- Every HTML file must have: `<!DOCTYPE html>`, `<html>`, `<head>`, and `<body>`.
- Save files as `.html` and open them in a browser to see results.

---

## 02 — Basic HTML Tags

### 🔤 Headings: `<h1>` to `<h6>`

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

### 📝 Paragraph: `<p>`

Used for blocks of text content.

```html
<p>This is a paragraph. It creates a block of text with spacing above and below.</p>

<p>This is a second paragraph. Each paragraph starts on a new line automatically.</p>
```

---

### ↩️ Line Break: `<br>` and Horizontal Rule: `<hr>`

```html
<!-- Line break: forces text to next line within the same paragraph -->
<p>
  Line one of this poem.<br />
  Line two continues here.<br />
  And this is line three.
</p>

<!-- Horizontal rule: creates a dividing line between sections -->
<h2>Section One</h2>
<p>Content of section one.</p>

<hr />

<h2>Section Two</h2>
<p>Content of section two.</p>
```

> ⚠️ **Don't overuse `<br>`!** Use CSS margins/padding for spacing instead.

---

### ✅ Key Takeaways

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

## 03 — Text Formatting Tags

### 📌 What is Text Formatting?

HTML provides special tags to style text with **semantic meaning**. This is different from CSS — these tags tell the browser (and screen readers) that the text has special importance.

> 💡 **Semantic vs Visual:** `<b>` makes text bold visually, but `<strong>` makes text bold AND tells the browser this text is **important**.

---

### 💪 Bold Text

#### `<b>` — Bold (Visual Only)
Makes text **bold** but has no extra meaning.
```html
<p>My favorite language is <b>HTML</b>.</p>
```

#### `<strong>` — Bold with Importance ✅ (Preferred)
Makes text bold AND indicates it is **important**. Screen readers will emphasize it.
```html
<p><strong>Warning:</strong> Do not delete this file!</p>
```

> 🔑 **Best Practice:** Use `<strong>` instead of `<b>` in most cases.

---

### 🔤 Italic Text

#### `<i>` — Italic (Visual Only)
Makes text *italic* but has no extra meaning. Used for technical terms, foreign words.
```html
<p>The word <i>Bonjour</i> means "hello" in French.</p>
```

#### `<em>` — Italic with Emphasis ✅ (Preferred)
Makes text italic AND tells the browser this text needs **emphasis** in speech.
```html
<p>I <em>really</em> want to learn CSS!</p>
```

---

### 🖌️ Other Formatting Tags

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

```html
<!-- mark: highlight like a pen -->
<p>The exam is on <mark>Friday, May 10th</mark>. Don't miss it!</p>

<!-- small: fine print -->
<p>Buy now for just $9.99 <small>(taxes not included)</small></p>

<!-- del and ins: show changes -->
<p>Old price: <del>$50.00</del> New price: <ins>$25.00</ins></p>
```

### ✅ Key Takeaways

- Use **semantic tags** (`<strong>`, `<em>`) over visual-only tags (`<b>`, `<i>`).
- These tags help **accessibility** — screen readers use them to understand the page.
- Combine multiple formatting tags carefully: `<strong><em>Very Important!</em></strong>`

---

## 04 — Links and Media

### 🔗 The Anchor Tag: `<a>`

The `<a>` (anchor) tag creates hyperlinks — clickable text that takes you to another page, file, or location.

```html
<!-- Link to an external website -->
<a href="https://www.google.com">Go to Google</a>

<!-- Open in a NEW browser tab -->
<a href="https://www.youtube.com" target="_blank">Open YouTube in new tab</a>

<!-- Link to another page in the same project -->
<a href="about.html">About Page</a>

<!-- Link to a section on the SAME page using an ID -->
<a href="#contact">Jump to Contact Section</a>
<section id="contact">
  <h2>Contact Us</h2>
</section>

<!-- Email link — opens the user's email app -->
<a href="mailto:hello@example.com">Send me an email</a>

<!-- Phone link — opens the dialer on mobile -->
<a href="tel:+977-9800000000">Call Us</a>
```

#### `target` Attribute:
| Value | Behavior |
|-------|---------|
| `_blank` | Opens in a new tab |
| `_self` | Opens in the same tab (default) |
| `_parent` | Opens in parent frame |
| `_top` | Opens in the full browser window |

> 💡 **Tip:** Always use `target="_blank"` for external links so users don't leave your site.

---

### 🖼️ The Image Tag: `<img>`

The `<img>` tag displays images. It is **self-closing** (no closing tag needed).

```html
<!-- Image from the internet (URL) -->
<img src="https://picsum.photos/400/200" alt="A random photo" />

<!-- Image from your project folder -->
<img src="images/my-photo.jpg" alt="Profile photo of Alex" />

<!-- Image with size specified -->
<img src="logo.png" alt="Company Logo" width="150" height="75" />
```

| Attribute | Purpose |
|-----------|---------|
| `src` | The path/URL to the image |
| `alt` | Alternative text (shown if image fails to load; important for accessibility & SEO) |
| `width` | Set width in pixels |
| `height` | Set height in pixels |

> ⚠️ **NEVER skip the `alt` attribute!** It's required for accessibility and SEO.

---

### 🎵 Audio: `<audio>`

```html
<audio controls>
    <source src="audio/song.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
</audio>
```

| Attribute | Effect |
|-----------|--------|
| `controls` | Shows play/pause/volume controls |
| `autoplay` | Plays automatically on page load |
| `loop` | Repeats the audio forever |
| `muted` | Starts muted |

---

### 🎬 Video: `<video>`

```html
<video width="640" height="360" controls poster="thumbnail.jpg">
    <source src="video/intro.mp4" type="video/mp4">
    Your browser does not support the video tag.
</video>

<!-- Auto-playing muted loop (common for background videos) -->
<video autoplay muted loop>
    <source src="background.mp4" type="video/mp4">
</video>
```

| Attribute | Effect |
|-----------|--------|
| `controls` | Shows player controls |
| `autoplay` | Auto-plays when page loads |
| `loop` | Repeats video |
| `muted` | Starts muted (needed for autoplay in most browsers) |
| `poster` | Image shown before the video plays |

---

## 05 — Lists

HTML has **three types** of lists:

### 1️⃣ Unordered List: `<ul>`

Items have no order — they display with bullet points.

```html
<ul>
    <li>HTML</li>
    <li>CSS</li>
    <li>JavaScript</li>
</ul>
```

**When to use:** Navigation menus, features lists, any list where order doesn't matter.

---

### 2️⃣ Ordered List: `<ol>`

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

#### `type` Attribute for `<ol>`:
```html
<ol type="1">...</ol>  <!-- Numbers (default) -->
<ol type="A">...</ol>  <!-- Uppercase Letters -->
<ol type="a">...</ol>  <!-- Lowercase Letters -->
<ol type="I">...</ol>  <!-- Uppercase Roman Numerals -->
<ol type="i">...</ol>  <!-- Lowercase Roman Numerals -->
<ol start="5">...</ol> <!-- Start from a custom number -->
```

---

### 3️⃣ Description List: `<dl>`

A list of terms and their definitions. Used for glossaries.

```html
<dl>
    <dt>HTML</dt>
    <dd>HyperText Markup Language — the structure of web pages.</dd>

    <dt>CSS</dt>
    <dd>Cascading Style Sheets — the styling of web pages.</dd>
</dl>
```

| Tag | Meaning |
|-----|---------|
| `<dl>` | Description List (the container) |
| `<dt>` | Description Term (the word/key) |
| `<dd>` | Description Definition (the explanation, indented) |

---

### 🪆 Nested Lists

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
        </ul>
    </li>
</ul>
```

---

### ✅ Key Takeaways

| Tag | Type | Use |
|-----|------|-----|
| `<ul>` | Unordered | Bullet points; order doesn't matter |
| `<ol>` | Ordered | Numbered; order matters |
| `<dl>` | Description | Terms and their definitions |
| `<li>` | List Item | Used inside `<ul>` and `<ol>` |
| `<dt>` | Description Term | The word in a `<dl>` |
| `<dd>` | Description Detail | The explanation in a `<dl>` |

---

## 06 — Tables

### 📌 What are Tables?

HTML tables display **structured data** in rows and columns — like a spreadsheet.

> ⚠️ **Important:** Tables are for **data only**, not for page layouts! Use CSS Flexbox and Grid for layouts.

---

### 🏗️ Basic Table Structure

```html
<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Subject</th>
            <th>Marks</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Aarav Shah</td>
            <td>Mathematics</td>
            <td>95</td>
        </tr>
        <tr>
            <td>Priya Thapa</td>
            <td>Science</td>
            <td>87</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="2"><strong>Class Average</strong></td>
            <td>91</td>
        </tr>
    </tfoot>
</table>
```

| Tag | Name | Purpose |
|-----|------|---------|
| `<table>` | Table | The container for the entire table |
| `<tr>` | Table Row | A horizontal row of cells |
| `<th>` | Table Header | A header cell — **bold and centered** by default |
| `<td>` | Table Data | A regular data cell |
| `<thead>` | Table Head | Groups the header row(s) |
| `<tbody>` | Table Body | Groups the main data rows |
| `<tfoot>` | Table Footer | Groups the footer row(s) |

---

### 🔀 Spanning Columns and Rows

```html
<!-- colspan: merge cells horizontally -->
<td colspan="3">This cell takes up 3 columns</td>

<!-- rowspan: merge cells vertically -->
<td rowspan="2">I cover 2 rows</td>
```

---

### 🎨 Table Styling Tips (CSS)

```css
/* Remove double borders */
table { border-collapse: collapse; width: 100%; }

/* Cell spacing */
th, td { padding: 12px 15px; border: 1px solid #ccc; text-align: left; }

/* Striped rows for readability */
tr:nth-child(even) { background-color: #f9f9f9; }

/* Hover effect on rows */
tr:hover { background-color: #eef6ff; }

/* Styled header */
th { background-color: #4a90d9; color: white; }
```

---

## 07 — Forms (The Most Important HTML Topic!)

### 📌 Why Forms?

Forms are how users **send data** to a website. Every login page, contact form, checkout, and search box uses HTML forms.

---

### 🏗️ The `<form>` Tag

```html
<form action="/submit" method="POST">
    <!-- form inputs go here -->
</form>
```

| Attribute | Purpose |
|-----------|---------|
| `action` | URL where form data is sent (your backend) |
| `method` | How data is sent: `GET` (in URL) or `POST` (hidden in request body) |

> 💡 Use `method="POST"` for sensitive data like passwords. Use `method="GET"` for search forms.

---

### 🔤 All Common Input Types

```html
<!-- Text field (single line) -->
<input type="text" placeholder="Enter your name">

<!-- Password (hidden characters) -->
<input type="password" placeholder="Enter password">

<!-- Email (validates email format) -->
<input type="email" placeholder="you@example.com">

<!-- Number (only accepts numbers) -->
<input type="number" min="1" max="100">

<!-- Phone number -->
<input type="tel" placeholder="+977-XXXXXXXXXX">

<!-- URL (validates URL format) -->
<input type="url" placeholder="https://example.com">

<!-- Date picker -->
<input type="date">

<!-- Time picker -->
<input type="time">

<!-- Color picker -->
<input type="color" value="#ff0000">

<!-- Range slider -->
<input type="range" min="0" max="100" step="5">

<!-- File upload -->
<input type="file" accept=".jpg,.png,.pdf">

<!-- Checkbox (multiple can be checked) -->
<input type="checkbox" id="agree" name="agree">
<label for="agree">I agree to the terms</label>

<!-- Radio buttons (only one can be selected) -->
<input type="radio" id="male" name="gender" value="male">
<label for="male">Male</label>
<input type="radio" id="female" name="gender" value="female">
<label for="female">Female</label>

<!-- Hidden field -->
<input type="hidden" name="user_id" value="12345">

<!-- Search field -->
<input type="search" placeholder="Search...">

<!-- Submit button -->
<input type="submit" value="Submit Form">

<!-- Reset button (clears the form) -->
<input type="reset" value="Clear All">
```

---

### 🏷️ The `<label>` Tag

`<label>` connects text to an input. Always use it for **accessibility**.

```html
<!-- Method 1: Using `for` and `id` (BEST PRACTICE) -->
<label for="email">Email Address:</label>
<input type="email" id="email" name="email">

<!-- Method 2: Wrapping the input inside the label -->
<label>
    Full Name:
    <input type="text" name="fullname">
</label>
```

> 🔑 **Rule:** Every `<input>` should have a `<label>`.

---

### 📝 Textarea: `<textarea>`

```html
<label for="message">Your Message:</label>
<textarea id="message" name="message" rows="5" cols="40" placeholder="Write your message here..."></textarea>
```

---

### 📋 Dropdown: `<select>`

```html
<label for="country">Select Country:</label>
<select id="country" name="country">
    <option value="">-- Choose a Country --</option>
    <option value="np">Nepal</option>
    <option value="in">India</option>
    <option value="us">United States</option>
</select>

<!-- Group options with <optgroup> -->
<select name="skill">
    <optgroup label="Frontend">
        <option value="html">HTML</option>
        <option value="css">CSS</option>
    </optgroup>
    <optgroup label="Backend">
        <option value="nodejs">Node.js</option>
    </optgroup>
</select>

<!-- Allow multiple selections -->
<select name="languages" multiple>
    <option value="html">HTML</option>
    <option value="css">CSS</option>
    <option value="js">JavaScript</option>
</select>
```

---

### 🔘 The `<button>` Tag

```html
<!-- Submit button (submits the form) -->
<button type="submit">Submit</button>

<!-- Reset button (clears the form) -->
<button type="reset">Clear</button>

<!-- Regular button (use with JavaScript) -->
<button type="button" onclick="alert('Clicked!')">Click Me</button>

<!-- Button with emoji inside -->
<button type="submit">🚀 Send Message</button>
```

---

### 🔍 Important Input Attributes

| Attribute | Purpose |
|-----------|---------|
| `required` | Makes the field mandatory |
| `placeholder` | Ghost text inside the input |
| `value` | Default/pre-filled value |
| `name` | Key name sent to the server |
| `id` | Links to a `<label for="">` |
| `min` / `max` | Minimum/maximum for numbers and dates |
| `minlength` / `maxlength` | Character limits for text |
| `disabled` | Disables the input |
| `readonly` | Shows value but can't be edited |
| `autofocus` | Automatically focuses this field on page load |

---

### ✅ Key Takeaways

- Use `<label>` with every `<input>` for accessibility.
- Choose the correct `type` for each input — it helps with mobile keyboards and validation.
- Use `required` to prevent empty submissions.
- Use `name` attribute — it's how the server receives the data.
- Use `POST` for sensitive data, `GET` for searches.

---

## 08 — Semantic HTML

### 📌 What is Semantic HTML?

**Semantic HTML** uses tags that describe the **meaning and purpose** of the content, not just how it looks.

**Non-Semantic (Bad Practice) ❌:**
```html
<div id="header"> ... </div>
<div id="nav"> ... </div>
<div id="content"> ... </div>
<div id="footer"> ... </div>
```

**Semantic (Good Practice ✅):**
```html
<header> ... </header>
<nav> ... </nav>
<main> ... </main>
<footer> ... </footer>
```

**Why Does It Matter?**
1. **SEO:** Search engines understand your page structure better.
2. **Accessibility:** Screen readers can navigate the page properly.
3. **Readability:** Your code is easier to understand and maintain.

---

### 🏷️ Semantic Tags Reference

#### `<header>`
The top section of the page. Usually contains the logo, site title, and navigation.
```html
<header>
    <h1>My Website</h1>
    <nav> ... </nav>
</header>
```

#### `<nav>`
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

#### `<main>`
The main, unique content of the page. There should be **only one** `<main>` per page.
```html
<main>
    <h1>Welcome to My Blog</h1>
    <!-- Page articles go here -->
</main>
```

#### `<article>`
A self-contained piece of content that could stand on its own (like a blog post, news article, or product card).
```html
<article>
    <h2>How to Learn HTML in 30 Days</h2>
    <p>Published: April 29, 2025</p>
    <p>Learning HTML is easier than most people think...</p>
</article>
```

#### `<section>`
A thematic grouping of content, usually with a heading.
```html
<section>
    <h2>Our Services</h2>
    <p>We offer web design, development, and SEO.</p>
</section>
```

#### `<aside>`
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

#### `<footer>`
The bottom section of the page. Contains copyright info, links, and contact details.
```html
<footer>
    <p>&copy; 2025 My Website. All rights reserved.</p>
    <nav>
        <a href="/privacy">Privacy Policy</a>
        <a href="/terms">Terms of Service</a>
    </nav>
</footer>
```

#### Other Semantic Tags:
| Tag | Meaning |
|-----|---------|
| `<figure>` | Self-contained content like images or code |
| `<figcaption>` | Caption for a `<figure>` |
| `<time>` | Represents a date/time |
| `<address>` | Contact information |
| `<details>` | Disclosure widget (expandable) |
| `<summary>` | Summary/heading for `<details>` |

---

### 🌐 Full Semantic Page Structure

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
        <section>
            <h2>Latest Articles</h2>

            <article>
                <h3>Getting Started with HTML</h3>
                <time datetime="2025-04-29">April 29, 2025</time>
                <p>HTML is the foundation of every website...</p>
                <a href="/posts/html-basics">Read More →</a>
            </article>
        </section>

        <!-- Image with caption -->
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

## 09 — Advanced HTML: Meta Tags, SEO & Accessibility

### 📌 Part 1: Meta Tags

Meta tags live inside `<head>` and provide information **about** the page. They are invisible to users but read by browsers and search engines.

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

    <!-- Open Graph — for social media link previews -->
    <meta property="og:title" content="Learn HTML from Scratch">
    <meta property="og:description" content="A complete guide to HTML for beginners.">
    <meta property="og:image" content="https://example.com/thumbnail.jpg">
    <meta property="og:url" content="https://example.com/html-guide">

    <!-- Twitter Card (for Twitter previews) -->
    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:title" content="Learn HTML from Scratch">
    <meta name="twitter:image" content="https://example.com/thumbnail.jpg">

    <title>Page Title — Site Name</title>
</head>
```

---

### 🔍 Part 2: SEO Basics

**SEO** (Search Engine Optimization) = making your page rank higher on Google.

**HTML SEO Best Practices:**

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

#### 5. Structured Data (Schema.org)
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

### ♿ Part 3: Accessibility (a11y) Basics

**Accessibility** means making websites usable for everyone, including people with disabilities.

> 💡 **Quick Fact:** Over 1 billion people worldwide have some form of disability. Good accessibility helps everyone!

#### ARIA Attributes:

```html
<!-- aria-label: Names an element for screen readers -->
<button aria-label="Close dialog">✕</button>

<!-- aria-hidden: Hides decorative elements from screen readers -->
<span aria-hidden="true">🎉</span>
<span>Congratulations!</span>

<!-- aria-describedby: Links to a description -->
<input type="password" id="pass" aria-describedby="pass-hint">
<p id="pass-hint">Password must be at least 8 characters long.</p>

<!-- role: Defines the type of element -->
<div role="navigation"> ... </div>
<div role="main"> ... </div>
```

#### Accessibility Checklist:
```html
<!-- ✅ Always use labels with inputs -->
<label for="email">Email:</label>
<input type="email" id="email">

<!-- ✅ Always use alt text on images -->
<img src="team.jpg" alt="Our team of 5 developers at our office">

<!-- ✅ Use semantic HTML (header, nav, main, footer) -->

<!-- ✅ Good link text — make sense out of context -->
<!-- Bad: -->
<a href="/products">Click here</a>
<!-- Good: -->
<a href="/products">View all products</a>

<!-- ✅ Add skip navigation link for keyboard users -->
<a href="#main-content" class="skip-link">Skip to main content</a>
<main id="main-content"> ... </main>
```

---

# 🎨 CSS Notes

---

## CSS 01 — Introduction to CSS

### 📌 What is CSS?

**CSS** stands for **Cascading Style Sheets**.

- CSS is the **design/styling language** of the web.
- It controls the **look and feel** of HTML elements: colors, fonts, spacing, layout, animations.
- Without CSS, websites would look like plain black-and-white text documents.

> 💡 **Analogy:** If HTML is the skeleton of a house, CSS is the paint, wallpaper, furniture, and decoration.

---

### 📦 Three Types of CSS

#### 1. Inline CSS
```html
<p style="color: red; font-size: 20px;">This is red text.</p>
```
✅ Quick for testing | ❌ Hard to maintain

#### 2. Internal CSS
```html
<head>
    <style>
        body { background-color: #f0f0f0; }
        h1 { color: #333; }
    </style>
</head>
```
✅ Good for small projects | ❌ Doesn't scale well

#### 3. External CSS ✅ (Best Practice)
**style.css:**
```css
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
```

**index.html:**
```html
<head>
    <link rel="stylesheet" href="style.css">
</head>
```

✅ Best for real projects | ✅ One CSS file can style many pages | ✅ Easy to maintain

---

### ⚡ CSS Cascade: Which Style Wins?

The word "Cascading" means styles are applied in a specific order.

#### 1. Specificity (Most Important)
```
Inline style > ID (#id) > Class (.class) > Element (h1, p)
```

#### 2. Order
```css
p { color: red; }   /* This is overridden */
p { color: blue; }  /* This wins */
```

#### 3. `!important` (Use Sparingly!)
```css
p { color: red !important; } /* This beats everything */
```

---

## CSS 02 — CSS Selectors

### 1. Element Selector
Targets **all** elements of that type.
```css
p { font-size: 16px; color: #333; }
h1 { font-size: 36px; }
```

### 2. Class Selector `.`
Targets elements with a specific `class` attribute. **Reusable**.
```css
.highlight { background-color: yellow; font-weight: bold; }
```
```html
<p class="highlight">This text is highlighted.</p>
<span class="highlight">This too!</span>
```

### 3. ID Selector `#`
Targets a **single, unique** element. IDs must be unique on a page.
```css
#hero { background-color: #1a1a2e; color: white; padding: 80px; text-align: center; }
```

### 4. Universal Selector `*`
Targets **every single element** on the page.
```css
* { margin: 0; padding: 0; box-sizing: border-box; }
```

### 5. Grouping Selector `,`
Apply the same styles to multiple selectors at once.
```css
h1, h2, h3 { font-family: 'Georgia', serif; color: #2c3e50; }
```

### 6. Descendant Selector (space)
Targets elements **nested inside** another element.
```css
nav a { color: white; text-decoration: none; }
```

### 7. Child Selector `>`
Targets **direct children** only.
```css
ul > li { font-weight: bold; list-style-type: square; }
```

### 8. Pseudo-Classes `:`
Style elements based on their **state** or **position**.
```css
/* Link states */
a:link    { color: blue; }
a:visited { color: purple; }
a:hover   { color: red; }
a:active  { color: orange; }

/* Position-based */
li:first-child { font-weight: bold; }
li:last-child  { color: gray; }
li:nth-child(2) { color: red; }
li:nth-child(even) { background: #f0f0f0; }

/* Input states */
input:focus    { border-color: blue; outline: none; }
input:disabled { background: #eee; cursor: not-allowed; }

/* Negation */
p:not(.special) { color: gray; }
```

### 9. Pseudo-Elements `::`
Style **specific parts** of an element.
```css
p::first-letter { font-size: 2em; font-weight: bold; color: #e74c3c; }
p::first-line   { font-variant: small-caps; }

.warning::before { content: "⚠️ "; }
.required::after { content: " *"; color: red; }

::selection { background: #4a90d9; color: white; }
```

### 10. Attribute Selector `[]`
```css
input[type="text"]  { border: 1px solid blue; }
a[target="_blank"]  { color: orange; }
a[href^="https"]    { font-weight: bold; }   /* starts with */
a[href$=".pdf"]     { color: red; }           /* ends with */
```

---

### 📊 Selector Specificity Chart

| Selector | Specificity Points |
|---------|-------------------|
| Inline style | 1000 |
| `#id` | 100 |
| `.class`, `:pseudo-class`, `[attr]` | 10 |
| `element`, `::pseudo-element` | 1 |
| `*` Universal | 0 |

---

## CSS 03 — Colors and Units

### 🎨 Part 1: Colors

#### 1. Named Colors
```css
h1 { color: red; }
p  { color: steelblue; }
body { background-color: whitesmoke; }
```

#### 2. HEX Colors `#RRGGBB`
```css
h1 { color: #ff0000; }     /* Pure red */
h1 { color: #ffffff; }     /* White */
h1 { color: #000000; }     /* Black */
h1 { color: #2c3e50; }     /* Dark blue-gray */
h1 { color: #333; }        /* Shorthand for #333333 */

/* With transparency: #RRGGBBAA */
div { background: #2c3e5080; }  /* 50% transparent */
```

#### 3. RGB and RGBA
```css
h1 { color: rgb(255, 0, 0); }    /* Red */
h1 { color: rgb(44, 62, 80); }   /* Dark blue-gray */

/* With transparency */
.overlay { background: rgba(0, 0, 0, 0.5); }   /* 50% black */
.card    { background: rgba(255, 255, 255, 0.9); }
```

#### 4. HSL `hsl(hue, saturation%, lightness%)` ✅ Recommended for Design

- **Hue (0-360):** Color wheel position (0=red, 120=green, 240=blue)
- **Saturation (0-100%):** 0% = gray, 100% = full color
- **Lightness (0-100%):** 0% = black, 100% = white, 50% = normal

```css
/* Creating a color palette — just change lightness! */
.primary        { color: hsl(220, 80%, 50%); }  /* Normal */
.primary-light  { color: hsl(220, 80%, 70%); }  /* Lighter */
.primary-dark   { color: hsl(220, 80%, 30%); }  /* Darker */

/* HSLA with transparency */
.modal-bg { background: hsla(0, 0%, 0%, 0.5); }
```

#### 5. CSS Custom Properties (Variables) — Best Practice
```css
/* Define your color palette once */
:root {
    --primary: hsl(220, 80%, 55%);
    --primary-dark: hsl(220, 80%, 40%);
    --text: hsl(0, 0%, 15%);
    --bg: hsl(0, 0%, 98%);
    --danger: hsl(0, 75%, 55%);
    --success: hsl(140, 60%, 45%);
}

/* Use them everywhere */
button { background: var(--primary); }
button:hover { background: var(--primary-dark); }
body { color: var(--text); background: var(--bg); }
```

---

### 📏 Part 2: CSS Units

#### Absolute Units
| Unit | Example | Use Case |
|------|---------|----------|
| `px` | `font-size: 16px` | Most common — precise sizing |
| `pt` | `font-size: 12pt` | Print stylesheets |
| `cm` / `mm` | `width: 10cm` | Print layouts only |

#### Relative Units ✅ (Preferred for Responsive Design)

```css
/* % — Percentage (relative to parent) */
.container { width: 80%; }
img { max-width: 100%; }

/* em — Relative to current element's font-size (can compound!) */
body { font-size: 16px; }
h1 { font-size: 2em; }   /* 2 × 16px = 32px */

/* rem — Relative to root font-size (RECOMMENDED) */
html { font-size: 16px; }
h1 { font-size: 3rem; }  /* 3 × 16px = 48px */
p  { font-size: 1rem; }  /* 1 × 16px = 16px */

/* vw / vh — Viewport Width / Height */
.hero { width: 100vw; height: 100vh; }
h1 { font-size: 5vw; }

/* ch — Width of the "0" character */
p { max-width: 65ch; }  /* Readable line length */
```

| Unit | Relative to | Best Use |
|------|------------|---------|
| `px` | Fixed | Precise spacing, borders |
| `%` | Parent element | Flexible widths and heights |
| `em` | Current font-size | Padding/margin relative to font |
| `rem` | Root font-size | Font sizes, consistent spacing |
| `vw` | Viewport width | Full-width layouts |
| `vh` | Viewport height | Full-screen sections |
| `ch` | Character width | Text container widths |

---

## CSS 04 — The CSS Box Model

### 📌 What is the Box Model?

In CSS, **every HTML element is a rectangular box** with four layers:

```
┌─────────────────────────────────────┐
│             MARGIN                  │  ← Outermost: space outside the border
│   ┌─────────────────────────────┐   │
│   │           BORDER            │   │  ← The visible edge
│   │   ┌─────────────────────┐   │   │
│   │   │       PADDING       │   │   │  ← Space between border and content
│   │   │   ┌─────────────┐   │   │   │
│   │   │   │   CONTENT   │   │   │   │  ← Your actual text/image
│   │   │   └─────────────┘   │   │   │
│   │   └─────────────────────┘   │   │
│   └─────────────────────────────┘   │
└─────────────────────────────────────┘
```

---

### 📦 The Four Parts Explained

#### 1. Content
```css
.box { width: 300px; height: 150px; }
```

#### 2. Padding — Space inside the border
```css
.card {
    padding: 20px;           /* All four sides */
    padding-top: 10px;       /* Individual sides */
    
    /* Shorthand: Top Right Bottom Left */
    padding: 10px 20px 10px 20px;
    
    /* Shorthand: Vertical Horizontal */
    padding: 10px 20px;
}
```

#### 3. Border — The visible edge
```css
.card {
    border: 2px solid #333;     /* Width Style Color */
    border-radius: 8px;         /* Rounded corners */
    
    /* Individual sides */
    border-top: 4px solid blue;
    border-right: 1px dashed gray;
    border-bottom: none;
    
    /* Border styles */
    border-style: solid;    /* ──────── */
    border-style: dashed;   /* -------- */
    border-style: dotted;   /* ........ */
}
```

#### 4. Margin — Space outside the border
```css
.section {
    margin: 20px;       /* All sides */
    margin-top: 40px;
    
    /* Center a block element horizontally */
    margin: 0 auto;
    
    /* Negative margin (pulls elements closer) */
    margin-top: -10px;
}
```

---

### 🔑 The `box-sizing` Property (Critical!)

```css
/* DEFAULT (content-box) — padding and border are ADDED to width */
.box {
    width: 200px;
    padding: 20px;
    border: 2px solid;
    /* ACTUAL SIZE = 200 + 40 (padding) + 4 (border) = 244px */
}

/* FIX: border-box — width INCLUDES padding and border */
*, *::before, *::after {
    box-sizing: border-box; /* ← Always add this to every project! */
}
.box {
    width: 200px;
    padding: 20px;
    border: 2px solid;
    /* ACTUAL SIZE = 200px exactly! */
}
```

> ⚠️ **Always include `box-sizing: border-box` in your CSS reset!**

---

### 📊 Shorthand Reference

```css
/* 4 values: Top Right Bottom Left */
margin: 10px 20px 10px 20px;

/* 2 values: Top/Bottom  Left/Right */
margin: 10px 20px;

/* 1 value: All sides */
margin: 10px;

/* 3 values: Top  Left/Right  Bottom */
margin: 10px 20px 30px;
```

---

## CSS 05 — Display and Positioning

### 📌 Part 1: The `display` Property

| Value | Behavior |
|-------|---------|
| `block` | Full width, starts on a new line. Respects width/height. |
| `inline` | Content width only. Flows with text. Ignores width/height. |
| `inline-block` | Flows inline, but respects width/height. |
| `none` | Element is completely removed (takes no space). |
| `flex` | Flexbox container (see CSS 06) |
| `grid` | Grid container (see CSS 07) |

```css
/* inline vs inline-block example */
.btn {
    display: inline-block;  /* Can have width + height */
    width: 150px;
    padding: 10px 20px;
}

/* Hide/show pattern */
.hidden  { display: none; }   /* Element is gone */
.visible { display: block; }  /* Show it again */
```

> 💡 `visibility: hidden` hides the element but **keeps its space**. `display: none` removes it entirely.

---

### 📌 Part 2: The `position` Property

| Value | Relative To | Stays in Flow? | Use Case |
|-------|------------|---------------|---------|
| `static` | Normal flow | ✅ Yes | Default (no positioning) |
| `relative` | Its own position | ✅ Yes | Slight offsets, anchoring children |
| `absolute` | Nearest positioned ancestor | ❌ No | Badges, dropdowns, tooltips |
| `fixed` | Viewport | ❌ No | Navbars, chat buttons, back-to-top |
| `sticky` | Viewport (after scroll) | ✅ Yes | Sticky headers, table headers |

```css
/* relative: offset from its own position */
.box {
    position: relative;
    top: 20px;    /* Move 20px DOWN */
    left: 30px;   /* Move 30px RIGHT */
}

/* absolute: relative to nearest positioned parent */
.parent { position: relative; width: 400px; height: 300px; }
.badge {
    position: absolute;
    top: 10px;    /* 10px from TOP of parent */
    right: 10px;  /* 10px from RIGHT of parent */
}

/* fixed: stuck to viewport (doesn't scroll) */
.navbar {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 1000;
}

/* sticky: relative until scroll threshold, then fixed */
.section-header {
    position: sticky;
    top: 60px;   /* Sticks 60px from top */
}
```

---

### 🔢 `z-index` — Stack Order

```css
.modal    { position: fixed; z-index: 1000; }   /* On top of everything */
.navbar   { position: fixed; z-index: 100; }    /* Above content */
.card     { position: relative; z-index: 10; }  /* Normal stacking */
.bg-image { position: absolute; z-index: -1; }  /* Behind everything */
```

> ⚠️ `z-index` only works on **positioned elements** (not `position: static`).

---

## CSS 06 — Flexbox

### 📌 What is Flexbox?

**Flexbox** (Flexible Box Layout) arranges items in a **row or column**, distributes space, and aligns them easily.

---

### 🏗️ Setup: Container and Items

```html
<div class="container">    <!-- Flex Container -->
    <div class="item">A</div>   <!-- Flex Item -->
    <div class="item">B</div>
    <div class="item">C</div>
</div>
```

```css
.container { display: flex; }
```

---

### 📦 Container Properties

```css
.container {
    /* Direction */
    flex-direction: row;           /* → Left to right (default) */
    flex-direction: column;        /* ↓ Top to bottom */
    flex-direction: row-reverse;   /* ← Right to left */
    flex-direction: column-reverse;/* ↑ Bottom to top */

    /* Main axis alignment (horizontal when flex-direction: row) */
    justify-content: flex-start;    /* [A B C          ] */
    justify-content: flex-end;      /* [          A B C ] */
    justify-content: center;        /* [    A B C       ] */
    justify-content: space-between; /* [A     B     C   ] */
    justify-content: space-around;  /* [ A   B   C  ] */
    justify-content: space-evenly;  /* [  A  B  C  ] */

    /* Cross axis alignment (vertical when flex-direction: row) */
    align-items: stretch;      /* Items stretch to full height (default) */
    align-items: flex-start;   /* Align to top */
    align-items: flex-end;     /* Align to bottom */
    align-items: center;       /* Align to middle ← Most used! */

    /* Wrapping */
    flex-wrap: nowrap;   /* Default — shrink to fit */
    flex-wrap: wrap;     /* Items wrap onto multiple lines */

    /* Gap between items */
    gap: 20px;            /* Equal gap */
    gap: 10px 20px;       /* Row gap, Column gap */
}
```

---

### 📦 Item Properties

```css
.item {
    /* How much to grow */
    flex-grow: 0;    /* Default — don't grow */
    flex-grow: 1;    /* Take all available space */

    /* How much to shrink */
    flex-shrink: 1;  /* Default — can shrink */
    flex-shrink: 0;  /* Won't shrink */

    /* Starting size */
    flex-basis: 200px;    /* Start at 200px */
    flex-basis: 33.33%;   /* Start at 33.33% */

    /* Shorthand: grow shrink basis */
    flex: 1;         /* Shorthand for: 1 1 0 — most common! */
    flex: 0 0 200px; /* Fixed at 200px */

    /* Override alignment for one item */
    align-self: flex-end;

    /* Change display order */
    order: -1;  /* Appears FIRST */
    order: 1;   /* Appears LAST */
}
```

---

### 🧪 Real-World Flexbox Examples

```css
/* Perfect centering */
.hero {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

/* Navigation bar: logo left, links right */
.navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 30px;
    height: 60px;
}

/* Card grid with wrapping */
.card-container {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}
.card { flex: 1 1 300px; }  /* Min 300px, grow to fill */

/* Sidebar layout */
.page { display: flex; }
.sidebar { flex: 0 0 250px; }  /* Fixed 250px */
.main    { flex: 1; }           /* Remaining space */
```

---

### 📊 Flexbox Cheat Sheet

| Property | On | Values |
|---------|-----|--------|
| `flex-direction` | Container | `row` / `column` / `row-reverse` / `column-reverse` |
| `justify-content` | Container | `flex-start` / `center` / `flex-end` / `space-between` / `space-around` |
| `align-items` | Container | `stretch` / `flex-start` / `center` / `flex-end` |
| `flex-wrap` | Container | `nowrap` / `wrap` |
| `gap` | Container | any size value |
| `flex` | Item | `grow shrink basis` (e.g., `1`) |
| `align-self` | Item | `flex-start` / `center` / `flex-end` |
| `order` | Item | any integer |

---

## CSS 07 — Grid Layout

### 📌 What is CSS Grid?

**CSS Grid** is a two-dimensional layout system — it handles both **rows AND columns** at the same time.

> 💡 **Flexbox vs Grid:**
> - **Flexbox** = one-dimensional (row OR column at a time)
> - **Grid** = two-dimensional (rows AND columns simultaneously)
> - Use Flexbox for components, use Grid for full page layouts.

---

### 📐 Defining Columns and Rows

```css
.container {
    display: grid;

    /* 3 equal columns */
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-columns: repeat(3, 1fr);  /* Same thing! */

    /* Sidebar layout */
    grid-template-columns: 250px 1fr;

    /* 3 unequal columns */
    grid-template-columns: 1fr 2fr 1fr;  /* Middle is twice as wide */

    /* Rows */
    grid-template-rows: 100px 1fr 50px;

    /* Gap */
    gap: 20px;
    gap: 20px 30px;  /* Row gap, Column gap */
}
```

---

### 🎨 The `fr` Unit (Fraction)

`fr` divides available space into fractions.

```css
.container {
    /* 200px fixed, then remaining space split 1:2 */
    grid-template-columns: 200px 1fr 2fr;
}
```

---

### 🔀 Auto-Responsive Grid: `auto-fit` + `minmax`

```css
/* Automatically responsive — no media queries needed! */
.container {
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}
```

> 💡 `auto-fit` stretches columns to fill space. `auto-fill` may leave empty columns.

---

### 🖊️ Placing Items

```css
/* Span multiple columns/rows */
.wide-item { grid-column: span 2; }  /* Spans 2 columns */
.tall-item { grid-row: span 2; }     /* Spans 2 rows */

/* Specific placement */
.hero { grid-column: 1 / 3; grid-row: 1 / 2; }

/* Span ALL columns */
.full-width { grid-column: 1 / -1; }
```

---

### 🗺️ Grid Template Areas — Visual Layout

```css
.container {
    display: grid;
    grid-template-columns: 200px 1fr;
    grid-template-rows: 60px 1fr 50px;
    grid-template-areas:
        "header  header"
        "sidebar main  "
        "footer  footer";
    min-height: 100vh;
}

/* Assign elements to areas */
.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.footer  { grid-area: footer; }
```

---

### 📊 Grid Quick Reference

| Property | Purpose |
|---------|---------|
| `display: grid` | Enable grid |
| `grid-template-columns` | Define column sizes |
| `grid-template-rows` | Define row sizes |
| `gap` | Space between cells |
| `grid-template-areas` | Named visual layout |
| `grid-area` | Assign item to named area |
| `grid-column: span 2` | Item spans 2 columns |
| `grid-row: span 2` | Item spans 2 rows |
| `repeat(3, 1fr)` | 3 equal columns |
| `auto-fit` + `minmax` | Responsive columns automatically |

---

## CSS 08 — Responsive Design

### 📌 What is Responsive Design?

A **responsive website** looks and works great on **any screen size** — from a small phone to a large desktop monitor.

> 💡 **Why it matters:** Over 60% of web traffic is from mobile devices. Your site MUST work on phones!

---

### 📱 Mobile-First Design (Best Practice)

**Mobile-first** = write CSS for the **smallest screen first**, then add styles for larger screens.

```css
/* Base styles — for mobile */
.card { width: 100%; padding: 16px; }

/* Tablet and up */
@media (min-width: 768px) {
    .card { width: 50%; }
}

/* Desktop and up */
@media (min-width: 1024px) {
    .card { width: 33.33%; }
}
```

---

### 📐 Media Queries

```css
/* Common Breakpoints */
/* Mobile: < 640px (default — no query needed) */
@media (min-width: 640px)  { /* sm: small tablets */ }
@media (min-width: 768px)  { /* md: tablets */ }
@media (min-width: 1024px) { /* lg: laptops */ }
@media (min-width: 1280px) { /* xl: desktops */ }
@media (min-width: 1536px) { /* 2xl: wide screens */ }

/* Other features */
@media (orientation: portrait)  { ... }   /* Phone upright */
@media (orientation: landscape) { ... }   /* Phone sideways */

/* Dark mode support */
@media (prefers-color-scheme: dark) {
    body { background: #1a1a2e; color: #eee; }
}

/* Reduced motion (accessibility!) */
@media (prefers-reduced-motion: reduce) {
    * { animation: none !important; transition: none !important; }
}
```

---

### 📏 Fluid Layouts

```css
/* Fixed (not responsive) ❌ */
.container { width: 960px; }

/* Fluid (responsive ✅) */
.container {
    width: 90%;           /* 90% of viewport */
    max-width: 1200px;    /* But never wider than 1200px */
    margin: 0 auto;       /* Center it */
}

/* Fluid images */
img { max-width: 100%; height: auto; display: block; }
```

---

### 🔤 Responsive Typography

```css
/* clamp(minimum, preferred, maximum) */
h1 { font-size: clamp(1.5rem, 5vw, 3rem); }
p  { font-size: clamp(1rem, 2.5vw, 1.2rem); }

/* Media queries approach */
h1 { font-size: 1.8rem; }
@media (min-width: 768px)  { h1 { font-size: 2.5rem; } }
@media (min-width: 1024px) { h1 { font-size: 3.5rem; } }
```

---

### 📱 Common Responsive Patterns

```css
/* 1. Stack to Row */
.container { display: flex; flex-direction: column; }
@media (min-width: 768px) {
    .container { flex-direction: row; }
}

/* 2. Hide on Mobile */
.desktop-only { display: none; }
@media (min-width: 1024px) { .desktop-only { display: block; } }

/* 3. Hamburger to Full Nav */
.nav-links { display: none; }
.hamburger { display: block; }
@media (min-width: 768px) {
    .nav-links { display: flex; gap: 20px; }
    .hamburger { display: none; }
}

/* 4. Auto-Responsive Card Grid — no media queries! */
.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 24px;
}
```

---

### ✅ Key Takeaways

- Always add the `<meta name="viewport">` tag — without it, responsive CSS won't work on mobile!
- Write **mobile-first** CSS, then use `min-width` media queries.
- Use **relative units** (`%`, `rem`, `vw`) instead of fixed `px` for flexible layouts.
- Use `clamp()` for fluid typography.
- Use `repeat(auto-fit, minmax())` for automatically responsive grids.

---

## CSS 09 — Animations & Transitions

### ⚡ Part 1: CSS Transitions

A **transition** smoothly animates a property change from one state to another.

```css
/* Syntax */
element { transition: property duration timing-function delay; }

/* Basic Example */
.btn {
    background: blue;
    transition: background 0.3s ease;
}
.btn:hover { background: darkblue; }  /* Animated! */

/* Multiple properties */
.box {
    transition: background-color 0.3s ease, transform 0.2s ease;
}

/* Timing functions */
transition: all 0.3s linear;       /* Constant speed */
transition: all 0.3s ease;         /* Slow→fast→slow (default) */
transition: all 0.3s ease-in;      /* Slow start */
transition: all 0.3s ease-out;     /* Slow end */
transition: all 0.3s ease-in-out;  /* Slow start and end */
transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55); /* Custom bounce! */
```

#### Practical Transition Examples:
```css
/* Smooth card hover — float up */
.card {
    transform: translateY(0);
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.card:hover {
    transform: translateY(-5px);
    box-shadow: 0 12px 30px rgba(0,0,0,0.15);
}

/* Button press effect */
.btn {
    transform: scale(1);
    transition: transform 0.1s ease, background 0.2s ease;
}
.btn:hover  { background: darkblue; }
.btn:active { transform: scale(0.97); }

/* Animated underline on hover */
.nav-link::after {
    content: '';
    position: absolute;
    bottom: -2px;
    left: 0;
    width: 0%;
    height: 2px;
    background: blue;
    transition: width 0.3s ease;
}
.nav-link:hover::after { width: 100%; }
```

---

### 🔄 Part 2: CSS Transform

`transform` moves, scales, rotates, or skews an element **without affecting the layout**.

```css
/* Translate (move) */
transform: translateX(50px);         /* Move right */
transform: translateY(-20px);        /* Move up */
transform: translate(50px, -20px);   /* Move both */

/* Scale (resize) */
transform: scale(1.2);   /* 20% bigger */
transform: scale(0.9);   /* 10% smaller */

/* Rotate */
transform: rotate(45deg);   /* 45° clockwise */
transform: rotate(-90deg);  /* 90° counter-clockwise */

/* Skew */
transform: skewX(15deg);
transform: skewY(10deg);

/* Combining */
transform: translateY(-5px) scale(1.05) rotate(2deg);

/* 3D */
transform: perspective(500px) rotateY(30deg);
```

---

### 🎬 Part 3: CSS Keyframe Animations

For **complex, multi-step animations**.

```css
/* 1. Define the animation */
@keyframes fadeIn {
    from { opacity: 0; }
    to   { opacity: 1; }
}

/* With percentage steps */
@keyframes slideUp {
    0%   { opacity: 0; transform: translateY(30px); }
    100% { opacity: 1; transform: translateY(0); }
}

/* 2. Apply it */
.page-load { animation: fadeIn 0.5s ease forwards; }
.hero-text  { animation: slideUp 0.8s ease-out forwards; }
```

#### Animation Properties:
```css
.element {
    animation-name: slideIn;
    animation-duration: 1s;
    animation-timing-function: ease;
    animation-delay: 0.5s;
    animation-iteration-count: infinite;  /* or a number */
    animation-direction: alternate;       /* normal, reverse, alternate */
    animation-fill-mode: forwards;        /* Keep final state */

    /* Shorthand */
    animation: slideIn 1s ease 0.5s 1 normal forwards;
}
```

#### Real-World Keyframe Examples:
```css
/* Spinning Loader */
@keyframes spin {
    from { transform: rotate(0deg); }
    to   { transform: rotate(360deg); }
}
.spinner {
    width: 40px; height: 40px;
    border: 4px solid #eee;
    border-top-color: #4a90d9;
    border-radius: 50%;
    animation: spin 1s linear infinite;
}

/* Pulsing Badge */
@keyframes pulse {
    0%, 100% { transform: scale(1); }
    50%       { transform: scale(1.1); }
}
.badge { animation: pulse 2s ease-in-out infinite; }

/* Bounce */
@keyframes bounce {
    0%, 100% { transform: translateY(0); }
    50%       { transform: translateY(-30px); }
}
.ball { animation: bounce 1s infinite; }

/* Shake (for form errors) */
@keyframes shake {
    0%, 100% { transform: translateX(0); }
    20%       { transform: translateX(-10px); }
    40%       { transform: translateX(10px); }
    60%       { transform: translateX(-6px); }
    80%       { transform: translateX(6px); }
}
.error { animation: shake 0.5s ease; }

/* Skeleton Loader Shimmer */
@keyframes shimmer {
    0%   { background-position: -200% 0; }
    100% { background-position: 200% 0; }
}
.skeleton {
    background: linear-gradient(90deg, #eee 25%, #f5f5f5 50%, #eee 75%);
    background-size: 200% 100%;
    animation: shimmer 1.5s infinite;
}
```

---

### ✅ Key Takeaways

| Property | What it does |
|---------|-------------|
| `transition` | Animate property changes on state change |
| `transform` | Move, scale, rotate elements |
| `animation` | Apply keyframe animations |
| `@keyframes` | Define animation steps |

- **Transitions** = smooth changes between two states (hover effects).
- **Transform** = move/scale/rotate without affecting page layout.
- **Keyframes** = complex multi-step animations.
- Always use `transition: transform, opacity` (not `all`) for **performance**.
- Respect user preferences: `@media (prefers-reduced-motion: reduce)` disables animations.

---

## 🛠️ Standard CSS Reset / Starter Template

Use this at the top of every project:

```css
/* ===== CSS Reset & Base Styles ===== */
*, *::before, *::after {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

html {
    font-size: 16px;
    scroll-behavior: smooth;
}

body {
    font-family: 'Inter', 'Segoe UI', Arial, sans-serif;
    line-height: 1.6;
    color: #333;
    background-color: #fff;
}

img, video {
    max-width: 100%;
    height: auto;
    display: block;
}

a { color: inherit; text-decoration: none; }

button { cursor: pointer; border: none; background: none; }

ul, ol { list-style: none; }

/* CSS Variables */
:root {
    --primary: hsl(220, 80%, 55%);
    --primary-dark: hsl(220, 80%, 40%);
    --text: hsl(0, 0%, 15%);
    --text-muted: hsl(0, 0%, 45%);
    --bg: hsl(0, 0%, 98%);
    --border: hsl(0, 0%, 85%);
    --radius: 8px;
    --shadow: 0 4px 15px rgba(0,0,0,0.08);
}

/* Utility Classes */
.container { width: 90%; max-width: 1200px; margin: 0 auto; }
.text-center { text-align: center; }
.hidden { display: none; }
.visually-hidden { position: absolute; width: 1px; height: 1px; overflow: hidden; clip: rect(0,0,0,0); }
```

---

## 📚 Quick Reference: HTML Tags Cheat Sheet

| Tag | Purpose | Self-Closing? |
|-----|---------|:---:|
| `<!DOCTYPE html>` | Document type declaration | ✅ |
| `<html>` | Root element | ❌ |
| `<head>` | Metadata container | ❌ |
| `<body>` | Visible content | ❌ |
| `<h1>` – `<h6>` | Headings | ❌ |
| `<p>` | Paragraph | ❌ |
| `<br>` | Line break | ✅ |
| `<hr>` | Horizontal rule | ✅ |
| `<strong>` | Bold + important | ❌ |
| `<em>` | Italic + emphasis | ❌ |
| `<mark>` | Highlighted text | ❌ |
| `<del>` / `<ins>` | Deleted / Inserted text | ❌ |
| `<a href="">` | Hyperlink | ❌ |
| `<img src="" alt="">` | Image | ✅ |
| `<audio>` | Audio player | ❌ |
| `<video>` | Video player | ❌ |
| `<ul>` / `<ol>` / `<li>` | Unordered/Ordered list | ❌ |
| `<dl>` / `<dt>` / `<dd>` | Description list | ❌ |
| `<table>` / `<tr>` / `<th>` / `<td>` | Table | ❌ |
| `<form>` | Form container | ❌ |
| `<input>` | Form input field | ✅ |
| `<label>` | Input label | ❌ |
| `<textarea>` | Multi-line text input | ❌ |
| `<select>` / `<option>` | Dropdown | ❌ |
| `<button>` | Button | ❌ |
| `<header>` | Page/section header | ❌ |
| `<nav>` | Navigation | ❌ |
| `<main>` | Main content | ❌ |
| `<section>` | Thematic section | ❌ |
| `<article>` | Self-contained content | ❌ |
| `<aside>` | Sidebar / related content | ❌ |
| `<footer>` | Page/section footer | ❌ |
| `<figure>` / `<figcaption>` | Image with caption | ❌ |
| `<div>` | Generic block container | ❌ |
| `<span>` | Generic inline container | ❌ |
| `<meta>` | Metadata | ✅ |
| `<link>` | External resource (CSS) | ✅ |
| `<script>` | JavaScript | ❌ |

---

## 💡 Study Tips

1. **Type, don't copy** — Manually typing code builds muscle memory.
2. **Open every example in a browser** — See the output immediately.
3. **Break things on purpose** — Change values and see what happens.
4. **Build something** — After each section, apply it to a small project.
5. **Use MDN** — The [MDN Web Docs](https://developer.mozilla.org) is the best reference.
6. **Use Chrome DevTools** — Right-click → Inspect to see and edit live CSS.

---

## 🛠️ Tools to Install

| Tool | Purpose | Download |
|------|---------|----------|
| **VS Code** | Code editor | [code.visualstudio.com](https://code.visualstudio.com) |
| **Google Chrome** | Browser for testing | [google.com/chrome](https://google.com/chrome) |
| **Live Server** (VS Code extension) | Auto-refresh browser on save | VS Code Extensions Panel |
| **Prettier** (VS Code extension) | Auto-format code | VS Code Extensions Panel |

---

*Happy Learning! 🎉 — Built from your frontend-notes by Antigravity AI*
