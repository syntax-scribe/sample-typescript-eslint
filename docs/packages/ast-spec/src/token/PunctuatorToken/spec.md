[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 🔄 Re-exports | 1 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Re-exports](#re-exports)
- [Interfaces](#interfaces)

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

## Re-exports

| Type | Source | Exported Names |
|------|--------|----------------|
| namespace | `./PunctuatorTokenToText` | * |


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