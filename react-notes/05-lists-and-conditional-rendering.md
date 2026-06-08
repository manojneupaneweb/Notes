# 05 — Lists and Conditional Rendering

---

## 📌 Rendering Lists

In React, you render lists using JavaScript's `.map()` method to convert an array of data into an array of JSX elements.

```jsx
function FruitList() {
  const fruits = ['Apple', 'Banana', 'Cherry', 'Mango'];

  return (
    <ul>
      {fruits.map((fruit, index) => (
        <li key={index}>{fruit}</li>
      ))}
    </ul>
  );
}
```

---

## 🔑 The `key` Prop — Why It's Required

React needs a **unique `key`** on each list item to efficiently track which items changed, were added, or removed.

```jsx
// ❌ Bad — using index as key (causes bugs when list order changes)
{items.map((item, index) => <li key={index}>{item}</li>)}

// ✅ Good — use a unique ID from the data
{users.map(user => <li key={user.id}>{user.name}</li>)}
```

> ⚠️ **Rule:** The `key` must be **unique among siblings**, not globally. Never use the array index as a key if the list can be reordered or filtered.

---

## 📋 Rendering a List of Objects

```jsx
function ProductList() {
  const products = [
    { id: 1, name: 'Laptop',  price: 999  },
    { id: 2, name: 'Mouse',   price: 29   },
    { id: 3, name: 'Monitor', price: 399  },
  ];

  return (
    <div>
      <h2>Products</h2>
      {products.map(product => (
        <div key={product.id} className="product-card">
          <h3>{product.name}</h3>
          <p>Price: ${product.price}</p>
        </div>
      ))}
    </div>
  );
}
```

---

## 🔍 Filtering Lists

```jsx
function StudentList() {
  const [search, setSearch] = useState('');

  const students = [
    { id: 1, name: 'Manoj',  grade: 'A' },
    { id: 2, name: 'Sita',   grade: 'B' },
    { id: 3, name: 'Ram',    grade: 'A' },
    { id: 4, name: 'Gita',   grade: 'C' },
  ];

  const filtered = students.filter(s =>
    s.name.toLowerCase().includes(search.toLowerCase())
  );

  return (
    <div>
      <input
        value={search}
        onChange={(e) => setSearch(e.target.value)}
        placeholder="Search students..."
      />
      <ul>
        {filtered.map(student => (
          <li key={student.id}>{student.name} — Grade: {student.grade}</li>
        ))}
      </ul>
      <p>Showing {filtered.length} of {students.length} students</p>
    </div>
  );
}
```

---

## 🔀 Conditional Rendering

There are 4 patterns for conditionally rendering JSX:

### 1. `if` statement (outside the return):

```jsx
function Greeting({ isLoggedIn }) {
  if (isLoggedIn) {
    return <h1>Welcome back! 👋</h1>;
  }
  return <h1>Please log in.</h1>;
}
```

---

### 2. Ternary operator `? :` (inside JSX):

```jsx
function StatusBadge({ isOnline }) {
  return (
    <span style={{ color: isOnline ? 'green' : 'gray' }}>
      {isOnline ? '🟢 Online' : '⚫ Offline'}
    </span>
  );
}
```

---

### 3. Logical AND `&&` (render or nothing):

```jsx
function Notifications({ count }) {
  return (
    <div>
      <h1>Dashboard</h1>
      {count > 0 && <p>You have {count} new notifications!</p>}
      {/* If count = 0, nothing is rendered */}
    </div>
  );
}
```

> ⚠️ **Gotcha:** `{0 && <Component />}` renders `0` — use `{count > 0 && ...}` to be safe!

---

### 4. Nullish coalescing / early return for loading states:

```jsx
function UserProfile({ user, loading, error }) {
  if (loading) return <p>Loading...</p>;
  if (error)   return <p>Error: {error}</p>;
  if (!user)   return <p>No user found.</p>;

  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.email}</p>
    </div>
  );
}
```

---

## 🔄 Conditional CSS Classes

```jsx
function Alert({ type, message }) {
  return (
    <div className={`alert alert-${type}`}>
      {message}
    </div>
  );
}

// Usage:
<Alert type="success" message="Saved!" />
<Alert type="error"   message="Something went wrong." />
// → renders: class="alert alert-success"  or  class="alert alert-error"
```

---

## 📊 Conditional Rendering Comparison

| Pattern | Best For |
|---------|---------|
| `if` statement | Complex conditions, multiple returns |
| Ternary `? :` | Either/or rendering inside JSX |
| `&&` | Render something or nothing |
| Early return | Loading/error/empty states |

---

## 🏗️ Complete Example: Data Table

```jsx
import { useState, useEffect } from 'react';

function UserTable() {
  const [users, setUsers]     = useState([]);
  const [loading, setLoading] = useState(true);
  const [search, setSearch]   = useState('');

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(res => res.json())
      .then(data => {
        setUsers(data);
        setLoading(false);
      });
  }, []);

  const filtered = users.filter(u =>
    u.name.toLowerCase().includes(search.toLowerCase())
  );

  if (loading) return <p>Loading users...</p>;

  return (
    <div>
      <input
        value={search}
        onChange={(e) => setSearch(e.target.value)}
        placeholder="Search users..."
      />

      {filtered.length === 0 ? (
        <p>No users found for "{search}"</p>
      ) : (
        <table>
          <thead>
            <tr>
              <th>Name</th>
              <th>Email</th>
              <th>City</th>
            </tr>
          </thead>
          <tbody>
            {filtered.map(user => (
              <tr key={user.id}>
                <td>{user.name}</td>
                <td>{user.email}</td>
                <td>{user.address.city}</td>
              </tr>
            ))}
          </tbody>
        </table>
      )}
    </div>
  );
}
```

---

## ✅ Key Takeaways

- Use `.map()` to render lists of JSX from arrays.
- Always provide a **unique `key`** prop — use item IDs, not array indexes.
- Use `.filter()` to build search/filter functionality.
- **4 conditional patterns:** `if`, ternary (`? :`), logical AND (`&&`), early return.
- Handle **loading, error, and empty** states before rendering the main UI.

---

## 🏋️ Practice Tasks

### Task 1 — Recipe List
Create a list of recipes with `name`, `cuisine`, and `cookTime`.
- Filter by cuisine type (Indian, Italian, etc.) using buttons.
- Display the count of filtered results.

---

### Task 2 — Accordion FAQ
Build an FAQ accordion:
- List of questions
- Clicking a question shows/hides the answer
- Only one answer open at a time

---

### Task 3 — Loading Skeleton
Fetch users from `jsonplaceholder.typicode.com/users`.
- While loading, show **3 skeleton cards** (gray placeholder blocks).
- Replace with real content once data arrives.

---

> ➡️ **Next:** `06-useref-and-advanced-hooks.md` — useRef, useMemo, and useCallback.
