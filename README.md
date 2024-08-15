# JavaScript Core Concepts

## Introduction

This document provides a comprehensive overview of core JavaScript concepts. Whether you're new to the language or looking to solidify your understanding, this guide covers essential topics with clear explanations and practical examples.

## Table of Contents

- [Syntax Parser](#syntax-parser)
- [Lexical Environment](#lexical-environment)
- [Execution Context](#execution-context)
- [Name/Value Pairs](#namevalue-pairs)
- [Objects](#objects)
- [Global Scope](#global-scope)
- [Execution Context Creation](#execution-context-creation-creation-phase)
- [JavaScript and undefined](#javascript-and-undefined)
- [Execution Context (Code Execution)](#execution-context-code-execution)
- [Single-Threaded, Synchronous Execution](#single-threaded-synchronous-execution)
- [Function Invocation and the Execution Stack](#function-invocation-and-the-execution-stack)
- [Variable Environment](#variable-environment)
- [The Scope Chain](#the-scope-chain)
- [Scope](#scope)
- [let and const in ES6](#let-and-const-in-es6)
- [Asynchronous Callbacks](#asynchronous-callbacks)
- [Dynamic Typing](#dynamic-typing)
- [Primitive Types](#primitive-types)
- [Operators](#operators)
- [Operator Precedence](#operator-precedence)
- [Operator Associativity](#operator-associativity)
- [Coercion](#coercion)
- [Default Values](#default-values)
- [Objects and Functions](#objects-and-functions)
- [First-Class Functions](#first-class-functions)
- [Function Statements and Function Expressions](#function-statements-and-function-expressions)
- [By Value vs. By Reference & Mutation](#by-value-vs-by-reference--mutation)
- [Objects, Functions, and 'this'](#objects-functions-and-this)
- [Arrays: Collections of Anything](#arrays-collections-of-anything)
- [Arguments and Spread](#arguments-and-spread)
- [Automatic Semicolon Insertion](#automatic-semicolon-insertion-asi)
- [Whitespace](#whitespace)
- [IIFE: Immediately Invoked Function Expression](#iife-immediately-invoked-function-expression)
- [Closures](#closures)
- [Function Factories and Closures](#function-factory-making-advantage-of-closures)
- [Callback Functions](#callback-functions)
- [Promises](#promises)
- [Event Loop](#the-event-loop)
- [call(), apply(), and bind()](#call-apply-and-bind)
- [Function Currying](#function-currying)
- [Functional Programming](#functional-programming)
- [Object-Oriented JavaScript and Prototypal Inheritance](#object-oriented-javascript-and-prototypal-inheritance)
- [Inheritance](#inheritance)
- [Prototype](#prototype)
- [Everything is an Object (or a Primitive)](#everything-is-an-object-or-a-primitive)
- [Reflection](#reflection)
- [Function Constructors, 'new', and JavaScript History](#function-constructors-new-and-javascript-history)
- [Setting the Prototype in Function Constructors](#setting-the-prototype-in-function-constructors)
- [Strict Mode](#strict-mode)
- [NaN (Not a Number)](#nan-not-a-number)
- [CORS (Cross-Origin Resource Sharing)](#cors-cross-origin-resource-sharing)
- [JSONP (JSON with Padding)](#jsonp-json-with-padding)
- [DOM (Document Object Model)](#dom-document-object-model)
- [Methods to Select DOM Elements](#methods-to-select-dom-elements)
- [Methods to Manipulate the DOM](#methods-to-manipulate-the-dom)
- [DOM Events](#dom-events)
- [Event Bubbling & Event Capturing](#event-bubbling--event-capturing)
- [stopPropagation() & preventDefault()](#stoppropagation--preventdefault)

## Syntax Parser

A syntax parser is a program that reads your JavaScript code and:

1. **Determines its meaning:** It figures out what your code is instructing the computer to do.
2. **Checks for valid grammar:** It ensures you've written code according to the rules of JavaScript syntax.

Your code isn't directly understood by the computer. The JavaScript engine (like the one in your web browser) acts as an intermediary. It uses the syntax parser to translate your code into instructions the computer can execute.

## Lexical Environment

The lexical environment refers to where code is physically located within your JavaScript file.  It determines variable and function visibility based on their position in the code structure.

## Execution Context

An execution context is a wrapper created by the JavaScript engine each time a piece of code is executed. It manages the execution of that code. 

**Key components:**

- **Global Object:** In web browsers, this is the `window` object, providing access to global variables and functions.
- **`this` keyword:**  Refers to the current execution context, which can change based on how a function is called.

**Relationship in the Global Execution Context:**

- In the global execution context, the `Global Object`, `window`, and `this` all refer to the same object.

## Name/Value Pairs

In JavaScript, data is often organized as name/value pairs:

- **Name:** A unique identifier for a value.
- **Value:** The data associated with the name.

Example:

```javascript
let age = 30; // "age" is the name, "30" is the value
```

## Objects

Objects are collections of name/value pairs. They provide a way to structure data and represent real-world entities.

Example:

```javascript
const user = {
  firstName: "Alice", 
  lastName: "Johnson", 
  age: 25 
};
```

## Global Scope

Code that resides outside of any function is said to be in the "global scope." Variables and functions declared in the global scope are accessible from anywhere within your JavaScript program.

## Execution Context Creation (Creation Phase)

Before JavaScript executes your code, it goes through a creation phase for each execution context. Here's what happens:

1. **Creation of Global Object, `this`, and Outer Environment:** The JavaScript engine sets up these core components.
2. **Hoisting:**
   - **Variables:** Variables declared with `var` are "hoisted" to the top of their scope and initialized with a value of `undefined`.
   - **Variables declared with `let` and `const`:** Are also hoisted to the top of their scope, BUT they are not initialized with any value. They are in a "Temporal Dead Zone" (TDZ) from the beginning of their scope until the line where they are declared is executed. Trying to access a `let` or `const` variable in its TDZ will result in a `ReferenceError`.
   - **Functions:** Function declarations (not function expressions) are also hoisted, making them callable before their actual definition in the code.

## JavaScript and undefined

The special value `undefined` in JavaScript signifies that a variable has been declared but has not yet been assigned a value. It's essential to understand this concept to avoid unexpected behavior.

**Example:**

```javascript
let myVariable;
console.log(myVariable); // Output: undefined
```

Attempting to access a variable that has not been declared results in a `ReferenceError`.

## Execution Context (Code Execution)

Once the creation phase is complete, the JavaScript engine executes your code line by line, interpreting each statement and running the corresponding instructions.

## Single-Threaded, Synchronous Execution

- **Single-Threaded:** JavaScript executes one command at a time. It has a single call stack to manage function execution.
- **Synchronous:**  Code is executed in the order it appears in the file. Each line of code must finish executing before the next line begins.

## Function Invocation and the Execution Stack

- **Invocation:** Running a function by using parentheses `()`.
- **Execution Stack (Call Stack):** A LIFO (Last In, First Out) structure that keeps track of function calls.

1. When a function is invoked, a new execution context for that function is created and pushed onto the execution stack.
2. The engine executes the code within the function.
3. If another function is called inside the current function, a new execution context is created and pushed onto the stack.
4.  When a function finishes executing, its execution context is popped off the stack, and control returns to the context below it.

## Variable Environment

The variable environment is a part of the execution context. It stores the variables and their values that are accessible within that specific context.

## The Scope Chain

Each execution context has a reference to its outer environment, forming a chain-like structure called the scope chain.  

- **Variable Lookup:** When JavaScript encounters a variable, it first searches the current execution context's variable environment. 
- **Outer Environments:** If the variable is not found, the search continues up the scope chain to outer environments.
- **Lexical Scoping:** The structure of the scope chain is determined by where functions are defined in the code (their lexical environment).

## Scope

Scope determines the accessibility of variables and functions.  JavaScript primarily has two types of scope:

- **Global Scope:** Variables and functions declared outside of any function have global scope and are accessible from anywhere in the code.
- **Function Scope:** Variables declared inside a function have function scope and are only accessible within that function.

## `let` and `const` in ES6

ES6 (ECMAScript 2015) introduced `let` and `const` for variable declarations, improving upon the older `var` keyword:

- **Block Scoping:** `let` and `const` have block scope, meaning they are limited to the block of code (defined by curly braces `{}`) in which they are declared.
- **`let`:** Allows re-assignment of values.
- **`const`:** Declares constants whose values cannot be re-assigned after initialization.

## Asynchronous Callbacks

- **Asynchronous:** Operations that don't block the execution of other code.  Results are handled later.
- **Callbacks:** Functions passed as arguments to other functions, intended to be executed when the asynchronous operation completes.

**Example:**

```javascript
setTimeout(function() {
  console.log("This runs after 2 seconds"); 
}, 2000); 

console.log("This runs immediately");
```

## Dynamic Typing

JavaScript is dynamically typed, meaning you don't have to explicitly declare the data type of a variable. The JavaScript engine determines the type at runtime.

**Advantages:**
- Flexibility.
- Faster development.

**Disadvantages:**
- Potential for runtime type errors.
- Can make code harder to reason about in large projects.

## Primitive Types

Primitive types represent single values in JavaScript. There are seven primitive types:

1. **`undefined`:** Represents the absence of a value (assigned automatically by JavaScript when a variable is declared but not initialized).
2. **`null`:** Represents intentional absence of any object value (you set this explicitly).
3. **`boolean`:** Represents `true` or `false` values.
4. **`number`:** Represents all numbers in JavaScript (including whole numbers, decimals, and exponents).
5. **`string`:** Represents text, enclosed in single (`'`) or double (`"`) quotes.
6. **`symbol`:**  (Introduced in ES6) Unique and immutable values, useful for creating object properties that are guaranteed to be unique.
7. **`bigint`:** (Introduced in ES2020) Represents integers of arbitrary size.

## Operators

Operators are special symbols or keywords that perform specific operations on values (operands).

**Common Operators:**

- **Arithmetic:**  `+`, `-`, `*`, `/`, `%` (modulo)
- **Comparison:** `==` (loose equality), `===` (strict equality), `!=` (not equal), `!==` (strict not equal), `>`, `<`, `>=`, `<=` 
- **Logical:** `&&` (AND), `||` (OR), `!` (NOT)
- **Assignment:** `=`, `+=`, `-=`, `*=`, `/=`, etc.

## Operator Precedence

Operator precedence determines the order in which operators are evaluated in an expression. Operators with higher precedence are executed before operators with lower precedence.

**Example:**

```javascript
let result = 5 + 3 * 2; // Multiplication has higher precedence than addition
console.log(result); // Output: 11 
```

## Operator Associativity

Associativity determines how operators of the same precedence are grouped together.

- **Left-to-right (left-associative):** Most operators in JavaScript are left-associative, meaning they are grouped from left to right.
- **Right-to-left (right-associative):** Some operators, such as the assignment operator (`=`), are right-associative.

## Coercion

Coercion is the automatic or implicit conversion of a value from one type to another. JavaScript frequently uses coercion in comparisons and operations involving different data types.

**Example:**

```javascript
let result = 1 + "2"; // Number 1 is coerced to a string
console.log(result);  // Output: "12" 
```

**Strict vs. Loose Equality:**

- **`===` (Strict Equality):** Checks for both value and type equality without coercion.
- **`==` (Loose Equality):** Performs type coercion if necessary before comparing values.

## Default Values

- The logical OR operator (`||`) is useful for providing default values:

```javascript
function greet(name) {
    name = name || 'Guest'; // If 'name' is undefined or falsy, use 'Guest'
    console.log('Hello ' + name);
}
```

## Objects and Functions

- **Objects as Data Structures:** Objects are collections of key-value pairs. Keys are strings (or Symbols), and values can be any data type.
- **Functions as First-Class Citizens:** In JavaScript, functions are treated as first-class citizens. This means:
    - Functions can be assigned to variables.
    - Functions can be passed as arguments to other functions.
    - Functions can be returned from other functions.

## First-Class Functions

First-class functions are a fundamental concept in JavaScript, enabling powerful programming paradigms:

- **Functions as Variables:**
  ```javascript
  const greet = function(name) {
    console.log("Hello, " + name + "!");
  };

  greet("Alice"); // Output: Hello, Alice!
  ```

- **Functions as Arguments (Callbacks):**
  ```javascript
  function fetchData(url, callback) {
    // Simulate fetching data (asynchronous operation)
    setTimeout(() => {
      const data = { name: "Bob", age: 30 };
      callback(data);
    }, 1000);
  }

  fetchData("https://example.com/api/user", (userData) => {
    console.log("User data:", userData);
  });
  ```

## Function Statements and Function Expressions

- **Function Statement (Declaration):**
  ```javascript
  function add(a, b) {
    return a + b;
  }
  ```
  - Hoisted to the top of their scope.
  - Can be called before their declaration in the code.

- **Function Expression:**
  ```javascript
  const subtract = function(a, b) {
    return a - b;
  };
  ```
  - Not hoisted (behave like regular variables).
  - Must be defined before they are called.

## By Value vs. By Reference & Mutation

- **By Value (Primitives):** When you assign a primitive value to a variable, you are creating a copy of that value in memory. Changes to one variable do not affect the other.

  ```javascript
  let x = 5;
  let y = x; 
  y = 10;
  console.log(x); // Output: 5
  console.log(y); // Output: 10 
  ```

- **By Reference (Objects):** When you assign an object to a variable, you are creating a reference that points to the same object in memory. Changes to one variable will affect the other.

  ```javascript
  const obj1 = { name: "Eve" };
  const obj2 = obj1;
  obj2.name = "Frank";
  console.log(obj1.name); // Output: Frank
  console.log(obj2.name); // Output: Frank 
  ```

- **Mutation:**  Modifying the properties or contents of an object is called mutation.  When you pass objects to functions, be mindful of potential mutations.

## Objects, Functions, and 'this'

The `this` keyword in JavaScript is a special identifier that refers to the context in which a function is executed. Its value can vary depending on how a function is called.

- **`this` in Methods:** When a function is called as a method of an object, `this` refers to the object that owns the method.

  ```javascript
  const myObject = {
    name: "My Object",
    greet: function() {
      console.log("Hello from " + this.name);
    }
  };

  myObject.greet(); // Output: Hello from My Object
  ```

- **`this` in Constructors:** When a function is used as a constructor with the `new` keyword, `this` refers to the newly created object.

  ```javascript
  function Car(brand) {
    this.brand = brand;
  }

  const myCar = new Car("Ford");
  console.log(myCar.brand); // Output: Ford
  ```

- **`this` in Global Context:** In the global execution context (outside of any function), `this` refers to the global object (usually `window` in web browsers).

## Arrays: Collections of Anything

Arrays in JavaScript are ordered collections that can hold elements of any data type.

- **Creating Arrays:**
  ```javascript
  const numbers = [1, 2, 3, 4, 5];
  const mixedArray = [10, "hello", true, { name: "Grace" }];
  ```

- **Accessing Elements:**  Array elements are accessed using zero-based indexing.
  ```javascript
  console.log(numbers[0]); // Output: 1
  ```

- **Array Methods:** JavaScript provides a rich set of built-in methods for working with arrays (e.g., `push()`, `pop()`, `slice()`, `map()`, `filter()`, `reduce()`).

## Arguments and Spread

- **`arguments` Object:** Inside a function, the `arguments` object is an array-like object that contains all the arguments passed to the function.

  ```javascript
  function sum() {
    let total = 0;
    for (let i = 0; i < arguments.length; i++) {
      total += arguments[i];
    }
    return total;
  }

  console.log(sum(1, 2, 3, 4)); // Output: 10
  ```

- **Spread Syntax (`...`):** ES6 introduced the spread syntax, which allows you to expand an iterable (like an array) into its individual elements.

  ```javascript
  const numbers1 = [1, 2, 3];
  const numbers2 = [4, 5, 6];

  const combined = [...numbers1, ...numbers2]; 
  console.log(combined); // Output: [1, 2, 3, 4, 5, 6]
  ```

## Automatic Semicolon Insertion (ASI)

JavaScript has a feature called Automatic Semicolon Insertion, which attempts to insert semicolons automatically where it thinks they are missing. While this can be convenient, it can sometimes lead to unexpected behavior. 

**Best Practice:** It's considered best practice to always include semicolons at the end of your JavaScript statements to avoid potential ASI issues.

## Whitespace

Whitespace refers to spaces, tabs, and newline characters in your code. While JavaScript largely ignores whitespace, consistent indentation and spacing improve code readability and maintainability.

## IIFE: Immediately Invoked Function Expression

An IIFE is a function expression that is executed as soon as it is defined. It's commonly used to create a private scope for variables and avoid polluting the global scope.

```javascript
(function() {
  // Code inside the IIFE
  let privateVariable = "This is private!";
})();

// console.log(privateVariable); // Error: privateVariable is not defined
```

## Closures

A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment).  Closures give functions the ability to "remember" and access variables from their lexical scope, even after the outer function has finished executing.

**Example:**

```javascript
function makeCounter() {
  let count = 0; 
  return function() {
    return count++;
  };
}

const counter1 = makeCounter();
const counter2 = makeCounter();

console.log(counter1()); // Output: 0
console.log(counter1()); // Output: 1
console.log(counter2()); // Output: 0 (counter2 has its own independent count)
```

## Function Factory: Making Advantage of Closures

A function factory leverages closures to create new functions with customized behavior. Each function generated by the factory has its own isolated scope, preserving the values passed during creation.

**Example:**

```javascript
function createMultiplier(factor) {
  return function(number) {
    return number * factor;
  };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5));  // Output: 10
console.log(triple(5));  // Output: 15
```

## Callback Functions

A callback function is a function that is passed as an argument to another function, with the intention of being called back later. Callbacks are frequently used in asynchronous operations (like timers, event handling, and AJAX requests) to provide a way to handle the result of an operation once it completes.

**Example:**

```javascript
function greetAfterDelay(name, delay, callback) {
  setTimeout(() => {
    const message = `Hello, ${name}!`;
    callback(message);
  }, delay);
}

greetAfterDelay("Henry", 1500, (greeting) => {
  console.log(greeting); // Output (after 1.5 seconds): Hello, Henry!
});
```

## Promises

A Promise is an object that represents the eventual outcome of an asynchronous operation. It can be in one of three states:

1. **Pending:** The initial state, neither fulfilled nor rejected.
2. **Fulfilled:** The asynchronous operation completed successfully.
3. **Rejected:** The asynchronous operation failed.

Promises provide a cleaner and more manageable way to handle asynchronous operations compared to traditional callback functions.

**Example:**

```javascript
function fetchData(url) {
  return new Promise((resolve, reject) => {
    fetch(url)
      .then(response => {
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        return response.json(); 
      })
      .then(data => {
        resolve(data); // Fulfill the promise with the fetched data
      })
      .catch(error => {
        reject(error); // Reject the promise if there's an error
      });
  });
}

fetchData('https://api.example.com/data')
  .then(data => {
    console.log('Data:', data);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

### Async/Await
ES2017 introduced async/await, which is syntactic sugar built on top of Promises, making asynchronous code even easier to write and read.
The async and await keywords enable asynchronous, promise-based behavior to be written in a cleaner style, avoiding the need to explicitly configure promise chains.

1. async Functions
An async function is a function that implicitly returns a Promise. You can use the async keyword before a function declaration to define an async function.

```javascript
async function fetchData() {
  return "Data fetched";
}

fetchData().then(data => console.log(data)); // Output: Data fetched
```

2. await Keyword
The await keyword can only be used inside an async function. It pauses the execution of the async function until the Promise is resolved.

```javascript
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function example() {
  console.log("Start");
  await delay(2000); // Waits for 2 seconds
  console.log("After 2 seconds");
}

example();
// Output:
// Start
// (2 seconds later)
// After 2 seconds
```

## The Event Loop
The event loop is a fundamental concept in JavaScript that enables non-blocking, asynchronous execution. It's the mechanism that allows JavaScript, which is single-threaded, to perform non-blocking operations.

How the Event Loop Works

1. Call Stack: 
   - The call stack is where JavaScript keeps track of function calls.
   - When a function is called, it's added to the stack.
   - When a function returns, it's removed from the stack.

2. Callback Queue (Task Queue):
   - Asynchronous operations (like setTimeout, Promise resolutions, or DOM events) add their callback functions to the callback queue when they're ready to be executed.

3. Microtask Queue:
   - Similar to the callback queue, but for microtasks like Promise callbacks.
   - Microtasks have higher priority than regular tasks.

4. Event Loop:
   - Continuously checks if the call stack is empty.
   - If empty, it first processes all microtasks.
   - Then, it takes the first task from the callback queue and pushes it to the call stack for execution.

1. Basic Event Loop Demonstration

```javascript
console.log('Start');

setTimeout(() => {
  console.log('Timeout 1');
}, 0);

Promise.resolve().then(() => {
  console.log('Promise 1');
});

console.log('End');

// Output:
// Start
// End
// Promise 1
// Timeout 1
```

- 'Start' and 'End' are logged immediately.
- The setTimeout callback is added to the callback queue.
- The Promise resolution is added to the microtask queue.
- After the call stack is empty, the microtask (Promise) is executed.
- Finally, the setTimeout callback is executed.

2. Microtasks vs Macrotasks

```javascript
console.log('Script start');

setTimeout(() => {
  console.log('setTimeout');
}, 0);

Promise.resolve().then(() => {
  console.log('Promise 1');
}).then(() => {
  console.log('Promise 2');
});

console.log('Script end');

// Output:
// Script start
// Script end
// Promise 1
// Promise 2
// setTimeout
```

- Synchronous code runs first ('Script start' and 'Script end').
- The Promise callbacks (microtasks) are executed before the setTimeout callback (macrotask).

3. Demonstrating the Non-Blocking Nature

```javascript
console.log('Starting long operation');

setTimeout(() => {
  let sum = 0;
  for(let i = 0; i < 1000000000; i++) {
    sum += i;
  }
  console.log('Long operation finished');
}, 0);

console.log('Continuing with other tasks');

// Output:
// Starting long operation
// Continuing with other tasks
// (after a delay) Long operation finished
```

- The long operation is scheduled to run asynchronously.
- The script continues executing without waiting for the long operation to complete.

4. Mixing Async Operations

```javascript
console.log('Start');

setTimeout(() => {
  console.log('Timeout 1');
  Promise.resolve().then(() => {
    console.log('Promise inside Timeout');
  });
}, 0);

Promise.resolve().then(() => {
  console.log('Promise 1');
  setTimeout(() => {
    console.log('Timeout inside Promise');
  }, 0);
});

console.log('End');

// Output:
// Start
// End
// Promise 1
// Timeout 1
// Promise inside Timeout
// Timeout inside Promise
```

- Microtasks queued during the execution of a task are processed before the next task is taken from the macrotask queue.

## `call()`, `apply()`, and `bind()`

These methods provide control over the `this` keyword in JavaScript functions.

- **`call()`:** Invokes a function immediately, explicitly setting the value of `this`.

  ```javascript
  function greet(greeting) {
    console.log(greeting + ", " + this.name + "!");
  }

  const person = { name: "Isabella" };

  greet.call(person, "Hello");  // Output: Hello, Isabella!
  ```

- **`apply()`:** Similar to `call()`, but it accepts the arguments to be passed to the function as an array.

  ```javascript
  function sum(a, b) {
    return a + b;
  }

  const numbers = [5, 10];

  console.log(sum.apply(null, numbers)); // Output: 15
  ```

- **`bind()`:** Creates a new function that, when called, has its `this` keyword set to the provided value.

  ```javascript
  const logName = function() {
    console.log(this.name);
  };

  const obj = { name: "My Object" };

  const boundLogName = logName.bind(obj);
  boundLogName(); // Output: My Object 
  ```

## Function Currying

Function currying is a technique where a function that takes multiple arguments is transformed into a sequence of nested functions that each take a single argument. Curried functions improve code clarity, reusability, and partial application.

**Example:**

```javascript
function curry(fn) {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    } else {
      return (...nextArgs) => curried.apply(this, [...args, ...nextArgs]);
    }
  };
}

function add3(x, y, z) {
  return x + y + z;
}

const curriedAdd3 = curry(add3);
console.log(curriedAdd3(1)(2)(3)); // Output: 6
console.log(curriedAdd3(1, 2)(3));  // Output: 6
console.log(curriedAdd3(1, 2, 3));   // Output: 6
```

## Functional Programming

Functional programming is a paradigm that emphasizes:

- **Pure Functions:**  Functions that always produce the same output for the same input and have no side effects.
- **Immutability:** Avoiding changing data in place; instead, creating new data structures with the desired modifications.
- **Higher-Order Functions:** Functions that can take other functions as arguments or return functions.

JavaScript supports functional programming concepts, which can lead to more predictable and maintainable code.

## Object-Oriented JavaScript and Prototypal Inheritance

Object-oriented programming (OOP) is a programming paradigm that organizes code around objects, which are instances of classes. JavaScript uses a prototype-based inheritance model, which is different from class-based inheritance found in languages like Java or C++.

## Inheritance

Inheritance allows objects to inherit properties and methods from other objects, promoting code reuse and a hierarchical structure.  In JavaScript, inheritance is achieved through prototypes.

## Prototype

Every object in JavaScript has a prototype, which is another object it can inherit properties and methods from.

- **`__proto__`:** The `__proto__` property (deprecated but still widely supported) provides a reference to an object's prototype.
- **Prototype Chain:** When you try to access a property or method on an object, JavaScript first checks if the object itself has it. If not, it looks up the prototype chain to the object's prototype, and so on, until it either finds the property/method or reaches the end of the chain.

## Everything is an Object (or a Primitive)

In JavaScript, almost everything is an object, except for the primitive data types. Even functions are objects.  This object-oriented nature of JavaScript allows for great flexibility.

## Reflection

Reflection in JavaScript allows you to inspect and modify objects at runtime.

- **`for...in` loop:** Iterates over the enumerable properties of an object.

  ```javascript
  const myObj = { a: 1, b: 2, c: 3 };

  for (const property in myObj) {
    console.log(`${property}: ${myObj[property]}`);
  }
  ```

- **`hasOwnProperty()`:** Checks if an object has a specific property as its own property (not inherited from its prototype).

  ```javascript
  console.log(myObj.hasOwnProperty('a')); // Output: true
  ```

## Function Constructors, 'new', and JavaScript History

Before ES6 classes were introduced, function constructors were a common way to create objects that shared similar properties and methods.  The `new` keyword is used with a function constructor to create new objects.

**Example:**

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.sayHello = function() {
  console.log(`Hello, my name is ${this.name}.`);
};

const person1 = new Person("Jack", 30);
person1.sayHello(); // Output: Hello, my name is Jack.
```

## Setting the Prototype in Function Constructors

When you create objects using a function constructor and the `new` keyword, you can add properties and methods to the constructor's `prototype` property.  These will be inherited by all objects created from that constructor.

## Strict Mode

Strict mode introduces stricter parsing and error handling rules in JavaScript. It helps to catch common coding mistakes and "silent errors" that would otherwise fail silently.

- **Enable Strict Mode:** You can enable strict mode globally by adding `"use strict";` at the top of your script or locally within a function.

  ```javascript
  "use strict";

  // Your code here
  ```

## NaN (Not a Number)

`NaN` (Not-a-Number) is a special value in JavaScript that represents an invalid numerical operation or an unrepresentable mathematical result.

While JavaScript provides multiple ways to check if a value is not a number, the built-in `isNaN()` function should be used cautiously due to its potential for unexpected results. The primary issue with `isNaN()` is its implicit type coercion: it attempts to convert the argument to a number before checking if it's `NaN`. This behavior can lead to confusing outcomes:

```javascript
console.log(isNaN("hello")); // true
console.log(isNaN("")); // false (empty string is converted to 0)
console.log(isNaN({})); // true
```

To address these inconsistencies, ECMAScript 6 (ES6) introduced `Number.isNaN()`, a more reliable method that doesn't perform type coercion:

```javascript
console.log(Number.isNaN(NaN)); // true
console.log(Number.isNaN("hello")); // false
console.log(Number.isNaN("")); // false
console.log(Number.isNaN({})); // false
```

An alternative approach leverages a unique property of `NaN`: it's the only value in JavaScript that is not equal to itself. This characteristic allows for a simple self-comparison check:

```javascript
console.log(NaN !== NaN); // true

// As a function:
const isNaN = (value) => value !== value;
```
Both the self-comparison method `(value !== value)` and `Number.isNaN()` are reliable ways to check for `NaN`. 

## CORS (Cross-Origin Resource Sharing)

CORS is a mechanism that allows resources from one origin (domain, protocol, port) to access resources from a different origin. It's a security measure implemented by web browsers to prevent malicious websites from making unauthorized requests to other websites.

## JSONP (JSON with Padding)

JSONP is a technique used to bypass the same-origin policy restriction for making cross-origin requests. It works by exploiting the fact that `<script>` tags can load resources from different origins. JSONP is generally considered less secure than CORS and is not as widely used today.

## DOM (Document Object Model)

The DOM is a programming interface for HTML and XML documents. It represents the page as a tree of objects, allowing you to access and manipulate the content, structure, and style of a webpage using JavaScript.

## Methods to Select DOM Elements

- **`getElementById()`:** Selects an element by its unique ID.
- **`getElementsByTagName()`:** Selects a collection of elements by their tag name.
- **`getElementsByClassName()`:** Selects a collection of elements by their class name.
- **`querySelector()`:** Selects the first element that matches a given CSS selector.
- **`querySelectorAll()`:**  Selects all elements that match a given CSS selector.

## Methods to Manipulate the DOM

- **`innerHTML`:** Gets or sets the HTML content of an element.
- **`textContent`:**  Gets or sets the text content of an element (without HTML tags).
- **`classList`:** Provides methods for adding, removing, and toggling CSS classes on an element.
- **`setAttribute()`:** Sets the value of an attribute on an element.
- **`getAttribute()`:** Gets the value of an attribute on an element.
- **`appendChild()`:**  Adds a child node to an element.
- **`removeChild()`:**  Removes a child node from an element.
- **`createElement()`:** Creates a new HTML element.
- **`style`:** Accesses the inline styles of an element.

## DOM Events

Events are actions or occurrences that happen in the browser that JavaScript can detect and respond to. Common events include:

- **`click`:**  Triggered when an element is clicked.
- **`mouseover`:**  Triggered when the mouse cursor hovers over an element.
- **`submit`:**  Triggered when a form is submitted.
- **`load`:**  Triggered when a page has finished loading.

You can use the `addEventListener()` method to attach event listeners to elements.

## Event Bubbling & Event Capturing

- **Event Bubbling:** When an event is triggered on an element, it first runs the handlers on that element, then on its parent element, then all the way up the DOM tree.
- **Event Capturing:**  The event travels down the DOM tree from the root element to the target element.

## `stopPropagation()` & `preventDefault()`

- **`event.stopPropagation()`:** Prevents an event from bubbling up the DOM tree, stopping it from triggering listeners on ancestor elements.
- **`event.preventDefault()`:** Prevents the default action of an event (e.g., prevents a link from navigating to its URL).
