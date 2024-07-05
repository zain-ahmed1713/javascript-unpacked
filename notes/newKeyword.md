# The new Keyword

In JavaScript, which isn't a strictly object-oriented language, constructors and the `new` keyword provide a mechanism to create objects with specific properties and behaviors.

## **Constructors:**

A constructor function is a special type of function that serves as a blueprint for creating objects. It typically starts with a capital letter to distinguish it from regular functions. When called with the `new` keyword, it performs specific actions to create a new object.

## **The `new` Keyword:**

- The `new` keyword is used before a constructor function call to:

  - Create a new empty object.
  - Set the object's internal prototype to the constructor's prototype property
  - Execute the constructor function with the newly created object as the `this` context. This allows the constructor to initialize the object's properties.

  ## Example

  Suppose we've the following object

  ```jsx
  const car = {
    make: "Honda",
    model: "Civic",
    year: 2024,
  };
  ```

  Now if we want to add a new car, we would have to create another object. A better approach is to create a constructor function

  ```jsx
  const AddCars = function (make, model, year) {
    this.make = make;
    this.model = model;
    this.year = year;

    // We know that in node.js environment, this refers to an empty global object, whereas in a browser environment
    // this refers to the global window object
    // So, what we are doing is, that we are adding the arguments into the global this object

    return this; // Not necessary to return this
  };
  ```

  Since our function `AddCars` is a constructor function, we've to use `new` keyword to create a new instance of the object on every call or else subsequent function calls will override the values in the global object

  ```jsx
  const carOne = new AddCars("Toyota", "Corolla", 2021);
  const carTwo = new AddCars("Nissan", "GTR", 2016);

  console.log(carOne);
  console.log(carTwo);
  ```
