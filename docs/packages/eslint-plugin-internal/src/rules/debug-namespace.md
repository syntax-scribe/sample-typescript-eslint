[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `debug-namespace.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 9 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 0 |
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
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin-internal/src/rules/debug-namespace.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `getStaticValue` | `@typescript-eslint/utils/ast-utils` |
| `createRule` | `../util` |


---

## Functions

### `filePathToNamespace(filePath: string): string`

<details><summary>Code</summary>

```ts
function filePathToNamespace(filePath: string) {
  const relativePath = filePath
    .split(/packages[\\/]+/)
    .slice(1)
    .join('');

  const relativeNamespace = relativePath
    .replace(/^[\\/]/, '')
    .replace(/(?:dist|lib|src)(\/|\\)/, '')
    .replace(/\.\w+$/, '')
    .replaceAll(/[^a-z0-9-]+/gi, ':');

  return `typescript-eslint:${relativeNamespace}`;
}
```
</details>

- **Parameters**:
  - `filePath: string`
- **Return Type**: `string`
- **Calls**:
  - `filePath
    .split(/packages[\\/]+/)
    .slice(1)
    .join`
  - `relativePath
    .replace(/^[\\/]/, '')
    .replace(/(?:dist|lib|src)(\/|\\)/, '')
    .replace(/\.\w+$/, '')
    .replaceAll`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(argument, `'${expected}'`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(argument, `'${expected}'`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(argument, `'${expected}'`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(argument, `'${expected}'`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(argument, `'${expected}'`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(argument, `'${expected}'`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(argument, `'${expected}'`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(argument, `'${expected}'`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`

---