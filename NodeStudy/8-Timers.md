# Mastering Node.js Timers: Understanding the Event Loop & Async Execution

In this exercise, I explored some of the most common timer functions in Node.js—including `setTimeout`, `setInterval`, `setImmediate`, and `process.nextTick`.  
I tested their behavior to understand when and how each of them gets executed within the Node.js event loop.

---

## ⏱ Exercise 1: Controlling Repeated Execution with `setInterval` and `setTimeout`

### 📄 `app.js`

```javascript
let num = 1;

const interval = setInterval(() => {
  console.log(num++); // Prints every 1 second
}, 1000);

setTimeout(() => {
  console.log("Timeout");
  clearInterval(interval); // Stops interval after 6 seconds
}, 6000);
```

## 🧠 What I Learned

- setInterval() schedules a callback repeatedly after a specified delay.
- setTimeout() runs a callback once after a delay.
- You can combine both: use setTimeout to stop a running interval.

## 🩺 Analogy

Think of this like monitoring a patient's vital signs every second, and then stopping the observation after 6 seconds.

## 🧪 Exercise 2: Execution Order in the Event Loop

### 📄 app2.js

```javascript
console.log("code1");
console.time("timeout 0");

setTimeout(() => {
  console.timeEnd("timeout 0");
  console.log("setTimeout 0");
}, 0);

for (let i = 0; i < 100; i++) {
  console.log("for loop");
}
```

## 🧠 What I Learned

- setTimeout(..., 0) does not run immediately. It waits until the current call stack is clear.
- The for loop executes first, then setTimeout() runs.
- console.time() and console.timeEnd() can measure the actual delay.

## 🩺 Analogy

It’s like telling a nurse, “Please chart this right away,” but she has to finish recording the current patient’s data first.
Even “right away” must wait for ongoing tasks to finish!

## 📌 Bonus Concept Summary

| Function             | Priority / When It Runs                              |
| -------------------- | ---------------------------------------------------- |
| `process.nextTick()` | Before any other async callbacks (highest priority)  |
| `setTimeout()`       | After the current task in the event queue            |
| `setImmediate()`     | After the I/O events, may run before `setTimeout(0)` |
