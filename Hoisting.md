# Hoisting in JavaScript

### Hoisting is a term used to explain the behavior of variable declarations in your code.

The following table summarizes the results of accessing variables before they are declared.

| Declaration                    | Accessing Before Declaration                               |
| ------------------------------ | ---------------------------------------------------------- |
| `var foo`                      | `undefined`                                                |
| `let foo`                      | `ReferenceError`                                           |
| `const foo`                    | `ReferenceError`                                           |
| `class Foo`                    | `ReferenceError`                                           |
| `var foo = function() { ... }` | `undefined`                                                |
| `function foo() { ... }`       | Normal (both declaration and definition are fully hoisted) |
| `import`                       | Normal                                                     |
