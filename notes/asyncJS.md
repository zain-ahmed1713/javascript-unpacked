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
