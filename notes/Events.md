# Events

Events are actions or occurrences that happen in the browser, which the browser can react to. These can be triggered by the user (e.g., clicking a button, pressing a key) or automatically by the browser (e.g., page load, resizing window).

### Event Handling

Event handling refers to the process of capturing and responding to events. In JavaScript, we use event listeners to handle events. An event listener is a procedure in JavaScript that waits for an event to occur.

### HTML Structure

Here's a simple HTML structure used to demonstrate event handling:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Events</title>
</head>
<body style="background-color: #2F2F2F; color: white;">
    <div>
        Events in JavaScript
        <ul id="langs">
            <li id="cpp">C++</li>
            <li id="js">JavaScript</li>
            <li id="py">Python</li>
        </ul>
    </div>
</body>
<script src="events.js"></script>
</html>

```

### Adding an Event Listener

To add an event listener to an element, use the `addEventListener` method. It requires at least two arguments: the event type and the callback function that will execute when the event occurs.

```jsx
document.getElementById('cpp').addEventListener("click", () => {
    console.log("Child's Event: You clicked C++");
});

document.getElementById('js').addEventListener("click", () => {
    console.log("Child's Event: You clicked JavaScript");
});

document.getElementById('py').addEventListener("click", () => {
    console.log("Child's Event: You clicked Python");
});

```

### Event Delegation

A better approach for handling events is event delegation. This involves adding a single event listener to a parent element instead of multiple listeners to child elements. This is more efficient and manageable.

```jsx
document.getElementById('langs').addEventListener("click", (e) => {
    console.log("Parent's Event: You clicked ", e.target.textContent);
});

```

### Event Propagation

Event propagation defines the path an event takes through the DOM tree. It has two main phases:

1. **Capturing Phase:** The event starts from the root element and travels down to the target element.
2. **Bubbling Phase:** The event starts from the target element and bubbles up to the root element.

By default, events propagate in the bubbling phase.

### Example of Event Bubbling

In the provided code, when clicking on a child element, the event also triggers the parent event due to event bubbling:

```jsx
document.getElementById('langs').addEventListener("click", (e) => {
    console.log("Parent's Event: You clicked ", e.target.textContent);
});

```

### Event Capturing

Event capturing is the opposite of event bubbling. Events travel from the parent element to the child element. To enable event capturing, pass `true` as the third argument to `addEventListener`.

```jsx
document.getElementById('langs').addEventListener("click", (e) => {
    console.log("Parent's Event: You clicked ", e.target.textContent);
}, true);

```

### Stopping Event Propagation

If you want to prevent the event from propagating (bubbling or capturing), use the `stopPropagation` method of the event object.

```jsx
document.getElementById('langs').addEventListener("click", (e) => {
    e.stopPropagation();
    console.log("Parent's Event: You clicked ", e.target.textContent);
}, true);

```

## Events Practice

Take x and y coordinates from `event` object and place a circle there

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body style="background-color: #2f2f2f; color: white;">
    <div id="parent" style="width: 100vw; height: 100vw; position: relative;"></div>

</body>
<script>
    const parentDiv = document.getElementById('parent');
    // Creating a circle
    const circle = document.createElement('div');
    circle.style.width = "100px";
    circle.style.height = "100px"
    circle.style.border = '2px solid white';
    circle.style.borderRadius = '50%';
    circle.style.position = "absolute"

    // We have to place the circle where ever the user clicks
    parentDiv.addEventListener("click", (e) => {
        console.log(e.x, e.y)
        circle.style.transform = `translate(${e.x - 50}px, ${e.y - 50}px)`
        parentDiv.appendChild(circle);
    })
</script>

</html>
```