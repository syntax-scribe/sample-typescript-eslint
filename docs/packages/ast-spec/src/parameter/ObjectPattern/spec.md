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