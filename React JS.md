
**What is React?**
- React is a front-end and open-source JavaScript library which is useful in developing user interfaces specifically for applications with a single page.
- It is helpful in building complex and reusable user interface(UI) components of mobile and web applications as it follows the component-based approach.
- React.JS is an open-source, front end, JavaScript library for building user interfaces or UI components.

**The important features of React are:**
- It supports server-side rendering.
- It will make use of the virtual DOM rather than real DOM (Data Object Model) as RealDOM manipulations are expensive.
- It follows unidirectional data binding or data flow.
- It uses reusable or composable UI components for developing the view.


**Virtual DOM:**
- The virtual DOM (VDOM) is a programming concept where an ideal, or “virtual”, representation of a UI is kept in memory and synced with the “real” DOM by a library such as ReactDOM. This process is called reconciliation.
- The virtual DOM is essentially a lightweight representation of the actual DOM (Document Object Model) that React uses to keep track of changes to your webpage.
- When you make changes to your webpage in React, instead of immediately updating the actual DOM, React first updates the virtual DOM to reflect these changes.
- This is because updating the actual DOM can be slow and resource-intensive, especially for complex webpages.
- By using the virtual DOM, React can quickly determine which parts of the actual DOM need to be updated, and only update those parts, which can lead to improved performance.
- Once the virtual DOM has been updated, React then performs a "diffing" algorithm to compare the new virtual DOM with the previous one, and identify any differences between them.
- Based on these differences, React determines which parts of the actual DOM need to be updated, and updates them accordingly.
- Overall, the virtual DOM is an important part of React's performance optimization strategy, and helps to ensure that your webpages are updated quickly and efficiently.

- **Shadow DOM** is a browser technology designed primarily for scoping variables and CSS in web components.

**How Virtual DOM helps React?**
- Each time we change something in our JSX file, all the objects that are there in the virtual DOM gets updated.
- React maintains two Virtual DOM at each time, one contains the updated Virtual DOM and one which is just the pre-update version of this updated Virtual DOM.
- Now it compares the pre-update version with the updated Virtual DOM and figures out what exactly has changed in the DOM.
- Once React finds out what exactly has changed then it updated those objects only, on real DOM.
- This significantly improves the performance.

- Shallow Comparision is a comparison of refernces of two objects but not deep comparison of objects.

**What is JSX?**
- JSX stands for JavaScript XML.
- It allows us to write HTML inside JavaScript and place them in the DOM without using functions like appendChild( ) or createElement( ).
- Note- We can create react applications without using JSX as well.
- Without using JSX, we would have to create an element by the following process:
const text = React.createElement('p', {}, 'This is a text');
const container = React.createElement('div','{}',text );
ReactDOM.render(container,rootElement);
- Using JSX, the above code can be simplified:
```javascript
const container = (
  <div>
   <p>This is a text</p>
  </div>
);
ReactDOM.render(container,rootElement);
```

- Class components are stateful components.
- Functional components are stateless components before introducing hooks.

**state:**
- state is basically an object that will be available and maintained within the component and cannot be accessible outside the component.
**props:**
- props are inputs to components. They are data passed down from a parent component to child component.

- Class component and Functional component differences
- How to pass data from child component to parent component?

**Controlled component:**
- A controlled component is one where the value of the form element is controlled by React state.
- This means that the component's value is always up-to-date and reflects the current state of the component.
- Whenever the user interacts with the component, the state is updated, and the component is re-rendered with the new value.
- The state is managed by the parent component, which passes down the value as a prop and provides an onChange handler to update the state when the value changes.
Example:
```javascript
import React, { useState } from 'react';

function ControlledInput() {
	const [value, setValue] = useState('');

	const handleChange = (event) => {
		setValue(event.target.value);
	};

	return (
		<input type="text" value={value} onChange={handleChange} />
	);
}
```

**Uncontrolled component:**
-  An uncontrolled component is one where the value of the form element is managed by the DOM.
- This means that the component's value is not controlled by React state but instead is read from the DOM when needed.
- Whenever the user interacts with the component, the DOM is updated, but React doesn't know about it.
- To get the current value of an uncontrolled component, we need to use a ref to access the DOM node.
  **Example:**
```javascript
    import React, { useRef } from 'react';

    function UncontrolledInput() {
      const inputRef = useRef(null);

      const handleSubmit = (event) => {
        event.preventDefault();
        console.log(inputRef.current.value);
      };

      return (
        <form onSubmit={handleSubmit}>
          <input type="text" ref={inputRef} />
          <button type="submit">Submit</button>
        </form>
      );
    }
```

**React Life Cycle Methods:**

1. Mounting Phase
2. Updating Phase
3. Unmounting Phase

**1. Mounting Phase**
- This phase is when a component is being created and inserted into the DOM. React provides lifecycle methods that are invoked at specific points during this process.

**Lifecycle methods in the mounting phase:**
- constructor(): This is the first method called when a component is being created. It is used for initializing the state and binding methods.
- static getDerivedStateFromProps(): This method is called before rendering, both on the initial mount and on subsequent updates. It is used to update the state based on the props.
- render(): This method is responsible for describing what the UI should look like. It returns JSX, which React uses to build and update the DOM.
- componentDidMount(): This method is invoked immediately after the component is inserted into the DOM. It is often used to fetch data or perform other side effects (e.g., setting up subscriptions or timers).

**2. Updating Phase**
- This phase occurs whenever a component’s state or props change, causing the component to re-render. This can happen due to a user interaction, data update, or when the parent component passes new props.

**Lifecycle methods in the updating phase:**
- static getDerivedStateFromProps(): As in the mounting phase, this method is invoked when the component receives new props. It allows the state to be updated in response to props changes.
- shouldComponentUpdate(): This method is used to control whether a re-render should occur or not. It returns a boolean value (true by default). You can override this to optimize performance by preventing unnecessary re-renders.
- render(): This method is called again to re-render the component when state or props change.
- getSnapshotBeforeUpdate(): This method is called right before the changes from the virtual DOM are reflected in the actual DOM. It is commonly used to capture some information from the DOM (e.g., scroll position) before it is updated.
- componentDidUpdate(): This method is invoked immediately after the component is updated in the DOM. It can be used to perform operations in response to the update, such as fetching new data based on updated props.


**3. Unmounting Phase**
- This is the phase when a component is being removed from the DOM. React provides a method to handle any necessary cleanup before the component is destroyed.

**Lifecycle method in the unmounting phase:**
- componentWillUnmount(): This method is called just before the component is removed from the DOM. It is typically used to clean up resources like timers, network requests, or subscriptions that were created during componentDidMount.

**React Lifecycle Overview (with modern hooks):**

```
Mounting:
  constructor() -> static getDerivedStateFromProps() -> render() -> componentDidMount()

Updating:
  static getDerivedStateFromProps() -> shouldComponentUpdate() -> render() -> getSnapshotBeforeUpdate() -> componentDidUpdate()

Unmounting:
  componentWillUnmount()
```

- componentWillMount
- componentDidMount
- static getDerivedStateFromProps
- shouldComponentUpdate
- componentDidUpdate
- componentWillUnmount
- getDerivedStateFromError
- componentDidCatch


**static getDerivedStateFromError(error):**
- This method is called when an error is thrown in a child component.
- It allows you to update the state to display a fallback UI.
- This method receives the error as a parameter and should return an object to update the state.
```javascript
static getDerivedStateFromError(error) {
    // Update state to display fallback UI
    return { hasError: true };
}
```
**componentDidCatch(error, info):**
- This method is called after an error has been thrown by a child component.
- It can be used for logging the error or performing side effects (e.g., sending error details to an error reporting service).
- This method receives the error and an info object containing details about the component that threw the error.
```javascript
componentDidCatch(error, info) {
    // Log the error to an error reporting service
    console.error("Error caught in error boundary:", error, info);
}
```

**React Lifecycle with Hooks (Functional Components)**
- With React hooks, functional components also have a way to handle lifecycle events, although the pattern is different. Here are common hooks that replace some of the lifecycle methods:

- useEffect(): This hook is the most common way to handle side effects like componentDidMount, componentDidUpdate, and componentWillUnmount. It runs after rendering and can return a cleanup function to handle unmounting.
```javascript
useEffect(() => {
  // Code to run on mount and update

  return () => {
    // Cleanup code to run on unmount
  };
}, [dependencies]); // Runs when the values in the dependencies array change
```
- useState(): This hook is used to declare state in functional components, replacing the state management in the constructor.

**Summary of Lifecycle Methods in Class Components:**
- Mounting: constructor(), getDerivedStateFromProps(), render(), componentDidMount()
- Updating: getDerivedStateFromProps(), shouldComponentUpdate(), render(), getSnapshotBeforeUpdate(), componentDidUpdate()
- Unmounting: componentWillUnmount()
- For functional components with hooks, useEffect() handles most of the side effects in both the mounting and updating phases, and it also manages cleanup during unmounting.



- A higher-order component (HOC) is a function that takes a component and returns a new component.
- We call them pure components because they can accept any dynamically provided child component but they won't modify or copy any behavior from their input components.

- Context provides a way to pass data through the component tree without having to pass props down manually at every level.

**What is the purpose of using super constructor with props argument?**

- We cannot use "this" reference inside constructor until super() method has been called.
- The reason of passing props parameter to super() is to access this.props in constructor

**What is reconciliation?**
- When a component's props or state change, React decides whether an actual DOM update is necessary by comparing the newly returned element with the previously rendered one.
- When they are not equal, React will update the DOM. This process is called reconciliation.

**What is useCallback in React? Explain with example?**
- useCallback is a hook provided by React that allows you to memoize a function and prevent it from being re-created on every re-render.
- This can be helpful in optimizing the performance of your React application, especially when dealing with large or complex components.

**Example:**
```javascript
      import React, { useState, useCallback } from 'react';

      function MyComponent() {
        const [count, setCount] = useState(0);

        // Define a function that increments the count state
        const incrementCount = useCallback(() => {
          setCount(prevCount => prevCount + 1);
        }, [setCount]);

        return (
          <div>
            <p>Count: {count}</p>
            <button onClick={incrementCount}>Increment</button>
          </div>
        );
      }
```

- In the example above, we define a state variable count using the useState hook.
- We also define a function incrementCount that increments the count state by 1.
- We use useCallback to memoize the incrementCount function so that it is only re-created when the setCount function changes.
- This prevents unnecessary re-renders of our component and improves performance.
- Note that the second argument of useCallback is an array of dependencies.
- These dependencies tell React when to re-create the memoized function.
- In this case, we pass in [setCount] as a dependency, which means that the incrementCount function will be re-created only when the setCount function changes.

**What is useMemo in React? Explain with example?**
- useMemo is another hook provided by React that allows you to memoize a value and prevent it from being re-computed on every re-render.
- This can be helpful in optimizing the performance of your React application, especially when dealing with expensive computations.

**Example:**
```javascript
    import React, { useState, useMemo } from 'react';

    function MyComponent() {
      const [count, setCount] = useState(0);

      // Define a function that returns a computed value
      const expensiveValue = useMemo(() => {
        console.log('Computing expensive value...');
        let result = 0;
        for (let i = 0; i < 1000000000; i++) {
          result += i;
        }
        return result;
      }, []);

      return (
        <div>
          <p>Count: {count}</p>
          <p>Expensive Value: {expensiveValue}</p>
          <button onClick={() => setCount(count + 1)}>Increment</button>
        </div>
      );
    }
```
- In the example above, we define a state variable count using the useState hook.
- We also define a function expensiveValue that computes an expensive value using a loop.
- We use useMemo to memoize the expensiveValue value so that it is only re-computed when the dependencies (in this case, the empty array []) change.
- This prevents unnecessary re-computation of our expensive value and improves performance.
- Note that the first argument of useMemo is a function that returns a computed value.
- The second argument is an array of dependencies.
- These dependencies tell React when to re-compute the memoized value.
- In this case, we pass in an empty array [] as a dependency, which means that the expensiveValue value will be re-computed only when the component mounts.


**What is the difference between useCallback and useMemo?**
- The useCallback and useMemo hooks are similar in that they both help to optimize the performance of React components by memoizing values.
- However, they differ in how they are used and what they memoize.
- useCallback is used to memoize a function and prevent it from being re-created on every re-render.
- It takes a function as its first argument and an array of dependencies as its second argument.
- The function is only re-created when one of the dependencies changes.
- This can be useful for optimizing the performance of event handlers or callbacks that are passed as props to child components.
- useMemo, on the other hand, is used to memoize a value and prevent it from being re-computed on every re-render.
- It takes a function as its first argument and an array of dependencies as its second argument.
- The function is only re-executed when one of the dependencies changes.
- This can be useful for optimizing the performance of expensive computations that are used as props or state variables.
- To summarize, useCallback memoizes a function, while useMemo memoizes a value.
- They both take an array of dependencies as a second argument, and they both help to optimize the performance of React components.

**What are the disadvantages of useCallback and useMemo?**
- While useCallback and useMemo can be helpful in optimizing the performance of React components, there are some potential disadvantages to consider.
- One disadvantage of useCallback is that it can be overused, leading to unnecessarily complex code.
- Memoizing every function in a component can make the code harder to read and maintain, and may not always provide a significant performance boost.
- Another disadvantage of useCallback is that it can lead to reference equality issues.
- If the dependencies array is not carefully managed, it can result in the memoized function not being updated when it should be.
- This can cause bugs that are difficult to track down.
- Similarly, a potential disadvantage of useMemo is that it can also lead to reference equality issues.
- If the dependencies array is not carefully managed, it can result in the memoized value not being updated when it should be.
- This can cause bugs and lead to unexpected behavior.
- Another potential disadvantage of useMemo is that it can add complexity to the code.
- Memoizing every value in a component can make the code harder to read and maintain, and may not always provide a significant performance boost.
- Overall, useCallback and useMemo can be helpful in optimizing the performance of React components, but it's important to use them judiciously and be aware of their potential disadvantages. It's also important to carefully manage the dependencies arrays to avoid reference equality issues.


**Main advantages of React:**
- Increases the application's performance with Virtual DOM.
- JSX makes code easy to read and write.
- It renders both on client and server side (SSR).
- Easy to integrate with frameworks (Angular, Backbone) since it is only a view library.
- Easy to write unit and integration tests with tools such as Jest.

**Few limitations of React too:**
- React is just a view library, not a full framework.
- There is a learning curve for beginners who are new to web development.
- Integrating React into a traditional MVC framework requires some additional configuration.
- The code complexity increases with inline templating and JSX.
- Too many smaller components leading to over engineering or boilerplate.

- Requires additional tools: To use React.js, developers need to use additional tools such as a build system and package manager. This can add complexity to the development process.

- Large file size: The React library is relatively large, which can increase page load times and affect performance.

- Boilerplate code: React.js requires developers to write a lot of boilerplate code, which can be time-consuming and tedious.

- SEO: React.js was not initially designed with SEO in mind. While there are workarounds, it can still be challenging to ensure good SEO performance with React.

- Security: React.js relies heavily on JavaScript, which can be vulnerable to security risks if not properly secured.

- Frequent updates: React.js is a rapidly evolving library, and new versions are released frequently. This can make it challenging to keep up with the latest updates and changes.

**React Hooks:**
- Hooks are functions that allow to use React state and lifecycle features in a functional component.
- React Hooks are a feature introduced in React 16.8 that allow developers to use state and other React features without writing a class component.
- With Hooks, developers can use stateful logic in functional components, which makes it easier to reuse and share code, and improves code readability.
- There are several built-in Hooks in React, such as useState, useEffect, useContext, useReducer, useCallback, useMemo, useRef, and useImperativeHandle.
- These Hooks allow developers to manage state, perform side effects, share data between components, optimize performance, and work with DOM elements, among other things.

**Rules of Hooks:**
1. Only Call Hooks at the Top Level
- Do not call hooks inside loops, conditions, or nested functions. This rule ensures that hooks are called in the same order each time a component renders.

2. Only Call Hooks from React Functions
- You can only call hooks from React functional components or custom hooks. Do not call them from regular JavaScript functions, class components, or event handlers.

**useEffect vs useLayoutEffect:**
**useEffect:**
- useEffect runs asynchronously after the DOM is rendered.
- This means that the effect will not block the browser from updating the screen
- It can lead to a slight delay before the effect runs, making it suitable for operations that don’t require immediate changes to the layout.

**Common Use Cases:**
- Fetching data.
- Subscribing to events.
- Manually changing the DOM (but without needing to read layout).

useLayoutEffect:
- useLayoutEffect runs synchronously after all DOM mutations but before the browser has a chance to render.
- This means that it runs immediately after the render phase and before the screen updates, which can be useful for operations that need to read layout information or make changes that affect the layout.

**Common Use Cases:**
- Measuring the size or position of DOM elements.
- Synchronizing visual updates to avoid flickering.
- Making adjustments based on layout before the user sees the updates.

**Ex:**
```javascript
useLayoutEffect(() => {
    // Measure the DOM node after rendering
    const rect = myRef.current.getBoundingClientRect();
    console.log(rect);

    // Optional cleanup function
    return () => {
        // Cleanup logic here
    };
}, [dependencies]); // Runs when dependencies change
```


Context API:
- In React, the Context API is a way to manage data that needs to be accessed by multiple components without having to pass the data through every component in the tree.
- The Context API provides a way to share data across the component tree, without the need to pass props down manually at every level.
- It allows you to define a global state that can be accessed by any component that is a descendant of the provider component.
- The Context API consists of two parts: the provider and the consumer.
- The provider is a component that wraps the part of the component tree where the context is needed, and the consumer is a component that reads from the context.
- To use the Context API, you first need to create a context object using the createContext() method.
- This creates a context object that has a Provider component and a Consumer component.
- You can then wrap the relevant parts of your component tree with the Provider component and pass in the data you want to share.

**Example:**
```javascript
  import React, { createContext, useState, useContext } from 'react';

  // Create a context object
  const CounterContext = createContext();

  // Create a provider component
  const CounterProvider = ({ children }) => {
    const [count, setCount] = useState(0);

    return (
      <CounterContext.Provider value={{ count, setCount }}>
        {children}
      </CounterContext.Provider>
    );
  };

  // Create a consumer component
  const CounterDisplay = () => {
    const { count } = useContext(CounterContext);

    return <div>The count is {count}</div>;
  };

  // Wrap relevant parts of the component tree with the provider component
  const App = () => {
    return (
      <CounterProvider>
        <CounterDisplay />
      </CounterProvider>
    );
  };
```
**When to Use Each Context APi and When to use Redux?**
**Use Context API When:**
- Your application has a small to moderate amount of state to manage.
- You need to share data like themes, user settings, or localization.
- You want to avoid the complexity of setting up Redux for simple state management.

**Use Redux When:**
- Your application is complex with a lot of shared state across many components.
- You need advanced features like middleware, debugging tools, and time-travel capabilities.
- You require predictable state management with a clear flow of data.


- How do we handle errors that occurs in a react component?
	- Using Error boundaries
- How do we handle asynchronous operation in react component?


**React Fiber:**
- React Fiber is a re-implementation of React's core algorithm, introduced with React 16, to improve its ability to manage component updates and rendering.
- React Fiber is the reconciliation algorithm in React.
- The primary purpose of Fiber is to enable incremental rendering, which breaks down updates into chunks.
- This allows React to pause work on one task, prioritize more important tasks, and resume work later, leading to a more fluid user experience.

**Why was Fiber introduced?**
- Before React Fiber, React used a recursive algorithm that worked synchronously, meaning that any large update would block the browser from rendering, potentially leading to performance issues (e.g., slow UI or frozen pages).
- Fiber allows for asynchronous rendering, enabling React to manage and prioritize multiple tasks simultaneously.
Key Features of React Fiber:
1. Incremental Rendering: React can break down large tasks into smaller chunks and execute them over multiple frames, preventing the UI from becoming unresponsive.
2. Task Prioritization: Tasks are assigned priorities, so React can work on high-priority updates (like user input or animations) first, while low-priority updates can be deferred.
3. Pausing and Resuming: React can pause the rendering of a component tree and resume it later. This ensures that updates don't block critical tasks.
4. Concurrency: Fiber enables concurrent mode, allowing multiple rendering paths to be processed concurrently, further improving performance.

**How Fiber Works:**
- React Fiber introduces a new data structure to keep track of work in progress:
- Fiber Nodes: Each component in React corresponds to a "fiber," which is a JavaScript object representing the component's current state and effects.
- Work Loop: The Fiber scheduler manages which work to perform, using a work loop to break tasks into smaller units. Each unit of work is processed one at a time, yielding back to the browser when necessary.

**Phases in React Fiber:**
- Render Phase (Reconciliation): React calculates what changes need to be made to the UI but doesn’t make them immediately. This phase can be paused or interrupted.
- Commit Phase: Once React has determined the necessary changes, it commits those changes to the DOM. This phase is synchronous and cannot be interrupted.

**Usage:**
- You don’t need to do anything special to use React Fiber—it’s already built into React 16 and above.
- For advanced features like Concurrent Mode, you need to enable it explicitly by using features like ```ReactDOM.createRoot()``` or ```<Suspense>```.

**How React knows which task is on high priority and which is on low priority?**
- React Fiber prioritizes tasks based on the type of update, user interactions, and system performance.
- Types of Priorities:
- React Fiber uses several priority levels to classify work:

1. Immediate Priority: These tasks need to be handled right away, such as updates triggered by user input (e.g., typing in a text box, clicking a button). React processes these tasks first to ensure responsiveness.
2. High Priority: Tasks like animations or transitions that need to run smoothly are treated as high priority. React ensures these are handled quickly to avoid stuttering or freezing during the animation.
3. Normal Priority: Routine updates, like re-rendering components based on data changes (e.g., fetching new data from a server), are classified as normal priority.
4. Low Priority: Tasks that can be deferred without affecting the user experience, such as non-critical background updates.
5. Idle Priority: Tasks that can be handled when the CPU is not busy, such as preloading data or offscreen rendering. These tasks only get executed when there's nothing else important to do.

**Example of Task Prioritization:**
- Immediate priority: A user clicks a button that triggers a UI change.
- React Fiber processes the event handler immediately, updates the state, and schedules a re-render for the affected components with high priority.
- High priority: An animation starts playing.
- React ensures that the animation updates happen smoothly and gives them high priority.
- Low priority: A data-fetching operation in the background completes.
- React waits until more important tasks are done before updating the UI with the new data.

**Task Scheduling with React’s Scheduler:**
- React Fiber includes a built-in scheduler that manages which units of work to process next. The scheduler continuously checks the priority of tasks, handles high-priority tasks first, and yields or pauses work on lower-priority tasks as necessary.
- The scheduler is responsible for ensuring that tasks with shorter deadlines are processed sooner and for deferring tasks that aren’t as urgent.
- This is how React knows when to pause work on low-priority updates and handle more critical work like responding to user inputs.

**React.createElement vs React.cloneElement:**
**React.createElement():**
- Purpose: It's the core function used to create React elements. When using JSX (```<div></div>```), under the hood, JSX is transpiled into React.createElement calls.
- Usage: You use this function directly when you are not using JSX or when you need to create an element programmatically.

**Syntax:**
```javascript
React.createElement(type, [props], [...children])
```

- type: The type of element (e.g., 'div', 'span', or a component).
- props: An object containing properties (attributes) for the element.
- children: Any child elements.

Ex:
```javascript
React.createElement('div', { className: 'container' }, 'Hello World')
```

In JSX, this is equivalent to
```html
<div className="container">Hello World</div>
```

**React.cloneElement():**
- Purpose: This function is used to clone an existing React element and optionally modify its props or children. It's particularly useful when you need to pass down additional props to a child component or element without completely rewriting it.
- Usage: You typically use cloneElement when you have an existing element (such as a child in props.children) and you want to enhance or modify it by adding or changing props.

**Syntax:**
```javascript
React.cloneElement(element, [props], [...children])
```
- element: The existing React element to be cloned.
- props: An object of props to merge or override in the original element.
- children: Optional new children to replace the original children.

Ex:
```javascript
const element = <button>Click me</button>;
const clonedElement = React.cloneElement(element, { className: 'btn-primary' });
```

This would produce:
```html
<button className="btn-primary">Click me</button>
```

**Key Differences:**
**Usage Context:**
- createElement is for creating elements from scratch.
- cloneElement is for copying existing elements and adding/modifying their props or children.

**Typical Use Case:**
- createElement is mainly used when you are rendering elements or components from scratch.
- cloneElement is typically used when you want to pass additional data (e.g., props) to children components without affecting their original structure.


**Elements vs components:**
**Elements**
Definition:
- Elements are the basic building blocks of HTML.
- They are predefined in HTML, and they represent structure on a webpage.
- Each element has a specific purpose and behavior, like displaying text, creating links, embedding images, etc.
Examples: ```<div>, <p>, <a>, <img>, <button> etc.```


- A React element is the smallest building block in React applications.
- It's a plain object describing what you want to appear on the screen.
- React elements are immutable and light, representing DOM elements or components.

**Usage:**
- React elements are used to describe the structure of the UI and are typically returned by components.
- They can represent HTML elements (e.g., ```<div>, <span>, etc.```) or other React components.

- Creation: Elements are created using JSX (or using React.createElement function directly).

Ex:
```javascript
const element = <h1>Hello, world!</h1>;
const element = React.createElement('h1', null, 'Hello, world!');
```
React elements are plain objects like:
```
{
  type: 'h1',
  props: { children: 'Hello, world!' },
  key: null
}
```
- Immutability: Once an element is created, it cannot be changed. To update the UI, you have to create a new element.

**Components:**
- Components are used to create reusable, modular pieces of the user interface.
- Components are higher-level abstractions used primarily in frameworks like React, Angular, Vue, etc.
- A component typically encapsulates both structure (HTML), style (CSS), and behavior (JavaScript) into a single reusable unit.

- Components are functions or classes that return React elements.
- They allow you to split the UI into reusable, self-contained pieces.
- A component can return any number of elements, manage state, handle logic, and interact with other components.

**Types:**

- Function Components: These are simpler, stateless components that are just JavaScript functions. With React Hooks, they can also manage state and side effects.
- Class Components: These are ES6 classes that extend React.Component and can have lifecycle methods and state (though with the rise of hooks, functional components are now more common).

**Unit Testing:**
Ex: Counter App
```javascript
import React, { useState } from 'react';

const CounterApp = () => {
  // Declare state variable 'count' and the function 'setCount' to update it
  const [count, setCount] = useState(0);

  // Function to increment the count
  const increment = () => {
    setCount(count + 1);
  };

  // Function to decrement the count
  const decrement = () => {
    setCount(count - 1);
  };

  // Function to reset the count to zero
  const reset = () => {
    setCount(0);
  };

  return (
    <div style={{ textAlign: 'center', marginTop: '50px' }}>
      <h1>Counter: {count}</h1>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement} style={{ marginLeft: '10px' }}>Decrement</button>
      <button onClick={reset} style={{ marginLeft: '10px' }}>Reset</button>
    </div>
  );
};

export default CounterApp;
```

**Unit test file:**
```javascript
// CounterApp.test.js
import React from 'react';
import { render, fireEvent } from '@testing-library/react';
import '@testing-library/jest-dom/extend-expect';
import CounterApp from './CounterApp';

describe('CounterApp', () => {
  it('renders CounterApp component correctly', () => {
    const { getByText } = render(<CounterApp />);
    
    // Check if initial counter value is 0
    expect(getByText('Counter: 0')).toBeInTheDocument();
  });

  it('increments the counter value', () => {
    const { getByText } = render(<CounterApp />);

    const incrementButton = getByText('Increment');
    
    // Click the increment button
    fireEvent.click(incrementButton);

    // Verify if the counter value is updated to 1
    expect(getByText('Counter: 1')).toBeInTheDocument();
  });

  it('decrements the counter value', () => {
    const { getByText } = render(<CounterApp />);

    const decrementButton = getByText('Decrement');
    
    // Click the decrement button
    fireEvent.click(decrementButton);

    // Verify if the counter value is updated to -1
    expect(getByText('Counter: -1')).toBeInTheDocument();
  });

  it('resets the counter value', () => {
    const { getByText } = render(<CounterApp />);

    const incrementButton = getByText('Increment');
    const resetButton = getByText('Reset');
    
    // Increment first
    fireEvent.click(incrementButton);
    expect(getByText('Counter: 1')).toBeInTheDocument();

    // Click the reset button
    fireEvent.click(resetButton);

    // Verify if the counter value is reset to 0
    expect(getByText('Counter: 0')).toBeInTheDocument();
  });
});
```

**To Simulate user typing:**
```javascript
fireEvent.change(inputElement, { target: { value: 'Hello World' } });
```



**Synthetic Events**
