[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `PreferOptionalChainOptions.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-optional-chain-utils/PreferOptionalChainOptions.ts`**

## Interfaces

### `PreferOptionalChainOptions`

<details><summary>Interface Code</summary>

```ts
export interface PreferOptionalChainOptions {
  allowPotentiallyUnsafeFixesThatModifyTheReturnTypeIKnowWhatImDoing?: boolean;
  checkAny?: boolean;
  checkBigInt?: boolean;
  checkBoolean?: boolean;
  checkNumber?: boolean;
  checkString?: boolean;
  checkUnknown?: boolean;
  requireNullish?: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `allowPotentiallyUnsafeFixesThatModifyTheReturnTypeIKnowWhatImDoing` | `boolean` | ✓ |  |
| `checkAny` | `boolean` | ✓ |  |
| `checkBigInt` | `boolean` | ✓ |  |
| `checkBoolean` | `boolean` | ✓ |  |
| `checkNumber` | `boolean` | ✓ |  |
| `checkString` | `boolean` | ✓ |  |
| `checkUnknown` | `boolean` | ✓ |  |
| `requireNullish` | `boolean` | ✓ |  |


---

## Type Aliases

### `PreferOptionalChainMessageIds`

```ts
type PreferOptionalChainMessageIds = | 'optionalChainSuggest'
  | 'preferOptionalChain';
```


---