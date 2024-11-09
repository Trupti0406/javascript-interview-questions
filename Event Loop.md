# Understanding the JavaScript Event Loop

The **event loop** is a concept within the browser runtime environment that defines how asynchronous operations are managed and executed in JavaScript engines.

### Step-by-Step Breakdown

1. **Initial Execution**

   - The JavaScript engine begins by executing scripts, placing **synchronous operations** on the **call stack**.

2. **Handling Asynchronous Operations**

   - When an asynchronous operation is encountered (e.g., `setTimeout()`, HTTP request), it is offloaded to the respective **Web API** (or **Node.js API** in a Node environment) to handle in the background.

3. **Queues for Callback Functions**

   - Once the asynchronous operation completes, its callback function is placed into one of two queues:

     - **Task Queue (Macrotask Queue)**: Handles web APIs like `setTimeout()`, HTTP requests, UI events like clicks and scrolls.
     - **Microtask Queue**: Handles promise callbacks (`then`, `catch`, `finally`, `await`operations)

4. **Event Loop Processing**

   - The **event loop** continuously checks the **call stack**. When the call stack is empty:

     1. **Microtask Queue Processing**
        - The event loop processes the **microtask queue** first. It takes the first callback in the microtask queue, pushes it to the call stack, and executes it. This process repeats until the microtask queue is empty.
     2. **Macrotask Queue Processing**
        - After the microtask queue is empty, the event loop processes the **macrotask queue**. It takes the first callback from the macrotask queue, adds it to the call stack, and executes it.
        - **Re-check Microtask Queue**: After each macrotask, the event loop checks the microtask queue again. If any new microtasks were added, it processes them before returning to the next macrotask.

   - This prioritization ensures that **microtasks are always processed before macrotasks**, even if a macrotask adds new microtasks.

5. **Continuous Cycle**
   - This process runs indefinitely, allowing JavaScript to handle synchronous and asynchronous operations efficiently without blocking the call stack.

### The best video explanation I have come across EVER: [Event Loop by Lydia Hallie](https://www.youtube.com/watch?v=eiC58R16hb8)
