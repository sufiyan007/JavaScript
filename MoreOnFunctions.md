# 📘 JavaScript Functions (Deep Notes for SDE Interviews)

Functions are one of the **core building blocks** in JavaScript.  
They allow us to group logic, reuse code, and handle asynchronous tasks.  

Let’s learn topic by topic 👇

---

## 1. Parameters vs Arguments
- **Parameters** → placeholders written in the function definition.  
- **Arguments** → actual values you pass when calling the function.  

```js
function greet(name) { // 'name' = parameter
  console.log("Hello " + name);
}

greet("Alice"); // "Alice" = argument
```

👉 Think of parameters as *empty containers* and arguments as the *water you pour inside*.

---

## 2. Functions vs Methods
- **Function:** Independent block of code.
- **Method:** A function that lives inside an object.

```js
function add(a, b) {
  return a + b; // function
}

const calculator = {
  multiply(x, y) {
    return x * y; // method
  }
};
```

👉 Methods always belong to an object.

---

## 3. Functions are Objects!
In JavaScript, **functions themselves are objects**.  
This means:
- You can store them in variables.
- Pass them as arguments.
- Attach properties to them.

```js
function sayHi() { console.log("Hi!"); }
sayHi.language = "English";

console.log(sayHi.language); // English
```

---

## 4. Function Expressions
You can store a function inside a variable.

```js
const greet = function(name) {
  return "Hello " + name;
};
console.log(greet("Bob"));
```

👉 Expression = “assigning” a function.

---

## 5. Function Expressions vs Declarations
- **Declaration:** Hoisted (available before execution).  
- **Expression:** Not hoisted.

```js
// Declaration
function sum(a, b) {
  return a + b;
}

// Expression
const sum2 = function(a, b) {
  return a + b;
};
```

---

## 6. Anonymous Functions
Functions without names.  
Used where you don’t need to reuse them.
This helps to avoid the memory leak

```js
setTimeout(function() {
  console.log("Runs once after 1 sec");
}, 1000);
```

---

## 7. Arrow Functions
A **shorter syntax** for writing functions.

```js
const greet = (name) => "Hello " + name;
```

---

## 8. Arrow Function Syntax Variations
```js
const square = x => x * x;      // single param
const add = (a, b) => a + b;    // multiple params
const log = () => console.log("Hi!"); // no params
```
4️⃣ Rules for implicit return

Works only with a single expression.
Curly braces {} mean a function block → then you must use return.

---

## 9. Outputting Messages
Ways to communicate with the user:
- `console.log("Debug")`
- `alert("Hello!")`
- `prompt("Enter your name")`

---

## 10. Default Arguments
Default arguments let you give a function parameter a default value.
If the caller doesn’t pass a value (or passes undefined), the default is used.
This helps avoid undefined values and makes functions safer.

```js
function greet(name = "Guest") {
  console.log("Hello " + name);
}

greet();           // Hello Guest
greet("Sufiyan");  // Hello Sufiyan
```
name = "Guest" → sets a default value "Guest".
If we call greet() without arguments, name automatically becomes "Guest".

---

## 11. Rest Parameters (`...`)
Rest parameters allow a function to accept any number of arguments and collect them into an array.
Syntax: ...name
Only one rest parameter is allowed per function, and it must be the last parameter.

```js
function sum(...nums) {
  console.log(nums); // [1, 2, 3, 4]
  return nums.reduce((a, b) => a + b, 0);
}

console.log(sum(1, 2, 3, 4)); // 10
```
✅ Explanation:
...nums collects all arguments into an internal array called nums.
You can now use array methods like for...of, reduce, map, etc.
Rest parameter must be last, because it will collect all remaining arguments.
Older JavaScript had arguments object, which is array-like but not a real array.
...rest is a real array, so you can use all array methods directly.

---

## 12. Functions Inside Functions
Yes, functions can live inside other functions.

```js
function outer() {
  function inner() {
    console.log("I am inner");
  }
  inner();
}
outer();
```

---

## 12. Callback Functions

* **Definition:** A callback function is a function passed as an argument to another function, which is then executed inside that function.
* **Purpose:** Provides flexibility and allows asynchronous code handling.

### Basic Example

```javascript
function greet(name, callback) {
  console.log("Hello " + name);
  callback(); // executes the passed function
}

greet("Alice", () => console.log("Welcome!"));
```

**Output:**

```
Hello Alice
Welcome!
```

### Named Callback Example

```javascript
function sayWelcome() {
  console.log("Welcome!");
}

greet("Bob", sayWelcome);
```

**Output:**

```
Hello Bob
Welcome!
```

### Callbacks in Asynchronous Code

* **Timers:**

```javascript
setTimeout(() => {
  console.log("Executed after 2 seconds");
}, 2000);
```

* **Event listeners:**

```javascript
document.querySelector("button").addEventListener("click", () => {
  console.log("Button clicked!");
});
```

* **APIs / fetch requests:**

```javascript
fetch("https://api.example.com/data")
  .then(response => response.json())
  .then(data => console.log(data)); // functions inside then() are callbacks
```

> **Note:** We are not executing the function directly; the browser or runtime executes it when an event occurs or something happens.

### Benefits of Callbacks

1. **Code Reusability:** Different functions can be passed as callbacks.
2. **Flexibility:** Determines what happens after an operation.
3. **Asynchronous Handling:** Handles timers, events, or network requests.

### Key Points

* Can be **anonymous or named**.
* Executed automatically when the event occurs or when called inside the main function.
* Often replaced by **Promises or async/await** in modern JavaScript for readability.

---

## 15. This and Bind

## 1. Object Method Call

```javascript
const person = {
  name: "Sufiyan",
  greet: function() {
    console.log(this.name);
  }
};

person.greet(); // Hello Sufiyan ✅
```
- `person` object → memory address 123
- `greet` function → memory address 456
- Calling `person.greet()` → `this` points to `person`

---

## 2. Detached Function

```javascript
const greetFunc = person.greet;
greetFunc(); // undefined ❌
```
- `greetFunc` stores **address 456** (same function code)
- **No object is calling it**, so `this = undefined`
- `this.name` → `undefined.name` → prints undefined

### Key Idea
- `this` depends on **how the function is called**, not the function itself.

---

## 3. Callback Example

```javascript
btn.addEventListener('click', greetFunc);
```
- `greetFunc` passed as a callback
- Browser calls it as `callback.call(button)`
- `this` points to the button, not `person`
- So `this.name` = undefined unless we bind it

---

## 4. Using `bind()`

```javascript
const boundGreet = person.greet.bind(person);
boundGreet(); // Hello Sufiyan ✅
```
- `bind(person)` creates a **new function** (say address 789)
- Inside this new function, `this` is **permanently fixed to `person`**
- Even if called somewhere else, `this` points to `person`
- Works in callbacks, timers, or detached calls

---

## 5. Summary Table

| Variable       | Function Address | `this` inside function |
|----------------|-----------------|-----------------------|
| `person.greet` | 456             | person (when called as person.greet()) |
| `greetFunc`    | 456             | undefined (detached) |
| `boundGreet`   | 789 → wraps 456 | permanently set to person |

---

### ✅ Key Points
1. `this` = the object **that called the function**
2. Detached function = function taken out of its object → `this` is lost
3. `bind()` = lock `this` to a specific object and create a new function
4. `bind()` is useful for callbacks, timers, or when the function is detached from its object

