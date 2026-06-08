# 08 — React Router (Multi-Page Apps)

---

## 📌 What is React Router?

React apps are **Single Page Applications (SPA)** — there's only one HTML file. **React Router** simulates navigation between "pages" by rendering different components based on the URL, without actually reloading the page.

> 💡 **Analogy:** React Router is like a traffic cop at intersections — when the URL changes, it directs traffic to the right component.

---

## 📦 Installation

```bash
npm install react-router-dom
```

---

## ⚙️ Basic Setup

**src/main.jsx:**
```jsx
import { BrowserRouter } from 'react-router-dom';
import App from './App';

ReactDOM.createRoot(document.getElementById('root')).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```

**src/App.jsx:**
```jsx
import { Routes, Route } from 'react-router-dom';
import Navbar from './components/Navbar';
import Home    from './pages/Home';
import About   from './pages/About';
import Contact from './pages/Contact';
import NotFound from './pages/NotFound';

function App() {
  return (
    <>
      <Navbar />
      <Routes>
        <Route path="/"        element={<Home />}    />
        <Route path="/about"   element={<About />}   />
        <Route path="/contact" element={<Contact />} />
        <Route path="*"        element={<NotFound />} />  {/* 404 catch-all */}
      </Routes>
    </>
  );
}
```

---

## 🔗 Navigation with `<Link>` and `<NavLink>`

**Never use `<a href>` in React Router** — it causes a full page reload!

```jsx
import { Link, NavLink } from 'react-router-dom';

function Navbar() {
  return (
    <nav>
      {/* Basic Link */}
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>

      {/* NavLink — adds 'active' class automatically when route matches */}
      <NavLink to="/"      className={({ isActive }) => isActive ? 'active' : ''}>Home</NavLink>
      <NavLink to="/about" className={({ isActive }) => isActive ? 'active' : ''}>About</NavLink>
    </nav>
  );
}
```

---

## 🔢 URL Parameters (Dynamic Routes)

```jsx
// Route definition:
<Route path="/users/:id" element={<UserProfile />} />

// URL: /users/42  →  renders UserProfile with id = "42"
```

```jsx
// Reading the parameter:
import { useParams } from 'react-router-dom';

function UserProfile() {
  const { id } = useParams();  // { id: "42" }

  return <h1>Viewing Profile: {id}</h1>;
}
```

---

## 🔍 Query Parameters (Search Params)

```jsx
// URL: /search?q=react&category=hooks

import { useSearchParams } from 'react-router-dom';

function SearchPage() {
  const [searchParams, setSearchParams] = useSearchParams();

  const query    = searchParams.get('q') || '';
  const category = searchParams.get('category') || 'all';

  function handleSearch(newQuery) {
    setSearchParams({ q: newQuery, category });
  }

  return (
    <div>
      <input value={query} onChange={(e) => handleSearch(e.target.value)} />
      <p>Searching for: "{query}" in "{category}"</p>
    </div>
  );
}
```

---

## 🧭 Programmatic Navigation with `useNavigate`

Navigate to a route from code (after form submit, login, etc.):

```jsx
import { useNavigate } from 'react-router-dom';

function LoginForm() {
  const navigate = useNavigate();

  async function handleSubmit(e) {
    e.preventDefault();
    // ... login logic
    navigate('/dashboard');        // go forward
    navigate(-1);                  // go back (like browser back button)
    navigate('/login', { replace: true });  // replace history (no back button)
  }

  return <form onSubmit={handleSubmit}>...</form>;
}
```

---

## 🛡️ Protected Routes (Auth Guards)

```jsx
// src/components/ProtectedRoute.jsx
import { Navigate } from 'react-router-dom';
import { useAuth } from '../context/AuthContext';

function ProtectedRoute({ children }) {
  const { isLoggedIn } = useAuth();

  if (!isLoggedIn) {
    return <Navigate to="/login" replace />;  // redirect to login
  }

  return children;
}
```

**Usage:**
```jsx
<Routes>
  <Route path="/"         element={<Home />} />
  <Route path="/login"    element={<Login />} />
  <Route
    path="/dashboard"
    element={
      <ProtectedRoute>
        <Dashboard />
      </ProtectedRoute>
    }
  />
</Routes>
```

---

## 📁 Nested Routes & Layouts

```jsx
// Shared layout for all /dashboard routes
function DashboardLayout() {
  return (
    <div>
      <DashboardSidebar />
      <main>
        <Outlet />  {/* ← child routes render here */}
      </main>
    </div>
  );
}

// Route setup:
<Routes>
  <Route path="/dashboard" element={<DashboardLayout />}>
    <Route index         element={<DashboardHome />}    />  {/* /dashboard */}
    <Route path="stats"  element={<DashboardStats />}  />  {/* /dashboard/stats */}
    <Route path="settings" element={<Settings />}      />  {/* /dashboard/settings */}
  </Route>
</Routes>
```

---

## 📊 React Router Hooks Summary

| Hook | Purpose | Example |
|------|---------|---------|
| `useNavigate` | Programmatic navigation | `navigate('/home')` |
| `useParams` | URL parameters | `const { id } = useParams()` |
| `useSearchParams` | Query string | `searchParams.get('q')` |
| `useLocation` | Current URL info | `location.pathname` |

---

## 📁 Recommended Folder Structure

```
src/
├── App.jsx
├── main.jsx
├── pages/
│   ├── Home.jsx
│   ├── About.jsx
│   ├── Contact.jsx
│   ├── UserProfile.jsx
│   └── NotFound.jsx
├── components/
│   ├── Navbar.jsx
│   ├── Footer.jsx
│   └── ProtectedRoute.jsx
└── context/
    └── AuthContext.jsx
```

---

## ✅ Key Takeaways

- React Router turns your SPA into a multi-page app by rendering different components per URL.
- Use `<Link>` and `<NavLink>` — **never `<a href>`** inside a React Router app.
- `useParams` reads dynamic URL segments (`:id`).
- `useNavigate` navigates programmatically (after login, form submit, etc.).
- Use nested routes with `<Outlet>` for shared layouts (dashboard, admin panel).
- **Protect routes** by checking auth before rendering sensitive pages.

---

## 🏋️ Practice Tasks

### Task 1 — Blog App Routes
Build a simple blog with routes:
- `/` → list of posts
- `/posts/:id` → single post page
- `/about` → about page
- `*` → 404 Not Found page

Fetch posts from `https://jsonplaceholder.typicode.com/posts`.

---

### Task 2 — Auth Flow
Build a login/logout flow:
- `/login` → Login form
- `/dashboard` → Protected page (redirect to `/login` if not logged in)
- Show a "Logout" button on the dashboard that clears auth and redirects to `/login`

---

### Task 3 — Breadcrumbs
Display breadcrumb navigation using `useLocation`:
- `/ > About` for the About page
- `/ > Dashboard > Stats` for the Stats page

---

> ➡️ **Next:** `09-custom-hooks.md` — Create reusable logic with custom hooks.
