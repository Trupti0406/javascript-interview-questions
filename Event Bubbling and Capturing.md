# Q. What is Event Bubbling and Event Capturing in JavaScript?

In JavaScript, when an event (like a click) occurs on an element, it doesn’t just stop there. Instead, it moves through a series of steps known as **event propagation**. Event propagation has two main phases:

## Event Propagation Phases

1. **Capturing Phase**: The event starts from the outermost element and moves down to the target element. This is also called **event capturing**.

2. **Bubbling Phase**(default): After reaching the target element, the event bubbles back up from the target element to the outermost element, which is known as **event bubbling**.

In most cases, events are handled during the bubbling phase by default in JavaScript, but we can control whether an event is handled in the capturing phase by setting an optional parameter.

## Example Scenario: Nested `grand-parent`, `parent`, and `child` divs

```html
<div id="grand-parent">
  <div id="parent">
    <div id="child"></div>
  </div>
</div>
```

corresponding JavaScript to observe event bubbling and propagation.

```javascript
document.querySelector("#grand-parent").addEventListener("click", () => {
  console.log("Grand Parent Clicked!");
});

document.querySelector("#parent").addEventListener("click", (e) => {
  console.log("Parent Clicked!");
});

document.querySelector("#child").addEventListener("click", () => {
  console.log("Child Clicked!");
});
```

## Event Bubbling

If you **click on the `child` div**, the event first triggers the `child`’s event handler, then "bubbles up" to the `parent`, triggering the `parent`’s event handler, and finally to the `grand-parent`, triggering its event handler.

The console output would look like this:

```
Child Clicked!
Parent Clicked!
Grand Parent Clicked!
```

## Capturing Phase (Event Capturing)

If we want to handle the event in the capturing phase (before the bubbling phase), we can pass a third argument as `true` to the event listener.

```javascript
document.querySelector("#grand-parent").addEventListener(
  "click",
  () => {
    console.log("Grand Parent Clicked!");
  },
  true
);

document.querySelector("#parent").addEventListener(
  "click",
  () => {
    console.log("Parent Clicked!");
  },
  true
);

document.querySelector("#child").addEventListener(
  "click",
  () => {
    console.log("Child Clicked!");
  },
  true
);
```

If you click on the `child` div, the output will be:

```
Grand Parent Clicked!
Parent Clicked!
Child Clicked!
```

Here, the capturing phase completes first (from `grand-parent` down to `child`).

## How to prevent Event propagation `e.stopPropagation()`

The `stopPropagation()` method in JavaScript is used to **prevent further propagation** of the current event in the capturing and bubbling phases.

### Usage of `stopPropagation()`

When you call `event.stopPropagation()` within an event handler, it stops the event from bubbling up to ancestor elements and prevents any further handlers from being executed on those elements.

This is particularly useful in cases where you want to handle an event at a specific element only and avoid the event from unintentionally triggering other handlers on parent elements. For instance:

```javascript
document.querySelector("#child").addEventListener(
  "click",
  (e) => {
    console.log("Child Clicked!");
    e.stopPropagation();
  },
  true
);
```

In this case, if the `child` div is clicked, only the `child`'s handler is executed, while handlers for `parent` and `grand-parent` are ignored.

## Summary

- **Event propagation** includes both capturing and bubbling phases.
- **Event bubbling** is the default behavior where events bubble up from the target element to its ancestors.
- **Event capturing** occurs from the top-most element down to the target if specified.
- Use `stopPropagation()` to prevent an event from bubbling up or down.

### [Link to live example](https://codepen.io/trupti0406/pen/oNKQQKL)
