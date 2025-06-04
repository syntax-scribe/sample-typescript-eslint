[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `isTypeReadonly.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📊 Variables & Constants | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/type-utils/tests/isTypeReadonly.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ReadonlynessOptions` | `../src/index.js` |
| `isTypeReadonly` | `../src/index.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `options` | `any` | const | `undefined` | ✗ |
| `options` | `ReadonlynessOptions` | const | `{
        treatMethodsAsReadonly: true,
      }` | ✗ |
| `options` | `ReadonlynessOptions` | const | `{
        allow: [
          {
            from: 'lib',
            name: 'RegExp',
          },
          {
            from: 'file',
            name: 'Foo',
          },
        ],
      }` | ✗ |


---