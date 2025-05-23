[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-misused-new.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-misused-new.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Functions

### `getTypeReferenceName(node: | TSESTree.EntityName
        | TSESTree.TSTypeAnnotation
        | TSESTree.TypeNode
        | undefined): string | null`

<details><summary>Code</summary>

```ts
function getTypeReferenceName(
      node:
        | TSESTree.EntityName
        | TSESTree.TSTypeAnnotation
        | TSESTree.TypeNode
        | undefined,
    ): string | null {
      if (node) {
        switch (node.type) {
          case AST_NODE_TYPES.TSTypeAnnotation:
            return getTypeReferenceName(node.typeAnnotation);
          case AST_NODE_TYPES.TSTypeReference:
            return getTypeReferenceName(node.typeName);
          case AST_NODE_TYPES.Identifier:
            return node.name;
          default:
            break;
        }
      }
      return null;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * @param node type to be inspected.
     * @returns name of simple type or null
     */
```

- **Parameters**:
  - `node: | TSESTree.EntityName
        | TSESTree.TSTypeAnnotation
        | TSESTree.TypeNode
        | undefined`
- **Return Type**: `string | null`
- **Calls**:
  - `getTypeReferenceName`
### `isMatchingParentType(parent: | TSESTree.ClassDeclaration
        | TSESTree.ClassExpression
        | TSESTree.Identifier
        | TSESTree.TSInterfaceDeclaration
        | undefined, returnType: TSESTree.TSTypeAnnotation | undefined): boolean`

<details><summary>Code</summary>

```ts
function isMatchingParentType(
      parent:
        | TSESTree.ClassDeclaration
        | TSESTree.ClassExpression
        | TSESTree.Identifier
        | TSESTree.TSInterfaceDeclaration
        | undefined,
      returnType: TSESTree.TSTypeAnnotation | undefined,
    ): boolean {
      if (
        parent &&
        (parent.type === AST_NODE_TYPES.ClassDeclaration ||
          parent.type === AST_NODE_TYPES.ClassExpression ||
          parent.type === AST_NODE_TYPES.TSInterfaceDeclaration) &&
        parent.id
      ) {
        return getTypeReferenceName(returnType) === parent.id.name;
      }
      return false;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * @param parent parent node.
     * @param returnType type to be compared
     */
```

- **Parameters**:
  - `parent: | TSESTree.ClassDeclaration
        | TSESTree.ClassExpression
        | TSESTree.Identifier
        | TSESTree.TSInterfaceDeclaration
        | undefined`
  - `returnType: TSESTree.TSTypeAnnotation | undefined`
- **Return Type**: `boolean`
- **Calls**:
  - `getTypeReferenceName`

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