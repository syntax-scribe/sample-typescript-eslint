[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `freezeDeeply.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/freezeDeeply.ts`**

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