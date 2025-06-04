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
📂 **`packages/ast-spec/src/parameter/ArrayPattern/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Decorator` | `../../special/Decorator/spec` |
| `TSTypeAnnotation` | `../../special/TSTypeAnnotation/spec` |
| `DestructuringPattern` | `../../unions/DestructuringPattern` |


---

## Interfaces

### `ArrayPattern`

<details><summary>Interface Code</summary>

```ts
export interface ArrayPattern extends BaseNode {
  type: AST_NODE_TYPES.ArrayPattern;
  decorators: Decorator[];
  elements: (DestructuringPattern | null)[];
  optional: boolean;
  typeAnnotation: TSTypeAnnotation | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ArrayPattern` | ✗ |  |
| `decorators` | `Decorator[]` | ✗ |  |
| `elements` | `(DestructuringPattern | null)[]` | ✗ |  |
| `optional` | `boolean` | ✗ |  |
| `typeAnnotation` | `TSTypeAnnotation | undefined` | ✗ |  |


---