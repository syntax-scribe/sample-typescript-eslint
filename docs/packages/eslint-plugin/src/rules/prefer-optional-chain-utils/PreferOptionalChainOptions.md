[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `PreferOptionalChainOptions.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-optional-chain-utils/PreferOptionalChainOptions.ts`**

## 🔧 Functions

> No functions found in this file.


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