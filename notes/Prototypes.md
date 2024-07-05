# Prototypes

Everything is an object in JavaScript. It basically means that almost everything is being derived from JS objects.

Try the following code in a browser

```jsx
let arr = [1, 2, 3];
console.log(arr);

// You can use objects or strings too
```

The `console.log()` will print out array elements, their index and the length property but there is also a `[[Prototype]]` object there. It references the `Array` object and display its properties or methods. Scroll to the end and you will see another `[[prototype]]` object referencing the `Object` object. You wouldn’t see another `[[prototype]]` because as I said earlier, everything in JS is derived from Objects.

When we try to access a property or method on any object, JavaScript basically checks for a method in object’s (Array in our case) `[[prototype]]` , if it doesn’t find it there, it goes up into the next `[[prototype]]` and the process continues until `null` is reached.

This is Prototypal Chain.

```jsx
console.log(arr.__proto__.__proto__);
// Logs Object.prototype
```

So this means, we can access array’s methods (Since our example is of arrays) and as well as object’s methods too on an array.

This is Prototypal Inheritance, more on that later.

## So what really is Prototype?

Its an internal property called `[[prototype]]` which is a reference to another object. This reference can be accessed through the `__proto__` property.
Every function in JavaScript, by default, has a `prototype` property, which is an object. When a function is used as a constructor (with the `new` keyword), the created object's `[[Prototype]]` property will be set to the function's `prototype` object.

`Object.prototype` is the top of the prototype chain. All objects inherit properties and methods from `Object.prototype` if they are not found in their own prototype chain.

## Prototypal Inheritance

Lets understand it with an example.

```jsx
const student = {
  name: "ABC",
  enrollment: 123,
};

const teacherAssistant = {
  willPrepareNotes: true,
  willCheckAssignments: false,
};

// student.__proto__ = teacherAssistant; // Old Method

// New Method
Object.setPrototypeOf(student, teacherAssistant);

console.log(student.willPrepareNotes); // true
```

In the example above, we have a student and a teacher assistant. I want the student to be a TA too, this means the student will have the rights of a TA or in other words the properties of a TA. This means that student will inherit the properties of a TA.

To do this, we used `setPrototypeOf` method of `Object` and see, the student can now access the properties of the TA.

## Prototype Injection

In [The new Keyword](newKeyword.md) we used this example

```jsx
const AddCars = function (make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;

  return this;
};

const carOne = new AddCars("Toyota", "Corolla", 2021);
const carTwo = new AddCars("Nissan", "GTR", 2016);

console.log(carOne);
console.log(carTwo);
```

Now, i want to create a method that can display the make, model, and year of the cars. I want to inject this method in the `addCars` prototype, so that we don’t have to create new copies for each instance, we can simply call the method using dot notation.

```jsx
const AddCars = function (make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;

  return this;
};

AddCars.prototype.displayCarDetails = function () {
  console.log(`Make: ${this.make}, Model: ${this.model}, Year: ${this.year}`);
};

const carOne = new AddCars("Toyota", "Corolla", 2021);
const carTwo = new AddCars("Nissan", "GTR", 2016);

console.log(carOne.displayCarDetails());
console.log(carTwo.displayCarDetails());
```

We accessed the prototype of our `addCars` function and injected our own method into it. You can inject your own methods into an array or object too.
