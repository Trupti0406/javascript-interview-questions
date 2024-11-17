# **Q. What are callbacks and callback functions in JavaScript?**

### A **callback** is a function that is passed as an argument to another function, and it is executed after the completion of that function. Callback functions allow asynchronous behavior in JavaScript, enabling tasks like API calls, reading files, or interacting with databases without blocking the execution of the rest of the code.

Example:

```javascript
function fetchData(callback) {
  setTimeout(() => {
    console.log("Data fetched!");
    callback(); // Invoke the callback function after the task is complete
  }, 1000);
}

function displayData() {
  console.log("Displaying data!");
}

fetchData(displayData);
```

Here, `displayData` is a callback passed to `fetchData`. It gets executed after `fetchData` finishes fetching the data.

### **Pros of Callbacks:**

1. **Asynchronous Programming:** Callbacks allow non-blocking operations, enabling JavaScript to handle multiple tasks efficiently.
2. **Modular Code:** Functions can be passed and reused, promoting code reusability and separation of concerns.
3. **Customizable Behavior:** Callbacks provide a way to specify what should happen once a task is completed, adding flexibility to the code.

### **Cons of Callbacks:**

1. **Callback Hell:** Nesting multiple callbacks can make the code difficult to read and maintain.
   ```javascript
   asyncOperation1(() => {
     asyncOperation2(() => {
       asyncOperation3(() => {
         console.log("Task complete!");
       });
     });
   });
   ```
2. **Error Handling:** Managing errors in nested callbacks can become tricky and cumbersome.
3. **Tight Coupling:** Passing functions as arguments might create dependencies between different parts of the code.

**How to Avoid the Cons?**

1. **Use Promises:** Promises simplify asynchronous code by chaining `.then()` calls instead of nesting callbacks.
   ```javascript
   asyncOperation1()
     .then(() => asyncOperation2())
     .then(() => asyncOperation3())
     .catch((error) => console.error(error));
   ```
2. **Async/Await:** This syntax makes asynchronous code appear more synchronous and readable.
   ```javascript
   async function performOperations() {
     try {
       await asyncOperation1();
       await asyncOperation2();
       await asyncOperation3();
       console.log("Task complete!");
     } catch (error) {
       console.error(error);
     }
   }
   ```
3. **Proper Error Handling:** Use centralized error handling mechanisms, such as `try-catch` with async/await or `.catch()` with Promises.
