# Async JavaScript: Callbacks, Promises & Async/Await

## Module Introduction
This module explains how JavaScript handles asynchronous code — operations that take time like network requests or timers — without blocking the main thread.

---

## Understanding Synchronous Code Execution ("Sync Code")
Synchronous code runs **line-by-line**, waiting for each operation to complete before moving to the next.

```js
console.log("Start");
console.log("End");
// Output: Start → End
```

---

## Understanding Asynchronous Code Execution ("Async Code")
Async code doesn't block execution. Functions like `setTimeout`, `fetch`, or event listeners run **later**, allowing other code to continue.

```js
console.log("Start");
setTimeout(() => console.log("Async Task"), 1000);
console.log("End");
// Output: Start → End → Async Task
```

---

## Blocking Code & The "Event Loop"
JavaScript uses a **single-threaded** model, meaning only **one task runs at a time**.

If a task takes too long (like a `while(true)` loop or CPU-heavy calculation), it **blocks all other code**, including UI updates.

The **Event Loop** manages asynchronous operations by:

1. Running all synchronous code (Call Stack).
2. Moving async tasks (like setTimeout) into **Callback Queue**.
3. Pushing queued tasks back into the stack **when it's empty**.

```
Call Stack → (executes sync code)
Web APIs → (handles async timers)
Callback Queue → (stores async results)
Event Loop → (moves tasks to stack when free)
```

---

## Sync + Async Code – Execution Order
```js
console.log("1");
setTimeout(() => console.log("2"), 0);
console.log("3");
// Output: 1 → 3 → 2
```

Even with `0ms`, async tasks **always wait** until sync code is done.

---

## Multiple Callbacks & `setTimeout(0)`
```js
setTimeout(() => console.log("A"), 0);
setTimeout(() => console.log("B"), 0);
console.log("C");
// Output: C → A → B
```

---

## Getting Started with Promises
A Promise represents a **future value** that may resolve or reject.

```js
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Done!"), 1000);
});

promise.then(res => console.log(res));
```

---

## Chaining Multiple Promises
```js
fetchUser()
  .then(user => fetchPosts(user.id))
  .then(posts => console.log(posts));
```

---

## Promise Error Handling (`.catch`)
```js
promise
  .then(res => doSomething(res))
  .catch(err => console.error(err));
```

---

## Promise States & `finally`
| State     | Meaning              |
|-----------|----------------------|
| Pending   | Still running        |
| Fulfilled | Success (resolved)   |
| Rejected  | Failed (error)       |

```js
promise.finally(() => console.log("Always runs"));
```

---

## Introduction to `async / await`
```js
async function loadData() {
  const user = await fetchUser();
  const posts = await fetchPosts(user.id);
  console.log(posts);
}
```

---

## Error Handling with `async / await`
```js
async function test() {
  try {
    const data = await fetchData();
  } catch (err) {
    console.error(err);
  }
}
```

---

## Async / Await vs Raw Promises
| Feature      | Promises             | Async/Await (Sugar Syntax) |
|--------------|----------------------|----------------------------|
| Readability  | Nested `.then()`     | Linear top-down            |
| Error Handling | `.catch()`         | `try/catch`                |

---

## `Promise.all()`, `Promise.race()`, etc.
```js
Promise.all([p1, p2]);  // Waits for all
Promise.race([p1, p2]); // Returns first settled
Promise.allSettled([p1, p2]); // Waits for all, returns status
Promise.any([p1, p2]); // First successful promise
```

---

## Microtasks vs Macrotasks Queue (Optional Advanced)
| Queue Type | Example APIs     | Priority |
|------------|------------------|----------|
| Macrotask  | `setTimeout`     | Low      |
| Microtask  | `.then() Promise`| High     |

```js
setTimeout(() => console.log("Timeout"), 0);
Promise.resolve().then(() => console.log("Promise"));

// Output: Promise → Timeout
```

---

## Common Mistakes & Best Practices
❌ Forgetting `await` inside async functions  
✅ Always wrap async code in `try/catch`  
✅ Use `Promise.all` for parallel tasks  

