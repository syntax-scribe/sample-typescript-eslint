[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/type/TSTemplateLiteralType/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TemplateElement` | `../../special/TemplateElement/spec` |
| `TypeNode` | `../../unions/TypeNode` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TSTemplateLiteralType`

<details><summary>Interface Code</summary>

```ts
export interface TSTemplateLiteralType extends BaseNode {
  type: AST_NODE_TYPES.TSTemplateLiteralType;
  quasis: TemplateElement[];
  types: TypeNode[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSTemplateLiteralType` | ✗ |  |
| `quasis` | `TemplateElement[]` | ✗ |  |
| `types` | `TypeNode[]` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---