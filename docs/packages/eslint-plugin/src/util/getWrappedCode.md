[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getWrappedCode.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

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