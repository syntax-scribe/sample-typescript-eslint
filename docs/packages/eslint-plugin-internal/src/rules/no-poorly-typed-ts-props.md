[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-poorly-typed-ts-props.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/eslint-plugin-internal/src/rules/no-poorly-typed-ts-props.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `ESLintUtils` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `BANNED_PROPERTIES` | `{ type: string; fixWith: string; property: string; }[]` | const | `[
  {
    type: 'Symbol',
    fixWith: 'getDeclarations()',
    property: 'declarations',
  },
  {
    // eslint-disable-next-line @typescript-eslint/internal/prefer-ast-types-enum
    type: 'Type',
    fixWith: 'getSymbol()',
    property: 'symbol',
  },
]` | ✗ |


---