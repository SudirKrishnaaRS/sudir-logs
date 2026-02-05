# 01 Lazy Loading (Code Splitting)

---

## Code Splitting with `React.lazy`

## What problem does it solve?

- Large React apps ship **one huge JavaScript bundle** by default.
- Browser must **download everything first** → slow initial load.
- Users wait even for code they **may never use**.

### Simple analogy

- Carrying **all school books every day** 🎒 = bad
- Carrying **only today’s books** = code splitting ✅

---

## What React does by default

- Bundles **all components into one file**
- Browser downloads entire bundle before rendering
- **Larger bundle = slower first paint**

---

## How `React.lazy` works

- Allows loading components **only when required**
- Splits code into **separate chunks**
- Improves **initial load time & perceived performance**

---

## Implementation

### ❌ Normal import (no code splitting)

```js
import Dashboard from "./Dashboard";
```

### ✅ Lazy loading with `React.lazy`

```js
import React, { Suspense } from "react";

const Dashboard = React.lazy(() => import("./Dashboard"));
```

### Wrap lazy component with `Suspense`

```jsx
<Suspense fallback={<Loader />}>
  <Dashboard />
</Suspense>
```

---

## When to use `React.lazy`

- **Route-based pages**
- **Modals / drawers**
- **Heavy components** (charts, editors)

---

## Important Notes

- Works only with **default exports**
- Requires bundler support (Webpack, Vite)
- For **SSR** → use framework helpers (Next.js `dynamic()`)

---

## Interview-ready explanation

> Code splitting improves performance by loading JavaScript only when needed.
> I use `React.lazy` with `Suspense` to dynamically import routes and heavy components, reducing initial bundle size and improving first load time.

---
