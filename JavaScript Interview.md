## JavaScript Interview Questions & Answers

### 1. Basics & Fundamentals

**Q1: Explain the difference between `var`, `let`, and `const`.**
**A1:** `var` is function-scoped and hoisted with `undefined`. `let` and `const` are block-scoped; `let` can be reassigned, `const` cannot (for primitives). Both `let`/`const` are hoisted to a temporal dead zone.

**Q2: What are the primitive data types in JavaScript?**
**A2:** `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`.

**Q3: Explain "hoisting" in JavaScript.**
**A3:** Hoisting moves declarations (variables with `var`, functions) to the top of their scope during compilation, before execution. `let`/`const` are hoisted but not initialized.

**Q4: What is the difference between `==` and `===`?**
**A4:** `==` performs type coercion before comparison (loose equality). `===` checks both value and type without coercion (strict equality). Use `===` for predictability.

**Q5: Describe array methods like `map()`, `filter()`, and `reduce()`.**
**A5:** `map()` creates a new array by transforming each element. `filter()` creates a new array with elements passing a test. `reduce()` aggregates array elements into a single value. All create new arrays, not modifying the original (except `reduce`).

### 2. Intermediate Concepts

**Q6: What are arrow functions, and how do they differ from regular functions regarding `this`?**
**A6:** Arrow functions are concise, lexically scoped for `this` (inherit `this` from parent scope). Regular functions' `this` depends on how they are called.

**Q7: Explain event bubbling and event capturing.**
**A7:** **Capturing** (trickle down) means the event goes from `window` to the target. **Bubbling** (bubble up) means the event goes from the target back to `window`. Bubbling is the default.

**Q8: How do you handle errors in JavaScript?**
**A8:** Using `try...catch...finally` blocks. `try` for potentially error-prone code, `catch` to handle errors, and `finally` for cleanup (always executes). You can also `throw` errors.

**Q9: What is a closure? Give an example.**
**A9:** A closure is a function bundled with its surrounding lexical environment, allowing it to access variables from its outer function even after the outer function has finished executing.
Example: `function outer(x) { return function inner(y) { console.log(x + y); }; } const add5 = outer(5); add5(3); // 8`

### 3. Asynchronous JavaScript

**Q10: Explain the difference between Callbacks, Promises, and `async/await`.**
**A10:**
* **Callbacks**: Functions passed to be executed later, can lead to "callback hell."
* **Promises**: Objects representing eventual completion/failure of an async op, offer chaining (`.then()`, `.catch()`) for better structure.
* **`async/await`**: Syntactic sugar over Promises, makes async code look synchronous, improving readability.

**Q11: How does the Event Loop work in JavaScript?**
**A11:** The Event Loop continuously checks if the Call Stack is empty. If so, it moves tasks from the Microtask Queue (Promises) to the Call Stack, then from the Macrotask Queue (`setTimeout`, I/O) one by one.

**Q12: How do you make an HTTP request in modern JavaScript?**
**A12:** Primarily using the built-in `Fetch API` (`fetch().then().catch()` or `async/await fetch()`). Libraries like Axios are also common.

### 4. Tooling and Ecosystem

**Q13: What is the purpose of `npm` (or `yarn`/`pnpm`) in a JavaScript project?**
**A13:** Package managers for dependency management (installing, updating libraries), running scripts, and managing project metadata via `package.json`.

**Q14: Why do we need Babel and transpilation in modern JavaScript development?**
**A14:** To convert modern JavaScript (ES6+) into older, widely compatible JavaScript (ES5) that browsers and older environments can understand, ensuring broad compatibility.

**Q15: What are bundlers (Webpack, Vite, Parcel) used for?**
**A15:** To combine multiple JavaScript modules and assets into optimized bundles for deployment, handling module resolution, code splitting, minification, and asset processing.

### 5. Application Architecture & Best Practices

**Q16: Explain the importance of modular code in JavaScript.**
**A16:** Improves maintainability, reusability, readability, collaboration, scalability, and testability by breaking code into independent units.

**Q17: Describe some essential debugging techniques in JavaScript.**
**A17:** `console.log()`, using browser DevTools (breakpoints, step-through, inspecting variables/call stack), and the `debugger` keyword.

**Q18: What are DRY, KISS, and YAGNI principles in software development?**
**A18:**
* **DRY**: Don't Repeat Yourself (avoid code duplication).
* **KISS**: Keep It Simple, Stupid (favor simplicity).
* **YAGNI**: You Ain't Gonna Need It (don't add functionality prematurely).

### 6. Advanced JavaScript

**Q19: Explain the `this` keyword in JavaScript and its different contexts.**
**A19:** `this` refers to the object executing the current code. Its value depends on how the function is called (global, method, standalone function, constructor, explicit bind, or lexical for arrow functions).

**Q20: What is prototypal inheritance in JavaScript?**
**A20:** JavaScript objects inherit properties and methods directly from other objects (their prototypes) through a prototype chain, rather than through classes.

**Q21: Explain the difference between microtasks and macrotasks and their role in the Event Loop.**
**A21:** Microtasks (Promises) have higher priority and are executed completely before the next Macrotask (`setTimeout`, I/O) is processed by the Event Loop.

**Q22: How does garbage collection work in JavaScript, and what are common memory leaks?**
**A22:** Garbage collection automatically reclaims memory from objects no longer reachable. Common leaks include accidental global variables, unused closures, detached DOM elements, un-cleared timers, and unremoved event listeners.

### 7. Web APIs & Browser Features

**Q23: What is the difference between `localStorage` and `sessionStorage`?**
**A23:** `localStorage` persists data across browser sessions and tabs (no expiry). `sessionStorage` clears data when the tab/window is closed and is specific to that tab.

**Q24: What are Service Workers and their primary use cases?**
**A24:** Background scripts that act as a proxy between the browser and network. Primary use cases are enabling offline capabilities/caching (PWAs), push notifications, and background sync.

**Q25: Briefly explain WebSockets.**
**A25:** WebSockets provide full-duplex, persistent, two-way communication channels between a client and server over a single TCP connection, ideal for real-time applications.

### 8. Frameworks & Libraries (React.js specific)

**Q26: What is the Virtual DOM in React, and how does it improve performance?**
**A26:** A lightweight JavaScript representation of the actual DOM. React compares the VDOM (diffing) and makes only necessary, batched updates to the real DOM, optimizing rendering performance.

**Q27: Explain the concept of "state" and "props" in React components.**
**A27:** **Props** are immutable inputs passed from parent to child. **State** is mutable internal data managed by a component, causing re-renders when it changes.

**Q28: What are React Hooks, and why were they introduced?**
**A28:** Functions that let you "hook into" React state (`useState`) and lifecycle features (`useEffect`) from functional components, reducing boilerplate, improving reusability of logic, and simplifying class component complexities.

**Q29: When would you use `Context API` vs. `Redux Toolkit` for state management in React?**
**A29:** Use **Context API** for simpler, less frequently updated global data (e.g., theme). Use **Redux Toolkit** for complex, frequently changing, distributed application state, benefiting from predictability and debugging tools.

### 9. TypeScript & Type Safety

**Q30: Why use TypeScript over plain JavaScript?**
**A30:** TypeScript adds static typing, catching errors at compile-time, improving code quality, developer tooling, readability, and scalability, especially in large projects.

**Q31: Explain Interfaces and Types in TypeScript. When would you use one over the other?**
**A31:** Both define object shapes. **Interfaces** can be merged and implemented by classes, ideal for object contracts. **Types** are more versatile for aliases of primitives, unions, and intersections. Use `interface` for object shapes, `type` for complex aliases.

### 10. Advanced Performance & DevOps

**Q32: What is code splitting and lazy loading, and why are they important for web performance?**
**A32:** **Code splitting** divides the app into smaller chunks. **Lazy loading** loads these chunks only when needed. Both reduce initial load time, improve user experience, and save memory.

**Q33: What is the significance of Accessibility (a11y) in web development?**
**A33:** Designing websites for people with disabilities (visual, motor, cognitive, etc.) ensures broader audience reach, legal compliance, and often improves the user experience for everyone.

**Q34: How does Docker help in deployment and development workflows?**
**A34:** Docker containers provide consistent, isolated, and portable environments, solving "it works on my machine" issues, streamlining deployment, and improving scalability and resource efficiency.

### 11. Going Beyond: Bonus Areas (Node.js/Backend specific)

**Q35: What is Node.js, and how does it enable full-stack JavaScript development?**
**A35:** Node.js is a JavaScript runtime that executes JS outside the browser, enabling backend development with the same language as the frontend, leading to unified development, code reuse, and efficient I/O.

**Q36: What is Express.js, and why is it commonly used with Node.js?**
**A36:** Express.js is a minimal and flexible Node.js web framework. It's used for its simplicity, robust routing, middleware system, and large ecosystem, making API and web server development easy.

**Q37: Briefly explain GraphQL and its advantages over traditional REST APIs.**
**A37:** GraphQL is a query language for APIs. Advantages over REST include allowing clients to fetch exactly what data they need (no over/under-fetching), a single endpoint, strong typing, and efficient data aggregation.
