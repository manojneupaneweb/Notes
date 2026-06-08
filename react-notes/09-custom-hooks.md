# 09 — Custom Hooks

---

## 📌 What are Custom Hooks?

A **custom hook** is a regular JavaScript function that:
- Starts with `use` (e.g., `useFetch`, `useLocalStorage`)
- Can call other hooks inside it
- Lets you **extract and reuse stateful logic** across multiple components

> 💡 **Analogy:** Custom hooks are like utility functions, but for React logic. Instead of copy-pasting `useState` + `useEffect` patterns, you extract them into a reusable hook.

---

## 🏗️ When to Create a Custom Hook?

When you notice the same `useState` + `useEffect` pattern repeated in multiple components — extract it into a custom hook.

```
Without custom hook:       With custom hook:
───────────────────────    ─────────────────────────
UserPage.jsx               useUsers.js (custom hook)
  useState(users)    ──►     useState(users)
  useState(loading)          useState(loading)
  useEffect(fetch)           useEffect(fetch)
                             return { users, loading }
ProductPage.jsx            UserPage.jsx → useUsers()
  useState(users)    ──►   ProductPage.jsx → useUsers()
  useState(loading)        ✅ No duplication!
  useEffect(fetch)
```

---

## 1️⃣ `useFetch` — Fetching Data

```jsx
// src/hooks/useFetch.js
import { useState, useEffect } from 'react';

function useFetch(url) {
  const [data, setData]       = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError]     = useState(null);

  useEffect(() => {
    setLoading(true);
    setError(null);

    async function fetchData() {
      try {
        const response = await fetch(url);
        if (!response.ok) throw new Error(`HTTP error: ${response.status}`);
        const result = await response.json();
        setData(result);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    }

    fetchData();
  }, [url]);  // re-fetch when URL changes

  return { data, loading, error };
}

export default useFetch;
```

**Usage — much cleaner!**

```jsx
import useFetch from '../hooks/useFetch';

function UserList() {
  const { data: users, loading, error } = useFetch('https://jsonplaceholder.typicode.com/users');

  if (loading) return <p>Loading...</p>;
  if (error)   return <p>Error: {error}</p>;

  return (
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  );
}
```

---

## 2️⃣ `useLocalStorage` — Persistent State

```jsx
// src/hooks/useLocalStorage.js
import { useState } from 'react';

function useLocalStorage(key, initialValue) {
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch {
      return initialValue;
    }
  });

  function setValue(value) {
    try {
      setStoredValue(value);
      localStorage.setItem(key, JSON.stringify(value));
    } catch (error) {
      console.error('LocalStorage error:', error);
    }
  }

  return [storedValue, setValue];
}

export default useLocalStorage;
```

**Usage:**

```jsx
import useLocalStorage from '../hooks/useLocalStorage';

function Settings() {
  const [theme, setTheme]       = useLocalStorage('theme', 'light');
  const [language, setLanguage] = useLocalStorage('language', 'en');

  return (
    <div>
      <p>Current theme: {theme}</p>
      <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
        Toggle Theme
      </button>
    </div>
  );
}
// ✅ Theme persists even after page refresh!
```

---

## 3️⃣ `useDebounce` — Delay Input Processing

```jsx
// src/hooks/useDebounce.js
import { useState, useEffect } from 'react';

function useDebounce(value, delay = 500) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const timer = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    return () => clearTimeout(timer);  // cleanup on every change
  }, [value, delay]);

  return debouncedValue;
}

export default useDebounce;
```

**Usage — search input that waits before querying:**

```jsx
import { useState } from 'react';
import useDebounce from '../hooks/useDebounce';
import useFetch from '../hooks/useFetch';

function SearchPage() {
  const [query, setQuery] = useState('');
  const debouncedQuery    = useDebounce(query, 500);  // wait 500ms after user stops typing

  const { data: results, loading } = useFetch(
    debouncedQuery ? `https://api.example.com/search?q=${debouncedQuery}` : null
  );

  return (
    <div>
      <input
        value={query}
        onChange={(e) => setQuery(e.target.value)}
        placeholder="Search..."
      />
      {loading && <p>Searching...</p>}
      {results?.map(r => <div key={r.id}>{r.title}</div>)}
    </div>
  );
}
```

---

## 4️⃣ `useToggle` — Boolean State Toggle

```jsx
// src/hooks/useToggle.js
import { useState, useCallback } from 'react';

function useToggle(initialValue = false) {
  const [value, setValue] = useState(initialValue);
  const toggle = useCallback(() => setValue(v => !v), []);
  return [value, toggle];
}

export default useToggle;
```

**Usage:**

```jsx
function Modal() {
  const [isOpen, toggleOpen] = useToggle(false);

  return (
    <div>
      <button onClick={toggleOpen}>
        {isOpen ? 'Close Modal' : 'Open Modal'}
      </button>
      {isOpen && (
        <div className="modal">
          <p>Modal content!</p>
          <button onClick={toggleOpen}>Close</button>
        </div>
      )}
    </div>
  );
}
```

---

## 📁 Hooks Folder Structure

```
src/
└── hooks/
    ├── useFetch.js
    ├── useLocalStorage.js
    ├── useDebounce.js
    ├── useToggle.js
    └── useWindowSize.js
```

---

## 📊 Custom Hooks Gallery

| Hook | What It Does |
|------|-------------|
| `useFetch(url)` | Fetch data with loading/error states |
| `useLocalStorage(key, val)` | State persisted in localStorage |
| `useDebounce(value, delay)` | Delay state update (search inputs) |
| `useToggle(initial)` | Toggle boolean state |
| `useWindowSize()` | Track window width/height |
| `useOnClickOutside(ref, fn)` | Detect clicks outside an element |
| `usePrevious(value)` | Get previous render's value |

---

## ✅ Key Takeaways

- Custom hooks extract **reusable stateful logic** from components.
- They always start with `use` so React knows they follow hook rules.
- A custom hook is just a **regular function** that calls other hooks.
- Common patterns: data fetching, local storage, debouncing, toggles.
- Place custom hooks in `src/hooks/` folder.
- Don't over-abstract — only create a custom hook when the same logic appears in 2+ places.

---

## 🏋️ Practice Tasks

### Task 1 — useWindowSize
Create a `useWindowSize` hook that returns `{ width, height }` of the browser window.
Update in real-time as the window is resized.
Display a message: `"Mobile"` if width < 768, `"Tablet"` if < 1024, otherwise `"Desktop"`.

---

### Task 2 — useCountdown
Create a `useCountdown(seconds)` hook that:
- Counts down from the given number to 0
- Returns `{ count, start, stop, reset, isDone }`
- Use it to build a quiz timer component

---

### Task 3 — Compose Multiple Hooks
Build a search component that uses ALL of these together:
- `useFetch` — fetch data
- `useDebounce` — debounce the search input
- `useLocalStorage` — remember the last search query

---

> ➡️ **Next:** `10-performance-and-best-practices.md` — Optimization and production-ready React.
