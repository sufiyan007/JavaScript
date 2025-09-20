# 📘 Section 5: Behind the Scenes

This section explains the inner workings of JavaScript: evolution, scope, hoisting, engine execution, parsing, memory, and browser APIs. All explained with simple examples, memory/engine flow, and interview-style insights.

---

## 1. JavaScript Evolution

* **ES5 vs ES6+ ("Next Gen JS")**:
  * ES5: function, var, objects, arrays.
  * ES6+: `let/const`, arrow functions, classes, template literals, destructuring, modules.
  * Focus: cleaner syntax, block scope, better async handling (Promises, async/await).

### Example:
```js
// ES5
var sum = function(a, b) { return a + b; };

// ES6+
const sum = (a, b) => a + b;
```
* **Interview Tip:** Know major ES6+ features and their benefits (scope, immutability, modern syntax).

---

## 2. Scope & Hoisting

### 🔹 var vs let & const

| Feature       | var                          | let             | const           |
| ------------- | ---------------------------- | --------------- | --------------- |
| Scope         | Function-scoped              | Block-scoped    | Block-scoped    |
| Hoisting      | Yes, initialized `undefined` | Yes, but in TDZ | Yes, but in TDZ |
| Redeclaration | Allowed                      | Not allowed     | Not allowed     |
| Reassignment  | Allowed                      | Allowed         | ❌ Not allowed   |

### 🔹 Understanding Hoisting

**Definition:** JS moves declarations to the top of their scope during memory creation.

* **Function Declarations** → hoisted fully, usable before declaration.
* **Var Variables** → hoisted, initialized as `undefined`.
* **Let/Const Variables** → hoisted, in **TDZ** until assignment.
* **Function Expressions / Arrow Functions** → follow var/let/const rules.

### Example:
```js
console.log(a); // undefined
var a = 10;

console.log(b); // ❌ ReferenceError
let b = 20;

foo(); // ✅ Works
function foo() { console.log("Hello"); }

bar(); // ❌ TypeError
var bar = function() { console.log("World"); };
```
* **Interview Tip:** Hoisting + TDZ questions are common; understand memory creation vs execution phases.

---

## 3. Strict Mode & Good Practices

* `"use strict"` → enforces safer code.
* Catches common mistakes: undeclared variables, duplicate params, assignment to read-only properties.

### Example:
```js
"use strict";
x = 10; // ❌ ReferenceError
```
* **Tip:** Always enable strict mode in modern JS code.

---

## 4. Parsing & Compilation

### 🔹 How Code is Parsed

1. **Tokenizer / Lexer** → converts source code into tokens.
2. **Parser** → creates **AST (Abstract Syntax Tree)**.
3. **Scope Analysis & Hoisting** → done during parsing.

### 🔹 Compilation

* AST → bytecode for interpreter.
* JIT compiler optimizes hot code to machine code.
* Inline caches & hidden classes speed up object access.

### Example:
```js
function add(a, b) { return a + b; }
```
Tokens → AST node → bytecode → JIT optimized machine code.
* **Interview Tip:** Understand parsing → AST → bytecode → JIT flow.

---

## 5. JS Engine & Execution

### 🔹 Execution Context Phases

JavaScript runs code in **two phases** for each function or global code:

1. **Memory Creation Phase (also called Hoisting Phase):**
   * JS engine sets up memory for variables and functions before executing code.
   * Function declarations are fully stored in memory.
   * `var` variables are initialized with `undefined`.
   * `let` and `const` variables are marked as in a **temporal dead zone (TDZ)**.
   * This is **also where the engine sets up the stack and heap**: 
     - **Stack:** keeps track of the function calls and execution order.
     - **Heap:** stores objects, arrays, and functions for long-term use.

2. **Execution Phase:**
   * JS runs code line by line.
   * Variables and functions are used from memory created in the previous phase.

### 🔹 Stack & Heap Explained Simply

* **Stack (Short-term memory):**
  - Keeps track of which function is running now.
  - Works like a stack of plates: last added is the first removed (LIFO).
  - Contains execution contexts (where current function variables are stored).

* **Heap (Long-term memory):**
  - Stores objects, arrays, and functions.
  - Accessible by any function via reference.

### 🔹 JavaScript Execution Flow with Example

```js
function greet() {
  const username = getName();
  console.log("Hello " + username);
}
function getName() {
  return prompt("Enter your name");
}
greet();
```
**Step-by-step Flow:**
1. Global code starts → pushed to **stack**
2. `greet()` called → pushed to stack
3. `getName()` called inside `greet()` → pushed to stack
4. `prompt()` called inside `getName()` → pushed to stack
5. `prompt()` returns → popped from stack
6. `getName()` returns → popped from stack
7. `greet()` finishes → popped from stack
8. Global context finishes → stack is empty

*Memory:* all function definitions and objects live in the heap.

### 🔹 Event Loop (Browser Feature)

* The **JavaScript engine** itself runs code **single-threaded** (one thing at a time).
* **Browser APIs** (like `setTimeout`, DOM events, fetch) are not part of JS engine.
* When you do something async, like click a button or call `setTimeout`:
  - Browser keeps track of the event.
  - Once the stack is empty, browser tells JS engine to handle the event.
  - This is done by the **event loop** which monitors the stack and the task queues.

### Event Loop Example:
```js
console.log('A');
setTimeout(()=>console.log('B'), 0);
Promise.resolve().then(()=>console.log('C'));
console.log('D');
```
**Output:** `A D C B`

*Explanation:*
1. `console.log('A')` → runs immediately
2. `setTimeout` → sent to browser, will execute later
3. `Promise.resolve()` → microtask queue, runs after current stack
4. `console.log('D')` → runs immediately
5. Event loop checks → microtasks run (`C`)
6. Then macrotasks (`B` from setTimeout)

* **Tip:** Always understand **engine vs browser responsibilities** when learning async.

---

## 6. Language vs Browser APIs

* **JavaScript Language:** syntax, functions, objects, arrays.
* **Browser APIs:** DOM, fetch, timers, localStorage, WebSocket.
* Engine handles language; browser provides APIs.

### Example:
```js
console.log(document.title); // Browser API
```
* **Tip:** Know which features are JS engine vs browser provided.

---

## 7. Memory & Garbage Collection

### 🔹 Primitive vs Reference Values

* **Primitive:** number, string, boolean, undefined, null, symbol → stored in **stack**.
* **Reference:** objects, arrays, functions → reference stored in stack, actual data in **heap**.

### Example:
```js
let a = 10;      // primitive
let obj = {x:5}; // reference
```
* **Tip:** Know how primitives vs references behave during assignment & function calls.

## 7. Memory Management & Garbage Collection 

## 1. Memory Allocation

When JavaScript runs, it stores variables, objects, arrays, and functions in memory.

**Memory Areas:**
- **Stack:** short-term memory for primitives and execution contexts (function calls).
- **Heap:** long-term memory for objects, arrays, and functions.

The operating system allocates memory to your browser (Chrome, Firefox, etc.), and the browser has internal memory management to prevent your webpage from using too much memory.

---

## 2. Garbage Collection (GC)

The garbage collector is a built-in mechanism in every JS engine (e.g., V8 in Chrome) that automatically frees memory.

- Runs periodically.
- Detects objects in the heap that have no references pointing to them.
- Reference = a variable or place in code storing the address of the object in heap.

### Example:
```js
let person = { name: "Max" }; // stored in heap, reference in stack
person = null; // object becomes unreachable, GC will clean it
```

**Key Points:**
- Cannot manually trigger GC.
- GC runs smartly on its own schedule.
- Modern JS engines detect unused arrays, objects, and functions automatically.

---

## 3. Memory Management Tips

- Avoid retaining references to objects no longer needed.
- Watch out for:
  - Closures holding large objects.
  - Event listeners not removed.
  - Global variables persisting unnecessarily.

### Example Scenario:
```js
function demo() {
  let obj = { data: [1,2,3] }; // heap allocation
  console.log(obj.data);
  // obj goes out of scope after function ends → GC will clean it
}
demo();
```

Object `obj` is removed after the function finishes if no other references exist.

---

## 4. # Memory Leaks & Event Listeners

### What is a Memory Leak?
- Memory is occupied but never used.
- Happens when references to unused objects remain.

### Simple Example:

```js
// Create an object
let person = { name: "Alice" };

// Use it
console.log(person.name); // Alice

// Forget to remove reference
// person is still pointing to the object
// Even if we don't need it, memory is occupied

Explanation:
The person object is stored in heap memory. As long as person variable exists, JS cannot garbage collect the object, even if we no longer need it.

### Example: Event Listeners
```html
<button id="addListenerBtn">Add Listener</button>
<button id="clickMeBtn">Click Me</button>
```
```js
function printMessage() {
  console.log("Test");
}
document.getElementById("addListenerBtn").addEventListener("click", function() {
  document.getElementById("clickMeBtn").addEventListener("click", printMessage);
});
```
- Clicking "Add Listener" attaches `printMessage` to "Click Me".
- Clicking "Click Me" prints "Test".
- Re-clicking "Add Listener" does NOT add duplicates → JS reuses the same function reference.

### Anonymous Functions Can Introduce Leaks
```js
document.getElementById("addListenerBtn").addEventListener("click", function() {
  document.getElementById("clickMeBtn").addEventListener("click", function() {
    console.log("Test");
  });
});
```
- Every click on "Add Listener" creates a new function object.
- Multiple outputs printed for each click on "Click Me".
- GC cannot clean these while referenced by the button.

**Key Points:**
- Named functions → safer, reused across listeners.
- Anonymous functions inside other functions → new objects each time → potential memory leaks.
- Garbage Collector is smart but cannot fix bad references.
- Too many functions in memory → slow performance.

---

**Tip for SDEs:** Always track references, prefer named functions for event listeners, and understand GC to avoid memory leaks in complex applications.

---

## ✅ Quick Interview Takeaways (Section 5)

* Know **ES5 vs ES6+** key features.
* **var/let/const** + hoisting + TDZ is critical.
* `"use strict"` → safer code.
* Parsing → AST → bytecode → JIT → machine code.
* Stack vs Heap, Execution Context phases, Event Loop → understand async execution.
* Language vs Browser APIs separation.
* Primitive vs Reference values.
* Garbage collection basics.
* Memory management & avoiding leaks.

