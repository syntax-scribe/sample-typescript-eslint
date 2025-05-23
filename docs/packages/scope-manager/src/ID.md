[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `ID.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/src/ID.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `createIdGenerator(): () => number`

<details><summary>Code</summary>

```ts
export function createIdGenerator(): () => number {
  const key = (NEXT_KEY += 1);
  ID_CACHE.set(key, 0);

  return (): number => {
    const current = ID_CACHE.get(key) ?? 0;
    const next = current + 1;
    ID_CACHE.set(key, next);
    return next;
  };
}
```
</details>

- **Return Type**: `() => number`
- **Calls**:
  - `ID_CACHE.set`
  - `ID_CACHE.get`
### `resetIds(): void`

<details><summary>Code</summary>

```ts
export function resetIds(): void {
  ID_CACHE.clear();
}
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `ID_CACHE.clear`

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