[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `cloneDeeplyExcludesParent.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/cloneDeeplyExcludesParent.ts`**

## 📦 Imports

> No imports found in this file.


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---