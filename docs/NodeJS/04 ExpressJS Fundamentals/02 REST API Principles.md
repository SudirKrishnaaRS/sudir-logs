# 📘 REST API Design Principles for Modern Backend Development

> **Section 5 : Vid 39**

---

## What is a REST API?

- **REST** stands for **Representational State Transfer**.
- It’s an **architectural style**, not a framework or language.
- REST defines **guidelines** for designing scalable, maintainable, and predictable web APIs.
- **Not limited to Node.js or Express** — can be implemented in **Java**, **Python**, **Rust**, **Go**, or any language.

> In simple words, REST defines **how clients and servers communicate over HTTP**.

---

## REST vs RESTful APIs

- A **RESTful API** is an API that **follows REST principles**.
- If an API violates these principles (e.g., stores user state on the server), it’s **not RESTful**.

---

## 🌐 Core REST API Principles

Let’s understand the key architectural constraints that make an API truly “RESTful”.

![REST API Principles](/img/nodejs/rest-principles.png)

---

## 1️⃣ Statelessness

### Definition

> Every request from the client to the server must contain all the information needed to understand and process it.

### Explanation

- The **server should not store client-related state or session data in memory**.
- Each API call is **independent** — server doesn’t remember previous requests.
- If temporary data is needed, store it in a **database** (like PostgreSQL, MongoDB) or **cache layer** (like Redis), not in server memory.

### Why?

- Servers can **scale horizontally** (multiple instances can handle different requests).
- No dependency on in-memory state = better reliability.

### ❌ Example (violates REST):

Server stores logged-in user data in its memory.

### ✅ Example (correct way):

User data or tokens stored in a **database or cache**, not inside server memory.

---

## 2️⃣ Client–Server Architecture

### Definition

> The client and server should be **separate applications** that communicate via APIs.

### Explanation

- **Client** → requests data (e.g., mobile app, web app).
- **Server** → provides data (e.g., JSON response).
- The server **should not handle UI rendering** (like HTML or CSS).
- The client decides **how to present** the data to users.

### Example

- Client: React / iOS / Android app
- Server: Node.js / Express API returning JSON

```http
GET /api/users
→ Server returns JSON
→ Client displays the data on screen
```

✅ Promotes **independence**, **scalability**, and **reusability**.

---

## 3️⃣ Uniform Interface

### Definition

> The API should have a **consistent and predictable design** so developers can easily understand and use it.

### SYNTAX

```http
GET /resource
POST /resource
PUT /resource/:id
DELETE /resource/:id
```

### Explanation

- Use **standard HTTP methods** for operations:

  - **GET** → Retrieve data
  - **POST** → Create new data
  - **PUT/PATCH** → Update data
  - **DELETE** → Remove data

- Keep endpoint names **noun-based** and **predictable**.

### Example

| Method | Endpoint      | Action              |
| ------ | ------------- | ------------------- |
| GET    | `/tweets`     | Retrieve all tweets |
| POST   | `/tweets`     | Create a new tweet  |
| PUT    | `/tweets/:id` | Update a tweet      |
| DELETE | `/tweets/:id` | Delete a tweet      |

### ❌ Bad Example

```http
GET /createTweet   → creates a tweet (unexpected behavior)
```

✅ Predictable design helps developers easily guess API purpose.

---

## 4️⃣ Cacheable Responses

### Definition

> Server responses should be **explicitly marked as cacheable** wherever possible.

### Explanation

- Caching allows clients (or intermediaries) to **reuse responses** instead of requesting fresh data every time.
- Improves **performance** and **reduces server load**.

### Example (using HTTP headers)

```http
Cache-Control: public, max-age=3600
```

- This allows clients to cache the response for 1 hour.

✅ Helps build **highly performant** and **scalable** REST APIs.

---

## ✅ Key Takeaways

- **REST = Architectural style** for designing web APIs.
- **Language-independent** — works with any tech stack.
- **RESTful API principles:**

  - Statelessness
  - Client–Server separation
  - Uniform Interface
  - Cacheable responses

- Avoid storing **user/session data in memory** → use DB or cache.
- Use **HTTP methods** predictably (GET → Read, POST → Create, etc.).
- Following REST principles ensures **scalable, maintainable, and predictable APIs**.

---
