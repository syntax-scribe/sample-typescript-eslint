[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `PreferOptionalChainOptions.ts`

## 📚 Table of Contents

- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 1
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-optional-chain-utils/PreferOptionalChainOptions.ts`**

## 📦 Imports

> No imports found in this file.


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

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