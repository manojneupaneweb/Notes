# 04 — Links and Media

---

## 🔗 The Anchor Tag: `<a>`

The `<a>` (anchor) tag creates hyperlinks — clickable text that takes you to another page, file, or location.

### Basic Syntax:
```html
<a href="URL">Link Text</a>
```

### Examples:

```html
<!-- Link to an external website -->
<a href="https://www.google.com" >Go to Google</a>

<!-- Open the link in a NEW browser tab (best for external links) -->
<a href="https://www.youtube.com" target="_blank">Open YouTube in new tab</a>

<!-- Link to another page in the same project -->
<a href="about.html">About Page</a>

<!-- Link to a section on the SAME page using an ID -->
<a href="#contact">Jump to Contact Section</a>
<!-- The target section must have this ID: -->
<section id="contact">
  <h2>Contact Us</h2>
</section>

<!-- Email link — opens the user's email app -->
<a href="mailto:hello@example.com">Send me an email</a>

<!-- Phone link — opens the dialer on mobile -->
<a href="tel:+977-9800000000">Call Us</a>
```

### `target` Attribute:
| Value | Behavior |
|-------|---------|
| `_blank` | Opens in a new tab |
| `_self` | Opens in the same tab (default) |
| `_parent` | Opens in parent frame |
| `_top` | Opens in the full browser window |

> 💡 **Tip:** Always use `target="_blank"` for external links so users don't leave your site.

---

## 🖼️ The Image Tag: `<img>`

The `<img>` tag displays images. It is **self-closing** (no closing tag needed).

### Basic Syntax:
```html
<img src="image-path" alt="description" />
```

### Attributes:
| Attribute | Purpose |
|-----------|---------|
| `src` | The path/URL to the image |
| `alt` | Alternative text (shown if image fails to load; important for accessibility & SEO) |
| `width` | Set width in pixels |
| `height` | Set height in pixels |

### Examples:

```html
<!-- Image from the internet (URL) -->
<img src="https://picsum.photos/400/200" alt="A random photo" />

<!-- Image from your project folder -->
<img src="images/my-photo.jpg" alt="Profile photo of Alex" />

<!-- Image with size specified -->
<img src="logo.png" alt="Company Logo" width="150" height="75" />
```

> ⚠️ **NEVER skip the `alt` attribute!** It's required for accessibility and SEO.

---

## 🎵 Audio: `<audio>`

Embeds an audio player in the page.

```html
<audio controls>
    <source src="audio/song.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
</audio>
```

### Key Attributes:
| Attribute | Effect |
|-----------|--------|
| `controls` | Shows play/pause/volume controls |
| `autoplay` | Plays automatically on page load |
| `loop` | Repeats the audio forever |
| `muted` | Starts muted |

> ⚠️ **Autoplay Warning:** Most browsers block autoplay with sound. Use `autoplay muted` if needed.

---

## 🎬 Video: `<video>`

Embeds a video player in the page.

```html
<video width="640" height="360" controls>
    <source src="video/intro.mp4" type="video/mp4">
    Your browser does not support the video tag.
</video>
```

### Key Attributes:
| Attribute | Effect |
|-----------|--------|
| `controls` | Shows player controls |
| `autoplay` | Auto-plays when page loads |
| `loop` | Repeats video |
| `muted` | Starts muted (needed for autoplay in most browsers) |
| `poster` | Image shown before the video plays |

```html
<!-- Video with a thumbnail/poster image -->
<video width="640" height="360" controls poster="thumbnail.jpg">
    <source src="video/intro.mp4" type="video/mp4">
</video>

<!-- Auto-playing muted loop (common for background videos) -->
<video autoplay muted loop>
    <source src="background.mp4" type="video/mp4">
</video>
```

---

## 🧪 Full Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Links & Media Demo</title>
</head>
<body>

    <h1>Media Gallery</h1>

    <!-- Links -->
    <h2>Useful Links</h2>
    <p>
        <a href="https://developer.mozilla.org" target="_blank">MDN Web Docs</a> |
        <a href="mailto:contact@example.com">Email Us</a>
    </p>

    <!-- Image -->
    <h2>Featured Image</h2>
    <img src="https://picsum.photos/600/300" alt="A sample landscape photo" width="600" />

    <!-- Audio -->
    <h2>Sample Audio</h2>
    <audio controls>
        <source src="audio/sample.mp3" type="audio/mpeg">
        Your browser doesn't support audio.
    </audio>

    <!-- Video -->
    <h2>Sample Video</h2>
    <video width="600" controls>
        <source src="video/sample.mp4" type="video/mp4">
        Your browser doesn't support video.
    </video>

</body>
</html>
```

---

## ✅ Key Takeaways

| Tag | Purpose |
|-----|---------|
| `<a href="">` | Creates a clickable link |
| `<img src="" alt="">` | Embeds an image |
| `<audio controls>` | Embeds an audio player |
| `<video controls>` | Embeds a video player |

---

> ➡️ **Next:** `05-lists.md` — Ordered, unordered, and description lists.
