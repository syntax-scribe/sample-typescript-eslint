[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-this-alias.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 4 |
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


---