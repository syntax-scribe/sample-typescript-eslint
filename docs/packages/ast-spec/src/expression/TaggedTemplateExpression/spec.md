[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/TaggedTemplateExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TSTypeParameterInstantiation` | `../../special/TSTypeParameterInstantiation/spec` |
| `Expression` | `../../unions/Expression` |
| `TemplateLiteral` | `../TemplateLiteral/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TaggedTemplateExpression`

<details><summary>Interface Code</summary>

```ts
export interface TaggedTemplateExpression extends BaseNode {
  type: AST_NODE_TYPES.TaggedTemplateExpression;
  quasi: TemplateLiteral;
  tag: Expression;
  typeArguments: TSTypeParameterInstantiation | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TaggedTemplateExpression` | ✗ |  |
| `quasi` | `TemplateLiteral` | ✗ |  |
| `tag` | `Expression` | ✗ |  |
| `typeArguments` | `TSTypeParameterInstantiation | undefined` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---