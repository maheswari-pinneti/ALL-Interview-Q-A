## React Notes: Comprehensive Concepts

React is a declarative, efficient, and flexible JavaScript library for building user interfaces. It allows you to compose complex UIs from small and isolated pieces of code called "components."

### I. Core Concepts & Fundamentals

1.  **Declarative UI:**

      * You describe *what* you want the UI to look like for a given state, and React handles *how* to achieve that.
      * Makes code easier to understand and debug compared to imperative DOM manipulation.

2.  **Component-Based Architecture:**

      * UI is broken down into independent, reusable pieces (components).
      * Each component manages its own state and renders itself.
      * Promotes modularity, reusability, and easier maintenance.

3.  **JSX (JavaScript XML):**

      * A syntax extension for JavaScript that allows you to write HTML-like code directly within your JavaScript.
      * **Syntactic Sugar:** It's transpiled by tools like Babel into `React.createElement()` calls.
      * **Rules:**
          * Must return a single root element (or use `<>...</>`).
          * HTML attributes are camelCase (e.g., `className` instead of `class`, `htmlFor` instead of `for`).
          * JavaScript expressions inside JSX use curly braces `{}`.
          * Self-closing tags must be explicitly closed (e.g., `<img />`).

    <!-- end list -->

    ```jsx
    // Example JSX
    function Greeting({ name }) {
      return (
        <div className="container">
          <h1>Hello, {name}!</h1>
          <p>Welcome to React.</p>
        </div>
      );
    }
    ```

4.  **Components: Functional vs. Class:**

      * **Functional Components (Preferred):**
          * Plain JavaScript functions that accept `props` as an argument and return JSX.
          * Used with **React Hooks** to manage state and side effects.
          * Simpler, more concise, and generally easier to test.
        <!-- end list -->
        ```jsx
        // Functional Component
        function Welcome(props) {
          return <h1>Hello, {props.name}</h1>;
        }
        ```
      * **Class Components (Legacy):**
          * ES6 classes that extend `React.Component`.
          * Manage state using `this.state` and `this.setState()`.
          * Use lifecycle methods (`componentDidMount`, `componentDidUpdate`, etc.).
          * Less common in new code due to Hooks.
        <!-- end list -->
        ```jsx
        // Class Component (example, typically not used for new code)
        class WelcomeClass extends React.Component {
          render() {
            return <h1>Hello, {this.props.name}</h1>;
          }
        }
        ```

5.  **Props (Properties):**

      * **Read-Only:** Data passed from a parent component to a child component. Children should never modify their props directly.
      * **Immutable:** Treated as immutable inside the component.
      * **Configuration:** Used to configure child components or pass data down the component tree.
      * **Prop Drilling:** Passing props through many intermediate components that don't directly use them (can be avoided with Context API/state management).

    <!-- end list -->

    ```jsx
    // Parent
    function App() {
      return <Greeting name="Alice" />;
    }
    // Child (from Q1 example)
    function Greeting({ name }) { /* ... uses name */ }
    ```

6.  **State:**

      * **Internal & Mutable:** Data that is managed *within* a component and can change over time.
      * **Triggers Re-render:** When a component's state changes, React re-renders that component and its children.
      * Managed using the `useState` Hook in functional components.

    <!-- end list -->

    ```jsx
    import React, { useState } from 'react';

    function Counter() {
      const [count, setCount] = useState(0); // [currentState, updaterFunction]

      const increment = () => {
        setCount(count + 1); // Or: setCount(prevCount => prevCount + 1);
      };

      return (
        <button onClick={increment}>
          Count: {count}
        </button>
      );
    }
    ```

7.  **Virtual DOM (VDOM) & Reconciliation:**

      * **VDOM:** A lightweight JavaScript object tree that is a representation of the actual browser DOM.
      * **How it Works:**
        1.  When component state/props change, React creates a new VDOM tree.
        2.  It then compares this new VDOM with the previous one (a process called **"diffing"**).
        3.  React calculates the minimal set of changes (the "diff") needed to update the real DOM.
        4.  These changes are then "batched" and applied to the real DOM efficiently (the **"reconciliation"** process).
      * **Benefit:** Reduces expensive direct DOM manipulations, significantly improving performance.

8.  **Event Handling:**

      * React uses **Synthetic Events**, which are cross-browser wrappers around the browser's native events. They ensure consistent behavior.
      * Event handlers are camelCased (e.g., `onClick`, `onChange`).
      * You pass functions as event handlers, not strings.

    <!-- end list -->

    ```jsx
    function MyButton() {
      function handleClick() {
        console.log('Button clicked!');
      }
      return <button onClick={handleClick}>Click Me</button>;
    }
    ```

9.  **Conditional Rendering:**

      * Renders different UI based on conditions.
      * Methods: `if` statements, ternary operator (`condition ? true : false`), logical `&&` operator.

    <!-- end list -->

    ```jsx
    function UserGreeting({ isLoggedIn }) {
      return isLoggedIn ? <h1>Welcome back!</h1> : <h1>Please log in.</h1>;
    }

    function AdminPanel({ isAdmin }) {
      return (
        <div>
          {isAdmin && <button>Manage Users</button>}
          <p>Standard content</p>
        </div>
      );
    }
    ```

10. **List Rendering:**

      * Use the `map()` array method to render lists of elements from an array of data.
      * **Keys:** Each item in a list *must* have a unique `key` prop (e.g., a unique ID from your data). Keys help React efficiently identify, add, remove, and reorder elements during updates.

    <!-- end list -->

    ```jsx
    function ItemList({ items }) {
      return (
        <ul>
          {items.map(item => (
            <li key={item.id}>{item.name}</li> // Unique 'key' is crucial
          ))}
        </ul>
      );
    }
    ```

11. **Fragments (`<></>` or `<React.Fragment>...</React.Fragment>`):**

      * Allow you to group multiple elements without adding an extra node to the DOM.
      * Useful when a component needs to return multiple elements but doesn't need a wrapper `div`.

### II. React Hooks (Modern React)

Hooks are functions that let you "hook into" React state and lifecycle features from functional components. They enable writing React applications entirely with functional components.

12. **`useState`:**

      * See explanation in "State" section above.
      * The `set` function (e.g., `setCount`) can take a new value or a function that receives the previous state. The latter is recommended for updates based on previous state.

13. **`useEffect`:**

      * For performing **side effects** in functional components (e.g., data fetching, subscriptions, manual DOM manipulations, setting up timers).
      * Runs *after* every render by default.
      * **Dependency Array (`[]`):**
          * No array: Runs after every render.
          * `[]` (empty array): Runs only once after the initial render (like `componentDidMount`).
          * `[dep1, dep2]` (dependencies): Runs only when any specified dependency changes (like `componentDidUpdate`).
      * **Cleanup Function:** The function optionally returned by `useEffect` is a cleanup function. It runs when the component unmounts or before the effect re-runs (if dependencies change). Used for unsubscribing, clearing timers.

    <!-- end list -->

    ```jsx
    import React, { useState, useEffect } from 'react';

    function DataFetcher() {
      const [data, setData] = useState(null);
      const [loading, setLoading] = useState(true);

      useEffect(() => {
        // Side effect: fetch data
        fetch('https://api.example.com/data')
          .then(res => res.json())
          .then(data => {
            setData(data);
            setLoading(false);
          });

        // Cleanup function (optional)
        return () => {
          // e.g., unsubscribe from a websocket
          console.log('Component unmounted or effect re-ran.');
        };
      }, []); // Empty dependency array: runs only once on mount

      if (loading) return <p>Loading...</p>;
      return <pre>{JSON.stringify(data, null, 2)}</pre>;
    }
    ```

14. **`useContext`:**

      * A Hook that allows a functional component to consume values from a React Context without needing a `Context.Consumer` component.
      * Simplifies accessing shared/global data.

    <!-- end list -->

    ```jsx
    // 1. Create Context
    const ThemeContext = React.createContext('light');

    // 2. Provider (higher up the tree)
    function App() {
      return (
        <ThemeContext.Provider value="dark">
          <Toolbar />
        </ThemeContext.Provider>
      );
    }

    // 3. Consumer (using useContext)
    function Toolbar() {
      const theme = useContext(ThemeContext);
      return <button>Current Theme: {theme}</button>;
    }
    ```

15. **`useRef`:**

      * Returns a mutable ref object whose `.current` property is initialized to the passed argument.
      * Persists across component renders.
      * **Primary Uses:**
          * Accessing DOM elements directly (e.g., focus, measurements).
          * Storing mutable values that don't cause re-renders when updated.

    <!-- end list -->

    ```jsx
    function MyInput() {
      const inputRef = useRef(null);

      const handleClick = () => {
        inputRef.current.focus(); // Direct DOM manipulation
      };

      return (
        <>
          <input type="text" ref={inputRef} />
          <button onClick={handleClick}>Focus Input</button>
        </>
      );
    }
    ```

16. **`useMemo`:**

      * Memoizes a **value**. It will recompute the memoized value only when one of its dependencies has changed.
      * Useful for optimizing expensive calculations to avoid re-running them on every render.

    <!-- end list -->

    ```jsx
    function ProductList({ products, filter }) {
      const filteredProducts = useMemo(() => {
        console.log('Filtering products...'); // This runs only when products or filter changes
        return products.filter(p => p.name.includes(filter));
      }, [products, filter]); // Dependencies

      // ... render filteredProducts
    }
    ```

17. **`useCallback`:**

      * Memoizes a **function instance**. It returns a memoized callback function that only changes if one of the dependencies has changed.
      * Useful for optimizing child components that rely on reference equality to prevent unnecessary re-renders (e.g., when passing a callback to `React.memo`'d child).

    <!-- end list -->

    ```jsx
    function ParentComponent() {
      const [count, setCount] = useState(0);

      // This function reference only changes if 'count' changes
      const handleClick = useCallback(() => {
        console.log('Button clicked. Count:', count);
      }, [count]); // Dependency

      return (
        <>
          <ChildComponent onClick={handleClick} />
          <button onClick={() => setCount(count + 1)}>Increment Parent Count</button>
        </>
      );
    }

    // ChildComponent wrapped with React.memo will only re-render if onClick prop changes
    const ChildComponent = React.memo(({ onClick }) => {
      console.log('ChildComponent rendered');
      return <button onClick={onClick}>Child Button</button>;
    });
    ```

18. **`useReducer`:**

      * An alternative to `useState` for more complex state logic.
      * Ideal for state that involves multiple sub-values or when the next state depends on the previous one.
      * Takes a `reducer` function (current state, action -\> new state) and an `initialState`. Returns `[state, dispatch]`.

    <!-- end list -->

    ```jsx
    const initialState = { count: 0 };

    function reducer(state, action) {
      switch (action.type) {
        case 'increment':
          return { count: state.count + 1 };
        case 'decrement':
          return { count: state.count - 1 };
        default:
          throw new Error();
      }
    }

    function CounterWithReducer() {
      const [state, dispatch] = useReducer(reducer, initialState);
      return (
        <>
          Count: {state.count}
          <button onClick={() => dispatch({ type: 'increment' })}>+</button>
          <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
        </>
      );
    }
    ```

19. **Custom Hooks:**

      * Regular JavaScript functions whose names start with `use`.
      * They call other Hooks to encapsulate and reuse stateful logic across multiple components.
      * Promote code reuse and separation of concerns.

    <!-- end list -->

    ```jsx
    // Custom Hook example
    import { useState, useEffect } from 'react';

    function useWindowWidth() {
      const [width, setWidth] = useState(window.innerWidth);

      useEffect(() => {
        const handleResize = () => setWidth(window.innerWidth);
        window.addEventListener('resize', handleResize);
        return () => window.removeEventListener('resize', handleResize);
      }, []); // Run once on mount

      return width;
    }

    function MyComponent() {
      const width = useWindowWidth();
      return <p>Window width: {width}px</p>;
    }
    ```

20. **Rules of Hooks:**

      * **Only Call Hooks at the Top Level:** Don't call Hooks inside loops, conditions, or nested functions.
      * **Only Call Hooks from React Functions:** Call them from functional components or custom Hooks, not from regular JavaScript functions.

### III. Advanced React Concepts

21. **`React.memo`:**

      * A Higher-Order Component (HOC) used to memoize functional components.
      * Prevents a functional component from re-rendering if its props have not changed (performs a shallow comparison of props).
      * Use for "pure" components that render the same output for the same input.

    <!-- end list -->

    ```jsx
    const MyMemoizedComponent = React.memo(function MyComponent(props) {
      /* render using props */
    });
    ```

22. **`forwardRef`:**

      * A utility that lets your component pass a ref it receives down to a child component, specifically to a DOM element or a class component instance.
      * Useful for focus management, measuring sizes, or triggering imperative animations.

    <!-- end list -->

    ```jsx
    const MyInput = React.forwardRef((props, ref) => (
      <input type="text" ref={ref} {...props} />
    ));

    function App() {
      const inputRef = useRef(null);
      return <MyInput ref={inputRef} />;
    }
    ```

23. **Portals:**

      * Provide a way to render children into a DOM node that exists outside the DOM hierarchy of the parent component.
      * Useful for modals, tooltips, or dropdowns that need to break out of their parent's CSS stacking context or overflow settings.

    <!-- end list -->

    ```jsx
    import ReactDOM from 'react-dom';

    function MyModal({ children }) {
      return ReactDOM.createPortal(
        <div className="modal-backdrop">
          <div className="modal-content">{children}</div>
        </div>,
        document.getElementById('modal-root') // Target DOM node
      );
    }
    // In index.html: <div id="modal-root"></div>
    ```

24. **Higher-Order Components (HOCs) & Render Props (Legacy Patterns for Logic Reuse):**

      * **HOCs:** A function that takes a component as an argument and returns a new component with enhanced props or behavior. (e.g., `withRouter` from React Router v5).
      * **Render Props:** A pattern where a component takes a function as a prop, and that function returns a React element. It allows for sharing reusable logic.
      * **Note:** Both are largely superseded by Custom Hooks for most use cases, as Hooks offer a simpler, more direct way to reuse stateful logic.

25. **Error Boundaries:**

      * React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of crashing the entire application.
      * Implemented as **class components** using `static getDerivedStateFromError()` and `componentDidCatch()`.
      * Only catch errors in their children, not in themselves.

    <!-- end list -->

    ```jsx
    class ErrorBoundary extends React.Component {
      constructor(props) {
        super(props);
        this.state = { hasError: false };
      }

      static getDerivedStateFromError(error) {
        return { hasError: true };
      }

      componentDidCatch(error, errorInfo) {
        console.error("ErrorBoundary caught an error:", error, errorInfo);
      }

      render() {
        if (this.state.hasError) {
          return <h1>Something went wrong.</h1>;
        }
        return this.props.children;
      }
    }

    // Usage:
    <ErrorBoundary>
      <MyPotentiallyBuggyComponent />
    </ErrorBoundary>
    ```

### IV. Performance Optimization

26. **Minimizing Re-renders:**

      * Use `React.memo` (functional) or `PureComponent` (class) to prevent re-renders if props/state haven't shallowly changed.
      * Use `useMemo` for expensive computations and `useCallback` for stable function references.
      * Avoid unnecessary state updates.
      * Ensure stable `keys` for lists.

27. **Code Splitting & Lazy Loading:**

      * **Code Splitting:** Dividing the application's JavaScript bundle into smaller "chunks" that can be loaded on demand.
      * **Lazy Loading:** Loading these chunks only when they are needed.
      * **`React.lazy` & `Suspense`:**
          * `React.lazy()` allows you to define a dynamically imported component.
          * `<Suspense fallback={<LoadingSpinner />}>` allows you to display a fallback UI (e.g., loading spinner) while lazy components are being loaded.

    <!-- end list -->

    ```jsx
    const OtherComponent = React.lazy(() => import('./OtherComponent'));

    function MyPage() {
      return (
        <Suspense fallback={<div>Loading...</div>}>
          <OtherComponent />
        </Suspense>
      );
    }
    ```

28. **List Virtualization:**

      * For very long lists, render only the items currently visible in the viewport using libraries like `react-window` or `react-virtualized`.

29. **React DevTools Profiler:**

      * A browser extension that helps analyze component render times and identify performance bottlenecks.

### V. React Routing

30. **React Router (v6+):**
      * A standard library for declarative routing in React applications.
      * Enables single-page application (SPA) navigation without full page reloads.
      * **Key Components:**
          * `<BrowserRouter>`: Uses HTML5 history API for routing.
          * `<Routes>`: Groups `<Route>` components. Only one `<Route>` child renders at a time.
          * `<Route path="/some-path" element={<MyComponent />} />`: Defines a route.
          * `<Link to="/path">`: For declarative navigation.
          * `useNavigate()`: Hook for programmatic navigation.
          * `useParams()`: Hook to access URL parameters (e.g., `/users/:id`).
          * `useLocation()`: Hook to get the current URL object.
          * `useSearchParams()`: Hook to access query parameters (e.g., `?name=Alice`).
    <!-- end list -->
    ```jsx
    import { BrowserRouter, Routes, Route, Link, useNavigate, useParams } from 'react-router-dom';

    function App() {
      return (
        <BrowserRouter>
          <nav>
            <Link to="/">Home</Link> | <Link to="/about">About</Link>
          </nav>
          <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />
            <Route path="/users/:userId" element={<UserProfile />} />
            <Route path="*" element={<NoMatch />} /> {/* Catch-all route */}
          </Routes>
        </BrowserRouter>
      );
    }

    function UserProfile() {
      const { userId } = useParams(); // Get URL parameter
      return <h2>User ID: {userId}</h2>;
    }
    ```

### VI. State Management Beyond `useState`

31. **Context API (Revisited):**

      * Best for data that is considered "global" or frequently accessed by many components at different levels, and doesn't change very frequently (e.g., user authentication, theme).
      * Avoids prop drilling.

32. **Redux:**

      * A predictable state container for JavaScript apps. Provides a centralized store for global application state.
      * **Core Principles:**
          * **Single Source of Truth:** One store holds all state.
          * **State is Read-Only:** Only way to change state is by dispatching an action.
          * **Changes with Pure Functions:** Reducers (pure functions) take current state and action to produce new state.
      * **Core Concepts:**
          * **Store:** Holds the application's state.
          * **Actions:** Plain JS objects describing *what happened* (`{ type: 'ADD_TODO', payload: 'Buy milk' }`).
          * **Reducers:** Pure functions that specify *how* the state changes in response to actions.
          * **Dispatch:** Method to send an action to the store.
          * **Selectors:** Functions to extract specific data from the store.
      * **Thunks (Middleware):** Enable asynchronous logic (e.g., API calls) in Redux actions.

33. **Redux Toolkit (RTK):**

      * **Official Recommended Approach:** Simplifies Redux development by reducing boilerplate and providing opinionated utilities.
      * **Key Features:**
          * `configureStore()`: Simplifies store setup.
          * `createSlice()`: Generates action creators and reducers automatically.
          * `createAsyncThunk()`: Handles common async patterns.
          * `RTK Query`: Powerful data fetching and caching solution built on Redux.
      * **Benefits:** Faster development, less boilerplate, better developer experience.

34. **Other State Management Libraries:**

      * **Zustand:** A small, fast, and scalable bear-necessities state management solution. Simpler than Redux for many cases.
      * **MobX:** Another popular alternative that uses observable data and reactive programming principles.

### VII. Styling React Components

35. **Inline Styles:**

      * Pass a JavaScript object where keys are camelCased CSS properties.
      * `style={{ color: 'blue', fontSize: '16px' }}`
      * Limited for complex styling, no pseudo-selectors, no media queries.

36. **CSS in JavaScript (CSS-in-JS):**

      * Write CSS directly within JavaScript using tagged template literals or objects.
      * **Libraries:** Styled Components, Emotion.
      * **Benefits:** Scoped styles (no class name conflicts), dynamic styles based on props/state, co-location of styles with components.

    <!-- end list -->

    ```jsx
    // Styled Components Example
    import styled from 'styled-components';

    const StyledButton = styled.button`
      background-color: ${props => props.primary ? 'blue' : 'gray'};
      color: white;
      padding: 10px 20px;
      border-radius: 5px;
    `;

    function MyComponent() {
      return <StyledButton primary>Click Me</StyledButton>;
    }
    ```

37. **CSS Modules:**

      * CSS files where all class names are scoped locally by default (generated unique class names).
      * Avoids global namespace conflicts.
      * Imported like JS objects: `import styles from './MyComponent.module.css';`
      * Usage: `<div className={styles.myClass}>`.

38. **Plain CSS/Sass:**

      * Regular CSS files. Need to manage class name conflicts manually (e.g., BEM methodology).

### VIII. Accessibility (a11y)

39. **Semantic HTML:** Use appropriate HTML elements (e.g., `<button>`, `<nav>`, `<main>`) for their semantic meaning.
40. **ARIA Attributes:** Use `aria-*` attributes (Accessible Rich Internet Applications) when semantic HTML isn't sufficient to convey meaning to assistive technologies.
41. **Keyboard Navigation:** Ensure all interactive elements are keyboard accessible (tabbing, enter key).
42. **Focus Management:** Provide clear visual focus indicators.
43. **Image Alt Text:** Always provide meaningful `alt` attributes for images.
44. **Linter Tools:** Use ESLint plugins like `jsx-a11y` to enforce accessibility best practices.

### IX. Testing React Components

45. **Jest:** A JavaScript testing framework (often used for unit and integration tests).
46. **React Testing Library (RTL):**
      * A testing utility that encourages good testing practices by focusing on testing components as users would interact with them.
      * Prioritizes queries that mimic how users find elements (e.g., `getByText`, `getByRole`, `getByLabelText`).
      * Less focused on internal implementation details.

### X. Ecosystem & Tooling

47. **Babel:** A JavaScript compiler that transforms modern JS (including JSX, ES6+) into backwards-compatible JS.
48. **Webpack / Vite / Parcel (Bundlers):**
      * Combine multiple JavaScript modules and assets into a single (or few) optimized bundles for deployment.
      * **Vite:** Gaining popularity for its speed (native ES module support, fast HMR).
49. **ESLint:** A static code analysis tool that identifies problematic patterns found in JavaScript code (linting).
50. **Prettier:** An opinionated code formatter that enforces a consistent style across your codebase.
51. **npm / Yarn / pnpm (Package Managers):** Manage project dependencies.

### XI. Current & Future React Concepts (2025 Outlook)

52. **Concurrent React (Concurrent Features):**

      * A set of new features that allow React to work on multiple tasks concurrently.
      * Enables **interruptible rendering** for better responsiveness.
      * **`startTransition`**: Marks non-urgent state updates as "transitions," allowing React to prioritize urgent updates (like typing) and interrupt transitions.
      * **`useDeferredValue`**: A Hook to defer updating a part of the UI, allowing other more urgent updates to render first.
      * **`Suspense` (for Data Fetching):** While already used for lazy loading, Suspense is being extended to handle data fetching, displaying fallbacks while data resolves.

53. **React Server Components (RSC) (Next.js App Router focus):**

      * A new type of React component that renders *only* on the server.
      * **Key Idea:** Reduce JavaScript sent to the client. Server Components send only their rendered HTML and CSS.
      * Can directly access server-side resources (e.g., databases, file system) without an API layer.
      * Interactivity often added by nesting **Client Components** within Server Components.

54. **Server Actions (Next.js App Router focus, React 19):**

      * Functions that run directly on the server, callable from client-side React components.
      * Simplify data mutations (form submissions, button clicks) by removing the need for explicit API endpoints.
      * Integrated with React's form management and optimistic updates (`useOptimistic`).

55. **`useFormStatus` (React 19):**

      * Hook for form components to read the pending state of an enclosing HTML `<form>` submission, enabling loading indicators and disabling inputs.

56. **`useFormState` (React 19):**

      * Hook for form components to manage state returned by a server action, enabling error messages or success states tied to form submissions.

57. **`useOptimistic` (React 19):**

      * Hook to update the UI immediately with an "optimistic" state (assuming a server action will succeed) before the actual server response is received, providing a more responsive user experience.

### XII. React Best Practices

58. **Component Granularity:** Keep components small, focused, and single-purpose.
59. **DRY (Don't Repeat Yourself):** Reuse logic via custom Hooks, utility functions.
60. **Favor Composition over Inheritance:** Build complex UIs by composing simpler components.
61. **Immutability:** Treat state and props as immutable. When updating state, create new objects/arrays instead of modifying existing ones.
62. **One-Way Data Flow:** Data flows down from parent to child via props. Child components communicate back up via callbacks passed as props.
63. **Props Validation:** Use PropTypes (legacy) or TypeScript (recommended) for type checking props.
64. **Avoid Direct DOM Manipulation:** Let React manage the DOM via state/props. Use `useRef` only when absolutely necessary.
65. **Accessibility First:** Design and develop with accessibility in mind from the start.

-----

