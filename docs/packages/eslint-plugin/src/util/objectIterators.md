[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `objectIterators.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/objectIterators.ts`**

## 📦 Imports

> No imports found in this file.


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---