# 📘 Node.js vs Browser JavaScript Engines: Key Differences

> Section 1 : Vid 2

## 1. Environment

- **Browser JavaScript** → Runs inside a browser, has access to **DOM & Web APIs**.
- **Node.js** → Runs on server/CLI, no DOM or browser window.

## 2. APIs Available

### Browser JS → Web APIs

- `alert()`, `prompt()`, `confirm()`
- `document`, `window` objects
- `fetch()` for HTTP requests
- `setTimeout`, `setInterval` (browser-implemented)

### Node.js → Node APIs

- `fs` (file system), `path`, `crypto`, etc.
- Own implementation of `setTimeout`, `setInterval`
- ❌ No `window`, `document`, `alert`, `fetch` (unless polyfilled)

## 3. Code Compatibility

- **Pure JavaScript features** → ✅ Work in both.
- **Browser-specific code** (DOM, `window`, `alert`) → ❌ Not in Node.js.
- **Node-specific code** (`fs`, `crypto`) → ❌ Not in browser.

## 4. API Reimplementation

- Some APIs like `setTimeout` exist in both:

  - **Browser** → Provided by Web API.
  - **Node.js** → Implemented by Node internally for CLI/server use.

## 📊 Comparison Table

| Feature / API                | Browser JS ✅    | Node.js ✅                                     |
| ---------------------------- | ---------------- | ---------------------------------------------- |
| DOM (`document`, `window`)   | ✔️ Available     | ❌ Not available                               |
| `alert`, `prompt`, `confirm` | ✔️ Available     | ❌ Not available                               |
| `fetch()`                    | ✔️ Available     | ❌ Not available (needs polyfill / Node-fetch) |
| `setTimeout`, `setInterval`  | ✔️ Web API       | ✔️ Node.js internal                            |
| File system (`fs`)           | ❌ Not available | ✔️ Available                                   |
| Cryptography (`crypto`)      | ❌ Not available | ✔️ Available                                   |
| HTTP server creation         | ❌ Not available | ✔️ Available                                   |

✅ **Key Takeaways**

- **JavaScript language = same** everywhere.
- What differs is **environment APIs**.
- **Browser** → DOM, UI, Web APIs.
- **Node.js** → System-level features (files, network, crypto).

---
