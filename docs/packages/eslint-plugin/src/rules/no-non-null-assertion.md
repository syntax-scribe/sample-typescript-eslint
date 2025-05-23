[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-non-null-assertion.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 1

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = 'noNonNull' | 'suggestOptionalChain';
```


---