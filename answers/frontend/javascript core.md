Sure! Below are the answers for all the **JavaScript Core for Frontend** questions:

---

### **1. What is the difference between `var`, `let`, and `const` in JavaScript?**

- **`var`**: Declares a variable that is function-scoped or globally-scoped (if declared outside a function). Variables declared with `var` can be redeclared and updated.
- **`let`**: Declares a block-scoped variable. Variables declared with `let` can be updated but cannot be redeclared in the same scope.
- **`const`**: Declares a block-scoped variable that cannot be reassigned after initialization. However, objects and arrays declared with `const` can still have their properties or elements modified.

---

### **2. What is hoisting in JavaScript? How does it affect `var`, `let`, and `const`?**

**Hoisting** is the behavior of JavaScript where variable and function declarations are moved to the top of their containing scope during the compile phase, before the code execution.

- **`var`**: Variables declared with `var` are hoisted and initialized with `undefined`.
- **`let` and `const`**: Both `let` and `const` are hoisted to the top, but they remain in a **temporal dead zone** (TDZ) until their declaration is encountered in the code. Accessing them before the declaration throws a `ReferenceError`.

---

### **3. What is the event loop in JavaScript, and how does it work?**

The **event loop** is responsible for executing the code, collecting and processing events, and executing sub-tasks (callback functions, promises, etc.) in the correct order. The event loop continuously checks if the call stack is empty. If it is, it pushes the callback or event to the stack from the message queue.

- The event loop processes synchronous code first (from the call stack) and then handles asynchronous code (from the message queue).

---

### **4. Explain closures in JavaScript. Why are they useful?**

A **closure** is a function that "remembers" its lexical scope even when the function is executed outside that scope. This happens because JavaScript functions create closures when they are defined within another function.

**Example:**

```javascript
function outer() {
  let counter = 0;
  return function inner() {
    counter++;
    console.log(counter);
  };
}

const increment = outer();
increment(); // 1
increment(); // 2
```

**Why useful?**  
Closures allow for data encapsulation and private variables, which are useful in many patterns like data privacy and function currying.

---

### **5. What is the `this` keyword in JavaScript? How does it work in different contexts?**

The `this` keyword refers to the context in which a function is executed. Its value depends on how the function is called.

- **Global Context**: In the global execution context, `this` refers to the global object (`window` in browsers).
- **Method Context**: Inside an object method, `this` refers to the object.
- **Constructor Function**: Inside a constructor, `this` refers to the newly created object.
- **Arrow Functions**: In arrow functions, `this` retains the value from the surrounding non-arrow function's `this`.

---

### **6. What are promises in JavaScript? How do `then`, `catch`, and `finally` work with promises?**

A **promise** is an object representing the eventual completion or failure of an asynchronous operation. It has three states: **pending**, **resolved**, or **rejected**.

- **`then()`**: Defines the callback to be executed if the promise is resolved.
- **`catch()`**: Defines the callback to be executed if the promise is rejected.
- **`finally()`**: Executes code regardless of the promise's resolution or rejection (clean-up tasks).

```javascript
let promise = new Promise((resolve, reject) => {
  resolve("Success");
});

promise
  .then((message) => console.log(message)) // Success
  .catch((error) => console.error(error))
  .finally(() => console.log("Done"));
```

---

### **7. What is the difference between `null` and `undefined`?**

- **`undefined`**: A variable that has been declared but not assigned a value is `undefined`. It also represents the absence of a value or an uninitialized state.
- **`null`**: Represents the intentional absence of any object value. It is an assignment value used to explicitly indicate no value.

---

### **8. What are higher-order functions in JavaScript?**

A **higher-order function** is a function that takes one or more functions as arguments or returns a function as its result.

**Example:**

```javascript
function applyOperation(a, b, operation) {
  return operation(a, b);
}

function add(x, y) {
  return x + y;
}

console.log(applyOperation(2, 3, add)); // 5
```

---

### **9. Explain the concept of prototypal inheritance in JavaScript.**

**Prototypal inheritance** is a way for objects to inherit properties and methods from other objects. Every JavaScript object has a **prototype**, which is another object, and it inherits properties and methods from this prototype.

**Example:**

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function () {
  console.log(`Hello, ${this.name}!`);
};

const john = new Person("John");
john.greet(); // Hello, John!
```

---

### **10. What is the difference between `==` and `===` in JavaScript?**

- **`==` (loose equality)**: Compares values for equality after performing type coercion if necessary.
- **`===` (strict equality)**: Compares both the value and the type, and does not perform type coercion.

```javascript
console.log(5 == "5"); // true
console.log(5 === "5"); // false
```

---

### **11. What are JavaScript modules? How do `import` and `export` work?**

**JavaScript modules** allow code to be divided into separate files, making it more maintainable and reusable.

- **`export`**: Used to export functions, objects, or variables from a module.
- **`import`**: Used to import exported code into another module.

**Example:**

```javascript
// module.js
export function greet() {
  console.log("Hello!");
}

// app.js
import { greet } from "./module.js";
greet(); // Hello!
```

---

### **12. What is the `bind()`, `call()`, and `apply()` methods in JavaScript? How are they different?**

- **`bind()`**: Returns a new function that, when called, has its `this` set to the provided value.
- **`call()`**: Calls a function with a specified `this` value and arguments passed immediately.
- **`apply()`**: Calls a function with a specified `this` value and an array of arguments.

**Example:**

```javascript
function greet() {
  console.log(`Hello, ${this.name}`);
}

const person = { name: "John" };
greet.call(person); // Hello, John
```

---

### **13. What is event delegation in JavaScript?**

**Event delegation** is a technique where instead of attaching event listeners to individual child elements, you attach a single event listener to a parent element. The event propagates through the DOM, and you can check the target of the event to identify which child element triggered it.

```javascript
document.getElementById("parent").addEventListener("click", function (e) {
  if (e.target && e.target.matches("button")) {
    console.log("Button clicked");
  }
});
```

---

### **14. What are arrow functions in JavaScript? How do they differ from regular functions?**

**Arrow functions** provide a more concise syntax for writing functions. They also do not have their own `this`, so they inherit it from the surrounding lexical scope.

**Example:**

```javascript
const greet = () => console.log("Hello!");
```

**Difference from regular functions**:

- No `this` binding.
- Cannot be used as constructors (no `new` keyword).
- No `arguments` object.

---

### **15. What is the spread operator and rest parameter in JavaScript?**

- **Spread operator (`...`)**: Used to unpack elements from an array or object.
- **Rest parameter (`...`)**: Used to gather elements into an array, often used in function arguments.

```javascript
// Spread
let arr = [1, 2, 3];
let newArr = [...arr, 4, 5]; // [1, 2, 3, 4, 5]

// Rest
function sum(...numbers) {
  return numbers.reduce((a, b) => a + b, 0);
}
console.log(sum(1, 2, 3)); // 6
```

---

### **16. What are `setTimeout()` and `setInterval()` functions in JavaScript? How do they work?**

- **`setTimeout()`**: Executes a function once after a specified delay.
- **`setInterval()`**: Executes a function repeatedly, with a fixed time delay between each call.

```javascript
setTimeout(() => console.log("Hello"), 1000); // Executes after 1 second
setInterval(() => console.log("Repeating"), 1000); // Repeats every second
```

---

### **17. What is the difference between synchronous and asynchronous code in JavaScript?**

- **Synchronous code**: Executes sequentially, blocking the execution of the next operation until the current one is complete.
- **Asynchronous code**: Executes independently, allowing the program to continue running other operations while waiting for completion.

---

### **18. How does JavaScript handle asynchronous operations?**

JavaScript uses **callback functions**, **promises**, and **async/await** to handle asynchronous operations. These mechanisms allow the program to continue execution without blocking.

---

### **19. What is the `forEach()` method in JavaScript? How is it different from `map()` and `filter()`?**

- **`forEach()`**: Iterates over an array but does not return a value (used for side-effects).
- **`map()`**: Creates a new array with the results of calling a function on every element.
- **`filter()`**: Creates a new array with elements that pass a test (i.e., elements that meet a certain condition).

---

### **20. What are the different ways to handle errors in JavaScript?**

- **`try...catch`**: Catches and handles exceptions.
- **`throw`**: Manually throws an error.
- **`finally`**: Executes code after the `try...catch` block, regardless of whether an error was thrown.

---

# section - 2

Sure! Here are answers to the additional **JavaScript Core** questions:

---

### **1. What is the difference between `undefined` and `undeclared` variables?**

- **`undefined`**: A variable that has been declared but not assigned a value is `undefined`. It is also the default value of uninitialized variables.
- **`undeclared`**: A variable that has not been declared at all. Accessing an undeclared variable will result in a `ReferenceError`.

```javascript
console.log(a); // ReferenceError: a is not defined
```

---

### **2. How does JavaScript handle variable scoping in functions?**

JavaScript uses **lexical scoping**, meaning that a function's scope is determined by its position in the source code, not where it's called. A variable declared inside a function is accessible only within that function, while variables declared outside are globally accessible.

```javascript
function outer() {
  let outerVar = 10;
  function inner() {
    console.log(outerVar); // inner can access outerVar
  }
  inner();
}
outer();
```

---

### **3. What is an IIFE (Immediately Invoked Function Expression)? Give an example.**

An **IIFE** is a function expression that is executed immediately after it is defined. It’s often used to create a local scope, preventing variable leakage to the global scope.

```javascript
(function () {
  console.log("This is an IIFE!");
})();
```

---

### **4. Explain the difference between **call stack** and **message queue** in JavaScript.**

- **Call Stack**: The call stack stores all the execution contexts (functions) that are called. Functions are executed in a last-in, first-out (LIFO) order.

- **Message Queue**: The message queue stores asynchronous tasks (e.g., setTimeout, promises). Once the call stack is empty, the event loop pushes the tasks from the message queue to the call stack.

---

### **5. What is the `typeof` operator in JavaScript? What are its possible return values?**

The `typeof` operator returns a string indicating the type of a variable or expression. Possible return values include:

- `"undefined"`
- `"object"`
- `"boolean"`
- `"number"`
- `"string"`
- `"function"`
- `"symbol"`

---

### **6. How does JavaScript handle concurrency?**

JavaScript handles concurrency through an **event-driven** and **non-blocking** model. It uses the **event loop** to execute tasks asynchronously. Callbacks, promises, and `async/await` help manage asynchronous operations, allowing JavaScript to continue running while waiting for other operations to complete.

---

### **7. What are **callback functions**? Provide an example of their usage.**

A **callback function** is a function passed into another function as an argument to be executed later. They are typically used in asynchronous operations.

```javascript
function fetchData(callback) {
  setTimeout(() => {
    callback("Data fetched");
  }, 1000);
}

fetchData((message) => {
  console.log(message); // "Data fetched"
});
```

---

### **8. How can you create private variables in JavaScript?**

Private variables can be created using **closures**. A closure allows for variables to be kept private within a function and inaccessible from the outside.

```javascript
function counter() {
  let count = 0;
  return {
    increment: function () {
      count++;
    },
    getCount: function () {
      return count;
    },
  };
}

const myCounter = counter();
myCounter.increment();
console.log(myCounter.getCount()); // 1
```

---

### **9. What is the difference between **shallow copy** and **deep copy** in JavaScript?**

- **Shallow copy**: Copies only the top-level properties of an object. Nested objects are shared between the original and the copy.
- **Deep copy**: Recursively copies all properties, including nested objects, creating a completely independent copy.

**Example:**

```javascript
let obj = { a: 1, b: { c: 2 } };
let shallowCopy = { ...obj }; // Shallow copy
let deepCopy = JSON.parse(JSON.stringify(obj)); // Deep copy
```

---

### **10. Explain the concept of **memoization** in JavaScript.**

**Memoization** is an optimization technique that stores the results of expensive function calls and returns the cached result when the same inputs occur again.

```javascript
function memoize(fn) {
  const cache = {};
  return function (arg) {
    if (cache[arg]) {
      return cache[arg];
    }
    const result = fn(arg);
    cache[arg] = result;
    return result;
  };
}

const square = memoize((n) => n * n);
console.log(square(4)); // 16 (calculated)
console.log(square(4)); // 16 (cached)
```

---

### **11. What are **generators** in JavaScript? How are they different from regular functions?**

A **generator** is a function that can be paused and resumed during execution. It uses the `yield` keyword to return a value and pause the function’s execution.

- **Difference**: Unlike regular functions, which return a single value, generators return an iterator that can produce multiple values.

```javascript
function* numbers() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = numbers();
console.log(gen.next()); // { value: 1, done: false }
console.log(gen.next()); // { value: 2, done: false }
```

---

### **12. What is **destructuring** in JavaScript? Provide examples of array and object destructuring.**

**Destructuring** is a syntax that allows you to unpack values from arrays or properties from objects into variables.

- **Array destructuring**:

```javascript
const arr = [1, 2, 3];
const [a, b] = arr;
console.log(a); // 1
console.log(b); // 2
```

- **Object destructuring**:

```javascript
const person = { name: "John", age: 30 };
const { name, age } = person;
console.log(name); // John
console.log(age); // 30
```

---

### **13. Explain the concept of **event bubbling** and **event capturing** in JavaScript.**

- **Event bubbling**: Events propagate from the target element to the root, triggering handlers along the way.
- **Event capturing**: Events propagate from the root to the target element, triggering handlers in reverse order.

You can control this behavior by using the third argument in `addEventListener()`.

```javascript
element.addEventListener(
  "click",
  function () {
    console.log("clicked");
  },
  true
); // Capturing
element.addEventListener(
  "click",
  function () {
    console.log("clicked");
  },
  false
); // Bubbling
```

---

### **14. What is the **setTimeout()** function's return value, and how can you clear a timeout?**

- **Return value**: `setTimeout()` returns a unique identifier that can be used with `clearTimeout()` to cancel the timeout.

```javascript
const timeoutId = setTimeout(() => console.log("Hello"), 1000);
clearTimeout(timeoutId); // Cancels the timeout
```

---

### **15. What is the **Intersection Observer API** used for in JavaScript?**

The **Intersection Observer API** allows you to asynchronously observe changes in the intersection of an element with the viewport (or another element). It’s useful for lazy loading, infinite scrolling, or triggering animations when an element comes into view.

```javascript
const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      console.log("Element is in view");
    }
  });
});

observer.observe(document.querySelector(".element"));
```

---

### **16. What are **Web Workers** and how do they help with concurrency in JavaScript?**

**Web Workers** are JavaScript scripts that run in background threads, allowing heavy computations without blocking the main thread. They enable multi-threading in JavaScript.

```javascript
const worker = new Worker("worker.js");
worker.postMessage("start");
worker.onmessage = (event) => console.log(event.data);
```

---

### **17. What is the **`new`** keyword used for in JavaScript, and how does it work in object creation?**

The `new` keyword creates an instance of an object defined by a constructor function. It sets the `this` value within the constructor and links the newly created object to the constructor's prototype.

```javascript
function Person(name) {
  this.name = name;
}

const john = new Person("John");
console.log(john.name); // John
```

---

### **18. What is the difference between **DOM** and **BOM** in JavaScript?**

- **DOM (Document Object Model)**: A programming interface for web documents. It represents the HTML and XML structure of a webpage as a tree of objects.
- **BOM (Browser Object Model)**: Represents the browser and its components (like `window`, `navigator`, `screen`, etc.) and allows interaction with the browser environment.

---

### **19. How can you implement **debouncing** and **throttling** in JavaScript?**

- **Debouncing**: Ensures that a function is only executed after a specified delay, and not repeatedly in quick succession.

- **Throttling**: Ensures that a function is executed at most once in a specified time interval, no matter how many times it's triggered.

```javascript
// Debouncing
function debounce(func, delay) {
  let timeout;
  return function () {
    clearTimeout(timeout);
    timeout = setTimeout(func, delay);
  };
}

// Throttling
function throttle(func, limit) {
  let lastFunc;
  let lastTime = 0;
  return function () {
    const now = new Date().getTime();
    if (now - lastTime >= limit) {
      func();
      lastTime = now;
    }
  };
}
```

---

### **20. What is **destructuring** assignment, and how does it help in handling function arguments?**

Destructuring allows you to unpack values from objects or arrays into variables, making it easier to handle function arguments, especially when dealing with objects.

```javascript
function greet({ name, age }) {
  console.log(`${name} is ${age} years old`);
}

greet({ name: "John", age: 30 });
```

---
