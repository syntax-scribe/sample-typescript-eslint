[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `predicates.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 1 |
| 📊 Variables & Constants | 22 |
| 📑 Type Aliases | 5 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/utils/src/ast-utils/eslint-utils/predicates.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `../../ts-estree` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `isArrowToken` | `IsPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isArrowToken as IsPunctuatorTokenWithValueFunction<'=>'>` | ✓ |
| `isNotArrowToken` | `IsNotPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isNotArrowToken as IsNotPunctuatorTokenWithValueFunction<'=>'>` | ✓ |
| `isClosingBraceToken` | `IsPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isClosingBraceToken as IsPunctuatorTokenWithValueFunction<'}'>` | ✓ |
| `isNotClosingBraceToken` | `IsNotPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isNotClosingBraceToken as IsNotPunctuatorTokenWithValueFunction<'}'>` | ✓ |
| `isClosingBracketToken` | `IsPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isClosingBracketToken as IsPunctuatorTokenWithValueFunction<']'>` | ✓ |
| `isNotClosingBracketToken` | `IsNotPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isNotClosingBracketToken as IsNotPunctuatorTokenWithValueFunction<']'>` | ✓ |
| `isClosingParenToken` | `IsPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isClosingParenToken as IsPunctuatorTokenWithValueFunction<')'>` | ✓ |
| `isNotClosingParenToken` | `IsNotPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isNotClosingParenToken as IsNotPunctuatorTokenWithValueFunction<')'>` | ✓ |
| `isColonToken` | `IsPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isColonToken as IsPunctuatorTokenWithValueFunction<':'>` | ✓ |
| `isNotColonToken` | `IsNotPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isNotColonToken as IsNotPunctuatorTokenWithValueFunction<':'>` | ✓ |
| `isCommaToken` | `IsPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isCommaToken as IsPunctuatorTokenWithValueFunction<','>` | ✓ |
| `isNotCommaToken` | `IsNotPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isNotCommaToken as IsNotPunctuatorTokenWithValueFunction<','>` | ✓ |
| `isCommentToken` | `IsSpecificTokenFunction<TSESTree.Comment>` | const | `eslintUtils.isCommentToken as IsSpecificTokenFunction<TSESTree.Comment>` | ✓ |
| `isNotCommentToken` | `IsNotSpecificTokenFunction<TSESTree.Comment>` | const | `eslintUtils.isNotCommentToken as IsNotSpecificTokenFunction<TSESTree.Comment>` | ✓ |
| `isOpeningBraceToken` | `IsPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isOpeningBraceToken as IsPunctuatorTokenWithValueFunction<'{'>` | ✓ |
| `isNotOpeningBraceToken` | `IsNotPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isNotOpeningBraceToken as IsNotPunctuatorTokenWithValueFunction<'{'>` | ✓ |
| `isOpeningBracketToken` | `IsPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isOpeningBracketToken as IsPunctuatorTokenWithValueFunction<'['>` | ✓ |
| `isNotOpeningBracketToken` | `IsNotPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isNotOpeningBracketToken as IsNotPunctuatorTokenWithValueFunction<'['>` | ✓ |
| `isOpeningParenToken` | `IsPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isOpeningParenToken as IsPunctuatorTokenWithValueFunction<'('>` | ✓ |
| `isNotOpeningParenToken` | `IsNotPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isNotOpeningParenToken as IsNotPunctuatorTokenWithValueFunction<'('>` | ✓ |
| `isSemicolonToken` | `IsPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isSemicolonToken as IsPunctuatorTokenWithValueFunction<';'>` | ✓ |
| `isNotSemicolonToken` | `IsNotPunctuatorTokenWithValueFunction<Value>` | const | `eslintUtils.isNotSemicolonToken as IsNotPunctuatorTokenWithValueFunction<';'>` | ✓ |


---

## Type Aliases

### `IsSpecificTokenFunction<SpecificToken extends TSESTree.Token extends TSESTree.Token>`

```ts
type IsSpecificTokenFunction<SpecificToken extends TSESTree.Token extends TSESTree.Token> = (
  token: TSESTree.Token,
) => token is SpecificToken;
```

### `IsNotSpecificTokenFunction<SpecificToken extends TSESTree.Token extends TSESTree.Token>`

```ts
type IsNotSpecificTokenFunction<SpecificToken extends TSESTree.Token extends TSESTree.Token> = (
  token: TSESTree.Token,
) => token is Exclude<TSESTree.Token, SpecificToken>;
```

### `PunctuatorTokenWithValue<Value extends string extends string>`

```ts
type PunctuatorTokenWithValue<Value extends string extends string> = {
  value: Value;
} & TSESTree.PunctuatorToken;
```

### `IsPunctuatorTokenWithValueFunction<Value extends string extends string>`

```ts
type IsPunctuatorTokenWithValueFunction<Value extends string extends string> = IsSpecificTokenFunction<PunctuatorTokenWithValue<Value>>;
```

### `IsNotPunctuatorTokenWithValueFunction<Value extends string extends string>`

```ts
type IsNotPunctuatorTokenWithValueFunction<Value extends string extends string> = IsNotSpecificTokenFunction<PunctuatorTokenWithValue<Value>>;
```


---