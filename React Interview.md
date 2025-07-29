## React Interview Questions & Answers 

### I. Core Concepts & Fundamentals (1-20)

**Q1: What is React and what are its core advantages?**
**A1:** React is a JavaScript library for building user interfaces, especially single-page applications. Advantages: Component-based, Virtual DOM for performance, declarative UI, large ecosystem.

**Q2: What is JSX? Why do we use it?**
**A2:** JSX (JavaScript XML) is a syntax extension that lets you write HTML-like code directly within JavaScript. It's a syntactic sugar for `React.createElement()`, making UI creation more intuitive.

**Q3: Explain the Virtual DOM. How does it improve performance?**
**A3:** A lightweight JavaScript representation of the actual DOM. React updates the VDOM, calculates minimal changes (diffing), and then applies only those changes to the real DOM, reducing expensive direct DOM manipulations.

**Q4: Differentiate between functional and class components.**
**A4:** Functional components are plain JS functions, simpler, use Hooks for state/lifecycle. Class components are ES6 classes, use `this.state`/`this.setState` and lifecycle methods. Functional components with Hooks are now the standard.

**Q5: What are `props` in React?**
**A5:** `props` (properties) are read-only inputs passed from a parent component to a child component. They're used to configure children or pass data down the tree.

**Q6: What is `state` in React?**
**A6:** `state` is an object that holds data internal to a component. It's mutable, changes over time (e.g., user input), and triggers re-renders when updated.

**Q7: How do you handle events in React?**
**A7:** React uses synthetic events, which are cross-browser wrappers around native events. Handlers are camelCased (e.g., `onClick`) and passed as functions (e.g., `<button onClick={handleClick}>`).

**Q8: Why are "Keys" important when rendering lists in React?**
**A8:** Keys are unique identifiers for list items. They help React efficiently identify which items have changed, been added, or removed, optimizing re-renders and preventing bugs.

**Q9: What is "lifting state up"?**
**A9:** It's a pattern where if multiple child components need to share or communicate state, the state is moved to their closest common parent. The parent manages the state and passes it down as props.

**Q10: What is conditional rendering?**
**A10:** Rendering different UI elements or components based on certain conditions using JavaScript operators like `if`, ternary (`? :`), or logical `&&`.

**Q11: What are React Fragments? Why use them?**
**A11:** Fragments (`<>...</>`) allow you to group multiple elements without adding an extra node to the DOM, which helps keep the DOM structure clean and avoids unnecessary wrapper `div`s.

**Q12: How does `setState` (or `useState` update function) work asynchronously?**
**A12:** React may batch multiple `setState` calls for performance. Updates might not be immediately visible. For sequential updates, use the functional update form (`setCount(prevCount => prevCount + 1)`).

**Q13: What is "reconciliation" in React?**
**A13:** The process where React compares the new Virtual DOM tree with the old one (the "diffing" algorithm) to determine the minimal number of changes needed to update the actual DOM.

**Q14: What is the purpose of `render()` method in class components?**
**A14:** The `render()` method is mandatory in class components. It returns the JSX (React elements) that describes what should be displayed on the screen. It should be a pure function.

**Q15: What is `StrictMode` in React?**
**A15:** A development tool that highlights potential problems in an application (e.g., deprecated lifecycle methods, unexpected side effects). It doesn't render anything visible but activates extra checks.

**Q16: How do you add inline styles in React?**
**A16:** By passing a JavaScript object where keys are camelCased CSS properties and values are strings: `<div style={{color: 'blue', fontSize: '16px'}}></div>`.

**Q17: What is the `children` prop?**
**A17:** A special prop that allows components to receive and render their children. It's often used for composition: `<MyLayout><MyButton /></MyLayout>`. `MyLayout` can access `MyButton` via `props.children`.

**Q18: What is a "pure" component?**
**A18:** A component that always renders the same output given the same props and state. `React.PureComponent` (class) or `React.memo` (functional) implement a shallow prop/state comparison.

**Q19: How do you prevent a component from re-rendering?**
**A19:** Using `React.memo` (for functional components) or `PureComponent` (for class components). You can also manually implement `shouldComponentUpdate` in class components.

**Q20: What are synthetic events?**
**A20:** React's cross-browser wrapper around the browser's native event system. They normalize event behavior across different browsers and provide consistent properties.

### II. React Hooks (21-40)

**Q21: What are React Hooks? Why were they introduced?**
**A21:** Hooks are functions that let you "hook into" React state and lifecycle features from functional components. They were introduced to allow stateful logic in functional components, simplify component logic, and promote code reuse.

**Q22: Explain the `useState` Hook.**
**A22:** `useState` allows functional components to manage state. It returns an array: `[currentStateValue, setStateFunction]`.

**Q23: Explain the `useEffect` Hook and its dependency array.**
**A23:** `useEffect` performs side effects (data fetching, subscriptions, DOM manipulation) in functional components. The dependency array `[]` controls when it re-runs:
* No array: Runs after every render.
* `[]`: Runs once after the initial render.
* `[dep1, dep2]`: Runs when any dependency changes.

**Q24: What is the purpose of `useContext` Hook?**
**A24:** `useContext` allows a functional component to consume values from a React Context provider without needing a `Context.Consumer` component, simplifying access to shared data.

**Q25: Differentiate between `useMemo` and `useCallback`.**
**A25:**
* **`useMemo`**: Memoizes a *value* (result of an expensive computation). Recalculates only when dependencies change.
* **`useCallback`**: Memoizes a *function* instance. Returns the same function reference unless dependencies change. Useful for optimizing child components.

**Q26: When would you use `useRef`?**
**A26:** `useRef` is used to create a mutable ref object that persists across renders. It's primarily used to directly access DOM elements or to store mutable values that don't trigger re-renders.

**Q27: What is `useReducer` and when is it preferred over `useState`?**
**A27:** `useReducer` is an alternative to `useState` for managing more complex state logic that involves multiple sub-values or when the next state depends on the previous one. It's often preferred for state transitions that are complex or involve multiple related pieces of state.

**Q28: What are Custom Hooks? Provide an example scenario.**
**A28:** Custom Hooks are JavaScript functions whose names start with `use` and that call other Hooks. They allow you to extract and reuse stateful logic (e.g., `useFormInput`, `useLocalStorage`).

**Q29: What is the rule of Hooks?**
**A29:** 1. Only call Hooks at the top level of a React functional component or custom Hook (not inside loops, conditions, or nested functions). 2. Only call Hooks from React functional components or custom Hooks (not from regular JavaScript functions).

**Q30: Can Hooks be used in class components?**
**A30:** No, Hooks can only be used in functional components.

**Q31: How do you fetch data with Hooks?**
**A31:** Typically using `useEffect` to perform the fetch request and `useState` to store the fetched data and loading/error states. `async/await` is commonly used inside `useEffect`.

**Q32: What does the empty dependency array `[]` in `useEffect` signify?**
**A32:** It means the effect will run only once after the initial render, and it won't re-run on subsequent updates. This is similar to `componentDidMount`.

**Q33: What is the cleanup function in `useEffect`?**
**A33:** A function optionally returned by `useEffect`. It runs when the component unmounts or before the effect re-runs (if dependencies change). Used for cleanup like clearing timers, unsubscribing from events.

**Q34: How do you memoize a component using Hooks?**
**A34:** By wrapping the functional component with `React.memo()`.

**Q35: What is `useLayoutEffect` and when would you use it?**
**A35:** `useLayoutEffect` runs synchronously *after* all DOM mutations but *before* the browser paints. Use it when you need to read DOM layout or perform DOM manipulations that must happen before the browser updates the screen (e.g., measuring element size).

**Q36: What is the difference between `useEffect` and `useLayoutEffect`?**
**A36:** `useEffect` runs asynchronously *after* paint. `useLayoutEffect` runs synchronously *before* paint. `useLayoutEffect` can block visual updates, so use `useEffect` by default.

**Q37: Can you conditionally call Hooks?**
**A37:** No, you cannot. Hooks must always be called unconditionally at the top level of your functional component.

**Q38: How do you manage focus in React functional components?**
**A38:** Using `useRef` to create a ref and attach it to the DOM element, then calling `.current.focus()` on the ref.

**Q39: What is `useImperativeHandle`?**
**A39:** A Hook used with `useRef` and `forwardRef` to customize the instance value that is exposed to parent components when using refs. It's for specific imperative scenarios.

**Q40: What's the benefit of the functional update form in `useState`?**
**A40:** `setCount(prevCount => prevCount + 1)` ensures that you're always working with the latest state value, especially in scenarios where updates might be batched or asynchronous.

### III. Routing & Navigation (41-45)

**Q41: What is React Router and what is its main purpose?**
**A41:** React Router is a standard library for declarative routing in React applications. It allows defining different routes (URLs) for your app and rendering specific components based on the current URL, enabling single-page application navigation.

**Q42: How do you define routes in React Router v6?**
**A42:** Using `<BrowserRouter>`, `<Routes>`, and `<Route>` components. Example: `<Routes><Route path="/about" element={<About />} /></Routes>`.

**Q43: How do you navigate programmatically in React Router v6?**
**A43:** Using the `useNavigate` hook, which returns a function. Example: `const navigate = useNavigate(); navigate('/dashboard');`.

**Q44: What is a `Nested Route`?**
**A44:** A route defined within another route. It allows for hierarchical UI structures where a parent component might render different child components based on further URL segments.

**Q45: How do you access URL parameters in React Router v6?**
**A45:** Using the `useParams` hook. It returns an object of key/value pairs of URL parameters.

### IV. State Management (46-55)

**Q46: Explain the React Context API.**
**A46:** Context API provides a way to pass data through the component tree without having to pass props down manually at every level (prop drilling). It's suitable for "global" data like themes, user authentication.

**Q47: When would you choose Context API over a third-party state management library (like Redux)?**
**A47:** Context API is good for simpler, less frequently updated data. For complex, large-scale applications with frequent updates, middleware, and a need for strict predictability, Redux or similar libraries are often preferred.

**Q48: What is Redux? What are its core principles?**
**A48:** Redux is a predictable state container for JavaScript applications. Core principles: Single source of truth (one store), state is read-only (changes only via actions), changes are made with pure functions (reducers).

**Q49: What are `Actions` in Redux?**
**A49:** Plain JavaScript objects that describe *what happened*. They must have a `type` property and can optionally carry a `payload` of data.

**Q50: What are `Reducers` in Redux?**
**A50:** Pure functions that take the current `state` and an `action` as arguments, and return a *new* state. They specify how the application's state changes in response to actions.

**Q51: What is the `Store` in Redux?**
**A51:** The single source of truth that holds the entire application's state tree. It's created using `createStore` (or `configureStore` in Redux Toolkit).

**Q52: What is `Redux Toolkit` and why is it recommended?**
**A52:** Redux Toolkit (RTK) is the official, opinionated set of utilities for Redux development. It simplifies Redux setup and common tasks, reduces boilerplate, and makes Redux easier to use by abstracting away complexities.

**Q53: What are `Selectors` in Redux?**
**A53:** Functions used to extract specific pieces of data from the Redux store state. They can be memoized (`reselect`) for performance optimization.

**Q54: What is a `Thunk` in Redux?**
**A54:** A pattern (often implemented with `redux-thunk` middleware) that allows Redux actions to be functions instead of plain objects, enabling asynchronous logic (e.g., API calls) to be dispatched.

**Q55: What is the difference between Redux and Flux?**
**A55:** Flux is a general architectural pattern for unidirectional data flow, while Redux is a specific implementation of that pattern. Redux has a single store, whereas Flux typically has multiple stores.

### V. Performance Optimization (56-65)

**Q56: How do you optimize React application performance?**
**A56:** Use `React.memo`/`PureComponent`, `useMemo`/`useCallback`, code splitting/lazy loading (`React.lazy`/`Suspense`), optimizing list keys, avoiding unnecessary re-renders, virtualization for large lists, and using the DevTools profiler.

**Q57: What is `React.lazy` and `Suspense`?**
**A57:** `React.lazy` allows for lazy loading components (code splitting), only loading them when they are needed. `Suspense` is used to display a fallback UI (e.g., a loading spinner) while lazy-loaded components are being fetched.

**Q58: Explain `code splitting` and `lazy loading`.**
**A58:** **Code splitting** divides the application's code into smaller chunks. **Lazy loading** is the practice of loading these chunks only when they are needed, reducing the initial bundle size and improving load times.

**Q59: What is `memoization` in React?**
**A59:** A technique where the result of a function or component rendering is cached, and subsequent calls with the same inputs return the cached result without re-executing the logic or re-rendering, thereby saving computation.

**Q60: When should you *not* use `React.memo` or `useMemo`/`useCallback`?**
**A60:** When the component or function is very small and inexpensive to re-render, or when the overhead of memoization (shallow comparison) outweighs the performance gain. Over-optimization can sometimes hurt performance.

**Q61: What are "render props"?**
**A61:** A pattern where a component receives a function as a prop, and that function returns a React element. It allows for sharing reusable logic between components. Less common with Hooks.

**Q62: What are `Higher-Order Components (HOCs)`?**
**A62:** A function that takes a component as an argument and returns a new component with enhanced props or behavior. Used for reusing component logic (e.g., `withRouter`, `withAuth`). Less common with Hooks.

**Q63: What is "Server-Side Rendering (SSR)" in React? Benefits?**
**A63:** Rendering React components to HTML on the server, then sending that HTML to the client. Benefits: Faster initial page load, better SEO, improved perceived performance.

**Q64: What is "hydration" in the context of React SSR?**
**A64:** The process where client-side React "takes over" the server-rendered HTML, attaching event listeners and making it interactive. It reuses the server's static content.

**Q65: How do you measure React performance?**
**A65:** Using React DevTools Profiler, Lighthouse (browser tool), Web Vitals metrics, and `console.log` for basic timing.

### VI. Error Handling & Testing (66-70)

**Q66: What are `Error Boundaries` in React?**
**A66:** React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of crashing the entire application.

**Q67: How do you create an Error Boundary?**
**A67:** Error Boundaries are implemented as class components using `static getDerivedStateFromError()` to update state and `componentDidCatch()` to log error information.

**Q68: What testing libraries are commonly used with React?**
**A68:** Jest (testing framework) and React Testing Library (for testing React components in a user-centric way). Enzyme is an older alternative.

**Q69: What is the philosophy behind React Testing Library?**
**A69:** It encourages testing components as users would interact with them, focusing on accessibility and the final rendered output rather than internal implementation details.

**Q70: How do you mock API calls in React tests?**
**A70:** Using Jest's mocking capabilities (`jest.fn()`, `jest.spyOn()`, `jest.mock()`) or dedicated mocking libraries (like `msw` for network requests).

### VII. Styling & Best Practices (71-80)

**Q71: What are different ways to style React components?**
**A71:**
* Plain CSS/Sass (e.g., importing `.css` files).
* CSS Modules (`.module.css`).
* Inline Styles (`style={{...}}`).
* CSS-in-JS libraries (e.g., Styled Components, Emotion).
* UI frameworks (e.g., Material-UI, Ant Design).

**Q72: What are CSS Modules?**
**A72:** A CSS file where all class names and animation names are scoped locally by default, avoiding naming conflicts. They create unique hash names for classes.

**Q73: What is "CSS-in-JS"? Name popular libraries.**
**A73:** A styling paradigm where CSS is written directly within JavaScript code, typically using template literals. Popular libraries: Styled Components, Emotion.

**Q74: What is the difference between `className` and `class` in React?**
**A74:** `className` is used in JSX to specify a CSS class. `class` is the native HTML attribute. React uses `className` to avoid conflicts with JavaScript's `class` keyword.

**Q75: What are common best practices for React component structure?**
**A75:** Keep components small and focused, prefer functional components with Hooks, use custom hooks for shared logic, organize by feature, prefer composition over inheritance.

**Q76: Why should component names start with a capital letter?**
**A76:** It's a convention that helps React differentiate between a custom React component (e.g., `<MyComponent />`) and a regular HTML element (e.g., `<div />`).

**Q77: What are uncontrolled components? When would you use them?**
**A77:** Form elements where their values are managed by the DOM itself, not by React state. You typically use `useRef` to get their values when needed. Used for simpler forms or when integrating with non-React code.

**Q78: What are controlled components?**
**A78:** Form elements where their values are controlled by React state. Every state change (e.g., `onChange` event) triggers a re-render of the component. This provides a single source of truth for form data.

**Q79: What is prop drilling? How can it be avoided?**
**A79:** Passing props down through multiple layers of nested components, even if intermediate components don't directly use those props. Avoided using Context API, or state management libraries (Redux, Zustand).

**Q80: What is the benefit of TypeScript in a React project?**
**A80:** TypeScript adds static typing, catching type-related errors at compile-time, improving code quality, developer tooling (autocompletion, refactoring), and overall maintainability, especially in large codebases.

### VIII. Concurrent React & Beyond (81-90)

**Q81: What is `React Fiber`?**
**A81:** React Fiber is the re-implemented core reconciliation algorithm of React. It enables incremental rendering, allowing React to pause, resume, and prioritize rendering work, leading to smoother animations and a more responsive UI.

**Q82: What is "Concurrent Mode" (now "Concurrent Features") in React?**
**A82:** A set of new features that allow React to work on multiple tasks concurrently, leading to better user experience, especially in CPU-bound or I/O-bound scenarios. It enables features like `Suspense` for data fetching and `Transitions`.

**Q83: What are "Transitions" in React?**
**A83:** A new concurrent feature that lets you mark certain state updates as "transitions." This tells React that these updates can be interrupted if more urgent updates (like typing input) come in, improving UI responsiveness.

**Q84: What is `startTransition`?**
**A84:** A React API function (`React.startTransition`) that marks a state update as a "transition." Updates inside `startTransition` are low priority and can be interrupted.

**Q85: What are `Server Components` in React (e.g., Next.js App Router)?**
**A85:** A new paradigm where some React components render entirely on the server. They improve initial load performance by sending less JavaScript to the client and can directly access server-side resources like databases.

**Q86: How do Server Components differ from SSR?**
**A86:** SSR renders client-side components to HTML on the server. Server Components are *never* sent to the client as JavaScript; only their rendered HTML is. They re-render on the server.

**Q87: What are `Server Actions` in React?**
**A87:** Functions that run directly on the server, callable from client-side React components (e.g., form submissions). They simplify data mutations by removing the need for explicit API endpoints.

**Q88: What is `useOptimistic`?**
**A88:** A Hook used with Server Actions to update the UI immediately with an optimistic state (assuming the server action will succeed) before the actual server response is received, providing a more responsive user experience.

**Q89: What is a "hydration error" in React?**
**A89:** An error that occurs when the server-rendered HTML (SSR) does not exactly match the client-rendered React component's output. This can lead to unexpected behavior or performance issues.

**Q90: How does React 19 (expected in 2025) aim to simplify state management and forms?**
**A90:** With new features like `useFormStatus`, `useFormState`, and built-in Server Actions, aiming to make handling forms and optimistic updates more declarative and integrated into React itself, reducing the need for external libraries for basic use cases.

### IX. Ecosystem & Tooling (91-95)

**Q91: What is `Vite` and why is it popular for React development?**
**A91:** Vite is a next-generation frontend tooling that focuses on speed. It uses native ES modules for development, providing incredibly fast cold starts and hot module replacement (HMR), and leverages Rollup for production builds.

**Q92: What is the purpose of a `bundler` (e.g., Webpack, Vite)?**
**A92:** Bundlers combine multiple JavaScript modules and assets (CSS, images) into optimized bundles for deployment, handling module resolution, code splitting, minification, and asset processing.

**Q93: What is `Babel` and why is it needed for React?**
**A93:** Babel is a JavaScript compiler (transpiler). It converts modern JavaScript (ES6+, JSX, TypeScript) into older, widely compatible JavaScript (ES5) that browsers and older environments can understand.

**Q94: What is a `linter` (e.g., ESLint) and why is it important in a React project?**
**A94:** A linter analyzes code for potential errors, style inconsistencies, and questionable constructs. ESLint enforces code quality, consistency, and best practices (including React-specific rules via plugins).

**Q95: What is a `package manager` (e.g., npm, Yarn, pnpm)?**
**A95:** Tools used to manage project dependencies (installing, updating, removing libraries), run scripts, and manage project metadata (via `package.json`).

### X. Miscellaneous & Advanced (96-100)

**Q96: What is the purpose of `forwardRef`?**
**A96:** `React.forwardRef` allows you to pass a ref from a parent component down to a child component, specifically a DOM element or a class component's instance. This enables direct manipulation of the child's DOM node.

**Q97: What is the significance of "Composition" over "Inheritance" in React?**
**A97:** React encourages composition (building complex UIs from simpler, independent components) rather than inheritance. This leads to more flexible, reusable, and maintainable components by passing data and functions via props.

**Q98: When would you use `useId`?**
**A98:** `useId` is a Hook for generating unique, stable IDs that can be used for accessibility attributes (e.g., `id`, `aria-labelledby`) when a component needs to generate multiple unique IDs dynamically.

**Q99: What is the difference between `Shadow DOM` and `Virtual DOM`?**
**A99:**
* **Virtual DOM**: React's in-memory representation of the DOM for efficient updates.
* **Shadow DOM**: A browser standard for encapsulating a component's internal structure, styles, and behavior, preventing global CSS from leaking in.

**Q100: How do you handle authentication/authorization in a React app?**
**A100:** Typically involves:
* **Authentication**: Sending user credentials to a backend, receiving a token (JWT). Storing the token in `localStorage`/`sessionStorage` or cookies.
* **Authorization**: Using the token for authenticated requests, and conditionally rendering UI or routing based on user roles/permissions, often managed via Context API or a state management library.
