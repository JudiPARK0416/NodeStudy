# Working with the Node.js `fs` Module: Callback, Sync, and Promise Styles Compared

In this session, I explored the `fs` (File System) module in Node.js to perform various operations like renaming, reading, writing, and managing folders.

The ability to manipulate files programmatically is a skill you’ll use often in real-world projects—whether it’s handling uploads, managing logs, or automating workflows.

---

## 📂 File Rename: 3 Ways to Do It

### 1. Callback-Based (Asynchronous)

```javascript
fs.rename("./hello.txt", "./world.txt", (error) => {
  if (error) console.error(error);
  else console.log("File renamed successfully");
});
```
### 2. Synchronous
```javascript
try {
  fs.renameSync("./hello.txt", "./world.txt");
} catch (error) {
  console.error(error);
}
```
## ⚠️ Synchronous methods block the entire thread—avoid them in production!

### 3. Promise-Based (Modern)
```javascript
fs.promises
  .rename("./hello.txt", "./world.txt")
  .then(() => console.log("File renamed successfully"))
  .catch(console.error);
```
## 📝 Other File System Operations
### 📄 Read a File
```javascript
fs.promises
  .readFile("./file.txt", "utf8")
  .then((data) => console.log(data))
  .catch(console.error);
  ```
📤 Output: "hello world!hello world! again!"

### 📄 Write to a File
```javascript
fs.promises.writeFile("./file.txt", "hello world!").catch(console.error);
```
💡 This will overwrite existing content.

### ➕ Append to a File
```javascript
fs.promises.appendFile("./file.txt", "hello world! again!").catch(console.error);
```

### 📑 Copy a File
```javascript
fs.promises.copyFile("./file.txt", "./file2.txt").catch(console.error);
```

### 📁 Create a Folder
```javascript
fs.promises.mkdir("sub-folder").catch(console.error);
```

### 📂 Read Directory Contents
```javascript
fs.promises.readdir("./").then(console.log).catch(console.error);
```

## 🧠 Key Takeaways
The fs module is essential for interacting with the file system.
- Synchronous methods (`renameSync`, `readFileSync`, etc.) block the event loop.
- Prefer Promise-based or callback-based methods for non-blocking I/O.
- With `fs.promises`, your code integrates smoothly with async/await syntax.
- These skills are crucial in real-world apps—especially backend and CLI tools.

## 🏥 Paramedic Analogy: Patient Record Management
Let’s imagine handling patient records:

- `readFile` = Reading the patient’s file
- `writeFile` = Creating a new record
- `appendFile` = Adding notes to an existing report
- `copyFile` = Making a backup of the file
- `rename` = Updating the patient’s file label

Synchronous actions?
It’s like all nurses waiting until one single task is done before continuing 😅 — not efficient!