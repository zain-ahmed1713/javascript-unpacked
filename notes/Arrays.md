# Arrays

Arrays are fundamental data structures in JavaScript that allow you to store a collection of items under a single variable name. These items can be of various data types, including strings, numbers, boolean, objects, and even other arrays, making them highly versatile.

## **Creating Arrays**

There are two primary ways to create arrays in JavaScript:

1. **Array Literal Syntax:**
This is the most concise and common method:
    
    ```jsx
    const fruits = ["Apple", "Banana", "Orange"]; // Array of strings
    const numbers = [1, 2, 3, 4, 5];           // Array of numbers
    
    ```
    
2. **Array Constructor:**
While less prevalent, you can use the `Array()` constructor to create empty arrays or specify initial elements:
    
    ```jsx
    const vegetables = new Array();    // Empty array
    const mixedArray = new Array(10);  // Array with 10 empty slots (length is 10)
    const allTypes = new Array("hello", 42, true); // Array with mixed data types
    
    ```
    

## **Accessing Array Elements**

- **Zero-Based Indexing:** JavaScript arrays are zero-indexed, meaning the first element resides at index 0, the second at index 1, and so on. To access an element, use its index within square brackets (`[]`) after the array variable name:
    
    ```jsx
    const fruits = ["Apple", "Banana", "Orange", "Mango"];
    const firstFruit = fruits[0]; // firstFruit will be "Apple"
    const lastFruit = fruits[fruits.length - 1]; // Accessing the last element
    
    ```
    
    - **Accessing beyond bounds:** If you try to access an element with an index outside the array's boundaries (less than 0 or greater than or equal to `length`), you'll likely get `undefined`.

## **Array Length**

- **`length` Property:** The `length` property of an array reflects the number of elements it currently holds. It's a dynamic property, meaning it automatically adjusts as elements are added or removed:
    
    ```jsx
    const numbers = [1, 2, 3];
    console.log(numbers.length); // Output: 3
    numbers.push(4, 5); // Adding elements
    console.log(numbers.length); // Output: 5
    numbers.pop(); // Removing the last element
    console.log(numbers.length); // Output: 4
    
    ```
    

## **Common Array Methods**

JavaScript provides a rich set of built-in methods for manipulating arrays. Here are some frequently used ones:

```jsx
arr.push(100);
arr.pop();
console.log(arr.includes(4));
console.log(arr);

// Slice method doesn't includes the end range 
// and doesn't change the original array
const slicedArr = arr.slice(0, 3); 
console.log("Sliced Array: ", slicedArr);
console.log("Original Array: ", arr)

// Splice method includes the end range and changes the original array
const splicedArr = arr.splice(0, 3);
console.log("Spliced Array: ", slicedArr);
console.log("Original Array: ", arr)

// Checks whether the given parameter is an array or not
console.log(Array.isArray("Hello"))

// Creates a new array of given parameters
console.log(Array.of("Hello", "World", 1, 2, 3))

// Creates a new array of given iterable or array like object 
// and can also map a function in 2nd argument and then that 
// function's return value will be added to the array. 
console.log(Array.from([10, 20, 30, "Hello"])) 

```