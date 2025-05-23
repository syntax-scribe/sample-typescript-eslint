[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 1
- **Type Aliases**: 0

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

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---