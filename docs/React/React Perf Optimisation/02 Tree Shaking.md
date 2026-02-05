# 02 Tree Shaking & Dependency Cleanup

## 1️⃣ Tree Shaking

## What is Tree Shaking?

### Simple analogy

- You buy a **tree 🌳**
- You only need **some branches**
- Tree shaking removes the unused branches

---

## In JavaScript terms

- Import a library
- Use only **few exports**
- Bundler removes unused code automatically

---

## Example without tree shaking

```js
import _ from "lodash";

_.debounce();
```

➡️ Entire lodash bundle included ❌

---

## Tree-shakable import

```js
import debounce from "lodash/debounce";
```

➡️ Only required function bundled ✅

---

## How tree shaking works

Tree shaking is effective when:

- ES Modules (`import / export`) are used
- Bundler supports it (Webpack, Rollup, Vite)
- Code has **no side effects**

---

## Enabling tree shaking

### `package.json`

```json
{
  "sideEffects": false
}
```

OR (for CSS / special cases)

```json
{
  "sideEffects": ["*.css"]
}
```

---

## Common mistakes

- Using `require()`
- Importing entire libraries
- Libraries with side effects

---

## 2️⃣ Removing Unused Dependencies

## What problem does it solve?

- Unused dependencies are like **unused apps on your phone** 📱
- They consume space and slow things down.

---

## Why unused dependencies are harmful

- Increase **bundle size**
- Slow **install & build time**
- Introduce **security risks**
- Increase **maintenance overhead**

---

## How to find unused dependencies

### 1 Manual audit

- Review `package.json`
- Identify:

  - Old libraries
  - Replaced utilities

---

### 2 Automated tools (recommended)

#### `depcheck`

```bash
npx depcheck
```

Finds:

- Unused dependencies
- Missing dependencies

---

### 3️⃣ Bundle analysis

```bash
npm install --save-dev webpack-bundle-analyzer
```

- Visualizes what **actually ships** to users

---

## How to remove safely

```bash
npm uninstall lodash
```

Then:

- Run the app
- Run tests
- Monitor production

---

## Interview-ready explanation

> I regularly audit dependencies using tools like `depcheck` and bundle analyzers.
> Removing unused dependencies reduces bundle size, improves security, and keeps the codebase clean.

---

## Things to be careful about

- Build-time dependencies
- Dynamically imported modules
- Peer dependencies

---

## Interview-ready explanation

> Tree shaking is a build-time optimization that removes unused exports from the final bundle.
> I ensure ES module imports and proper side-effect configuration to maximize bundle reduction.

---

## 🔥 How These Optimizations Work Together

| Optimization        | Purpose                        |
| ------------------- | ------------------------------ |
| Code Splitting      | Load code only when needed     |
| Remove Dependencies | Reduce what you ship           |
| Tree Shaking        | Remove unused code inside libs |

---

## 🎯 Final Interview Power Summary

> I'd optimize React application performance by combining code splitting using `React.lazy`, removing unused dependencies through audits, and leveraging tree shaking via ES modules and proper imports.
> Together, these significantly reduce bundle size and improve load performance.

---

✅ **Key Takeaways**

- `React.lazy` improves **initial load time**
- Removing unused dependencies reduces **bundle size & risk**
- Tree shaking eliminates **unused code at build time**
- Combined optimizations = **fast, scalable React apps**

---
