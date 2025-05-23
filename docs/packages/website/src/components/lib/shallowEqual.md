[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `shallowEqual.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/lib/shallowEqual.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `shallowEqual(object1: T | null | undefined, object2: T | null | undefined): boolean`

<details><summary>Code</summary>

```ts
export function shallowEqual<T extends Record<PropertyKey, unknown>>(
  object1: T | null | undefined,
  object2: T | null | undefined,
): boolean {
  if (object1 === object2) {
    return true;
  }
  const keys1 = Object.keys(object1 ?? {});
  const keys2 = Object.keys(object2 ?? {});
  if (keys1.length !== keys2.length) {
    return false;
  }
  for (const key of keys1) {
    // We'd love to be all proper and use a type predicate earlier, but:
    // https://github.com/microsoft/TypeScript/issues/26916
    // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
    if (object1![key] !== object2![key]) {
      return false;
    }
  }
  return true;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Shallowly compare two objects.
 */
```

- **Parameters**:
  - `object1: T | null | undefined`
  - `object2: T | null | undefined`
- **Return Type**: `boolean`
- **Calls**:
  - `Object.keys`
- **Internal Comments**:
```
// We'd love to be all proper and use a type predicate earlier, but:
// https://github.com/microsoft/TypeScript/issues/26916
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion
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