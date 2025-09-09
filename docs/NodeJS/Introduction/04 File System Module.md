# 📘 File System (FS) Module to Read, Write and Delete Files

> Section 2 : Vid 21

## What is the FS Module?

- A **built-in Node.js module** for interacting with the file system.
- Provides methods to **read, write, update, delete files and directories**.
- Can be used in both **synchronous (blocking)** and **asynchronous (non-blocking)** ways.

## Importing the Built-in Module (Example: fs)

```js
// Old way
const fs = require("fs");

// Recommended (new way with namespace)
const fs = require("node:fs");
```

- **Why `node:` prefix?**

  - Explicitly marks it as a **core module**.
  - Avoids conflicts with third-party modules of the same name.
  - Convention:

    - `node:fs` → built-in
    - `fs` → could be built-in OR third-party
    - `./file.js` → custom module

## Files

### Reading Files

```js
const fs = require("node:fs");

// Read file synchronously (Sync means blocking the main thread)
const content = fs.readFileSync("notes.txt", "utf8");
console.log(content);
```

- `readFileSync(path, encoding)` → blocking (waits until file is read).
- If encoding is not provided, returns a **buffer**.

### Writing Files

```js
// Overwrites file contents (creates file if it doesn’t exist)
fs.writeFileSync("copy.txt", "Hello World!", "utf8");
```

- Always **overwrites** the file content.
- Use when you want a **fresh write**.

### Appending to Files

```js
fs.appendFileSync("copy.txt", "\nNew Line Added!");
```

- Adds content to the end of the file.
- Previous data remains intact.
- Use `\n` for new lines.

### Copying Files (Read + Write)

```js
const content = fs.readFileSync("notes.txt", "utf8");
fs.writeFileSync("copy.txt", content, "utf8");
```

- Reads from `notes.txt` and writes to `copy.txt`.
- If `copy.txt` exists → it will be overwritten.

### Deleting Files

```js
fs.unlinkSync("copy.txt");
```

- Permanently deletes a file.

## Directory

### Creating Directories

```js
// Create single folder
fs.mkdirSync("games");

// Create nested folders with recursive option
fs.mkdirSync("games/xyz/a", { recursive: true });
```

- `recursive: true` → creates parent folders if they don’t exist.

### Removing Directories

```js
// Remove directory (only works if empty)
fs.rmdirSync("games");

// Must delete inner folders first, like Linux behavior
fs.rmdirSync("food/starters/fries"); // fries is deleted
fs.rmdirSync("food/starters"); // starters is deleted
fs.rmdirSync("food"); // food is deleted
```

- Cannot delete non-empty directories.

### Other Useful FS Methods

- `fs.renameSync(oldPath, newPath)` → Rename/move files.
- `fs.statSync(path)` → Get file info (size, createdAt, etc.).
- `fs.existsSync(path)` → Check if file/directory exists.
- `fs.chmodSync(path, mode)` → Change file permissions.

✅ **Key Takeaways**

- FS module lets Node.js interact with the file system.
- Two styles of methods:

  - **Sync** (blocking, ends with `Sync`) → simpler, but blocks event loop.
  - **Async** (non-blocking, uses callbacks/promises) → preferred for production.

- Key operations:

  - Read: `readFileSync`
  - Write: `writeFileSync`
  - Append: `appendFileSync`
  - Delete: `unlinkSync`
  - Directories: `mkdirSync`, `rmdirSync`

- Use `node:fs` import style in modern Node.js projects.

---
