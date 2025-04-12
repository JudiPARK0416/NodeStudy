# Deep Dive into Node.js File System: Streams, Compression & Memory Optimization

In this session, I explored how to handle large files efficiently in Node.js using the `fs` module, streams, and compression techniques.  
Understanding the concept of **Streams** is essential in real-world scenarios where performance and memory usage matter—especially in backend systems.

---

## 📄 Standard File Read vs Stream-Based Approach

### `app-file.js`: Read Entire File at Once

```javascript
const beforeMem = process.memoryUsage().rss;

fs.readFile("./file.txt", (_, data) => {
  fs.writeFile("./file2.txt", data, () => {});
  const afterMem = process.memoryUsage().rss;
  console.log(`Consumed memory: ${(afterMem - beforeMem) / 1024 / 1024} MB`);
});
```
🧨 Downside:
Using `readFile()` loads the entire file into memory.
This causes a memory spike, especially with large files!

## 💧 Stream-Based File Handling
### `app-stream.js`: Reading with Stream
```javascript
const readStream = fs.createReadStream("./file.txt");
const data = [];

readStream.on("data", (chunk) => data.push(chunk));
readStream.on("end", () => console.log(Buffer.concat(data).toString()));
```
- Stream processes the file chunk by chunk.
- Much lower memory footprint.

### `app-write.js`: Writing with Stream
```javascript
const writeStream = fs.createWriteStream("./file3.txt");

writeStream.write("hello!");
writeStream.write("world!");
writeStream.end();
```
✅ Streams are excellent for writing logs, handling uploads, and managing large outputs.

## 🌀 Connecting Streams with pipe()
### `app-pipe.js`: Read → Compress → Write
```javascript
const readStream = fs.createReadStream("./file.txt");
const gzip = zlib.createGzip();
const writeStream = fs.createWriteStream("./file4.zip");

readStream.pipe(gzip).pipe(writeStream);
```
- `pipe()` allows chaining multiple stream processes together.
- Intermediate buffers are skipped → more efficient!

## 🧠 Summary Table: What Works Best?
| Method              | Description                     | Memory Efficiency | Use Case               |
|---------------------|----------------------------------|-------------------|-------------------------|
| `readFile`          | Loads entire file                | ❌ Low            | Small file processing   |
| Stream (`read/write`) | Handles data in chunks         | ✅ High           | Large files, servers    |
| `pipe()`            | Chains multiple streams          | ✅✅ Highest       | Compression, transform  |
| `zlib.createGzip()` | Creates a gzip compression stream| -                 | File compression        |

## 🏥 A Paramedic Analogy: Managing Patient Records
Think of this like an emergency room workflow:
- `readFile()` = Pulling an entire patient’s chart at once → overwhelming! 💦
- `Stream` = Reading notes one section at a time → efficient, calm, scalable 👨‍⚕️
- `pipe()` = Sending the chart from the ER → lab → pharmacy in one smooth flow 📄➡️💻➡️📦

