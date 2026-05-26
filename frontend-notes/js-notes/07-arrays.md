# 07 — Arrays

---

## 📌 What is an Array?

An **array** is an ordered list of values stored in a single variable.

```javascript
// Without an array (bad):
const fruit1 = "Apple";
const fruit2 = "Banana";
const fruit3 = "Mango";

// With an array (good ✅):
const fruits = ["Apple", "Banana", "Mango"];
```

> 💡 **Analogy:** An array is like a numbered shopping list. Each item has a position (index) and you can access any item by its number.

---

## 📦 Creating Arrays

```javascript
// Array literal (most common ✅):
const numbers = [1, 2, 3, 4, 5];
const names   = ["Manoj", "Sita", "Ram"];
const mixed   = [1, "hello", true, null]; // can mix types (not recommended)
const empty   = [];                       // empty array

// Array constructor (less common):
const arr = new Array(3); // creates [undefined, undefined, undefined]
```

---

## 🔢 Accessing Elements (Indexing)

Arrays are **zero-indexed** — the first element is at index `0`.

```javascript
const fruits = ["Apple", "Banana", "Mango", "Orange"];
//  Indices:       0         1        2         3

fruits[0]  // "Apple"
fruits[1]  // "Banana"
fruits[3]  // "Orange"
fruits[4]  // undefined — no element at index 4

// Last element:
fruits[fruits.length - 1]  // "Orange"

// Negative index (ES2022):
fruits.at(-1)  // "Orange" — last element
fruits.at(-2)  // "Mango"  — second to last
```

---

## 🔧 Common Array Methods

### Adding and Removing Elements:

```javascript
const arr = [1, 2, 3];

// Add to END:
arr.push(4);        // [1, 2, 3, 4] — returns new length
arr.push(5, 6);     // [1, 2, 3, 4, 5, 6]

// Remove from END:
arr.pop();          // removes 6, returns 6 — [1, 2, 3, 4, 5]

// Add to BEGINNING:
arr.unshift(0);     // [0, 1, 2, 3, 4, 5] — returns new length

// Remove from BEGINNING:
arr.shift();        // removes 0, returns 0 — [1, 2, 3, 4, 5]

// Add/Remove at ANY position (splice):
// arr.splice(startIndex, deleteCount, ...itemsToAdd)
arr.splice(2, 0, 99);    // [1, 2, 99, 3, 4, 5] — insert 99 at index 2
arr.splice(2, 1);        // [1, 2, 3, 4, 5] — remove 1 element at index 2
arr.splice(1, 2, 10, 20);// [1, 10, 20, 4, 5] — replace 2 elements with 10, 20
```

### Searching:

```javascript
const fruits = ["Apple", "Banana", "Mango", "Banana"];

fruits.indexOf("Banana");      // 1 — first occurrence
fruits.lastIndexOf("Banana");  // 3 — last occurrence
fruits.indexOf("Grape");       // -1 — not found

fruits.includes("Mango");      // true
fruits.includes("Grape");      // false

fruits.find(f => f.startsWith("M"));     // "Mango" — returns first match
fruits.findIndex(f => f === "Mango");    // 2 — returns index of first match
```

### Transforming Arrays (Returns NEW array):

```javascript
const numbers = [1, 2, 3, 4, 5];

// map: transform every element
numbers.map(n => n * 2);          // [2, 4, 6, 8, 10]
numbers.map(n => n + "!");        // ["1!", "2!", "3!", "4!", "5!"]

// filter: keep only elements that pass a test
numbers.filter(n => n > 3);      // [4, 5]
numbers.filter(n => n % 2 === 0); // [2, 4] — even numbers only

// reduce: collapse array to a single value
numbers.reduce((acc, n) => acc + n, 0);  // 15 — sum of all numbers
numbers.reduce((acc, n) => acc * n, 1);  // 120 — product

// slice: extract a portion (non-destructive)
numbers.slice(1, 4);  // [2, 3, 4] — from index 1 up to (not including) 4
numbers.slice(2);     // [3, 4, 5] — from index 2 to end
numbers.slice(-2);    // [4, 5] — last 2 elements

// flat: flatten nested arrays
[1, [2, [3, [4]]]].flat();     // [1, 2, [3, [4]]] — 1 level deep
[1, [2, [3, [4]]]].flat(2);    // [1, 2, 3, [4]] — 2 levels deep
[1, [2, [3, [4]]]].flat(Infinity); // [1, 2, 3, 4] — fully flatten

// flatMap: map + flatten (1 level)
[1, 2, 3].flatMap(n => [n, n * 2]); // [1, 2, 2, 4, 3, 6]
```

### Sorting:

```javascript
const fruits = ["Banana", "Apple", "Mango", "Cherry"];

// Sort alphabetically:
fruits.sort();  // ["Apple", "Banana", "Cherry", "Mango"] ⚠️ mutates original!

// Sort numbers — MUST use a compare function:
const nums = [10, 1, 5, 30, 2];
nums.sort((a, b) => a - b);  // [1, 2, 5, 10, 30] — ascending
nums.sort((a, b) => b - a);  // [30, 10, 5, 2, 1] — descending

// Reverse:
[1, 2, 3, 4].reverse();  // [4, 3, 2, 1] ⚠️ mutates original!
```

### Other Useful Methods:

```javascript
const a = [1, 2, 3];
const b = [4, 5, 6];

// concat: merge arrays
a.concat(b);         // [1, 2, 3, 4, 5, 6]
[...a, ...b];        // [1, 2, 3, 4, 5, 6] — spread (modern ✅)

// join: convert to string
[1, 2, 3].join(", ");    // "1, 2, 3"
["a", "b"].join("-");    // "a-b"
["Hello", "World"].join(" "); // "Hello World"

// every: are ALL elements true?
[2, 4, 6].every(n => n % 2 === 0);   // true — all even
[2, 3, 6].every(n => n % 2 === 0);   // false — 3 is odd

// some: is AT LEAST ONE element true?
[1, 2, 3].some(n => n > 2);  // true — 3 > 2
[1, 2, 3].some(n => n > 5);  // false — none > 5

// fill: fill with a value
[1, 2, 3, 4].fill(0);       // [0, 0, 0, 0]
[1, 2, 3, 4].fill(0, 1, 3); // [1, 0, 0, 4] — fill from index 1 to 3
```

---

## 📊 Destructuring Arrays

Extract values into variables cleanly:

```javascript
const [first, second, third] = ["Red", "Green", "Blue"];
console.log(first);  // "Red"
console.log(second); // "Green"

// Skip elements:
const [a, , c] = [1, 2, 3];
console.log(a, c); // 1, 3

// Rest operator:
const [head, ...tail] = [1, 2, 3, 4, 5];
console.log(head); // 1
console.log(tail); // [2, 3, 4, 5]

// Default values:
const [x = 10, y = 20] = [5];
console.log(x, y); // 5, 20 (y used default)

// Swap variables (elegant!):
let m = 1, n = 2;
[m, n] = [n, m];
console.log(m, n); // 2, 1
```

---

## 🌐 Spread Operator `...`

Spread an array into individual elements:

```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

// Merge arrays:
const merged = [...arr1, ...arr2]; // [1, 2, 3, 4, 5, 6]

// Copy an array (shallow copy):
const copy = [...arr1]; // [1, 2, 3]

// Pass array as function arguments:
Math.max(...[5, 3, 9, 1]); // 9 — same as Math.max(5, 3, 9, 1)
```

---

## ✅ Key Takeaways

| Method | Purpose | Mutates Original? |
|--------|---------|:-----------------:|
| `push()` / `pop()` | Add/remove from end | ✅ Yes |
| `unshift()` / `shift()` | Add/remove from start | ✅ Yes |
| `splice()` | Add/remove anywhere | ✅ Yes |
| `sort()` / `reverse()` | Sort/reverse | ✅ Yes |
| `map()` | Transform each element | ❌ No |
| `filter()` | Keep matching elements | ❌ No |
| `reduce()` | Collapse to single value | ❌ No |
| `slice()` | Extract portion | ❌ No |
| `find()` | Find first matching element | ❌ No |
| `includes()` | Check if exists | ❌ No |

---

> ➡️ **Next:** `08-objects.md` — Storing related data in key-value pairs.
