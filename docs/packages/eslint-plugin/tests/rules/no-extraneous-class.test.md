[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-extraneous-class.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📊 Variables & Constants | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/no-extraneous-class.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `rule` | `../../src/rules/no-extraneous-class` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `empty` | `{ messageId: "empty"; }` | const | `{
  messageId: 'empty' as const,
}` | ✗ |
| `onlyStatic` | `{ messageId: "onlyStatic"; }` | const | `{
  messageId: 'onlyStatic' as const,
}` | ✗ |
| `onlyConstructor` | `{ messageId: "onlyConstructor"; }` | const | `{
  messageId: 'onlyConstructor' as const,
}` | ✗ |
| `ruleTester` | `any` | const | `new RuleTester()` | ✗ |


---