[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `self-reference-super.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/class/expression/self-reference-super.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `A` | `typeof A` | const | `class A
  // this A references the class A, not the variable A
  extends A {}` | ✗ |


---