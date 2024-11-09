# Differences Between `let`, `var`, and `const` in JavaScript

In JavaScript, `let`, `var`, and `const` are keywords used to declare variables.

They differ significantly in terms of scope, initialization rules, redeclaration, reassignment, and behavior when accessed before declaration.

| Behavior                         | var                | let              | const            |
| -------------------------------- | ------------------ | ---------------- | ---------------- |
| **Scope**                        | Function or Global | Block            | Block            |
| **Initialization**               | Optional           | Optional         | Required         |
| **Redeclaration**                | Yes                | No               | No               |
| **Reassignment**                 | Yes                | Yes              | No               |
| **Accessing before declaration** | `undefined`        | `ReferenceError` | `ReferenceError` |
