[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getValueOfLiteralType.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 1 |
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
📂 **`packages/eslint-plugin/tests/util/getValueOfLiteralType.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `getValueOfLiteralType` | `../../src/util/getValueOfLiteralType` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `stringLiteralType` | `ts.LiteralType` | const | `{
      value: 'hello' satisfies string,
    } as ts.LiteralType` | ✗ |
| `numberLiteralType` | `ts.LiteralType` | const | `{
      value: 42 satisfies number,
    } as ts.LiteralType` | ✗ |
| `pseudoBigIntLiteralType` | `ts.LiteralType` | const | `{
      value: {
        base10Value: '12345678901234567890',
        negative: false,
      } satisfies ts.PseudoBigInt,
    } as ts.LiteralType` | ✗ |
| `negativePseudoBigIntLiteralType` | `ts.LiteralType` | const | `{
      value: {
        base10Value: '98765432109876543210',
        negative: true,
      } satisfies ts.PseudoBigInt,
    } as ts.LiteralType` | ✗ |


---


---