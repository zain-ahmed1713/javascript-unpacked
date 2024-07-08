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
myObj.greet = function () {
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

## Hidden Properties

JavaScript objects can have properties with specific characteristics that determine their behavior. These characteristics, known as property descriptors, include attributes such as `writable`, `enumerable`, and `configurable`. The `Object.getOwnPropertyDescriptors` method can be used to retrieve all property descriptors of an object, and `Object.defineProperty` can be used to modify them.

### Example

Consider the following object

```jsx
const item = {
  name: "Laptop",
  model: "M123",
  price: 100000,
};
```

To view the property descriptors of `item`, use `getOwnPropertyDescriptors` Object method

```jsx
console.log(Object.getOwnPropertyDescriptors(item));

// Output
// {
//   name: {
//     value: 'Laptop',
//     writable: true,
//     enumerable: true,
//     configurable: true
//   },
//   model: {
//     value: 'M123',
//     writable: true,
//     enumerable: true,
//     configurable: true
//   },
//   price: {
//     value: 100000,
//     writable: true,
//     enumerable: true,
//     configurable: true
//   }
// }
```

You can change the behavior of an object by modifying its property descriptors. For example, to modify the `name` property:

```jsx
Object.defineProperty(item, "name", {
  writable: false,
  enumerable: false,
  configurable: false,
});
```

- **writable: false** - The property value cannot be changed.
- **enumerable: false** - The property will not be included in loops or when logging the object.
- **configurable: false** - The property descriptor cannot be changed, and the property cannot be deleted.

Attempting to change the `name` property will have no effect:

```jsx
item.name = "Phone"; // This will not change the value of `name`
console.log(item); // { model: "M123", price: 100000 }
```

The `name` property is not shown because it is not enumerable.
