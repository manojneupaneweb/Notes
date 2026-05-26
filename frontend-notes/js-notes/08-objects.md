# 08 — Objects

---

## 📌 What is an Object?

An **object** is a collection of **key-value pairs** that represent a real-world entity.

```javascript
// Representing a person — WITHOUT an object (bad):
const personName = "Manoj";
const personAge  = 20;
const personCity = "Kathmandu";

// WITH an object (good ✅):
const person = {
  name: "Manoj",
  age:  20,
  city: "Kathmandu"
};
```

> 💡 **Analogy:** An object is like a contact card — it has different fields (name, phone, email) all describing one entity.

---

## 📦 Creating Objects

```javascript
// Object literal (most common ✅):
const car = {
  brand: "Toyota",
  model: "Corolla",
  year:  2022,
  isElectric: false
};

// Object with a method (a function as a property):
const calculator = {
  add:      (a, b) => a + b,
  subtract: (a, b) => a - b,
  multiply: (a, b) => a * b
};

console.log(calculator.add(5, 3)); // 8
```

---

## 🔓 Accessing Properties

```javascript
const person = { name: "Manoj", age: 20, "favorite color": "blue" };

// Dot notation (most common — cleaner):
person.name   // "Manoj"
person.age    // 20

// Bracket notation (required for keys with spaces or dynamic keys):
person["name"]           // "Manoj"
person["favorite color"] // "blue"

// Dynamic key access:
const key = "age";
person[key]  // 20 — useful when key is stored in a variable
```

---

## ✏️ Adding, Updating, and Deleting Properties

```javascript
const user = { name: "Manoj", age: 20 };

// Add new property:
user.email = "manoj@example.com";
user["role"] = "student";

// Update existing property:
user.age = 21;

// Delete property:
delete user.role;

console.log(user); // { name: "Manoj", age: 21, email: "manoj@example.com" }
```

---

## 🔍 Checking Properties

```javascript
const person = { name: "Manoj", age: 20 };

// in operator:
"name" in person  // true
"email" in person // false

// hasOwnProperty method:
person.hasOwnProperty("name")  // true
person.hasOwnProperty("email") // false

// Optional chaining — safe access on potentially undefined properties:
const user = { address: { city: "Kathmandu" } };
user?.address?.city      // "Kathmandu"
user?.phone?.number      // undefined (no error! ✅)
```

---

## 📋 Object Methods (Built-in)

```javascript
const person = { name: "Manoj", age: 20, city: "Kathmandu" };

// Get all KEYS as an array:
Object.keys(person)    // ["name", "age", "city"]

// Get all VALUES as an array:
Object.values(person)  // ["Manoj", 20, "Kathmandu"]

// Get all KEY-VALUE PAIRS as array of arrays:
Object.entries(person) // [["name","Manoj"], ["age",20], ["city","Kathmandu"]]

// Merge objects (spread) ✅:
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };
const merged = { ...obj1, ...obj2 };  // { a:1, b:2, c:3, d:4 }

// Object.assign (older way):
Object.assign({}, obj1, obj2);        // { a:1, b:2, c:3, d:4 }

// Freeze an object (prevent any changes):
const config = Object.freeze({ API_KEY: "abc123" });
config.API_KEY = "new";  // silently ignored (strict mode throws error)
```

### Looping with `Object.entries()`:

```javascript
const scores = { math: 90, science: 85, english: 78 };

for (const [subject, score] of Object.entries(scores)) {
  console.log(`${subject}: ${score}`);
}
// math: 90
// science: 85
// english: 78
```

---

## 📊 Object Destructuring

Extract properties into variables cleanly:

```javascript
const person = { name: "Manoj", age: 20, city: "Kathmandu" };

// Basic destructuring:
const { name, age } = person;
console.log(name, age); // "Manoj", 20

// Rename variable:
const { name: fullName, age: years } = person;
console.log(fullName, years); // "Manoj", 20

// Default values:
const { name, country = "Nepal" } = person;
console.log(country); // "Nepal" (default, since person has no country)

// Nested destructuring:
const user = {
  name: "Manoj",
  address: {
    city: "Kathmandu",
    zip: "44600"
  }
};
const { name: uName, address: { city } } = user;
console.log(uName, city); // "Manoj", "Kathmandu"

// Rest operator:
const { name: n, ...rest } = person;
console.log(n);    // "Manoj"
console.log(rest); // { age: 20, city: "Kathmandu" }
```

---

## 🏗️ `this` Keyword in Objects

Inside a method, `this` refers to the object the method belongs to.

```javascript
const person = {
  name: "Manoj",
  age:  20,
  greet() {
    console.log(`Hi, I'm ${this.name} and I'm ${this.age} years old.`);
  }
};

person.greet(); // Hi, I'm Manoj and I'm 20 years old.
```

> ⚠️ **Arrow functions and `this`:** Arrow functions do NOT have their own `this`. Use regular function syntax for methods.

```javascript
const obj = {
  value: 42,
  // ❌ Arrow function — 'this' is NOT the object:
  badMethod: () => console.log(this.value), // undefined

  // ✅ Regular function — 'this' IS the object:
  goodMethod() {
    console.log(this.value); // 42
  }
};
```

---

## 🏛️ Constructor Functions and Classes

Create multiple objects of the same type:

```javascript
// Old way — Constructor Function:
function Person(name, age) {
  this.name = name;
  this.age  = age;
  this.greet = function() {
    console.log(`Hi, I'm ${this.name}!`);
  };
}
const p1 = new Person("Manoj", 20);
const p2 = new Person("Sita",  22);
p1.greet(); // Hi, I'm Manoj!

// Modern way — Class ✅ (ES6):
class Person {
  constructor(name, age) {
    this.name = name;
    this.age  = age;
  }

  greet() {
    console.log(`Hi, I'm ${this.name}!`);
  }

  // Getter:
  get info() {
    return `${this.name}, ${this.age} years old`;
  }
}

const p1 = new Person("Manoj", 20);
p1.greet();    // Hi, I'm Manoj!
console.log(p1.info); // "Manoj, 20 years old"
```

---

## 📊 Array of Objects (Very Common Pattern)

```javascript
const students = [
  { name: "Manoj",  grade: 90 },
  { name: "Sita",   grade: 85 },
  { name: "Ram",    grade: 72 },
  { name: "Gita",   grade: 95 }
];

// Get all names:
students.map(s => s.name);   // ["Manoj", "Sita", "Ram", "Gita"]

// Filter passing students (grade >= 80):
students.filter(s => s.grade >= 80);

// Sort by grade (descending):
students.sort((a, b) => b.grade - a.grade);

// Find a specific student:
students.find(s => s.name === "Ram"); // { name: "Ram", grade: 72 }
```

---

## ✅ Key Takeaways

- Objects store **key-value pairs** — related data together.
- Access properties with **dot notation** (`.`) or **bracket notation** (`[]`).
- `Object.keys()`, `Object.values()`, `Object.entries()` are essential methods.
- Use **destructuring** to extract values cleanly.
- `this` inside a method refers to the object — don't use arrow functions for methods.
- Use **classes** to create multiple objects of the same type.

---

> ➡️ **Next:** `09-dom-manipulation.md` — Controlling the web page with JavaScript.
