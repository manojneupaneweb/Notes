# 11 — Modern JavaScript (ES6+) Features

---

## 📌 What is ES6+?

**ES6** (ECMAScript 2015) was a major update to JavaScript that introduced many powerful features. Subsequent versions (ES7, ES8, ES9...) added more. These "modern" features are now standard in all browsers.

> 💡 You'll use these features every day in professional JavaScript development.

---

## 1️⃣ `let` and `const` (ES6)

Already covered in chapter 02, but worth noting as an ES6 feature.

```javascript
const PI  = 3.14159;  // constant
let count = 0;        // re-assignable
```

---

## 2️⃣ Template Literals (ES6) ✅

Backtick strings with embedded expressions.

```javascript
const name = "Manoj";
const age  = 20;

// Multi-line strings:
const html = `
  <div class="card">
    <h2>${name}</h2>
    <p>Age: ${age}</p>
  </div>
`;

// Expressions inside `${}`:
console.log(`${2 + 2}`);           // "4"
console.log(`${age >= 18 ? "Adult" : "Minor"}`);  // "Adult"
```

---

## 3️⃣ Arrow Functions (ES6) ✅

```javascript
// Traditional:
function add(a, b) { return a + b; }

// Arrow:
const add = (a, b) => a + b;
const square = n => n * n;
const greet  = () => "Hello!";
```

---

## 4️⃣ Destructuring (ES6) ✅

Already covered in Arrays (ch.07) and Objects (ch.08).

```javascript
// Array destructuring:
const [first, second] = [10, 20];

// Object destructuring:
const { name, age } = { name: "Manoj", age: 20 };

// Function parameter destructuring:
function display({ name, age }) {
  console.log(`${name} is ${age}`);
}
display({ name: "Manoj", age: 20 });
```

---

## 5️⃣ Spread and Rest Operator `...` (ES6) ✅

### Spread (expand):
```javascript
// Arrays:
const a = [1, 2, 3];
const b = [...a, 4, 5];     // [1, 2, 3, 4, 5]
const copy = [...a];         // shallow copy

// Objects:
const user = { name: "Manoj" };
const updated = { ...user, age: 20 }; // { name: "Manoj", age: 20 }

// Function calls:
Math.max(...[5, 1, 9, 3]); // 9
```

### Rest (collect remaining):
```javascript
// Function parameters:
function sum(...numbers) {
  return numbers.reduce((acc, n) => acc + n, 0);
}
sum(1, 2, 3, 4, 5); // 15

// Array destructuring:
const [head, ...tail] = [1, 2, 3, 4];
// head = 1, tail = [2, 3, 4]

// Object destructuring:
const { name, ...rest } = { name: "Manoj", age: 20, city: "KTM" };
// name = "Manoj", rest = { age: 20, city: "KTM" }
```

---

## 6️⃣ Short-hand Object Properties (ES6)

When the variable name matches the key name:

```javascript
const name = "Manoj";
const age  = 20;

// Old way:
const person = { name: name, age: age };

// Shorthand ✅:
const person = { name, age };  // same result!

// Shorthand methods:
const obj = {
  // Old:
  greet: function() { ... },
  // Shorthand ✅:
  greet() { ... }
};
```

---

## 7️⃣ Optional Chaining `?.` (ES2020) ✅

Safely access nested properties that might not exist.

```javascript
const user = {
  name: "Manoj",
  address: {
    city: "Kathmandu"
  }
};

// Without optional chaining (throws error if address is undefined):
user.address.city    // "Kathmandu"
user.phone.number    // ❌ TypeError!

// With optional chaining ✅:
user?.address?.city  // "Kathmandu"
user?.phone?.number  // undefined (no error)

// Also works on methods:
user.greet?.()       // undefined if greet doesn't exist

// And arrays:
user.tags?.[0]       // undefined if tags doesn't exist
```

---

## 8️⃣ Nullish Coalescing `??` (ES2020) ✅

```javascript
const value = null ?? "default";    // "default"
const score = 0    ?? 100;          // 0 (not "falsy fallback"!)
const name  = ""   ?? "Anonymous";  // "" (empty string is kept)
```

---

## 9️⃣ Logical Assignment Operators (ES2021)

```javascript
// ||= : assign if current value is falsy
let a = null;
a ||= "default";  // a = "default"

// &&= : assign if current value is truthy
let b = "hello";
b &&= b.toUpperCase();  // b = "HELLO"

// ??= : assign only if null or undefined
let c = 0;
c ??= 42;  // c = 0 (0 is not null/undefined)
```

---

## 🔟 Array Destructuring in Loops

```javascript
const students = [["Manoj", 90], ["Sita", 85], ["Ram", 72]];

for (const [name, score] of students) {
  console.log(`${name}: ${score}`);
}
```

---

## 1️⃣1️⃣ Modules: `import` / `export` (ES6) ✅

Split code across multiple files.

**math.js:**
```javascript
// Named exports:
export const PI = 3.14159;
export function add(a, b) { return a + b; }
export function multiply(a, b) { return a * b; }

// Default export (one per file):
export default function subtract(a, b) { return a - b; }
```

**main.js:**
```javascript
// Import named exports:
import { PI, add, multiply } from "./math.js";

// Import default export (any name you want):
import subtract from "./math.js";

// Import everything as namespace:
import * as Math from "./math.js";
Math.add(1, 2);

// Rename on import:
import { add as sum } from "./math.js";
```

**In HTML (must use `type="module"`):**
```html
<script type="module" src="main.js"></script>
```

---

## 1️⃣2️⃣ `Map` and `Set` Collections (ES6)

### `Set` — Unique values only:

```javascript
const set = new Set([1, 2, 3, 2, 1]);  // {1, 2, 3} — duplicates removed!

set.add(4);       // {1, 2, 3, 4}
set.has(3);       // true
set.delete(2);    // {1, 3, 4}
set.size;         // 3

// ✅ Super useful: Remove duplicates from an array:
const arr = [1, 2, 3, 2, 1, 3];
const unique = [...new Set(arr)]; // [1, 2, 3]

// Iterate:
for (const val of set) {
  console.log(val);
}
```

### `Map` — Key-value pairs (any key type):

```javascript
const map = new Map();

// Keys can be any type (unlike objects!):
map.set("name", "Manoj");
map.set(1, "one");
map.set(true, "yes");
map.set({ id: 1 }, "object key");

map.get("name");    // "Manoj"
map.has("name");    // true
map.delete("name");
map.size;           // number of entries

// Iterate:
for (const [key, value] of map) {
  console.log(`${key}: ${value}`);
}
```

---

## 1️⃣3️⃣ Symbol (ES6)

Creates a unique, immutable identifier. Rarely used in everyday code.

```javascript
const id1 = Symbol("id");
const id2 = Symbol("id");
id1 === id2  // false — every Symbol is unique!

// Common use: prevent property name collisions:
const ID = Symbol("id");
const obj = {
  [ID]: 123,
  name: "Manoj"
};
obj[ID]; // 123
```

---

## 1️⃣4️⃣ WeakMap and WeakSet (Advanced)

Like `Map` and `Set` but hold **weak references** — objects inside can be garbage-collected.

```javascript
const weakMap = new WeakMap();
const key = {};
weakMap.set(key, "value");
// If 'key' has no other references, it can be garbage-collected
```

---

## 📊 Modern Features Quick Reference

| Feature | ES Version | Syntax |
|---------|-----------|--------|
| `let` / `const` | ES6 | `const x = 1` |
| Template literals | ES6 | `` `Hello ${name}` `` |
| Arrow functions | ES6 | `(a, b) => a + b` |
| Destructuring | ES6 | `const { a, b } = obj` |
| Spread / Rest | ES6 | `...args` |
| Classes | ES6 | `class Foo {}` |
| Modules | ES6 | `import / export` |
| `Promise` | ES6 | `.then().catch()` |
| `async/await` | ES8 | `await fetch(...)` |
| Optional chaining | ES2020 | `obj?.prop` |
| Nullish coalescing | ES2020 | `a ?? b` |
| Logical assignment | ES2021 | `a ??= b` |
| `Array.at()` | ES2022 | `arr.at(-1)` |

---

## ✅ Key Takeaways

- Modern JS (ES6+) is much more expressive and less verbose.
- **Must know:** template literals, arrow functions, destructuring, spread/rest, optional chaining, `??`.
- **For large apps:** modules (`import`/`export`) keep code organized.
- **For unique collections:** `Set`; **for map-like structures with any key type:** `Map`.

---

## 🏋️ Practice Tasks

### Task 1 — Refactor to Modern JS
Rewrite this old-style code using **ES6+ features** (arrow functions, destructuring, template literals, default params, spread):
```javascript
// OLD CODE — rewrite this:
function greetUser(user) {
  var name = user.name;
  var age  = user.age;
  var city = user.address.city;
  return "Hello " + name + "! You are " + age + " from " + city;
}

function mergeArrays(a, b) {
  return a.concat(b);
}

function sumAll() {
  var args = Array.prototype.slice.call(arguments);
  return args.reduce(function(acc, n) { return acc + n; }, 0);
}
```

---

### Task 2 — Module System
Split this code into 3 files using `import`/`export`:
```javascript
// Everything in one file — separate into: math.js, utils.js, main.js
const PI = 3.14159;
function circleArea(r) { return PI * r * r; }
function capitalize(str) { return str[0].toUpperCase() + str.slice(1); }
function clamp(n, min, max) { return Math.min(Math.max(n, min), max); }

console.log(circleArea(5));
console.log(capitalize("hello"));
console.log(clamp(150, 0, 100));
```

---

### Task 3 — Map and Set in Practice
```javascript
const votes = ["apple", "banana", "apple", "cherry", "banana", "apple", "cherry", "cherry", "cherry"];
```
1. Use a `Map` to count how many votes each fruit got
2. Use a `Set` to get the list of unique fruits voted for
3. Find the **winner** (most votes) using the Map
4. Display: `"🏆 Winner: cherry with 4 votes"`

---

> 🎉 **Congratulations!** You've covered the core of JavaScript. Practice by building projects!
