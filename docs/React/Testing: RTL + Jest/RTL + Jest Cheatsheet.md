# Complete RTL + Jest Cheatsheet

---

## 🧪 React Testing Library + Jest Cheatsheet

---

### 📦 Setup

```bash
npm install --save-dev @testing-library/react @testing-library/jest-dom jest
```

```js
// setupTests.js (if needed)
import "@testing-library/jest-dom";
```

---

### 🧱 Test Structure

```js
import { render, screen, fireEvent } from "@testing-library/react";
import MyComponent from "./MyComponent";

test("renders something", () => {
  render(<MyComponent />);
  const element = screen.getByText(/hello/i);
  expect(element).toBeInTheDocument();
});
```

---

### 📌 Setup & Teardown Hooks

| Hook           | Purpose                    |
| -------------- | -------------------------- |
| `beforeAll()`  | Runs once before all tests |
| `afterAll()`   | Runs once after all tests  |
| `beforeEach()` | Runs before each test      |
| `afterEach()`  | Runs after each test       |

#### Example:

```js
beforeAll(() => {
  // setup before all tests
});

afterAll(() => {
  // teardown after all tests
});

beforeEach(() => {
  jest.clearAllMocks();
});

afterEach(() => {
  // cleanup is automatic with RTL, but can be used explicitly
});
```

---

### 🔍 Common Queries

| Query                     | Description                   |
| ------------------------- | ----------------------------- |
| `getByText('text')`       | Returns element or throws     |
| `queryByText('text')`     | Returns `null` if not found   |
| `findByText('text')`      | Async version (Promise)       |
| `getByRole('button')`     | Finds by accessibility role   |
| `getByLabelText('Email')` | Finds input linked with label |
| `getAllByText('text')`    | Returns all matching elements |

📌 Tip: Use [https://testing-playground.com](https://testing-playground.com) to generate queries visually.

---

### ⚡ Events

```js
fireEvent.click(button);
fireEvent.change(input, { target: { value: "hello" } });
fireEvent.submit(form);
```

---

### 🧪 Assertions (via Jest + `jest-dom`)

```js
expect(element).toBeInTheDocument();
expect(button).toBeDisabled();
expect(input).toHaveValue("hello");
expect(mockFn).toHaveBeenCalledTimes(1);
```

---

### 🧪 Async / useEffect Tests

```js
test("loads user data", async () => {
  fetch.mockResolvedValueOnce({
    ok: true,
    json: async () => [{ id: 1, name: "Alice" }],
  });

  render(<UserList />);
  expect(await screen.findByText("Alice")).toBeInTheDocument();
});
```

---

### 🔁 Mock Functions

```js
const mockFn = jest.fn();
mockFn.mockReturnValue("Hello");
jest.spyOn(obj, "method").mockImplementation(() => {});
```

---

### 🧼 Best Practices

- Use `screen` instead of destructured queries.
- Prefer `findBy*` over `waitFor`.
- Use roles and labels over `getByTestId`.

---
