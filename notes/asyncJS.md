# Asynchronous JavaScript

JavaScript operates on a single thread, meaning it can execute one task at a time. This model is simpler and helps avoid issues related to concurrency, like race conditions.

Synchronous execution means that each operation must complete before the next one starts, which can lead to slow performance if a task takes a long time.

Despite being single-threaded, JavaScript handles asynchronous operations efficiently using the **event loop**. Asynchronous operations include events, promises, and file I/O, among others.

## **The Runtime Environment:**

JavaScript doesn't run in isolation; it requires a runtime environment like a browser or Node.js. The runtime environment provides APIs for performing asynchronous operations, such as `setTimeout`, `XMLHttpRequest`, `fetch`, and I/O operations.

## **Event Loop and Task Queue:**

When an asynchronous operation is called, the JavaScript engine delegates it to the runtime environment. The runtime environment handles the operation and places a callback in the **task queue** once it's complete.

The **event loop** continuously checks the call stack and the task queue. If the call stack is empty, it pushes the next task from the task queue onto the call stack for execution.

## **Microtasks and Macrotasks:**

Asynchronous callbacks are divided into **microtasks** and **macrotasks**.

- **Microtasks** include promises and `MutationObserver` callbacks. They have higher priority and are executed before any macrotask.
- **Macrotasks** include events, timers (`setTimeout`, `setInterval`), and I/O operations.

## **Fetch API and High-Priority Queues:**

The Fetch API can create network requests that are handled asynchronously. The callback for a fetch request is placed in the **microtask queue**, which has higher priority than the macrotask queue.

## Timeouts and Intervals with Example

Consider the following code

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <h1>Background Changer</h1>
    <button class="btn1">Start</button>
    <button class="btn2">Stop</button>
  </body>
  <script src="setTimeOut and setInterval.js"></script>
</html>
```

```jsx
const body = document.querySelector("body");
const startBtn = document.querySelector(".btn1");
const stopBtn = document.querySelector(".btn2");

const changeBGColor = () => {
  const hexCode = "0123456789ABCDEF";
  let color = "#";

  for (let i = 0; i < 6; i++) {
    color += hexCode[Math.floor(Math.random() * 16)];
  }

  body.style.backgroundColor = color;
};

let timeOut = null;
startBtn.addEventListener("click", () => {
  if (!timeOut) {
    timeOut = setTimeout(changeBGColor, 1000);
  }
});

stopBtn.addEventListener("click", () => {
  clearTimeout(timeOut);
  timeOut = null;
});
```

We’re trying to build a continuous BG color changer. Whenever the start button is clicked, the colors should start to change continuously and should stop once the stop button is pressed. The above code works but only once.

You can see, we’ve used `setTimeout` , it takes in two parameters, a callback function and a time in milliseconds. It executes the the function only once after the specified time. We’ve also used `clearTimeout` which stops the execution of callback function passed to `setTimeout` but it has to run before the specified time of `setTimeout`. In our case, BG color changes after 1 second after pressing the start button but only once.

To change the color continuously, we’ve to use `setInterval` method. It is similar to `setTimeout` but it keeps on executing after specified time unless `clearInterval` executes.

```jsx
const changeBGColor = () => {
  const hexCode = "0123456789ABCDEF";
  let color = "#";

  for (let i = 0; i < 6; i++) {
    color += hexCode[Math.floor(Math.random() * 16)];
  }

  body.style.backgroundColor = color;
};

let timeOut = null;
startBtn.addEventListener("click", () => {
  if (!timeOut) {
    timeOut = setInterval(changeBGColor, 1000);
  }
});

stopBtn.addEventListener("click", () => {
  clearInterval(timeOut);
  timeOut = null;
});
```

## Promises

A **Promise** in JavaScript is an object representing the eventual completion (or failure) of an asynchronous operation and its resulting value. Promises allow you to write asynchronous code in a more synchronous-like fashion, avoiding the "callback hell."

### Promise States

A Promise can be in one of three states:

1. **Pending**: Initial state, neither fulfilled nor rejected.
2. **Fulfilled**: The operation completed successfully.
3. **Rejected**: The operation failed.

### Creating a Promise

A Promise is created using the `Promise` constructor:

```jsx
let promise = new Promise((resolve, reject) => {
  // Asynchronous operation
  let success = true;

  if (success) {
    resolve("Operation was successful!");
  } else {
    reject("Operation failed!");
  }
});
```

### Consuming a Promise

To handle the resolved or rejected state of a Promise, we use `.then()` and `.catch()` methods:

```jsx
promise
  .then((result) => {
    console.log(result); // "Operation was successful!"
  })
  .catch((error) => {
    console.log(error); // "Operation failed!"
  });
```

### Chaining Promises

You can chain multiple `.then()` calls to handle a sequence of asynchronous operations:

```jsx
promise
  .then((result) => {
    console.log(result);
    return "Next step";
  })
  .then((nextResult) => {
    console.log(nextResult);
  })
  .catch((error) => {
    console.log(error);
  });
```

### Promise Methods

1. **Promise.all()**

   This method takes an array of Promises and returns a new Promise that resolves when all the input Promises have resolved, or rejects if any of the input Promises reject.

   ```jsx
   let promise1 = Promise.resolve(3);
   let promise2 = 42;
   let promise3 = new Promise((resolve, reject) => {
     setTimeout(resolve, 100, "foo");
   });

   Promise.all([promise1, promise2, promise3]).then((values) => {
     console.log(values); // [3, 42, 'foo']
   });
   ```

2. **Promise.race()**

   This method returns a Promise that resolves or rejects as soon as one of the Promises in the array resolves or rejects.

   ```jsx
   let promise1 = new Promise((resolve, reject) => {
     setTimeout(resolve, 500, "one");
   });

   let promise2 = new Promise((resolve, reject) => {
     setTimeout(resolve, 100, "two");
   });

   Promise.race([promise1, promise2]).then((value) => {
     console.log(value); // "two"
   });
   ```

3. **Promise.allSettled()**

   This method returns a Promise that resolves after all of the given Promises have either resolved or rejected, with an array of objects that each describes the outcome of each Promise.

   ```jsx
   let promise1 = Promise.resolve(3);
   let promise2 = new Promise((resolve, reject) =>
     setTimeout(reject, 100, "error")
   );

   Promise.allSettled([promise1, promise2]).then((results) =>
     results.forEach((result) => console.log(result.status))
   );
   // "fulfilled"
   // "rejected"
   ```

4. **Promise.any()**

   This method returns a Promise that resolves as soon as any of the Promises in the array resolves. If all of the Promises reject, it returns an AggregateError.

   ```jsx
   let promise1 = Promise.reject(0);
   let promise2 = new Promise((resolve) => setTimeout(resolve, 100, "quick"));
   let promise3 = new Promise((resolve) => setTimeout(resolve, 500, "slow"));

   Promise.any([promise1, promise2, promise3])
     .then((value) => {
       console.log(value); // "quick"
     })
     .catch((error) => {
       console.log(error);
     });
   ```

### Error Handling

It is important to handle errors in Promises to avoid unhandled promise rejections:

```jsx
promise
  .then((result) => {
    console.log(result);
    throw new Error("Something went wrong!");
  })
  .catch((error) => {
    console.error("Caught an error:", error.message);
  });
```

## Fetch

The **Fetch API** provides a modern, flexible interface for making HTTP requests to servers from web browsers. It is an improvement over the older XMLHttpRequest and provides a simpler and cleaner way to interact with network resources.

### Basic Fetch Usage

The basic syntax for using fetch is:

```jsx
fetch(url)
  .then((response) => {
    // handle the response
  })
  .catch((error) => {
    // handle the error
  });
```

### Fetching Data from an API

Let's fetch data from a simple API endpoint. For example, we will use the JSONPlaceholder API, which is a free fake online REST API for testing and prototyping.

```jsx
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((response) => {
    if (!response.ok) {
      throw new Error("Network response was not ok");
    }
    return response.json();
  })
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.error("There has been a problem with your fetch operation:", error);
  });
```

## Async/Await

**Async/Await** is a syntactic sugar built on top of promises. It allows you to write asynchronous code in a synchronous manner, making it easier to read and write.

### Basic Usage

1. **async function**: Declares an asynchronous function.
2. **await**: Pauses the execution of the async function, waiting for the promise to resolve.

```jsx
async function fetchData() {
  try {
    const response = await fetch(
      "https://jsonplaceholder.typicode.com/posts/1"
    );
    if (!response.ok) {
      throw new Error("Network response was not ok");
    }
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("There has been a problem with your fetch operation:", error);
  }
}

fetchData();
```
