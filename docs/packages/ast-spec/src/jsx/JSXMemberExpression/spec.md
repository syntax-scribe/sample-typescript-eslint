[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
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
📂 **`packages/ast-spec/src/jsx/JSXMemberExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `JSXTagNameExpression` | `../../unions/JSXTagNameExpression` |
| `JSXIdentifier` | `../JSXIdentifier/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Interfaces

### `JSXMemberExpression`

<details><summary>Interface Code</summary>

```ts
export interface JSXMemberExpression extends BaseNode {
  type: AST_NODE_TYPES.JSXMemberExpression;
  object: JSXTagNameExpression;
  property: JSXIdentifier;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.JSXMemberExpression` | ✗ |  |
| `object` | `JSXTagNameExpression` | ✗ |  |
| `property` | `JSXIdentifier` | ✗ |  |


---