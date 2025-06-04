[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `typeDeclaredInFile.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

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