# Questions

🧠 1. Interface vs Type (TypeScript)
➡️ What’s the difference, and when would you prefer one over the other?

🎨 2. Why Tailwind CSS?
➡️ Why do developers prefer Tailwind over Bootstrap / traditional CSS?
➡️ How is it better for scalable UI and component-based apps?

🧪 3. Testing in React
➡️ Are you comfortable writing test cases in React?
➡️ Have you used Jest / React Testing Library?
➡️ How do you test components and API flows?

⏱️ 4. Cancelling an API request
➡️ If an API takes ~5 seconds, how would you stop/cancel it midway?
(Hint: AbortController / Axios cancel token)

🧠 5. Detecting Memory Leaks in React / Frontend
➡️ How do you identify that a memory leak is happening in your application?

💧 6. Fixing Hydration Errors in Next.js
➡️ What is a hydration error, and why does it happen?

🔐 7. localStorage & Cross-Domain Access
➡️ If you store data in localStorage on one domain, can another domain access it?

📦 8. Why Code Splitting?
➡️ Why is code splitting better compared to loading everything at once?

⚡ 9. Dynamic Imports
➡️ What are dynamic imports?

🧩 10. Code Splitting vs Chunking
➡️ What’s the difference between code splitting and chunking?

🌿 11. Git Rebase
➡️ What is rebase in Git?

📊 12. Bundle Size Awareness
➡️ What was your last production bundle file size?

---

# Answers

## 🧠 1. Interface vs Type (TypeScript)

### 👶 Simple explanation

Think of **interface** and **type** like **blueprints** 🏗️ for objects.

- Interface is like a **school uniform** — you can add more rules later.
- Type is like a **fixed costume** — once defined, it’s mostly final.

---

### 🔍 Deep explanation

#### `interface`

- Mainly used to describe **object shapes**
- Can be **extended**
- Can be **merged** (declaration merging)

```ts
interface User {
  name: string;
}

interface User {
  age: number;
}
// This is valid
```

---

#### `type`

- Can represent **objects, unions, primitives, functions**
- More **flexible**
- Cannot be merged

```ts
type Status = "loading" | "success" | "error";
```

---

### 🧠 When to prefer what

| Use case                  | Prefer      |
| ------------------------- | ----------- |
| Public APIs / libraries   | `interface` |
| Objects & class contracts | `interface` |
| Unions / tuples           | `type`      |
| Complex compositions      | `type`      |

---

### 🗣️ Interview-ready answer

> I use `interface` for object shapes and contracts because it’s extendable and works well with classes. I use `type` when I need unions, intersections, or more complex type compositions.

---

## 🎨 2. Why Tailwind CSS?

### 👶 Simple explanation

Traditional CSS is like writing **instructions from scratch** 📝.
Tailwind gives you **ready-made Lego blocks** 🧱.

---

### 🔍 Why developers prefer Tailwind

#### 1️⃣ Utility-first approach

```html
<div class="flex items-center justify-between p-4"></div>
```

- No switching between CSS & JS files
- Faster development

---

#### 2️⃣ Better for component-based apps

- Styles live **with components**
- No global CSS conflicts
- Easy reuse

---

#### 3️⃣ Scalability

- No growing CSS files
- No naming problems (`btn-primary-v2-final` 😄)
- Consistent design system

---

### 🆚 Tailwind vs Bootstrap

| Bootstrap           | Tailwind           |
| ------------------- | ------------------ |
| Prebuilt components | Build your own     |
| Opinionated UI      | Fully customizable |
| Hard to override    | Easy to control    |

---

### 🗣️ Interview-ready answer

> Tailwind works well with component-based architectures. It avoids global CSS issues, improves consistency, and scales better in large applications compared to traditional CSS or Bootstrap.

---

## 🧪 3. Testing in React

### 👶 Simple explanation

Testing is like **checking homework before submission** 📚.

---

### 🔍 Types of testing I focus on

#### 1️⃣ Component testing

- Does component render correctly?
- Does user interaction work?

```js
render(<Button />);
expect(screen.getByText("Submit")).toBeInTheDocument();
```

---

#### 2️⃣ User behavior testing

- Clicks
- Typing
- Form submission

```js
fireEvent.click(button);
```

---

#### 3️⃣ API flow testing

- Mock API calls
- Test loading & error states

```js
jest.mock("axios");
```

---

### 🛠 Tools

- Jest → test runner
- React Testing Library → user-focused testing

---

### 🗣️ Interview-ready answer

> I focus on testing components from the user’s perspective using React Testing Library. I mock APIs, test loading and error states, and avoid testing implementation details.

---

## ⏱️ 4. Cancelling an API request

### 👶 Simple explanation

You ordered food 🍕, but then changed your mind.
You cancel the order before it arrives.

---

### 🔍 Why cancellation is needed

- Prevent memory leaks
- Avoid setting state after unmount
- Improve UX

---

### ✅ Using AbortController

```js
const controller = new AbortController();

fetch(url, { signal: controller.signal });

controller.abort();
```

---

### 🧠 In React

```js
useEffect(() => {
  const controller = new AbortController();

  fetchData(controller.signal);

  return () => controller.abort();
}, []);
```

---

### 🗣️ Interview-ready answer

> I use AbortController to cancel API requests when a component unmounts or when a new request replaces the old one.

---

## 🧠 5. Detecting Memory Leaks

### 👶 Simple explanation

Memory leak = app keeps things in memory it doesn’t need 🧠💧

---

### 🔍 Signs of memory leaks

- App becomes slower over time
- Browser tab uses more memory
- Crashes after long usage

---

### 🔧 How I detect them

1. Chrome DevTools → Memory tab
2. Heap snapshots
3. Monitor retained objects
4. Production monitoring tools

---

### 🗣️ Interview-ready answer

> I identify memory leaks using heap snapshots, checking uncleaned listeners, timers, or subscriptions, and validating cleanup in useEffect.

---

## 💧 6. Hydration Errors in Next.js

### 👶 Simple explanation

Server says: “HTML looks like this”
Browser says: “That’s not what I expected” 😵

---

### 🔍 What is hydration?

- Server renders HTML
- React attaches event listeners on client

---

### ❌ Why hydration errors happen

- Using `window` during SSR
- Date/time differences
- Random values (`Math.random`)
- Conditional rendering mismatch

---

### 🛠 Fixes

- Use `useEffect`
- `dynamic(import, { ssr: false })`

---

### 🗣️ Interview-ready answer

> Hydration errors occur when server-rendered HTML doesn’t match client-rendered output. I fix them by avoiding browser-only APIs during SSR and deferring such logic to the client.

---

## 🔐 7. localStorage & Cross-Domain Access

### 👶 Simple explanation

Your diary 📔 is locked per house 🏠.

---

### 🔍 Rule

👉 **localStorage is domain-specific**

- `example.com` ❌ cannot access `google.com`
- Subdomains are also isolated

---

### 🗣️ Interview-ready answer

> No, localStorage is scoped to a domain. One domain cannot access another domain’s localStorage due to browser security restrictions.

---

## 📦 8. Why Code Splitting?

### 👶 Simple explanation

Don’t download the whole movie 🎬 if you’re watching only the trailer.

---

### 🔍 Benefits

- Faster initial load
- Smaller bundles
- Better performance

---

### 🗣️ Interview-ready answer

> Code splitting improves performance by loading only required code, reducing initial bundle size and improving perceived speed.

---

## ⚡ 9. Dynamic Imports

### 👶 Simple explanation

Load something **only when needed**.

---

### 🔍 Example

```js
import("./Chart").then((module) => {
  module.render();
});
```

---

### 🧠 Used for

- Lazy loading
- Code splitting
- Conditional loading

---

### 🗣️ Interview-ready answer

> Dynamic imports allow loading modules at runtime, enabling lazy loading and improving performance.

---

## 🧩 10. Code Splitting vs Chunking

### 👶 Simple explanation

- Code splitting = **strategy**
- Chunking = **result**

---

### 🔍 Difference

| Code Splitting      | Chunking       |
| ------------------- | -------------- |
| Developer decision  | Bundler output |
| Logical             | Physical files |
| Manual or automatic | Automatic      |

---

### 🗣️ Interview-ready answer

> Code splitting is the technique of dividing code logically, while chunking is how the bundler outputs those splits into files.

---

## 🌿 11. Git Rebase

### 👶 Simple explanation

Rebase = **cleaning history** 🧹

---

### 🔍 What rebase does

- Moves commits to new base
- Creates linear history

---

### 🧠 When to use

- Before merging
- Cleaning feature branches

---

### 🗣️ Interview-ready answer

> Rebase reapplies commits on top of another branch to maintain a clean, linear Git history.

---

## 📊 12. Bundle Size Awareness

### 👶 Simple explanation

Big bundle = slow app 🐢

---

### 🔍 What interviewers want

They want awareness, not exact numbers.

---

### 🗣️ Smart interview answer

> I actively monitor bundle size using tools like Webpack Bundle Analyzer. Our last production bundle was optimized using code splitting and tree shaking, keeping initial load under acceptable limits.

(If pressed, say something like **~200–300 KB gzipped**)

---

## 🎯 Final Interview Tip

For **senior questions**:

- Structure matters more than syntax
- Explain **why**, not just **how**
- Mention **trade-offs**

---
