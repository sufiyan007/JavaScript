# 📘 JavaScript Functions Deep Notes

This document explains **functions** in JavaScript step by step with simple words, examples, and internal details.

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

