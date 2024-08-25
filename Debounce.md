# Q. What is Debouncing in JavaScript?

### Debouncing is a technique that controls how often a function is executed. Imagine you're typing in a search box—without debouncing, the search function might try to run on every single keystroke, which can overwhelm the system with too many requests. With debouncing, we wait until the user has stopped typing for a short moment before running the search. This not only reduces unnecessary API calls but also improves performance. Debouncing is also useful in other situations, like when resizing a window or scrolling, where we only want to take action after the user has finished their interaction.

### HTML

```html
<input type="text" onkeyup="debouncedData()" />
```

### Javascript(without apply method)

```javascript
let counter = 0;

// Function simulating an API call on search input
const getData = () => {
  console.log("Fetching data...", counter++);
};

const debounce = function (fn, delay) {
  let timer;
  return function () {
    clearTimeout(timer);
    timer = setTimeout(() => {
      fn();
    }, delay);
  };
};

const debouncedData = debounce(getData, 500);
```

### Javascript(Most optimal solution)

```javascript
let counter = 0;

// Function simulating an API call on search input
const getData = () => {
  console.log("Fetching data...", counter++);
};

const debounce = function (fn, delay) {
  let timer;
  return function (...args) {
    const context = this;
    clearTimeout(timer);
    timer = setTimeout(() => {
      fn.apply(context, args);
    }, delay);
  };
};

const debouncedData = debounce(getData, 500);
```

### Explanation(Potetial questions that can be asked)

1. **Context (`this` Binding):**

   - `const context = this;` captures the `this` context from the function call. This is important when the function being debounced is a method of an object and relies on `this` to refer to that object.

2. **Arguments (`args`):**

   - The `...args` syntax captures all arguments passed to the debounced function. These arguments are stored and later passed to the original function when the timeout expires.

3. **Using `apply`:**

   - `fn.apply(context, args);` calls the original function (`fn`) with the correct `this` context (`context`) and the arguments (`args`). This makes the debounce function more flexible and capable of handling more complex cases.

4. **Why declare `timer` outside the returned function?**

   - Declaring `timer` outside the returned function allows it to persist between multiple calls to the debounced function. This way, we can clear the previous timeout and set a new one each time the function is invoked, ensuring that the debounced function only runs after the specified delay has passed without new calls.

5. **Why is `clearTimeout` needed?**
   - `clearTimeout` is used to cancel the previous timeout if the debounced function is called again before the delay expires. Without it, multiple timeouts would accumulate, potentially causing the function to be executed multiple times, which could negate the benefits of debouncing.

### [Link to live example](https://codepen.io/trupti0406/pen/RwzyWwK)
