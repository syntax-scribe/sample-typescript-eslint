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
📂 **`packages/ast-spec/src/special/ClassBody/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `ClassElement` | `../../unions/ClassElement` |


---

## Interfaces

### `ClassBody`

<details><summary>Interface Code</summary>

```ts
export interface ClassBody extends BaseNode {
  type: AST_NODE_TYPES.ClassBody;
  body: ClassElement[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ClassBody` | ✗ |  |
| `body` | `ClassElement[]` | ✗ |  |


---