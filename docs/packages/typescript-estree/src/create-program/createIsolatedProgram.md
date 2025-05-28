[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `createIsolatedProgram.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
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

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `compilerHost` | `ts.CompilerHost` | const | `{
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
  }` | ✗ |


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