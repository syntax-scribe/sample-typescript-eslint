[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isNodeEqual.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/isNodeEqual.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |


---

## Functions

### `isNodeEqual(a: TSESTree.Node, b: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
export function isNodeEqual(a: TSESTree.Node, b: TSESTree.Node): boolean {
  if (a.type !== b.type) {
    return false;
  }
  if (
    a.type === AST_NODE_TYPES.ThisExpression &&
    b.type === AST_NODE_TYPES.ThisExpression
  ) {
    return true;
  }
  if (a.type === AST_NODE_TYPES.Literal && b.type === AST_NODE_TYPES.Literal) {
    return a.value === b.value;
  }
  if (
    a.type === AST_NODE_TYPES.Identifier &&
    b.type === AST_NODE_TYPES.Identifier
  ) {
    return a.name === b.name;
  }
  if (
    a.type === AST_NODE_TYPES.MemberExpression &&
    b.type === AST_NODE_TYPES.MemberExpression
  ) {
    return (
      isNodeEqual(a.property, b.property) && isNodeEqual(a.object, b.object)
    );
  }
  return false;
}
```
</details>

- **Parameters**:
  - `a: TSESTree.Node`
  - `b: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isNodeEqual`

---