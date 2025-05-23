[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `semanticInfo.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 8
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/tests/lib/semanticInfo.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `../../src/index.js` |
| `TSESTreeOptions` | `../../src/index.js` |
| `createProgram` | `../../src/create-program/useProvidedPrograms.js` |
| `clearCaches` | `../../src/index.js` |
| `parseAndGenerateServices` | `../../src/index.js` |
| `deeplyCopy` | `../test-utils/test-utils.js` |
| `formatSnapshotName` | `../test-utils/test-utils.js` |
| `parseCodeAndGenerateServices` | `../test-utils/test-utils.js` |


---

## Functions

### `createOptions(fileName: string): { cwd?: string } & TSESTreeOptions`

<details><summary>Code</summary>

```ts
function createOptions(fileName: string): { cwd?: string } & TSESTreeOptions {
  return {
    comment: true,
    disallowAutomaticSingleRunInference: true,
    errorOnUnknownASTType: true,
    filePath: fileName,
    jsx: false,
    loc: true,
    loggerFn: false,
    project: `./tsconfig.json`,
    range: true,
    tokens: true,
    tsconfigRootDir: FIXTURES_DIR,
  };
}
```
</details>

- **Parameters**:
  - `fileName: string`
- **Return Type**: `{ cwd?: string } & TSESTreeOptions`

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