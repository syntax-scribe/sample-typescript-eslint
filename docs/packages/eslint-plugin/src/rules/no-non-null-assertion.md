[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-non-null-assertion.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 1 |
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
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-non-null-assertion.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `isNonNullAssertionPunctuator` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `suggest` | `TSESLint.ReportSuggestionArray<MessageIds>` | const | `[]` | ✗ |


---

## Functions

### `replaceTokenWithOptional(): TSESLint.ReportFixFunction`

<details><summary>Code</summary>

```ts
function replaceTokenWithOptional(): TSESLint.ReportFixFunction {
          return fixer => fixer.replaceText(nonNullOperator, '?.');
        }
```
</details>

- **Return Type**: `TSESLint.ReportFixFunction`
- **Calls**:
  - `fixer.replaceText`
### `removeToken(): TSESLint.ReportFixFunction`

<details><summary>Code</summary>

```ts
function removeToken(): TSESLint.ReportFixFunction {
          return fixer => fixer.remove(nonNullOperator);
        }
```
</details>

- **Return Type**: `TSESLint.ReportFixFunction`
- **Calls**:
  - `fixer.remove`

---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = 'noNonNull' | 'suggestOptionalChain';
```


---