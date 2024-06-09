# Primitive & Non-Primitive Types

In JavaScript, data comes in two main flavors: primitive and non-primitive. Understanding these types and how they interact with memory (stack and heap) is crucial for writing efficient and predictable code.

## **1. Primitive Data Types:**

Primitive data types are the basic building blocks of data in JavaScript. They represent simple values and are stored directly on the stack memory. The stack is a Last-In-First-Out (LIFO) data structure, meaning the last value added is the first one accessed.

Here are the primitive data types in JavaScript:

- **Number:** Represents numeric values (e.g., 10, 3.14).
- **String:** Represents sequences of characters (e.g., "Hello").
- **Boolean:** Represents logical values (true or false).
- **Symbol:** (Introduced in ES6) A unique and immutable identifier (e.g., Symbol("mySymbol")).
- **undefined:** Represents a variable that has been declared but not assigned a value.
- **null:** Represents the intentional absence of an object value.

**Key Points about Primitives:**

- **Immutable:** Once created, the value of a primitive cannot be changed. Any modification creates a new primitive value.
- **Stored on Stack:** Primitives are stored on the stack due to their fixed size and simple nature. The stack is faster to access but has limited space.
- **Passed by Value:** When you pass a primitive value to a function, a copy of the value is passed. Changes made to the copy within the function won't affect the original value.

## **2. Non-Primitive Data Types:**

Non-primitive data types, also called reference types, are more complex data structures that hold collections of values or references to other objects. They are stored on the heap memory. The heap is a more dynamic memory allocation system that can grow or shrink as needed.

Here are some common non-primitive data types in JavaScript:

- **Object:** A collection of key-value pairs (properties) used to represent real-world entities or concepts.
- **Array:** An ordered collection of items, accessed by numerical indexes.
- **Function:** A block of code designed to perform a specific task.

**Key Points about Non-Primitives:**

- **Mutable:** The values stored within a non-primitive data type can be changed after creation.
- **Stored on Heap:** Non-primitives are stored on the heap due to their variable size and complex structure. The heap is slower to access but can accommodate larger data structures.
- **Passed by Reference:** When you pass a non-primitive value to a function, a reference (memory address) to the object is passed. Changes made within the function will affect the original object.

## **Understanding Stack and Heap:**

Imagine the stack as a stack of plates: you can only add or remove plates from the top. It's fast and efficient for small, temporary data. The heap is like a large storage room: you can add or remove items from anywhere, but it takes a bit longer to find things.

**In Summary:**

- Use primitives for simple data and calculations.
- Use non-primitives for complex data structures and object-oriented programming.
- Knowing how data types are stored in memory (stack vs. heap) helps you write code that is efficient and avoids memory-related issues.

## Question: I can change the value of a variable declared with `let` How is it immutable then?

**Primitive values in JavaScript are immutable, but variable assignment creates a new reference.**

Consider the following example:

```jsx
let message = "Hello";
message = "World";

console.log(message);
```

In the example:

1. You declare a variable `message` and assign the string value "Hello" to it. This creates a string primitive in memory with the value "Hello".
2. When you assign "World" to `message` again, you're not modifying the original string value "Hello". Instead, you're creating a new string primitive in memory with the value "World".
3. You're then re-assigning the variable `message` to reference this new string primitive.

So, the original string "Hello" remains unchanged in memory, but the variable `message` now points to the new string "World".

**Here's an analogy:**

Imagine `message` as a variable that holds a note. Initially, you write "Hello" on the note and assign it to `message`. Later, you don't erase the original note; instead, you write "World" on a new note and give that new note to `message`. The first note ("Hello") remains unchanged, but `message` now references the new note ("World").

**In summary:**

- Primitive values themselves cannot be modified.
- Assigning a new value to a variable with a primitive value creates a new primitive and reassigns the variable reference.
