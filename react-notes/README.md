# ⚛️ React Notes
### React — Beginner to Advanced

---

> **Designed for:** Students who already know HTML, CSS, and JavaScript.
> **Goal:** Master React step by step — from components to performance optimization.

---

## 📁 Folder Structure

```
react-notes/
├── README.md                              ← You are here
├── 01-introduction.md
├── 02-components.md
├── 03-state-and-hooks.md
├── 04-event-handling-and-forms.md
├── 05-lists-and-conditional-rendering.md
├── 06-useref-and-advanced-hooks.md
├── 07-context-api.md
├── 08-react-router.md
├── 09-custom-hooks.md
└── 10-performance-and-best-practices.md
```

---

## 🗺️ React Learning Path

| # | File | Topics Covered | Level |
|---|------|----------------|-------|
| 01 | `01-introduction.md` | What is React, Virtual DOM, JSX, Vite setup | 🟢 Beginner |
| 02 | `02-components.md` | Function components, props, composition, children | 🟢 Beginner |
| 03 | `03-state-and-hooks.md` | `useState`, `useEffect`, state with objects/arrays | 🟡 Beginner-Mid |
| 04 | `04-event-handling-and-forms.md` | Events, controlled inputs, validation | 🟡 Beginner-Mid |
| 05 | `05-lists-and-conditional-rendering.md` | `.map()`, `key`, filter, conditional patterns | 🟡 Intermediate |
| 06 | `06-useref-and-advanced-hooks.md` | `useRef`, `useMemo`, `useCallback`, `useReducer` | 🟠 Intermediate |
| 07 | `07-context-api.md` | Context, prop drilling, `useContext`, Auth context | 🟠 Intermediate |
| 08 | `08-react-router.md` | Routing, `useNavigate`, dynamic routes, protected routes | 🟠 Intermediate |
| 09 | `09-custom-hooks.md` | `useFetch`, `useLocalStorage`, `useDebounce`, `useToggle` | 🔴 Advanced |
| 10 | `10-performance-and-best-practices.md` | `React.memo`, lazy loading, best practices, project structure | 🔴 Advanced |

---

## 📚 Recommended Learning Order

```
Prerequisites (make sure you know these first!)
    │
    ▼
HTML + CSS + JavaScript (ES6+)
    │   especially: arrow functions, destructuring, spread, async/await
    ▼
01 — Introduction to React
    │   Learn: What React is, JSX, Virtual DOM, setup with Vite
    ▼
02 — Components
    │   Learn: Function components, props, composition
    ▼
03 — State and Hooks
    │   Learn: useState, useEffect, managing state
    ▼
04 — Event Handling & Forms
    │   Learn: Events, controlled components, validation
    ▼
05 — Lists & Conditional Rendering
    │   Learn: map, key, filter, if/ternary/&&
    ▼
06 — Advanced Hooks
    │   Learn: useRef, useMemo, useCallback, useReducer
    ▼
07 — Context API
    │   Learn: Global state, prop drilling solution
    ▼
08 — React Router
    │   Learn: Multi-page apps, dynamic routes
    ▼
09 — Custom Hooks
    │   Learn: Extract reusable logic into hooks
    ▼
10 — Performance & Best Practices
    │   Learn: Optimization, project structure
    ▼
Build Projects! 🚀
```

---

## 🛠️ Tools You Need

| Tool | Purpose | How to Get |
|------|---------|-----------|
| **Node.js** | Run npm commands | [nodejs.org](https://nodejs.org) (LTS version) |
| **VS Code** | Code editor | [code.visualstudio.com](https://code.visualstudio.com) |
| **React DevTools** | Inspect React components in browser | Chrome/Firefox extension |
| **Vite** | Fast React project setup | `npm create vite@latest` |

### VS Code Extensions for React:
- **ES7+ React/Redux/React-Native snippets** — shortcuts like `rafce` to scaffold components
- **Prettier** — auto-format code
- **ESLint** — catch bugs as you type
- **Auto Rename Tag** — auto-close JSX tags

---

## ⚡ Quick Start

```bash
# 1. Create a new React project
npm create vite@latest my-app -- --template react

# 2. Go into the project folder
cd my-app

# 3. Install dependencies
npm install

# 4. Start the development server
npm run dev

# Open http://localhost:5173 in your browser
```

---

## 📦 Common React Packages

| Package | Purpose | Install |
|---------|---------|---------|
| `react-router-dom` | Routing between pages | `npm i react-router-dom` |
| `axios` | HTTP requests (alternative to fetch) | `npm i axios` |
| `@tanstack/react-query` | Server state management | `npm i @tanstack/react-query` |
| `zustand` | Simple global state | `npm i zustand` |
| `react-hook-form` | Form handling | `npm i react-hook-form` |
| `framer-motion` | Animations | `npm i framer-motion` |

---

## 💡 Study Tips

1. **Type, don't copy** — Typing code by hand builds muscle memory.
2. **Use React DevTools** — Inspect component state and props in the browser.
3. **Build projects** — After each chapter, build something small with those concepts.
4. **Read error messages** — React error messages are actually very helpful.
5. **Use the official docs** — [react.dev](https://react.dev) is excellent and beginner-friendly.

---

## 🚀 Project Ideas to Build

| Project | Concepts Practiced |
|---------|------------------|
| **Counter App** | useState, events |
| **Todo List** | useState, lists, map, filter |
| **Weather App** | useEffect, fetch, API |
| **Quiz App** | useState, conditional rendering, useReducer |
| **Blog** | React Router, useParams, useFetch |
| **E-commerce Cart** | Context API, useReducer |
| **Dashboard** | All concepts combined |

---

*Happy Learning! ⚛️🎉*
