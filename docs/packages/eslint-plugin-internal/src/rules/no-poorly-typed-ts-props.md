[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-poorly-typed-ts-props.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

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


---