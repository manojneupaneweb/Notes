# 05 — Loops

---

## 📌 What are Loops?

**Loops** repeat a block of code until a condition is no longer true. Instead of writing the same code 100 times, you write it once and let the loop run it.

> 💡 **Analogy:** A loop is like a "repeat" button on a music player — it keeps playing until you tell it to stop.

---

## 🔁 1. `for` Loop

The most common loop. Best when you know **how many times** to repeat.

```javascript
// Syntax:
for (initialization; condition; update) {
  // code to repeat
}

// Count from 1 to 5:
for (let i = 1; i <= 5; i++) {
  console.log(i);
}
// Output: 1, 2, 3, 4, 5

// Count backwards:
for (let i = 5; i >= 1; i--) {
  console.log(i);
}
// Output: 5, 4, 3, 2, 1

// Count by 2s:
for (let i = 0; i <= 10; i += 2) {
  console.log(i);
}
// Output: 0, 2, 4, 6, 8, 10
```

### Breaking Down the `for` Loop:

| Part | Example | Runs |
|------|---------|------|
| **Initialization** | `let i = 1` | Once, before loop starts |
| **Condition** | `i <= 5` | Checked before EVERY iteration |
| **Update** | `i++` | After EVERY iteration |

---

## 🔁 2. `while` Loop

Repeats as long as a condition is `true`. Best when you **don't know** how many iterations you need.

```javascript
// Syntax:
while (condition) {
  // code to repeat
}

// Example:
let count = 1;
while (count <= 5) {
  console.log(count);
  count++;
}
// Output: 1, 2, 3, 4, 5

// Real-world example: keep asking until valid input
let password = "";
while (password !== "secret123") {
  password = prompt("Enter password:");
}
console.log("Access granted! ✅");
```

> ⚠️ **Infinite Loop Warning:** If the condition never becomes `false`, the loop runs forever and crashes the browser. Always make sure the condition will eventually be `false`.

---

## 🔁 3. `do...while` Loop

Runs the code **at least once**, then checks the condition.

```javascript
// Syntax:
do {
  // code to repeat
} while (condition);

// Example:
let num;
do {
  num = Number(prompt("Enter a number between 1 and 10:"));
} while (num < 1 || num > 10);
console.log(`You entered: ${num}`);
```

### `while` vs `do...while`:

| | `while` | `do...while` |
|-|---------|-------------|
| Condition checked | Before code runs | After code runs |
| Minimum runs | 0 (if condition is false from start) | **1 always** |
| Use when | Condition might be false immediately | You need at least one run |

---

## 🔁 4. `for...of` Loop ✅ (Modern — for Arrays)

The cleanest way to loop through **arrays** (and other iterables like strings).

```javascript
const fruits = ["Apple", "Banana", "Mango", "Orange"];

for (const fruit of fruits) {
  console.log(fruit);
}
// Output:
// Apple
// Banana
// Mango
// Orange

// Loop through a string:
for (const char of "Hello") {
  console.log(char);
}
// Output: H, e, l, l, o
```

---

## 🔁 5. `for...in` Loop (for Objects)

Loops through the **keys** (property names) of an object.

```javascript
const person = {
  name: "Manoj",
  age: 20,
  city: "Kathmandu"
};

for (const key in person) {
  console.log(`${key}: ${person[key]}`);
}
// Output:
// name: Manoj
// age: 20
// city: Kathmandu
```

> ⚠️ **Don't use `for...in` on arrays** — use `for...of` instead. `for...in` gives you string keys like `"0"`, `"1"`, which is unexpected.

---

## ⏹️ `break` and `continue`

### `break` — Exit the loop immediately

```javascript
for (let i = 1; i <= 10; i++) {
  if (i === 5) break;  // stop when i reaches 5
  console.log(i);
}
// Output: 1, 2, 3, 4
```

### `continue` — Skip this iteration, go to next

```javascript
for (let i = 1; i <= 10; i++) {
  if (i % 2 === 0) continue;  // skip even numbers
  console.log(i);
}
// Output: 1, 3, 5, 7, 9 (odd numbers only)
```

---

## 🪆 Nested Loops

A loop inside another loop. Common for 2D data (grids, multiplication tables).

```javascript
// Multiplication table:
for (let i = 1; i <= 3; i++) {
  for (let j = 1; j <= 3; j++) {
    console.log(`${i} × ${j} = ${i * j}`);
  }
}
// Output:
// 1 × 1 = 1
// 1 × 2 = 2
// 1 × 3 = 3
// 2 × 1 = 2
// ... etc.
```

> ⚠️ Nested loops run `outer × inner` times. Three nested loops can be very slow for large data.

---

## 📊 Loop Comparison Table

| Loop | Best For | Condition Check |
|------|---------|----------------|
| `for` | Known number of iterations | Before each run |
| `while` | Unknown iterations, condition first | Before each run |
| `do...while` | Must run at least once | After each run |
| `for...of` | Arrays and iterables (modern ✅) | Automatic |
| `for...in` | Object keys | Automatic |

---

## ✅ Key Takeaways

- Use `for` when you know the number of iterations.
- Use `while` when the number of iterations is unknown.
- Use `for...of` to loop through arrays (cleanest syntax).
- Use `for...in` to loop through object keys.
- `break` exits a loop; `continue` skips to the next iteration.
- Always make sure your loop condition will eventually be `false` — avoid infinite loops!

---

## 🏋️ Practice Tasks

### Task 1 — Multiplication Table
Using a `for` loop, print the multiplication table for any number.
```javascript
const num = 7;
// Expected output:
// 7 × 1 = 7
// 7 × 2 = 14
// ...
// 7 × 10 = 70
```

---

### Task 2 — Sum of Digits
Given a number like `4567`, use a `while` loop to calculate the **sum of its digits**.
```javascript
let num = 4567;
// Process: 4 + 5 + 6 + 7 = 22
// Hint: use % 10 to get last digit, then Math.floor(num / 10) to remove it
```

---

### Task 3 — Star Pattern (Nested Loop)
Use nested `for` loops to print this triangle pattern for `n = 5`:
```
*
* *
* * *
* * * *
* * * * *
```
**Bonus:** Also print the upside-down version (5 stars to 1 star).

---

> ➡️ **Next:** `06-functions.md` — Creating reusable blocks of code.
