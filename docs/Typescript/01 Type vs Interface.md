# 01 Interface vs Type

---

## Concept (Simple Explanation)

Both **`interface`** and **`type`** are used to define **blueprints for data structures** in TypeScript.

- Think of **`interface`** like a **school uniform** 👕
  → You can **add more rules later**.
- Think of **`type`** like a **fixed costume** 🎭
  → Once defined, it’s mostly **final**.

At a high level, both help with **type safety**, but they are designed for **slightly different use cases**.

---

## Deep Explanation

### `interface`

- Primarily used to describe **object shapes**
- Commonly used for:

  - Objects
  - Class contracts
  - Public APIs

- Supports **extension**
- Supports **declaration merging**

```ts
interface User {
  name: string;
}

interface User {
  age: number;
}
// Valid due to declaration merging
```

👉 This makes `interface` very useful in **large codebases and libraries**, where types may evolve over time.

---

### `type`

- More **flexible** and expressive
- Can represent:

  - Objects
  - Unions
  - Tuples
  - Primitives
  - Function signatures

- Does **not** support declaration merging

```ts
type Status = "loading" | "success" | "error";
```

👉 This makes `type` ideal for **state modeling, unions, and complex compositions**.

---

## When to Use What

| Scenario                  | Preferred   |
| ------------------------- | ----------- |
| Public APIs / libraries   | `interface` |
| Object shapes             | `interface` |
| Class contracts           | `interface` |
| Union or literal types    | `type`      |
| Tuples                    | `type`      |
| Complex type compositions | `type`      |

---

## Interview-Ready Answer

> Both `interface` and `type` are used to define types in TypeScript.
> I prefer `interface` for object shapes and class contracts because it’s extendable and supports declaration merging, which works well for scalable and public APIs.
> I use `type` when I need unions, tuples, or more complex type compositions, especially for state management and utility types.

---
