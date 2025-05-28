[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unused-expressions.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 2 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `defaultOptions` | `Options` | const | `[
  {
    allowShortCircuit: false,
    allowTaggedTemplates: false,
    allowTernary: false,
  },
]` | ✗ |
| `expressionType` | `any` | const | `node.expression.type` | ✗ |


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