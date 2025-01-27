
---

In JavaScript, **prototype** is a mechanism by which objects can inherit properties and methods from other objects. Every JavaScript object has an internal property called `[[Prototype]]`, which points to another object. This is often referred to as the object's **prototype**.

The prototype chain allows us to reuse code and achieve inheritance. For instance, if a property or method is not found directly on an object, JavaScript looks for it in the object's prototype, then its prototype's prototype, and so on, until it either finds the property or reaches the end of the prototype chain.

Before ES6 introduced `class` syntax, we used prototypes explicitly to implement inheritance. For example, we could add methods to a constructor function's `prototype` property, and all objects created by that constructor would share those methods.

Here’s an example:

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function() {
  console.log(`Hello, my name is ${this.name}`);
};

const john = new Person('John');
john.sayHello(); // Output: Hello, my name is John
```

In this example, the `sayHello` method is shared among all instances of `Person` via the prototype, instead of being duplicated for each instance. This makes prototypes an efficient way to achieve inheritance in JavaScript.

---

The difference between `__proto__` and `prototype` in JavaScript can be explained as follows:

---

### 1. **`__proto__`:**
   - It is an **internal property** (though accessible publicly in most environments) of an object.
   - It points to the **prototype of the constructor function** that created the object.
   - It is part of the **prototype chain** that JavaScript uses for inheritance.
   - Every object in JavaScript (except `Object.prototype`) has a `__proto__` property.

#### Example:
```javascript
const obj = {};
console.log(obj.__proto__ === Object.prototype); // true
```

Here, `obj.__proto__` points to `Object.prototype` because `obj` was created using the `Object` constructor.

---

### 2. **`prototype`:**
   - It is a property of **constructor functions** (e.g., `Function.prototype`, `Object.prototype`, etc.).
   - It is used to define methods and properties that are shared by all instances created using that constructor.
   - The `prototype` property is what becomes the **`__proto__`** of objects created from that constructor.

#### Example:
```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function() {
  console.log(`Hello, my name is ${this.name}`);
};

const john = new Person('John');
console.log(john.__proto__ === Person.prototype); // true
```

Here, `Person.prototype` contains methods like `sayHello`, and the `__proto__` of the `john` object points to `Person.prototype`.

---

### Key Differences:
| **`__proto__`**                           | **`prototype`**                            |
|------------------------------------------|-------------------------------------------|
| Refers to the prototype of the object.   | Refers to the prototype of a constructor function. |
| Exists on all objects.                   | Exists only on constructor functions (functions used with `new`). |
| Determines the prototype chain for inheritance. | Used to define properties/methods that are shared among instances. |
| Not recommended for direct use (use `Object.getPrototypeOf` instead). | Used for setting up inheritance in constructors. |

---

### Summary:
- **`__proto__`** links an object to its prototype (used internally for inheritance).
- **`prototype`** is a property of a constructor function that defines shared behavior for instances created with that constructor.