[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `validateDefaultProjectForFilesGlob.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/create-program/validateDefaultProjectForFilesGlob.ts`**

## 📦 Imports

> No imports found in this file.


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---