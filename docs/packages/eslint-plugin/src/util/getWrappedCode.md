[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getWrappedCode.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/getWrappedCode.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `OperatorPrecedence` | `./getOperatorPrecedence` |


---

## Functions

### `getWrappedCode(text: string, nodePrecedence: OperatorPrecedence, parentPrecedence: OperatorPrecedence): string`

<details><summary>Code</summary>

```ts
export function getWrappedCode(
  text: string,
  nodePrecedence: OperatorPrecedence,
  parentPrecedence: OperatorPrecedence,
): string {
  return nodePrecedence > parentPrecedence ? text : `(${text})`;
}
```
</details>

- **Parameters**:
  - `text: string`
  - `nodePrecedence: OperatorPrecedence`
  - `parentPrecedence: OperatorPrecedence`
- **Return Type**: `string`

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