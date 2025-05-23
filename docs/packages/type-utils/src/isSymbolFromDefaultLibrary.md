[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `isSymbolFromDefaultLibrary.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/type-utils/src/isSymbolFromDefaultLibrary.ts`**

## 📦 Imports

> No imports found in this file.


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---