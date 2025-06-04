[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `BaseToken.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/BaseToken.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_TOKEN_TYPES` | `../ast-token-types` |
| `NodeOrTokenData` | `./NodeOrTokenData` |


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