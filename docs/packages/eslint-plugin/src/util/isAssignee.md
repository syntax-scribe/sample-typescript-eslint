[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isAssignee.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/isAssignee.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `parent` | `any` | const | `node.parent` | ✗ |


---

## Functions

### `isAssignee(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
export function isAssignee(node: TSESTree.Node): boolean {
  const parent = node.parent;
  if (!parent) {
    return false;
  }

  // a[i] = 1, a[i] += 1, etc.
  if (
    parent.type === AST_NODE_TYPES.AssignmentExpression &&
    parent.left === node
  ) {
    return true;
  }

  // delete a[i]
  if (
    parent.type === AST_NODE_TYPES.UnaryExpression &&
    parent.operator === 'delete' &&
    parent.argument === node
  ) {
    return true;
  }

  // a[i]++, --a[i], etc.
  if (
    parent.type === AST_NODE_TYPES.UpdateExpression &&
    parent.argument === node
  ) {
    return true;
  }

  // [a[i]] = [0]
  if (parent.type === AST_NODE_TYPES.ArrayPattern) {
    return true;
  }

  // [...a[i]] = [0]
  if (parent.type === AST_NODE_TYPES.RestElement) {
    return true;
  }

  // ({ foo: a[i] }) = { foo: 0 }
  if (
    parent.type === AST_NODE_TYPES.Property &&
    parent.value === node &&
    parent.parent.type === AST_NODE_TYPES.ObjectExpression &&
    isAssignee(parent.parent)
  ) {
    return true;
  }

  // (a[i] as number)++, [...a[i]!] = [0], etc.
  if (
    (parent.type === AST_NODE_TYPES.TSNonNullExpression ||
      parent.type === AST_NODE_TYPES.TSAsExpression ||
      parent.type === AST_NODE_TYPES.TSTypeAssertion ||
      parent.type === AST_NODE_TYPES.TSSatisfiesExpression) &&
    isAssignee(parent)
  ) {
    return true;
  }

  return false;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isAssignee`
- **Internal Comments**:
```
// a[i] = 1, a[i] += 1, etc.
// delete a[i]
// a[i]++, --a[i], etc.
// [a[i]] = [0]
// [...a[i]] = [0]
// ({ foo: a[i] }) = { foo: 0 }
// (a[i] as number)++, [...a[i]!] = [0], etc.
```


---