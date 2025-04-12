# Exploring the `global` Object in Node.js

Recently, I experimented with the `global` object in Node.js. Although it doesn't show up frequently during regular development, it's quite handy when dealing with variables or functions that need to be accessible in a global context.

## 🧪 Code Example

```javascript
const fs = require("fs");
console.log(global);

global.hello = () => {
  console.log("Hello"); // Explicit use of global
  global.console.log("Hello"); // Same effect
};

global.hello(); // Calling with global
hello();        // Calling implicitly (still works)
```

## 📚 What I Learned
- global in Node.js is similar to the window object in the browser environment.
- By assigning a function like global.hello = () => {}, it becomes globally accessible throughout your app.
- global.console.log and just console.log work the same—because console is itself a global object.
- By printing global, we can observe the full structure of the Node.js global scope.

## 🏥 A Paramedic’s Analogy 
Think of global as a hospital-wide announcement system.
When you register a function like hello() globally, it's like sending a message over the intercom:
"Hello!" echoes throughout the entire hospital, accessible to any department or team—no matter where they are. 📣