[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `applyDefault.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 1 |
| 📊 Variables & Constants | 10 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/utils/tests/eslint-utils/applyDefault.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ESLintUtils` | `../../src` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `defaults` | `{ prop: string; }[]` | const | `[{ prop: 'setting' }]` | ✗ |
| `user` | `any` | const | `null` | ✗ |
| `defaults` | `Record<string, string>[]` | const | `[
      {
        other: 'other',
        prop: 'setting1',
      },
      {
        prop: 'setting2',
      },
    ]` | ✗ |
| `user` | `Record<string, string>[]` | const | `[
      {
        other: 'something',
        prop: 'new',
      },
    ]` | ✗ |
| `defaults` | `undefined[]` | const | `[]` | ✗ |
| `user` | `undefined[]` | const | `[]` | ✗ |
| `defaults` | `unknown[]` | const | `['1tbs']` | ✗ |
| `user` | `unknown[]` | const | `['2tbs']` | ✗ |
| `defaults` | `unknown[]` | const | `[null]` | ✗ |
| `user` | `unknown[]` | const | `[
      {
        other: 'other',
        prop: 'setting1',
      },
    ]` | ✗ |


---