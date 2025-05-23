[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isHigherPrecedenceThanAwait.ts`

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
📂 **`packages/eslint-plugin/src/util/isHigherPrecedenceThanAwait.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `getOperatorPrecedence` | `./getOperatorPrecedence` |


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---