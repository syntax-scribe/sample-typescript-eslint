[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `deepMerge.ts`

## 📚 Table of Contents

- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/utils/src/eslint-utils/deepMerge.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `isObjectNotArray(obj: unknown): obj is ObjectLike`

<details><summary>Code</summary>

```ts
export function isObjectNotArray(obj: unknown): obj is ObjectLike {
  return typeof obj === 'object' && obj != null && !Array.isArray(obj);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check if the variable contains an object strictly rejecting arrays
 * @returns `true` if obj is an object
 */
```

- **Parameters**:
  - `obj: unknown`
- **Return Type**: `obj is ObjectLike`
- **Calls**:
  - `Array.isArray`
### `deepMerge(first: ObjectLike, second: ObjectLike): Record<string, unknown>`

<details><summary>Code</summary>

```ts
export function deepMerge(
  first: ObjectLike = {},
  second: ObjectLike = {},
): Record<string, unknown> {
  // get the unique set of keys across both objects
  const keys = new Set([...Object.keys(first), ...Object.keys(second)]);

  return Object.fromEntries(
    [...keys].map(key => {
      const firstHasKey = key in first;
      const secondHasKey = key in second;
      const firstValue = first[key];
      const secondValue = second[key];

      let value;
      if (firstHasKey && secondHasKey) {
        if (isObjectNotArray(firstValue) && isObjectNotArray(secondValue)) {
          // object type
          value = deepMerge(firstValue, secondValue);
        } else {
          // value type
          value = secondValue;
        }
      } else if (firstHasKey) {
        value = firstValue;
      } else {
        value = secondValue;
      }
      return [key, value];
    }),
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Pure function - doesn't mutate either parameter!
 * Merges two objects together deeply, overwriting the properties in first with the properties in second
 * @param first The first object
 * @param second The second object
 * @returns a new object
 */
```

- **Parameters**:
  - `first: ObjectLike`
  - `second: ObjectLike`
- **Return Type**: `Record<string, unknown>`
- **Calls**:
  - `Object.keys`
  - `Object.fromEntries`
  - `[...keys].map`
  - `isObjectNotArray`
  - `deepMerge`
- **Internal Comments**:
```
// get the unique set of keys across both objects (x2)
// object type (x3)
// value type (x3)
```


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `ObjectLike<T = unknown = unknown>`

```ts
type ObjectLike<T = unknown = unknown> = Record<string, T>;
```


---