[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `source-files.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/source-files.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `maybeSourceFile` | `ts.SourceFile` | const | `code as Partial<ts.SourceFile>` | ✗ |


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