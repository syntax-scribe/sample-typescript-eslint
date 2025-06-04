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
📂 **`packages/ast-spec/src/special/TSTypeParameter/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |
| `TypeNode` | `../../unions/TypeNode` |


---

## Interfaces

### `TSTypeParameter`

<details><summary>Interface Code</summary>

```ts
export interface TSTypeParameter extends BaseNode {
  type: AST_NODE_TYPES.TSTypeParameter;
  const: boolean;
  constraint: TypeNode | undefined;
  default: TypeNode | undefined;
  in: boolean;
  name: Identifier;
  out: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSTypeParameter` | ✗ |  |
| `const` | `boolean` | ✗ |  |
| `constraint` | `TypeNode | undefined` | ✗ |  |
| `default` | `TypeNode | undefined` | ✗ |  |
| `in` | `boolean` | ✗ |  |
| `name` | `Identifier` | ✗ |  |
| `out` | `boolean` | ✗ |  |


---