[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `debounce.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/components/lib/debounce.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `timeout` | `any` | let/var | `*not shown*` | ✗ |


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