# Understanding `this` in Node.js: It’s Not Always What You Think

The `this` keyword can be tricky in JavaScript—and even more so in Node.js, where it behaves differently than in the browser.  
In this post, I explored how `this` behaves in various scopes and contexts within Node.js.

## 🧪 Code Example

```javascript
function hello() {
  console.log(this);
  console.log(this === global); // true in global function
}

hello(); // Called in global scope

class A {
  constructor(num) {
    this.num = num;
  }
  memberFunction() {
    console.log("==== class ====");
    console.log(this); // Refers to the instance
    console.log(this === global); // false
  }
}

const a = new A(1);
a.memberFunction();

console.log("==== global ====");
console.log(this); // {}
console.log(this === module.exports); // true
```

## 📚 What I Learned

- In a regular function (outside of a class), this refers to the global object in Node.js (global).
- Inside a class method, this points to the class instance.
- At the top-level of a Node.js module, this refers to module.exports, not the global object.

## 🏥 A Paramedic's Analogy

To make it easier to visualize, let’s compare it to an emergency room:

- Global function’s this
  Like the hospital-wide intercom system—it broadcasts across all departments (global).

- Inside a class
  Think of a specific ambulance team. this refers to that one team working inside their own vehicle (instance).

- At the module level
  It’s like working within a single department. The scope is limited to that file/module only.
