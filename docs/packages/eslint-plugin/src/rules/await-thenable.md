[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `await-thenable.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 12 |
| 📊 Variables & Constants | 2 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Type Aliases](#type-aliases)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `awaitArgumentEsNode` | `any` | const | `node.argument` | ✗ |
| `init` | `any` | const | `declarator.init` | ✗ |


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