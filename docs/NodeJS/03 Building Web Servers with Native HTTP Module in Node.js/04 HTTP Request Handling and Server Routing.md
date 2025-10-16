# 📘 Deep Dive into HTTP Request, Body and URL's

> Section 4 : Vid 32

## What is an HTTP Request?

- **HTTP (HyperText Transfer Protocol)** is the foundation of communication on the web.
- When a **client** (like your browser) sends a **request** to a **server**, it expects a **response** back.
- Each request includes essential components:

  | Component   | Description                                               |
  | ----------- | --------------------------------------------------------- |
  | **Method**  | Defines the type of action (GET, POST, PUT, DELETE, etc.) |
  | **Headers** | Key-value metadata sent along with the request            |
  | **Body**    | Actual data being sent to the server (optional)           |
  | **URL**     | Identifies the server address and resource path           |

![HTTP Request structure](/img/nodejs/http-request-structure.png)

---

## Understanding HTTP Methods

- The **method** specifies what action the client wants to perform on the server.

| Method     | Purpose                       | Has Body?     |
| ---------- | ----------------------------- | ------------- |
| **GET**    | Retrieve data from the server | ❌ No         |
| **POST**   | Send data to the server       | ✅ Yes        |
| **PUT**    | Update an existing resource   | ✅ Yes        |
| **DELETE** | Remove a resource             | ❌ Usually No |

---

## HTTP Headers – The Metadata of Requests

### Analogy 💡

Think of an **HTTP request** as a **physical parcel** you send by post:

- The **envelope** (outer part) contains the **address**, **sender**, and **tracking info** → this is your **header**.
- The **contents inside the envelope** → this is your **body**.

![Request Header-Body analogy](/img/nodejs/request-header-body-analogy.png)

### What Are Headers?

- Headers are **key–value pairs** that carry **extra information** about the request.
- They help the server understand **how to process** your request.

### Example of Common Headers

```http
Content-Type: application/json
Authorization: Bearer <token>
User-Agent: Chrome/123.0 (Mac)
Accept: application/html
```

### Explanation

- **Content-Type** → Type of data sent (e.g., JSON, HTML).
- **Authorization** → Token or credentials for authentication.
- **User-Agent** → Info about the client making the request.
- **Accept-Encoding / Accept-Language** → Define what kind of response format or language you prefer.

✅ Headers are included in **every HTTP request**, and can even include details like device type or OS.

---

## The HTTP Body

### SYNTAX

```json
{
  "tweet": "What an awesome day!"
}
```

### Explanation

- The **body** contains the **actual data** being sent to the server.
- Typically used in **POST** or **PUT** requests.
- Not required for **GET** or **DELETE** requests.

| Method | Body Needed? | Example Use                             |
| ------ | ------------ | --------------------------------------- |
| GET    | ❌           | Fetching data (e.g., `/users`)          |
| POST   | ✅           | Submitting data (e.g., `/create-tweet`) |
| PUT    | ✅           | Updating user info                      |
| DELETE | ❌           | Removing a resource                     |

### Example Scenario

```http
POST
Content-Type: application/json

{
  "tweet": "What an awesome day!"
}
```

- Server receives this JSON body → saves it to the database → sends a response.

---

## Understanding URLs

![URL structure](/img/nodejs/url-structure.png)

#### Breaking Down the URL

| Part                | Name                    | Description                                |
| ------------------- | ----------------------- | ------------------------------------------ |
| `https`             | **Scheme / Protocol**   | Defines communication type (HTTP or HTTPS) |
| `www`               | **Subdomain**           | Points to a specific section or service    |
| `google.com`        | **Naked / Apex Domain** | The main domain name                       |
| `/contact-us`       | **Path**                | The resource or endpoint being accessed    |
| `?lang=en&sort=asc` | **Query Parameters**    | Extra key–value data in the URL            |

#### Query Parameters Explained

- Added after a **?** symbol in the URL.
- Used to send **extra key-value data** to the server.
- Multiple parameters separated by **&**.

✅ Server can parse these parameters and tailor its response (e.g., show sorted results).

---
