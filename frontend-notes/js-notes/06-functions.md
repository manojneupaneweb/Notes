# 06 — Functions

---

## 📌 What is a Function?

A **function** is a reusable block of code that performs a specific task. Instead of writing the same code multiple times, you define it once and call it whenever you need it.

> 💡 **Analogy:** A function is like a recipe. You write the recipe once (define the function), and cook it as many times as you want (call the function).

---

## 📝 Function Declaration

The traditional way to define a function.

```javascript
// Define the function:
function greet() {
  console.log("Hello, World!");
}

// Call (invoke) the function:
greet();         // Hello, World!
greet();         // Hello, World! (can call multiple times)
```

---

## 📥 Parameters and Arguments

**Parameters** are placeholders defined in the function. **Arguments** are the actual values passed when calling the function.

```javascript
// Parameters: name, age
function greet(name, age) {
  console.log(`Hello, ${name}! You are ${age} years old.`);
}

// Arguments: "Manoj", 20
greet("Manoj", 20);  // Hello, Manoj! You are 20 years old.
greet("Sita",  25);  // Hello, Sita! You are 25 years old.
```

### Default Parameters:

```javascript
function greet(name = "Guest") {
  console.log(`Hello, ${name}!`);
}

greet("Manoj"); // Hello, Manoj!
greet();        // Hello, Guest! (uses default)
```

---

## 📤 The `return` Statement

Functions can **return** a value that you can use elsewhere.

```javascript
function add(a, b) {
  return a + b;  // sends back the result
}

const result = add(5, 3);  // result = 8
console.log(result);        // 8
console.log(add(10, 20));   // 30

// ⚠️ Code after return never runs:
function example() {
  return 42;
  console.log("This never executes!"); // ❌ unreachable
}
```

### Functions Without `return`:
If a function has no `return` statement, it returns `undefined`.

```javascript
function sayHello() {
  console.log("Hello!");
}
const val = sayHello(); // prints "Hello!"
console.log(val);       // undefined
```

---

## 📦 Function Expression

A function stored in a variable.

```javascript
const add = function(a, b) {
  return a + b;
};

console.log(add(3, 4)); // 7
```

### Function Declaration vs Expression:

| | Declaration | Expression |
|-|------------|-----------|
| Syntax | `function name() {}` | `const name = function() {}` |
| Hoisting | ✅ Can be called before defined | ❌ Cannot be called before defined |
| Named | Always has a name | Function can be anonymous |

---

## ⚡ Arrow Functions (ES6) ✅

Modern, shorter syntax for functions. Very commonly used in modern JavaScript.

```javascript
// Regular function:
function add(a, b) {
  return a + b;
}

// Arrow function:
const add = (a, b) => {
  return a + b;
};

// Shorthand (implicit return — for single expressions):
const add = (a, b) => a + b;

// One parameter — parentheses optional:
const double = n => n * 2;
const greet  = name => `Hello, ${name}!`;

// No parameters — must use empty parentheses:
const sayHi = () => console.log("Hi!");
```

### Arrow Function Cheatsheet:

```javascript
// Multiple lines: use {} and explicit return
const calculate = (a, b) => {
  const result = a * b;
  return result;
};

// Single expression: no {} and no return needed
const square = n => n * n;

// Returning an object (wrap in parentheses):
const getUser = name => ({ name: name, role: "user" });
```

---

## 🔝 Hoisting

**Function declarations** are hoisted — they can be called before they're defined:

```javascript
// This works! (function declaration is hoisted)
greet(); // ✅ Hello!

function greet() {
  console.log("Hello!");
}

// This DOES NOT work (function expression / arrow function NOT hoisted)
sayHi(); // ❌ ReferenceError

const sayHi = () => console.log("Hi!");
```

---

## 🧅 Scope

**Scope** determines where a variable is accessible.

```javascript
const globalVar = "I'm global"; // accessible everywhere

function myFunction() {
  const localVar = "I'm local"; // only inside this function
  console.log(globalVar);  // ✅ can access global
  console.log(localVar);   // ✅ can access local
}

myFunction();
console.log(globalVar); // ✅ accessible
console.log(localVar);  // ❌ ReferenceError: not accessible outside function
```

### Block Scope (`let` and `const`):

```javascript
if (true) {
  let blockVar   = "block scoped";
  const another  = "also block scoped";
  var legacyVar  = "function scoped"; // var ignores blocks!
}

console.log(blockVar);  // ❌ ReferenceError
console.log(legacyVar); // ✅ accessible (var leaks out of blocks!)
```

---

## 🔄 Callback Functions

A function passed as an **argument to another function**, to be called later.

```javascript
function doMath(a, b, operation) {
  return operation(a, b);  // calls the passed function
}

const add      = (a, b) => a + b;
const multiply = (a, b) => a * b;

doMath(3, 4, add);       // 7
doMath(3, 4, multiply);  // 12

// Most common real-world example: setTimeout
setTimeout(() => {
  console.log("This runs after 2 seconds!");
}, 2000);
```

---

## 🌀 IIFE — Immediately Invoked Function Expression

A function that runs immediately when defined. Used to avoid polluting the global scope.

```javascript
(function() {
  const secret = "I run immediately!";
  console.log(secret);
})();

// Arrow function IIFE:
(() => {
  console.log("Also runs immediately!");
})();
```

---

## ♻️ Pure Functions

A **pure function** always produces the same output for the same input and has no side effects. Best practice in functional programming.

```javascript
// ✅ Pure function:
function add(a, b) {
  return a + b; // no side effects, same output every time
}

// ❌ Impure function (modifies external state):
let total = 0;
function addToTotal(n) {
  total += n; // modifies external variable — side effect!
}
```

---

## ✅ Key Takeaways

| Concept | Summary |
|---------|---------|
| Function | Reusable block of code |
| Parameters | Inputs defined in the function |
| Arguments | Values passed when calling |
| `return` | Sends a value back from a function |
| Arrow functions | Shorter, modern syntax (`=>`) |
| Hoisting | Declarations are hoisted; expressions are not |
| Scope | Where a variable is accessible |
| Callback | Function passed as an argument |

---

## 🏋️ Practice Tasks

### Task 1 — Temperature Converter
Write **arrow functions** for temperature conversion:
```javascript
const celsiusToFahrenheit = (c) => /* your formula */;
const fahrenheitToCelsius = (f) => /* your formula */;
const celsiusToKelvin     = (c) => /* your formula */;

// Test:
console.log(celsiusToFahrenheit(100)); // 212
console.log(fahrenheitToCelsius(32));  // 0
console.log(celsiusToKelvin(0));       // 273.15
```

---

### Task 2 — Palindrome Checker
Write a function `isPalindrome(word)` that returns `true` if the word reads the same forwards and backwards.
```javascript
isPalindrome("racecar"); // true
isPalindrome("hello");   // false
isPalindrome("madam");   // true
isPalindrome("level");   // true
```
**Hint:** Use `.split("").reverse().join("")`

---

### Task 3 — Higher-Order Function Practice
Write a function `applyTwice(fn, value)` that applies a function to a value **twice**.
```javascript
const double  = n => n * 2;
const addTen  = n => n + 10;
const square  = n => n * n;

applyTwice(double, 3);   // double(double(3)) = 12
applyTwice(addTen, 5);   // addTen(addTen(5)) = 25
applyTwice(square, 2);   // square(square(2)) = 16
```

---

> ➡️ **Next:** `07-arrays.md` — Working with lists of data.
