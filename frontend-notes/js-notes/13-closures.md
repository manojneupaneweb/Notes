# 13 — Closures

---

## 📌 What is a Closure?

A **closure** is a function that **remembers** the variables from its outer scope, even after the outer function has finished executing.

> 💡 **Analogy:** Imagine a backpack. When you leave school (outer function ends), you still carry your backpack (closure). The items in your backpack (variables) stay with you even after you've left.

```javascript
function outer() {
  const secret = "I am remembered!";  // outer variable

  function inner() {
    console.log(secret);  // inner accesses outer's variable ✅
  }

  return inner;
}

const myFn = outer();  // outer() finishes, but...
myFn();  // "I am remembered!" — closure still holds 'secret'!
```

---

## 🔍 How Closures Work

Every function in JavaScript forms a closure — it "closes over" the variables in its surrounding scope.

```javascript
function makeCounter() {
  let count = 0;  // private variable — can't be accessed from outside

  return {
    increment() { count++; },
    decrement() { count--; },
    getCount()  { return count; }
  };
}

const counter = makeCounter();

counter.increment(); // count = 1
counter.increment(); // count = 2
counter.increment(); // count = 3
counter.decrement(); // count = 2
console.log(counter.getCount()); // 2

// count is PRIVATE — no direct access:
console.log(counter.count); // undefined
```

> 🔐 This is the **Module Pattern** — using closures to create private data!

---

## 🏗️ Common Closure Use Cases

### 1. Data Privacy / Encapsulation

```javascript
function createBankAccount(initialBalance) {
  let balance = initialBalance;  // private!

  return {
    deposit(amount) {
      if (amount <= 0) throw new Error("Invalid amount");
      balance += amount;
      console.log(`Deposited Rs.${amount}. Balance: Rs.${balance}`);
    },
    withdraw(amount) {
      if (amount > balance) throw new Error("Insufficient funds");
      balance -= amount;
      console.log(`Withdrew Rs.${amount}. Balance: Rs.${balance}`);
    },
    getBalance() {
      return balance;
    }
  };
}

const account = createBankAccount(1000);
account.deposit(500);   // "Deposited Rs.500. Balance: Rs.1500"
account.withdraw(200);  // "Withdrew Rs.200. Balance: Rs.1300"
console.log(account.getBalance()); // 1300
// account.balance is undefined — private! ✅
```

---

### 2. Function Factories

Create specialized functions from a general template:

```javascript
function multiplier(factor) {
  return (number) => number * factor;  // closes over 'factor'
}

const double  = multiplier(2);
const triple  = multiplier(3);
const tenTimes = multiplier(10);

double(5);    // 10
triple(5);    // 15
tenTimes(5);  // 50

// Greeting factory:
function makeGreeter(greeting) {
  return (name) => `${greeting}, ${name}!`;
}

const sayHello   = makeGreeter("Hello");
const sayNamaste = makeGreeter("Namaste");

sayHello("Manoj");    // "Hello, Manoj!"
sayNamaste("Sita");   // "Namaste, Sita!"
```

---

### 3. Memoization (Caching Results)

```javascript
function memoize(fn) {
  const cache = {};  // closure holds the cache

  return function(...args) {
    const key = JSON.stringify(args);
    if (cache[key] !== undefined) {
      console.log("From cache!");
      return cache[key];
    }
    const result = fn(...args);
    cache[key] = result;
    return result;
  };
}

function slowSquare(n) {
  // Simulating a slow calculation
  return n * n;
}

const fastSquare = memoize(slowSquare);
fastSquare(5);  // calculates: 25
fastSquare(5);  // "From cache!" 25
fastSquare(10); // calculates: 100
```

---

### 4. Event Handlers (Very Common in React!)

```javascript
function makeButton(label) {
  let clickCount = 0;  // private to this button

  const btn = document.createElement("button");
  btn.textContent = label;

  btn.addEventListener("click", () => {
    clickCount++;  // closure remembers clickCount
    console.log(`${label} clicked ${clickCount} times`);
  });

  return btn;
}

const btn1 = makeButton("Like");
const btn2 = makeButton("Share");
// Each button has its OWN independent clickCount!
```

---

## ⚠️ Common Closure Gotcha — Loop + `var`

```javascript
// ❌ Bug with var — all buttons show "Button 3"
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000); // logs 3, 3, 3
}

// ✅ Fix 1: Use let (block-scoped — each loop has its own i)
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000); // logs 0, 1, 2 ✅
}

// ✅ Fix 2: Use a closure
for (var i = 0; i < 3; i++) {
  (function(j) {
    setTimeout(() => console.log(j), 1000); // logs 0, 1, 2 ✅
  })(i);
}
```

> 💡 This is why `let` was introduced in ES6 — to fix this exact problem!

---

## 🔗 Closure vs Regular Scope

```javascript
// Without closure — data is NOT preserved:
function makeCounter() {
  let count = 0;
  count++;
  return count;
}
makeCounter(); // 1
makeCounter(); // 1 again (resets each call)

// With closure — data IS preserved:
function makeCounter() {
  let count = 0;
  return () => ++count;
}
const counter = makeCounter();
counter(); // 1
counter(); // 2
counter(); // 3 ✅ persists between calls!
```

---

## ✅ Key Takeaways

- A closure is a function that **remembers its outer scope** even after the outer function returns.
- Closures enable **private variables** (data encapsulation).
- Used for: data privacy, function factories, memoization, event handlers.
- `let` in loops solves the classic closure-in-loop bug.
- **React uses closures constantly** — every event handler inside a component is a closure!

---

## 🏋️ Practice Tasks

### Task 1 — Persistent Counter Factory
Write a `makeCounter(start = 0, step = 1)` function that returns an object with `increment`, `decrement`, `reset`, and `value` (getter). Each counter should have its **own private count**.
```javascript
const c1 = makeCounter(10, 2);   // starts at 10, steps by 2
const c2 = makeCounter();         // starts at 0, steps by 1

c1.increment(); // 12
c1.increment(); // 14
c2.increment(); // 1
console.log(c1.value); // 14
console.log(c2.value); // 1  ← independent!
```

---

### Task 2 — Greeting Factory
Use closures to create a function factory `makeGreeter(greeting, punctuation = "!")`:
```javascript
const hello   = makeGreeter("Hello");
const namaste = makeGreeter("Namaste", " 🙏");
const bye     = makeGreeter("Goodbye", ".");

hello("Manoj");     // "Hello, Manoj!"
namaste("Sita");    // "Namaste, Sita 🙏"
bye("Ram");         // "Goodbye, Ram."
```

---

### Task 3 — Private Bank Account
Using closures (no classes!), create a `createAccount(ownerName, initialBalance)` function that returns deposit, withdraw, getBalance, and getStatement methods. Balance must be **truly private** (not accessible from outside).
```javascript
const account = createAccount("Manoj", 1000);
account.deposit(500);    // "Deposited 500. Balance: 1500"
account.withdraw(200);   // "Withdrew 200. Balance: 1300"
account.withdraw(9999);  // "Insufficient funds!"
console.log(account.getBalance()); // 1300
console.log(account.balance);      // undefined ← private!
```

---

> ➡️ **Next:** `14-json.md`
