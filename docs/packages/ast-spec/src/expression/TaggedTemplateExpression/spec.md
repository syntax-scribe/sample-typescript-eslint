[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

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