# Using ES6 `import/export` Modules in Node.js

In this session, I explored how to use the modern ES6 module system in Node.js instead of the traditional CommonJS approach (`require` and `module.exports`).  
I’ve mostly used `require` so far, so this was a great chance to understand how `import` and `export` work—and how they're different.

---

## 🧪 Sample Code

### 📄 `counter.js`

```javascript
let count = 0;

export function increase() {
  count++;
}

export function getCount() {
  return count;
}
```
### 📄 app.js
```javascript
// Option 1: Destructured import
import { increase, getCount } from "./counter.js";

increase();
increase();
increase();
console.log(getCount()); // 3

// Option 2: Import everything as a module object
import * as counter from "./counter.js";

counter.increase();
counter.increase();
counter.increase();
console.log(getCount()); // 3
```
### 📄 package.json
```json
{
  "type": "module"
}
```
✅ By setting "type": "module" in package.json, we enable ES6 module support in Node.js.

## 📚 Key Takeaways
- ES6 import/export syntax is clean, declarative, and works great with tree-shaking.
- You must specify `"type": "module"` in your `package.json` to enable ES6 module syntax in Node.js.
- Two ways to import:
    - `import { func } from "./file.js"` → pull specific exports
    - `import * as module from "./file.js"` → bring in everything under a single namespace

## 🏥 A Paramedic's Analogy
Here’s how I think of it as a Paramedic:
- `export` is like extracting important data from a report to share with another department.
- `import` is like using that data on-site in the ER to treat a patient.
- `import * as counter` brings the entire report, while `import { increase }` grabs only the exact data you need.

