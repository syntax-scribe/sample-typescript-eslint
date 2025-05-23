[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-duplicate-enum-values.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-duplicate-enum-values.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Functions

### `isStringLiteral(node: TSESTree.Expression): node is TSESTree.StringLiteral`

<details><summary>Code</summary>

```ts
function isStringLiteral(
      node: TSESTree.Expression,
    ): node is TSESTree.StringLiteral {
      return (
        node.type === AST_NODE_TYPES.Literal && typeof node.value === 'string'
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `node is TSESTree.StringLiteral`
### `isNumberLiteral(node: TSESTree.Expression): node is TSESTree.NumberLiteral`

<details><summary>Code</summary>

```ts
function isNumberLiteral(
      node: TSESTree.Expression,
    ): node is TSESTree.NumberLiteral {
      return (
        node.type === AST_NODE_TYPES.Literal && typeof node.value === 'number'
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `node is TSESTree.NumberLiteral`
### `isStaticTemplateLiteral(node: TSESTree.Expression): node is TSESTree.TemplateLiteral`

<details><summary>Code</summary>

```ts
function isStaticTemplateLiteral(
      node: TSESTree.Expression,
    ): node is TSESTree.TemplateLiteral {
      return (
        node.type === AST_NODE_TYPES.TemplateLiteral &&
        node.expressions.length === 0 &&
        node.quasis.length === 1
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `node is TSESTree.TemplateLiteral`

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