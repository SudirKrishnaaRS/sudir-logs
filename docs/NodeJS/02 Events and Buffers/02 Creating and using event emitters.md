---
title: 📘 Creating and Using Event Emitters
---

# 📘 Creating and Using Event Emitters in Node.js

> Section 3 : Vid 25

## What Are Event Emitters?

- Events in Node.js are handled using the **EventEmitter class** from the `events` module.
- Event Emitters allow us to:

  - **Define custom events**
  - **Attach listeners (callbacks)**
  - **Emit events with optional data**

## Step 1: Import EventEmitter

```js
const EventEmitter = require("events");
```

- Comes **built-in with Node.js** (no need to install).
- `EventEmitter` is a class → we create instances from it.

## Step 2: Create an Instance

```js
const eventEmitter = new EventEmitter();
```

- Use `new` keyword → creates a **fresh eventEmitter object**.

## Step 3: Define and Listen to an Event

```js
eventEmitter.on("greet", (username) => {
  console.log(`Hello ${username}, welcome to events in Node.js!`);
});
```

- **`.on(event, listener)`** → attaches a listener to an event.
- Listener is just a **callback function**.

## Step 4: Emit an Event

```js
eventEmitter.emit("greet", "Sudir");
```

- **`.emit(event, [args...])`** → triggers the event, optionally passing data.

**Output:**

```
Hello Sudir, welcome to events in Node.js!
```

---

## Passing Data with Events

- You can pass strings, numbers, objects, etc.

```js
eventEmitter.emit("greet", "Chai");
```

**Output:**

```
Hello Chai, welcome to events in Node.js!
```

---

## Scenario 1: Run Listener Only Once

```js
eventEmitter.once("pushNotify", () => {
  console.log("This notification runs only once!");
});

eventEmitter.emit("pushNotify"); // Works ✅
eventEmitter.emit("pushNotify"); // Ignored ❌
```

- Use **`.once()`** when you want a listener to execute **only once** (e.g., new user joined chat).

---

## Scenario 2: Remove a Listener

```js
const myListener = () => console.log("Test event triggered");

eventEmitter.on("test", myListener);
eventEmitter.emit("test"); // Runs ✅

eventEmitter.removeListener("test", myListener);
eventEmitter.emit("test"); // Nothing happens ❌
```

---

## Scenario 3: Multiple Listeners for the Same Event

```js
eventEmitter.on("greet", (user) => console.log(`Hello ${user}`));
eventEmitter.on("greet", (user) => console.log(`Hola ${user}`));

eventEmitter.emit("greet", "Node.js");
```

**Output:**

```
Hello Node.js
Hola Node.js
```

- Multiple listeners can respond to the same event.

---

## Scenario 4: Using EventEmitter with Classes

```js
const EventEmitter = require("node:events");

class Greet extends EventEmitter {
  constructor() {
    super();

    // Register event listeners inside constructor
    this.on("greet", (name) => {
      console.log(`Hello, ${name}`);
    });

    this.on("greet", () => {
      console.log("Thanks for your visit");
    });
  }

  // Method to emit the event
  sendMessage(name) {
    this.emit("greet", name);
  }
}

const visitorGreet = new Greet();
visitorGreet.sendMessage("Sudir");
```

**Output:**

```
Hello, Sudir
Thanks for your visit
```

---

## Scenario 5: Handling Errors with Events

```js
const EventEmitter = require("events");
const eventEmitter = new EventEmitter();

eventEmitter.on("error", (err) => {
  console.error("Error occurred:", err.message);
});

eventEmitter.emit("error", new Error("Something went wrong"));
```

- If no **`error` listener** exists → Node.js will **crash**.
- Always handle errors properly in large applications.

---

## Useful EventEmitter Methods

| Method                             | Description                                |
| ---------------------------------- | ------------------------------------------ |
| `.on(event, listener)`             | Attach a listener (can run multiple times) |
| `.once(event, listener)`           | Attach a listener that runs only once      |
| `.emit(event, [args])`             | Trigger an event                           |
| `.removeListener(event, listener)` | Remove a specific listener                 |
| `.listeners(event)`                | Returns an array of listeners for an event |
| `.listenerCount(event)`            | Returns number of listeners attached       |
| `.eventNames()`                    | Get all registered event names             |

---

## ✅ Key Takeaways

- **EventEmitter is the backbone** of Node.js’ event-driven architecture.
- Use `.on` for regular listeners, `.once` for single-use listeners.
- You can pass data when emitting events.
- Always handle **errors** with an `error` listener.
- EventEmitter works **directly or via classes** for structured design.
- Multiple listeners can listen to the same event.
- Use `.removeListener` to clean up event handlers and prevent memory leaks.

---
