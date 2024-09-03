# Q. What is Throttling in JavaScript?

### Throttling is a way to manage how often a function gets called, making sure it only runs once every set amount of time, even if an event happens repeatedly. Imagine scrolling through a webpage—each scroll action can trigger the scroll event dozens or even hundreds of times in just a second. Without throttling, this would cause the function linked to the scroll event to run every single time, which can slow things down. Throttling helps by spacing out these function calls, so they happen at steady intervals, keeping things running smoothly and avoiding unnecessary work.

### HTML

```html
<body style="background-color: lightcoral; height: 2000px"></body>
```

### JavaScript (Optimized Solution)

```javascript
let counter = 0;

// Function to log scroll events and increment a counter
const logScroll = () => {
  console.log("Scroll event triggered", counter++);
};

function throttle(fn, limit) {
  let lastFunc; // Holds the ID of the last setTimeout
  let lastRan; // Stores the timestamp of the last execution

  return function (...args) {
    const context = this;

    if (!lastRan) {
      fn.apply(context, args); // If the function has not been executed yet, call it immediately
      lastRan = Date.now();
    } else {
      clearTimeout(lastFunc); // Clear the previous timeout

      lastFunc = setTimeout(() => {
        // Check if the time limit has been reached
        if (Date.now() - lastRan >= limit) {
          fn.apply(context, args);
          lastRan = Date.now(); // Update the lastRan timestamp
        }
      }, limit - (Date.now() - lastRan));
    }
  };
}

// Apply throttling to the scroll event with a 1000ms (1 second) limit
window.addEventListener("scroll", throttle(logScroll, 1000));
```

### Explanation (Potential Questions that can be asked)

1. **Why declare \`lastFunc\` and \`lastRan\` outside the returned function?**

   - Declaring \`lastFunc\` and \`lastRan\` outside the returned function allows them to persist between multiple calls to the throttled function. This way, the function can manage when it was last executed and when it should be called next, ensuring that it only runs at the specified interval.

2. **Why is \`clearTimeout\` needed?**
   - \`clearTimeout\` is used to cancel the previous timeout if the throttled function is called again before the interval expires. This prevents multiple timeouts from accumulating, ensuring the function is executed in a controlled and timely manner.

### Throttling vs. Debouncing

| Feature              | Debouncing                                                                                                      | Throttling                                                                                                            |
| -------------------- | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Definition**       | Delays the function call until the user stops triggering the event for a specified delay.                       | Limits the function execution to once every specified interval, regardless of event frequency.                        |
| **Use Case**         | Useful for scenarios like search bars, where the API call should only be made when the user has stopped typing. | Ideal for events like window resizing, scrolling, or button clicks where constant function execution could be costly. |
| **Execution**        | Function is called only after the event has stopped firing for the specified delay.                             | Function is guaranteed to be called once every specified interval, even if the event continues to fire.               |
| **Example Delay**    | Delay of 500ms after the last keypress.                                                                         | Execution at most once every 1000ms.                                                                                  |
| **Common Scenarios** | Typing in a search box                                                                                          | Scrolling, resizing a window.                                                                                         |

### [Link to live example](https://codepen.io/trupti0406/pen/abgRMMQ)
