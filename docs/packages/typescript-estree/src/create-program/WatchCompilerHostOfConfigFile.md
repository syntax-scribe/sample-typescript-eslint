[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `WatchCompilerHostOfConfigFile.ts`

## 📚 Table of Contents

- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 3
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/create-program/WatchCompilerHostOfConfigFile.ts`**

## 📦 Imports

> No imports found in this file.


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `DirectoryStructureHost`

<details><summary>Interface Code</summary>

```ts
interface DirectoryStructureHost {
  readDirectory?(
    path: string,
    extensions?: readonly string[],
    exclude?: readonly string[],
    include?: readonly string[],
    depth?: number,
  ): string[];
}
```
</details>

### `CachedDirectoryStructureHost`

<details><summary>Interface Code</summary>

```ts
interface CachedDirectoryStructureHost extends DirectoryStructureHost {
  readDirectory(
    path: string,
    extensions?: readonly string[],
    exclude?: readonly string[],
    include?: readonly string[],
    depth?: number,
  ): string[];
}
```
</details>

### `WatchCompilerHostOfConfigFile<T extends ts.BuilderProgram>`

<details><summary>Interface Code</summary>

```ts
export interface WatchCompilerHostOfConfigFile<T extends ts.BuilderProgram>
  extends ts.WatchCompilerHostOfConfigFile<T> {
  extraFileExtensions?: readonly ts.FileExtensionInfo[];
  onCachedDirectoryStructureHostCreate(
    host: CachedDirectoryStructureHost,
  ): void;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `extraFileExtensions` | `readonly ts.FileExtensionInfo[]` | ✓ |  |


---

## Type Aliases

> No type aliases found in this file.


---