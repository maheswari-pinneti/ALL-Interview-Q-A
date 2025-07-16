### 1\. JavaScript: Definition, Purpose, Syntax, and Example

**Definition:**
JavaScript (JS) is a high-level, interpreted (or just-in-time compiled), multi-paradigm programming language that conforms to the ECMAScript specification. It is primarily known as the programming language for the web, enabling interactive and dynamic content on websites.

**Purpose:**
The primary purposes of JavaScript include:

  * **Client-Side Web Development:** Making web pages interactive (e.g., form validation, animations, dynamic content updates, interactive maps, games). It runs directly in the user's web browser.
  * **Server-Side Development (Node.js):** With Node.js, JavaScript can be used to build scalable network applications, RESTful APIs, microservices, and more, allowing full-stack development with a single language.
  * **Mobile App Development (React Native, NativeScript, Ionic):** Building cross-platform native mobile applications.
  * **Desktop App Development (Electron):** Creating desktop applications for Windows, macOS, and Linux.
  * **Game Development:** Building browser-based games.
  * **Backend for Data Science/Machine Learning (limited):** While not its primary domain, frameworks like TensorFlow.js allow for machine learning in the browser or with Node.js.

**Key Features & Concepts:**

  * **Dynamic Typing:** Variables are not strictly typed; their type can change during runtime.
  * **First-Class Functions:** Functions can be treated like any other variable (passed as arguments, returned from other functions, assigned to variables).
  * **Prototype-based Object-Oriented:** Uses prototypes for inheritance, rather than classes (though ES6 introduced `class` syntax as syntactic sugar over prototypes).
  * **Event-Driven:** Often reacts to user actions or other events.
  * **Asynchronous:** Handles operations like network requests without blocking the main thread using callbacks, Promises, and `async/await`.

**Basic Syntax:**

  * **Statements:** Instructions to be executed. End with a semicolon (`;`), though it's often optional (but recommended for clarity and avoiding issues with automatic semicolon insertion).
    ```javascript
    let message = "Hello, World!";
    console.log(message);
    ```
  * **Variables:** Containers for storing data. Declared with `var`, `let`, or `const`.
    ```javascript
    var oldVariable = 10; // Function-scoped, can be re-declared and re-assigned
    let newVariable = "text"; // Block-scoped, can be re-assigned
    const constantValue = true; // Block-scoped, cannot be re-assigned
    ```
  * **Data Types:**
      * **Primitive:** `string`, `number`, `boolean`, `undefined`, `null`, `symbol` (ES6), `bigint` (ES11)
      * **Non-Primitive (Object):** `object` (arrays, functions, objects, dates, regex)
  * **Operators:**
      * **Arithmetic:** `+`, `-`, `*`, `/`, `%`
      * **Assignment:** `=`, `+=`, `-=`, etc.
      * **Comparison:** `==`, `===`, `!=`, `!==`, `<`, `>`, `<=`, `>=`
      * **Logical:** `&&` (AND), `||` (OR), `!` (NOT)
  * **Comments:**
    ```javascript
    // Single-line comment

    /*
    Multi-line
    comment
    */
    ```
  * **Functions:** Reusable blocks of code.
    ```javascript
    function greet(name) {
        return "Hello, " + name + "!";
    }
    let greeting = greet("Alice"); // greeting will be "Hello, Alice!"

    // Arrow Function (ES6)
    const add = (a, b) => a + b;
    let sum = add(5, 3); // sum will be 8
    ```
  * **Control Flow (Conditionals & Loops):**
    ```javascript
    // If/Else If/Else
    let age = 20;
    if (age < 18) {
        console.log("Minor");
    } else if (age >= 18 && age < 65) {
        console.log("Adult");
    } else {
        console.log("Senior");
    }

    // Switch
    let day = "Monday";
    switch (day) {
        case "Monday":
            console.log("Start of week");
            break;
        case "Friday":
            console.log("End of week");
            break;
        default:
            console.log("Mid-week");
    }

    // For loop
    for (let i = 0; i < 5; i++) {
        console.log(i); // 0, 1, 2, 3, 4
    }

    // While loop
    let count = 0;
    while (count < 3) {
        console.log(count); // 0, 1, 2
        count++;
    }

    // For...of (for iterating over iterable objects like arrays, strings)
    let colors = ["red", "green", "blue"];
    for (const color of colors) {
        console.log(color);
    }

    // For...in (for iterating over enumerable properties of an object)
    let person = { name: "John", age: 30 };
    for (const key in person) {
        console.log(`${key}: ${person[key]}`);
    }
    ```

**Simple Example (HTML with JavaScript):**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JavaScript Example</title>
</head>
<body>
    <h1>Welcome to My Page!</h1>
    <p id="myParagraph">Click the button below to change this text.</p>
    <button id="myButton">Change Text</button>

    <script>
        // Get references to the HTML elements by their IDs
        const paragraph = document.getElementById('myParagraph');
        const button = document.getElementById('myButton');

        // Add an event listener to the button
        button.addEventListener('click', function() {
            // Change the text content of the paragraph
            paragraph.textContent = "Text has been successfully changed by JavaScript!";
            // Change the style of the paragraph
            paragraph.style.color = "blue";
            paragraph.style.fontWeight = "bold";
        });

        // Log a message to the browser's console
        console.log("JavaScript is running!");
    </script>
</body>
</html>
```

### 2\. Key HTML Tags for JavaScript Integration

JavaScript code is typically embedded within HTML documents using the `<script>` tag.

  * **`<script>`:**

      * **Purpose:** Used to embed or reference executable script.
      * **Placement:** Can be placed in the `<head>` or `<body>`.
          * **In `<head>`:** Scripts here are executed before the HTML `<body>` content is parsed. If they interact with DOM elements, those elements might not exist yet, leading to errors. Use `defer` or `async` attributes.
          * **At the end of `<body>` (recommended):** Scripts here execute after the entire HTML document has been parsed, ensuring all DOM elements are available. This also prevents render-blocking.
      * **Attributes:**
          * `src="path/to/your/script.js"`: Specifies the URL of an external script file.
          * `defer`: (Boolean) Tells the browser to execute the script after the document has been parsed, but before the `DOMContentLoaded` event fires. Scripts with `defer` maintain their relative order of execution. Ideal for scripts that depend on the DOM.
          * `async`: (Boolean) Tells the browser to execute the script asynchronously. The script is downloaded in parallel with HTML parsing and executed as soon as it's available, without blocking HTML parsing. Order of execution is not guaranteed. Ideal for independent scripts (e.g., analytics).
          * `type="module"`: (ES6 Modules) Indicates that the script is a JavaScript module. Modules have their own scope, strict mode by default, and can use `import`/`export`. They are deferred by default.

    **Examples:**

    ```html
    <script>
        console.log("Hello from inline JavaScript!");
    </script>

    <script src="my-script.js"></script>

    <head>
        <script src="dom-manipulation.js" defer></script>
    </head>

    <head>
        <script src="analytics.js" async></script>
    </head>

    <script type="module" src="my-module.js"></script>
    ```

  * **`<noscript>`:**

      * **Purpose:** Provides alternative content for users whose browsers do not support scripts or have scripting disabled.
      * **Example:**
        ```html
        <noscript>
            <p>Please enable JavaScript to view the full content of this page.</p>
        </noscript>
        ```

### 3\. Common JavaScript Topics (with Sample Questions and Answers)

Here's a structured approach to common JavaScript topics with questions and answers. I'll provide a significant number, but remember, "800" is a very large target for a single response. This will give you a solid foundation.

**Topic 1: Basics & Fundamentals**

**Q1.1: What are JavaScript data types? List them with examples.**
**A1.1:** JavaScript has primitive and non-primitive data types.

  * **Primitives:**
      * `string`: `"Hello"`, `'World'`
      * `number`: `10`, `3.14`, `NaN` (Not-a-Number), `Infinity`
      * `boolean`: `true`, `false`
      * `undefined`: A variable declared but not assigned a value. `let x;`
      * `null`: Intentional absence of any object value. `let y = null;`
      * `symbol` (ES6): Unique and immutable primitive value. `Symbol('id')`
      * `bigint` (ES11): For integers larger than `2^53 - 1`. `100n`
  * **Non-Primitive (Object):**
      * `object`: Used to store collections of data and more complex entities.
          * Plain Objects: `{ name: "Alice", age: 30 }`
          * Arrays: `[1, 2, 3]`
          * Functions: `function myFunc() {}`
          * Dates: `new Date()`
          * Regular Expressions: `/abc/`

**Q1.2: Explain the concept of "scope" in JavaScript.**
**A1.2:** Scope determines the accessibility of variables, functions, and objects in some part of your code during runtime.

  * **Global Scope:** Variables declared outside any function or block are globally scoped and accessible from anywhere in the code.
  * **Function Scope (`var`):** Variables declared with `var` inside a function are accessible only within that function.
  * **Block Scope (`let`, `const`):** Variables declared with `let` or `const` inside a block (e.g., `if` statement, `for` loop, `{ }`) are only accessible within that block.

**Q1.3: What is type coercion in JavaScript? Give an example.**
**A1.3:** Type coercion is the automatic or implicit conversion of values from one data type to another (e.g., string to number, number to boolean). This often happens during operations involving different data types.
**Example:**

```javascript
console.log(5 + "5"); // "55" (number 5 is coerced to string "5", then concatenated)
console.log(5 == "5"); // true (string "5" is coerced to number 5 for comparison)
console.log(5 === "5"); // false (strict equality, no coercion)
```

**Q1.4: Differentiate between `==` and `===` operators.**
**A1.4:**

  * **`==` (Loose Equality):** Compares values after performing type coercion if the operands are of different types. It tries to convert the operands to a common type before comparison.
  * **`===` (Strict Equality):** Compares both value and type without any type coercion. If the operands are of different types, it immediately returns `false`. This is generally recommended to avoid unexpected behavior.

**Q1.5: How do you handle errors in JavaScript?**
**A1.5:** JavaScript uses the `try...catch...finally` block for error handling.

  * **`try`:** Contains the code that might throw an error.
  * **`catch (error)`:** Executes if an error occurs in the `try` block. The `error` object contains information about the error.
  * **`finally`:** Executes regardless of whether an error occurred or not. Often used for cleanup operations.

<!-- end list -->

```javascript
try {
    let result = 10 / y; // If y is 0, this will throw a division by zero error
    console.log(result);
} catch (error) {
    console.error("An error occurred:", error.message);
} finally {
    console.log("Execution complete.");
}
```

You can also `throw` custom errors: `throw new Error("Something went wrong!");`

-----

**Topic 2: Functions**

**Q2.1: What are the different ways to define a function in JavaScript?**
**A2.1:**

1.  **Function Declaration (Named Function):**
    ```javascript
    function greet(name) {
        return "Hello, " + name;
    }
    ```
2.  **Function Expression (Anonymous or Named):**
    ```javascript
    const sayHello = function(name) { // Anonymous function expression
        return "Hello, " + name;
    };
    const factorial = function fact(n) { // Named function expression (name 'fact' only visible inside function)
        return n <= 1 ? 1 : n * fact(n - 1);
    };
    ```
3.  **Arrow Function (ES6):**
    ```javascript
    const multiply = (a, b) => a * b; // Concise syntax
    const getUser = (id, name) => ({ id: id, name: name }); // Returns an object
    ```
4.  **Immediately Invoked Function Expression (IIFE):**
    ```javascript
    (function() {
        console.log("This runs immediately!");
    })();
    ```
5.  **Constructor Function (for objects):**
    ```javascript
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    const john = new Person("John", 30);
    ```

**Q2.2: Explain "closures" in JavaScript with an example.**
**A2.2:** A closure is a function bundled together with references to its surrounding state (the lexical environment). In simpler terms, a closure "remembers" the environment in which it was created, even after the outer function has finished executing. This allows the inner function to access variables from its outer (enclosing) function's scope.

**Example:**

```javascript
function outerFunction(outerVariable) {
    return function innerFunction(innerVariable) {
        console.log('Outer Variable:', outerVariable);
        console.log('Inner Variable:', innerVariable);
    };
}

const newFunction = outerFunction('I am outer!');
newFunction('I am inner!');
// Output:
// Outer Variable: I am outer!
// Inner Variable: I am inner!

// Even though outerFunction has finished executing, newFunction (the closure)
// still has access to 'outerVariable'.
```

**Q2.3: What is the purpose of the `this` keyword in JavaScript?**
**A2.3:** The `this` keyword refers to the context in which a function is executed. Its value depends on *how* the function is called.

  * **Global Context:** In the global scope, `this` refers to the global object (`window` in browsers, `global` in Node.js).
  * **Method Call:** When a function is called as a method of an object, `this` refers to the object itself.
  * **Simple Function Call:** In non-strict mode, `this` refers to the global object. In strict mode, `this` is `undefined`.
  * **Constructor Call (`new`):** When a function is used as a constructor with `new`, `this` refers to the newly created instance.
  * **Event Handlers:** `this` typically refers to the element that triggered the event.
  * **Arrow Functions:** Arrow functions do not have their own `this` context; they inherit `this` from their enclosing lexical scope.

**Q2.4: How do `call`, `apply`, and `bind` methods work with `this`?**
**A2.4:** These are methods of `Function.prototype` that allow you to explicitly set the `this` context of a function.

  * **`call(thisArg, arg1, arg2, ...)`:** Invokes the function immediately, setting `this` to `thisArg` and passing arguments individually.
  * **`apply(thisArg, [argsArray])`:** Invokes the function immediately, setting `this` to `thisArg` and passing arguments as an array.
  * **`bind(thisArg, arg1, arg2, ...)`:** Returns a *new function* with `this` permanently bound to `thisArg` and optional initial arguments. The new function can be invoked later.

**Example:**

```javascript
const person = {
    name: "Alice",
    greet: function(city, country) {
        console.log(`Hello, my name is ${this.name} from ${city}, ${country}.`);
    }
};

const anotherPerson = {
    name: "Bob"
};

person.greet("New York", "USA"); // Output: Hello, my name is Alice from New York, USA.

// Using call
person.greet.call(anotherPerson, "London", "UK"); // Output: Hello, my name is Bob from London, UK.

// Using apply
person.greet.apply(anotherPerson, ["Paris", "France"]); // Output: Hello, my name is Bob from Paris, France.

// Using bind
const boundGreet = person.greet.bind(anotherPerson, "Berlin");
boundGreet("Germany"); // Output: Hello, my name is Bob from Berlin, Germany.
```

-----

**Topic 3: Objects & Prototypes**

**Q3.1: What is an object in JavaScript? How do you create them?**
**A3.1:** In JavaScript, almost everything is an object (except primitive values). An object is a collection of key-value pairs (properties) where values can be primitive data types, other objects, or functions (methods).
**Ways to create objects:**

1.  **Object Literal (most common):**
    ```javascript
    const user = {
        name: "John Doe",
        age: 30,
        isAdmin: false,
        greet: function() {
            console.log(`Hello, ${this.name}`);
        }
    };
    ```
2.  **`new Object()` constructor:**
    ```javascript
    const user2 = new Object();
    user2.name = "Jane Doe";
    user2.age = 25;
    ```
3.  **Constructor Functions:**
    ```javascript
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    const alice = new Person("Alice", 28);
    ```
4.  **ES6 Classes (syntactic sugar over prototypes):**
    ```javascript
    class Car {
        constructor(make, model) {
            this.make = make;
            this.model = model;
        }
        start() {
            console.log(`${this.make} ${this.model} started.`);
        }
    }
    const myCar = new Car("Toyota", "Camry");
    ```
5.  **`Object.create()`:** Creates a new object, using an existing object as the prototype of the newly created object.
    ```javascript
    const protoUser = {
        greet() { console.log(`Hello, I am ${this.name}`); }
    };
    const bob = Object.create(protoUser);
    bob.name = "Bob";
    bob.greet(); // Output: Hello, I am Bob
    ```

**Q3.2: Explain the concept of "Prototypal Inheritance" in JavaScript.**
**A3.2:** JavaScript uses prototypal inheritance, meaning objects can inherit properties and methods directly from other objects (their prototypes). Every JavaScript object has a private property `[[Prototype]]` (exposed as `__proto__` or accessed via `Object.getPrototypeOf()`) which points to its prototype object. When you try to access a property or method on an object, if it's not found on the object itself, JavaScript looks up the prototype chain until it finds the property or reaches `null`.

**Example:**

```javascript
const animal = {
    eats: true,
    walk() {
        console.log("Animal walks.");
    }
};

const rabbit = {
    jumps: true,
    __proto__: animal // rabbit inherits from animal
};

const longEar = {
    earLength: 10,
    __proto__: rabbit // longEar inherits from rabbit (and thus from animal)
};

console.log(longEar.eats); // true (inherited from animal)
longEar.walk();          // Output: Animal walks. (inherited from animal)
console.log(longEar.jumps); // true (inherited from rabbit)
```

**Q3.3: What is the difference between `null` and `undefined`?**
**A3.3:**

  * **`undefined`:** Indicates that a variable has been declared but has not yet been assigned a value. It's also returned when accessing a non-existent object property or a function doesn't explicitly return a value.
      * `typeof undefined` is `'undefined'`.
  * **`null`:** Represents the intentional absence of any object value. It's a primitive value.
      * `typeof null` is `'object'` (a long-standing bug in JavaScript).
      * `null == undefined` is `true` (loose equality).
      * `null === undefined` is `false` (strict equality).

-----

**Topic 4: Asynchronous JavaScript (Callbacks, Promises, Async/Await)**

**Q4.1: What is "asynchronous" programming in JavaScript and why is it important?**
**A4.1:** Asynchronous programming in JavaScript refers to operations that can run in the background without blocking the main execution thread. This is crucial for responsiveness, especially in web browsers. If operations like fetching data from a server or reading a file were synchronous, the browser would freeze until the operation completed, leading to a poor user experience. Asynchronous patterns allow tasks to initiate and then notify the main thread once they are done, freeing up the thread for other tasks in the meantime.

**Q4.2: Explain "Callback Hell" and how Promises help solve it.**
**A4.2:** "Callback Hell" (also known as "Pyramid of Doom") is a common issue in asynchronous JavaScript where multiple nested callbacks make the code difficult to read, understand, and maintain. It occurs when handling sequences of asynchronous operations that depend on the results of previous ones, leading to deeply indented code.

**Example of Callback Hell:**

```javascript
getData(function(data) {
    processData(data, function(processedData) {
        saveData(processedData, function(result) {
            console.log("Success:", result);
        }, function(error) {
            console.error("Save Error:", error);
        });
    }, function(error) {
        console.error("Process Error:", error);
    });
}, function(error) {
    console.error("Get Error:", error);
});
```

**How Promises Solve It:** Promises allow chaining asynchronous operations using `.then()` and `.catch()`, resulting in flatter and more readable code.

```javascript
getData()
    .then(data => processData(data))
    .then(processedData => saveData(processedData))
    .then(result => console.log("Success:", result))
    .catch(error => console.error("Error:", error));
```

**Q4.3: What are Promises? Describe their states.**
**A4.3:** A Promise is an object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value. It acts as a placeholder for a value that is not yet known but will be available in the future.
**States of a Promise:**

1.  **`pending`:** Initial state; the operation has not yet completed.
2.  **`fulfilled` (or `resolved`):** The operation completed successfully, and the Promise has a resulting value.
3.  **`rejected`:** The operation failed, and the Promise has a reason for the failure (an error).

**Q4.4: How do `async` and `await` keywords work?**
**A4.4:** `async` and `await` are syntactic sugar built on top of Promises, making asynchronous code look and behave more like synchronous code, improving readability.

  * **`async` function:** A function declared with `async` always returns a Promise. If the function returns a non-Promise value, it will be wrapped in a resolved Promise.
  * **`await` expression:** The `await` keyword can only be used inside an `async` function. It pauses the execution of the `async` function until the Promise it's waiting for settles (either resolves or rejects). If the Promise resolves, `await` returns its resolved value. If it rejects, `await` throws an error, which can be caught using a `try...catch` block.

**Example:**

```javascript
function fetchData() {
    return new Promise(resolve => {
        setTimeout(() => resolve("Data fetched!"), 2000);
    });
}

async function getAndProcessData() {
    try {
        console.log("Fetching data...");
        const data = await fetchData(); // Pause here until fetchData resolves
        console.log(data);
        console.log("Data processed.");
    } catch (error) {
        console.error("Error fetching data:", error);
    }
}

getAndProcessData();
console.log("This logs before data is fetched, demonstrating non-blocking behavior.");
```

-----

**Topic 5: DOM Manipulation**

**Q5.1: What is the DOM and what is its purpose?**
**A5.1:** DOM stands for **Document Object Model**. It's a programming interface for HTML and XML documents. It represents the structure of a web page as a tree of objects, where each node in the tree represents an HTML element, attribute, or text.
**Purpose:** The DOM provides a way for JavaScript (and other scripting languages) to access, manipulate, and update the content, structure, and style of a web page dynamically. It allows scripts to:

  * Change HTML content.
  * Change CSS styles.
  * Add and remove HTML elements.
  * React to user events (clicks, key presses, etc.).
  * Create new elements and add them to the page.

**Q5.2: How do you select elements from the DOM using JavaScript?**
**A5.2:** Common methods for selecting DOM elements:

  * `document.getElementById('idName')`: Selects a single element by its unique `id` attribute. Returns `null` if not found.
  * `document.getElementsByClassName('className')`: Selects all elements with a given class name. Returns an HTMLCollection (live list).
  * `document.getElementsByTagName('tagName')`: Selects all elements with a given tag name (e.g., `p`, `div`). Returns an HTMLCollection.
  * `document.querySelector('CSS selector')`: Selects the *first* element that matches the specified CSS selector. Returns `null` if not found. (Highly flexible)
  * `document.querySelectorAll('CSS selector')`: Selects *all* elements that match the specified CSS selector. Returns a NodeList (static list).

**Example:**

```javascript
const myDiv = document.getElementById('myDiv');
const paragraphs = document.getElementsByTagName('p');
const highlightedItems = document.querySelectorAll('.highlight');
const firstLink = document.querySelector('a');
```

**Q5.3: How do you modify HTML content and attributes using JavaScript?**
**A5.3:**

  * **Modifying Text Content:**
      * `element.textContent`: Gets or sets the text content of an element (safe, escapes HTML).
      * `element.innerText`: Similar to `textContent`, but considers CSS styling (less efficient).
  * **Modifying HTML Content:**
      * `element.innerHTML`: Gets or sets the HTML content within an element. Be cautious with user input to prevent XSS attacks.
  * **Modifying Attributes:**
      * `element.setAttribute('attributeName', 'value')`: Sets the value of an attribute.
      * `element.getAttribute('attributeName')`: Gets the value of an attribute.
      * `element.removeAttribute('attributeName')`: Removes an attribute.
      * Direct property access (for common attributes): `element.id = 'newId'`, `element.src = 'new_image.jpg'`, `element.className = 'new-class'`

**Example:**

```html
<p id="myPara">Old text</p>
<img id="myImage" src="old.jpg" alt="Old Image">
```

```javascript
const para = document.getElementById('myPara');
para.textContent = "New text!"; // Changes text
para.innerHTML = "<em>New</em> text with <strong>HTML</strong>!"; // Changes HTML

const image = document.getElementById('myImage');
image.src = "new.jpg"; // Changes the src attribute
image.setAttribute('alt', 'New Image Description'); // Changes the alt attribute
image.classList.add('rounded'); // Adds a CSS class
```

**Q5.4: How do you add/remove elements and handle events in the DOM?**
**A5.4:**

  * **Creating New Elements:**
      * `document.createElement('tagName')`: Creates a new element node.
      * `document.createTextNode('text')`: Creates a new text node.
  * **Adding/Removing Elements:**
      * `parentElement.appendChild(childElement)`: Adds a child element to the end of a parent.
      * `parentElement.insertBefore(newElement, referenceElement)`: Inserts `newElement` before `referenceElement`.
      * `parentElement.removeChild(childElement)`: Removes a specified child element.
      * `childElement.remove()`: (Modern way) Removes the element itself from its parent.
  * **Event Handling:**
      * `element.addEventListener('eventName', function, [options])`: Attaches an event listener. Recommended.
      * `element.removeEventListener('eventName', function, [options])`: Removes an event listener.
      * `element.onclick = function`: Old way, allows only one handler per event.

**Example:**

```html
<div id="container">
    <p>Existing paragraph</p>
</div>
<button id="addBtn">Add Item</button>
<button id="removeBtn">Remove First Item</button>
```

```javascript
const container = document.getElementById('container');
const addBtn = document.getElementById('addBtn');
const removeBtn = document.getElementById('removeBtn');

addBtn.addEventListener('click', function() {
    const newItem = document.createElement('li');
    newItem.textContent = `New item ${container.children.length + 1}`;
    const ul = document.createElement('ul'); // Create a UL if it doesn't exist
    if (!container.querySelector('ul')) {
        container.appendChild(ul);
    }
    container.querySelector('ul').appendChild(newItem);
});

removeBtn.addEventListener('click', function() {
    const firstLi = container.querySelector('li');
    if (firstLi) {
        firstLi.remove(); // Removes the element
        // OR: firstLi.parentNode.removeChild(firstLi);
    }
});
```

-----

**Topic 6: ES6+ Features (Modern JavaScript)**

**Q6.1: What are template literals (template strings) in ES6?**
**A6.1:** Template literals are a way to define strings that allow for embedded expressions, multi-line strings, and "tagged" templates. They are enclosed by backticks (`` ` ``) instead of single or double quotes.
**Features:**

  * **Multi-line Strings:** No need for `\n`.
  * **Expression Interpolation:** Embed expressions (variables, function calls) using `${expression}`.

**Example:**

```javascript
const name = "Alice";
const age = 30;
const greeting = `Hello, my name is ${name} and I am ${age} years old.
This is a multi-line string.
The sum of 5 and 3 is ${5 + 3}.`;
console.log(greeting);
```

**Q6.2: Explain destructuring assignment with arrays and objects.**
**A6.2:** Destructuring assignment is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.

  * **Array Destructuring:**
    ```javascript
    const numbers = [10, 20, 30, 40];
    const [a, b, , d] = numbers; // Skips the third element
    console.log(a, b, d); // Output: 10 20 40

    const [first, ...rest] = numbers; // Rest parameter
    console.log(first, rest); // Output: 10 [20, 30, 40]
    ```
  * **Object Destructuring:**
    ```javascript
    const person = { firstName: "John", lastName: "Doe", age: 30 };
    const { firstName, age } = person;
    console.log(firstName, age); // Output: John 30

    const { lastName: surname } = person; // Renaming
    console.log(surname); // Output: Doe

    function printPersonDetails({ firstName, lastName }) { // Destructuring in function parameters
        console.log(`Name: ${firstName} ${lastName}`);
    }
    printPersonDetails(person); // Output: Name: John Doe
    ```

**Q6.3: What is the spread operator (`...`) and rest parameter (`...`)?**
**A6.3:** Both use the `...` syntax, but their usage context determines their meaning.

  * **Spread Operator (`...`):**
      * **Purpose:** Expands an iterable (like an array or string) into individual elements.
      * **Use Cases:**
          * Copying arrays: `const newArr = [...oldArr];`
          * Combining arrays: `const combined = [...arr1, ...arr2];`
          * Passing array elements as arguments to functions: `Math.max(...numbers)`
          * Creating new objects with properties from existing objects: `const newObj = { ...oldObj, newProp: 'value' };`
  * **Rest Parameter (`...`):**
      * **Purpose:** Collects an indefinite number of arguments into an array. It must be the last parameter in a function definition.
      * **Use Cases:** Handling functions with a variable number of arguments.

**Example:**

```javascript
// Spread Operator
const arr1 = [1, 2];
const arr2 = [3, 4];
const combined = [...arr1, ...arr2]; // [1, 2, 3, 4]

const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };
const combinedObj = { ...obj1, ...obj2 }; // { a: 1, b: 2, c: 3, d: 4 }

function sum(a, b, c) {
    return a + b + c;
}
const numbers = [1, 2, 3];
console.log(sum(...numbers)); // Output: 6

// Rest Parameter
function logArguments(firstArg, ...restOfArgs) {
    console.log("First:", firstArg);
    console.log("Rest:", restOfArgs);
}
logArguments(1, 2, 3, 4, 5);
// Output:
// First: 1
// Rest: [2, 3, 4, 5]
```

**Q6.4: Explain ES6 Modules (`import`/`export`).**
**A6.4:** ES6 Modules provide a standardized, declarative way to organize JavaScript code into reusable, independent pieces.

  * **`export`:** Used to make variables, functions, classes, etc., available for other modules to import.
      * **Named Exports:** `export const name = "Alice"; export function func() {}`
      * **Default Exports:** `export default class MyClass {}` (only one default export per module)
  * **`import`:** Used to bring exported members from other modules into the current module's scope.
      * **Named Imports:** `import { name, func } from './myModule.js';`
      * **Default Import:** `import MyClass from './myModule.js';`
      * **Import all as a namespace:** `import * as MyModule from './myModule.js';`

**Benefits:**

  * **Modularity & Reusability:** Break code into smaller, manageable files.
  * **Dependency Management:** Clearer dependencies between files.
  * **Name Conflicts Avoidance:** Each module has its own scope.
  * **Static Analysis:** Tools can better understand module dependencies.

**Example (`myModule.js`):**

```javascript
// myModule.js
export const PI = 3.14159;

export function add(a, b) {
    return a + b;
}

const privateVar = "I am private";

export default class Calculator {
    subtract(a, b) {
        return a - b;
    }
}
```

**Example (`main.js`):**

```javascript
// main.js
import { PI, add } from './myModule.js';
import Calculator from './myModule.js'; // Default import

console.log(PI); // 3.14159
console.log(add(5, 2)); // 7

const calc = new Calculator();
console.log(calc.subtract(10, 4)); // 6
```

To use modules in HTML, use `<script type="module" src="main.js"></script>`.

-----

**Topic 7: Error Handling & Debugging**

**Q7.1: What is the `debugger` keyword and how is it used?**
**A7.1:** The `debugger` keyword acts as a breakpoint in your JavaScript code. When encountered during execution in a browser's developer console (or Node.js inspector), it will pause execution at that line, allowing you to inspect variables, step through code, and debug your application.
**Example:**

```javascript
function calculateSum(a, b) {
    let result = a + b;
    debugger; // Execution will pause here
    console.log("Result:", result);
    return result;
}
calculateSum(10, 20);
```

**Q7.2: What are common types of errors in JavaScript?**
**A7.2:**

  * **Syntax Errors:** Errors in the language structure (e.g., missing parenthesis, misplaced comma). Detected during parsing.
  * **Reference Errors:** Occur when trying to access a variable that is not declared or is out of scope. (e.g., `console.log(undeclaredVar);`)
  * **Type Errors:** Occur when an operation is performed on a value that is not of the expected type. (e.g., `null.method()`, `const obj = {}; obj.forEach();`)
  * **Range Errors:** Occur when a number is outside an allowed range (e.g., creating an array with a negative length: `new Array(-1)`).
  * **URI Errors:** Occur when an invalid URI is used in functions like `decodeURI()`.
  * **Eval Errors:** Related to the `eval()` function, which rarely occurs in modern code.
  * **Custom Errors:** Can be created and thrown using `throw new Error("My custom message");`.

-----

