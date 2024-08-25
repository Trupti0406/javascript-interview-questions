# Q: Implement Currying in JavaScript

### Currying is a functional programming technique that involves breaking down a function that takes multiple arguments into a series of functions that each take a single argument. This makes your functions more flexible and reusable, as you can create specialized versions of a function by pre-setting some arguments.

### In web apps, currying can be useful in scenarios like event handling, configuration settings, or when you need to create a series of similar operations but with different initial parameters.

## Example

```javascript
// Using bind()
let multiply = function (x, y) {
  console.log("x:", x);
  console.log("y:", y);
  console.log("Result with bind:", x * y);
};

let multiplyByTwo = multiply.bind(null, 2);
multiplyByTwo(5); // Outputs: x: 2, y: 5, Result with bind: 10

// Using closure
let cMultiply = function (x) {
  return function (y) {
    console.log("cx:", x);
    console.log("cy:", y);
    console.log("Result with closure:", x * y);
  };
};

let cmultiplyByTwo = cMultiply(2);
cmultiplyByTwo(5); // Outputs: cx: 2, cy: 5, Result with closure: 10
```

## Explanation

1. **Using `bind()`**:

   - Here, we have a `multiply` function that takes two arguments `x` and `y`.
   - We create a new function `multiplyByTwo` by binding the first argument (`x`) to `2`.
   - `null` is passed as the first argument to `bind()` because `bind()` expects the first argument to be the `this` value for the new function. Since `multiply` does not rely on `this`, passing `null` effectively ignores the `this` context.
   - When we call `multiplyByTwo(5)`, it automatically uses `2` as the first argument, and `5` as the second.
   - This is a basic example of currying using `bind()`, where the `2` is pre-set.

2. **Using a Closure**:
   - In the closure example, we create a function `cMultiply` that takes `x` as an argument and returns another function that takes `y`.
   - When we call `cMultiply(2)`, it returns a new function that has `2` stored as `x`.
   - Then, calling this new function with `5` multiplies the stored `2` by `5`, giving us the result.
   - This is currying using closures, where each function remembers the argument it was called with.

### [Link to Live Code](https://codepen.io/trupti0406/pen/VwJxoGG)
