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

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---