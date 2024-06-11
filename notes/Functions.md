# Functions

### Functions

A function in JavaScript is a block of code designed to perform a particular task, and it is executed when it is invoked (called).

```jsx
function functionName(parameters) {
  // code to be executed
}

```

**Example:**

```jsx
function greet(name) {
  return "Hello, " + name + "!";
}

console.log(greet("Alice")); // Output: Hello, Alice!

```

In this example, `greet` is a function that takes one parameter `name` and returns a greeting message.

**Key Points:**

- **Function Declaration:** The `function` keyword is used to declare a function.
- **Parameters:** Functions can accept zero or more parameters.
- **Return Value:** Functions can return a value using the `return` statement. If no `return` is specified, the function returns `undefined`.
- **Hoisting:** Function declarations are hoisted, meaning they can be called before they are defined in the code.

### Anonymous Functions

Anonymous functions are functions without a name. They are often used as arguments to other functions or assigned to variables.

```jsx
const sayHello = function(name) {
  return "Hello, " + name + "!";
};

console.log(sayHello("Bob")); // Output: Hello, Bob!

```

**Example in Callbacks:**

```jsx
setTimeout(function() {
  console.log("This runs after 2 seconds");
}, 2000);

```

In this example, an anonymous function is passed as a callback to `setTimeout`.

**Key Points:**

- **No Name:** They do not have a name identifier.
- **Use Cases:** Commonly used in situations where a function is used only once, such as event handlers or callbacks.
- **Scope:** They have the same scope rules as named functions.

### 3. Arrow Functions

Arrow functions provide a more concise syntax for writing functions. They are anonymous by nature.

```jsx
const functionName = (parameters) => {
  // code to be executed
};

```

**Example:**

```jsx
const greet = (name) => {
  return "Hello, " + name + "!";
};

console.log(greet("Charlie")); // Output: Hello, Charlie!

```

**Simplified Example (Implicit Return):**

```jsx
const greet = name => "Hello, " + name + "!";

console.log(greet("David")); // Output: Hello, David!

```

In this example, `greet` is an arrow function that takes one parameter `name` and returns a greeting message.

**Key Points:**

- **Concise Syntax:** Arrow functions have a shorter syntax compared to normal functions.
- **Implicit Return:** If the function body contains only one expression, the curly braces and `return` keyword can be omitted.
- **Lexical `this`:** Arrow functions do not have their own `this` context; they inherit `this` from the parent scope. This makes them particularly useful for methods like event handlers, where you want to preserve the context of `this`.

**Comparison with Normal Functions:**

1. **Syntax:**
    
    ```jsx
    // Normal function
    function add(a, b) {
      return a + b;
    }
    
    // Arrow function
    const add = (a, b) => a + b;
    
    ```
    
2. **`this` Context:**
    
    ```jsx
    function Person() {
      this.age = 0;
    
      setInterval(function growUp() {
        this.age++;
      }, 1000);
    }
    
    const p = new Person();
    // `this` inside growUp refers to the global object, not the instance of Person
    
    // Corrected with arrow function
    function Person() {
      this.age = 0;
    
      setInterval(() => {
        this.age++;
      }, 1000);
    }
    
    const p = new Person();
    // `this` inside the arrow function refers to the instance of Person
    
    ```
    
    In the first example, `this` inside `growUp` refers to the global object (or `undefined` in strict mode), not the instance of `Person`. In the corrected version using an arrow function, `this` refers to the instance of `Person`.