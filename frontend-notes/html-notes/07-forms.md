# 07 — Forms (The Most Important HTML Topic!)

---

## 📌 Why Forms?

Forms are how users **send data** to a website. Every login page, contact form, checkout, and search box uses HTML forms.

---

## 🏗️ The `<form>` Tag

```html
<form action="/submit" method="POST">
    <!-- form inputs go here -->
</form>
```

### Key Attributes:
| Attribute | Purpose |
|-----------|---------|
| `action` | URL where form data is sent (your backend) |
| `method` | How data is sent: `GET` (in URL) or `POST` (hidden in request body) |

> 💡 Use `method="POST"` for sensitive data like passwords. Use `method="GET"` for search forms.

---

## 🔤 Input Types: `<input type="...">`

The `<input>` tag is the most versatile form element. Its `type` attribute changes its behavior completely.

### All Common Input Types:

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

<!-- Radio buttons (only one can be selected in a group) -->
<input type="radio" id="male" name="gender" value="male">
<label for="male">Male</label>
<input type="radio" id="female" name="gender" value="female">
<label for="female">Female</label>

<!-- Hidden field (not visible but submitted with form) -->
<input type="hidden" name="user_id" value="12345">

<!-- Search field -->
<input type="search" placeholder="Search...">

<!-- Submit button -->
<input type="submit" value="Submit Form">

<!-- Reset button (clears the form) -->
<input type="reset" value="Clear All">
```

---

## 🏷️ The `<label>` Tag

`<label>` connects text to an input. Always use it for **accessibility** — clicking the label focuses the input.

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

## 📝 Textarea: `<textarea>`

For multi-line text input (like a message or bio).

```html
<label for="message">Your Message:</label>
<textarea id="message" name="message" rows="5" cols="40" placeholder="Write your message here..."></textarea>
```

- `rows` — height (number of visible rows)
- `cols` — width (number of visible columns)
- Controlled better with CSS: `width: 100%; height: 150px;`

---

## 📋 Dropdown: `<select>`

Creates a dropdown menu for selecting one (or multiple) options.

```html
<label for="country">Select Country:</label>
<select id="country" name="country">
    <option value="">-- Choose a Country --</option>
    <option value="np">Nepal</option>
    <option value="in">India</option>
    <option value="us">United States</option>
    <option value="uk">United Kingdom</option>
</select>

<!-- Group options with <optgroup> -->
<select name="skill">
    <optgroup label="Frontend">
        <option value="html">HTML</option>
        <option value="css">CSS</option>
    </optgroup>
    <optgroup label="Backend">
        <option value="nodejs">Node.js</option>
        <option value="php">PHP</option>
    </optgroup>
</select>

<!-- Allow multiple selections (hold Ctrl/Cmd to select multiple) -->
<select name="languages" multiple>
    <option value="html">HTML</option>
    <option value="css">CSS</option>
    <option value="js">JavaScript</option>
</select>
```

---

## 🔘 The `<button>` Tag

More flexible than `<input type="submit">`.

```html
<!-- Submit button (submits the form) -->
<button type="submit">Submit</button>

<!-- Reset button (clears the form) -->
<button type="reset">Clear</button>

<!-- Regular button (use with JavaScript) -->
<button type="button" onclick="alert('Clicked!')">Click Me</button>

<!-- Button with HTML inside -->
<button type="submit">
    🚀 Send Message
</button>
```

---

## 🧪 Full Registration Form Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Registration Form</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 500px; margin: 40px auto; padding: 0 20px; }
        label { display: block; margin-top: 15px; font-weight: bold; }
        input, select, textarea { width: 100%; padding: 8px; margin-top: 5px; box-sizing: border-box; border: 1px solid #ccc; border-radius: 4px; }
        button { margin-top: 20px; padding: 10px 25px; background: #4a90d9; color: white; border: none; border-radius: 4px; cursor: pointer; }
        button:hover { background: #357abd; }
    </style>
</head>
<body>

    <h1>Create an Account</h1>

    <form action="/register" method="POST">

        <!-- Text inputs -->
        <label for="fname">First Name:</label>
        <input type="text" id="fname" name="first_name" placeholder="Aarav" required>

        <label for="lname">Last Name:</label>
        <input type="text" id="lname" name="last_name" placeholder="Shah" required>

        <!-- Email -->
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" placeholder="aarav@example.com" required>

        <!-- Password -->
        <label for="pass">Password:</label>
        <input type="password" id="pass" name="password" minlength="8" required>

        <!-- Number -->
        <label for="age">Age:</label>
        <input type="number" id="age" name="age" min="18" max="100">

        <!-- Date -->
        <label for="dob">Date of Birth:</label>
        <input type="date" id="dob" name="dob">

        <!-- Dropdown -->
        <label for="country">Country:</label>
        <select id="country" name="country">
            <option value="np">Nepal</option>
            <option value="in">India</option>
            <option value="us">United States</option>
        </select>

        <!-- Radio -->
        <label>Gender:</label>
        <input type="radio" id="m" name="gender" value="male">
        <label for="m" style="display:inline; font-weight:normal;">Male</label>
        <input type="radio" id="f" name="gender" value="female">
        <label for="f" style="display:inline; font-weight:normal;">Female</label>

        <!-- Textarea -->
        <label for="bio">Bio:</label>
        <textarea id="bio" name="bio" rows="4" placeholder="Tell us about yourself..."></textarea>

        <!-- Checkbox -->
        <div style="margin-top: 15px;">
            <input type="checkbox" id="terms" name="terms" required>
            <label for="terms" style="display:inline; font-weight:normal;">
                I agree to the <a href="#">Terms and Conditions</a>
            </label>
        </div>

        <!-- Submit -->
        <button type="submit">Create Account</button>
        <button type="reset">Clear Form</button>

    </form>

</body>
</html>
```

---

## 🔍 Important Input Attributes

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

## ✅ Key Takeaways

- Use `<label>` with every `<input>` for accessibility.
- Choose the correct `type` for each input — it helps with mobile keyboards and validation.
- Use `required` to prevent empty submissions.
- Use `name` attribute — it's how the server receives the data.
- Use `POST` for sensitive data, `GET` for searches.

---

> ➡️ **Next:** `08-semantic-html.md` — Writing meaningful, accessible HTML.
