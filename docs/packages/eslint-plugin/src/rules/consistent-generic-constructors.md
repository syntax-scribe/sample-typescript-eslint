[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `consistent-generic-constructors.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/consistent-generic-constructors.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |


---

## Functions

### `getLHSRHS(): [
          (
            | TSESTree.AccessorProperty
            | TSESTree.BindingName
            | TSESTree.PropertyDefinition
          ),
          TSESTree.Expression | null,
        ]`

<details><summary>Code</summary>

```ts
function getLHSRHS(): [
          (
            | TSESTree.AccessorProperty
            | TSESTree.BindingName
            | TSESTree.PropertyDefinition
          ),
          TSESTree.Expression | null,
        ] {
          switch (node.type) {
            case AST_NODE_TYPES.VariableDeclarator:
              return [node.id, node.init];
            case AST_NODE_TYPES.PropertyDefinition:
            case AST_NODE_TYPES.AccessorProperty:
              return [node, node.value];
            case AST_NODE_TYPES.AssignmentPattern:
              return [node.left, node.right];
            default:
              throw new Error(
                `Unhandled node type: ${(node as { type: string }).type}`,
              );
          }
        }
```
</details>

- **Return Type**: `[
          (
            | TSESTree.AccessorProperty
            | TSESTree.BindingName
            | TSESTree.PropertyDefinition
          ),
          TSESTree.Expression | null,
        ]`
### `getIDToAttachAnnotation(): | TSESTree.Node
                  | TSESTree.Token`

<details><summary>Code</summary>

```ts
function getIDToAttachAnnotation():
                  | TSESTree.Node
                  | TSESTree.Token {
                  if (
                    node.type !== AST_NODE_TYPES.PropertyDefinition &&
                    node.type !== AST_NODE_TYPES.AccessorProperty
                  ) {
                    return lhsName;
                  }
                  if (!node.computed) {
                    return node.key;
                  }
                  // If the property's computed, we have to attach the
                  // annotation after the square bracket, not the enclosed expression
                  return nullThrows(
                    context.sourceCode.getTokenAfter(node.key),
                    NullThrowsReasons.MissingToken(']', 'key'),
                  );
                }
```
</details>

- **Return Type**: `| TSESTree.Node
                  | TSESTree.Token`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getTokenAfter`
  - `NullThrowsReasons.MissingToken`
- **Internal Comments**:
```
// If the property's computed, we have to attach the
// annotation after the square bracket, not the enclosed expression
```


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = 'preferConstructor' | 'preferTypeAnnotation';
```

### `Options`

```ts
type Options = ['constructor' | 'type-annotation'];
```


---