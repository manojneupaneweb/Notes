# 10 — Async JavaScript: Callbacks, Promises, and Async/Await

---

## 📌 What is Asynchronous JavaScript?

JavaScript is **single-threaded** — it can only do one thing at a time. But many tasks take time: fetching data from an API, reading files, waiting for a timer.

**Asynchronous** code allows JavaScript to **start a task, move on to other things**, and come back when the task is done — without freezing the page.

```
Synchronous (blocking):       Asynchronous (non-blocking):
  ┌──────┐                      ┌──────┐
  │Task 1│ ← waits for Task 1   │Task 1│──────► (still running)
  └──────┘                      └──────┘
  ┌──────┐                      ┌──────┐
  │Task 2│ ← waits for Task 2   │Task 2│──────► (starts immediately)
  └──────┘                      └──────┘
```

---

## ⏰ Stage 1: Callbacks (Old Approach)

A **callback** is a function passed to another function that runs when an async task finishes.

```javascript
// setTimeout — runs code after a delay:
setTimeout(() => {
  console.log("This runs after 2 seconds!");
}, 2000);

console.log("This runs first!"); // ← runs immediately

// Output:
// "This runs first!"
// "This runs after 2 seconds!" (after 2s)
```

### The Problem: Callback Hell 😱

When you nest many callbacks, code becomes unreadable:

```javascript
// ❌ Callback hell — pyramid of doom:
getUserData(userId, function(user) {
  getOrders(user.id, function(orders) {
    getOrderDetails(orders[0], function(details) {
      processPayment(details, function(result) {
        console.log("Done!"); // buried 4 levels deep
      });
    });
  });
});
```

---

## 🤝 Stage 2: Promises (ES6)

A **Promise** represents a value that will be available **in the future**. It has three states:

- **Pending** — task is still running
- **Fulfilled** — task succeeded, value is ready
- **Rejected** — task failed, error occurred

```javascript
// Creating a Promise:
const myPromise = new Promise((resolve, reject) => {
  const success = true;

  if (success) {
    resolve("Data loaded! ✅");  // fulfilled
  } else {
    reject("Something went wrong! ❌");  // rejected
  }
});

// Consuming a Promise:
myPromise
  .then(result => {
    console.log(result);  // "Data loaded! ✅"
  })
  .catch(error => {
    console.log(error);   // "Something went wrong! ❌"
  })
  .finally(() => {
    console.log("This always runs!");  // cleanup code
  });
```

### Promise Chaining (Solving Callback Hell):

```javascript
getUserData(userId)
  .then(user => getOrders(user.id))
  .then(orders => getOrderDetails(orders[0]))
  .then(details => processPayment(details))
  .then(result => console.log("Done!"))
  .catch(error => console.error("Error:", error));
// ✅ Linear and readable!
```

### Promise Utility Methods:

```javascript
// Run multiple promises at the same time:
Promise.all([fetchUsers(), fetchPosts(), fetchComments()])
  .then(([users, posts, comments]) => {
    // All three resolved ✅ — runs when ALL finish
    console.log(users, posts, comments);
  })
  .catch(err => console.error(err)); // fails if ANY one rejects

// Wait for all, even if some fail:
Promise.allSettled([fetch("/users"), fetch("/fail")])
  .then(results => {
    results.forEach(r => {
      if (r.status === "fulfilled") console.log(r.value);
      if (r.status === "rejected")  console.log(r.reason);
    });
  });

// Returns the FIRST promise that resolves (race condition):
Promise.race([slowFetch(), fastFetch()])
  .then(result => console.log("First result:", result));

// Returns the FIRST promise that fulfills (ignores rejections):
Promise.any([fetch("/mirror1"), fetch("/mirror2")])
  .then(fastest => console.log("First success:", fastest));
```

---

## ✨ Stage 3: Async/Await (ES8) ✅ Modern Best Practice

`async/await` is **syntactic sugar** over Promises. It lets you write async code that **looks like synchronous code** — much easier to read and write.

```javascript
// Mark a function as async:
async function fetchUser() {
  // await pauses execution until the Promise resolves:
  const response = await fetch("https://jsonplaceholder.typicode.com/users/1");
  const user     = await response.json();  // response.json() is also async!
  console.log(user.name);
}

fetchUser();
```

### Error Handling with `try/catch`:

```javascript
async function loadData() {
  try {
    const response = await fetch("https://api.example.com/data");

    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }

    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("Failed to load:", error.message);
  } finally {
    console.log("Loading complete (success or fail)");
  }
}

loadData();
```

### Parallel Execution with Async/Await:

```javascript
async function loadAllData() {
  // ❌ Sequential (slow — waits for each one):
  const users  = await fetchUsers();
  const posts  = await fetchPosts();

  // ✅ Parallel (fast — all run at the same time):
  const [users, posts] = await Promise.all([fetchUsers(), fetchPosts()]);
  console.log(users, posts);
}
```

---

## 🌐 The Fetch API

`fetch()` is the modern way to make HTTP requests to APIs.

```javascript
// GET request — read data:
async function getUsers() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users");
    const users    = await response.json();
    console.log(users);
  } catch (err) {
    console.error("Network error:", err);
  }
}

// POST request — send data:
async function createPost(data) {
  const response = await fetch("https://jsonplaceholder.typicode.com/posts", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify(data)  // convert JS object to JSON string
  });
  const result = await response.json();
  console.log("Created:", result);
}

createPost({ title: "My Post", body: "Hello!", userId: 1 });
```

### HTTP Methods:

| Method | Purpose |
|--------|---------|
| `GET` | Read/fetch data |
| `POST` | Create new data |
| `PUT` | Replace/update all fields |
| `PATCH` | Update only some fields |
| `DELETE` | Delete data |

### Checking Response Status:

```javascript
const response = await fetch("/api/data");

response.ok           // true if status is 200-299
response.status       // 200, 404, 500, etc.
response.statusText   // "OK", "Not Found", etc.

// Parse different response types:
response.json()   // parse JSON data
response.text()   // parse as plain text
response.blob()   // parse as binary (images, files)
```

---

## 📊 Async Comparison Table

| Approach | Syntax | Readability | Error Handling |
|---------|--------|------------|---------------|
| Callbacks | `fn(callback)` | ❌ Nested (pyramid) | `.catch` in callback |
| Promises | `.then().catch()` | ✅ Chained | `.catch()` |
| Async/Await | `await fn()` | ✅✅ Readable like sync | `try/catch` |

---

## ✅ Key Takeaways

- JavaScript is **non-blocking** — async tasks run in the background.
- **Callbacks** were the original solution but lead to "callback hell".
- **Promises** solved nesting with `.then()` chaining.
- **Async/Await** is the modern, cleanest way to write async code.
- Always use `try/catch` with `async/await` for error handling.
- Use `fetch()` for HTTP requests to APIs.
- Use `Promise.all()` to run multiple async tasks in **parallel**.

---

## 🏋️ Practice Tasks

### Task 1 — setTimeout Chain
Create a countdown from 5 to 0 using `setTimeout` (not `setInterval`).
Each number should appear 1 second after the previous one.
```
5... (after 1s)
4... (after 2s)
3... (after 3s)
2... (after 4s)
1... (after 5s)
🚀 Go! (after 6s)
```
**Hint:** Use recursive setTimeout calls.

---

### Task 2 — Fetch User Profile
Fetch a user from this free API and display their info:
```javascript
const url = "https://jsonplaceholder.typicode.com/users/1";

// Fetch and log:
// Name: Leanne Graham
// Email: Sincere@april.biz
// City: Gwenborough
// Website: hildegard.org
```
Handle errors with `try/catch`. If the fetch fails, log `"Failed to load user"`.

---

### Task 3 — Parallel Fetch (Promise.all)
Fetch **posts** and **users** from the API at the same time using `Promise.all`:
```javascript
const postsUrl = "https://jsonplaceholder.typicode.com/posts?_limit=5";
const usersUrl = "https://jsonplaceholder.typicode.com/users?_limit=5";

// After both load, log:
// "Loaded 5 posts and 5 users"
// Display the title of each post with the matching user's name
```

---

> ➡️ **Next:** `11-es6-modern-features.md` — Essential modern JavaScript features.
