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
📂 **`packages/ast-spec/src/special/ImportDefaultSpecifier/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |


---

## Interfaces

### `ImportDefaultSpecifier`

<details><summary>Interface Code</summary>

```ts
export interface ImportDefaultSpecifier extends BaseNode {
  type: AST_NODE_TYPES.ImportDefaultSpecifier;
  local: Identifier;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ImportDefaultSpecifier` | ✗ |  |
| `local` | `Identifier` | ✗ |  |


---