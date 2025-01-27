
---

### 1. **Prototype Chain**
   - JavaScript uses a **prototype chain** to look up properties and methods.
   - If a property or method is not found on the object itself, JavaScript looks for it on the object’s `__proto__` (its prototype), and continues up the chain until it reaches `null` (the end of the chain).

   **Example:**
   ```javascript
   const obj = {};
   console.log(obj.toString()); // Found in Object.prototype
   ```

   Here, `toString` is not defined on `obj`, so JavaScript checks `Object.prototype`, where `toString` is found.

---

### 2. **Adding Methods to Prototype**
   - Adding methods to a constructor's `prototype` makes them available to all instances without duplicating the method for each instance.

   **Example:**
   ```javascript
   function Animal(name) {
     this.name = name;
   }

   Animal.prototype.speak = function() {
     console.log(`${this.name} makes a noise`);
   };

   const dog = new Animal('Dog');
   dog.speak(); // Dog makes a noise
   ```

---

### 3. **Changing the Prototype of an Object**
   - You can set or change an object’s prototype using `Object.setPrototypeOf` or during object creation using `Object.create`.

   **Example:**
   ```javascript
   const parent = { greet: () => console.log('Hello') };
   const child = Object.create(parent); // Sets parent as the prototype
   child.greet(); // Hello
   ```

   **Note:** Avoid frequently changing the prototype of objects, as it can negatively impact performance.

---

### 4. **Prototype vs Own Properties**
   - **Own properties** are properties directly on an object (not inherited from its prototype).
   - Use `hasOwnProperty` to check if a property is an own property.

   **Example:**
   ```javascript
   const obj = { name: 'John' };
   console.log(obj.hasOwnProperty('name')); // true
   console.log(obj.hasOwnProperty('toString')); // false (inherited)
   ```

---

### 5. **Object.create()**
   - The `Object.create()` method creates a new object and allows you to directly set its prototype.

   **Example:**
   ```javascript
   const proto = { greet: () => console.log('Hi') };
   const obj = Object.create(proto);
   obj.greet(); // Hi
   ```

---

### 6. **Prototype Inheritance Before ES6**
   - Before ES6 introduced `class`, prototype-based inheritance was the standard way to implement inheritance.

   **Example:**
   ```javascript
   function Parent() {
     this.role = 'Parent';
   }

   Parent.prototype.sayRole = function() {
     console.log(this.role);
   };

   function Child() {
     Parent.call(this); // Call parent constructor
     this.role = 'Child';
   }

   Child.prototype = Object.create(Parent.prototype); // Inherit prototype
   Child.prototype.constructor = Child;

   const child = new Child();
   child.sayRole(); // Child
   ```

---

### 7. **Performance Considerations**
   - Accessing properties higher up the prototype chain is slower than accessing properties directly on the object.
   - Modifying the prototype of built-in objects (like `Object.prototype` or `Array.prototype`) is generally discouraged as it can lead to unpredictable behavior.

---

### 8. **Prototype and ES6 Classes**
   - ES6 `class` syntax is syntactic sugar over prototype-based inheritance.
   - Behind the scenes, `class` still uses prototypes to handle inheritance.

   **Example:**
   ```javascript
   class Animal {
     constructor(name) {
       this.name = name;
     }

     speak() {
       console.log(`${this.name} makes a noise`);
     }
   }

   const cat = new Animal('Cat');
   cat.speak(); // Cat makes a noise
   ```

---

### 9. **Prototype vs `Object.getPrototypeOf`**
   - Directly accessing `__proto__` is discouraged as it's not standard in all environments.
   - Instead, use `Object.getPrototypeOf` to safely get an object’s prototype.

   **Example:**
   ```javascript
   const obj = {};
   console.log(Object.getPrototypeOf(obj) === Object.prototype); // true
   ```

---