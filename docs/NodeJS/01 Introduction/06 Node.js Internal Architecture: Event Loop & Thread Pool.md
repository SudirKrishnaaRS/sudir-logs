# 📘 Node.js Internal Architecture: Event Loop & Thread Pool

> Section 2 – Vid 23

### Event Loop

- Core of Node.js execution model.
- Handles incoming requests.
- Decides whether a task is **Blocking** or **Non-Blocking**.

### Event Queue

- Stores tasks/events waiting to be executed.

### Thread Pool (libuv)

- Handles heavy/async tasks (file I/O, DNS lookups, crypto).
- Default size: **4 threads** (configurable).

## Scenarios

### Scenario 1: Blocking Operation (Sync FS)

- Task enters Event Loop.
- `fs.readFileSync` → Event Loop **waits** until finished.
- Other tasks stuck in Event Queue.

📍 **Diagram:**

```
User Req → Event Queue → Event Loop → [Blocking Task] ❌
                   (everything waits)
```

### Scenario 2: Non-Blocking Operation (Async FS)

- Task enters Event Loop.
- Offloaded to **Thread Pool** (via libuv).
- Event Loop continues processing other tasks.
- Once finished → result returned via callback → Event Queue → Event Loop.

📍 **Diagram:**

```
User Req → Event Queue → Event Loop → [Non-Blocking] → Thread Pool → Callback → Event Queue → Event Loop
```

### Scenario 3: Multiple Users (Server Example)

- **Blocking:** One user requests 1GB file → everyone else waits.
- **Non-Blocking:** 1GB file read in background → other users served immediately.

📍 **Diagram:**

- Blocking → ❌ one request chokes server.
- Non-blocking → ✅ concurrent handling.

## Comparison Table

| Feature     | Blocking (Sync)            | Non-Blocking (Async)         |
| ----------- | -------------------------- | ---------------------------- |
| Example     | `fs.readFileSync`          | `fs.readFile`                |
| Execution   | Halts until task done      | Continues execution          |
| Scalability | Poor (single request hogs) | High (multiple users served) |
| Use Case    | Small scripts, CLI tools   | Servers, APIs, production    |

## ✅ Key Takeaways

- **Blocking = Sync** → Execution halts until done → ❌ not scalable.
- **Non-Blocking = Async** → Offloaded to thread pool → ✅ scalable & efficient.
- **Event Loop** = coordinator.
- **Thread Pool** = heavy lifting.

⚡ **Analogy**

- **Blocking:** ATM with only 1 slot → everyone waits.
- **Non-Blocking:** Take a token, ATM sends SMS when cash ready → others can use ATM in the meantime.

---
