# 📘 Node.js Modules and Their Role

> Section 2 : Vid 19

## What are Modules?

- A **module** = collection of code (functions/objects) providing specific functionality.
- Helps in **structuring, reusing, and organizing** code.

## Types of Modules in Node.js

1. **Built-in Modules** (core modules)

   - Provided out-of-the-box by Node.js.
   - Examples: `fs` (file system), `path`, `http`, `crypto`.

2. **Third-Party Modules**

   - Installed via **npm** (`npm install package-name`).
   - Examples: `express`, `jsonwebtoken`, `lodash`.

3. **Custom (User-defined) Modules**

   - Written by developers for their own projects.
   - Referred using relative paths:

     - `require("./math.js")` → current directory
     - `require("../utils.js")` → parent directory

## The `require()` Function

- Used to **import modules**.
- Resolution order(Internal working):

  1. Checks **third-party modules** (in `node_modules`).
  2. Checks **built-in modules**.
  3. If path starts with `./` or `../` → treated as a **custom module**.
  4. If not found → throws error.

- **Caching**: once loaded, a module is cached for performance.

## Module Wrapper in Node.js (Internal implementation on how functions like module(), require() are made available)

- Node internally wraps each module in a function:

  ```js
  function (exports, require, module, __filename, __dirname) {
    // module code here
  };
  ```

- This gives access to:

  - `require` → import modules
  - `exports/module.exports` → export code
  - `__filename` → current file name
  - `__dirname` → directory name

### Example: Using Built-in `fs` Module

```js
const fs = require("fs");
const content = fs.readFileSync("notes.txt", "utf8");
console.log(content);
```

✅ **Key Takeaways**

- Node.js modules = foundation of code structuring.
- Three types: built-in, third-party, custom.
- `require()` is central to module loading & resolution.
- Node wraps code in a module function to provide exports, require, and file info.

---

# 📘 Working with Third-Party Modules using npm and Package.json

> Section 2 : Vid 20

## What is npm?

- **npm** = Node Package Manager (unofficially called this, no official full form).
- Used to **install, manage, and share packages** in Node.js projects.
- Packages = Reusable pieces of code published by developers.

## Making a Project a Package

- To manage dependencies, a Node.js project needs a **`package.json`** file.
- `package.json` = configuration/manifest file of the project.

### Contents of `package.json`

- Project **name**
- **Version**
- **Description** (optional)
- **Entry point** (default: `index.js`)
- **Scripts** (custom commands like `npm start`)
- **Dependencies** (external packages required for project)

👉 Create `package.json`:

```bash
npm init
```

- Prompts for project details (name, version, description, entry point, etc.).
- Generates a `package.json` file at the project root.

## Installing a Third-Party Module

Example: Install Node.js typings for VS Code autocompletion.

```bash
npm install @types/node
# shortcut
npm i @types/node
```

- Installs the package from npm registry.
- Adds the package to **dependencies** in `package.json`.
- Creates a new folder → **`node_modules`** → contains source code of installed packages.

## The `node_modules` Folder

- Stores **source code of installed packages**.
- Should never be manually edited.
- ❌ Do not push `node_modules` to GitHub → it is **huge**.
- Instead, share only source code + `package.json`.
- Other developers can run `npm install` → it will download dependencies again.

## Regenerating Dependencies

- If `node_modules` is deleted → run:

  ```bash
  npm install
  ```

- Reads from `package.json` → reinstalls all dependencies.

## The `package-lock.json` File

- Auto-generated when installing packages.
- Tracks **exact version** and **dependency tree** (dependencies of dependencies).
- Example:

  - Project A depends on B
  - B depends on C and D
  - `package-lock.json` keeps track of this hierarchy.

- ❌ Do not edit manually.
- Can be deleted → regenerated with `npm install`.

## Importance of `package.json` vs `package-lock.json`

| File                | Purpose                                                             | Editable? |
| ------------------- | ------------------------------------------------------------------- | --------- |
| `package.json`      | Main config file. Lists **direct dependencies**, scripts, metadata. | ✔️ Yes    |
| `package-lock.json` | Records **exact versions** + dependency tree (ensures consistency). | ❌ No     |

## 🔑 In a Nutshell

- package.json → “Which packages do I need?” (loose versions)

- package-lock.json → “Which exact versions am I using right now?” (locked tree)

✅ **Key Takeaways**

- **npm** is the package manager for Node.js projects.
- `package.json` = main config file (dependencies, scripts, metadata).
- `npm install <package>` adds packages to project + `node_modules`.
- `node_modules` contains source code of dependencies → **never push to GitHub**.
- `package-lock.json` ensures consistent dependency versions across machines.
- To regenerate dependencies: `npm install`.
- Always maintain `package.json` + source code → everything else is regeneratable.

---
