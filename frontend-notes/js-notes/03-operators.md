# 03 — Operators

---

## 📌 What are Operators?

**Operators** are symbols that perform operations on values (operands). JavaScript has several types of operators.

---

## ➕ 1. Arithmetic Operators

Used for mathematical calculations.

```javascript
let a = 10;
let b = 3;

a + b   // 13  — Addition
a - b   // 7   — Subtraction
a * b   // 30  — Multiplication
a / b   // 3.333... — Division
a % b   // 1   — Modulus (remainder after division)
a ** b  // 1000 — Exponentiation (power) — 10^3
```

### Modulus `%` Use Cases:
```javascript
// Check if a number is even or odd:
10 % 2 === 0  // true — even
9  % 2 === 0  // false — odd

// Always get the last digit of a number:
1234 % 10     // 4
```

### Increment and Decrement:
```javascript
let count = 5;

count++;  // Post-increment: returns 5, THEN count becomes 6
++count;  // Pre-increment: count becomes 7 first, returns 7
count--;  // Post-decrement: returns 7, THEN count becomes 6
--count;  // Pre-decrement: count becomes 5 first, returns 5
```

---

## 🔗 2. Assignment Operators

```javascript
let x = 10;   // Assign

x += 5;   // x = x + 5  → 15
x -= 3;   // x = x - 3  → 12
x *= 2;   // x = x * 2  → 24
x /= 4;   // x = x / 4  → 6
x %= 4;   // x = x % 4  → 2
x **= 3;  // x = x ** 3 → 8
```

---

## ⚖️ 3. Comparison Operators

Comparison operators always return `true` or `false`.

```javascript
let a = 5;
let b = "5";

// Loose equality (== / !=) — compares VALUE only, ignores type
a == b      // true  ← 5 == "5" (JS converts "5" to number)
a != b      // false

// Strict equality (=== / !==) — compares VALUE AND TYPE ✅
a === b     // false ← 5 !== "5" (different types)
a !== b     // true

// Other comparisons:
a > 3       // true  — Greater than
a < 3       // false — Less than
a >= 5      // true  — Greater than or equal
a <= 5      // true  — Less than or equal
```

> 🔑 **ALWAYS use `===` and `!==`** (strict equality). Never use `==` in real code — it causes subtle bugs.

---

## 🧠 4. Logical Operators

Used to combine boolean expressions.

```javascript
// AND (&&) — true only if BOTH sides are true
true  && true   // true
true  && false  // false
false && true   // false

// OR (||) — true if AT LEAST ONE side is true
true  || false  // true
false || false  // false

// NOT (!) — flips the boolean
!true   // false
!false  // true
!0      // true  (0 is falsy)
!"hello" // false ("hello" is truthy)
```

### Real World Example:
```javascript
const age = 25;
const hasTicket = true;

// Both conditions must be true to enter
if (age >= 18 && hasTicket) {
  console.log("Welcome!");
}

// At least one condition must be true
const isWeekend = false;
const isHoliday = true;
if (isWeekend || isHoliday) {
  console.log("No school today!");
}
```

### Short-Circuit Evaluation:

```javascript
// && stops at first falsy value:
false && console.log("This never runs");  // stops at false
true  && console.log("This runs!");       // ✅ runs

// || stops at first truthy value:
null  || "default"    // "default" — used for fallback values!
"hi"  || "default"    // "hi"      — uses first truthy value

// Practical usage — default values:
const username = userInput || "Guest";  // if userInput is empty, use "Guest"
```

---

## 🔀 5. Nullish Coalescing Operator `??`

Returns the right side **only if** the left side is `null` or `undefined` (not all falsy values).

```javascript
null ?? "default"      // "default"
undefined ?? "default" // "default"
0    ?? "default"      // 0      ← different from || !
""   ?? "default"      // ""     ← different from || !
false ?? "default"     // false  ← different from || !

// Practical use:
const userAge = 0;
const age1 = userAge || 18;   // 18 ← WRONG: 0 is falsy, so it uses default
const age2 = userAge ?? 18;   // 0  ← CORRECT: 0 is not null/undefined
```

---

## ❓ 6. Ternary Operator (Conditional Operator)

A compact way to write an `if/else` statement on one line.

```javascript
// Syntax:
condition ? valueIfTrue : valueIfFalse

// Example:
const age = 20;
const status = age >= 18 ? "Adult" : "Minor";
console.log(status); // "Adult"

// Can be chained (use sparingly — can get hard to read):
const score = 75;
const grade = score >= 90 ? "A"
            : score >= 75 ? "B"
            : score >= 60 ? "C"
            : "F";
console.log(grade); // "B"
```

---

## 🔢 7. Bitwise Operators (Advanced — for reference)

Work on binary (bit-level) representations of numbers.

| Operator | Symbol | Example | Result |
|----------|--------|---------|--------|
| AND | `&` | `5 & 3` | `1` |
| OR | `\|` | `5 \| 3` | `7` |
| XOR | `^` | `5 ^ 3` | `6` |
| NOT | `~` | `~5` | `-6` |
| Left shift | `<<` | `5 << 1` | `10` |
| Right shift | `>>` | `5 >> 1` | `2` |

> 💡 Bitwise operators are rarely needed in everyday JavaScript. You'll encounter them in performance-critical code.

---

## 📊 Operator Precedence (Order of Operations)

Like math — JavaScript follows BODMAS/PEMDAS:

```javascript
2 + 3 * 4     // 14 (not 20) — multiplication first
(2 + 3) * 4   // 20 — parentheses override order

// Full order (highest to lowest):
// 1. ()   — Grouping
// 2. **   — Exponentiation
// 3. * / % — Multiplication, Division, Modulus
// 4. + -  — Addition, Subtraction
// 5. > >= < <= — Comparison
// 6. === !== — Equality
// 7. &&   — Logical AND
// 8. ||   — Logical OR
// 9. ?:   — Ternary
// 10. =   — Assignment
```

---

## ✅ Key Takeaways

| Operator Type | Symbols | Purpose |
|--------------|---------|---------|
| Arithmetic | `+ - * / % **` | Math calculations |
| Assignment | `= += -= *= /=` | Store values |
| Comparison | `=== !== > < >= <=` | Compare values (always use `===`) |
| Logical | `&& \|\| !` | Combine boolean conditions |
| Nullish Coalescing | `??` | Default when `null`/`undefined` |
| Ternary | `? :` | Short if/else |

---

> ➡️ **Next:** `04-control-flow.md` — Making decisions and repeating actions.
