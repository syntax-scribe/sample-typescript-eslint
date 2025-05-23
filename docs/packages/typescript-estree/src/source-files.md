[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `source-files.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/source-files.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `isSourceFile(code: unknown): code is ts.SourceFile`

<details><summary>Code</summary>

```ts
export function isSourceFile(code: unknown): code is ts.SourceFile {
  if (typeof code !== 'object' || code == null) {
    return false;
  }

  const maybeSourceFile = code as Partial<ts.SourceFile>;
  return (
    maybeSourceFile.kind === ts.SyntaxKind.SourceFile &&
    typeof maybeSourceFile.getFullText === 'function'
  );
}
```
</details>

- **Parameters**:
  - `code: unknown`
- **Return Type**: `code is ts.SourceFile`
### `getCodeText(code: string | ts.SourceFile): string`

<details><summary>Code</summary>

```ts
export function getCodeText(code: string | ts.SourceFile): string {
  return isSourceFile(code) ? code.getFullText(code) : code;
}
```
</details>

- **Parameters**:
  - `code: string | ts.SourceFile`
- **Return Type**: `string`
- **Calls**:
  - `isSourceFile`
  - `code.getFullText`

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