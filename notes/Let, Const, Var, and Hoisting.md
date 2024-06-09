# Let, Const, Var, and Hoisting

```jsx
const accountId = 2001;
let accountEmail = "zainahmed1713@gmail.com";
var accountPassword = "12345";

// Can declare variable but not recommended
accountCity = "Lahore";

console.table([accountId, accountEmail, accountPassword, accountCity])
```

`const` is used to declare constants, meaning it’s value cannot be changed after initialization.

`let` and `var` are used to declare variables. It is recommended not to use `var` anymore. `Var` has **function scope**, it means that variables declared with `var` are accessible anywhere in a function while `let` is **block scope**, it means that variables are only accessible within a code block.

Consider the following example:

```jsx
function greet(name) {
    if (name === "Zain") {
        var message = "Hello, " + name;
    }
    console.log(message);

}

greet("Zain");
// output: Hello, Zain
```

Here you can see that variable `message` is declared with `var` inside the `if` ****block but it is still accessible outside the `if` ****block. This is **Function Scope**.

```jsx
function greet(name) {
    if (name === "Zain") {
        let message = "Hello, " + name;
    }
    console.log(message);

}

greet("Zain");
// output: ReferenceError
```

Here, `let` is used and we cannot access the variable outside the `if` ****block. This is **Block Scope**.

Another problem with `var` is **Hoisting**. 

## Hoisting

Hoisting is a concept in JavaScript that affects how variables and functions are declared and accessed in your code. During the creation phase of a function's execution context, JavaScript hoists all variable and function declarations (but not assignments) to the top of their scope. This means the declarations are treated as if they were written at the very beginning, even if they appear later in the code.

Hoisting applies to `var` and while declaring functions and not assigning them to a variable. `Let` and `Const` don’t exhibit hoisting behavior.

```jsx
console.log(message); // Outputs: undefined
var message = "Hello!";
```

Here, `message` is declared with `var`. Even though it's declared after the `console.log`, due to hoisting, the declaration is treated as if it were at the top. So, the variable exists, but its value hasn't been assigned yet, resulting in `undefined`.

```jsx
console.log(message); // Throws: ReferenceError: message is not defined
let message = "Hello!";
```

With `let`, there's no hoisting. Since the declaration is after the `console.log`, the variable doesn't exist yet, causing a `ReferenceError`.

```jsx
greet(); // Works!
function greet() {
console.log("Hello from the function!");
}
```

The function declaration `greet` is hoisted, so you can call it before its actual definition in the code.

```jsx
greet(); // Throws: TypeError: greet is not a function
const greet = function() {
console.log("Hello from the function!");
}
```

Function expressions assigned to variables are not hoisted. Trying to call `greet` before its definition results in a `TypeError`.

Hoisting allows for Backwards Compatibility, which means that older code that relied on hoisting behavior continue to work in modern JavaScript environments.