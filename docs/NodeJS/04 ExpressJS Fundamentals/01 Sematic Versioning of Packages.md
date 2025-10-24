# 📘 Understanding Semantic Versioning in Node Projects

> **Section 5 : Vid 38**

## What is Semantic Versioning (SemVer)?

- **Semantic Versioning** is a standardized way to label versions for software packages.
- It follows the format:

### SYNTAX

```
MAJOR.MINOR.PATCH
```

Each part (bit) has a meaning:

| Part | Name              | Purpose                                  |
| ---- | ----------------- | ---------------------------------------- |
| `1`  | **Major Version** | Breaking changes — backward incompatible |
| `0`  | **Minor Version** | New features — backward compatible       |
| `0`  | **Patch Version** | Bug fixes — backward compatible          |

Example:

```
"express": "4.21.1"
```

- **4** → Major version
- **21** → Minor version
- **1** → Patch version

![Semantic Versioning Intro](/img/nodejs/sem-version-intro.png)

## Why Semantic Versioning Matters

- It helps developers understand how risky an update is.
- If you’re using a dependency and it gets updated:

  - You’ll know if it’s **safe to upgrade**, or
  - If the **update might break** your existing code.

## Understanding Each Part

### 1️⃣ PATCH Version (Right-most bit)

- Represents **small, backward-compatible bug fixes**.
- No new features — only fixes to existing functionality.
- Safe to update without fear of breaking your app.

### Example

| From     | To       | Meaning            |
| -------- | -------- | ------------------ |
| `4.21.1` | `4.21.2` | Minor bug fix only |

### Definition

> **Incremented for backward-compatible bug fixes.**

✅ **Key point:** No new functionality, nothing breaks.

### 2️⃣ MINOR Version (Middle bit)

- Represents **new features** that do **not break existing code**.
- Old features continue to work.
- Usually reset the patch bit to `0` after a minor version bump.

### Example

| From     | To       | Meaning                                   |
| -------- | -------- | ----------------------------------------- |
| `4.21.1` | `4.22.0` | Added a new feature (backward compatible) |

### Definition

> **Incremented when new functionality is added in a backward-compatible manner.**

✅ **Safe to update** if you want the new feature,
but not mandatory if your app works fine.

### 3️⃣ MAJOR Version (Left-most bit)

- Represents **breaking changes** or **incompatible API updates**.
- May require code rewrites or configuration changes.
- Updating to a new major version can break existing projects.

### Example

| From     | To      | Meaning                                       |
| -------- | ------- | --------------------------------------------- |
| `4.21.1` | `5.0.0` | Major breaking change — may need code changes |

### Definition

> **Incremented when incompatible API changes occur.**

⚠️ **Important:** Updating to a new major version requires caution and testing.

## How Patch, Minor, and Major Work Together

| Version           | Type of Change | Example         |
| ----------------- | -------------- | --------------- |
| `4.21.1 → 4.21.2` | Patch          | Bug fix         |
| `4.21.1 → 4.22.0` | Minor          | New feature     |
| `4.21.1 → 5.0.0`  | Major          | Breaking change |

✅ Safe updates → **Patch**, **Minor**
⚠️ Risky update → **Major**

![Versioning Explained](/img/nodejs/version-explained.png)

---

## Symbols in `package.json` (`^` and `~`)

In dependencies, you’ll often see versions written like this:

```json
"express": "^4.21.1"
```

These **symbols control automatic version updates**.

### 1️⃣ No Symbol (Exact Version)

```json
"express": "4.21.1"
```

- Always installs **this exact version** — no auto-updates.
- Used when you need strict version control.

### 2️⃣ Tilde (`~`)

```json
"express": "~4.21.1"
```

- Allows updates **only for the patch version**.
- Keeps major and minor fixed.

| Allowed Updates | Example           |
| --------------- | ----------------- |
| Patch only      | `4.21.1 → 4.21.5` |
| Not allowed     | `4.21.1 → 4.22.0` |

🟢 Safe for bug fixes.
🚫 Doesn’t allow new features or breaking changes.

### 3️⃣ Caret (`^`)

```json
"express": "^4.21.1"
```

- Allows updates for **minor and patch versions**, but **not major**.
- Freezes only the **major version**.

| Allowed Updates | Example           |
| --------------- | ----------------- |
| Minor + Patch   | `4.21.1 → 4.30.2` |
| Not allowed     | `4.21.1 → 5.0.0`  |

🟢 Default behavior when installing packages with `npm install <pkg>`.
⚠️ Won’t automatically install breaking changes (major updates).

---

## Where Does npm Fetch Versions From?

- All npm packages are hosted on [https://www.npmjs.com](https://www.npmjs.com).
- When you run:

  ```bash
  npm install express
  ```

  npm checks this site for the latest compatible version based on your version rule.

Example:
If your `package.json` says `"^4.21.1"`, npm will install the latest version below `5.0.0`.

## Example: Express Version History

- `4.21.1` → Stable release (minor & patch updates safe).
- `5.0.0` → Major version (breaking changes introduced).

---

## ✅ Key Takeaways

- **Semantic Versioning (SemVer)** → `MAJOR.MINOR.PATCH`.
- **Patch (x.x.1)** → Bug fixes (safe).
- **Minor (x.1.x)** → New features (safe).
- **Major (1.x.x)** → Breaking changes (risky).
- **`~`** → Update patches only.
- **`^`** → Update minors and patches, not majors.
- Always test your app when upgrading dependencies, especially for **major** changes.

---
