[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `cloneDeeplyExcludesParent.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/cloneDeeplyExcludesParent.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `retv` | `T & object` | const | `{} as typeof x` | ✗ |


---

## Functions

### `cloneDeeplyExcludesParent(x: T): T`

<details><summary>Code</summary>

```ts
export function cloneDeeplyExcludesParent<T>(x: T): T {
  if (typeof x === 'object' && x != null) {
    if (Array.isArray(x)) {
      return x.map(cloneDeeplyExcludesParent) as T;
    }

    const retv = {} as typeof x;

    for (const key in x) {
      if (key !== 'parent' && Object.hasOwn(x, key)) {
        retv[key] = cloneDeeplyExcludesParent(x[key]);
      }
    }

    return retv;
  }

  return x;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Clones a given value deeply.
 * Note: This ignores `parent` property.
 */
```

- **Parameters**:
  - `x: T`
- **Return Type**: `T`
- **Calls**:
  - `Array.isArray`
  - `x.map`
  - `Object.hasOwn`
  - `cloneDeeplyExcludesParent`

---