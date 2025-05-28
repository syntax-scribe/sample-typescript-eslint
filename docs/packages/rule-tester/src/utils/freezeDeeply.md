[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `freezeDeeply.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

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