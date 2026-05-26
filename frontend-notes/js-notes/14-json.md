# 14 — JSON

---

## 📌 What is JSON?

**JSON** (JavaScript Object Notation) is a lightweight **data format** used to send and receive data between a client and a server (APIs).

- JSON is **text** — a plain string that looks like a JavaScript object.
- Every API you use (weather, payments, social media) sends data as JSON.
- JSON is language-independent — Python, Java, PHP all use it too.

> 💡 **Analogy:** JSON is like a universal shipping box — everyone knows how to pack and unpack it, regardless of where it came from.

---

## 📊 JSON vs JavaScript Object

```javascript
// JavaScript Object (in your code):
const user = {
  name: "Manoj",
  age: 20,
  isStudent: true,
  hobbies: ["coding", "reading"],
  address: {
    city: "Kathmandu",
    country: "Nepal"
  }
};

// JSON (what you send/receive over the internet — a STRING):
const userJSON = '{"name":"Manoj","age":20,"isStudent":true,"hobbies":["coding","reading"],"address":{"city":"Kathmandu","country":"Nepal"}}';
```

### JSON Rules (vs JavaScript):

| Rule | JavaScript Object | JSON |
|------|-----------------|------|
| Keys | Can be unquoted | **Must be in double quotes `"`** |
| Strings | Single or double quotes | **Double quotes only `"`** |
| Functions | Allowed | ❌ Not allowed |
| `undefined` | Allowed | ❌ Not allowed |
| Comments | Allowed | ❌ Not allowed |
| Trailing commas | Allowed | ❌ Not allowed |

---

## 🔄 `JSON.stringify()` — JS Object → JSON String

Converts a JavaScript object into a JSON string (to send to a server).

```javascript
const user = {
  name: "Manoj",
  age: 20,
  isStudent: true
};

const jsonString = JSON.stringify(user);
console.log(jsonString);
// '{"name":"Manoj","age":20,"isStudent":true}'
console.log(typeof jsonString); // "string"

// Pretty print (with indentation):
console.log(JSON.stringify(user, null, 2));
// {
//   "name": "Manoj",
//   "age": 20,
//   "isStudent": true
// }
```

### What Gets Removed by `JSON.stringify()`:

```javascript
const obj = {
  name: "Manoj",
  greet: function() { return "Hi!"; },  // ❌ removed — functions not allowed
  age: undefined,                        // ❌ removed — undefined not allowed
  score: null,                           // ✅ kept — null is valid
  active: true                           // ✅ kept
};

JSON.stringify(obj);
// '{"name":"Manoj","score":null,"active":true}'
```

---

## 🔄 `JSON.parse()` — JSON String → JS Object

Converts a JSON string back into a usable JavaScript object (received from a server).

```javascript
const jsonString = '{"name":"Manoj","age":20,"hobbies":["coding","reading"]}';

const user = JSON.parse(jsonString);
console.log(user.name);           // "Manoj"
console.log(user.hobbies[0]);     // "coding"
console.log(typeof user);         // "object"

// Always handle parse errors:
try {
  const data = JSON.parse("invalid json{{{");
} catch (err) {
  console.error("Invalid JSON:", err.message); // SyntaxError
}
```

---

## 🌐 JSON with the Fetch API (Most Common Real-World Use)

```javascript
// GET — reading JSON from an API:
async function getUsers() {
  const response = await fetch("https://jsonplaceholder.typicode.com/users");
  const users    = await response.json();  // internally calls JSON.parse()
  console.log(users[0].name);             // "Leanne Graham"
}

// POST — sending JSON to an API:
async function createPost(postData) {
  const response = await fetch("https://jsonplaceholder.typicode.com/posts", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"   // tell server we're sending JSON
    },
    body: JSON.stringify(postData)          // convert object to JSON string
  });

  const created = await response.json();   // parse the JSON response
  console.log("Created post ID:", created.id);
}

createPost({ title: "My Post", body: "Hello!", userId: 1 });
```

---

## 💾 JSON with localStorage

LocalStorage stores strings — use JSON to save/load objects.

```javascript
const settings = {
  theme: "dark",
  fontSize: 16,
  language: "en"
};

// Save object to localStorage:
localStorage.setItem("settings", JSON.stringify(settings));

// Load object from localStorage:
const saved = JSON.parse(localStorage.getItem("settings"));
console.log(saved.theme);  // "dark"

// Safe loading (handles null if key doesn't exist):
const data = JSON.parse(localStorage.getItem("settings") ?? "null");
if (data) {
  console.log("Loaded settings:", data);
} else {
  console.log("No saved settings, using defaults.");
}
```

---

## 🧹 Deep Clone with JSON (Quick Trick)

```javascript
// Shallow copy (problem with nested objects):
const original = { name: "Manoj", address: { city: "Kathmandu" } };
const shallow  = { ...original };
shallow.address.city = "Pokhara";
console.log(original.address.city); // "Pokhara" ← MUTATED! Bug!

// Deep copy with JSON (quick and simple — but loses functions/undefined):
const deep = JSON.parse(JSON.stringify(original));
deep.address.city = "Pokhara";
console.log(original.address.city); // "Kathmandu" ← Safe! ✅

// ⚠️ Limitations: removes functions, undefined, Dates become strings
```

---

## 📊 Valid JSON Data Types

JSON supports only these types:

| Type | Example |
|------|---------|
| String | `"Hello"` |
| Number | `42`, `3.14` |
| Boolean | `true`, `false` |
| Null | `null` |
| Array | `[1, "two", true]` |
| Object | `{"key": "value"}` |

❌ **NOT valid JSON:** `undefined`, functions, `Date`, `Symbol`, `BigInt`

---

## ✅ Key Takeaways

| Method | Direction | Use |
|--------|-----------|-----|
| `JSON.stringify(obj)` | JS Object → String | Send to API, save to localStorage |
| `JSON.parse(str)` | String → JS Object | Receive from API, load from localStorage |

- JSON uses **double quotes only** for keys and strings.
- Wrap `JSON.parse()` in `try/catch` — bad JSON throws a `SyntaxError`.
- Use `response.json()` in Fetch (it calls `JSON.parse()` for you).
- JSON deep clone trick works but removes functions and `undefined`.

---

## 🏋️ Practice Tasks

### Task 1 — Stringify & Parse Roundtrip
```javascript
const student = {
  name: "Manoj",
  age: 20,
  grades: [85, 90, 78],
  address: { city: "Kathmandu", zip: "44600" },
  greet() { return "Hi!"; }  // ← watch what happens to this!
};
```
1. Convert `student` to a JSON string and log it
2. Pretty-print it with 2-space indentation
3. Parse it back into an object and access `student.address.city`
4. What happened to the `greet` method? Why?

---

### Task 2 — Save & Load Settings (localStorage)
Build a simple settings system:
```javascript
const defaultSettings = { theme: "light", fontSize: 14, language: "en" };

// 1. Save settings to localStorage as JSON
// 2. Load them back from localStorage
// 3. Update theme to "dark" and save again
// 4. Load again and confirm theme is "dark"
// 5. If nothing is in localStorage, use defaultSettings
```

---

### Task 3 — Fetch & Display JSON from API
Fetch the first 5 posts from `https://jsonplaceholder.typicode.com/posts?_limit=5`.
For each post, log a formatted card:
```
📄 Post #1
Title  : sunt aut facere repellat...
Preview: quia et suscipit suscipit...
```
Handle the case where the fetch fails (simulate by using a bad URL and catch the error).

---

> 🎉 You now have all the JavaScript knowledge needed to start **React** or **Node.js**!
