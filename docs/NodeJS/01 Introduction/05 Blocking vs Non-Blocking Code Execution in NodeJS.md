# 📘 Blocking vs Non-Blocking Code Execution in NodeJS

> Section 2 : Vid 22

## What is Blocking Code?

- **Blocking (synchronous) code** executes **line by line**, and waits until the current operation finishes before moving to the next.
- Example: `fs.readFileSync()` → reads file **synchronously**.

```js
const fs = require("node:fs");

console.log("Start of script");

const content = fs.readFileSync("notes.txt", "utf8");
console.log(content);

console.log("End of script");
```

**Output (order preserved):**

```
Start of script
<File contents here>
End of script
```

- Problem: If file is **large** (e.g., 1GB), it **blocks the entire program** until reading is done.
- In case of a web server, this means **all users are blocked** while one request is being processed.

---

## What is Non-Blocking Code?

- **Non-blocking (asynchronous) code** allows program execution to **continue without waiting**.
- Uses **callbacks, promises, or async/await** to handle results later.
- Example: `fs.readFile()` → reads file **asynchronously**.

```js
const fs = require("node:fs");

console.log("Start of script");

fs.readFile("notes.txt", "utf8", (err, data) => {
  if (err) {
    console.error("Error:", err);
  } else {
    console.log("File contents:", data);
  }
});

console.log("End of script");
```

**Output (order different):**

```
Start of script
End of script
File contents: <data here>
```

- File reading happens **in background**, script execution continues.
- Once file is ready, the **callback function executes**.

---

## Real-World Analogy

- **Blocking (Sync)**: You stand in line at a restaurant until your food is ready. Everyone else behind you must also wait.
- **Non-Blocking (Async)**: You place your order, take a token, and sit down. Others can order while your food is being prepared.

---

## FS Module Example (Sync vs Async)

| Operation        | Blocking (Sync)       | Non-Blocking (Async) |
| ---------------- | --------------------- | -------------------- |
| Read File        | `fs.readFileSync()`   | `fs.readFile()`      |
| Write File       | `fs.writeFileSync()`  | `fs.writeFile()`     |
| Append File      | `fs.appendFileSync()` | `fs.appendFile()`    |
| Delete File      | `fs.unlinkSync()`     | `fs.unlink()`        |
| Create Directory | `fs.mkdirSync()`      | `fs.mkdir()`         |

---

✅ **Key Takeaways**

- **Blocking (Sync)** → waits for operation to finish (not scalable for servers).
- **Non-Blocking (Async)** → executes in background, allows concurrency.
- Every FS method in Node.js has both Sync and Async versions.
- Always prefer **non-blocking (async)** in production (e.g., servers).

---
