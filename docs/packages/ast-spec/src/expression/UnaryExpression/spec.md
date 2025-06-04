[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/UnaryExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `UnaryExpressionBase` | `../../base/UnaryExpressionBase` |


---


---

## Interfaces

### `UnaryExpression`

<details><summary>Interface Code</summary>

```ts
export interface UnaryExpression extends UnaryExpressionBase {
  type: AST_NODE_TYPES.UnaryExpression;
  operator: '!' | '+' | '-' | 'delete' | 'typeof' | 'void' | '~';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.UnaryExpression` | ✗ |  |
| `operator` | `'!' | '+' | '-' | 'delete' | 'typeof' | 'void' | '~'` | ✗ |  |


---