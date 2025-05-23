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
📂 **`packages/ast-spec/src/token/RegularExpressionToken/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_TOKEN_TYPES` | `../../ast-token-types` |
| `BaseToken` | `../../base/BaseToken` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `RegularExpressionToken`

<details><summary>Interface Code</summary>

```ts
export interface RegularExpressionToken extends BaseToken {
  type: AST_TOKEN_TYPES.RegularExpression;
  regex: {
    flags: string;
    pattern: string;
  };
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_TOKEN_TYPES.RegularExpression` | ✗ |  |
| `regex` | `{
    flags: string;
    pattern: string;
  }` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---