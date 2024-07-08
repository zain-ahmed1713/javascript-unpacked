# Classes

JavaScript is not purely a class based language. Classes are actually a syntactical sugar for working with prototypes and inheritance.

We did something like this before

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
```

This is how things used to happen before ES6. Classes were added in ES6 and made it easy to work with prototypes and inheritance.

Lets change above code into a class

```jsx
class AddCars {
  constructor(make, model, year) {
    this.make = make;
    this.model = model;
    this.year = year;
  }

  displayCarDetails() {
    console.log(`Make: ${this.make}, Model: ${this.model}, Year: ${this.year}`);
  }
}

const carOne = new AddCars("Honda", "Civic", 2024);
carOne.displayCarDetails();
```

## Inheritance

To inherit properties from a parent class, we can use `extends` keyword

```jsx
class AddBike extends AddCars {
  constructor(make, model, year) {
    super(make, model, year);
  }
}

const bikeOne = new AddBike("Yamaha", "R1", 2024);
bikeOne.displayCarDetails();
```

Remember the `call` method?

`super` works on `call` ’s principles behind the scenes.

## Static Props

Static properties are private, No instance of a class can use them.

```jsx
class AddCars {
  constructor(make, model, year) {
    this.make = make;
    this.model = model;
    this.year = year;
  }

  static displayCarDetails() {
    console.log(`Make: ${this.make}, Model: ${this.model}, Year: ${this.year}`);
  }
}

const carOne = new AddCars("Honda", "Civic", 2024);
carOne.displayCarDetails(); // Error: carOne.displayCarDetails is not a function

// Error occurred as displayCarDetails is a static method.
```
