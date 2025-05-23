[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/jsx/JSXNamespacedName/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `JSXIdentifier` | `../JSXIdentifier/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `JSXNamespacedName`

<details><summary>Interface Code</summary>

```ts
export interface JSXNamespacedName extends BaseNode {
  type: AST_NODE_TYPES.JSXNamespacedName;
  name: JSXIdentifier;
  namespace: JSXIdentifier;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.JSXNamespacedName` | ✗ |  |
| `name` | `JSXIdentifier` | ✗ |  |
| `namespace` | `JSXIdentifier` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---