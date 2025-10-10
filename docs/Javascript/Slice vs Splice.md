# Slice vs Splice

### **1️⃣ `slice()`**

- **Does NOT change the original array** (it’s **non-destructive**).
- **Creates a new array** with the selected elements.
- Syntax:

```js
arr.slice(startIndex, endIndex); // endIndex is not included
```

**Example:**

```js
const fruits = ["apple", "banana", "cherry", "date"];
const newFruits = fruits.slice(1, 3); // ['banana', 'cherry']
console.log(fruits); // ['apple', 'banana', 'cherry', 'date'] (unchanged)
```

---

### **2️⃣ `splice()`**

- **Changes the original array** (it’s **destructive**).
- Can **remove, replace, or add** elements in place.
- Syntax:

```js
arr.splice(startIndex, deleteCount, item1, item2, ...)
```

**Example:**

```js
const fruits = ["apple", "banana", "cherry", "date"];
fruits.splice(1, 2, "kiwi", "mango");
// start at index 1, remove 2 items, add 'kiwi' and 'mango'
console.log(fruits); // ['apple', 'kiwi', 'mango', 'date']
```

---
