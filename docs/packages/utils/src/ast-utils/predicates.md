[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `predicates.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 8
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---