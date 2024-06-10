# Objects

Objects are fundamental data structures in JavaScript that allow you to store collections of key-value pairs. These keys (also called properties) act like unique identifiers for the associated values, which can be of various data types, including strings, numbers, boolean, arrays, and even other objects. Objects provide a powerful way to model real-world entities and their attributes.

## **Creating Objects**

- **Object Literal Syntax (Recommended):**
This is the most concise and common way to create objects:
    
    ```jsx
    const myObj = {
        name: "Zain",
        location: "Lahore",
        email: "zainahmed1713@gmail.com",
        favFood: ["Biryani", "Steak"]
    };
    
    ```
    

## **Accessing Object Properties**

- **Dot Notation:** You can access properties using dot notation (`.`) after the object variable name:
    
    ```jsx
    console.log(myObj.name); // Output: "Zain"
    console.log(myObj.favFood[0]); // Output: "Biryani" (accessing first element of favFood array)
    
    ```
    
- **Bracket Notation:** Bracket notation (`[]`) allows for more dynamic property access:
    - When the property name is a string or contains special characters:
        
        ```jsx
        const mySymbol = Symbol("sym1");
        myObj[mySymbol] = "zzz";
        console.log(myObj[mySymbol]); // Output: "zzz"
        
        ```
        
    - When you need to construct property names dynamically:
        
        ```jsx
        const userId = 123;
        const userProp = `user_${userId}`;
        myObj[userProp] = "data";
        console.log(myObj[userProp]); // Output: "data"
        
        ```
        

## **Modifying Objects**

Objects are mutable, meaning you can change their properties after creation:

```jsx
console.log("Original Object:", myObj);
myObj.name = "Hamza";
console.log("Modified Object:", myObj);
```

## **Adding Methods to Objects**

Objects can also hold functions (methods) as properties:

```jsx
myObj.greet = function() {
    console.log(`Hello, ${this.name}`); // `this` refers to the current object
};
console.log(myObj.greet()); // Output: "Hello, Hamza" (assuming name was changed)

```

## **Object De-structuring**

Object de-structuring provides a concise syntax to extract properties from objects and assign them to variables:

```jsx
const { name, location } = myObj;
console.log(name, location); // Output: "Hamza", "Lahore"

const { email: e } = myObj; // Aliasing a property name
console.log(e); // Output: "zainahmed1713@gmail.com"

```

## **Beyond the Basics:**

- **Nested Objects:** Objects can contain other objects as properties, creating hierarchical data structures.
- **Prototypal Inheritance:** Objects inherit properties and methods from a prototype chain, allowing for code reuse and object hierarchy.
- **`Object.freeze()`, `Object.seal()`, and `Object.preventExtensions()`:** Methods to control object mutability.
- **Getters and Setters:** Special functions to customize property access and modification.