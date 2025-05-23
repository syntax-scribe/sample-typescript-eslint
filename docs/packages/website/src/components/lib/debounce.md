[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `debounce.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/lib/debounce.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `debounce(func: (...args: X) => void, wait: number): (...args: X) => void`

<details><summary>Code</summary>

```ts
export function debounce<X extends unknown[]>(
  func: (...args: X) => void,
  wait: number,
): (...args: X) => void {
  // eslint-disable-next-line @typescript-eslint/no-explicit-any
  let timeout: any;
  return function (...args: X): void {
    // eslint-disable-next-line @typescript-eslint/no-unsafe-argument
    clearTimeout(timeout);
    timeout = setTimeout(() => {
      timeout = undefined;
      func(...args);
    }, wait);
  };
}
```
</details>

- **Parameters**:
  - `func: (...args: X) => void`
  - `wait: number`
- **Return Type**: `(...args: X) => void`
- **Calls**:
  - `clearTimeout`
  - `setTimeout`
  - `func`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-explicit-any (x2)
// eslint-disable-next-line @typescript-eslint/no-unsafe-argument (x3)
```


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---