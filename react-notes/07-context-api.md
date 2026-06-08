# 07 — Context API (Global State)

---

## 📌 What is Prop Drilling?

**Prop drilling** happens when you pass data through many layers of components just to get it to a deeply nested child — even though the middle components don't use it.

```
App (has theme: "dark")
  └─ Layout (passes theme down)
       └─ Sidebar (passes theme down)
            └─ Button (finally uses theme) ← only this needs it!
```

This becomes messy and hard to maintain as the app grows.

---

## 🌐 The Context API — Solution to Prop Drilling

**Context** allows you to share data **globally** — any component in the tree can read it directly, no matter how deeply nested.

```
Context (theme: "dark")
  ↓ (any component can access directly)
Button reads from Context — no prop drilling!
```

---

## ⚙️ How to Use Context — 3 Steps

### Step 1 — Create the Context

```jsx
// src/context/ThemeContext.jsx
import { createContext } from 'react';

const ThemeContext = createContext('light');  // 'light' is the default value

export default ThemeContext;
```

---

### Step 2 — Provide the Context (wrap your app)

```jsx
// src/App.jsx
import { useState } from 'react';
import ThemeContext from './context/ThemeContext';
import Navbar from './components/Navbar';
import Content from './components/Content';

function App() {
  const [theme, setTheme] = useState('light');

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Navbar />
      <Content />
    </ThemeContext.Provider>
  );
}
```

---

### Step 3 — Consume the Context (in any child)

```jsx
// src/components/Navbar.jsx
import { useContext } from 'react';
import ThemeContext from '../context/ThemeContext';

function Navbar() {
  const { theme, setTheme } = useContext(ThemeContext);

  return (
    <nav style={{ background: theme === 'dark' ? '#1a1a1a' : '#ffffff' }}>
      <h1>My App</h1>
      <button onClick={() => setTheme(theme === 'dark' ? 'light' : 'dark')}>
        {theme === 'dark' ? '☀️ Light Mode' : '🌙 Dark Mode'}
      </button>
    </nav>
  );
}
```

---

## 🏗️ Best Practice — Context with Custom Hook

Wrap your context in a **custom hook** for cleaner usage:

```jsx
// src/context/ThemeContext.jsx
import { createContext, useContext, useState } from 'react';

const ThemeContext = createContext(null);

// Provider component
export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');

  function toggleTheme() {
    setTheme(prev => prev === 'light' ? 'dark' : 'light');
  }

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

// Custom hook for consuming the context
export function useTheme() {
  const context = useContext(ThemeContext);
  if (!context) throw new Error('useTheme must be used inside ThemeProvider');
  return context;
}
```

**Usage in App.jsx:**
```jsx
import { ThemeProvider } from './context/ThemeContext';

function App() {
  return (
    <ThemeProvider>
      <Navbar />
      <Main />
    </ThemeProvider>
  );
}
```

**Usage in any component:**
```jsx
import { useTheme } from '../context/ThemeContext';

function Button() {
  const { theme, toggleTheme } = useTheme();
  return <button onClick={toggleTheme}>Current: {theme}</button>;
}
```

---

## 🔐 Auth Context — Real-World Example

```jsx
// src/context/AuthContext.jsx
import { createContext, useContext, useState } from 'react';

const AuthContext = createContext(null);

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);  // null = not logged in

  function login(userData) {
    setUser(userData);
    localStorage.setItem('user', JSON.stringify(userData));
  }

  function logout() {
    setUser(null);
    localStorage.removeItem('user');
  }

  return (
    <AuthContext.Provider value={{ user, login, logout, isLoggedIn: !!user }}>
      {children}
    </AuthContext.Provider>
  );
}

export function useAuth() {
  return useContext(AuthContext);
}
```

**Protecting routes:**
```jsx
import { useAuth } from '../context/AuthContext';

function Dashboard() {
  const { user, logout, isLoggedIn } = useAuth();

  if (!isLoggedIn) return <p>Please log in to view this page.</p>;

  return (
    <div>
      <h1>Welcome, {user.name}!</h1>
      <button onClick={logout}>Log Out</button>
    </div>
  );
}
```

---

## 📊 When to Use Context vs Props

| Situation | Use Props | Use Context |
|-----------|----------|------------|
| Data only needed by 1-2 components | ✅ | — |
| Data shared by many components | — | ✅ |
| Passing data 3+ levels deep | — | ✅ |
| Theme (dark/light mode) | — | ✅ |
| User authentication | — | ✅ |
| Language / Locale | — | ✅ |
| Frequently changing data | ✅ (too many re-renders with context) | — |

---

## ⚠️ Context Gotchas

1. **Re-renders:** All consumers re-render when the context value changes — split contexts by concern.
2. **Not a replacement for all state:** Local component state is still better for component-specific data.
3. **Not suitable for high-frequency updates** (e.g., mouse position) — use a dedicated library like Zustand.

---

## ✅ Key Takeaways

- **Prop drilling** = passing data through intermediate components — painful to maintain.
- **Context** provides a way to share data globally without prop drilling.
- Use `createContext` → `Provider` → `useContext` pattern.
- **Wrap context in a custom hook** (`useTheme`, `useAuth`) for cleaner code.
- Best used for: theme, auth, language, preferences — data that changes infrequently.

---

## 🏋️ Practice Tasks

### Task 1 — Dark Mode
Build a theme context that provides `theme` and `toggleTheme`.
- Apply `theme` to the root `<div>` to switch CSS classes.
- A toggle button in the Navbar switches between dark and light mode.

---

### Task 2 — Language Switcher
Create a language context with translations for English and Nepali.
- Switch between languages using a button.
- All text on the page updates instantly.

---

### Task 3 — Shopping Cart Context
Create a cart context with:
- `cartItems` — list of items in cart
- `addToCart(item)` — add item
- `removeFromCart(id)` — remove item
- `cartTotal` — calculated total price

Display a cart icon in the Navbar with the item count badge.

---

> ➡️ **Next:** `08-react-router.md` — Build multi-page apps with React Router.
