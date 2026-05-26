# 📝 Task 02 — Variables and Data Types

> **Related Notes:** `02-variables-and-data-types.md`  
> **Goal:** Practice using `let`, `const`, strings, numbers, booleans, and type conversion.

---

## ✅ Beginner Tasks

### Task 1 — Declare Variables
Create variables to store the following information about yourself and log them:
- Your full name (`const`)
- Your age (`let`)
- Are you a student? (`const` — boolean)
- Your favorite number (`const`)

```javascript
// Write your code here:

```

**Expected output (example):**
```
Name: Manoj Neupane
Age: 20
Is student: true
Favorite number: 7
```

---

### Task 2 — Template Literals
Using the variables from Task 1, create ONE sentence using a template literal and log it.

```javascript
// Write your code here:

```

**Expected output (example):**
```
My name is Manoj Neupane, I am 20 years old, and my favorite number is 7.
```

---

### Task 3 — String Methods
Given the string below, use string methods to:
1. Find its length
2. Convert to UPPERCASE
3. Check if it includes the word `"JavaScript"`
4. Extract the word `"JavaScript"` using `slice()`

```javascript
const sentence = "I am learning JavaScript every day!";

// 1. Length:
// 2. Uppercase:
// 3. Includes "JavaScript":
// 4. Slice "JavaScript":
```

**Expected output:**
```
35
I AM LEARNING JAVASCRIPT EVERY DAY!
true
JavaScript
```

---

### Task 4 — Number Math
Use `Math` methods to solve the following:

```javascript
const price    = 199.75;
const discount = 15;        // percent
const items    = [-5, 3, -2, 8, 1];

// 1. Round the price to 2 decimal places
// 2. Calculate the discounted price (price - discount%)
// 3. Find the maximum value in the items array using Math.max()
// 4. Find the absolute value of -42
// 5. Generate a random integer between 1 and 100
```

---

### Task 5 — typeof Check
What does `typeof` return for each of these? Write your answers as comments, then verify in the console.

```javascript
typeof "Hello"        // ?
typeof 42             // ?
typeof 3.14           // ?
typeof true           // ?
typeof false          // ?
typeof undefined      // ?
typeof null           // ?  ← Trick question!
typeof []             // ?  ← Trick question!
typeof {}             // ?
typeof function(){}   // ?
```

---

## 🟡 Intermediate Tasks

### Task 6 — Type Conversion
Convert the following values and log the result with `typeof` to confirm:

```javascript
// 1. Convert the string "100" to a number
// 2. Convert the number 0 to a boolean
// 3. Convert the boolean true to a string
// 4. Convert "3.99" to a whole integer (use parseInt)
// 5. Parse the number from the string "50px"
```

**Expected output:**
```
100 → type: number
false → type: boolean
"true" → type: string
3 → type: number
50 → type: number
```

---

### Task 7 — Falsy Detective 🔍
Which of these values are **falsy**? Predict first, then verify with `Boolean()`.

```javascript
const values = [0, 1, "", "0", null, undefined, NaN, [], {}, false, true, -1];

// Loop through and print: "value is TRUTHY/FALSY"
values.forEach(v => {
  // your code here
});
```

**Hint:** Only 6 values should be falsy!

---

### Task 8 — User Profile Card
Create a `const` object variable called `myProfile` with at least 5 properties (name, age, city, isStudent, favoriteLanguage). Then use a template literal to display a formatted profile card.

```javascript
// Write your code here:

// Expected output (example):
// ================================
// 👤 Profile Card
// ================================
// Name    : Manoj Neupane
// Age     : 20
// City    : Kathmandu
// Student : Yes
// Language: JavaScript
// ================================
```

---

## 🔴 Challenge Tasks

### Task 9 — String Manipulation Challenge
Given a person's full name as a string, write code to:
1. Count the number of words
2. Reverse the full name (last name first)
3. Convert to title case (first letter of each word uppercase)
4. Check if the name is a palindrome (reads same forwards and backwards)

```javascript
const fullName = "manoj neupane";

// 1. Word count:
// 2. Reversed: "neupane manoj"
// 3. Title case: "Manoj Neupane"
// 4. Is palindrome:
```

---

### Task 10 — Temperature Converter
Create variables for temperature conversion:

```javascript
const celsius = 100;

// 1. Convert to Fahrenheit: (C × 9/5) + 32
// 2. Convert to Kelvin: C + 273.15

// Display using template literal:
// "100°C = 212°F = 373.15K"
```

---

## 💡 Bonus — Explore on Your Own

Try these in the browser console:
```javascript
// What happens with these?
console.log(0.1 + 0.2);           // Surprise! 😮
console.log(0.1 + 0.2 === 0.3);  // true or false?
console.log("5" * 2);            // What type is the result?
console.log(typeof NaN);          // What is NaN's type?
console.log(NaN === NaN);        // true or false?
```

> 🤯 These are famous JavaScript quirks! Understanding them makes you a better developer.

---

## ✅ Answers Checklist

- [ ] Task 1 — Variables declared with correct keywords
- [ ] Task 2 — Template literal used (not string concatenation)
- [ ] Task 3 — All 4 string methods used correctly
- [ ] Task 4 — All Math methods used
- [ ] Task 5 — All `typeof` results predicted correctly
- [ ] Task 6 — All type conversions correct
- [ ] Task 7 — Correctly identified all 6 falsy values
- [ ] Task 8 — Profile card displayed with template literal
- [ ] Task 9 — String manipulation completed
- [ ] Task 10 — Temperature converter works

---

> ➡️ **Next Task:** `03-task-operators.md`
