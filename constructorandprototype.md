# Deep Dive: Constructor Functions & Prototypes

JavaScript is a prototypal language, meaning inheritance works via prototypes, not classical classes (although `class` syntax exists as sugar). Understanding constructor functions, prototypes, and the prototype chain is key to writing efficient, maintainable JS code.

---

## 1. Module Introduction

This module teaches:
- How constructor functions create objects.
- How prototypes enable shared behavior.
- Differences between classes vs constructor functions.
- How the prototype chain works internally.

---

## 2. Introducing Constructor Functions

Before `class` syntax, JS used constructor functions to create multiple similar objects.

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

const person1 = new Person("Alice", 25);
const person2 = new Person("Bob", 30);

console.log(person1.name); // Alice
console.log(person2.age);  // 30
```

**How it works:**
- `new Person()` creates a new object.
- `this` inside constructor points to the new object.
- Properties assigned with `this` become own properties of that object.

---

## 3. Constructor Functions vs Classes & Understanding `new`

### `new` keyword does 4 things:
1. Creates a new empty object.
2. Sets the new object’s internal prototype (`[[Prototype]]`) to the constructor function’s `.prototype`.
3. Binds `this` in the constructor to the new object.
4. Returns the object (unless constructor returns an object explicitly).

**Example:**
```js
function Dog(name) {
  this.name = name;
}

Dog.prototype.bark = function() {
  console.log(`${this.name} barks`);
};

const dog1 = new Dog("Buddy");
dog1.bark(); // Buddy barks
```

---

## 4. Introducing Prototypes

- Every function in JS has a `prototype` property, which is an object.
- Objects created with a constructor have `__proto__` pointing to that prototype.
- Shared methods are usually stored on the prototype.

**Example:**
```js
function Person(name) {
  this.name = name;
}
Person.prototype.greet = function() {
  console.log(`Hi, I am ${this.name}`);
};

const p1 = new Person("Alice");
const p2 = new Person("Bob");

p1.greet(); // Hi, I am Alice
p2.greet(); // Hi, I am Bob
```

✅ Key point: `greet()` is shared, not duplicated on each instance.

---

## 5. Prototypes - Summary

- `constructor.prototype` → object used as template for instances.
- `instance.__proto__` → points to that prototype.
- Shared methods should live on the prototype to save memory.
- `instanceof` checks if an object exists in the prototype chain.

```js
console.log(p1.__proto__ === Person.prototype); // true
console.log(p1 instanceof Person);             // true
```

---

## 6. Working with Prototypes

You can add, modify, or remove prototype methods anytime:
```js
Person.prototype.sayBye = function() {
  console.log(`${this.name} says bye`);
};
p1.sayBye(); // Alice says bye
```

- Own properties shadow prototype properties.
```js
p1.name = "Charlie";
p1.greet(); // Hi, I am Charlie
```

---

## 7. The Prototype Chain & Global `Object`

- Every object has an internal `[[Prototype]]` (`__proto__`).
- If a property/method is not found on the object, JS looks up the prototype chain.
- The chain ends at `Object.prototype`.

**Example:**
```js
const obj = {};
console.log(obj.toString()); // "[object Object]"
```
- `toString` is not own property of `obj`, found in `Object.prototype`.

**Prototype Chain Example:**
```
dog1 ---> Dog.prototype ---> Object.prototype ---> null
```

---

## 8. Classes & Prototypes

`class` syntax is just syntactic sugar over constructor functions:
```js
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(`Hi, I am ${this.name}`);
  }
}
```
Equivalent:
```js
function Person(name) {
  this.name = name;
}
Person.prototype.greet = function() {
  console.log(`Hi, I am ${this.name}`);
};
```

---

## 9. Methods in Classes & In Constructors

- Methods in constructor → each instance gets a new copy (not memory efficient).
- Methods in prototype/class body → shared among instances.

```js
function Person(name) {
  this.name = name;
  this.sayHi = function() { console.log(this.name); }
}
Person.prototype.sayBye = function() { console.log("Bye"); }
```

---

## 10. Built-in Prototypes in JavaScript

Many JS built-ins use prototypes:
```js
const arr = [1,2,3];
console.log(arr.map); // function map() {...} on Array.prototype

const str = "hello";
console.log(str.toUpperCase()); // String.prototype.toUpperCase()
```
- This is why you can call `.map()` or `.toUpperCase()`.

---

## 11. Setting & Getting Prototypes

- `Object.getPrototypeOf(obj)` → returns prototype
- `Object.setPrototypeOf(obj, proto)` → sets prototype

```js
const animal = { eats: true };
const rabbit = { jumps: true };

Object.setPrototypeOf(rabbit, animal);
console.log(rabbit.eats); // true
```
⚡ Changing prototypes at runtime can hurt performance.

---

## ✅ Wrap-up

- Constructor functions + `new` → old way to create objects.
- Prototypes allow shared methods to save memory.
- Prototype chain → how JS looks for properties/methods.
- `class` syntax → cleaner, modern syntax.
- Understanding prototypes is essential for inheritance, memory efficiency, and debugging.

