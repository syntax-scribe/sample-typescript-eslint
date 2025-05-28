[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `createSourceFile.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
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
📂 **`packages/typescript-estree/src/create-program/createSourceFile.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `debug` | `debug` |
| `ParseSettings` | `../parseSettings` |
| `ASTAndNoProgram` | `./shared` |
| `isSourceFile` | `../source-files` |
| `getScriptKind` | `./getScriptKind` |


---

## Functions

### `createSourceFile(parseSettings: ParseSettings): ts.SourceFile`

<details><summary>Code</summary>

```ts
export function createSourceFile(parseSettings: ParseSettings): ts.SourceFile {
  log(
    'Getting AST without type information in %s mode for: %s',
    parseSettings.jsx ? 'TSX' : 'TS',
    parseSettings.filePath,
  );

  return isSourceFile(parseSettings.code)
    ? parseSettings.code
    : ts.createSourceFile(
        parseSettings.filePath,
        parseSettings.codeFullText,
        {
          jsDocParsingMode: parseSettings.jsDocParsingMode,
          languageVersion: ts.ScriptTarget.Latest,
          setExternalModuleIndicator: parseSettings.setExternalModuleIndicator,
        },
        /* setParentNodes */ true,
        getScriptKind(parseSettings.filePath, parseSettings.jsx),
      );
}
```
</details>

- **Parameters**:
  - `parseSettings: ParseSettings`
- **Return Type**: `ts.SourceFile`
- **Calls**:
  - `log`
  - `isSourceFile (from ../source-files)`
  - `ts.createSourceFile`
  - `getScriptKind (from ./getScriptKind)`
- **Internal Comments**:
```
/* setParentNodes */
```

### `createNoProgram(parseSettings: ParseSettings): ASTAndNoProgram`

<details><summary>Code</summary>

```ts
export function createNoProgram(parseSettings: ParseSettings): ASTAndNoProgram {
  return {
    ast: createSourceFile(parseSettings),
    program: null,
  };
}
```
</details>

- **Parameters**:
  - `parseSettings: ParseSettings`
- **Return Type**: `ASTAndNoProgram`
- **Calls**:
  - `createSourceFile`

---