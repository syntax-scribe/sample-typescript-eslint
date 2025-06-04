[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `WatchCompilerHostOfConfigFile.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 3 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/create-program/WatchCompilerHostOfConfigFile.ts`**


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