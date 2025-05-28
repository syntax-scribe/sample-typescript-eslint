[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-duplicate-enum-values.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 3 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-duplicate-enum-values.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `enumMembers` | `any` | const | `node.body.members` | ✗ |
| `seenValues` | `Set<string | number>` | const | `new Set<number | string>()` | ✗ |
| `value` | `number | string | undefined` | let/var | `*not shown*` | ✗ |


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