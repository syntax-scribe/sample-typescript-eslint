[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `rangeToLoc.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/rangeToLoc.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |


---

## Functions

### `rangeToLoc(sourceCode: TSESLint.SourceCode, range: TSESLint.AST.Range): TSESTree.SourceLocation`

<details><summary>Code</summary>

```ts
export function rangeToLoc(
  sourceCode: TSESLint.SourceCode,
  range: TSESLint.AST.Range,
): TSESTree.SourceLocation {
  return {
    end: sourceCode.getLocFromIndex(range[1]),
    start: sourceCode.getLocFromIndex(range[0]),
  };
}
```
</details>

- **Parameters**:
  - `sourceCode: TSESLint.SourceCode`
  - `range: TSESLint.AST.Range`
- **Return Type**: `TSESTree.SourceLocation`
- **Calls**:
  - `sourceCode.getLocFromIndex`

---