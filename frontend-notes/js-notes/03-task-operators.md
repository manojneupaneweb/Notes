# 📝 Task 03 — Operators

> **Related Notes:** `03-operators.md`  
> **Goal:** Practice arithmetic, comparison (`===`), logical (`&&`, `||`), ternary, and the nullish coalescing operator (`??`).

---

## ✅ Beginner Tasks

### Task 1 — Arithmetic Operators
Perform the following calculations and log the results:

```javascript
const a = 17;
const b = 5;

// 1. Add a and b
// 2. Subtract b from a
// 3. Multiply a and b
// 4. Divide a by b (show the decimal result)
// 5. Find the remainder when a is divided by b (modulus)
// 6. Raise a to the power of 2 (a²)
```

**Expected output:**
```
17 + 5 = 22
17 - 5 = 12
17 * 5 = 85
17 / 5 = 3.4
17 % 5 = 2
17 ** 2 = 289
```

---

### Task 2 — Even or Odd?
Use the **modulus operator** to check if a number is even or odd.

```javascript
const numbers = [1, 4, 7, 10, 13, 20, 33];

// Loop through each number and print "X is even" or "X is odd"
```

**Expected output:**
```
1 is odd
4 is even
7 is odd
10 is even
13 is odd
20 is even
33 is odd
```

---

### Task 3 — Strict vs Loose Equality
Predict the result of each comparison **before** running them. Then verify in the console.

```javascript
// Loose equality (==):
console.log(5 == "5");       // ?
console.log(0 == false);     // ?
console.log(null == undefined); // ?
console.log(1 == true);      // ?

// Strict equality (===):
console.log(5 === "5");      // ?
console.log(0 === false);    // ?
console.log(null === undefined); // ?
console.log(1 === true);     // ?
```

> 🔑 **Key lesson:** Always use `===` in real code. Write down WHY you think each result is what it is.

---

### Task 4 — Comparison Operators
Given two numbers `x = 10` and `y = 25`, evaluate these comparisons:

```javascript
const x = 10;
const y = 25;

// 1. Is x greater than y?
// 2. Is x less than or equal to y?
// 3. Are x and y equal? (strict)
// 4. Are x and y NOT equal? (strict)
// 5. Is x + y greater than 30?
// 6. Is x * 3 equal to y + 5?
```

**Log results as:** `"10 > 25 → false"`

---

### Task 5 — Logical Operators
Evaluate each expression and write the result as a comment first:

```javascript
// AND (&&):
console.log(true  && true);    // ?
console.log(true  && false);   // ?
console.log(false && true);    // ?

// OR (||):
console.log(true  || false);   // ?
console.log(false || false);   // ?
console.log(false || true);    // ?

// NOT (!):
console.log(!true);            // ?
console.log(!false);           // ?
console.log(!0);               // ?  ← What type is 0?
console.log(!"hello");         // ?  ← Is "hello" truthy?
```

---

## 🟡 Intermediate Tasks

### Task 6 — Ternary Operator
Rewrite each `if/else` as a **ternary** expression:

```javascript
// 1. Voting eligibility:
let age = 17;
// if (age >= 18) { console.log("Can vote"); } else { console.log("Cannot vote"); }
// Rewrite as ternary:


// 2. Pass or fail:
let score = 45;
// if (score >= 50) { console.log("Pass"); } else { console.log("Fail"); }
// Rewrite as ternary:


// 3. Day or night (hour is 0-23):
let hour = 14;
// if (hour >= 6 && hour < 18) { console.log("Day"); } else { console.log("Night"); }
// Rewrite as ternary:
```

---

### Task 7 — Short-Circuit Evaluation
Predict what each line logs, then verify:

```javascript
// Short-circuit with &&:
false && console.log("A");    // Does "A" print?
true  && console.log("B");    // Does "B" print?

// Short-circuit with ||:
const name1 = "" || "Default Name";
const name2 = "Manoj" || "Default Name";
console.log(name1); // ?
console.log(name2); // ?

// Nullish coalescing (??):
const score1 = null ?? 100;
const score2 = 0    ?? 100;
const score3 = ""   ?? "empty";
console.log(score1); // ?
console.log(score2); // ?  ← Key difference from ||
console.log(score3); // ?  ← Key difference from ||
```

> 💡 Explain in a comment **why** `score2` gives a different result with `??` vs `||`.

---

### Task 8 — Assignment Operators
Start with `let points = 100`. Apply the following operations in order and log after each:

```javascript
let points = 100;

// 1. Add 50
// 2. Subtract 30
// 3. Multiply by 2
// 4. Divide by 5
// 5. Get the remainder when divided by 7
// 6. Raise to the power of 2

// Log after each step showing the operation and result:
// "points += 50 → 150"
// "points -= 30 → 120"
// ...
```

---

### Task 9 — Compound Conditions
Write boolean expressions using `&&`, `||`, and `!` to answer:

```javascript
const age      = 22;
const hasID    = true;
const isVIP    = false;
const isMember = true;
const balance  = 500;

// 1. Can this person enter a 21+ club? (age >= 21 AND has ID)
// 2. Gets free entry? (is VIP OR is member)
// 3. Can purchase premium? (balance >= 200 AND is member AND NOT isVIP — VIPs get it free)
// 4. Is this person blocked? (age < 18 OR NOT hasID)
// 5. Full access? (all conditions: age >= 21, hasID, either member or VIP)
```

---

## 🔴 Challenge Tasks

### Task 10 — Grade Calculator with Ternary Chain
Use **chained ternary operators** to assign a letter grade based on score:

```javascript
const scores = [95, 83, 71, 65, 48, 30];

// Rules:
// 90-100 → "A" (Excellent)
// 75-89  → "B" (Good)
// 60-74  → "C" (Average)
// 50-59  → "D" (Below Average)
// 0-49   → "F" (Fail)

// For each score, log: "Score: 95 → Grade: A (Excellent)"
```

---

### Task 11 — Discount Calculator
Build a discount calculator using logical operators:

```javascript
const price       = 1500;  // in rupees
const isMember    = true;
const isFirstTime = false;
const totalItems  = 5;

// Discount rules:
// - Members get 10% off
// - First-time buyers get 15% off
// - Buying 5+ items gets additional 5% off
// - Discounts STACK (add together)
// - Max discount is 25%

// Calculate final price and log:
// "Original: Rs.1500"
// "Discount: 15%"
// "You save: Rs.225"
// "Final price: Rs.1275"
```

---

### Task 12 — FizzBuzz (Classic!)
Print numbers from 1 to 50. But:
- If divisible by 3 → print **"Fizz"**
- If divisible by 5 → print **"Buzz"**
- If divisible by both 3 and 5 → print **"FizzBuzz"**
- Otherwise → print the number

```javascript
// Use a for loop with the modulus operator %
// Hint: check FizzBuzz condition FIRST (both 3 and 5)
```

**Expected output (partial):**
```
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
...
```

---

## 💡 Bonus — Operator Precedence Puzzle

Predict the output of each WITHOUT running it first. Then verify:

```javascript
console.log(2 + 3 * 4);          // ?
console.log((2 + 3) * 4);        // ?
console.log(10 - 3 + 2);         // ?
console.log(true + true);         // ?  ← Type coercion!
console.log(true + false);        // ?
console.log("5" - 2);            // ?  ← Implicit conversion
console.log("5" + 2);            // ?  ← Same operator, different result!
console.log(+"5");               // ?  ← Unary + operator
console.log(!!"hello");          // ?  ← Double NOT trick
```

> 🤯 The last three are common JavaScript interview questions!

---

## ✅ Answers Checklist

- [ ] Task 1 — All 6 arithmetic operations correct
- [ ] Task 2 — Modulus used for even/odd check
- [ ] Task 3 — Understood `==` vs `===` difference
- [ ] Task 4 — All comparisons evaluated correctly
- [ ] Task 5 — All logical expressions predicted correctly
- [ ] Task 6 — All 3 `if/else` converted to ternary
- [ ] Task 7 — Short-circuit and `??` vs `||` understood
- [ ] Task 8 — All assignment operators used in order
- [ ] Task 9 — All 5 compound conditions correct
- [ ] Task 10 — Grade calculator with ternary chain works
- [ ] Task 11 — Discount calculator logic correct
- [ ] Task 12 — FizzBuzz prints correctly for 1-50

---

> ➡️ **Next Task:** `04-task-control-flow.md`
