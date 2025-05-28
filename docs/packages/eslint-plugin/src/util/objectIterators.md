[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `objectIterators.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 2 |
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
📂 **`packages/eslint-plugin/src/util/objectIterators.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `values` | `Return[]` | const | `[]` | ✗ |
| `accumulator` | `Accumulator` | let/var | `initial` | ✗ |


---

## Functions

### `objectForEachKey(obj: T, callback: (key: keyof T) => void): void`

<details><summary>Code</summary>

```ts
export function objectForEachKey<T extends Record<string, unknown>>(
  obj: T,
  callback: (key: keyof T) => void,
): void {
  const keys = Object.keys(obj);
  for (const key of keys) {
    callback(key);
  }
}
```
</details>

- **Parameters**:
  - `obj: T`
  - `callback: (key: keyof T) => void`
- **Return Type**: `void`
- **Calls**:
  - `Object.keys`
  - `callback`
### `objectMapKey(obj: T, callback: (key: keyof T) => Return): Return[]`

<details><summary>Code</summary>

```ts
export function objectMapKey<T extends Record<string, unknown>, Return>(
  obj: T,
  callback: (key: keyof T) => Return,
): Return[] {
  const values: Return[] = [];
  objectForEachKey(obj, key => {
    values.push(callback(key));
  });
  return values;
}
```
</details>

- **Parameters**:
  - `obj: T`
  - `callback: (key: keyof T) => Return`
- **Return Type**: `Return[]`
- **Calls**:
  - `objectForEachKey`
  - `values.push`
  - `callback`
### `objectReduceKey(obj: T, callback: (acc: Accumulator, key: keyof T) => Accumulator, initial: Accumulator): Accumulator`

<details><summary>Code</summary>

```ts
export function objectReduceKey<T extends Record<string, unknown>, Accumulator>(
  obj: T,
  callback: (acc: Accumulator, key: keyof T) => Accumulator,
  initial: Accumulator,
): Accumulator {
  let accumulator = initial;
  objectForEachKey(obj, key => {
    accumulator = callback(accumulator, key);
  });
  return accumulator;
}
```
</details>

- **Parameters**:
  - `obj: T`
  - `callback: (acc: Accumulator, key: keyof T) => Accumulator`
  - `initial: Accumulator`
- **Return Type**: `Accumulator`
- **Calls**:
  - `objectForEachKey`
  - `callback`

---