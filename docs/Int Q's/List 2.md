# Questions

Here are 15 questions top frontend engineers are being asked right now:
1️⃣ How would you optimize a React application rendering 100k+ items in a list?

2️⃣ What strategies would you use to improve page load time for a global audience?

3️⃣ You notice a memory leak in a production SPA—how do you identify and fix it?

4️⃣ A component breaks when upgrading a library version—how do you manage dependencies?

5️⃣ How would you debug a performance bottleneck in a React app using DevTools?

6️⃣ You need to migrate a legacy frontend codebase to a modern framework—what’s your plan?

7️⃣ How do you ensure secure handling of sensitive user data on the client side?

8️⃣ Users report intermittent UI glitches in different browsers—how would you troubleshoot?

9️⃣ A critical UI feature is failing during peak traffic—how do you mitigate the issue?

🔟 How do you manage state in a complex app to avoid unnecessary re-renders?

1️⃣1️⃣ How would you implement a robust frontend monitoring and logging system?

1️⃣2️⃣ You need to render a large dataset without blocking the main thread—how do you approach it?

1️⃣3️⃣ How would you implement A/B testing without affecting current users?

1️⃣4️⃣ A CSS animation is janky on mobile devices—how do you identify and fix the issue?

1️⃣5️⃣ How do you handle real-time updates in a React application efficiently?

---

# Answers

# 1️⃣ Optimizing a React app rendering **100k+ items**

**How I would approach it:**

First, I’d understand **why performance is slow**. Rendering 100k items means React is creating and managing 100k DOM nodes, which is expensive for the browser.

**Key optimizations I’d apply:**

1. **List Virtualization**

   - I would use libraries like `react-window` or `react-virtualized`
   - These render only the items visible on the screen
   - As the user scrolls, items are reused instead of recreated

2. **Memoization**

   - Wrap row components with `React.memo`
   - Prevent unnecessary re-renders when props don’t change

3. **Avoid Inline Functions**

   - Inline callbacks cause new references on every render
   - I’d use `useCallback` for handlers

4. **Stable Keys**

   - Avoid using array index as key
   - Use unique IDs for correct reconciliation

5. **Data Strategy**

   - Pagination or infinite scrolling instead of loading everything

**How I’d validate improvement:**

- Use React Profiler
- Measure FPS and render times

**Trade-offs:**

- Virtualization adds complexity
- Not ideal for SEO-heavy pages

---

# 2️⃣ Improving page load time for a **global audience**

**My thought process:**

Page load time depends on:

- Network latency
- Bundle size
- Asset optimization
- Delivery location

**Steps I’d take:**

1. **Use CDN**

   - Serve static assets from edge locations
   - Reduces distance between user and server

2. **Reduce JavaScript Bundle Size**

   - Code splitting with `React.lazy`
   - Remove unused dependencies
   - Tree shaking

3. **Optimize Assets**

   - Compress images (WebP)
   - Lazy load images and components
   - Minify CSS and JS

4. **Caching Strategy**

   - Long cache headers for static assets
   - Service workers if applicable

5. **Critical Rendering Path**

   - Preload important resources
   - Defer non-critical scripts

**How I’d measure success:**

- Lighthouse
- Core Web Vitals (LCP, FID, CLS)

---

# 3️⃣ Identifying and fixing a **memory leak in production**

**First step: identify the leak**

I’d reproduce the issue locally or in staging and use:

- Chrome DevTools → Memory tab
- Heap snapshots over time

**Common causes I check first:**

- Event listeners not removed
- `setInterval` / `setTimeout` not cleared
- WebSocket subscriptions
- Observers (Intersection, Resize)

**Fix approach:**

- Ensure cleanup in `useEffect`
- Use AbortController for fetch
- Close subscriptions on unmount

```js
useEffect(() => {
  const controller = new AbortController();
  fetch(url, { signal: controller.signal });
  return () => controller.abort();
}, []);
```

**Prevention:**

- ESLint rules
- Code reviews
- Monitoring tools like Sentry

---

# 4️⃣ Component breaks after a **library upgrade**

**My approach is systematic, not reactive:**

1. **Read changelog**

   - Identify breaking changes
   - Deprecated APIs

2. **Reproduce in isolation**

   - Create a minimal failing example

3. **Check Dependency Tree**

   - Peer dependency mismatches
   - Multiple versions of same library

4. **Fix or Pin**

   - Update code to new API
   - Temporarily pin version if blocked

5. **Add Tests**

   - Prevent regression in future upgrades

**Best practice:**

- Incremental upgrades
- Lock versions using `package-lock`

---

# 5️⃣ Debugging a React **performance bottleneck**

**First, I measure. Never guess.**

1. **React DevTools Profiler**

   - Identify slow components
   - Check unnecessary re-renders

2. **Chrome Performance Tab**

   - Look for long scripting tasks
   - Layout thrashing

3. **why-did-you-render**

   - Detect wasted renders

**Optimization techniques:**

- `React.memo`
- `useMemo` for expensive calculations
- `useCallback` for stable references
- Splitting large components

**Key mindset:**

> Optimize only what’s proven to be slow.

---

# 6️⃣ Migrating a legacy frontend codebase

**I avoid big-bang rewrites.**

**My migration plan:**

1. **Audit**

   - Identify critical paths
   - Understand dependencies

2. **Stabilize**

   - Add tests
   - Fix major bugs

3. **Incremental Migration**

   - Use strangler pattern
   - New features in modern stack
   - Old code gradually removed

4. **Shared Layer**

   - Shared design system
   - Shared API clients

**Why this works:**

- Lower risk
- Business continuity
- Faster value delivery

---

# 7️⃣ Secure handling of sensitive user data

**Core principle:**
Frontend is **never fully secure**.

**My approach:**

1. **Minimize Exposure**

   - Never store tokens in `localStorage`
   - Avoid exposing secrets in JS

2. **Use Secure Mechanisms**

   - HTTP-only cookies
   - CSRF protection

3. **Input Handling**

   - Sanitize user input
   - Prevent XSS

4. **Browser Security**

   - Content Security Policy
   - SameSite cookies

**Final note:**

- All critical validation happens on backend

---

# 8️⃣ Debugging intermittent UI glitches across browsers

**Step-by-step approach:**

1. **Reproduce**

   - Use BrowserStack
   - Match OS + browser

2. **Isolate**

   - CSS layout issues
   - Race conditions in JS

3. **Check Compatibility**

   - CSS support
   - Polyfills

4. **Fix**

   - Feature detection
   - Graceful fallbacks

**Documentation & regression tests prevent future issues.**

---

# 9️⃣ Critical UI failing during peak traffic

**Priority order:**

1. **Mitigate Impact**

   - Disable feature using feature flags
   - Show fallback UI

2. **Stabilize System**

   - Reduce client-side load
   - Cache aggressively

3. **Investigate**

   - Logs
   - Metrics

4. **Postmortem**

   - Root cause
   - Preventive fixes

**Mindset:**

> User experience first, perfection later.

---

# 🔟 Managing state in complex apps

**State strategy:**

1. **Local First**

   - Keep state close to component

2. **Global Only When Needed**

   - Auth
   - Theme
   - Shared data

3. **Avoid Over-Renders**

   - Memoized selectors
   - Split context providers

4. **Normalize Data**

   - Prevent deep updates

**Tools:**

- Redux Toolkit
- Zustand
- React Query

---

# 1️⃣1️⃣ Frontend monitoring & logging

**I focus on observability:**

1. **Error Tracking**

   - Runtime exceptions
   - Source maps

2. **Performance Monitoring**

   - Slow screens
   - API latency

3. **User Context**

   - Session replay
   - Breadcrumbs

4. **Alerting**

   - Threshold-based alerts

**Tools:**

- Sentry
- Datadog
- LogRocket

---

# 1️⃣2️⃣ Rendering large datasets without blocking UI

**My strategy:**

1. **Split Work**

   - Chunk rendering
   - Idle callbacks

2. **Offload Work**

   - Web Workers for computation

3. **Optimize Rendering**

   - Virtualization
   - Progressive rendering

**Result:**
Smooth UI, responsive interactions.

---

# 1️⃣3️⃣ Implementing A/B testing safely

**Safe rollout plan:**

1. **Feature Flags**
2. **Consistent User Bucketing**
3. **Metrics Tracking**
4. **Gradual Rollout**
5. **Rollback Strategy**

**Important:**
No flickering, no layout shifts.

---

# 1️⃣4️⃣ Fixing janky CSS animations

**Diagnosis:**

- Profile animation
- Check paint & layout costs

**Fixes:**

- Use `transform` and `opacity`
- Reduce DOM size
- Avoid forced reflows

**Result:**
Smooth animations even on low-end devices.

---

# 1️⃣5️⃣ Efficient real-time updates in React

**Approach:**

1. **WebSockets**
2. **Selective Updates**
3. **Batching**
4. **Optimistic UI**

**State design is key** to avoid full re-renders.

---
