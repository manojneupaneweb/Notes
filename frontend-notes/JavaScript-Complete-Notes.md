# 📚 JavaScript — Complete Reference Notes
### Frontend Development · Beginner to Advanced

> **Author:** Manoj Neupane  
> **Last Updated:** May 2026  
> **Goal:** A complete, detailed reference for JavaScript — from the very basics to modern ES6+ features.

---

## 📑 Table of Contents

- [01 — Introduction to JavaScript](#01--introduction-to-javascript)
- [02 — Variables and Data Types](#02--variables-and-data-types)
- [03 — Operators](#03--operators)
- [04 — Control Flow](#04--control-flow-if-else-switch)
- [05 — Loops](#05--loops)
- [06 — Functions](#06--functions)
- [07 — Arrays](#07--arrays)
- [08 — Objects](#08--objects)
- [09 — DOM Manipulation](#09--dom-manipulation)
- [10 — Async JavaScript](#10--async-javascript-callbacks-promises-asyncawait)
- [11 — Modern JavaScript (ES6+)](#11--modern-javascript-es6-features)

---

## 01 — Introduction to JavaScript

### 📌 What is JavaScript?

**JavaScript** (JS) is the **programming language of the web**.

- It makes web pages **interactive and dynamic**.
- While HTML gives structure and CSS gives style, **JavaScript gives behavior**.
- JavaScript can update content, respond to clicks, validate forms, fetch data, animate elements, and much more.
- It runs directly in the **browser** (no installation needed).

> 💡 **Analogy:** If HTML is the skeleton and CSS is the clothing, JavaScript is the **muscles and brain** — it makes things move and respond.

### 🌐 Where Does JavaScript Run?

| Environment | Examples | Used For |
|-------------|---------|---------|
| **Browser** (Client-side) | Chrome, Firefox, Edge | DOM manipulation, UI, animations |
| **Server** (Node.js) | Node.js, Deno | Backend APIs, databases, file systems |

### 📄 How to Add JavaScript to a Web Page

#### 1. Inline JavaScript (Not Recommended)
```html
<button onclick="alert('Hello!')">Click Me</button>
```

#### 2. Internal JavaScript
```html
<body>
  <h1>Hello!</h1>
  <script>
    console.log("Page loaded!");
  </script>
</body>
```

#### 3. External JavaScript ✅ (Best Practice)

**script.js:**
```javascript
console.log("Hello from external JS!");
```

**index.html:**
```html
<body>
  <h1>Hello!</h1>
  <script src="script.js"></script>
</body>
```

> ⚠️ **Always place `<script>` before `</body>`** — ensures HTML loads first.

### 🖥️ Your First Program
```javascript
console.log("Hello, World!");
```

Open the **browser Console** with `F12` → Console tab.

### 📊 JavaScript vs HTML vs CSS

| Language | Role | Example |
|----------|------|---------|
| **HTML** | Structure | `<h1>Hello</h1>` |
| **CSS** | Style | `color: blue;` |
| **JavaScript** | Behavior | `el.addEventListener("click", fn)` |

---

## 02 — Variables and Data Types

### 📦 Declaring Variables

```javascript
var   name = "Manoj";   // Old — avoid
let   age  = 20;        // Reassignable
const PI   = 3.14159;   // Cannot be reassigned
```

| Keyword | Re-assignable | Block-scoped | When to Use |
|---------|--------------|-------------|------------|
| `var`   | ✅ Yes | ❌ No | ❌ Avoid |
| `let`   | ✅ Yes | ✅ Yes | ✅ Changing values |
| `const` | ❌ No  | ✅ Yes | ✅ Default choice |

> 🔑 **Rule:** Always use `const` first. Only use `let` if the value needs to change.

### 🔢 Primitive Data Types

| Type | Example | Description |
|------|---------|-------------|
| `String` | `"Hello"` | Text |
| `Number` | `42`, `3.14` | Numbers (int & float) |
| `Boolean` | `true`, `false` | Yes/No |
| `Undefined` | `undefined` | Declared but not assigned |
| `Null` | `null` | Intentionally empty |
| `BigInt` | `9999n` | Very large integers |
| `Symbol` | `Symbol("id")` | Unique identifiers |

### 🔡 Strings

```javascript
let str = "Hello, World!";

str.length;            // 13
str.toUpperCase();     // "HELLO, WORLD!"
str.toLowerCase();     // "hello, world!"
str.includes("World"); // true
str.slice(0, 5);       // "Hello"
str.replace("World", "Nepal"); // "Hello, Nepal!"
str.trim();            // remove whitespace from ends
str.split(", ");       // ["Hello", "World!"]
```

**Template Literals (Backticks ✅):**
```javascript
const name = "Manoj";
const age  = 20;
console.log(`My name is ${name} and I am ${age} years old.`);
```

### 🔢 Numbers

```javascript
Math.round(3.7);    // 4
Math.floor(3.7);    // 3
Math.ceil(3.2);     // 4
Math.abs(-5);       // 5
Math.max(1, 5, 3);  // 5
Math.min(1, 5, 3);  // 1
Math.random();      // 0 to 1
Math.floor(Math.random() * 10) + 1; // random 1-10
```

### 🔍 `typeof` Operator

```javascript
typeof "Hello"   // "string"
typeof 42        // "number"
typeof true      // "boolean"
typeof undefined // "undefined"
typeof null      // "object" ⚠️ (JS quirk)
typeof []        // "object"
typeof {}        // "object"
```

### 🔄 Type Conversion

```javascript
Number("42")     // 42
Number(true)     // 1
String(42)       // "42"
Boolean(0)       // false
Boolean("hi")    // true
parseInt("42px") // 42
```

**Falsy values (only 6):** `false`, `0`, `""`, `null`, `undefined`, `NaN`

---

## 03 — Operators

### ➕ Arithmetic

```javascript
10 + 3   // 13
10 - 3   // 7
10 * 3   // 30
10 / 3   // 3.333...
10 % 3   // 1   — remainder
10 ** 3  // 1000 — power
```

### ⚖️ Comparison — Always use `===`!

```javascript
5 === "5"   // false — strict (type matters) ✅
5 == "5"    // true  — loose (avoid!) ❌
5 !== "5"   // true
5 > 3       // true
5 >= 5      // true
```

### 🧠 Logical

```javascript
true && false   // false — AND
true || false   // true  — OR
!true           // false — NOT
null ?? "default"   // "default" — nullish coalescing
"hi" || "default"   // "hi"      — OR fallback
```

### ❓ Ternary

```javascript
const status = age >= 18 ? "Adult" : "Minor";
```

---

## 04 — Control Flow: if, else, switch

### 🔀 if / else if / else

```javascript
const score = 72;

if (score >= 90) {
  console.log("Grade: A");
} else if (score >= 75) {
  console.log("Grade: B");
} else if (score >= 60) {
  console.log("Grade: C");
} else {
  console.log("Grade: F");
}
```

### 🔀 switch

```javascript
const day = "Monday";

switch (day) {
  case "Monday":
    console.log("Work week starts!");
    break;
  case "Saturday":
  case "Sunday":
    console.log("Weekend!");
    break;
  default:
    console.log("Regular day.");
}
```

> ⚠️ Always use `break` in switch cases. Switch uses `===` (strict equality).

---

## 05 — Loops

### 🔁 for loop

```javascript
for (let i = 1; i <= 5; i++) {
  console.log(i); // 1 2 3 4 5
}
```

### 🔁 while loop

```javascript
let i = 1;
while (i <= 5) {
  console.log(i);
  i++;
}
```

### 🔁 do...while loop

```javascript
let num;
do {
  num = prompt("Enter 1-10:");
} while (num < 1 || num > 10);
```

### 🔁 for...of (Arrays ✅)

```javascript
const fruits = ["Apple", "Banana", "Mango"];
for (const fruit of fruits) {
  console.log(fruit);
}
```

### 🔁 for...in (Objects)

```javascript
const person = { name: "Manoj", age: 20 };
for (const key in person) {
  console.log(`${key}: ${person[key]}`);
}
```

### ⏹️ break and continue

```javascript
// break — exit loop:
for (let i = 1; i <= 10; i++) {
  if (i === 5) break; // stops at 4
}

// continue — skip iteration:
for (let i = 1; i <= 10; i++) {
  if (i % 2 === 0) continue; // skip evens
  console.log(i); // 1 3 5 7 9
}
```

---

## 06 — Functions

### 📝 Function Declaration

```javascript
function greet(name = "Guest") {
  return `Hello, ${name}!`;
}
greet("Manoj"); // "Hello, Manoj!"
greet();        // "Hello, Guest!"
```

### 📦 Function Expression

```javascript
const add = function(a, b) {
  return a + b;
};
```

### ⚡ Arrow Functions ✅

```javascript
const add      = (a, b) => a + b;
const square   = n => n * n;
const greet    = () => "Hello!";

// Multi-line:
const calculate = (a, b) => {
  const result = a * b;
  return result;
};
```

### 🔝 Hoisting

```javascript
greet(); // ✅ works — function declarations are hoisted

function greet() { console.log("Hello!"); }

sayHi(); // ❌ error — expressions are NOT hoisted
const sayHi = () => "Hi!";
```

### 🧅 Scope

```javascript
const global = "global"; // accessible everywhere

function myFn() {
  const local = "local"; // only inside myFn
  console.log(global);   // ✅
}

console.log(local); // ❌ ReferenceError
```

### 🔄 Callbacks

```javascript
function doMath(a, b, operation) {
  return operation(a, b);
}
doMath(3, 4, (a, b) => a + b);  // 7
doMath(3, 4, (a, b) => a * b);  // 12

setTimeout(() => console.log("After 2s!"), 2000);
```

---

## 07 — Arrays

### 📦 Create and Access

```javascript
const fruits = ["Apple", "Banana", "Mango"];
fruits[0]             // "Apple"
fruits.at(-1)         // "Mango" (last element)
fruits.length         // 3
```

### 🔧 Add / Remove Elements

```javascript
fruits.push("Orange");     // add to end → [..., "Orange"]
fruits.pop();              // remove from end
fruits.unshift("Grape");   // add to start
fruits.shift();            // remove from start
fruits.splice(1, 0, "Kiwi"); // insert at index 1
fruits.splice(1, 1);          // remove 1 element at index 1
```

### 🔄 Transform (Returns New Array)

```javascript
const nums = [1, 2, 3, 4, 5];

nums.map(n => n * 2);           // [2, 4, 6, 8, 10]
nums.filter(n => n > 3);        // [4, 5]
nums.reduce((acc, n) => acc + n, 0); // 15
nums.slice(1, 3);               // [2, 3]
```

### 🔍 Search

```javascript
nums.includes(3);           // true
nums.indexOf(3);            // 2
nums.find(n => n > 3);      // 4
nums.findIndex(n => n > 3); // 3
nums.every(n => n > 0);     // true
nums.some(n => n > 4);      // true
```

### 📊 Destructuring

```javascript
const [first, second, ...rest] = [10, 20, 30, 40];
// first=10, second=20, rest=[30,40]
```

### 🌐 Spread

```javascript
const merged = [...arr1, ...arr2];
const copy   = [...arr1];
Math.max(...[5, 3, 9]);  // 9
```

---

## 08 — Objects

### 📦 Create and Access

```javascript
const person = {
  name: "Manoj",
  age: 20,
  greet() {
    return `Hi, I'm ${this.name}!`;
  }
};

person.name         // "Manoj" — dot notation
person["name"]      // "Manoj" — bracket notation
person.greet()      // "Hi, I'm Manoj!"
```

### 🔧 Add / Update / Delete

```javascript
person.email = "manoj@example.com"; // add
person.age   = 21;                  // update
delete person.email;                // delete
```

### 🔍 Object Methods

```javascript
Object.keys(person)    // ["name", "age"]
Object.values(person)  // ["Manoj", 20]
Object.entries(person) // [["name","Manoj"], ["age",20]]

const merged = { ...obj1, ...obj2 }; // merge with spread
```

### 📊 Destructuring

```javascript
const { name, age, country = "Nepal" } = person;
// country uses default since person has no 'country'

// Rename:
const { name: fullName } = person;
```

### ⛓️ Optional Chaining `?.`

```javascript
user?.address?.city   // undefined if address doesn't exist
user?.greet?.()       // undefined if greet doesn't exist
```

### 🏛️ Classes

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age  = age;
  }

  greet() {
    return `Hi, I'm ${this.name}!`;
  }

  get info() {
    return `${this.name}, ${this.age}`;
  }
}

const p = new Person("Manoj", 20);
p.greet();  // "Hi, I'm Manoj!"
p.info;     // "Manoj, 20"
```

---

## 09 — DOM Manipulation

### 🔍 Selecting Elements

```javascript
document.getElementById("id")            // one element
document.querySelector(".class")         // first match
document.querySelectorAll("p")           // all matches (NodeList)
```

### ✏️ Reading / Changing Content

```javascript
el.textContent = "New text";           // safe ✅
el.innerHTML   = "<em>New</em>";       // parses HTML

input.value    // get input value
input.value = "text" // set input value
```

### 🎨 Styles and Classes

```javascript
el.style.color = "red";
el.style.display = "none";

el.classList.add("active");
el.classList.remove("active");
el.classList.toggle("active");
el.classList.contains("active"); // true/false
```

### 🏗️ Create / Insert / Remove Elements

```javascript
const p = document.createElement("p");
p.textContent = "Hello!";

parent.appendChild(p);
parent.prepend(p);
reference.before(p);
reference.after(p);

el.remove();
```

### 🖱️ Events

```javascript
btn.addEventListener("click", (e) => {
  console.log(e.target);       // element clicked
  e.preventDefault();          // stop default action
  e.stopPropagation();         // stop event bubbling
});

// Common events:
// click, dblclick, mouseover, mouseout
// keydown, keyup, input, change, submit
// focus, blur, scroll, resize, load
```

**Event Delegation ✅:**
```javascript
list.addEventListener("click", (e) => {
  if (e.target.tagName === "LI") {
    e.target.classList.toggle("done");
  }
});
```

---

## 10 — Async JavaScript: Callbacks, Promises, Async/Await

### ⏰ setTimeout / setInterval

```javascript
setTimeout(() => console.log("After 2s"), 2000);

const id = setInterval(() => console.log("Every 1s"), 1000);
clearInterval(id); // stop it
```

### 🤝 Promises

```javascript
const promise = new Promise((resolve, reject) => {
  if (success) resolve("Data ✅");
  else reject("Error ❌");
});

promise
  .then(result => console.log(result))
  .catch(error => console.error(error))
  .finally(() => console.log("Done"));
```

### ✨ Async/Await ✅

```javascript
async function loadUser() {
  try {
    const res  = await fetch("https://api.example.com/users/1");
    const user = await res.json();
    console.log(user.name);
  } catch (err) {
    console.error(err.message);
  }
}
loadUser();
```

### 🌐 Fetch API

```javascript
// GET:
const res = await fetch("/api/users");
const data = await res.json();

// POST:
await fetch("/api/users", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ name: "Manoj" })
});
```

### ⚡ Promise.all — Parallel Requests

```javascript
const [users, posts] = await Promise.all([
  fetch("/users").then(r => r.json()),
  fetch("/posts").then(r => r.json())
]);
```

---

## 11 — Modern JavaScript (ES6+) Features

### Template Literals ✅
```javascript
`Hello, ${name}! You are ${age} years old.`
```

### Destructuring ✅
```javascript
const [a, b] = [1, 2];
const { name, age } = person;
```

### Spread / Rest ✅
```javascript
const merged = [...arr1, ...arr2];
const copy   = { ...obj };

function sum(...nums) { return nums.reduce((a, b) => a + b, 0); }
```

### Optional Chaining `?.` ✅
```javascript
user?.address?.city  // undefined if missing, no error
user?.greet?.()      // undefined if method missing
```

### Nullish Coalescing `??` ✅
```javascript
const name = user ?? "Guest";   // only null/undefined triggers default
const age  = 0 ?? 18;           // 0 (keeps falsy values that aren't null!)
```

### Modules ✅
```javascript
// math.js
export const PI = 3.14;
export function add(a, b) { return a + b; }
export default function subtract(a, b) { return a - b; }

// main.js
import { PI, add } from "./math.js";
import subtract from "./math.js";
```

### Set — Unique Values
```javascript
const unique = [...new Set([1, 2, 2, 3, 3])]; // [1, 2, 3]
```

### Map — Any Key Type
```javascript
const map = new Map();
map.set("name", "Manoj");
map.get("name"); // "Manoj"
```

---

## 🚀 Quick Reference Cheat Sheet

### Variables
```javascript
const name = "Manoj";   // immutable
let count  = 0;         // mutable
```

### Functions
```javascript
const fn = (a, b = 10) => a + b;
```

### Array Methods
```javascript
arr.map(fn)       // transform
arr.filter(fn)    // filter
arr.reduce(fn, 0) // collapse
arr.find(fn)      // find first
arr.includes(x)   // check exists
arr.push(x)       // add to end
arr.pop()         // remove from end
```

### Object Methods
```javascript
Object.keys(obj)    // ["key1", "key2"]
Object.values(obj)  // [val1, val2]
Object.entries(obj) // [[k,v], [k,v]]
```

### DOM
```javascript
document.querySelector("selector")
el.textContent = "..."
el.classList.toggle("class")
el.addEventListener("event", fn)
```

### Async
```javascript
const data = await fetch(url).then(r => r.json());
```

---

*🎉 Keep practicing — JavaScript mastery comes from building real projects!*
