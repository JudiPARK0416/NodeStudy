# Understanding Node.js Module System: `exports` vs `module.exports`

In this session, I explored how module exports work in Node.js—specifically, the difference between `exports` and `module.exports`.  
Instead of just memorizing the theory, running some real code helped me understand how things behave under the hood.

---

## 🧪 Code Structure

### 📄 `counter.js`

```javascript
let count = 0;

function increase() {
  count++;
}

function getCount() {
  return count;
}

module.exports.getCount = getCount;
exports.increase = increase;

console.log(module.exports === exports); // true
exports = {}; // Breaks the reference
console.log(module.exports === exports); // false
exports.increase = increase; // Won’t be exported!
```

### 📄 app.js

```javascript
const counter = require("./counter");

counter.increase(); // May fail if not exported properly
console.log(counter.getCount()); // 1

console.log(module); // Inspect the module object
```

## 📚 Key Takeaways

- exports is simply a reference to module.exports at the beginning.
- Doing exports.foo = ... is functionally the same as module.exports.foo = ....
- But reassigning exports = {} breaks the reference—and Node.js won’t export it.
- ✅ To avoid confusion or bugs, it’s safest to use module.exports directly when exporting anything.

## 🏥 Emergency Room Analogy

Let’s say you're working in a hospital:

- module.exports is like the official medical documentation team.
- exports is the administration staff working with them.
- As long as the administration continues filling out the shared report, everything works.
- But if they decide, “We’re making our own system” (exports = {}), the actual report (module.exports) remains empty—and that breaks everything! 😅
