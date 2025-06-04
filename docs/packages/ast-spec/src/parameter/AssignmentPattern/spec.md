[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 6 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/parameter/AssignmentPattern/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Decorator` | `../../special/Decorator/spec` |
| `TSTypeAnnotation` | `../../special/TSTypeAnnotation/spec` |
| `BindingName` | `../../unions/BindingName` |
| `Expression` | `../../unions/Expression` |


---

## Interfaces

### `AssignmentPattern`

<details><summary>Interface Code</summary>

```ts
export interface AssignmentPattern extends BaseNode {
  type: AST_NODE_TYPES.AssignmentPattern;
  decorators: Decorator[];
  left: BindingName;
  optional: boolean;
  right: Expression;
  typeAnnotation: TSTypeAnnotation | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.AssignmentPattern` | ✗ |  |
| `decorators` | `Decorator[]` | ✗ |  |
| `left` | `BindingName` | ✗ |  |
| `optional` | `boolean` | ✗ |  |
| `right` | `Expression` | ✗ |  |
| `typeAnnotation` | `TSTypeAnnotation | undefined` | ✗ |  |


---