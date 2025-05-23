[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `freezeDeeply.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/freezeDeeply.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `freezeDeeply(x: unknown): void`

<details><summary>Code</summary>

```ts
export function freezeDeeply(x: unknown): void {
  if (typeof x === 'object' && x != null) {
    if (Array.isArray(x)) {
      x.forEach(freezeDeeply);
    } else {
      for (const key in x) {
        if (key !== 'parent' && Object.hasOwn(x, key)) {
          freezeDeeply((x as Record<string, unknown>)[key]);
        }
      }
    }
    Object.freeze(x);
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Freezes a given value deeply.
 */
```

- **Parameters**:
  - `x: unknown`
- **Return Type**: `void`
- **Calls**:
  - `Array.isArray`
  - `x.forEach`
  - `Object.hasOwn`
  - `freezeDeeply`
  - `Object.freeze`

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