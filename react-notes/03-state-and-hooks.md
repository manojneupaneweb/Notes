# 03 — State and Hooks (useState, useEffect)

---

## 📌 What is State?

**State** is data that **changes over time** inside a component.

- When state changes, React **automatically re-renders** the component to show the new data.
- Think of state as a component's **memory** — it remembers things between renders.

> 💡 **Analogy:** A light switch has "state" — it's either ON or OFF. When you flip it (update state), the room re-renders (lights change).

---

## 🎣 What are Hooks?

**Hooks** are special React functions that start with `use`. They let function components use React features like state and lifecycle.

| Hook | Purpose |
|------|---------|
| `useState` | Add state to a component |
| `useEffect` | Run side effects (API calls, timers) |
| `useRef` | Access DOM elements directly |
| `useContext` | Read from Context (global state) |
| `useMemo` | Cache expensive calculations |
| `useCallback` | Cache functions |

---

## 1️⃣ `useState` Hook

### Syntax:

```jsx
import { useState } from 'react';

const [value, setValue] = useState(initialValue);
//     ↑ current    ↑ updater function    ↑ starting value
```

### Simple Counter Example:

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);  // starts at 0

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
      <button onClick={() => setCount(count - 1)}>-1</button>
      <button onClick={() => setCount(0)}>Reset</button>
    </div>
  );
}
```

---

### useState with Strings:

```jsx
function NameInput() {
  const [name, setName] = useState("");

  return (
    <div>
      <input
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}  // e.target.value = what user typed
        placeholder="Enter your name"
      />
      <p>Hello, {name || "stranger"}!</p>
    </div>
  );
}
```

---

### useState with Objects:

```jsx
function UserForm() {
  const [user, setUser] = useState({ name: "", email: "" });

  function handleChange(e) {
    setUser({
      ...user,                      // ← spread existing fields
      [e.target.name]: e.target.value  // ← update only the changed field
    });
  }

  return (
    <form>
      <input name="name"  value={user.name}  onChange={handleChange} placeholder="Name" />
      <input name="email" value={user.email} onChange={handleChange} placeholder="Email" />
      <p>Name: {user.name} | Email: {user.email}</p>
    </form>
  );
}
```

---

### useState with Arrays:

```jsx
function TodoList() {
  const [todos, setTodos] = useState(["Buy milk", "Learn React"]);
  const [input, setInput]   = useState("");

  function addTodo() {
    if (!input.trim()) return;
    setTodos([...todos, input]);  // ✅ always create a NEW array
    setInput("");
  }

  function removeTodo(index) {
    setTodos(todos.filter((_, i) => i !== index));
  }

  return (
    <div>
      <input value={input} onChange={(e) => setInput(e.target.value)} />
      <button onClick={addTodo}>Add</button>
      <ul>
        {todos.map((todo, index) => (
          <li key={index}>
            {todo}
            <button onClick={() => removeTodo(index)}>❌</button>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

> ⚠️ **Never mutate state directly:** `todos.push(item)` ❌ — always create a new array/object.

---

## 2️⃣ `useEffect` Hook

`useEffect` runs **side effects** — code that runs after the component renders.

Side effects include: fetching data, timers, event listeners, updating the document title.

### Syntax:

```jsx
import { useEffect } from 'react';

useEffect(() => {
  // runs after every render
});

useEffect(() => {
  // runs only ONCE after first render (on mount)
}, []);

useEffect(() => {
  // runs when 'count' changes
}, [count]);
```

### Common Use Cases:

#### 1. Update the document title:

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]);  // runs whenever count changes

  return <button onClick={() => setCount(count + 1)}>Count: {count}</button>;
}
```

---

#### 2. Fetch data from an API:

```jsx
import { useState, useEffect } from 'react';

function UserList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    async function fetchUsers() {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/users');
        const data = await response.json();
        setUsers(data);
      } catch (error) {
        console.error('Failed to fetch:', error);
      } finally {
        setLoading(false);
      }
    }

    fetchUsers();
  }, []);  // ← empty array = run once on mount

  if (loading) return <p>Loading...</p>;

  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name} — {user.email}</li>
      ))}
    </ul>
  );
}
```

---

#### 3. Cleanup function (unsubscribe timers/listeners):

```jsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log('tick');
  }, 1000);

  // ✅ Return a cleanup function — runs before the component unmounts
  return () => {
    clearInterval(timer);
    console.log('Timer cleared!');
  };
}, []);
```

---

## 📊 useEffect Dependency Array

| Dependency Array | When Does Effect Run? |
|-----------------|----------------------|
| No array | After **every render** |
| `[]` (empty) | Only **once** after first render (mount) |
| `[value]` | After first render + whenever `value` changes |
| `[a, b]` | After first render + whenever `a` or `b` changes |

---

## 🔄 Component Lifecycle with useEffect

```
Mount    → useEffect runs ([] dependency)
↓
Re-render → useEffect runs if dependencies changed
↓
Unmount  → cleanup function runs
```

---

## ✅ Key Takeaways

- **State** is data that changes and triggers a re-render.
- Use `useState` to declare state: `const [value, setValue] = useState(initial)`.
- **Never mutate state directly** — always pass a new value to the setter.
- `useEffect` runs **after rendering** — use it for API calls, timers, subscriptions.
- The **dependency array** controls when the effect runs.
- Return a **cleanup function** from `useEffect` to avoid memory leaks.

---

## 🏋️ Practice Tasks

### Task 1 — Toggle Switch
Create a component with a button that toggles between "ON" and "OFF" state.
- Display different text and background color for each state.

---

### Task 2 — Character Counter
Create a textarea with a live character counter:
- Show: `"Characters: 47 / 200"`
- Turn the counter **red** when over 180 characters.

---

### Task 3 — Fetch & Display Posts
Fetch posts from `https://jsonplaceholder.typicode.com/posts?_limit=10` and display:
- Post title (bold)
- Post body (truncated to 100 characters with "...")
- Show a **loading** state while fetching.
- Show an **error** message if the fetch fails.

---

> ➡️ **Next:** `04-event-handling-and-forms.md` — Handle user interactions and forms.
