[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `deepMerge.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 6 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/utils/src/eslint-utils/deepMerge.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `keys` | `Set<string>` | const | `new Set([...Object.keys(first), ...Object.keys(second)])` | ✗ |
| `firstHasKey` | `boolean` | const | `key in first` | ✗ |
| `secondHasKey` | `boolean` | const | `key in second` | ✗ |
| `firstValue` | `unknown` | const | `first[key]` | ✗ |
| `secondValue` | `unknown` | const | `second[key]` | ✗ |
| `value` | `any` | let/var | `*not shown*` | ✗ |


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

## Type Aliases

### `ObjectLike<T = unknown = unknown>`

```ts
type ObjectLike<T = unknown = unknown> = Record<string, T>;
```


---