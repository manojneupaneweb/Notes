# 01 — Introduction to React

---

## 📌 What is React?

**React** is a **JavaScript library for building user interfaces**, created by Facebook (Meta) in 2013.

- It lets you build **reusable UI components** — pieces of the page like buttons, cards, navbars.
- React makes it easy to create **fast, interactive** web applications.
- Instead of manipulating the DOM manually, you **describe what the UI should look like**, and React handles the rest.

> 💡 **Analogy:** If HTML is the blueprint, and vanilla JS is the construction crew, React is a **smart construction manager** — you tell it what to build, it figures out the most efficient way to do it.

---

## 🌐 Why Use React?

| Problem with Plain JS | React Solution |
|----------------------|----------------|
| Manually updating the DOM is slow & error-prone | React updates only what changed (Virtual DOM) |
| Code becomes messy as the app grows | Components keep code organized and reusable |
| Hard to share logic between pages | Share components across the entire app |
| State management is complex | React has built-in state with hooks |

---

## ⚙️ How React Works — The Virtual DOM

React uses a **Virtual DOM** — a lightweight copy of the real DOM kept in memory.

```
1. You update state (data changes)
2. React re-renders the Virtual DOM
3. React compares old vs new Virtual DOM (diffing)
4. React only updates the parts of the real DOM that changed
```

> ✅ This is called **reconciliation** — it's what makes React so fast.

---

## 🛠️ Setting Up a React Project

### Option 1 — Vite (Recommended ✅)

The fastest way to start a React project today:

```bash
npm create vite@latest my-app -- --template react
cd my-app
npm install
npm run dev
```

### Option 2 — Create React App (CRA) — Older, Slower

```bash
npx create-react-app my-app
cd my-app
npm start
```

> ⚠️ **Prefer Vite** — CRA is slow and no longer actively maintained.

---

## 📁 React Project Structure (Vite)

```
my-app/
├── public/               ← Static assets (favicon, etc.)
├── src/
│   ├── App.jsx           ← Main component
│   ├── main.jsx          ← Entry point (renders App)
│   └── index.css         ← Global styles
├── index.html            ← The single HTML page
├── package.json          ← Dependencies & scripts
└── vite.config.js        ← Vite configuration
```

> 💡 React apps have a **single HTML file** (`index.html`). React dynamically renders all content into a `<div id="root">`.

---

## 📄 Your First React App

**index.html:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>My React App</title>
</head>
<body>
  <div id="root"></div>   <!-- React mounts here -->
  <script type="module" src="/src/main.jsx"></script>
</body>
</html>
```

**src/main.jsx:**
```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

// Mount the App component into the #root div
ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

**src/App.jsx:**
```jsx
function App() {
  return (
    <div>
      <h1>Hello, React! 👋</h1>
      <p>My first React app.</p>
    </div>
  );
}

export default App;
```

---

## 🔤 What is JSX?

**JSX** (JavaScript XML) is a syntax extension that lets you write HTML-like code inside JavaScript.

```jsx
// JSX:
const element = <h1>Hello, World!</h1>;

// What it compiles to (behind the scenes):
const element = React.createElement('h1', null, 'Hello, World!');
```

### JSX Rules:
1. **Return one root element** — wrap multiple elements in a `<div>` or `<>` (Fragment)
2. **Close all tags** — `<br />`, `<img />`, `<input />`
3. **Use `className`** instead of `class` (because `class` is a JS keyword)
4. **Use `htmlFor`** instead of `for` on labels
5. **JavaScript goes in `{}`** — `{name}`, `{2 + 2}`, `{isLoggedIn ? 'Yes' : 'No'}`

```jsx
function App() {
  const name = "Manoj";
  const age = 20;
  const isStudent = true;

  return (
    <>
      <h1>Hello, {name}!</h1>
      <p>Age: {age}</p>
      <p>Status: {isStudent ? "Student" : "Professional"}</p>
      <p>Next year: {age + 1}</p>
    </>
  );
}
```

---

## 📊 React vs Vanilla JavaScript

| Feature | Vanilla JS | React |
|---------|-----------|-------|
| DOM Updates | Manual (`innerHTML`, `textContent`) | Automatic (Virtual DOM) |
| Code Organization | Functions & files | Components |
| State Management | Variables + manual re-render | `useState` hook |
| Reusability | Copy-paste code | Import & reuse components |
| Ecosystem | Browser built-ins | Huge library ecosystem |

---

## ✅ Key Takeaways

- React is a **UI library** — it handles the view layer of your app.
- React uses a **Virtual DOM** to efficiently update the real DOM.
- **JSX** lets you write HTML-like syntax inside JavaScript.
- Use **Vite** to create new React projects (`npm create vite@latest`).
- React apps have a **single HTML page** — everything is rendered by JavaScript.

---

## 🏋️ Practice Tasks

### Task 1 — Create Your First React App
1. Run: `npm create vite@latest my-first-react -- --template react`
2. Open `src/App.jsx` and change the content to show:
   - A heading with your name
   - Your age
   - Your favorite programming language
3. Run `npm run dev` and view it in the browser.

---

### Task 2 — JSX Expressions
In `App.jsx`, create variables for:
- `firstName`, `lastName`, `birthYear`
- Calculate and display `currentAge = 2025 - birthYear`
- Display a message: `"Hello, I am [firstName] [lastName] and I am [age] years old."`
- Use a ternary to show `"Adult"` or `"Minor"` based on age.

---

### Task 3 — JSX Rules Practice
Fix the bugs in this JSX code:
```jsx
function App() {
  return (
    <div class="container">
      <h1>My App
      <p>Welcome to <b>React</b>
      <img src="logo.png">
      <label for="name">Your Name:</label>
      <input type="text" id="name">
    </div>
  );
}
```

---

> ➡️ **Next:** `02-components.md` — Learn how to build and use React components.
