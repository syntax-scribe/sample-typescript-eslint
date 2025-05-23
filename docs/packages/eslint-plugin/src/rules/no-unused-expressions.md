[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unused-expressions.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unused-expressions.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `InferMessageIdsTypeFromRule` | `../util` |
| `InferOptionsTypeFromRule` | `../util` |
| `createRule` | `../util` |
| `getESLintCoreRule` | `../util/getESLintCoreRule` |


---

## Functions

### `isValidExpression(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isValidExpression(node: TSESTree.Node): boolean {
      if (allowShortCircuit && node.type === AST_NODE_TYPES.LogicalExpression) {
        return isValidExpression(node.right);
      }
      if (allowTernary && node.type === AST_NODE_TYPES.ConditionalExpression) {
        return (
          isValidExpression(node.alternate) &&
          isValidExpression(node.consequent)
        );
      }
      return (
        (node.type === AST_NODE_TYPES.ChainExpression &&
          node.expression.type === AST_NODE_TYPES.CallExpression) ||
        node.type === AST_NODE_TYPES.ImportExpression
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isValidExpression`

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
type MessageIds = InferMessageIdsTypeFromRule<typeof baseRule>;
```

### `Options`

```ts
type Options = InferOptionsTypeFromRule<typeof baseRule>;
```


---