# Closures in JavaScript

### Closures in javascript is a fundamental concept that allows function to access variables from it's outer scope even after its outer function has finished executing.

or

### Closures allow a function to "remember" and access variables from its lexical scope even after the outer function has returned.

or

### Function bundled along with it's lexical scope forms a closure.

```javascript
function x() {
  var a = 100;
  return function y() {
    console.log(a);
  };
}
var returnedFunction = x();
returnedFunction();
```

### **Code Explanation**

1. **Function `x`**:

   - The function `x` is defined with a local variable `a`, which is assigned the value `100`.
   - Inside `x`, another function `y` is declared. This function logs the value of `a` to the console.
   - Function `x` **returns** the inner function `y` without executing it.

2. **Function Call `x()`**:

   - When `x()` is called, the following happens:
     - A new execution context is created for `x`, and the variable `a` is defined with the value `100`.
     - The function `y` is returned as a value from `x`, but `x` itself finishes execution and its execution context is popped off the stack.

3. **Storing the Returned Function**:

   - The returned function `y` is assigned to the variable `returnedFunction`.
   - At this point, `returnedFunction` is a reference to the inner function `y`.

4. **Executing `returnedFunction`**:
   - When `returnedFunction()` is called, the function `y` executes.
   - Even though the outer function `x` has already finished execution, the inner function `y` still has access to the variable `a` from `x`'s scope. This is because of **closure**.

## Closure example in react:

Closures are commonly used in React for handling component state and passing functions with pre-bound arguments. Here are a few simple examples that demonstrate closures in React:

### **Basic Counter Example**

Using closures to encapsulate state updates.

```javascript
import React, { useState } from "react";

const Counter = () => {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount((prevCount) => {
      // Closure: prevCount is remembered from its scope
      return prevCount + 1;
    });
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
};

export default Counter;
```

Here, the `setCount` callback function uses a closure to access the previous value of `count` safely.
