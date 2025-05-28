[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 7 |
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
📂 **`packages/ast-spec/src/jsx/JSXAttribute/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `JSXElement` | `../../expression/JSXElement/spec` |
| `JSXExpression` | `../../unions/JSXExpression` |
| `Literal` | `../../unions/Literal` |
| `JSXIdentifier` | `../JSXIdentifier/spec` |
| `JSXNamespacedName` | `../JSXNamespacedName/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Interfaces

### `JSXAttribute`

<details><summary>Interface Code</summary>

```ts
export interface JSXAttribute extends BaseNode {
  type: AST_NODE_TYPES.JSXAttribute;
  name: JSXIdentifier | JSXNamespacedName;
  value: JSXElement | JSXExpression | Literal | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.JSXAttribute` | ✗ |  |
| `name` | `JSXIdentifier | JSXNamespacedName` | ✗ |  |
| `value` | `JSXElement | JSXExpression | Literal | null` | ✗ |  |


---