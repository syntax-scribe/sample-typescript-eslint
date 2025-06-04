[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `compilerOptions.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/tsconfig-utils/src/compilerOptions.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `CORE_COMPILER_OPTIONS` | `ts.CompilerOptions` | const | `{
  // Required to avoid parse from causing emit to occur
  noEmit: true,

  // Flags required to make no-unused-vars work
  noUnusedLocals: true,
  noUnusedParameters: true,
} satisfies ts.CompilerOptions` | ✓ |


---