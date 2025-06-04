[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `hasOwnProperty.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/hasOwnProperty.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `hasOwnProperty` | `<Obj extends object, K extends keyof Obj>(obj: Obj, key: K) => obj is { [key in K]-?: Obj[key]; } & Obj` | const | `Object.hasOwn as <
  Obj extends object,
  K extends keyof Obj,
>(
  obj: Obj,
  key: K,
) => obj is { [key in K]-?: Obj[key] } & Obj` | ✓ |


---