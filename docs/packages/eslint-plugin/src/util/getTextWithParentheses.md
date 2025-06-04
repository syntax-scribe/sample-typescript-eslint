[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getTextWithParentheses.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 7 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/getTextWithParentheses.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `SourceCode` | `@typescript-eslint/utils/ts-eslint` |
| `isClosingParenToken` | `.` |
| `isOpeningParenToken` | `.` |
| `isParenthesized` | `.` |
| `nullThrows` | `.` |
| `NullThrowsReasons` | `.` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `beforeCount` | `number` | let/var | `0` | ✗ |
| `afterCount` | `number` | let/var | `0` | ✗ |


---

## Functions

### `getTextWithParentheses(sourceCode: Readonly<SourceCode>, node: TSESTree.Node): string`

<details><summary>Code</summary>

```ts
export function getTextWithParentheses(
  sourceCode: Readonly<SourceCode>,
  node: TSESTree.Node,
): string {
  // Capture parentheses before and after the node
  let beforeCount = 0;
  let afterCount = 0;

  if (isParenthesized(node, sourceCode)) {
    const bodyOpeningParen = nullThrows(
      sourceCode.getTokenBefore(node, isOpeningParenToken),
      NullThrowsReasons.MissingToken('(', 'node'),
    );
    const bodyClosingParen = nullThrows(
      sourceCode.getTokenAfter(node, isClosingParenToken),
      NullThrowsReasons.MissingToken(')', 'node'),
    );

    beforeCount = node.range[0] - bodyOpeningParen.range[0];
    afterCount = bodyClosingParen.range[1] - node.range[1];
  }

  return sourceCode.getText(node, beforeCount, afterCount);
}
```
</details>

- **Parameters**:
  - `sourceCode: Readonly<SourceCode>`
  - `node: TSESTree.Node`
- **Return Type**: `string`
- **Calls**:
  - `isParenthesized (from .)`
  - `nullThrows (from .)`
  - `sourceCode.getTokenBefore`
  - `NullThrowsReasons.MissingToken`
  - `sourceCode.getTokenAfter`
  - `sourceCode.getText`
- **Internal Comments**:
```
// Capture parentheses before and after the node (x2)
```


---