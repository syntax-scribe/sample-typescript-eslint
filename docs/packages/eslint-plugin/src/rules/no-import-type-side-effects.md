[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-import-type-side-effects.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 8 |
| 📊 Variables & Constants | 2 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-import-type-side-effects.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `isImportKeyword` | `../util` |
| `isTypeKeyword` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `specifiers` | `TSESTree.ImportSpecifier[]` | const | `[]` | ✗ |
| `fixes` | `TSESLint.RuleFix[]` | const | `[]` | ✗ |


---

## 🔧 Functions

> No functions found in this file.


---

## Type Aliases

### `Options`

```ts
type Options = [];
```

### `MessageIds`

```ts
type MessageIds = 'useTopLevelQualifier';
```


---