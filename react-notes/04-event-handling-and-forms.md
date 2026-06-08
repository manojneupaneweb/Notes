# 04 — Event Handling and Forms in React

---

## 📌 Event Handling in React

React uses **synthetic events** — wrappers around native browser events that work the same way across all browsers.

Event handlers are passed as **props** using camelCase names:

| HTML | React |
|------|-------|
| `onclick="..."` | `onClick={...}` |
| `onchange="..."` | `onChange={...}` |
| `onsubmit="..."` | `onSubmit={...}` |
| `onmouseover="..."` | `onMouseOver={...}` |
| `onkeydown="..."` | `onKeyDown={...}` |

---

## 🖱️ Basic Event Handling

```jsx
function ButtonExample() {
  function handleClick() {
    alert('Button clicked!');
  }

  return <button onClick={handleClick}>Click Me</button>;
  //                        ↑ pass the function, don't CALL it!
}
```

> ⚠️ **Common Mistake:**
> ```jsx
> onClick={handleClick}   // ✅ Correct — passes the function
> onClick={handleClick()} // ❌ Wrong — calls it immediately on render!
> ```

---

## 📋 The Event Object

React passes an **event object** (`e`) to every handler — it has useful info about what happened.

```jsx
function InputExample() {
  function handleChange(e) {
    console.log(e.target.value);     // text the user typed
    console.log(e.target.name);      // input's name attribute
    console.log(e.target.type);      // "text", "checkbox", etc.
    console.log(e.target.checked);   // for checkboxes
  }

  return <input type="text" onChange={handleChange} />;
}
```

---

## 📝 Controlled Components (Forms)

In React, form inputs should be **controlled** — their value is stored in state and React is the single source of truth.

```
User types → onChange fires → setName(value) → state updates → input re-renders with new value
```

### Text Input:

```jsx
import { useState } from 'react';

function NameForm() {
  const [name, setName] = useState('');

  function handleSubmit(e) {
    e.preventDefault();    // ← prevents page reload
    alert(`Hello, ${name}!`);
  }

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="name">Your Name:</label>
      <input
        id="name"
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <button type="submit">Submit</button>
    </form>
  );
}
```

---

### Multiple Inputs with One Handler:

```jsx
function SignupForm() {
  const [form, setForm] = useState({
    username: '',
    email: '',
    password: '',
  });

  function handleChange(e) {
    setForm({
      ...form,
      [e.target.name]: e.target.value,  // dynamically update the right field
    });
  }

  function handleSubmit(e) {
    e.preventDefault();
    console.log('Form submitted:', form);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input name="username" value={form.username} onChange={handleChange} placeholder="Username" />
      <input name="email"    value={form.email}    onChange={handleChange} placeholder="Email" type="email" />
      <input name="password" value={form.password} onChange={handleChange} placeholder="Password" type="password" />
      <button type="submit">Sign Up</button>
    </form>
  );
}
```

---

### Checkbox:

```jsx
function CheckboxExample() {
  const [isChecked, setIsChecked] = useState(false);

  return (
    <label>
      <input
        type="checkbox"
        checked={isChecked}
        onChange={(e) => setIsChecked(e.target.checked)}  // use .checked for checkboxes
      />
      Accept Terms and Conditions
    </label>
  );
}
```

---

### Select Dropdown:

```jsx
function SelectExample() {
  const [country, setCountry] = useState('nepal');

  return (
    <select value={country} onChange={(e) => setCountry(e.target.value)}>
      <option value="nepal">Nepal</option>
      <option value="india">India</option>
      <option value="usa">USA</option>
    </select>
  );
}
```

---

## 🚫 Preventing Default Behavior

Always call `e.preventDefault()` on form `onSubmit` to stop the page from reloading.

```jsx
function handleSubmit(e) {
  e.preventDefault();    // ← CRITICAL for forms!
  // process form data...
}
```

---

## 🛡️ Basic Form Validation

```jsx
function LoginForm() {
  const [email, setEmail]       = useState('');
  const [password, setPassword] = useState('');
  const [errors, setErrors]     = useState({});

  function validate() {
    const newErrors = {};
    if (!email)               newErrors.email    = 'Email is required';
    if (!email.includes('@')) newErrors.email    = 'Email is invalid';
    if (!password)            newErrors.password = 'Password is required';
    if (password.length < 6)  newErrors.password = 'Password must be at least 6 characters';
    return newErrors;
  }

  function handleSubmit(e) {
    e.preventDefault();
    const validationErrors = validate();
    if (Object.keys(validationErrors).length > 0) {
      setErrors(validationErrors);
      return;
    }
    console.log('Login:', { email, password });
  }

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <input type="email" value={email} onChange={(e) => setEmail(e.target.value)} placeholder="Email" />
        {errors.email && <p style={{ color: 'red' }}>{errors.email}</p>}
      </div>
      <div>
        <input type="password" value={password} onChange={(e) => setPassword(e.target.value)} placeholder="Password" />
        {errors.password && <p style={{ color: 'red' }}>{errors.password}</p>}
      </div>
      <button type="submit">Login</button>
    </form>
  );
}
```

---

## 📊 Common Events Cheat Sheet

| Event | When It Fires | Common Use |
|-------|---------------|------------|
| `onClick` | Element is clicked | Buttons, links |
| `onChange` | Input value changes | Text, select, checkbox |
| `onSubmit` | Form is submitted | Forms |
| `onFocus` | Input gains focus | Show tooltip |
| `onBlur` | Input loses focus | Validate field |
| `onKeyDown` | Key is pressed down | Keyboard shortcuts |
| `onKeyUp` | Key is released | Search-as-you-type |
| `onMouseOver` | Mouse hovers over | Tooltips |
| `onMouseOut` | Mouse leaves element | Tooltips |

---

## ✅ Key Takeaways

- React events use **camelCase**: `onClick`, `onChange`, `onSubmit`.
- Pass functions to event handlers — **don't call them**: `onClick={fn}` not `onClick={fn()}`.
- The **event object** `e` has useful data: `e.target.value`, `e.target.checked`.
- Use `e.preventDefault()` in `onSubmit` to stop page reload.
- Use **controlled components** — keep form values in state.
- For multiple inputs, use `e.target.name` with a single handler.

---

## 🏋️ Practice Tasks

### Task 1 — Live Search Filter
Create a list of 10 names. Add a text input above it.
Filter the list in real-time as the user types — only show names that contain the search text.

---

### Task 2 — Registration Form
Build a registration form with:
- Name, Email, Password, Confirm Password, Country (select)
- Validate all fields on submit
- Show error messages below each invalid field
- Show a success message when all fields are valid

---

### Task 3 — Rating Widget
Create a star rating component (⭐⭐⭐⭐⭐):
- Clicking a star sets that as the rating
- Hovering shows a preview of the rating
- Display the selected rating as: `"You rated: 4/5 stars"`

---

> ➡️ **Next:** `05-lists-and-conditional-rendering.md` — Render dynamic lists and conditional UI.
