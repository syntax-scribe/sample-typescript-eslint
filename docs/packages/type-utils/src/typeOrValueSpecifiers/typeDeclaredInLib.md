[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `typeDeclaredInLib.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/type-utils/src/typeOrValueSpecifiers/typeDeclaredInLib.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `typeDeclaredInLib(declarationFiles: ts.SourceFile[], program: ts.Program): boolean`

<details><summary>Code</summary>

```ts
export function typeDeclaredInLib(
  declarationFiles: ts.SourceFile[],
  program: ts.Program,
): boolean {
  // Assertion: The type is not an error type.

  // Intrinsic type (i.e. string, number, boolean, etc) - Treat it as if it's from lib.
  if (declarationFiles.length === 0) {
    return true;
  }
  return declarationFiles.some(declaration =>
    program.isSourceFileDefaultLibrary(declaration),
  );
}
```
</details>

- **Parameters**:
  - `declarationFiles: ts.SourceFile[]`
  - `program: ts.Program`
- **Return Type**: `boolean`
- **Calls**:
  - `declarationFiles.some`
  - `program.isSourceFileDefaultLibrary`
- **Internal Comments**:
```
// Assertion: The type is not an error type.
// Intrinsic type (i.e. string, number, boolean, etc) - Treat it as if it's from lib.
```


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