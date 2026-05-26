# 12 — Error Handling

---

## 📌 Why Error Handling?

When code runs into a problem (bad input, network failure, missing data), JavaScript throws an **error**. Without handling it, the entire program crashes.

> 💡 **Analogy:** Error handling is like a safety net under a trapeze artist — if something goes wrong, it catches the fall instead of letting everything crash.

---

## 🚨 Types of Errors in JavaScript

| Error Type | When It Happens | Example |
|------------|----------------|---------|
| `SyntaxError` | Code can't be parsed | `let x = ;` |
| `ReferenceError` | Variable doesn't exist | `console.log(y)` (y not defined) |
| `TypeError` | Wrong type used | `null.name` |
| `RangeError` | Value out of allowed range | `new Array(-1)` |
| `URIError` | Bad URI encoding | `decodeURIComponent("%")` |
| Custom Errors | Thrown by you | `throw new Error("Invalid input")` |

---

## 🛡️ `try...catch...finally`

```javascript
try {
  // Code that might throw an error
  const result = riskyOperation();
  console.log(result);
} catch (error) {
  // Runs ONLY if an error is thrown in try
  console.error("Something went wrong:", error.message);
} finally {
  // ALWAYS runs — with or without error (cleanup code)
  console.log("Operation complete.");
}
```

### Real Example:

```javascript
function divide(a, b) {
  if (b === 0) {
    throw new Error("Cannot divide by zero!");
  }
  return a / b;
}

try {
  console.log(divide(10, 2));   // 5
  console.log(divide(10, 0));   // ❌ throws error
  console.log("This never runs"); // skipped after throw
} catch (err) {
  console.error("Error:", err.message); // "Cannot divide by zero!"
} finally {
  console.log("Division attempted."); // always runs
}
```

---

## 🎯 The `error` Object

Inside `catch`, the error object has useful properties:

```javascript
try {
  null.name; // TypeError
} catch (err) {
  console.log(err.name);    // "TypeError"
  console.log(err.message); // "Cannot read properties of null"
  console.log(err.stack);   // Full call stack (for debugging)
}
```

---

## 🔨 Throwing Custom Errors

You can throw any value, but best practice is to use `Error` objects:

```javascript
// Throw a basic error:
throw new Error("Something failed!");

// Throw specific error types:
throw new TypeError("Expected a number!");
throw new RangeError("Age must be between 0 and 150!");

// Custom error class (advanced ✅):
class ValidationError extends Error {
  constructor(message, field) {
    super(message);       // call parent Error constructor
    this.name = "ValidationError";
    this.field = field;
  }
}

function validateAge(age) {
  if (typeof age !== "number") {
    throw new ValidationError("Age must be a number", "age");
  }
  if (age < 0 || age > 150) {
    throw new ValidationError("Age out of range", "age");
  }
  return true;
}

try {
  validateAge("twenty");
} catch (err) {
  if (err instanceof ValidationError) {
    console.log(`Validation failed on field: ${err.field}`);
    console.log(err.message);
  } else {
    throw err; // re-throw unexpected errors
  }
}
```

---

## ⚡ Error Handling in Async/Await

Always wrap `await` calls in `try/catch`:

```javascript
async function fetchUser(id) {
  try {
    const response = await fetch(`https://api.example.com/users/${id}`);

    if (!response.ok) {
      throw new Error(`User not found. Status: ${response.status}`);
    }

    const user = await response.json();
    return user;
  } catch (err) {
    console.error("Failed to fetch user:", err.message);
    return null;   // return fallback
  }
}

const user = await fetchUser(1);
if (user) {
  console.log(user.name);
}
```

---

## 🛡️ Error Handling Patterns

### Pattern 1 — Fail Silently with Default Value:
```javascript
function safeParse(json) {
  try {
    return JSON.parse(json);
  } catch {
    return null;  // return null on bad JSON
  }
}

safeParse('{"name":"Manoj"}');  // { name: "Manoj" }
safeParse("invalid json");      // null (no crash!)
```

### Pattern 2 — Re-throw Unknown Errors:
```javascript
try {
  riskyOperation();
} catch (err) {
  if (err instanceof TypeError) {
    // Handle TypeError specifically
    console.log("Type error:", err.message);
  } else {
    throw err;  // re-throw if unexpected error type
  }
}
```

### Pattern 3 — Error Boundary in Async:
```javascript
const [data, error] = await fetchData().then(d => [d, null]).catch(e => [null, e]);

if (error) {
  console.error("Failed:", error.message);
} else {
  console.log(data);
}
```

---

## ✅ Key Takeaways

| Concept | Description |
|---------|-------------|
| `try` | Wraps risky code |
| `catch(err)` | Handles the error |
| `finally` | Always runs (cleanup) |
| `throw` | Manually trigger an error |
| `err.name` | Type of error |
| `err.message` | Human-readable description |
| Custom Error classes | `extends Error` for specific error types |

---

## 🏋️ Practice Tasks

### Task 1 — Safe Division Function
Write a function `safeDivide(a, b)` that:
- Throws a `TypeError` if `a` or `b` is not a number
- Throws a `RangeError` if `b` is 0
- Returns the result if valid
```javascript
safeDivide(10, 2);     // 5
safeDivide(10, 0);     // RangeError: Cannot divide by zero
safeDivide("10", 2);   // TypeError: Both arguments must be numbers
```
Wrap each call in `try/catch` and log the error type and message.

---

### Task 2 — Form Validator with Custom Errors
Create a `ValidationError` class (extends `Error`). Write a `validateUser(user)` function that validates:
- `name` must be a non-empty string (min 2 chars)
- `age` must be a number between 0 and 120
- `email` must contain `"@"` and `"."`

Throw a `ValidationError` with the field name for any rule that fails.
```javascript
validateUser({ name: "M", age: 25, email: "manoj@gmail.com" });
// ValidationError: "name must be at least 2 characters" (field: "name")
```

---

### Task 3 — Safe JSON Parser Utility
Write a function `safeParse(jsonString, fallback = null)` that:
- Returns the parsed object if JSON is valid
- Returns the `fallback` value if JSON is invalid (no crash!)
```javascript
safeParse('{"name":"Manoj"}');   // { name: "Manoj" }
safeParse("invalid{{json");      // null
safeParse("bad", []);            // [] (custom fallback)
```

---

> ➡️ **Next:** `13-closures.md`
