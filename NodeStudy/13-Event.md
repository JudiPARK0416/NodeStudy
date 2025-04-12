# Practicing Event-Driven Architecture in Node.js with `EventEmitter`

In this session, I explored the built-in `EventEmitter` class in Node.js by building a simple event-driven system.  
Understanding how to emit and listen for events is crucial not only for internal Node.js operations but also for real-world use cases like **chat apps, logging, and streaming services**.

---

## 🧱 Basic Event Flow

### 📄 `app.js`

```javascript
const EventEmitter = require("events");
const emitter = new EventEmitter();

const callback1 = (args) => {
  console.log("first callback - ", args);
};

emitter.on("judy", callback1);

emitter.on("judy", (args) => {
  console.log("second callback - ", args);
});

emitter.emit("judy", { message: 1 });
emitter.emit("judy", { message: 2 });

emitter.removeAllListeners("judy");
emitter.emit("judy", { message: 3 }); // No listeners now
```
## 🧠 Core Concepts
| Method                                 | Description                                             |
|----------------------------------------|---------------------------------------------------------|
| `on(event, callback)`                  | Register an event listener                              |
| `emit(event, data)`                    | Emit (trigger) an event                                 |
| `removeListener()` / `removeAllListeners()` | Remove specific or all listeners                   |
| *(Note)*                               | Callback references like `callback1` are needed if you want to later remove them. |

## 🔁 Modular Custom Event System
### 📄 logger.js
```javascript
const EventEmitter = require("events");

class Logger extends EventEmitter {
  log(callback) {
    this.emit("log", "started...");
    callback();
    this.emit("log", "ended!");
  }
}

module.exports.Logger = Logger;
```
### 📄 main.js
```javascript
const logger = require("./logger");
const emitter = new logger.Logger();

emitter.on("log", (event) => {
  console.log(event);
});

emitter.log(() => {
  console.log("...doing something");
});
```
## 🧠 Why This Structure Works
- The Logger class emits internal events.
- Other modules can subscribe to those events with on().
- It creates a modular, decoupled architecture using event-driven patterns.

## 🏥 A Paramedic Analogy: Hospital-Wide Announcements
Here’s how I picture it as a Paramedic:
- `emit()` → Like the PA system shouting “Incoming emergency!” 📣
- `on()` → Different departments (ER, Radiology, etc.) respond based on what they hear.
- `removeAllListeners()` → Turning off the broadcast system—no one gets notified. 🙉
- `Logger class` → A structured internal communication system between departments. 📡

## ✅ Summary: When to Use EventEmitter
| Situation                          | Why EventEmitter Helps                              |
|------------------------------------|------------------------------------------------------|
| Complex async flow                 | Simplifies control with event-based architecture     |
| Building notification/state systems | Makes your system modular and reactive              |
| Streaming or network processing    | Node.js core uses this under the hood               |

