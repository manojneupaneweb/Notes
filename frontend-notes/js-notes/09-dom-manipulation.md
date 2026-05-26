# 09 — DOM Manipulation

---

## 📌 What is the DOM?

The **DOM** (Document Object Model) is the browser's representation of your HTML page as a **tree of objects** that JavaScript can read and modify.

```
Document
└── html
    ├── head
    │   └── title: "My Page"
    └── body
        ├── h1: "Hello!"
        ├── p: "Welcome to my site."
        └── button: "Click Me"
```

> 💡 **Analogy:** The DOM is like a live map of your web page. JavaScript can use this map to find elements, change their content, style, or structure, and react to user actions.

---

## 🔍 Selecting Elements

```javascript
// By ID (returns single element or null):
const title = document.getElementById("main-title");

// By CSS selector (returns FIRST match):
const btn = document.querySelector(".btn");          // class
const box = document.querySelector("#container");    // id
const p   = document.querySelector("p");             // tag
const nav = document.querySelector("nav > a");       // nested selector

// By CSS selector (returns ALL matches as NodeList):
const allBtns = document.querySelectorAll(".btn");
const allLi   = document.querySelectorAll("ul li");

// Older methods (less used today):
document.getElementsByClassName("btn");  // HTMLCollection by class
document.getElementsByTagName("p");      // HTMLCollection by tag
```

### NodeList vs HTMLCollection:

```javascript
const items = document.querySelectorAll("li");  // NodeList
items.forEach(item => console.log(item.textContent));  // ✅ forEach works

const items2 = document.getElementsByTagName("li");  // HTMLCollection
// ❌ forEach doesn't work directly — convert to array first:
Array.from(items2).forEach(item => console.log(item.textContent));
```

---

## ✏️ Reading and Changing Content

```javascript
const heading = document.querySelector("h1");

// Read content:
heading.textContent  // Text only (no HTML tags)
heading.innerHTML    // HTML string (includes nested HTML)

// Write content:
heading.textContent = "New Title";           // sets plain text (safe ✅)
heading.innerHTML   = "<em>New Title</em>";  // sets HTML (⚠️ XSS risk if from user input)

// Input field value:
const input = document.querySelector("input");
input.value           // read the current value
input.value = "hello" // set the value
```

---

## 🎨 Changing Styles

```javascript
const box = document.querySelector(".box");

// Inline styles (camelCase property names):
box.style.color           = "red";
box.style.backgroundColor = "#333";
box.style.fontSize        = "24px";
box.style.display         = "none";     // hide element
box.style.display         = "block";    // show element

// Better approach: toggle CSS classes ✅
box.classList.add("active");           // add a class
box.classList.remove("active");        // remove a class
box.classList.toggle("active");        // add if missing, remove if present
box.classList.contains("active");      // returns true/false
box.classList.replace("old", "new");   // replace one class with another
```

---

## 🏗️ Creating and Inserting Elements

```javascript
// Create a new element:
const newParagraph = document.createElement("p");
newParagraph.textContent = "This was added by JavaScript!";
newParagraph.classList.add("highlight");

// Insert into the page:
document.body.appendChild(newParagraph);       // append to end of body

const container = document.querySelector("#container");
container.appendChild(newParagraph);           // append to container

// Insert before a specific element:
const reference = document.querySelector("h2");
document.body.insertBefore(newParagraph, reference);

// Modern insertion methods ✅ (more flexible):
container.append(newParagraph);          // append element or text
container.prepend(newParagraph);         // insert at start
reference.before(newParagraph);          // insert before reference
reference.after(newParagraph);           // insert after reference

// Insert raw HTML string:
container.insertAdjacentHTML("beforeend", "<p>Hello!</p>");
// Positions: 'beforebegin' | 'afterbegin' | 'beforeend' | 'afterend'
```

---

## 🗑️ Removing Elements

```javascript
const element = document.querySelector(".old-item");

// Modern way ✅:
element.remove();

// Older way (via parent):
element.parentElement.removeChild(element);
```

---

## 🎛️ Working with Attributes

```javascript
const img = document.querySelector("img");

// Read attribute:
img.getAttribute("src")   // "photo.jpg"
img.getAttribute("alt")   // "A photo"

// Set attribute:
img.setAttribute("src", "new-photo.jpg");
img.setAttribute("alt", "New description");

// Remove attribute:
img.removeAttribute("alt");

// Check if attribute exists:
img.hasAttribute("alt");  // true or false

// Direct property access (for common attributes):
img.src   // ✅ same as getAttribute("src")
img.alt   // ✅
img.href  // for links
```

---

## 🖱️ Event Handling

Events are things that happen in the browser: clicks, key presses, form submissions, mouse movement, etc.

```javascript
const button = document.querySelector("#my-btn");

// Add event listener ✅ (best practice):
button.addEventListener("click", function(event) {
  console.log("Button was clicked!");
  console.log(event);  // the event object
});

// Arrow function (shorter):
button.addEventListener("click", (e) => {
  console.log("Clicked!", e.target); // e.target = the clicked element
});
```

### Common Events:

| Event | When it fires |
|-------|--------------|
| `click` | User clicks an element |
| `dblclick` | Double click |
| `mouseover` | Mouse enters element |
| `mouseout` | Mouse leaves element |
| `keydown` | Key is pressed down |
| `keyup` | Key is released |
| `keypress` | Key is held (deprecated) |
| `input` | Input field value changes |
| `change` | Input loses focus with new value |
| `submit` | Form is submitted |
| `focus` | Element gains focus |
| `blur` | Element loses focus |
| `load` | Page or image finishes loading |
| `DOMContentLoaded` | HTML fully parsed |
| `scroll` | User scrolls |
| `resize` | Window is resized |

### The Event Object:

```javascript
document.addEventListener("click", (e) => {
  e.target              // element that was clicked
  e.currentTarget       // element the listener is attached to
  e.type                // "click"
  e.clientX / e.clientY // mouse coordinates

  e.preventDefault()    // stop default browser behavior (e.g., form submission)
  e.stopPropagation()   // stop event bubbling up
});

// Keyboard event:
document.addEventListener("keydown", (e) => {
  e.key      // "Enter", "Escape", "ArrowUp", etc.
  e.code     // "Enter", "KeyA", etc.
  e.ctrlKey  // true if Ctrl is held
  e.shiftKey // true if Shift is held
});
```

### Event Delegation (Best Practice for Dynamic Elements):

```javascript
// Instead of adding listeners to each item...
// Add ONE listener to the parent ✅
document.querySelector("ul").addEventListener("click", (e) => {
  if (e.target.tagName === "LI") {
    console.log("Clicked on:", e.target.textContent);
    e.target.classList.toggle("selected");
  }
});
```

---

## 🌟 Practical Example — Toggle Dark Mode

```javascript
const toggle = document.querySelector("#dark-mode-btn");

toggle.addEventListener("click", () => {
  document.body.classList.toggle("dark");
});
```

```css
.dark {
  background-color: #1a1a1a;
  color: #ffffff;
}
```

---

## 🌟 Practical Example — Dynamic List

```javascript
const input  = document.querySelector("#task-input");
const addBtn = document.querySelector("#add-btn");
const ul     = document.querySelector("#task-list");

addBtn.addEventListener("click", () => {
  const text = input.value.trim();
  if (!text) return;   // do nothing if empty

  const li = document.createElement("li");
  li.textContent = text;

  // Delete button inside each list item:
  const deleteBtn = document.createElement("button");
  deleteBtn.textContent = "❌";
  deleteBtn.addEventListener("click", () => li.remove());

  li.appendChild(deleteBtn);
  ul.appendChild(li);
  input.value = "";    // clear input
});
```

---

## ✅ Key Takeaways

| Task | Code |
|------|------|
| Select 1 element | `document.querySelector("selector")` |
| Select all | `document.querySelectorAll("selector")` |
| Change text | `el.textContent = "..."` |
| Change HTML | `el.innerHTML = "..."` |
| Toggle class | `el.classList.toggle("class")` |
| Create element | `document.createElement("tag")` |
| Append element | `parent.appendChild(child)` |
| Remove element | `el.remove()` |
| Add event | `el.addEventListener("click", fn)` |
| Stop default | `e.preventDefault()` |

---

## 🏋️ Practice Tasks

### Task 1 — Background Color Changer
Create an HTML page with 3 buttons: 🔴 Red, 🟢 Green, 🔵 Blue.
When each button is clicked, change the `document.body` background color.
Add a 4th **"Reset"** button that sets background back to white.

```html
<!-- Starter HTML -->
<button id="btn-red">🔴 Red</button>
<button id="btn-green">🟢 Green</button>
<button id="btn-blue">🔵 Blue</button>
<button id="btn-reset">Reset</button>
```

---

### Task 2 — Click Counter
Build a counter app with:
- A `<p>` showing the current count (starts at 0)
- An **Increment** button (+1)
- A **Decrement** button (-1, minimum 0)
- A **Reset** button (back to 0)
- Change the count text color: green if > 0, red if 0

---

### Task 3 — Live Todo List
Build a working todo list:
1. Text input + "Add Task" button → adds `<li>` to a `<ul>`
2. Each `<li>` has a ✅ checkbox — clicking it toggles a `line-through` style
3. Each `<li>` has a 🗑️ delete button — clicking it removes that item
4. Show count: `"Tasks: 3 remaining"` (updates live)
5. Prevent adding empty tasks

---

> ➡️ **Next:** `10-async-javascript.md` — Fetching data and handling asynchronous code.
