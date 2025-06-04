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
📂 **`packages/ast-spec/src/parameter/RestElement/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Decorator` | `../../special/Decorator/spec` |
| `TSTypeAnnotation` | `../../special/TSTypeAnnotation/spec` |
| `DestructuringPattern` | `../../unions/DestructuringPattern` |
| `AssignmentPattern` | `../AssignmentPattern/spec` |


---

## Interfaces

### `RestElement`

<details><summary>Interface Code</summary>

```ts
export interface RestElement extends BaseNode {
  type: AST_NODE_TYPES.RestElement;
  argument: DestructuringPattern;
  decorators: Decorator[];
  optional: boolean;
  typeAnnotation: TSTypeAnnotation | undefined;
  value: AssignmentPattern | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.RestElement` | ✗ |  |
| `argument` | `DestructuringPattern` | ✗ |  |
| `decorators` | `Decorator[]` | ✗ |  |
| `optional` | `boolean` | ✗ |  |
| `typeAnnotation` | `TSTypeAnnotation | undefined` | ✗ |  |
| `value` | `AssignmentPattern | undefined` | ✗ |  |


---