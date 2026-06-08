# 06 — useRef and Advanced Hooks

---

## 1️⃣ `useRef` Hook

`useRef` creates a **mutable reference** that persists between renders. It has two main uses:

1. **Access DOM elements directly** (like `document.getElementById`)
2. **Store a value that doesn't trigger re-render** when changed

### Syntax:

```jsx
import { useRef } from 'react';

const myRef = useRef(initialValue);
// myRef.current = the stored value or DOM element
```

---

### Use Case 1 — DOM Access:

```jsx
import { useRef } from 'react';

function FocusInput() {
  const inputRef = useRef(null);

  function handleFocus() {
    inputRef.current.focus();  // directly focus the input DOM element
  }

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="I'll get focused..." />
      <button onClick={handleFocus}>Focus Input</button>
    </div>
  );
}
```

---

### Use Case 2 — Storing Values Without Re-renders:

```jsx
import { useState, useRef, useEffect } from 'react';

function Timer() {
  const [seconds, setSeconds]   = useState(0);
  const [running, setRunning]   = useState(false);
  const intervalRef             = useRef(null);  // stores timer ID without re-rendering

  function start() {
    if (running) return;
    setRunning(true);
    intervalRef.current = setInterval(() => {
      setSeconds(prev => prev + 1);
    }, 1000);
  }

  function stop() {
    setRunning(false);
    clearInterval(intervalRef.current);
  }

  function reset() {
    stop();
    setSeconds(0);
  }

  return (
    <div>
      <h2>{seconds}s</h2>
      <button onClick={start}>Start</button>
      <button onClick={stop}>Stop</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}
```

---

## ⚖️ `useRef` vs `useState`

| | `useState` | `useRef` |
|--|-----------|---------|
| Triggers re-render? | ✅ Yes | ❌ No |
| Best for | UI data (display it) | Non-UI data (IDs, DOM refs) |
| Access via | `value` | `ref.current` |

---

## 2️⃣ `useMemo` Hook

`useMemo` **caches the result** of an expensive calculation and only re-runs it when its dependencies change.

### Problem Without useMemo:

```jsx
// ❌ This runs on EVERY render, even when unrelated state changes
function App() {
  const [count, setCount]   = useState(0);
  const [text, setText]     = useState('');

  // This runs whenever 'text' changes, even though it only needs 'count':
  const expensiveValue = heavyCalculation(count);

  return (...);
}
```

### Solution With useMemo:

```jsx
import { useState, useMemo } from 'react';

function App() {
  const [count, setCount] = useState(0);
  const [text, setText]   = useState('');

  // ✅ Only re-calculates when 'count' changes
  const expensiveValue = useMemo(() => {
    console.log('Calculating...');
    return heavyCalculation(count);
  }, [count]);

  return (
    <div>
      <p>Result: {expensiveValue}</p>
      <button onClick={() => setCount(count + 1)}>Change Count</button>
      <input value={text} onChange={(e) => setText(e.target.value)} />
    </div>
  );
}
```

### Practical Example — Filtered List:

```jsx
const filteredUsers = useMemo(
  () => users.filter(u => u.name.toLowerCase().includes(search.toLowerCase())),
  [users, search]  // only re-filter when users or search changes
);
```

> 💡 **When to use:** Only use `useMemo` for genuinely expensive operations. Don't prematurely optimize — it adds complexity.

---

## 3️⃣ `useCallback` Hook

`useCallback` **caches a function** so the same function reference is returned between renders.

### Why Does It Matter?

When you pass a function as a prop to a child component, a new function is created every render — causing the child to unnecessarily re-render.

```jsx
import { useState, useCallback } from 'react';

function Parent() {
  const [count, setCount] = useState(0);
  const [text, setText]   = useState('');

  // ❌ Without useCallback: new function created every render
  // ✅ With useCallback: same function reference when count doesn't change
  const handleClick = useCallback(() => {
    console.log('count:', count);
  }, [count]);

  return (
    <div>
      <Child onClick={handleClick} />
      <button onClick={() => setCount(count + 1)}>+</button>
      <input value={text} onChange={(e) => setText(e.target.value)} />
    </div>
  );
}
```

---

## 4️⃣ `useReducer` Hook

`useReducer` is an alternative to `useState` for **complex state logic** — similar to how Redux works.

### Syntax:

```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

### Counter with useReducer:

```jsx
import { useReducer } from 'react';

// Reducer: pure function that takes current state + action, returns new state
function counterReducer(state, action) {
  switch (action.type) {
    case 'INCREMENT': return { count: state.count + 1 };
    case 'DECREMENT': return { count: state.count - 1 };
    case 'RESET':     return { count: 0 };
    case 'SET':       return { count: action.payload };
    default:          return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(counterReducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>+1</button>
      <button onClick={() => dispatch({ type: 'DECREMENT' })}>-1</button>
      <button onClick={() => dispatch({ type: 'RESET'     })}>Reset</button>
      <button onClick={() => dispatch({ type: 'SET', payload: 10 })}>Set to 10</button>
    </div>
  );
}
```

---

## ⚖️ useState vs useReducer

| | `useState` | `useReducer` |
|--|-----------|-------------|
| Best for | Simple, independent values | Complex state logic with many actions |
| Update style | `setValue(newValue)` | `dispatch({ type: 'ACTION' })` |
| Logic location | Inline (in handlers) | In the reducer function |
| Debugging | Can be scattered | Centralized in reducer |

---

## 📊 Hooks Quick Reference

| Hook | Purpose | When to Use |
|------|---------|------------|
| `useState` | Basic state | Simple values |
| `useEffect` | Side effects | API calls, timers |
| `useRef` | DOM access / persistent values | Focus, intervals, previous values |
| `useMemo` | Cache calculated values | Expensive computations |
| `useCallback` | Cache functions | Prevent child re-renders |
| `useReducer` | Complex state logic | Many related state updates |
| `useContext` | Global state | Theme, auth, language |

---

## ✅ Key Takeaways

- `useRef` accesses DOM elements and stores values **without re-rendering**.
- `useMemo` caches **values** — use for expensive calculations.
- `useCallback` caches **functions** — prevents unnecessary child re-renders.
- `useReducer` manages **complex state** with actions and a reducer function.
- Don't over-optimize — add `useMemo`/`useCallback` only when you measure a performance problem.

---

## 🏋️ Practice Tasks

### Task 1 — Password Reveal
Create a password input with a "Show/Hide" toggle button.
Use `useRef` to access the input and toggle its `type` between `"text"` and `"password"`.

---

### Task 2 — Shopping Cart with useReducer
Build a shopping cart with actions:
- `ADD_ITEM` — add a product to cart
- `REMOVE_ITEM` — remove a product
- `UPDATE_QUANTITY` — change quantity of an item
- `CLEAR_CART` — empty the cart

---

### Task 3 — Previous Value Tracker
Using `useRef`, track and display both the **current** and **previous** value of a counter.

---

> ➡️ **Next:** `07-context-api.md` — Share state globally without prop drilling.
