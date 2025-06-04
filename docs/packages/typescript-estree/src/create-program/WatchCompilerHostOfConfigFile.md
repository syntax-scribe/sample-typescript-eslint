[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `WatchCompilerHostOfConfigFile.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📐 Interfaces | 3 |

## 📚 Table of Contents

- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/create-program/WatchCompilerHostOfConfigFile.ts`**

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