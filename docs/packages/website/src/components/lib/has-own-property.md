[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `has-own-property.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/lib/has-own-property.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `hasOwnProperty(property: Key, object: Container): object is Container & Record<Key, unknown>`

<details><summary>Code</summary>

```ts
export function hasOwnProperty<
  Container extends object,
  Key extends PropertyKey,
>(
  property: Key,
  object: Container,
): object is Container & Record<Key, unknown> {
  return property in object;
}
```
</details>

- **Parameters**:
  - `property: Key`
  - `object: Container`
- **Return Type**: `object is Container & Record<Key, unknown>`

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