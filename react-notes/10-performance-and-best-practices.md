# 10 — Performance and Best Practices

---

## 📌 Why Performance Matters

A slow React app means frustrated users. As apps grow, unnecessary re-renders, large bundles, and unoptimized code can make the UI feel sluggish.

> 💡 **Rule of thumb:** Don't optimize prematurely. First make it work, then measure, then optimize.

---

## 1️⃣ React.memo — Prevent Unnecessary Re-renders

By default, a component re-renders whenever its **parent** re-renders — even if the props didn't change. `React.memo` skips re-rendering if props haven't changed.

```jsx
// ❌ Without memo — re-renders even when 'name' didn't change:
function Avatar({ name }) {
  console.log('Avatar rendered');
  return <img src={`https://api.dicebear.com/7.x/initials/svg?seed=${name}`} />;
}

// ✅ With memo — only re-renders when 'name' changes:
const Avatar = React.memo(function Avatar({ name }) {
  console.log('Avatar rendered');
  return <img src={`https://api.dicebear.com/7.x/initials/svg?seed=${name}`} />;
});
```

### When to use `React.memo`:
- Component renders often
- Receives the same props most of the time
- Rendering is visually expensive (large lists, charts)

---

## 2️⃣ Lazy Loading Components

Load components **only when they're needed** — reduces the initial bundle size.

```jsx
import { lazy, Suspense } from 'react';

// ✅ Component is loaded only when user navigates to this route:
const Dashboard = lazy(() => import('./pages/Dashboard'));
const Settings  = lazy(() => import('./pages/Settings'));

function App() {
  return (
    <Suspense fallback={<p>Loading...</p>}>
      <Routes>
        <Route path="/dashboard" element={<Dashboard />} />
        <Route path="/settings"  element={<Settings />}  />
      </Routes>
    </Suspense>
  );
}
```

> ✅ **Result:** The initial JS bundle is smaller — the app loads faster.

---

## 3️⃣ Key Optimization Techniques

### Avoid creating objects/functions in JSX:

```jsx
// ❌ New object created on EVERY render (breaks React.memo):
<Card style={{ padding: 16, margin: 8 }} />

// ✅ Define outside the component (stable reference):
const cardStyle = { padding: 16, margin: 8 };
function App() {
  return <Card style={cardStyle} />;
}
```

```jsx
// ❌ New function created on EVERY render:
<Button onClick={() => handleAction(id)} />

// ✅ Use useCallback if passing to memoized child:
const handleClick = useCallback(() => handleAction(id), [id]);
<Button onClick={handleClick} />
```

---

### Virtualize long lists (react-virtual):

Rendering 10,000 list items all at once is extremely slow. Only render items that are **visible on screen**.

```bash
npm install @tanstack/react-virtual
```

```jsx
import { useVirtualizer } from '@tanstack/react-virtual';

function VirtualList({ items }) {
  const parentRef = useRef(null);

  const virtualizer = useVirtualizer({
    count: items.length,
    getScrollElement: () => parentRef.current,
    estimateSize: () => 50,  // estimated height of each item in px
  });

  return (
    <div ref={parentRef} style={{ height: 400, overflow: 'auto' }}>
      <div style={{ height: virtualizer.getTotalSize() }}>
        {virtualizer.getVirtualItems().map(vItem => (
          <div
            key={vItem.index}
            style={{ transform: `translateY(${vItem.start}px)` }}
          >
            {items[vItem.index].name}
          </div>
        ))}
      </div>
    </div>
  );
}
// ✅ Only ~10 DOM nodes rendered at a time, regardless of list size!
```

---

## 4️⃣ React Best Practices

### Component Design:
```
✅ One component per file
✅ Small, focused components (< 150 lines)
✅ Descriptive names: UserProfileCard, not UPC
✅ Extract complex JSX into sub-components
✅ Keep side effects in useEffect, not inline
```

### State Management:
```
✅ Keep state as local as possible
✅ Lift state only when multiple components need it
✅ Avoid storing derived data in state (compute it)
✅ Never mutate state directly
✅ Use functional updates for state based on previous value
```

```jsx
// ❌ Depends on potentially stale 'count' value:
setCount(count + 1);

// ✅ Always current — use when new state depends on old state:
setCount(prev => prev + 1);
```

---

### useEffect Best Practices:

```jsx
// ✅ Always specify all dependencies
useEffect(() => {
  fetchData(userId);
}, [userId]);  // ← include ALL variables used inside

// ✅ Clean up subscriptions and timers
useEffect(() => {
  const subscription = subscribe(topic);
  return () => subscription.unsubscribe();  // cleanup
}, [topic]);

// ✅ Don't use async directly in useEffect
useEffect(() => {
  // ❌ async function() directly as useEffect callback
  // ✅ Define async inside and call it:
  async function load() { ... }
  load();
}, []);
```

---

## 5️⃣ Project Folder Structure (Scalable)

```
src/
├── assets/                 ← images, fonts, icons
├── components/             ← reusable UI components
│   ├── Button/
│   │   ├── Button.jsx
│   │   ├── Button.module.css
│   │   └── index.js        ← re-export for clean imports
│   └── Card/
│       ├── Card.jsx
│       └── Card.module.css
├── context/                ← global state (Auth, Theme)
│   ├── AuthContext.jsx
│   └── ThemeContext.jsx
├── hooks/                  ← custom hooks
│   ├── useFetch.js
│   └── useLocalStorage.js
├── pages/                  ← top-level route components
│   ├── Home.jsx
│   ├── About.jsx
│   └── Dashboard.jsx
├── services/               ← API call functions
│   └── api.js
├── utils/                  ← pure helper functions
│   └── formatDate.js
├── App.jsx
└── main.jsx
```

---

## 6️⃣ Error Boundaries

Catch JavaScript errors in the component tree and display a fallback UI instead of crashing the whole app.

```jsx
import { Component } from 'react';

class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  componentDidCatch(error, info) {
    console.error('Error caught:', error, info);
  }

  render() {
    if (this.state.hasError) {
      return <h2>Something went wrong. Please refresh the page.</h2>;
    }
    return this.props.children;
  }
}

// Usage:
<ErrorBoundary>
  <RiskyComponent />
</ErrorBoundary>
```

---

## 📊 Performance Checklist

| Optimization | When to Apply |
|-------------|--------------|
| `React.memo` | Component re-renders with same props |
| `useCallback` | Function prop passed to memoized child |
| `useMemo` | Expensive calculation on every render |
| `lazy()` + `Suspense` | Large components/pages |
| Virtualization | Lists with 100+ items |
| Functional state updates | State depends on previous value |
| Image optimization | Large images in the app |

---

## ✅ Key Takeaways

- Use `React.memo` to skip re-renders when props haven't changed.
- Use `lazy()` + `Suspense` to code-split large pages — faster initial load.
- Use **functional updates** (`prev => prev + 1`) for safe state updates.
- **Don't prematurely optimize** — profile first with React DevTools.
- Structure your project with clear folders: `components`, `pages`, `hooks`, `context`, `services`.
- Wrap risky components in `ErrorBoundary` to prevent full app crashes.

---

## 🏋️ Practice Tasks

### Task 1 — Measure Re-renders
Add `console.log("rendered")` to several components. Notice how often they render. Then apply `React.memo` and see the difference.

---

### Task 2 — Lazy Load Dashboard
Take an existing multi-page app and lazy load all page components.
Compare the initial bundle size before and after (check Network tab in DevTools).

---

### Task 3 — Build an Optimized Search
Create a search component that:
- Debounces input (300ms)
- Memoizes filtered results with `useMemo`
- Wraps each result item with `React.memo`

---

> 🎉 **Congratulations!** You've covered the core of React. Now go build projects!
