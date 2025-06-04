[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/token/JSXTextToken/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_TOKEN_TYPES` | `../../ast-token-types` |
| `BaseToken` | `../../base/BaseToken` |


---

## Interfaces

### `JSXTextToken`

<details><summary>Interface Code</summary>

```ts
export interface JSXTextToken extends BaseToken {
  type: AST_TOKEN_TYPES.JSXText;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_TOKEN_TYPES.JSXText` | ✗ |  |


---