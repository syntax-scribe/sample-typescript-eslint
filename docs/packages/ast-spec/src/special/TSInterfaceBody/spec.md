[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/special/TSInterfaceBody/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TypeElement` | `../../unions/TypeElement` |


---

## Interfaces

### `TSInterfaceBody`

<details><summary>Interface Code</summary>

```ts
export interface TSInterfaceBody extends BaseNode {
  type: AST_NODE_TYPES.TSInterfaceBody;
  body: TypeElement[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSInterfaceBody` | ✗ |  |
| `body` | `TypeElement[]` | ✗ |  |


---