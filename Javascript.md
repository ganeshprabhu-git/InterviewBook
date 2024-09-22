
Certainly! I'll start from the beginning and include examples where applicable.

### Set 1: Core Concepts

1. **What is the use of the `this` keyword in JavaScript?**
   - The `this` keyword refers to the object that is executing the current piece of code. Its value is determined by how a function is called.
   - **Example**:
     ```javascript
     function show() {
       console.log(this);
     }
     const obj = { name: 'Alice', show: show };
     obj.show(); // Logs the obj: { name: 'Alice', show: [Function: show] }
     ```

2. **What is the difference between `undefined` and `undeclared` in JavaScript?**
   - **`undefined`**: A variable is declared but has not been assigned a value.
     ```javascript
     let x;
     console.log(x); // undefined
     ```
   - **`undeclared`**: A variable that has not been declared at all.
     ```javascript
     console.log(y); // ReferenceError: y is not defined
     ```

3. **What happens when you try to access a variable before declaring it?**
   - For `var`, the variable declaration is hoisted to the top, but not the initialization. Accessing it before initialization returns `undefined`.
     ```javascript
     console.log(a); // undefined
     var a = 10;
     ```
   - For `let` and `const`, accessing them before declaration results in a `ReferenceError` due to the temporal dead zone.
     ```javascript
     console.log(b); // ReferenceError: Cannot access 'b' before initialization
     let b = 20;
     ```

4. **What is hoisting in JavaScript, and how does it affect variables declared with `var`?**
   - Hoisting is the behavior where variable and function declarations are moved to the top of their scope during compilation. For `var`, declarations are hoisted and initialized to `undefined`, but assignments are not hoisted.
     ```javascript
     console.log(c); // undefined
     var c = 30;
     ```

5. **What is the difference between `var`, `let`, and `const` in terms of hoisting?**
   - **`var`**: Declarations are hoisted and initialized to `undefined`. Can be updated and re-declared within the same scope.
     ```javascript
     console.log(d); // undefined
     var d = 40;
     ```
   - **`let`**: Declarations are hoisted but not initialized. Accessing before initialization results in a `ReferenceError`. Can be updated but not re-declared in the same scope.
     ```javascript
     console.log(e); // ReferenceError: Cannot access 'e' before initialization
     let e = 50;
     ```
   - **`const`**: Declarations are hoisted but not initialized. Must be initialized at declaration and cannot be updated or re-declared.
     ```javascript
     const f = 60;
     f = 70; // TypeError: Assignment to constant variable
     ```

6. **What is the difference between an arrow function and a normal function in JavaScript?**
   - **Arrow Function**: Lexically binds `this`, does not have its own `this`, `arguments`, or `super`, and cannot be used as constructors.
     ```javascript
     const arrowFunc = () => {
       console.log(this); // `this` is lexically bound
     };
     ```
   - **Normal Function**: Has its own `this` context, and can be used as constructors.
     ```javascript
     function normalFunc() {
       console.log(this); // `this` refers to the object that owns the method
     }
     ```

7. **What is a closure in JavaScript?**
   - A closure is a function that retains access to its lexical scope even after the function has finished executing. This allows functions to have private variables.
     ```javascript
     function outer() {
       let count = 0;
       return function inner() {
         count++;
         console.log(count);
       };
     }
     const increment = outer();
     increment(); // 1
     increment(); // 2
     ```

8. **What is an immediately invoked function expression (IIFE)?**
   - An IIFE is a function that is defined and executed immediately. It creates a new scope to avoid polluting the global namespace.
     ```javascript
     (function() {
       let temp = 'I am local';
       console.log(temp);
     })(); // Logs: I am local
     ```

9. **What are the spread and rest operators in JavaScript?**
   - **Spread Operator (`...`)**: Expands an iterable (like an array) into individual elements.
     ```javascript
     const nums = [1, 2, 3];
     const newNums = [...nums, 4, 5]; // [1, 2, 3, 4, 5]
     ```
   - **Rest Operator (`...`)**: Collects multiple elements into a single array.
     ```javascript
     function sum(...numbers) {
       return numbers.reduce((a, b) => a + b, 0);
     }
     console.log(sum(1, 2, 3)); // 6
     ```

10. **What is destructuring in JavaScript?**
    - Destructuring is a syntax that allows unpacking values from arrays or properties from objects into separate variables.
      - **Array Destructuring**:
        ```javascript
        const [a, b] = [1, 2, 3];
        console.log(a); // 1
        console.log(b); // 2
        ```
      - **Object Destructuring**:
        ```javascript
        const { name, age } = { name: 'John', age: 25 };
        console.log(name); // John
        console.log(age); // 25
        ```

### Set 2: Advanced Concepts

11. **What is event bubbling and event capturing in JavaScript?**
    - **Event Bubbling**: When an event occurs on an element, it first triggers on that element and then propagates up to its ancestors in the DOM tree.
      - **Example**:
        ```javascript
        document.getElementById('child').addEventListener('click', () => {
          alert('Child element clicked!');
        });
        document.getElementById('parent').addEventListener('click', () => {
          alert('Parent element clicked!');
        });
        ```
        If you click the child element, both alerts will appear, with the child’s alert appearing first.
    - **Event Capturing**: The event starts from the root and travels down to the target element. This is less common but can be used by setting the `capture` parameter to `true` in `addEventListener`.
      - **Example**:
        ```javascript
        document.getElementById('parent').addEventListener('click', () => {
          alert('Parent element clicked during capture!');
        }, true);
        ```

12. **What is debouncing or throttling in JavaScript?**
    - **Debouncing**: Ensures that a function is executed only after a certain period of inactivity. Useful for events like window resizing or text input.
      - **Example**:
        ```javascript
        function debounce(func, delay) {
          let timer;
          return function(...args) {
            clearTimeout(timer);
            timer = setTimeout(() => func.apply(this, args), delay);
          };
        }
        window.addEventListener('resize', debounce(() => {
          console.log('Window resized!');
        }, 500));
        ```
    - **Throttling**: Limits the number of times a function is executed over a period of time, ensuring it runs at most once per specified interval.
      - **Example**:
        ```javascript
        function throttle(func, limit) {
          let lastFunc;
          let lastRan;
          return function(...args) {
            const context = this;
            if (!lastRan) {
              func.apply(context, args);
              lastRan = Date.now();
            } else {
              clearTimeout(lastFunc);
              lastFunc = setTimeout(() => {
                if ((Date.now() - lastRan) >= limit) {
                  func.apply(context, args);
                  lastRan = Date.now();
                }
              }, limit - (Date.now() - lastRan));
            }
          };
        }
        window.addEventListener('scroll', throttle(() => {
          console.log('Scroll event throttled!');
        }, 1000));
        ```

13. **What is a callback function in JavaScript?**
    - A callback function is a function passed into another function as an argument, which is then executed after some operation or event occurs.
    - **Example**:
      ```javascript
      function fetchData(callback) {
        setTimeout(() => {
          callback('Data loaded');
        }, 1000);
      }
      fetchData((message) => {
        console.log(message); // Data loaded
      });
      ```

14. **What are `async` and `await` in JavaScript, and how do they work?**
    - **`async`**: Declares an asynchronous function that implicitly returns a promise.
      - **Example**:
        ```javascript
        async function fetchData() {
          return 'Data loaded';
        }
        fetchData().then(data => console.log(data)); // Data loaded
        ```
    - **`await`**: Pauses the execution of an `async` function until a promise is resolved or rejected. Can only be used inside `async` functions.
      - **Example**:
        ```javascript
        async function fetchData() {
          let data = await new Promise(resolve => setTimeout(() => resolve('Data loaded'), 1000));
          console.log(data); // Data loaded
        }
        fetchData();
        ```

15. **What is the difference between local storage and session storage?**
    - **Local Storage**: Stores data with no expiration time. Data persists even after the browser is closed and reopened.
      - **Example**:
        ```javascript
        localStorage.setItem('key', 'value');
        console.log(localStorage.getItem('key')); // value
        ```
    - **Session Storage**: Stores data for the duration of the page session. Data is cleared when the page session ends (i.e., when the page is closed).
      - **Example**:
        ```javascript
        sessionStorage.setItem('key', 'value');
        console.log(sessionStorage.getItem('key')); // value
        ```

16. **What values can you access across tabs in local storage and session storage?**
    - **Local Storage**: Data is accessible across all tabs and windows from the same origin.
    - **Session Storage**: Data is only accessible within the same tab or window. Each tab or window has its own session storage.

17. **What are web workers in JavaScript?**
    - Web Workers allow you to run JavaScript code in the background, separate from the main thread. This helps in performing tasks like computations or data processing without blocking the user interface.
    - **Example**:
      ```javascript
      // worker.js
      self.onmessage = function(e) {
        self.postMessage('Hello ' + e.data);
      };
      
      // main.js
      const worker = new Worker('worker.js');
      worker.onmessage = function(e) {
        console.log(e.data); // Hello [data]
      };
      worker.postMessage('World');
      ```

18. **What is variable hoisting in JavaScript?**
    - Variable hoisting is the behavior where variable and function declarations are moved to the top of their containing scope during compilation. This means that variables declared with `var` can be accessed before their declaration, but they will be `undefined` until the declaration is evaluated.

19. **How do you declare a global variable in JavaScript?**
    - A global variable is declared outside of any function or block, or by omitting the `var`, `let`, or `const` keyword inside a function.
      - **Example**:
        ```javascript
        var globalVar = 'I am global';
        function show() {
          globalVar = 'I am still global';
        }
        console.log(globalVar); // I am global
        show();
        console.log(globalVar); // I am still global
        ```

20. **What causes a reference error in JavaScript?**
    - A `ReferenceError` occurs when code attempts to access a variable that has not been declared. This often happens with undeclared variables or accessing variables before they are declared.

21. **How does inheritance work in JavaScript?**
    - Inheritance in JavaScript can be achieved through prototypes. An object can inherit properties and methods from another object using the prototype chain. ES6 introduced `class` syntax which provides a clearer way to set up inheritance.
      - **Example with Prototypes**:
        ```javascript
        function Person(name) {
          this.name = name;
        }
        Person.prototype.sayHello = function() {
          console.log('Hello, ' + this.name);
        };
        
        function Student(name, grade) {
          Person.call(this, name);
          this.grade = grade;
        }
        Student.prototype = Object.create(Person.prototype);
        Student.prototype.constructor = Student;
        
        const student = new Student('Alice', 'A');
        student.sayHello(); // Hello, Alice
        ```

22. **What is the role of prototypes in JavaScript?**
    - Prototypes are used to add properties and methods to objects. Every JavaScript object has a prototype object, and it inherits methods and properties from its prototype. Prototypes form the prototype chain, enabling inheritance and method sharing.

23. **What are the benefits of using arrow functions over regular functions?**
    - Arrow functions have a more concise syntax and do not have their own `this` context, which can be advantageous when dealing with callbacks or methods inside other functions. They also do not have their own `arguments` object.

24. **What is `Promise.all` and how does it behave when one promise fails?**
    - `Promise.all` accepts an iterable of promises and returns a single promise that resolves when all of the promises in the iterable have resolved, or rejects if any promise rejects.
      - **Example**:
        ```javascript
        const p1 = Promise.resolve(1);
        const p2 = Promise.resolve(2);
        const p3 = Promise.reject('Error');
        
        Promise.all([p1, p2, p3])
          .then(results => console.log(results))
          .catch(error => console.error(error)); // Error
        ```

25. **What is the temporal dead zone in JavaScript?**
    - The temporal dead zone is the period from the start of a block until the declaration of a variable with `let` or `const` where the variable is in scope but not yet initialized. Accessing it during this time results in a `ReferenceError`.

26. **How can you dynamically add a property to an object in JavaScript?**
    - You can add a property to an object using dot notation or bracket notation.
      - **Example**:
        ```javascript
        const obj = {};
        obj.newProp = 'value'; // Dot notation
        obj['anotherProp'] = 'another value'; // Bracket notation
        console.log(obj); // { newProp: 'value', anotherProp: 'another value' }
        ```

27. **What is event delegation in JavaScript?**
    - Event delegation is a technique where you attach a single event listener to a parent element instead of multiple listeners on individual child elements. This takes

 advantage of event bubbling and can improve performance and simplify code.
      - **Example**:
        ```javascript
        document.getElementById('parent').addEventListener('click', function(event) {
          if (event.target && event.target.matches('button')) {
            console.log('Button clicked:', event.target.textContent);
          }
        });
        ```

28. **How does JavaScript handle asynchronous operations?**
    - JavaScript handles asynchronous operations using callbacks, promises, and `async`/`await`. These mechanisms allow code to execute without blocking the main thread, enabling concurrent operations like API requests or file reading.

29. **How do you update a variable inside an IIFE from outside the function?**
    - Typically, you cannot directly update variables inside an IIFE from outside. However, you can return an object or a function from the IIFE that provides access to those variables.
      - **Example**:
        ```javascript
        const updater = (function() {
          let value = 0;
          return {
            getValue: function() {
              return value;
            },
            setValue: function(newValue) {
              value = newValue;
            }
          };
        })();
        
        console.log(updater.getValue()); // 0
        updater.setValue(10);
        console.log(updater.getValue()); // 10
        ```

30. **What are the phases of JavaScript execution?**
    - JavaScript execution generally involves the following phases:
      1. **Compilation**: JavaScript code is parsed and compiled into bytecode.
      2. **Execution**: The bytecode is executed by the JavaScript engine, which includes setting up the execution context, hoisting variables, and executing code.

31. **What is the disadvantage of callback functions?**
    - Callback functions can lead to "callback hell" or "pyramid of doom" when multiple nested callbacks are used, making the code hard to read and maintain.

32. **What are the types of promises in JavaScript?**
    - There are three states of a promise:
      1. **Pending**: The initial state; neither fulfilled nor rejected.
      2. **Fulfilled**: The operation completed successfully.
      3. **Rejected**: The operation failed with an error.

33. **What is lexical scope in JavaScript?**
    - Lexical scope refers to the scope created by the placement of code blocks and functions in the source code. Variables are accessible based on their position within nested functions.

34. **What are global variables in JavaScript?**
    - Global variables are declared outside of any function or block and are accessible from anywhere in the code. They are typically declared using `var` without any function or block scope.

35. **What is the event loop in JavaScript?**
    - The event loop is a mechanism that handles asynchronous operations by managing the execution of code, collecting and processing events, and executing queued sub-tasks.

36. **What is the call stack in JavaScript?**
    - The call stack is a data structure that keeps track of function calls and their execution context. It operates on a Last In, First Out (LIFO) principle.

37. **What is the difference between synchronous and asynchronous JavaScript?**
    - **Synchronous JavaScript**: Code is executed line by line, blocking subsequent operations until the current one is complete.
    - **Asynchronous JavaScript**: Code execution can proceed without waiting for other operations to complete, allowing tasks like fetching data or timers to run in the background.

38. **Explain the difference between `undefined` and `null`.**
    - **`undefined`**: Represents a variable that has been declared but not yet assigned a value.
    - **`null`**: Represents the intentional absence of any object value, often used to indicate that a variable should hold an object but is currently empty.

39. **What is the difference between `==` and `===` in JavaScript?**
    - **`==`**: Equality operator that performs type coercion before comparing values, which can lead to unexpected results.
    - **`===`**: Strict equality operator that does not perform type coercion and only returns `true` if both value and type are the same.

40. **How do you handle errors in asynchronous code?**
    - Errors in asynchronous code can be handled using `.catch()` with promises or `try/catch` blocks with `async`/`await`.
      - **Example with Promises**:
        ```javascript
        fetch('invalid-url')
          .then(response => response.json())
          .catch(error => console.error(error));
        ```
      - **Example with `async`/`await`**:
        ```javascript
        async function fetchData() {
          try {
            let response = await fetch('invalid-url');
            let data = await response.json();
          } catch (error) {
            console.error(error);
          }
        }
        ```

41. **How does understanding JavaScript concepts benefit Angular developers?**
    - Understanding JavaScript concepts like scopes, closures, prototypes, and asynchronous programming helps Angular developers build more efficient and effective Angular applications. It aids in writing cleaner code, debugging issues, and leveraging Angular’s features such as data binding and component lifecycle hooks.

42. **What are the core JavaScript features used in Angular development, such as `map`, `reduce`, `filter`, and the spread/rest operators?**
    - **`map`**: Transforms each element of an array based on a function.
    - **`reduce`**: Accumulates array values into a single result.
    - **`filter`**: Creates a new array with elements that pass a test.
    - **Spread Operator**: Expands arrays or objects into individual elements or properties.
    - **Rest Operator**: Collects multiple elements into an array.

43. **Why is it important to understand JavaScript basics even when working primarily with TypeScript and Angular?**
    - Understanding JavaScript basics is crucial because TypeScript is a superset of JavaScript, and Angular builds upon JavaScript concepts. Knowing JavaScript helps in understanding TypeScript’s features and Angular’s underlying mechanisms, improving code quality, debugging, and performance optimization.

Certainly! Here’s a set of important JavaScript concepts that were not covered in the previous lists:

### Set 3: Essential JavaScript Concepts

44. **What is the `bind` method in JavaScript, and how is it used?**
    - The `bind` method creates a new function that, when called, has its `this` keyword set to a specified value and pre-set arguments.
    - **Example**:
      ```javascript
      function greet(greeting, punctuation) {
        console.log(greeting + ', ' + this.name + punctuation);
      }
      const person = { name: 'Alice' };
      const greetPerson = greet.bind(person, 'Hello');
      greetPerson('!'); // Hello, Alice!
      ```

45. **What are higher-order functions in JavaScript?**
    - Higher-order functions are functions that take other functions as arguments or return functions as results. They are commonly used in functional programming to create more abstract and reusable code.
    - **Example**:
      ```javascript
      function createMultiplier(multiplier) {
        return function(value) {
          return value * multiplier;
        };
      }
      const double = createMultiplier(2);
      console.log(double(5)); // 10
      ```

46. **What is event delegation and why is it useful?**
    - Event delegation is a technique where you attach a single event listener to a parent element rather than multiple listeners to individual child elements. It leverages event bubbling to manage events more efficiently and reduce memory usage.
    - **Example**:
      ```javascript
      document.getElementById('parent').addEventListener('click', function(event) {
        if (event.target && event.target.matches('button')) {
          console.log('Button clicked:', event.target.textContent);
        }
      });
      ```

47. **What is a JavaScript module, and how do you use it?**
    - A JavaScript module is a file that exports and imports code, allowing for better organization and encapsulation of code. Modules can export functions, objects, or primitives and import them into other files.
    - **Example**:
      ```javascript
      // module.js
      export function greet(name) {
        return `Hello, ${name}`;
      }

      // main.js
      import { greet } from './module.js';
      console.log(greet('Alice')); // Hello, Alice
      ```

48. **What is the difference between shallow copy and deep copy?**
    - **Shallow Copy**: Creates a new object but does not recursively copy nested objects. Modifications to nested objects will affect both the original and copied objects.
      - **Example**:
        ```javascript
        const original = { a: 1, b: { c: 2 } };
        const shallowCopy = { ...original };
        shallowCopy.b.c = 3;
        console.log(original.b.c); // 3
        ```
    - **Deep Copy**: Creates a new object and recursively copies all nested objects, resulting in a completely independent copy.
      - **Example**:
        ```javascript
        const original = { a: 1, b: { c: 2 } };
        const deepCopy = JSON.parse(JSON.stringify(original));
        deepCopy.b.c = 3;
        console.log(original.b.c); // 2
        ```

49. **What is the `Object.create()` method and how does it work?**
    - The `Object.create()` method creates a new object with the specified prototype object and properties. It is used to create a new object with a specified prototype and optionally add properties.
    - **Example**:
      ```javascript
      const person = {
        greet() {
          console.log('Hello!');
        }
      };
      const employee = Object.create(person);
      employee.job = 'Developer';
      employee.greet(); // Hello!
      ```

50. **What are JavaScript decorators and how are they used?**
    - Decorators are a proposal for JavaScript that allows special syntax to modify classes and their methods. They provide a way to add metadata or modify class behavior in a declarative manner.
    - **Example**:
      ```javascript
      // Example using a decorator (note: decorators are still a stage 2 proposal)
      function readonly(target, key, descriptor) {
        descriptor.writable = false;
        return descriptor;
      }

      class MyClass {
        @readonly
        name = 'Immutable';
      }
      ```

51. **What is the `Proxy` object and how is it used?**
    - The `Proxy` object allows you to create a handler for operations on another object. It can intercept and redefine fundamental operations (e.g., property lookup, assignment).
    - **Example**:
      ```javascript
      const handler = {
        get(target, property) {
          return property in target ? target[property] : 'Not found';
        }
      };
      const target = { a: 1, b: 2 };
      const proxy = new Proxy(target, handler);
      console.log(proxy.a); // 1
      console.log(proxy.c); // Not found
      ```

52. **What is the `Reflect` API in JavaScript and how is it used?**
    - The `Reflect` API provides methods to interact with and manipulate objects in a way similar to the `Proxy` object. It is used to perform operations like property access, assignment, and method invocation in a more controlled manner.
    - **Example**:
      ```javascript
      const target = { a: 1 };
      Reflect.set(target, 'b', 2);
      console.log(target.b); // 2
      ```

53. **What are the `WeakMap` and `WeakSet` objects and how are they different from `Map` and `Set`?**
    - **`WeakMap`**: A collection of key-value pairs where the keys are objects and the values can be any value. Weak references are used for keys, so they do not prevent garbage collection of the keys.
      - **Example**:
        ```javascript
        const weakMap = new WeakMap();
        const obj = {};
        weakMap.set(obj, 'value');
        console.log(weakMap.get(obj)); // value
        ```
    - **`WeakSet`**: A collection of objects where the objects are held weakly, meaning they do not prevent garbage collection of the objects.
      - **Example**:
        ```javascript
        const weakSet = new WeakSet();
        const obj = {};
        weakSet.add(obj);
        console.log(weakSet.has(obj)); // true
        ```

54. **What are `Symbol` objects in JavaScript and how are they used?**
    - `Symbol` objects are primitive data types that are unique and immutable. They are used to create unique property keys that do not clash with other property keys.
    - **Example**:
      ```javascript
      const uniqueKey = Symbol('description');
      const obj = {};
      obj[uniqueKey] = 'value';
      console.log(obj[uniqueKey]); // value
      ```

55. **What is the `Object.freeze()` method and how does it work?**
    - The `Object.freeze()` method prevents modification of an object’s properties and values. It makes an object immutable by preventing new properties from being added, existing properties from being removed, and existing properties from being altered.
    - **Example**:
      ```javascript
      const obj = { a: 1 };
      Object.freeze(obj);
      obj.a = 2; // No effect
      console.log(obj.a); // 1
      ```

56. **What are `async iterators` and how are they used?**
    - `Async iterators` are objects that conform to the async iterable protocol, allowing asynchronous iteration over data sources. They use the `for-await-of` loop for asynchronous iteration.
    - **Example**:
      ```javascript
      async function* asyncGenerator() {
        yield 'Hello';
        yield 'World';
      }
      
      (async () => {
        for await (const value of asyncGenerator()) {
          console.log(value); // Hello, World
        }
      })();
      ```

57. **What is the `new` keyword in JavaScript and how does it work?**
    - The `new` keyword creates a new instance of a user-defined object type or built-in object type, initializing it with the specified constructor function.
    - **Example**:
      ```javascript
      function Person(name) {
        this.name = name;
      }
      const person = new Person('Alice');
      console.log(person.name); // Alice
      ```

58. **What is the `this` context in arrow functions?**
    - In arrow functions, `this` is lexically bound to the context in which the arrow function was defined. This means it inherits `this` from its surrounding code, rather than having its own `this` binding.
    - **Example**:
      ```javascript
      function Counter() {
        this.count = 0;
        setInterval(() => {
          this.count++;
          console.log(this.count);
        }, 1000);
      }
      const counter = new Counter(); // Correctly logs incremented count
      ```

59. **What is the `Function.prototype.apply()` method and how is it used?**
    - The `apply()` method calls a function with a given `this` value and arguments provided as an array (or array-like object).
    - **Example**:
      ```javascript
      function sum(a, b) {
        return a + b;
      }
      console.log(sum.apply(null, [1, 2])); // 3
      ```

60. **What is the `Function.prototype.call()` method and how is it used?**


    - The `call()` method calls a function with a given `this` value and individual arguments provided directly.
    - **Example**:
      ```javascript
      function greet(greeting, name) {
        return `${greeting}, ${name}`;
      }
      console.log(greet.call(null, 'Hello', 'Alice')); // Hello, Alice
      ```

