# Deep Dive: Classes & Object-Oriented Programming (OOP)

## Overview Table

| Topic | Definition | Why / Use Case |
|-------|-----------|----------------|
| Module Introduction | Overview of Classes & OOP in JS | Understand core concepts for scalable, maintainable code |
| What is OOP? | Programming paradigm using objects and classes | Model real-world entities and behaviors efficiently |
| Getting Started with OOP Code | Basic JS setup for classes | Begin applying OOP principles in code |
| Defining & Using a Class | Blueprint for objects | Reuse code and encapsulate behavior |
| Constructor Methods | Special method to initialize objects | Setup object state on creation |
| Fields vs Properties | Data inside classes | Distinguish internal vs exposed object data |
| Connecting Multiple Classes | Linking classes | Build complex systems with multiple interacting objects |
| Binding Methods & `this` | Ensuring correct context | Avoid bugs when passing methods as callbacks |
| Cart & Shop Class Example | Real-world classes | Example of e-commerce object interaction |
| Class Communication | Classes interacting | Maintain clear and modular architecture |
| Static Methods & Properties | Class-level members | Shared functionality without instantiating objects |
| Classes vs Object Literals | Comparison | Know when to use each for scalability |
| Getters & Setters | Controlled access to properties | Encapsulation, validation, computed properties |
| Inheritance | Subclassing classes | Reuse and extend functionality |
| Using Inheritance Everywhere | Practical use | Apply DRY principle in large codebases |
| Overriding Methods & `super()` | Customize subclass behavior | Extend functionality while keeping base behavior |
| `super()` Execution, Order & `this` | Rules of constructor calls | Ensure correct initialization and context |
| Ways to Add Methods | Different method types | Flexibility in design and encapsulation |
| Private Properties | Restrict access | Encapsulation, avoid external tampering |
| Pseudo-Private Properties | Convention for privacy | Maintain code readability while signaling private members |
| Assignment: Practice Classes & OOP | Hands-on practice | Reinforce concepts with exercises |
| `instanceof` | Operator to check object type | Type validation in OOP code |
| Built-in Classes | Native JS classes | Leverage standard objects like Map, Set, Date |
| Object Descriptors | Property control | Configure writable, enumerable, configurable behavior |

---

## 1. Module Introduction
**Definition:** Overview of Classes & OOP in JavaScript.
**Why:** Understand the foundational concepts to write maintainable, scalable applications.
**Real-World Use:** Prepares for building complex apps like e-commerce platforms, dashboards, games.

## 2. What is Object-Oriented Programming (OOP)?
**Definition:** OOP is a programming paradigm centered around **objects** that encapsulate data (properties) and behavior (methods).
**Why:** Helps model real-world entities, promote code reuse, modularity, and scalability.
**When:** Use OOP when designing systems with interacting entities (e.g., Users, Products, Orders).
**Syntax Example:**
```js
// OOP concept with class
class Product {
  constructor(name, price) {
    this.name = name;
    this.price = price;
  }
  display() {
    console.log(`${this.name}: $${this.price}`);
  }
}
```
**Real-world Project Example:** E-commerce site representing products and cart items.

## 3. Getting Started with OOP Code
**Definition:** Writing the first classes and objects in JS.
**Why:** To initialize objects and methods properly.
**Syntax:**
```js
const prod = new Product('Laptop', 1500);
prod.display();
```
**Best Practice:** Always use `new` with class constructors.

## 4. Defining & Using a Class
**Definition:** Blueprint for creating objects.
**Why:** Reuse code and maintain encapsulated logic.
**Syntax:**
```js
class User {
  constructor(username, email) {
    this.username = username;
    this.email = email;
  }
  greet() {
    console.log(`Hello, ${this.username}`);
  }
}
```
**Example:**
```js
const user1 = new User('Alice', 'alice@mail.com');
user1.greet(); // Hello, Alice
```
**Use Case:** Any scenario where multiple objects share behavior (users, products, orders).

## 5. Constructor Methods
**Definition:** `constructor()` method initializes object properties.
**Why:** Ensures each object starts with correct state.
**Syntax:**
```js
class Car {
  constructor(model, color) {
    this.model = model;
    this.color = color;
  }
}
```
**Example:**
```js
const car1 = new Car('Tesla', 'Red');
console.log(car1.model); // Tesla
```
**Use Case:** Always needed for setting object-specific data at creation.

## 6. Fields vs Properties
**Definition:**
- Fields: variables inside class (JS now supports public/private fields)
- Properties: values attached to instances
**Why:** Distinguish between instance data and accessible properties.
**Example:**
```js
class Person {
  age = 25; // public field
  #ssn = '123-45-6789'; // private field
}
```
**Use Case:** Encapsulate sensitive data; expose only what's necessary.

## 7. Using & Connecting Multiple Classes
**Definition:** Multiple classes interacting with each other.
**Why:** For modular, maintainable systems.
**Example:**
```js
class Shop {
  constructor() {
    this.cart = new Cart();
  }
}
class Cart {
  constructor() {
    this.items = [];
  }
}
```
**Use Case:** E-commerce apps, games, complex dashboards.

## 8. Binding Class Methods & `this`
**Definition:** Ensuring correct `this` context.
**Why:** Methods lose `this` when passed as callbacks.
**Syntax:**
```js
class Logger {
  log() { console.log(this); }
}
const logger = new Logger();
const logFn = logger.log.bind(logger); // bind context
logFn();
```
**Use Case:** Event handlers, timers, asynchronous code.

## 9. Adding a Cart and Shop Class
**Definition:** Example implementation of interacting classes.
**Why:** Demonstrates OOP in real-world scenario.
**Example:**
```js
class Product { constructor(name, price){ this.name=name; this.price=price;} }
class Cart { constructor(){ this.items=[]; } add(p){ this.items.push(p); }}
class Shop { constructor(){ this.cart = new Cart(); }}
```
**Use Case:** Online shopping cart.

## 10. Communicating Between Classes
**Definition:** Passing messages or data between classes.
**Why:** Required for modular systems.
**Example:**
```js
class User { constructor(name){ this.name=name; } }
class MessageService { send(user, msg){ console.log(`${user.name} receives: ${msg}`); }}
```
**Use Case:** Notifications, messaging systems.

## 11. Static Methods & Properties
**Definition:** Methods/properties accessible on class itself, not instance.
**Why:** Shared functionality without object creation.
**Syntax:**
```js
class Utils { static greet(){ console.log('Hello'); } }
Utils.greet();
```
**Use Case:** Utility functions, constants.

## 12. Classes vs Object Literals
**Definition:** Class = blueprint, Object literal = single object.
**Why:** Classes = reusable, Object literal = simple one-off.
**Example:**
```js
const obj = {name:'Alice'};
class User{ constructor(name){ this.name=name; }}
```
**Use Case:** Use classes for multiple similar objects, literals for single use.

## 13. Getters & Setters
**Definition:** Controlled property access.
**Why:** Encapsulation, validation, computed properties.
**Syntax:**
```js
class Person {
  constructor(name){ this._name=name; }
  get name(){ return this._name; }
  set name(val){ this._name = val.toUpperCase(); }
}
```
**Use Case:** Input validation, computed attributes.

## 14. Inheritance
**Definition:** Subclass inherits from superclass.
**Why:** Reuse code, extend behavior.
**Syntax:**
```js
class Animal { speak(){ console.log('Generic sound'); } }
class Dog extends Animal { speak(){ console.log('Woof!'); } }
```
**Use Case:** UI components, animals in game simulation.

## 15. Using Inheritance Everywhere
**Definition:** Applying OOP principles widely.
**Why:** DRY principle, maintainable architecture.
**Example:**
```js
class Vehicle{}; class Car extends Vehicle{}; class Bike extends Vehicle{};
```

## 16. Overriding Methods & `super()`
**Definition:** Replace parent methods in subclass, call parent via `super()`.
**Syntax:**
```js
class Parent { greet(){ console.log('Hi'); } }
class Child extends Parent {
  greet(){ super.greet(); console.log('Child says hello'); }
}
```
**Use Case:** Customize behavior while retaining base logic.

## 17. `super()` Execution, Order & `this`
**Definition:** Rules for calling parent constructor.
**Why:** JS requires `super()` in subclass before using `this`.
**Example:**
```js
class Parent{ constructor(){ this.p='parent'; } }
class Child extends Parent{ constructor(){ super(); this.c='child'; } }
```

## 18. Different Ways of Adding Methods
**Definition:** Class methods, prototype methods, arrow functions.
**Use Case:** Decide encapsulation vs inheritance sharing.

## 19. Private Properties
**Definition:** `#` private fields.
**Why:** Encapsulation.
**Example:**
```js
class User { #password; constructor(p){ this.#password=p; } }
```

## 20. Pseudo-Private Properties
**Definition:** `_name` convention.
**Why:** Signal private, maintain readability.

## 21. Assignment: Practice Classes & OOP
**Definition:** Hands-on exercises.
**Why:** Reinforce learning.

## 22. `instanceof`
**Definition:** Check object type.
**Syntax:** `obj instanceof Class`
**Use Case:** Type validation.

## 23. Built-in Classes
**Definition:** Native JS classes like Map, Set, Date.
**Use Case:** Leverage built-in functionality instead of reinventing.

## 24. Object Descriptors
**Definition:** Control property attributes: writable, enumerable, configurable.
**Syntax:**
```js
Object.defineProperty(obj, 'name', {
  writable: false,
  enumerable: true,
  configurable: false
});
```
**Use Case:** Libraries, APIs, fine-grained control over objects.


