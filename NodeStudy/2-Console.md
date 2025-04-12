# Exploring Various `console` Methods in Node.js

Today, I explored different `console` methods available in Node.js.  
Beyond just `console.log`, there are multiple options for displaying information in different contexts—each with its own purpose and level of importance.

## 🧪 Code Example

```javascript
console.log("logging...");
console.clear(); // Clears previous console output

// Log levels
console.log("log");       // General log (for development)
console.info("info");     // Informational message
console.warn("warn");     // Warning message
console.error("error");   // Error message

// Conditional output
console.assert(2 === 3, "not same!"); // Will log the message
console.assert(2 === 2, "same!");     // Will not log anything

// Displaying objects
const student = { name: "judy", age: 28 };
console.log(student);       // Default output
console.table(student);     // Tabular format
console.dir(student);       // Detailed view of properties
```

## 📚 Key Takeaways
- console.log, info, warn, and error can be used to categorize log severity or purpose.
- console.assert only prints when the condition is false, making it great for quick debugging.
- For displaying objects:
    - log() is simple and familiar,
    - table() gives a clean, structured look,
    - dir() provides a deep dive into object structure.

## 🏥 A Paramedic's Analogy
Let’s put it in emergency room terms:
- 🧾 console.log → A standard handover note between medical staff
- ⚠️ console.warn → A heads-up: “This patient is showing unusual signs.”
- 🚨 console.error → A full-blown emergency: “Code Blue! Immediate action needed.”
- 🔍 console.assert → Like double-checking: “This patient should have symptom A, but something’s not adding up.”

