# Exploring the `process` Module in Node.js: System Info & Event Loop Order

In this exercise, I explored the built-in `process` module in Node.js to inspect system information and better understand how the event loop works.

The `process` object is essential when you're working with runtime details, system environments, or low-level control over the app's lifecycle.

---

## 🔍 Code Example

```javascript
const process = require("node:process");

console.log(process.execPath);    // Path to Node executable
console.log(process.version);     // Node.js version
console.log(process.pid);         // Process ID
console.log(process.ppid);        // Parent Process ID
console.log(process.platform);    // OS platform
console.log(process.env);         // Environment variables
console.log(process.uptime());    // Process uptime (in seconds)
console.log(process.cwd());       // Current working directory
console.log(process.cpuUsage());  // CPU usage metrics

setTimeout(() => {
  console.log("setTimeout");
}, 0);

process.nextTick(() => {
  console.log("nextTick");
});

for (let i = 0; i < 100; i++) {
  console.log("for loop");
}
```
## 📚 What I Learned
- The `process` object gives access to detailed runtime and system-level information.
- `process.nextTick()` schedules a callback to be executed before any I/O or timer callbacks—even before `setTimeout(..., 0)`.
- `process.cpuUsage()` and `process.uptime()` are useful for monitoring performance metrics.
- `process.env` provides access to environment-specific configurations (like API keys, build environments, etc).

## 🏥 A Paramedic's Analogy: Patient Monitoring System
Let’s compare this to an ER scenario:

- `uptime` → Like checking how long a patient has been in the emergency room.
- `cpuUsage` → How much staff energy or hospital resources are being used for this patient.
- `process.env` → Medical background info: allergies, medications, conditions, etc.
- `nextTick()` → A super-high priority note: “Add this to the chart before anything else happens!”

