---
title: 📘 Events in NodeJS
---

# 📘 What Are Events in Node.js and Why Are They Important?

> Section 3 : Vid 24

## What Are Events in Node.js?

- Node.js follows an **event-driven architecture** → actions (events) trigger responses.
- Events are managed using the **`EventEmitter` class** from the `events` module.
- Works like a **Publisher–Subscriber (Pub-Sub) model**:

  - **Publisher (Emitter)** → emits an event.
  - **Subscriber (Listener/Handler)** → responds when the event is triggered.

📍 **Analogy**:

- Amazon delivery → ringing the bell = event emitted.
- User opening door = event listener responds.

## Why Use Events?

- Enables **asynchronous programming** without callback hell.
- Used heavily in **real-time applications**:

  - Chat apps
  - Notifications
  - Streams

- Core Node.js modules (`fs`, `http`, `stream`) are **built on events internally**.

## How Events Work (Step-by-Step)

1. **Event Emitter** → creates & emits events.
2. **Event Listeners** → functions attached to events.
3. When an event is emitted → matching listener(s) are invoked.
4. Listeners can be:

   - **Multi-callable** (can run multiple times).
   - **Single-callable** (runs only once).

## Example: Using EventEmitter

```js
const EventEmitter = require("events");
const emitter = new EventEmitter();

// Register a listener
emitter.on("orderPlaced", (product) => {
  console.log(`Order received for: ${product}`);
});

// Emit an event
emitter.emit("orderPlaced", "Laptop");
```

**Output:**

```
Order received for: Laptop
```

## ✅ Key Takeaways

- Events = **backbone of Node.js asynchronous architecture**.
- Follow a **Pub-Sub model** (emit → listen → respond).
- Used by **core modules** (`fs`, `http`, `stream`).
- Foundation for **real-time apps** (chat, notifications, sockets).

---
