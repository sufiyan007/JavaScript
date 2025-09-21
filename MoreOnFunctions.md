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

---

## 9. Outputting Messages
Ways to communicate with the user:
- `console.log("Debug")`
- `alert("Hello!")`
- `prompt("Enter your name")`

---

## 10. Default Arguments
Set default values if no argument is passed.

```js
function greet(name = "Guest") {
  console.log("Hello " + name);
}

greet(); // Hello Guest
```

---

## 11. Rest Parameters (`...`)
Collects multiple arguments into an array.

```js
function sum(...nums) {
  return nums.reduce((a, b) => a + b, 0);
}
console.log(sum(1, 2, 3, 4)); // 10
```

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

## 13. Callback Functions
A **function passed as an argument** to another function.

```js
function greet(name, callback) {
  console.log("Hello " + name);
  callback();
}

greet("Alice", () => console.log("Welcome!"));
```

👉 Callbacks are heavily used in async code (like APIs, setTimeout, events).

---

## 15. Adding `bind()` to Calculator

```js
const calculator = {
  num: 10,
  add: function(a) {
    return this.num + a;
  }
};

const addFn = calculator.add.bind(calculator);
console.log(addFn(5)); // 15
```
✔️ Here `bind()` makes sure `this` always refers to the `calculator` object.

---

# 🔗 `bind()`, `call()`, and `apply()` in JavaScript

In JavaScript, functions are **objects**.  
That means we can control **how they run** and **what `this` points to** inside them.  
For this, we use **3 helpers**: `bind`, `call`, and `apply`.

---

## 1. `bind()` → **Attach & Store a Function with a Fixed `this`**
- It **does not run immediately**.
- Instead, it **returns a new function** with `this` permanently set.

📌 Example:
```js
const user = {
  name: "Sufiyan",
  greet: function() {
    console.log(`Hello, ${this.name}`);
  }
};

const greetFn = user.greet.bind(user);
greetFn(); // Hello, Sufiyan
```

💡 **Why use it?**
- Useful when passing functions around (like callbacks) where `this` can get lost.
- Example: event listeners, setTimeout, or calculator methods.

---

## 2. `call()` → **Run Function Immediately with `this`**
- Runs the function **right away**.
- You pass `this` as the **first argument**, then normal arguments.

📌 Example:
```js
function introduce(greeting, age) {
  console.log(`${greeting}, I am ${this.name} and I am ${age} years old`);
}

const person = { name: "Ali" };

introduce.call(person, "Hi", 25);
// Hi, I am Ali and I am 25 years old
```

💡 **Why use it?**
- If you want to borrow a method from one object and use it on another.
- Runs the function directly.

---

## 3. `apply()` → **Almost Same as `call()`, but Arguments as Array**
- Useful when you **already have arguments in an array**.

📌 Example:
```js
function introduce(greeting, age) {
  console.log(`${greeting}, I am ${this.name} and I am ${age} years old`);
}

const person = { name: "Ali" };

introduce.apply(person, ["Hello", 25]);
// Hello, I am Ali and I am 25 years old
```

💡 **Why use it?**
- When arguments come in the form of an array (like `Math.max()` trick).

```js
console.log(Math.max.apply(null, [1, 5, 7, 2])); // 7
```

---

## 🔑 Quick Difference Table

| Method  | Runs Immediately? | Arguments Format | Returns |
|---------|-------------------|------------------|---------|
| `bind`  | ❌ No             | Normal           | A new function |
| `call`  | ✅ Yes            | Normal           | Function result |
| `apply` | ✅ Yes            | Array            | Function result |

---

## 🎯 Where to Use in Real Life
1. **bind()** → Fixing `this` in event handlers or when passing functions.
   ```js
   const button = document.querySelector("button");
   button.addEventListener("click", user.greet.bind(user));
   ```

2. **call()** → Borrowing methods.
   ```js
   const obj1 = { name: "A" };
   const obj2 = { name: "B" };
   
   function sayHello() { console.log(this.name); }

   sayHello.call(obj1); // A
   sayHello.call(obj2); // B
   ```

3. **apply()** → When arguments are in arrays.
   ```js
   const numbers = [3, 5, 1, 10];
   console.log(Math.max.apply(null, numbers)); // 10
   ```

---

⚡ **In short**:  
- Use **`bind`** when you want to **save a function for later** with fixed `this`.  
- Use **`call`** when you want to **run immediately with separate arguments**.  
- Use **`apply`** when you want to **run immediately with array arguments**.  

