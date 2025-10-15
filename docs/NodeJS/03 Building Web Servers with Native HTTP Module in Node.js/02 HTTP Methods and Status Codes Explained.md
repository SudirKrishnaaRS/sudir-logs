# 📘 HTTP Methods and Status Codes Explained

> Section 4 : Vid 30

## Understanding the Request-Response Cycle

- **Client and Server Interaction** happens in a **request-response cycle**.
- **Client** sends a **request** → **Server** processes it → **Server** sends back a **response**.
- This cycle continues every time a new request is made.

- The **client closes the connection** once the response is received (unless persistent connections like **Server-Sent Events** are used).

![Request-Response Cycle](/img/nodejs/request-response-cycle.png)

---

## HTTP Methods (Sent from CLIENT)

HTTP defines **standard methods** that specify the **type of action** to perform on a resource.

### Common Methods

| **Method** | **Purpose**                             | **Example Scenario**                                 |
| ---------- | --------------------------------------- | ---------------------------------------------------- |
| **GET**    | Retrieve data from the server           | View all tweets, fetch comments, get a list of users |
| **POST**   | Send new data to the server             | Create a tweet, upload a video, add a comment        |
| **PATCH**  | Update **part** of an existing resource | Update only the username in a profile                |
| **PUT**    | Replace or update **entire** resource   | Replace a user’s complete profile data               |
| **DELETE** | Remove a resource from the server       | Delete a tweet, remove a comment                     |

![Client Request Methods](/img/nodejs/client-request.png)

### Explanation

- The **method** (GET, POST, PUT, etc.) indicates what the client wants the server to do.
- Each request contains:

  - **URL** (e.g., `/api/users`)
  - **Headers** (e.g., `Content-Type`)
  - **Body** (for methods like POST, PUT, PATCH)

---

## HTTP Status Codes (Sent by SERVER)

HTTP responses include **status codes** to inform the client about the result of their request.

### Classification of Status Codes

| **Range** | **Type**      | **Meaning**                                                |
| --------- | ------------- | ---------------------------------------------------------- |
| **1xx**   | Informational | Request received, continuing process                       |
| **2xx**   | Success       | The request was successfully received and processed        |
| **3xx**   | Redirection   | Client must take additional action to complete the request |
| **4xx**   | Client Error  | The request contains bad syntax or cannot be fulfilled     |
| **5xx**   | Server Error  | The server failed to fulfill a valid request               |

### Common HTTP Status Codes

| **Code** | **Meaning**           | **When Used**                        |
| -------- | --------------------- | ------------------------------------ |
| **200**  | OK                    | Request processed successfully       |
| **201**  | Created               | Resource created successfully        |
| **301**  | Moved Permanently     | Resource has been moved to a new URL |
| **400**  | Bad Request           | Invalid or malformed request         |
| **401**  | Unauthorized          | Authentication required              |
| **403**  | Forbidden             | Authenticated but not authorized     |
| **404**  | Not Found             | Resource doesn’t exist               |
| **500**  | Internal Server Error | Generic server-side failure          |
| **503**  | Service Unavailable   | Server temporarily unavailable       |

![Server Response Status Codes](/img/nodejs/server-response.png)

**Scenario 1 – Successful Request**

- Client requests all tweets using **GET /tweets**.
- Server processes and returns a **200 OK** response.

**Scenario 2 – Resource Not Found**

- Client requests **/user/9999**, but that user doesn’t exist.
- Server returns a **404 Not Found**.

**Scenario 3 – Unauthorized Access**

- Client tries to access a protected route without authentication.
- Server responds with **401 Unauthorized**.

✅ **Key Takeaways**

- HTTP is a **stateless protocol** — each request is independent.
- **Methods** define what the client wants to do (GET, POST, PUT, PATCH, DELETE).
- **Status Codes** describe how the server handled the request.
- Knowing which status code to send improves **API design and debugging**.
- 2xx = success, 4xx = client error, 5xx = server error.

---
