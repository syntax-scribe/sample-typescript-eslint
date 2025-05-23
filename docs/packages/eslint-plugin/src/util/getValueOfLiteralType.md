[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getValueOfLiteralType.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/getValueOfLiteralType.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `valueIsPseudoBigInt(value: number | string | ts.PseudoBigInt): value is ts.PseudoBigInt`

<details><summary>Code</summary>

```ts
(
  value: number | string | ts.PseudoBigInt,
): value is ts.PseudoBigInt => {
  return typeof value === 'object';
}
```
</details>

- **Parameters**:
  - `value: number | string | ts.PseudoBigInt`
- **Return Type**: `value is ts.PseudoBigInt`
### `pseudoBigIntToBigInt(value: ts.PseudoBigInt): bigint`

<details><summary>Code</summary>

```ts
(value: ts.PseudoBigInt): bigint => {
  return BigInt((value.negative ? '-' : '') + value.base10Value);
}
```
</details>

- **Parameters**:
  - `value: ts.PseudoBigInt`
- **Return Type**: `bigint`
- **Calls**:
  - `BigInt`
### `getValueOfLiteralType(type: ts.LiteralType): bigint | number | string`

<details><summary>Code</summary>

```ts
(
  type: ts.LiteralType,
): bigint | number | string => {
  if (valueIsPseudoBigInt(type.value)) {
    return pseudoBigIntToBigInt(type.value);
  }
  return type.value;
}
```
</details>

- **Parameters**:
  - `type: ts.LiteralType`
- **Return Type**: `bigint | number | string`
- **Calls**:
  - `valueIsPseudoBigInt`
  - `pseudoBigIntToBigInt`

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