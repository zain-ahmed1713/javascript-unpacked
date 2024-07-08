# Call Method

In JavaScript, the `call` method is a function that allows you to call a function with a specific `this` value and arguments provided individually.

This can be particularly useful when you want to borrow a method from one object and use it on another object.

## Example

We’ve a constructor function that takes car details

```jsx
const displayCarDetails = function (make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;
};
```

Now, I want another function, that displays bike details but i don’t want to write the “complex logic” again, so i will just call displayCarDetails inside displayBike function

```jsx
const displayBike = function (make, model, year) {
  // Calling displayCarDetails to pass bike details
  displayCarDetails(make, model, year);
};
```

Now lets call these functions

```jsx
const carDetails = new displayCarDetails("Honda", "Civic", 2024);
const bikeDetails = new displayBike("Yamaha", "R1", 2024);
console.log(carDetails);
console.log(bikeDetails);
```

After running, you will notice that carDetails contains the object containing car details, but bikeDetails displays an empty object.

This is because, Every function has it’s own `this` context, displayCarDetails function isn’t aware of displayBike’s `this` context, we’ve to pass it using `call` method.

```jsx
const displayBike = function (make, model, year) {
  displayCarDetails.call(this, make, model, year);
};

const carDetails = new displayCarDetails("Honda", "Civic", 2024);
const bikeDetails = new displayBike("Yamaha", "R1", 2024);
console.log(carDetails);
console.log(bikeDetails);
```

Now everything is working correctly as we’ve passed displayBike’s `this` context to displayCarDetails and it added the values to it.

## Bind

`Bind` method allows us to create a new function which we can execute later with the new `this` context.

Suppose we’ve a button on our form, When the button is clicked, we want our user to register.

```jsx
class Signup {
  constructor(username, password) {
    this.username = username;
    this.password = password;
    this.btn = document.querySelector("button");
  }

  signupUser() {
    console.log(`${this.username} has been registered.`);
  }

  handleClick() {
    this.btn.addEventListener("click", this.signupUser);
  }
}

const userOne = new Signup("Zain", 1234);
console.log(userOne.handleClick());
```

When the button gets clicked, We get **undefined has been registered.** This is happening because the `this` inside the `signUpUser` refers to `<button>` element since it’s event listener calls `signUpUser` method.

To correct the code, we’ve to bind the `this` context of the `Signup` class to the method.

```jsx
class Signup {
  constructor(username, password) {
    this.username = username;
    this.password = password;
    this.btn = document.querySelector("button");

    this.signupUser = this.signupUser.bind(this);
  }

  signupUser() {
    console.log(`${this.username} has been registered.`);
  }

  handleClick() {
    this.btn.addEventListener("click", this.signupUser);
  }
}

const userOne = new Signup("Zain", 1234);
console.log(userOne.handleClick());
```
