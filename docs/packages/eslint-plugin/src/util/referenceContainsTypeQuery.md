[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `referenceContainsTypeQuery.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/referenceContainsTypeQuery.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |


---

## Functions

### `referenceContainsTypeQuery(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
export function referenceContainsTypeQuery(node: TSESTree.Node): boolean {
  switch (node.type) {
    case AST_NODE_TYPES.TSTypeQuery:
      return true;

    case AST_NODE_TYPES.TSQualifiedName:
    case AST_NODE_TYPES.Identifier:
      return referenceContainsTypeQuery(node.parent);

    default:
      // if we find a different node, there's no chance that we're in a TSTypeQuery
      return false;
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Recursively checks whether a given reference has a type query declaration among its parents
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `referenceContainsTypeQuery`
- **Internal Comments**:
```
// if we find a different node, there's no chance that we're in a TSTypeQuery
```


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