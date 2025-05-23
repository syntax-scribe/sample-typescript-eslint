[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `BaseToken.ts`

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
📂 **`packages/ast-spec/src/base/BaseToken.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_TOKEN_TYPES` | `../ast-token-types` |
| `NodeOrTokenData` | `./NodeOrTokenData` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `BaseToken`

<details><summary>Interface Code</summary>

```ts
export interface BaseToken extends NodeOrTokenData {
  type: AST_TOKEN_TYPES;
  value: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_TOKEN_TYPES` | ✗ |  |
| `value` | `string` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---