[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `compilerOptions.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
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


---