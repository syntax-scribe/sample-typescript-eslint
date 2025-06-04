[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isHigherPrecedenceThanAwait.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/isHigherPrecedenceThanAwait.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `getOperatorPrecedence` | `./getOperatorPrecedence` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `operator` | `any` | const | `ts.isBinaryExpression(tsNode)
    ? tsNode.operatorToken.kind
    : ts.SyntaxKind.Unknown` | ✗ |


---

## Functions

### `isHigherPrecedenceThanAwait(tsNode: ts.Node): boolean`

<details><summary>Code</summary>

```ts
export function isHigherPrecedenceThanAwait(tsNode: ts.Node): boolean {
  const operator = ts.isBinaryExpression(tsNode)
    ? tsNode.operatorToken.kind
    : ts.SyntaxKind.Unknown;
  const nodePrecedence = getOperatorPrecedence(tsNode.kind, operator);
  const awaitPrecedence = getOperatorPrecedence(
    ts.SyntaxKind.AwaitExpression,
    ts.SyntaxKind.Unknown,
  );
  return nodePrecedence > awaitPrecedence;
}
```
</details>

- **Parameters**:
  - `tsNode: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `ts.isBinaryExpression`
  - `getOperatorPrecedence (from ./getOperatorPrecedence)`

---