[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-relative-paths-to-internal-packages.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 8 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 3 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin-internal/src/rules/no-relative-paths-to-internal-packages.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `path` | `node:path` |
| `createRule` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `importSource` | `any` | const | `node.source` | ✗ |
| `packageOfFile` | `string` | const | `pathOfFileFromPackagesDir.split(path.sep)[0]` | ✗ |
| `packageOfImport` | `string` | const | `pathOfImportFromPackagesDir.split(path.sep)[0]` | ✗ |


---

## Functions

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              // Force the output path to be separated with '/' to get consistent
              // results on windows.
              const platformIndependentRelativePathOfImportFromPackagesDir =
                pathOfImportFromPackagesDir.split(path.sep).join('/');
              return fixer.replaceText(
                importSource,
                `'@typescript-eslint/${platformIndependentRelativePathOfImportFromPackagesDir}'`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `pathOfImportFromPackagesDir.split(path.sep).join`
  - `fixer.replaceText`
- **Internal Comments**:
```
// Force the output path to be separated with '/' to get consistent (x2)
// results on windows. (x2)
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              // Force the output path to be separated with '/' to get consistent
              // results on windows.
              const platformIndependentRelativePathOfImportFromPackagesDir =
                pathOfImportFromPackagesDir.split(path.sep).join('/');
              return fixer.replaceText(
                importSource,
                `'@typescript-eslint/${platformIndependentRelativePathOfImportFromPackagesDir}'`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `pathOfImportFromPackagesDir.split(path.sep).join`
  - `fixer.replaceText`
- **Internal Comments**:
```
// Force the output path to be separated with '/' to get consistent (x2)
// results on windows. (x2)
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              // Force the output path to be separated with '/' to get consistent
              // results on windows.
              const platformIndependentRelativePathOfImportFromPackagesDir =
                pathOfImportFromPackagesDir.split(path.sep).join('/');
              return fixer.replaceText(
                importSource,
                `'@typescript-eslint/${platformIndependentRelativePathOfImportFromPackagesDir}'`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `pathOfImportFromPackagesDir.split(path.sep).join`
  - `fixer.replaceText`
- **Internal Comments**:
```
// Force the output path to be separated with '/' to get consistent (x2)
// results on windows. (x2)
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              // Force the output path to be separated with '/' to get consistent
              // results on windows.
              const platformIndependentRelativePathOfImportFromPackagesDir =
                pathOfImportFromPackagesDir.split(path.sep).join('/');
              return fixer.replaceText(
                importSource,
                `'@typescript-eslint/${platformIndependentRelativePathOfImportFromPackagesDir}'`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `pathOfImportFromPackagesDir.split(path.sep).join`
  - `fixer.replaceText`
- **Internal Comments**:
```
// Force the output path to be separated with '/' to get consistent (x2)
// results on windows. (x2)
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              // Force the output path to be separated with '/' to get consistent
              // results on windows.
              const platformIndependentRelativePathOfImportFromPackagesDir =
                pathOfImportFromPackagesDir.split(path.sep).join('/');
              return fixer.replaceText(
                importSource,
                `'@typescript-eslint/${platformIndependentRelativePathOfImportFromPackagesDir}'`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `pathOfImportFromPackagesDir.split(path.sep).join`
  - `fixer.replaceText`
- **Internal Comments**:
```
// Force the output path to be separated with '/' to get consistent (x2)
// results on windows. (x2)
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              // Force the output path to be separated with '/' to get consistent
              // results on windows.
              const platformIndependentRelativePathOfImportFromPackagesDir =
                pathOfImportFromPackagesDir.split(path.sep).join('/');
              return fixer.replaceText(
                importSource,
                `'@typescript-eslint/${platformIndependentRelativePathOfImportFromPackagesDir}'`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `pathOfImportFromPackagesDir.split(path.sep).join`
  - `fixer.replaceText`
- **Internal Comments**:
```
// Force the output path to be separated with '/' to get consistent (x2)
// results on windows. (x2)
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              // Force the output path to be separated with '/' to get consistent
              // results on windows.
              const platformIndependentRelativePathOfImportFromPackagesDir =
                pathOfImportFromPackagesDir.split(path.sep).join('/');
              return fixer.replaceText(
                importSource,
                `'@typescript-eslint/${platformIndependentRelativePathOfImportFromPackagesDir}'`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `pathOfImportFromPackagesDir.split(path.sep).join`
  - `fixer.replaceText`
- **Internal Comments**:
```
// Force the output path to be separated with '/' to get consistent (x2)
// results on windows. (x2)
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
              // Force the output path to be separated with '/' to get consistent
              // results on windows.
              const platformIndependentRelativePathOfImportFromPackagesDir =
                pathOfImportFromPackagesDir.split(path.sep).join('/');
              return fixer.replaceText(
                importSource,
                `'@typescript-eslint/${platformIndependentRelativePathOfImportFromPackagesDir}'`,
              );
            }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `pathOfImportFromPackagesDir.split(path.sep).join`
  - `fixer.replaceText`
- **Internal Comments**:
```
// Force the output path to be separated with '/' to get consistent (x2)
// results on windows. (x2)
```


---