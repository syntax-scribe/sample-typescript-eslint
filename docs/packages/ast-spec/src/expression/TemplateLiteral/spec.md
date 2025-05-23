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
📂 **`packages/ast-spec/src/expression/TemplateLiteral/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TemplateElement` | `../../special/TemplateElement/spec` |
| `Expression` | `../../unions/Expression` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TemplateLiteral`

<details><summary>Interface Code</summary>

```ts
export interface TemplateLiteral extends BaseNode {
  type: AST_NODE_TYPES.TemplateLiteral;
  expressions: Expression[];
  quasis: TemplateElement[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TemplateLiteral` | ✗ |  |
| `expressions` | `Expression[]` | ✗ |  |
| `quasis` | `TemplateElement[]` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---