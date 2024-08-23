# Q. Explain `call()`, `apply()`, and `bind()` in JavaScript

### call(), apply(), and bind() are methods used to control the context (this) in which a function is executed.

## Practical Use Cases

- call() and apply() are often used when you want to borrow methods from another object or when you need to pass different contexts dynamically.
- bind() is useful when you need a function to be called later with a specific this context, such as in event handling.

## Code Example

```javascript
let name1 = {
  firstName: "Trupti",
  lastName: "Yadav",
  printInfo: function (city, county) {
    console.log(
      this.firstName + " " + this.lastName + " is from " + city + ", " + county
    );
  },
};

name1.printInfo("Mumbai", "India"); // Output: Trupti Yadav is from Mumbai, India

let name2 = {
  firstName: "John",
  lastName: "Doe",
};

// call()
name1.printInfo.call(name2, "LA", "USA"); // Output: John Doe is from LA, USA

// apply()
name1.printInfo.apply(name2, ["LA", "USA"]); // Output: John Doe is from LA, USA

// bind()
let bindMethod = name1.printInfo.bind(name2, "LA", "USA");
console.log(bindMethod); // Output: [Function: bound printInfo]
bindMethod(); // Output: John Doe is from LA, USA
```

## Explanation

### `call()` Method

- The `call()` method is used to invoke a function with a specific `this` value and individual arguments.
- In the example, `name1.printInfo.call(name2, "LA", "USA")` invokes the `printInfo` method on `name2` with `"LA"` and `"USA"` as arguments.
- This changes the `this` context inside `printInfo` from `name1` to `name2`.

### `apply()` Method

- The `apply()` method is similar to `call()`, but it takes the arguments as an array rather than individually.
- In the example, `name1.printInfo.apply(name2, ["LA", "USA"])` also changes the `this` context to `name2` but expects the arguments to be passed in an array.

### `bind()` Method

- The `bind()` method returns a new function, where the `this` context is bound to the specified object. It does not immediately invoke the function but instead returns a copy with the `this` value fixed.
- In the example, `let bindMethod = name1.printInfo.bind(name2, "LA", "USA")` creates a new function that, when invoked, will call `printInfo` with `name2` as `this` and the specified arguments.

### [Link to live example](https://codepen.io/trupti0406/pen/OJeZpRq)
