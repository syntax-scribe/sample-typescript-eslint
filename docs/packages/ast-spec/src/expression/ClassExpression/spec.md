[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/ClassExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `ClassBase` | `../../base/ClassBase` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `ClassExpression`

<details><summary>Interface Code</summary>

```ts
export interface ClassExpression extends ClassBase {
  type: AST_NODE_TYPES.ClassExpression;
  abstract: false;
  declare: false;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ClassExpression` | ✗ |  |
| `abstract` | `false` | ✗ |  |
| `declare` | `false` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---