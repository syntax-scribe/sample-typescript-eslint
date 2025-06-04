[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isUndefinedIdentifier.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/isUndefinedIdentifier.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |


---

## Functions

### `isUndefinedIdentifier(i: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
export function isUndefinedIdentifier(i: TSESTree.Node): boolean {
  return i.type === AST_NODE_TYPES.Identifier && i.name === 'undefined';
}
```
</details>

- **Parameters**:
  - `i: TSESTree.Node`
- **Return Type**: `boolean`

---