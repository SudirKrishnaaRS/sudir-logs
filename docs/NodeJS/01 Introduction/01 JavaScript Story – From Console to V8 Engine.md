# 📘 JavaScript Story – From Console to V8 Engine

> Section 1 : Vid 1

## What is JavaScript?

- A **programming language** that started as a tool to make web pages interactive.
- Initially executed **only inside browsers**.
- Over time, evolved into a **general-purpose language** that runs on:

  - Browsers
  - Servers
  - Desktop
  - Mobile devices

## The Need for a Runtime / Engine

- JavaScript required a **runtime** to execute.
- Initially, only **browser engines** could run it.
- Couldn’t run JavaScript **independently** on a machine.

## V8 Engine – The Game Changer

- **V8** = Google’s **open-source, high-performance JavaScript & WebAssembly engine**.
- Written in **C++**.
- Originally built for **Chrome**, later extracted for standalone use.

### 🔑 Features

- Very **fast execution**
- **Open source** → widely adopted
- Can be **embedded** into applications

## Node.js – JavaScript Outside the Browser

- Created by **Ryan Dahl (2009)** using the **V8 engine**.
- **Node.js = V8 + extra features** to run JavaScript outside the browser.

### Definition

> Node.js is a **free, open-source, cross-platform JavaScript runtime environment**.

### What Node.js Enables

- Build **servers** (backend)
- Create **web apps**
- Run **command-line tools**
- Execute **scripts**

## Other Runtimes Beyond Node.js

- **Deno** → Secure JS & TS runtime (by Ryan Dahl).
- **Bun** → Modern runtime focused on speed and tooling.
- Common goal: **run JavaScript outside the browser**.

## Installing Node.js

- Download from: [https://nodejs.org](https://nodejs.org)
- Verify installation:

  ```bash
  node -v
  npm -v
  ```

✅ **Key Takeaways**

- JavaScript started as a **browser-only language**.
- **V8 Engine** (Google) made JS **super fast & portable**.
- **Node.js** allowed JS to run **outside browsers** → backend, tools, scripts.
- Alternatives: **Deno** and **Bun**.
- Node.js installation gives you `node` + `npm`.

---
