[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getValueOfLiteralType.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/getValueOfLiteralType.ts`**

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