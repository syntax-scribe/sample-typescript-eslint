[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/Identifier/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Decorator` | `../../special/Decorator/spec` |
| `TSTypeAnnotation` | `../../special/TSTypeAnnotation/spec` |


---

## Interfaces

### `Identifier`

<details><summary>Interface Code</summary>

```ts
export interface Identifier extends BaseNode {
  type: AST_NODE_TYPES.Identifier;
  decorators: Decorator[];
  name: string;
  optional: boolean;
  typeAnnotation: TSTypeAnnotation | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.Identifier` | ✗ |  |
| `decorators` | `Decorator[]` | ✗ |  |
| `name` | `string` | ✗ |  |
| `optional` | `boolean` | ✗ |  |
| `typeAnnotation` | `TSTypeAnnotation | undefined` | ✗ |  |


---