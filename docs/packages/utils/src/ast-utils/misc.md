[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `misc.ts`

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
📂 **`packages/utils/src/ast-utils/misc.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `../ts-estree` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `LINEBREAK_MATCHER` | `RegExp` | const | `/\r\n|[\r\n\u2028\u2029]/` | ✓ |


---

## Functions

### `isTokenOnSameLine(left: TSESTree.Node | TSESTree.Token, right: TSESTree.Node | TSESTree.Token): boolean`

<details><summary>Code</summary>

```ts
export function isTokenOnSameLine(
  left: TSESTree.Node | TSESTree.Token,
  right: TSESTree.Node | TSESTree.Token,
): boolean {
  return left.loc.end.line === right.loc.start.line;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Determines whether two adjacent tokens are on the same line
 */
```

- **Parameters**:
  - `left: TSESTree.Node | TSESTree.Token`
  - `right: TSESTree.Node | TSESTree.Token`
- **Return Type**: `boolean`

---