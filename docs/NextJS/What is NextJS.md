# 🧠 Next.js in a Nutshell

**Video Reference:** [What is Next.js? – The React Framework Explained](https://youtu.be/xnOwOBYaA3w?si=74DcE9ijiIQRMt_x)

---

## 🚀 What is Next.js?

- **Next.js** is a **React framework** that provides:

  - **Routing**
  - **Server-side rendering (SSR)**
  - **API routes**
  - **Image optimization**
  - **SEO out of the box**

- Unlike plain React, Next.js comes with a **complete setup** to start building production-ready apps quickly.

---

## ⚙️ Setting Up a Next.js Project

- Run this command to create a new project:

  ```bash
  npx create-next-app
  ```

- The generated project looks like a regular React app but includes:

  - `next.config.ts` → for custom **configuration** (environment variables, build settings, etc.)

---

## 🧭 Routing in Next.js

### **1. Pages Router (Legacy)**

- Located in the **`pages/`** folder.
- Each file inside becomes a route.

  ```bash
  pages/
    about.tsx  →  /about
  ```

### **2. App Router (Modern, since Next.js 13)**

- Located in the **`app/`** folder.
- Create a folder per route, and inside it place a `page.tsx` file.

  ```bash
  app/
    about/
      page.tsx  →  /about
  ```

✅ **App Router is recommended** — it’s more scalable and modern.

---

## 🧩 Server Components vs Client Components

### **Server Components**

- Rendered **on the server** and send only **HTML** to the client.

- **Great for performance and SEO**.

- Example (Server Component):

  ```tsx
  export default function Page() {
    return <h1>Hello from server!</h1>;
  }
  ```

- ❌ No browser APIs (like `onClick` or `useState`).

---

### **Client Components**

- Used for **interactivity** (hooks, event handlers, etc.).

- Add `"use client"` at the top:

  ```tsx
  "use client";

  export default function Button() {
    return <button onClick={() => alert("Clicked!")}>Click Me</button>;
  }
  ```

- Client components can be **imported into server components** for mixed rendering.

---

## 🔄 Data Fetching in Next.js

- Unlike React, you can **fetch data directly inside your component** using async/await.

  ```tsx
  export default async function Page() {
    const res = await fetch("https://jsonplaceholder.typicode.com/users");
    const users = await res.json();

    return <pre>{JSON.stringify(users, null, 2)}</pre>;
  }
  ```

- Next.js **handles caching, revalidation, and loading states** automatically.

- To show a **loading UI**, create a `loading.tsx` file in the same folder:

  ```tsx
  // app/users/loading.tsx
  export default function Loading() {
    return <p>Loading users...</p>;
  }
  ```

---

## ⚡ API Routes

- You can create your own **backend endpoints** inside the same Next.js project.

- Example:

  ```
  app/
    api/
      hello/
        route.ts
  ```

  ```ts
  // app/api/hello/route.ts
  export async function GET() {
    return Response.json({ message: "Hello from API" });
  }
  ```

- Supports **GET, POST, PUT, DELETE** — no need for Express.js.

---

## 🖼️ Image Optimization

- Use the built-in `<Image />` component for:

  - **Automatic compression**
  - **Lazy loading**
  - **Improved performance**

  ```tsx
  import Image from "next/image";

  <Image src="/logo.png" alt="Logo" width={200} height={200} />;
  ```

---

## 🌐 SEO in Next.js

- Each route can define its own **metadata**:

  ```tsx
  export const metadata = {
    title: "About Us - My Website",
    description: "Learn more about our company",
    keywords: ["about", "company", "info"],
  };
  ```

- This helps **search engines** easily index your pages and **rank higher**.

---

## ✅ Key Takeaways

- **Next.js = React + Batteries Included**
- **App Router** (introduced in v13) is the new standard.
- **Server Components** improve SEO and performance.
- **Client Components** handle interactivity (hooks, events).
- **Built-in API Routes** eliminate the need for a separate backend.
- **Image Optimization** and **SEO Metadata** come built-in.
- Perfect for building **scalable, SEO-friendly** apps with minimal setup.

---
