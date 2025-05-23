[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `predicates.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 5

## 🛠️ File Location:
📂 **`packages/utils/src/ast-utils/eslint-utils/predicates.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `../../ts-estree` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


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