[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `isSymbolFromDefaultLibrary.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
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
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/type-utils/src/isSymbolFromDefaultLibrary.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `declarations` | `any` | const | `symbol.getDeclarations() ?? []` | ✗ |


---

## Functions

### `isSymbolFromDefaultLibrary(program: ts.Program, symbol: ts.Symbol | undefined): boolean`

<details><summary>Code</summary>

```ts
export function isSymbolFromDefaultLibrary(
  program: ts.Program,
  symbol: ts.Symbol | undefined,
): boolean {
  if (!symbol) {
    return false;
  }

  const declarations = symbol.getDeclarations() ?? [];
  for (const declaration of declarations) {
    const sourceFile = declaration.getSourceFile();
    if (program.isSourceFileDefaultLibrary(sourceFile)) {
      return true;
    }
  }

  return false;
}
```
</details>

- **Parameters**:
  - `program: ts.Program`
  - `symbol: ts.Symbol | undefined`
- **Return Type**: `boolean`
- **Calls**:
  - `symbol.getDeclarations`
  - `declaration.getSourceFile`
  - `program.isSourceFileDefaultLibrary`

---