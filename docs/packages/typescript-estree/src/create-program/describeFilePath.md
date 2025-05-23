[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `describeFilePath.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/create-program/describeFilePath.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `path` | `node:path` |


---

## Functions

### `describeFilePath(filePath: string, tsconfigRootDir: string): string`

<details><summary>Code</summary>

```ts
export function describeFilePath(
  filePath: string,
  tsconfigRootDir: string,
): string {
  // If the TSConfig root dir is a parent of the filePath, use
  // `<tsconfigRootDir>` as a prefix for the path.
  const relative = path.relative(tsconfigRootDir, filePath);
  if (relative && !relative.startsWith('..') && !path.isAbsolute(relative)) {
    return `<tsconfigRootDir>/${relative}`;
  }

  // Root-like Mac/Linux (~/*, ~*) or Windows (C:/*, /) paths that aren't
  // relative to the TSConfig root dir should be fully described.
  // This avoids strings like <tsconfigRootDir>/../../../../repo/file.ts.
  // https://github.com/typescript-eslint/typescript-eslint/issues/6289
  if (/^[(\w+:)\\/~]/.test(filePath)) {
    return filePath;
  }

  // Similarly, if the relative path would contain a lot of ../.., then
  // ignore it and print the file path directly.
  if (/\.\.[/\\]\.\./.test(relative)) {
    return filePath;
  }

  // Lastly, since we've eliminated all special cases, we know the cleanest
  // path to print is probably the prefixed relative one.
  return `<tsconfigRootDir>/${relative}`;
}
```
</details>

- **Parameters**:
  - `filePath: string`
  - `tsconfigRootDir: string`
- **Return Type**: `string`
- **Calls**:
  - `path.relative`
  - `relative.startsWith`
  - `path.isAbsolute`
  - `/^[(\w+:)\\/~]/.test`
  - `/\.\.[/\\]\.\./.test`
- **Internal Comments**:
```
// If the TSConfig root dir is a parent of the filePath, use (x2)
// `<tsconfigRootDir>` as a prefix for the path. (x2)
// Root-like Mac/Linux (~/*, ~*) or Windows (C:/*, /) paths that aren't
// relative to the TSConfig root dir should be fully described.
// This avoids strings like <tsconfigRootDir>/../../../../repo/file.ts.
// https://github.com/typescript-eslint/typescript-eslint/issues/6289
// Similarly, if the relative path would contain a lot of ../.., then
// ignore it and print the file path directly.
// Lastly, since we've eliminated all special cases, we know the cleanest
// path to print is probably the prefixed relative one.
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