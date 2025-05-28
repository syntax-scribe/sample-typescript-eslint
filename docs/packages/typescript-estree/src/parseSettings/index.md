[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `index.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)
- [Enums](#enums)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/parseSettings/index.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ProjectServiceAndMetadata` | `@typescript-eslint/project-service` |
| `CanonicalPath` | `../create-program/shared` |
| `TSESTree` | `../ts-estree` |
| `CacheLike` | `./ExpiringCache` |


---

## 🔧 Functions

> No functions found in this file.


---

## Interfaces

### `MutableParseSettings`

<details><summary>Interface Code</summary>

```ts
export interface MutableParseSettings {
  /**
   * Prevents the parser from throwing an error if it receives an invalid AST from TypeScript.
   */
  allowInvalidAST: boolean;

  /**
   * Code of the file being parsed, or raw source file containing it.
   */
  code: string | ts.SourceFile;

  /**
   * Full text of the file being parsed.
   */
  codeFullText: string;

  /**
   * Whether the `comment` parse option is enabled.
   */
  comment: boolean;

  /**
   * If the `comment` parse option is enabled, retrieved comments.
   */
  comments: TSESTree.Comment[];

  /**
   * Which debug areas should be logged.
   */
  debugLevel: Set<DebugModule>;

  /**
   * Whether to error if TypeScript reports a semantic or syntactic error diagnostic.
   */
  errorOnTypeScriptSyntacticAndSemanticIssues: boolean;

  /**
   * Whether to error if an unknown AST node type is encountered.
   */
  errorOnUnknownASTType: boolean;

  /**
   * Any non-standard file extensions which will be parsed.
   */
  extraFileExtensions: string[];

  /**
   * Path of the file being parsed.
   */
  filePath: string;

  /**
   * Sets the external module indicator on the source file.
   * Used by Typescript to determine if a sourceFile is an external module.
   *
   * needed to always parsing `mjs`/`mts` files as ESM
   */
  setExternalModuleIndicator?: (file: ts.SourceFile) => void;

  /**
   * JSDoc parsing style to pass through to TypeScript
   */
  jsDocParsingMode: ts.JSDocParsingMode;

  /**
   * Whether parsing of JSX is enabled.
   *
   * @remarks The applicable file extension is still required.
   */
  jsx: boolean;

  /**
   * Whether to add `loc` information to each node.
   */
  loc: boolean;

  /**
   * Log function, if not `console.log`.
   */
  log: (message: string) => void;

  /**
   * Whether two-way AST node maps are preserved during the AST conversion process.
   */
  preserveNodeMaps?: boolean;

  /**
   * One or more instances of TypeScript Program objects to be used for type information.
   */
  programs: Iterable<ts.Program> | null;

  /**
   * Normalized paths to provided project paths.
   */
  projects: ReadonlyMap<CanonicalPath, string>;

  /**
   * TypeScript server to power program creation.
   */
  projectService: ProjectServiceAndMetadata | undefined;

  /**
   * Whether to add the `range` property to AST nodes.
   */
  range: boolean;

  /**
   * Whether this is part of a single run, rather than a long-running process.
   */
  singleRun: boolean;

  /**
   * Whether deprecated AST properties should skip calling console.warn on accesses.
   */
  suppressDeprecatedPropertyWarnings: boolean;

  /**
   * If the `tokens` parse option is enabled, retrieved tokens.
   */
  tokens: TSESTree.Token[] | null;

  /**
   * Caches searches for TSConfigs from project directories.
   */
  tsconfigMatchCache: CacheLike<string, string>;

  /**
   * The absolute path to the root directory for all provided `project`s.
   */
  tsconfigRootDir: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `allowInvalidAST` | `boolean` | ✗ |  |
| `code` | `string | ts.SourceFile` | ✗ |  |
| `codeFullText` | `string` | ✗ |  |
| `comment` | `boolean` | ✗ |  |
| `comments` | `TSESTree.Comment[]` | ✗ |  |
| `debugLevel` | `Set<DebugModule>` | ✗ |  |
| `errorOnTypeScriptSyntacticAndSemanticIssues` | `boolean` | ✗ |  |
| `errorOnUnknownASTType` | `boolean` | ✗ |  |
| `extraFileExtensions` | `string[]` | ✗ |  |
| `filePath` | `string` | ✗ |  |
| `setExternalModuleIndicator` | `(file: ts.SourceFile) => void` | ✓ |  |
| `jsDocParsingMode` | `ts.JSDocParsingMode` | ✗ |  |
| `jsx` | `boolean` | ✗ |  |
| `loc` | `boolean` | ✗ |  |
| `log` | `(message: string) => void` | ✗ |  |
| `preserveNodeMaps` | `boolean` | ✓ |  |
| `programs` | `Iterable<ts.Program> | null` | ✗ |  |
| `projects` | `ReadonlyMap<CanonicalPath, string>` | ✗ |  |
| `projectService` | `ProjectServiceAndMetadata | undefined` | ✗ |  |
| `range` | `boolean` | ✗ |  |
| `singleRun` | `boolean` | ✗ |  |
| `suppressDeprecatedPropertyWarnings` | `boolean` | ✗ |  |
| `tokens` | `TSESTree.Token[] | null` | ✗ |  |
| `tsconfigMatchCache` | `CacheLike<string, string>` | ✗ |  |
| `tsconfigRootDir` | `string` | ✗ |  |


---

## Type Aliases

### `DebugModule`

```ts
type DebugModule = 'eslint' | 'typescript' | 'typescript-eslint';
```

### `ParseSettings`

```ts
type ParseSettings = Readonly<MutableParseSettings>;
```


---

## Enums

### `enum JSDocParsingMode`

<details><summary>Enum Code</summary>

```ts
enum JSDocParsingMode {}
```
</details>

### `enum JSDocParsingMode`

<details><summary>Enum Code</summary>

```ts
enum JSDocParsingMode {}
```
</details>


---