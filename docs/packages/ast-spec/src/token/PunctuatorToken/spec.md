[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/token/PunctuatorToken/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_TOKEN_TYPES` | `../../ast-token-types` |
| `BaseToken` | `../../base/BaseToken` |
| `ValueOf` | `../../utils` |
| `PunctuatorTokenToText` | `./PunctuatorTokenToText` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `PunctuatorToken`

<details><summary>Interface Code</summary>

```ts
export interface PunctuatorToken extends BaseToken {
  type: AST_TOKEN_TYPES.Punctuator;
  value: ValueOf<PunctuatorTokenToText>;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_TOKEN_TYPES.Punctuator` | ✗ |  |
| `value` | `ValueOf<PunctuatorTokenToText>` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---