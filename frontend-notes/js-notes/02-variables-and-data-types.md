# 02 — Variables and Data Types

---

## 📌 What is a Variable?

A **variable** is a named container that stores a value in memory.

> 💡 **Analogy:** A variable is like a labeled box. You put something in the box, and you can open it later to use or change what's inside.

---

## 📦 Declaring Variables: `var`, `let`, `const`

JavaScript has **three ways** to declare variables:

```javascript
var   name = "Manoj";   // Old way — avoid in modern JS
let   age  = 20;        // Modern, can be reassigned
const PI   = 3.14159;   // Modern, CANNOT be reassigned
```

### Differences At a Glance:

| Keyword | Re-assignable | Block-scoped | When to Use |
|---------|--------------|-------------|------------|
| `var`   | ✅ Yes | ❌ No (function-scoped) | ❌ Avoid (legacy) |
| `let`   | ✅ Yes | ✅ Yes | ✅ Use for values that change |
| `const` | ❌ No  | ✅ Yes | ✅ Use for values that stay the same |

> 🔑 **Rule of Thumb:** Always use `const` first. If the value needs to change, use `let`. Never use `var`.

```javascript
// Good practice:
const username = "Manoj";    // won't change
let score = 0;               // will change during the game
score = 100;                 // ✅ allowed (let can be reassigned)

const PI = 3.14;
PI = 3;                      // ❌ TypeError: Assignment to constant variable
```

---

## 🔢 The 8 Data Types in JavaScript

JavaScript has **7 primitive types** and **1 object type**.

### Primitive Types

| Type | Example | Description |
|------|---------|-------------|
| `String` | `"Hello"`, `'World'` | Text |
| `Number` | `42`, `3.14`, `-7` | Numbers (int & float) |
| `Boolean` | `true`, `false` | Yes/No, On/Off |
| `Undefined` | `undefined` | Variable declared but not assigned |
| `Null` | `null` | Intentionally empty value |
| `BigInt` | `9007199254740991n` | Very large integers |
| `Symbol` | `Symbol("id")` | Unique identifiers (advanced) |

### Object Type

| Type | Example | Description |
|------|---------|-------------|
| `Object` | `{ name: "Manoj" }`, `[1, 2, 3]` | Collections of data |

---

## 🔡 1. Strings

Strings store **text** and are written in quotes.

```javascript
let firstName = "Manoj";
let lastName  = 'Neupane';
let greeting  = `Hello, ${firstName}!`; // Template literal (modern ✅)

console.log(greeting); // Hello, Manoj!
```

### String Methods (Most Common):

```javascript
let str = "Hello, World!";

str.length;            // 13 — number of characters
str.toUpperCase();     // "HELLO, WORLD!"
str.toLowerCase();     // "hello, world!"
str.includes("World"); // true
str.startsWith("He");  // true
str.endsWith("!");     // true
str.indexOf("World");  // 7 — position of first match
str.slice(0, 5);       // "Hello" — extract a portion
str.replace("World", "Nepal"); // "Hello, Nepal!"
str.trim();            // removes whitespace from both ends
str.split(", ");       // ["Hello", "World!"] — split into array
```

### Template Literals (Backticks `` ` ``)

The modern way to embed variables and expressions in strings:

```javascript
const name = "Manoj";
const age  = 20;

// Old way (concatenation):
console.log("My name is " + name + " and I am " + age + " years old.");

// Modern way (template literal) ✅:
console.log(`My name is ${name} and I am ${age} years old.`);

// Multi-line strings with template literals:
const message = `
  Dear ${name},
  Welcome to JavaScript!
`;
```

---

## 🔢 2. Numbers

JavaScript has only **one number type** — it covers both integers and decimals.

```javascript
let age   = 25;        // integer
let price = 9.99;      // decimal (float)
let temp  = -5;        // negative
let big   = 1_000_000; // underscore for readability ✅ (ES2021)

// Special number values:
Infinity    // 1 / 0
-Infinity   // -1 / 0
NaN         // "Not a Number" — result of invalid math
```

### Number Methods:

```javascript
let n = 3.14159;

n.toFixed(2);       // "3.14" — round to 2 decimal places (returns string)
n.toString();       // "3.14159" — convert to string
Math.round(n);      // 3 — round to nearest integer
Math.floor(n);      // 3 — round down
Math.ceil(n);       // 4 — round up
Math.abs(-5);       // 5 — absolute value
Math.max(1, 5, 3);  // 5 — maximum
Math.min(1, 5, 3);  // 1 — minimum
Math.sqrt(16);      // 4 — square root
Math.pow(2, 8);     // 256 — power (2^8)
Math.random();      // random number between 0 and 1

// Random integer between 1 and 10:
Math.floor(Math.random() * 10) + 1;
```

---

## ✅ 3. Booleans

A boolean has only two values: `true` or `false`.

```javascript
let isLoggedIn = true;
let isAdmin    = false;

let age = 20;
let canVote = age >= 18; // true — a comparison returns a boolean
```

---

## ❓ 4. Undefined and Null

```javascript
// Undefined: variable declared but not given a value
let score;
console.log(score); // undefined

// Null: intentionally set to "nothing"
let selectedUser = null; // no user selected yet
```

| | `undefined` | `null` |
|-|-------------|--------|
| **Meaning** | Variable exists but has no value | Variable intentionally set to empty |
| **Set by** | JavaScript (automatically) | Developer (manually) |
| **Type** | `undefined` | `object` (this is a historical bug in JS!) |

---

## 🔍 Checking Types: `typeof`

Use `typeof` to find out the data type of a value:

```javascript
typeof "Hello"       // "string"
typeof 42            // "number"
typeof true          // "boolean"
typeof undefined     // "undefined"
typeof null          // "object" ⚠️ (JS quirk — null is NOT an object)
typeof { a: 1 }      // "object"
typeof [1, 2, 3]     // "object" ⚠️ (arrays are objects in JS)
typeof function(){}  // "function"
```

---

## 🔄 Type Conversion

### Implicit (Automatic) Coercion:

```javascript
// JS automatically converts types — can be surprising!
"5" + 3        // "53"  ← string concatenation (number becomes string)
"5" - 3        // 2     ← numeric subtraction (string becomes number)
true + 1       // 2     ← true is treated as 1
false + 1      // 1     ← false is treated as 0
```

### Explicit Conversion:

```javascript
// To Number:
Number("42")     // 42
Number(true)     // 1
Number(false)    // 0
Number("")       // 0
Number("hello")  // NaN
parseInt("42px") // 42 — parses integer from a string
parseFloat("3.14em") // 3.14 — parses decimal

// To String:
String(42)       // "42"
String(true)     // "true"
(42).toString()  // "42"

// To Boolean:
Boolean(0)       // false
Boolean("")      // false
Boolean(null)    // false
Boolean(undefined) // false
Boolean(NaN)     // false
// Everything else is true:
Boolean(1)       // true
Boolean("hi")    // true
Boolean([])      // true
Boolean({})      // true
```

### Falsy Values (Only 6 in JavaScript):
```javascript
false, 0, "", null, undefined, NaN
```

> ⚠️ Everything else is **truthy**. An empty array `[]` and empty object `{}` are truthy!

---

## ✅ Key Takeaways

- Use `const` by default, `let` when the value needs to change, never `var`.
- JavaScript has **7 primitive types** + `object`.
- Use template literals (`` ` `` backticks) for strings with variables.
- `typeof` tells you the data type of any value.
- JavaScript does automatic type conversion — be careful with `+` when mixing strings and numbers.
- Only **6 falsy values** exist: `false`, `0`, `""`, `null`, `undefined`, `NaN`.

---

## 🏋️ Practice Tasks

### Task 1 — Personal Info Variables
Declare variables for: name (`const`), age (`let`), city (`const`), isStudent (`const`).
Use a template literal to log a sentence like:
```
"Hi! I'm Manoj, 20 years old from Kathmandu. Student: true"
```

---

### Task 2 — String Method Challenge
Given `const str = "  Hello, JavaScript World!  "`, use string methods to:
1. Remove the whitespace from both ends (`trim`)
2. Count total characters (after trim)
3. Replace `"JavaScript"` with `"JS"`
4. Convert to lowercase
5. Check if it starts with `"hello"` (case-insensitive tip: convert first!)

---

### Task 3 — Type Detective
```javascript
const values = [42, "42", true, null, undefined, 0, "", NaN, [], {}];
```
Loop through `values` and for each one log: `"value: X | type: Y | truthy/falsy: Z"`

Expected output format:
```
value: 42        | type: number    | truthy
value: "42"      | type: string    | truthy
value: null      | type: object    | falsy
...
```

---

> ➡️ **Next:** `03-operators.md` — Performing calculations and comparisons.
