[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `validateDefaultProjectForFilesGlob.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/create-program/validateDefaultProjectForFilesGlob.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `DEFAULT_PROJECT_FILES_ERROR_EXPLANATION` | `"\n\nHaving many files run with the default project is known to cause performance issues and slow down linting.\n\nSee https://typescript-eslint.io/troubleshooting/typed-linting#allowdefaultproject-glob-too-wide\n"` | const | ``

Having many files run with the default project is known to cause performance issues and slow down linting.

See https://typescript-eslint.io/troubleshooting/typed-linting#allowdefaultproject-glob-too-wide
`` | ✓ |


---

## Functions

### `validateDefaultProjectForFilesGlob(allowDefaultProject: string[] | undefined): void`

<details><summary>Code</summary>

```ts
export function validateDefaultProjectForFilesGlob(
  allowDefaultProject: string[] | undefined,
): void {
  if (!allowDefaultProject?.length) {
    return;
  }

  for (const glob of allowDefaultProject) {
    if (glob === '*') {
      throw new Error(
        `allowDefaultProject contains the overly wide '*'.${DEFAULT_PROJECT_FILES_ERROR_EXPLANATION}`,
      );
    }
    if (glob.includes('**')) {
      throw new Error(
        `allowDefaultProject glob '${glob}' contains a disallowed '**'.${DEFAULT_PROJECT_FILES_ERROR_EXPLANATION}`,
      );
    }
  }
}
```
</details>

- **Parameters**:
  - `allowDefaultProject: string[] | undefined`
- **Return Type**: `void`
- **Calls**:
  - `glob.includes`

---