[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `shared.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 7
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 2
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/create-program/shared.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Program` | `typescript` |
| `CORE_COMPILER_OPTIONS` | `@typescript-eslint/tsconfig-utils` |
| `path` | `node:path` |
| `ParseSettings` | `../parseSettings` |


---

## Functions

### `createDefaultCompilerOptionsFromExtra(parseSettings: ParseSettings): ts.CompilerOptions`

<details><summary>Code</summary>

```ts
export function createDefaultCompilerOptionsFromExtra(
  parseSettings: ParseSettings,
): ts.CompilerOptions {
  if (parseSettings.debugLevel.has('typescript')) {
    return {
      ...DEFAULT_COMPILER_OPTIONS,
      extendedDiagnostics: true,
    };
  }

  return DEFAULT_COMPILER_OPTIONS;
}
```
</details>

- **Parameters**:
  - `parseSettings: ParseSettings`
- **Return Type**: `ts.CompilerOptions`
- **Calls**:
  - `parseSettings.debugLevel.has`
### `getCanonicalFileName(filePath: string): CanonicalPath`

<details><summary>Code</summary>

```ts
export function getCanonicalFileName(filePath: string): CanonicalPath {
  let normalized = path.normalize(filePath);
  if (normalized.endsWith(path.sep)) {
    normalized = normalized.slice(0, -1);
  }
  return correctPathCasing(normalized) as CanonicalPath;
}
```
</details>

- **Parameters**:
  - `filePath: string`
- **Return Type**: `CanonicalPath`
- **Calls**:
  - `path.normalize`
  - `normalized.endsWith`
  - `normalized.slice`
  - `correctPathCasing`
### `ensureAbsolutePath(p: string, tsconfigRootDir: string): string`

<details><summary>Code</summary>

```ts
export function ensureAbsolutePath(p: string, tsconfigRootDir: string): string {
  return path.isAbsolute(p)
    ? p
    : path.join(tsconfigRootDir || process.cwd(), p);
}
```
</details>

- **Parameters**:
  - `p: string`
  - `tsconfigRootDir: string`
- **Return Type**: `string`
- **Calls**:
  - `path.isAbsolute`
  - `path.join`
  - `process.cwd`
### `canonicalDirname(p: CanonicalPath): CanonicalPath`

<details><summary>Code</summary>

```ts
export function canonicalDirname(p: CanonicalPath): CanonicalPath {
  return path.dirname(p) as CanonicalPath;
}
```
</details>

- **Parameters**:
  - `p: CanonicalPath`
- **Return Type**: `CanonicalPath`
- **Calls**:
  - `path.dirname`
### `getExtension(fileName: string | undefined): string | null`

<details><summary>Code</summary>

```ts
function getExtension(fileName: string | undefined): string | null {
  if (!fileName) {
    return null;
  }

  return (
    DEFINITION_EXTENSIONS.find(definitionExt =>
      fileName.endsWith(definitionExt),
    ) ?? path.extname(fileName)
  );
}
```
</details>

- **Parameters**:
  - `fileName: string | undefined`
- **Return Type**: `string | null`
- **Calls**:
  - `DEFINITION_EXTENSIONS.find`
  - `fileName.endsWith`
  - `path.extname`
### `getAstFromProgram(currentProgram: Program, filePath: string): ASTAndDefiniteProgram | undefined`

<details><summary>Code</summary>

```ts
export function getAstFromProgram(
  currentProgram: Program,
  filePath: string,
): ASTAndDefiniteProgram | undefined {
  const ast = currentProgram.getSourceFile(filePath);

  // working around https://github.com/typescript-eslint/typescript-eslint/issues/1573
  const expectedExt = getExtension(filePath);
  const returnedExt = getExtension(ast?.fileName);
  if (expectedExt !== returnedExt) {
    return undefined;
  }

  return ast && { ast, program: currentProgram };
}
```
</details>

- **Parameters**:
  - `currentProgram: Program`
  - `filePath: string`
- **Return Type**: `ASTAndDefiniteProgram | undefined`
- **Calls**:
  - `currentProgram.getSourceFile`
  - `getExtension`
- **Internal Comments**:
```
// working around https://github.com/typescript-eslint/typescript-eslint/issues/1573 (x2)
```

### `createHash(content: string): string`

<details><summary>Code</summary>

```ts
export function createHash(content: string): string {
  // No ts.sys in browser environments.
  // eslint-disable-next-line @typescript-eslint/no-unnecessary-condition
  if (ts.sys?.createHash) {
    return ts.sys.createHash(content);
  }
  return content;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Hash content for compare content.
 * @param content hashed contend
 * @returns hashed result
 */
```

- **Parameters**:
  - `content: string`
- **Return Type**: `string`
- **Calls**:
  - `ts.sys.createHash`
- **Internal Comments**:
```
// No ts.sys in browser environments.
// eslint-disable-next-line @typescript-eslint/no-unnecessary-condition
```


---

## Classes

> No classes found in this file.


---

## Interfaces

### `ASTAndNoProgram`

<details><summary>Interface Code</summary>

```ts
export interface ASTAndNoProgram {
  ast: ts.SourceFile;
  program: null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `ast` | `ts.SourceFile` | ✗ |  |
| `program` | `null` | ✗ |  |

### `ASTAndDefiniteProgram`

<details><summary>Interface Code</summary>

```ts
export interface ASTAndDefiniteProgram {
  ast: ts.SourceFile;
  program: ts.Program;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `ast` | `ts.SourceFile` | ✗ |  |
| `program` | `ts.Program` | ✗ |  |


---

## Type Aliases

### `ASTAndProgram`

```ts
type ASTAndProgram = ASTAndDefiniteProgram | ASTAndNoProgram;
```

### `CanonicalPath`

```ts
type CanonicalPath = { __brand: unknown } & string;
```


---