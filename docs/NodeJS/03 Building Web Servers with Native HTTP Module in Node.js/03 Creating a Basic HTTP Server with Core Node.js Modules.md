# 📘 Creating a Basic HTTP Server with Core Node.js Modules

> Section 4 : Vid 31

## Importing the HTTP Module

- Node.js has a **built-in `http` module** that helps create servers.

- You can import it using:

  ```js
  const http = require("node:http");
  ```

- The `http` module is built-in (comes with Node.js).

---

## SYNTAX: Creating a Server

```js
const http = require("node:http");

const server = http.createServer((req, res) => {
  console.log("I got an incoming request");

  // Perform your business logic here and return the response
  res.writeHead(200);
  res.end("Thanks for visiting my server");
});

server.listen(8000, () => {
  console.log(`Http server is up and running on port 8000`);
});
```

## Step-by-Step Explanation

### 1️⃣ Create a Server

- **`http.createServer()`** creates a new server instance.
- It accepts a **callback function** with two arguments:

  - **`req`** → Incoming Request
  - **`res`** → Response to be sent back

    ```js
    const server = http.createServer((req, res) => {
      console.log("I got an incoming request");
      // Perform your business logic here and return the response
      res.writeHead(200);
      res.end("Thanks for visiting my server");
    });
    ```

### 2️⃣ Start Listening on a Port

- Use **`server.listen(port, callback)`** to start your server.
- Example:

  ```js
  server.listen(8000, () => {
    console.log("Server running on port 8000");
  });
  ```

## Understanding Request & Response

### Request (`req`) Object

- Contains **information about the client’s request**, such as:

  - HTTP method (GET, POST, etc.)
  - URL/path being accessed
  - Headers

### Response (`res`) Object

- Used to **send back data** to the client.
- Common methods:

  - `res.writeHead(statusCode, headers)` – sets HTTP status and headers
  - `res.end(data)` – ends the response and sends data to client

---

## Understanding Ports

### What is a Port?

- Think of your **computer as a house** 🏠 and **ports as room numbers** 🚪.
- Each service (like a web server, database, etc.) runs on a unique port.
- Example:

  | Service     | Port |
  | ----------- | ---- |
  | Database    | 3001 |
  | Node.js App | 3002 |
  | Redis Cache | 3003 |

### Why We Use Ports

- Multiple services can run on the same machine, but **each must use a different port**.
- For local development:

  ```
  http://localhost:8000
  ```

  - **localhost** → your machine
  - **8000** → port number your app listens on

---

## Example of Different Services on One Machine

```
+-----------------------+
| Physical Machine (Host) |
|  ├── Port 3001 → Database Service  |
|  ├── Port 3002 → Node.js App       |
|  └── Port 3003 → Redis Cache       |
+-----------------------+
```

- Access format → `http://<hostname>:<port>`

  - Example: `http://localhost:8000`

---
