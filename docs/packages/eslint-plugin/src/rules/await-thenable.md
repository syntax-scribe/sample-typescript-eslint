[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `await-thenable.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 12 |
| 📊 Variables & Constants | 2 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

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

## 🔧 Functions

> No functions found in this file.


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