[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `typeDeclaredInLib.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/type-utils/src/typeOrValueSpecifiers/typeDeclaredInLib.ts`**

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