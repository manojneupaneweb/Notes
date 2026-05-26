# 04 — Control Flow: if, else, switch

---

## 📌 What is Control Flow?

**Control flow** is the order in which code executes. By default, code runs line-by-line from top to bottom. **Control flow statements** let you:

- Make **decisions** (if/else, switch)
- **Repeat** actions (loops — covered next chapter)

---

## 🔀 The `if` Statement

Executes code only **if** a condition is `true`.

```javascript
const temperature = 35;

if (temperature > 30) {
  console.log("It's hot outside! ☀️");
}
```

---

## 🔀 `if...else`

Provides an alternative if the condition is `false`.

```javascript
const age = 16;

if (age >= 18) {
  console.log("You can vote! 🗳️");
} else {
  console.log("You are too young to vote.");
}
```

---

## 🔀 `if...else if...else`

Check multiple conditions in sequence.

```javascript
const score = 72;

if (score >= 90) {
  console.log("Grade: A — Excellent! 🌟");
} else if (score >= 75) {
  console.log("Grade: B — Good! 👍");
} else if (score >= 60) {
  console.log("Grade: C — Average.");
} else if (score >= 40) {
  console.log("Grade: D — Below Average.");
} else {
  console.log("Grade: F — Failed. ❌");
}
```

> 💡 **Tip:** Only ONE block executes — the first one whose condition is `true`.

---

## 🔀 Nested `if` Statements

Conditions inside other conditions.

```javascript
const isLoggedIn = true;
const isAdmin    = false;

if (isLoggedIn) {
  if (isAdmin) {
    console.log("Welcome, Admin! Access granted to dashboard.");
  } else {
    console.log("Welcome, User! Access to your profile only.");
  }
} else {
  console.log("Please log in first.");
}
```

> ⚠️ Avoid deeply nested `if` statements — they become hard to read. Use logical operators (`&&`, `||`) when possible.

---

## 🔀 `switch` Statement

Best for checking one variable against **many specific values**.

```javascript
const day = "Monday";

switch (day) {
  case "Monday":
    console.log("Start of the work week 💼");
    break;
  case "Friday":
    console.log("TGIF! 🎉");
    break;
  case "Saturday":
  case "Sunday":          // multiple cases, same result
    console.log("Weekend! 😎");
    break;
  default:
    console.log("Regular weekday.");
}
```

### Important `switch` Rules:

| Rule | Explanation |
|------|-------------|
| `break` | **REQUIRED** — stops execution at the end of each case. Without it, "fall-through" happens. |
| `default` | Runs if no `case` matches (like `else`) |
| Fall-through | Intentionally omit `break` to run multiple cases together |
| Uses `===` | Switch uses **strict equality** for comparisons |

### Fall-through Example (Intentional):

```javascript
const month = 4; // April

switch (month) {
  case 1:
  case 3:
  case 5:
  case 7:
  case 8:
  case 10:
  case 12:
    console.log("31 days");
    break;
  case 4:
  case 6:
  case 9:
  case 11:
    console.log("30 days");
    break;
  case 2:
    console.log("28 or 29 days");
    break;
}
// Output: "30 days"
```

---

## ⚡ Truthy and Falsy in Conditions

You don't need `=== true` in conditions — JavaScript automatically evaluates truthiness:

```javascript
const username = "Manoj";

// These do the same thing:
if (username !== "" && username !== null && username !== undefined) { ... }
if (username) { ... }  // ✅ Cleaner — empty string, null, undefined are all falsy

// Checking for empty array is a common pitfall:
const items = [];
if (items) { ... }        // ✅ runs — [] is truthy!
if (items.length > 0) { } // ✅ better check for non-empty array
```

---

## 📊 `if` vs `switch` — When to Use Which?

| Situation | Use |
|-----------|-----|
| Checking ranges (`score >= 90`) | `if/else if` |
| One variable against many exact values | `switch` |
| Complex boolean conditions (`&&`, `\|\|`) | `if/else` |
| Only 2 outcomes | `if/else` or ternary `? :` |

---

## ✅ Key Takeaways

- `if` runs code when a condition is `true`.
- `else` provides a fallback.
- `else if` checks additional conditions.
- `switch` is cleaner when checking one value against many options.
- Always include `break` in `switch` cases.
- Falsy values: `false`, `0`, `""`, `null`, `undefined`, `NaN` — everything else is truthy.

---

> ➡️ **Next:** `05-loops.md` — Repeating code with for, while, and more.
