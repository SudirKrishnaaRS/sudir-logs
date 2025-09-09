# React Testing - RTL + Jest

**basics you need to write and understand unit tests in React**.

---

## 🧪 1. What is RTL + Jest?

| Library                         | Purpose                                                                         |
| ------------------------------- | ------------------------------------------------------------------------------- |
| **Jest**                        | Test runner + mocking + assertion                                               |
| **React Testing Library (RTL)** | Test React components like a user would (by rendering UI and querying elements) |

---

## 🚀 2. Setup (usually pre-configured in Create React App / Next.js)

Install manually (if needed):

```bash
npm install --save-dev @testing-library/react @testing-library/jest-dom jest
```

---

## ⚙️ 3. Anatomy of a Test

```js
import { render, screen } from "@testing-library/react";
import MyComponent from "./MyComponent";

test("renders greeting message", () => {
  render(<MyComponent />);
  const greeting = screen.getByText(/hello world/i);
  expect(greeting).toBeInTheDocument();
});
```

---

## 🧰 4. Common RTL Utilities

| Function                | Purpose                                                               |
| ----------------------- | --------------------------------------------------------------------- |
| `render()`              | Mounts the React component for testing                                |
| `screen`                | Global access to DOM queries                                          |
| `fireEvent()`           | Simulates user events like click, change                              |
| `waitFor()` / `findBy*` | Waits for async updates like after `useEffect` or promises            |
| `act()`                 | Ensures all state updates are flushed (usually handled automatically) |

---

## 🔍 5. Common Queries

```js
screen.getByText("Submit"); // Must be in DOM
screen.queryByText("Submit"); // Returns null if not found
screen.findByText("Submit"); // Returns promise (for async)

screen.getByRole("button");
screen.getByLabelText("Username"); // For form fields
```

Use [Testing Playground](https://testing-playground.com/) to generate queries.

---

## 🔥 6. Jest Syntax Essentials

| Concept        | Syntax                                                              |
| -------------- | ------------------------------------------------------------------- |
| Define a test  | `test('desc', () => {})` or `it('desc', () => {})`                  |
| Group tests    | `describe('group', () => {})`                                       |
| Assertion      | `expect(value).toBe(...)`, `.toEqual(...)`, `.toContain(...)`, etc. |
| Mock function  | `jest.fn()`, `jest.mock(...)`                                       |
| Mock timer/API | `jest.useFakeTimers()`, `jest.spyOn(...)`                           |

---

## 🧪 7. Example: Button Click

```js
import { render, screen, fireEvent } from "@testing-library/react";
import Counter from "./Counter"; // simple component with a +1 button

test("increments count on click", () => {
  render(<Counter />);
  const button = screen.getByRole("button", { name: /increment/i });
  fireEvent.click(button);
  expect(screen.getByText("Count: 1")).toBeInTheDocument();
});
```

---

## 🧪 8. Example: Async Fetch

```js
test("shows user data after fetch", async () => {
  fetch.mockResolvedValueOnce({
    ok: true,
    json: async () => [{ id: 1, name: "Alice" }],
  });

  render(<UserList />);
  expect(await screen.findByText("Alice")).toBeInTheDocument();
});
```

---

## 🧼 9. Cleanup & Setup

- `afterEach(() => cleanup())` is automatic in RTL
- `jest.clearAllMocks()` to reset mocks between tests

---

## 📌 10. Cheatsheet Summary

```js
// Rendering
render(<Component />);

// Querying
screen.getByText("text");
screen.queryByRole("button");
await screen.findByLabelText("email");

// Asserting
expect(something).toBeInTheDocument();
expect(button).toBeDisabled();
expect(fn).toHaveBeenCalledTimes(1);

// Events
fireEvent.click(button);
fireEvent.change(input, { target: { value: "new" } });
```

---
