[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-this-alias.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📊 Variables & Constants | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/no-this-alias.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `rule` | `../../src/rules/no-this-alias` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `idError` | `{ messageId: "thisAssignment"; type: any; }` | const | `{
  messageId: 'thisAssignment' as const,
  type: AST_NODE_TYPES.Identifier,
}` | ✗ |
| `destructureError` | `{ messageId: "thisDestructure"; type: any; }` | const | `{
  messageId: 'thisDestructure' as const,
  type: AST_NODE_TYPES.ObjectPattern,
}` | ✗ |
| `arrayDestructureError` | `{ messageId: "thisDestructure"; type: any; }` | const | `{
  messageId: 'thisDestructure' as const,
  type: AST_NODE_TYPES.ArrayPattern,
}` | ✗ |
| `ruleTester` | `any` | const | `new RuleTester()` | ✗ |


---