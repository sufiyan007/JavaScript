# 📘 JavaScript Deep Notes (Interview + Real-World) — Section 5: Behind the Scenes

This section explains the inner workings of JavaScript: evolution, scope, hoisting, engine execution, parsing, memory, and browser APIs. All explained with examples, memory/engine flow, and interview-style insights.

---

## 1. JavaScript Evolution

* **ES5 vs ES6+ ("Next Gen JS")**:  
  - ES5: function, var, objects, arrays.  
  - ES6+: `let/const`, arrow functions, classes, template literals, destructuring, modules.  
  - Focus: cleaner syntax, block scope, better async handling (Promises, async/await).

### Example:

```js
// ES5
var sum = function(a, b) { return a + b; };

// ES6+
const sum = (a, b) => a + b;
```

* **Interview Tip:** Know major ES6+ features and their benefits (scope, immutability, modern syntax).

---

## 2. Scope & Variables

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

## 3. Code Practices

### 🔹 Strict Mode & Good Practices

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

* **Memory Creation Phase (Hoisting)**: variables/functions allocated.  
* **Execution Phase**: code runs line by line.

### 🔹 Stack & Heap

* **Stack:** stores references (primitives, function contexts).  
* **Heap:** stores objects & arrays.

### 🔹 Event Loop

* Call Stack → Tasks (macrotask) → Microtasks (Promises) → Rendering.  
* Async code scheduled correctly without blocking.

### Example:

```js
console.log('A');
setTimeout(()=>console.log('B'), 0);
Promise.resolve().then(()=>console.log('C'));
console.log('D');
```

Output: `A D C B`

---

## 6. Language vs Browser APIs

* **JavaScript Language:** syntax, functions, objects, arrays.  
* **Browser APIs:** DOM, fetch, timers, localStorage, WebSocket.  
* Engine handles language; browser provides APIs.  

### Example:

```js
console.log(document.title); // Browser API
```

* **Tip:** Understand JS vs Browser runtime responsibilities.

---

## 7. Memory Management

### 🔹 Primitive vs Reference Values

* **Primitive** → number, string, boolean, undefined, null, symbol → stored in stack.  
* **Reference** → objects, arrays, functions → reference in stack, data in heap.

### Example:

```js
let a = 10;      // primitive
let obj = {x:5}; // reference
```

### 🔹 Garbage Collection (GC)

* Engine automatically frees memory of unreachable objects.  
* Algorithms: mark-and-sweep, generational GC.

* **Tip:** Avoid memory leaks (forgotten event listeners, closures holding big objects).

---

## ✅ Quick Interview Takeaways (Section 5)

* Know **ES5 vs ES6+** key features.  
* **var/let/const** + hoisting + TDZ is critical.  
* `"use strict"` → safer code.  
* Parsing → AST → bytecode → JIT → machine code.  
* Stack vs Heap, Event Loop → understand async execution.  
* Language vs Browser APIs separation.  
* Garbage collection basics, primitives vs references.


