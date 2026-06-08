# 02 — React Components

---

## 📌 What is a Component?

A **component** is a **reusable, self-contained piece of UI**. Think of it like a custom HTML tag that you define yourself.

- Every part of a React app is a component: navbar, button, card, form, footer.
- Components can be **nested** inside each other to build complex UIs.
- Components receive **props** (inputs) and return **JSX** (output).

> 💡 **Analogy:** Components are like LEGO bricks — you build small, reusable pieces and snap them together to make anything.

---

## 🧱 Types of Components

### 1. Function Components ✅ (Modern — Use This)

```jsx
function Greeting() {
  return <h1>Hello, World!</h1>;
}
```

### 2. Class Components ❌ (Old — Avoid)

```jsx
// Old way — you'll see this in legacy code but don't write new code like this
class Greeting extends React.Component {
  render() {
    return <h1>Hello, World!</h1>;
  }
}
```

> ✅ **Always use function components** — class components are outdated since React 16.8 introduced Hooks.

---

## 📦 Creating and Using Components

### Step 1 — Create a component file

**src/components/Navbar.jsx:**
```jsx
function Navbar() {
  return (
    <nav>
      <h1>My Website</h1>
      <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About</a></li>
        <li><a href="/contact">Contact</a></li>
      </ul>
    </nav>
  );
}

export default Navbar;
```

### Step 2 — Import and use it

**src/App.jsx:**
```jsx
import Navbar from './components/Navbar';

function App() {
  return (
    <div>
      <Navbar />
      <h2>Welcome to my site!</h2>
    </div>
  );
}

export default App;
```

> 💡 **Convention:** Component names always start with an **uppercase letter** (`Navbar`, not `navbar`). Lowercase names are treated as regular HTML tags.

---

## 📁 Component File Organization

```
src/
├── App.jsx
├── main.jsx
└── components/
    ├── Navbar.jsx
    ├── Footer.jsx
    ├── Button.jsx
    └── Card.jsx
```

---

## 🎁 Props — Passing Data to Components

**Props** (properties) are how you pass data **from a parent component to a child component**.

### Passing Props:

```jsx
// Parent passes data as attributes:
function App() {
  return (
    <div>
      <Greeting name="Manoj" age={20} />
      <Greeting name="Sita"  age={22} />
      <Greeting name="Ram"   age={19} />
    </div>
  );
}
```

### Receiving Props:

```jsx
// Child receives props as a parameter:
function Greeting(props) {
  return (
    <div>
      <h2>Hello, {props.name}!</h2>
      <p>Age: {props.age}</p>
    </div>
  );
}
```

### Destructuring Props (Cleaner ✅):

```jsx
function Greeting({ name, age }) {
  return (
    <div>
      <h2>Hello, {name}!</h2>
      <p>Age: {age}</p>
    </div>
  );
}
```

### Default Props:

```jsx
function Button({ text = "Click Me", color = "blue" }) {
  return <button style={{ backgroundColor: color }}>{text}</button>;
}

// Usage:
<Button />                          // Uses defaults: "Click Me", blue
<Button text="Submit" color="green" /> // Overrides both
```

---

## 🔄 Props vs State

| | Props | State |
|--|-------|-------|
| Who sets it? | Parent component | The component itself |
| Can it change? | ❌ Read-only (immutable) | ✅ Yes — triggers re-render |
| Purpose | Pass data down | Track changing data |

---

## 🧩 Component Composition

You can nest components inside each other — this is called **composition**.

```jsx
function Avatar({ name }) {
  return <img src={`https://api.dicebear.com/7.x/initials/svg?seed=${name}`} alt={name} />;
}

function UserCard({ name, role }) {
  return (
    <div className="card">
      <Avatar name={name} />
      <h3>{name}</h3>
      <p>{role}</p>
    </div>
  );
}

function App() {
  return (
    <div>
      <UserCard name="Manoj" role="Developer" />
      <UserCard name="Sita"  role="Designer"  />
    </div>
  );
}
```

---

## 👶 The `children` Prop

React passes everything between a component's **opening and closing tags** as `children`:

```jsx
function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}

// Usage — anything inside <Card>...</Card> becomes children:
function App() {
  return (
    <Card>
      <h2>My Title</h2>
      <p>This is card content passed as children!</p>
    </Card>
  );
}
```

---

## 📊 Component Summary

| Concept | Description |
|---------|-------------|
| Component | Reusable piece of UI returning JSX |
| Props | Data passed from parent to child (read-only) |
| Children | JSX nested inside component tags |
| Composition | Building UIs by nesting components |
| File convention | One component per file, PascalCase name |

---

## ✅ Key Takeaways

- Components are the **building blocks** of every React app.
- Always use **function components** (not class components).
- **Props** flow **down** from parent to child — they are **read-only**.
- Destructure props for cleaner code: `({ name, age })` instead of `(props)`.
- Use `children` prop to make flexible wrapper components.
- Keep components **small and focused** — one responsibility per component.

---

## 🏋️ Practice Tasks

### Task 1 — Build a Profile Card
Create a `ProfileCard` component that accepts:
- `name`, `role`, `location`, `bio`

Display them in a styled card. Render 3 different profile cards in `App.jsx`.

---

### Task 2 — Reusable Button
Create a `Button` component with:
- `text` prop (default: "Click")
- `color` prop (default: "#0070f3")
- `size` prop — `"small"`, `"medium"`, `"large"` (default: `"medium"`)

---

### Task 3 — Layout Wrapper
Create a `Section` component that:
- Accepts a `title` prop and `children`
- Wraps children in a `<section>` with a `<h2>` title above them

Use it like:
```jsx
<Section title="About Me">
  <p>I am a web developer...</p>
</Section>
```

---

> ➡️ **Next:** `03-state-and-hooks.md` — Learn how to make components interactive with state.
