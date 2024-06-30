# Filter, Map, and Reduce

## Filter

The `filter` method in JavaScript allows for the creation of a new array containing elements that satisfy a specified condition. It iterates over each element of the array, executing a provided callback function, and returns a new array containing only the elements for which the callback function returns true.

Example:

```jsx
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14];
const evenNums = arr.filter((item) => item % 2 === 0);
console.log(evenNums); // [2, 4, 6, 8, 10, 12, 14]

```

## Map

The `map` method applies a provided function to each element of the array, returning a new array with the results of these function calls. It preserves the original array length and does not mutate the original array.

Example:

```jsx
const arr1 = [2, 4, 6, 8, 10];
const doubleItems = arr1.map((item) => item * 2);
console.log(doubleItems); // [4, 8, 12, 16, 20]

```

## Reduce

The `reduce` method executes a reducer function on each element of the array, resulting in a single output value. It iterates over each element of the array, accumulating a value based on the logic defined in the reducer function. The `reduce` method can optionally accept an initial value for the accumulator.

Example:

```jsx
const prices = [100, 299, 399];
const totalBill = prices.reduce((acc, item) => acc + item, 0);
console.log(totalBill); // 798

```