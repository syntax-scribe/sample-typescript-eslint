[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `LiteralBase.ts`

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
📂 **`packages/ast-spec/src/base/LiteralBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../ast-node-types` |
| `BaseNode` | `./BaseNode` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `LiteralBase`

<details><summary>Interface Code</summary>

```ts
export interface LiteralBase extends BaseNode {
  type: AST_NODE_TYPES.Literal;
  raw: string;
  value: bigint | boolean | number | string | RegExp | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.Literal` | ✗ |  |
| `raw` | `string` | ✗ |  |
| `value` | `bigint | boolean | number | string | RegExp | null` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---