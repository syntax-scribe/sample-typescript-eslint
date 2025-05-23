[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `typeDeclaredInFile.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/type-utils/src/typeOrValueSpecifiers/typeDeclaredInFile.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `getCanonicalFileName` | `@typescript-eslint/typescript-estree` |
| `path` | `node:path` |


---

## Functions

### `typeDeclaredInFile(relativePath: string | undefined, declarationFiles: ts.SourceFile[], program: ts.Program): boolean`

<details><summary>Code</summary>

```ts
export function typeDeclaredInFile(
  relativePath: string | undefined,
  declarationFiles: ts.SourceFile[],
  program: ts.Program,
): boolean {
  if (relativePath == null) {
    const cwd = getCanonicalFileName(program.getCurrentDirectory());
    return declarationFiles.some(declaration =>
      getCanonicalFileName(declaration.fileName).startsWith(cwd),
    );
  }
  const absolutePath = getCanonicalFileName(
    path.join(program.getCurrentDirectory(), relativePath),
  );
  return declarationFiles.some(
    declaration => getCanonicalFileName(declaration.fileName) === absolutePath,
  );
}
```
</details>

- **Parameters**:
  - `relativePath: string | undefined`
  - `declarationFiles: ts.SourceFile[]`
  - `program: ts.Program`
- **Return Type**: `boolean`
- **Calls**:
  - `getCanonicalFileName (from @typescript-eslint/typescript-estree)`
  - `program.getCurrentDirectory`
  - `declarationFiles.some`
  - `getCanonicalFileName(declaration.fileName).startsWith`
  - `path.join`

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