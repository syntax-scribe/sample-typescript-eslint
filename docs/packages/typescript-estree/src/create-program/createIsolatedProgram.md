[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `createIsolatedProgram.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/create-program/createIsolatedProgram.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `debug` | `debug` |
| `ParseSettings` | `../parseSettings` |
| `ASTAndDefiniteProgram` | `./shared` |
| `getScriptKind` | `./getScriptKind` |
| `createDefaultCompilerOptionsFromExtra` | `./shared` |


---

## Functions

### `createIsolatedProgram(parseSettings: ParseSettings): ASTAndDefiniteProgram`

<details><summary>Code</summary>

```ts
export function createIsolatedProgram(
  parseSettings: ParseSettings,
): ASTAndDefiniteProgram {
  log(
    'Getting isolated program in %s mode for: %s',
    parseSettings.jsx ? 'TSX' : 'TS',
    parseSettings.filePath,
  );

  const compilerHost: ts.CompilerHost = {
    fileExists() {
      return true;
    },
    getCanonicalFileName() {
      return parseSettings.filePath;
    },
    getCurrentDirectory() {
      return '';
    },
    getDefaultLibFileName() {
      return 'lib.d.ts';
    },
    getDirectories() {
      return [];
    },

    // TODO: Support Windows CRLF
    getNewLine() {
      return '\n';
    },
    getSourceFile(filename: string) {
      return ts.createSourceFile(
        filename,
        parseSettings.codeFullText,
        ts.ScriptTarget.Latest,
        /* setParentNodes */ true,
        getScriptKind(parseSettings.filePath, parseSettings.jsx),
      );
    },
    readFile() {
      return undefined;
    },
    useCaseSensitiveFileNames() {
      return true;
    },
    writeFile() {
      return null;
    },
  };

  const program = ts.createProgram(
    [parseSettings.filePath],
    {
      jsDocParsingMode: parseSettings.jsDocParsingMode,
      jsx: parseSettings.jsx ? ts.JsxEmit.Preserve : undefined,
      noResolve: true,
      target: ts.ScriptTarget.Latest,
      ...createDefaultCompilerOptionsFromExtra(parseSettings),
    },
    compilerHost,
  );

  const ast = program.getSourceFile(parseSettings.filePath);
  if (!ast) {
    throw new Error(
      'Expected an ast to be returned for the single-file isolated program.',
    );
  }

  return { ast, program };
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns Returns a new source file and program corresponding to the linted code
 */
```

- **Parameters**:
  - `parseSettings: ParseSettings`
- **Return Type**: `ASTAndDefiniteProgram`
- **Calls**:
  - `log`
  - `ts.createSourceFile`
  - `getScriptKind (from ./getScriptKind)`
  - `ts.createProgram`
  - `createDefaultCompilerOptionsFromExtra (from ./shared)`
  - `program.getSourceFile`
- **Internal Comments**:
```
// TODO: Support Windows CRLF (x2)
/* setParentNodes */
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