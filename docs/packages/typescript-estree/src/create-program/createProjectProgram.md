[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `createProjectProgram.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/create-program/createProjectProgram.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `debug` | `debug` |
| `ParseSettings` | `../parseSettings` |
| `ASTAndDefiniteProgram` | `./shared` |
| `firstDefined` | `../node-utils` |
| `createProjectProgramError` | `./createProjectProgramError` |
| `getAstFromProgram` | `./shared` |


---

## Functions

### `createProjectProgram(parseSettings: ParseSettings, programsForProjects: readonly ts.Program[]): ASTAndDefiniteProgram`

<details><summary>Code</summary>

```ts
export function createProjectProgram(
  parseSettings: ParseSettings,
  programsForProjects: readonly ts.Program[],
): ASTAndDefiniteProgram {
  log('Creating project program for: %s', parseSettings.filePath);

  const astAndProgram = firstDefined(programsForProjects, currentProgram =>
    getAstFromProgram(currentProgram, parseSettings.filePath),
  );

  if (!astAndProgram) {
    throw new Error(
      createProjectProgramError(parseSettings, programsForProjects).join('\n'),
    );
  }

  return astAndProgram;
}
```
</details>

- **JSDoc**:
```ts
/**
 * @param parseSettings Internal settings for parsing the file
 * @returns If found, the source file corresponding to the code and the containing program
 */
```

- **Parameters**:
  - `parseSettings: ParseSettings`
  - `programsForProjects: readonly ts.Program[]`
- **Return Type**: `ASTAndDefiniteProgram`
- **Calls**:
  - `log`
  - `firstDefined (from ../node-utils)`
  - `getAstFromProgram (from ./shared)`
  - `createProjectProgramError(parseSettings, programsForProjects).join`

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