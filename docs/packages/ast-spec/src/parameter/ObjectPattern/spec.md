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
📂 **`packages/ast-spec/src/parameter/ObjectPattern/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Property` | `../../element/Property/spec` |
| `Decorator` | `../../special/Decorator/spec` |
| `TSTypeAnnotation` | `../../special/TSTypeAnnotation/spec` |
| `RestElement` | `../RestElement/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `ObjectPattern`

<details><summary>Interface Code</summary>

```ts
export interface ObjectPattern extends BaseNode {
  type: AST_NODE_TYPES.ObjectPattern;
  decorators: Decorator[];
  optional: boolean;
  properties: (Property | RestElement)[];
  typeAnnotation: TSTypeAnnotation | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ObjectPattern` | ✗ |  |
| `decorators` | `Decorator[]` | ✗ |  |
| `optional` | `boolean` | ✗ |  |
| `properties` | `(Property | RestElement)[]` | ✗ |  |
| `typeAnnotation` | `TSTypeAnnotation | undefined` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---