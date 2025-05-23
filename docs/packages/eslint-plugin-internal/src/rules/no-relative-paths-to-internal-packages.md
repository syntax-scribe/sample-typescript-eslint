[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-relative-paths-to-internal-packages.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 8
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin-internal/src/rules/no-relative-paths-to-internal-packages.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `path` | `node:path` |
| `createRule` | `../util` |


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---