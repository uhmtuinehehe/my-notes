- [JavaScript Basics](#javascript-basics)
  - [JavaScript principles](#javascript-principles)
    - [Execution Context](#execution-context)
      - [What happens when javascript executes (runs) my code?](#what-happens-when-javascript-executes-runs-my-code)
        - [JavaScript sets up a global execution context.](#javascript-sets-up-a-global-execution-context)

# JavaScript Basics

## JavaScript principles

### Execution Context

#### What happens when javascript executes (runs) my code?

##### JavaScript sets up a global execution context.

This includes the **global object**, the **global variable environment**, and the **global scope**.

**Global object** provides access to global variables and functions. For example, `window` in browsers or `global` in Node.js.

**Global variable environment** stores the global variables declarations and function declarations. It is an internal data structure used by the JavaScript engine to manage these entities. This involves hosting and setting up memory space for variables and functions.

- Hosting is the process of setting up memory space for variables and functions.
  - Variables: Global variables declared using `var` are hoisted, meaning they are created and initialized to `undefined` during this phase. For `let` and `const`, the variable is also hoisted but remains in a "temporal dead zone" until it is initialized.
  - Functions: Function declarations are also hoisted, meaning their definitions are set up during this phase. This allows functions to be called before they are defined in the code.

**Global scope** becomes active once the global variable environment is established and initialized. It determines the visibility and accessibility of global variables and functions. The global scope is where these variables become accessible.

- Consider the following example:

```javascript
var globalVar = "I am a global variable";

function outerFunction() {
  var outerVar = "I am an outer variable";

  function innerFunction() {
    var innerVar = "I am an inner variable";
    console.log(globalVar); // Accessible due to global scope
    console.log(outerVar); // Accessible due to closure
  }

  innerFunction();
}

outerFunction();
```

- In this example:

  - `globalVar` is defined in the global scope and stored in the global variable environment.
  - `outerVar` is defined in the scope of `outerFunction` and is not stored in the global variable environment.
  - `innerVar` is defined in the scope of `innerFunction` and is not stored in the global variable environment.
  - When `innerFunction` accesses `globalVar`, it does so through the global scope, which is managed by the global variable environment.

**Thread of Execution**: The JavaScript engine starts executing the code line-by-line, from top to bottom, in the order it appears. This involves running statements, evaluating expressions, and invoking functions.

**Variable and Function Execution**: As the code runs, variables are assigned values, and functions are executed. The engine also manages scope and closure, handling local and global variables according to their definitions and usage.

**Call Stack Management**: JavaScript uses an execution stack (or call stack) to manage execution contexts. The global execution context is the first to be pushed onto the stack. Each function call creates a new execution context that is pushed onto the stack. When a function completes, its execution context is popped off the stack.

**Event Loop**: JavaScript handles asynchronous operations using the event loop. This manages the execution of callbacks, such as those from `setTimeout`, `fetch`, or event handlers, ensuring they run at the appropriate time.

**Memory Management**: JavaScript periodically performs garbage collection to clean up memory by removing objects that are no longer referenced. This helps to manage memory usage efficiently.
