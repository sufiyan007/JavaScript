# Deep Dive: Arrays & Iterables

Arrays and iterables are **foundational tools in JavaScript**. They allow us to **store, organize, and manipulate multiple pieces of data efficiently**. Understanding them deeply is key to writing clean, performant software.

---

## 1. Why Arrays Exist

- Arrays let you **store multiple values in a single variable**.
- They provide **order**, **indexing**, and **methods to manipulate data**.
- Without arrays, you’d need separate variables for every piece of data → messy and inefficient.

**Example:**
```js
const fruits = ["apple", "banana", "mango"];
console.log(fruits[0]); // "apple"
```

✅ Use Case:
- Store lists (users, products, messages)
- Loop through collections
- Apply transformations (map, filter, reduce)

---

## 2. What are Iterables & Array-like Objects?

**Iterable** = an object that **can be looped over** with `for...of`.  
- Arrays, strings, maps, sets → all iterables.  

**Array-like object** = looks like an array (`length` property + numeric indices) but **doesn’t have array methods**.  
- Example: `arguments`, `NodeList`, `HTMLCollection`

```js
const nodeList = document.querySelectorAll("p"); // array-like
console.log(nodeList.length); // works
// nodeList.map(...) → ERROR
```

⚡ Key: You can convert array-like to array:
```js
const arr = Array.from(nodeList);
arr.map(el => console.log(el.textContent));
```

---

## 3. Creating Arrays

Several ways to create arrays:

```js
const arr1 = [1, 2, 3];       // literal
const arr2 = Array(5);        // empty array of length 5
const arr3 = Array.from('hello'); // ['h','e','l','l','o']
```

---

## 4. Which Data Can You Store In Arrays?

- Any type: numbers, strings, booleans, objects, arrays, functions, even other arrays.

```js
const data = [42, 'hello', true, {name: 'Alice'}, [1,2,3], () => console.log('hi')];
```

⚡ Arrays are heterogeneous in JS — no type restriction.

---

## 5. Adding & Removing Elements

### push() / pop()  (end of array)
```js
const arr = [1,2];
arr.push(3);  // [1,2,3]
arr.pop();   // [1,2]
```

### unshift() / shift()  (start of array)
```js
arr.unshift(0); // [0,1,2]
arr.shift();    // [1,2]
```

---

## 6. The splice() Method

- Can add, remove, or replace elements.
```js
const arr = [1,2,3,4];
arr.splice(1, 2, 'a','b'); // remove 2 elements at index 1, insert 'a','b'
console.log(arr); // [1,'a','b',4]
```

---

## 7. slice() Method

- Creates a **shallow copy** or selects a **range**.
```js
const arr = [1,2,3,4];
const sub = arr.slice(1,3); // [2,3]
```

---

## 8. concat() Method

- Merge arrays without modifying originals.
```js
const arr1 = [1,2];
const arr2 = [3,4];
const merged = arr1.concat(arr2); // [1,2,3,4]
```

---

## 9. indexOf() / lastIndexOf()

```js
const arr = [1,2,3,2];
arr.indexOf(2);      // 1
arr.lastIndexOf(2);  // 3
```

---

## 10. find() / findIndex()

```js
const arr = [5,12,8];
arr.find(x => x>10);      // 12
arr.findIndex(x => x>10); // 1
```

---

## 11. includes()

```js
const arr = ['a','b','c'];
arr.includes('b'); // true
```

---

## 12. forEach()

- Alternative to for-loops, executes function on each element.
```js
arr.forEach(item => console.log(item));
```

---

## 13. map()

- Transform array elements, returns a new array.
```js
const nums = [1,2,3];
const squares = nums.map(x => x*x); // [1,4,9]
```

---

## 14. sort() / reverse()

```js
const nums = [3,1,2];
nums.sort();    // [1,2,3]
nums.reverse(); // [3,2,1]
```

⚡ Note: sort() by default sorts as strings.

---

## 15. filter()

- Returns elements that pass a test.
```js
const nums = [1,2,3,4];
const even = nums.filter(x => x%2===0); // [2,4]
```

---

## 16. Arrow Functions Shine

- Cleaner syntax with array methods:
```js
const squares = nums.map(x => x*x);
```

---

## 17. reduce()

- Aggregate array values into a single value.
```js
const sum = [1,2,3].reduce((acc, curr) => acc + curr, 0); // 6
```

---

## 18. Chaining Methods

```js
const result = [1,2,3,4]
  .filter(x => x%2===0)
  .map(x => x*x);
console.log(result); // [4,16]
```

---

## 19. Arrays & Strings - split() / join()

```js
const str = "a,b,c";
const arr = str.split(","); // ['a','b','c']
arr.join("-"); // 'a-b-c'
```

---

## 20. Spread Operator (...)

- Expand elements.
```js
const arr1 = [1,2];
const arr2 = [...arr1,3,4]; // [1,2,3,4]
```

---

## 21. Array Destructuring

```js
const [a,b] = [10,20];
console.log(a,b); // 10 20
```

---

## 22. Maps & Sets Overview

- **Set** = unique values.  
- **Map** = key-value pairs (any type for key).

```js
const set = new Set([1,2,2]); // {1,2}
const map = new Map();
map.set('a', 1);
```

---

## 23. Working with Sets

```js
set.add(3); // {1,2,3}
set.delete(1); // {2,3}
set.has(2); // true
```

---

## 24. Working with Maps

```js
map.set('b',2);
map.get('a'); // 1
map.has('b'); // true
map.delete('a');
```

---

## 25. Maps vs Objects

- Map: keys can be any type, ordered, size property.  
- Object: keys are strings/symbols, unordered, no direct size.

---

## 26. WeakSet & WeakMap

- **WeakSet** = objects only, weak references → GC can clean.  
- **WeakMap** = keys must be objects, weakly referenced.

⚡ Use WeakSet/WeakMap for **memory-efficient caching**.

---

# ✅ Wrap-up

- Arrays = ordered, indexable collections.  
- Iterables = anything JS can loop over.  
- Array methods = push/pop/shift/unshift/splice/map/filter/reduce etc.  
- Map & Set = flexible, modern alternatives for objects and arrays.  
- WeakSet/WeakMap = advanced memory-safe structures.  
- Knowing these is essential for **writing clean, performant JavaScript apps**.
