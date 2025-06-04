[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `predicates.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 8 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/utils/src/ast-utils/predicates.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `../ts-estree` |
| `AST_NODE_TYPES` | `../ts-estree` |
| `AST_TOKEN_TYPES` | `../ts-estree` |
| `isNodeOfType` | `./helpers` |
| `isNodeOfTypes` | `./helpers` |
| `isNodeOfTypeWithConditions` | `./helpers` |
| `isNotTokenOfTypeWithConditions` | `./helpers` |
| `isTokenOfTypeWithConditions` | `./helpers` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `functionTypes` | `readonly [any, any, any]` | const | `[
  AST_NODE_TYPES.ArrowFunctionExpression,
  AST_NODE_TYPES.FunctionDeclaration,
  AST_NODE_TYPES.FunctionExpression,
] as const` | ✗ |
| `functionTypeTypes` | `readonly [any, any, any, any, any, any, any]` | const | `[
  AST_NODE_TYPES.TSCallSignatureDeclaration,
  AST_NODE_TYPES.TSConstructorType,
  AST_NODE_TYPES.TSConstructSignatureDeclaration,
  AST_NODE_TYPES.TSDeclareFunction,
  AST_NODE_TYPES.TSEmptyBodyFunctionExpression,
  AST_NODE_TYPES.TSFunctionType,
  AST_NODE_TYPES.TSMethodSignature,
] as const` | ✗ |


---

## Functions

### `isSetter(node: TSESTree.Node | undefined): node is { kind: 'set' } & (TSESTree.MethodDefinition | TSESTree.Property)`

<details><summary>Code</summary>

```ts
export function isSetter(
  node: TSESTree.Node | undefined,
): node is { kind: 'set' } & (TSESTree.MethodDefinition | TSESTree.Property) {
  return (
    !!node &&
    (node.type === AST_NODE_TYPES.MethodDefinition ||
      node.type === AST_NODE_TYPES.Property) &&
    node.kind === 'set'
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if a node is a setter method.
 */
```

- **Parameters**:
  - `node: TSESTree.Node | undefined`
- **Return Type**: `node is { kind: 'set' } & (TSESTree.MethodDefinition | TSESTree.Property)`

---