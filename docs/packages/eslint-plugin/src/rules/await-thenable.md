[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `await-thenable.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 12
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/await-thenable.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `Awaitable` | `../util` |
| `createRule` | `../util` |
| `getFixOrSuggest` | `../util` |
| `getParserServices` | `../util` |
| `isAwaitKeyword` | `../util` |
| `isTypeAnyType` | `../util` |
| `needsToBeAwaited` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |
| `getForStatementHeadLoc` | `../util/getForStatementHeadLoc` |


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

### `MessageId`

```ts
type MessageId = | 'await'
  | 'awaitUsingOfNonAsyncDisposable'
  | 'convertToOrdinaryFor'
  | 'forAwaitOfNonAsyncIterable'
  | 'removeAwait';
```


---