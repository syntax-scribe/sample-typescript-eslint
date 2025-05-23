[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `parser.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 4
- **Classes**: 0
- **Imports**: 14
- **Interfaces**: 2
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/parser/src/parser.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AnalyzeOptions` | `@typescript-eslint/scope-manager` |
| `ScopeManager` | `@typescript-eslint/scope-manager` |
| `Lib` | `@typescript-eslint/types` |
| `ParserOptions` | `@typescript-eslint/types` |
| `TSESTree` | `@typescript-eslint/types` |
| `AST` | `@typescript-eslint/typescript-estree` |
| `ParserServices` | `@typescript-eslint/typescript-estree` |
| `TSESTreeOptions` | `@typescript-eslint/typescript-estree` |
| `VisitorKeys` | `@typescript-eslint/visitor-keys` |
| `analyze` | `@typescript-eslint/scope-manager` |
| `parseAndGenerateServices` | `@typescript-eslint/typescript-estree` |
| `visitorKeys` | `@typescript-eslint/visitor-keys` |
| `debug` | `debug` |
| `ScriptTarget` | `typescript` |


---

## Functions

### `validateBoolean(value: boolean | undefined, fallback: boolean): boolean`

<details><summary>Code</summary>

```ts
function validateBoolean(
  value: boolean | undefined,
  fallback = false,
): boolean {
  if (typeof value !== 'boolean') {
    return fallback;
  }
  return value;
}
```
</details>

- **Parameters**:
  - `value: boolean | undefined`
  - `fallback: boolean`
- **Return Type**: `boolean`
### `getLib(compilerOptions: ts.CompilerOptions): Lib[]`

<details><summary>Code</summary>

```ts
function getLib(compilerOptions: ts.CompilerOptions): Lib[] {
  if (compilerOptions.lib) {
    return compilerOptions.lib
      .map(lib => LIB_FILENAME_REGEX.exec(lib.toLowerCase())?.[1])
      .filter((lib): lib is Lib => !!lib);
  }

  const target = compilerOptions.target ?? ScriptTarget.ES5;
  // https://github.com/microsoft/TypeScript/blob/ae582a22ee1bb052e19b7c1bc4cac60509b574e0/src/compiler/utilitiesPublic.ts#L13-L36
  switch (target) {
    case ScriptTarget.ES2015:
      return ['es6'];
    case ScriptTarget.ES2016:
      return ['es2016.full'];
    case ScriptTarget.ES2017:
      return ['es2017.full'];
    case ScriptTarget.ES2018:
      return ['es2018.full'];
    case ScriptTarget.ES2019:
      return ['es2019.full'];
    case ScriptTarget.ES2020:
      return ['es2020.full'];
    case ScriptTarget.ES2021:
      return ['es2021.full'];
    case ScriptTarget.ES2022:
      return ['es2022.full'];
    case ScriptTarget.ES2023:
      return ['es2023.full'];
    case ScriptTarget.ES2024:
      return ['es2024.full'];
    case ScriptTarget.ESNext:
      return ['esnext.full'];
    default:
      return ['lib'];
  }
}
```
</details>

- **Parameters**:
  - `compilerOptions: ts.CompilerOptions`
- **Return Type**: `Lib[]`
- **Calls**:
  - `compilerOptions.lib
      .map(lib => LIB_FILENAME_REGEX.exec(lib.toLowerCase())?.[1])
      .filter`
- **Internal Comments**:
```
// https://github.com/microsoft/TypeScript/blob/ae582a22ee1bb052e19b7c1bc4cac60509b574e0/src/compiler/utilitiesPublic.ts#L13-L36
```

### `parse(code: string | ts.SourceFile, options: ParserOptions): ParseForESLintResult['ast']`

<details><summary>Code</summary>

```ts
export function parse(
  code: string | ts.SourceFile,
  options?: ParserOptions,
): ParseForESLintResult['ast'] {
  return parseForESLint(code, options).ast;
}
```
</details>

- **Parameters**:
  - `code: string | ts.SourceFile`
  - `options: ParserOptions`
- **Return Type**: `ParseForESLintResult['ast']`
- **Calls**:
  - `parseForESLint`
### `parseForESLint(code: string | ts.SourceFile, parserOptions: ParserOptions | null): ParseForESLintResult`

<details><summary>Code</summary>

```ts
export function parseForESLint(
  code: string | ts.SourceFile,
  parserOptions?: ParserOptions | null,
): ParseForESLintResult {
  if (!parserOptions || typeof parserOptions !== 'object') {
    parserOptions = {};
  } else {
    parserOptions = { ...parserOptions };
  }
  // https://eslint.org/docs/user-guide/configuring#specifying-parser-options
  // if sourceType is not provided by default eslint expect that it will be set to "script"
  if (
    parserOptions.sourceType !== 'module' &&
    parserOptions.sourceType !== 'script'
  ) {
    parserOptions.sourceType = 'script';
  }
  if (typeof parserOptions.ecmaFeatures !== 'object') {
    parserOptions.ecmaFeatures = {};
  }

  /**
   * Allow the user to suppress the warning from typescript-estree if they are using an unsupported
   * version of TypeScript
   */
  const warnOnUnsupportedTypeScriptVersion = validateBoolean(
    parserOptions.warnOnUnsupportedTypeScriptVersion,
    true,
  );

  const tsestreeOptions = {
    jsx: validateBoolean(parserOptions.ecmaFeatures.jsx),
    ...(!warnOnUnsupportedTypeScriptVersion && { loggerFn: false }),
    ...parserOptions,
    // Override errorOnTypeScriptSyntacticAndSemanticIssues and set it to false to prevent use from user config
    // https://github.com/typescript-eslint/typescript-eslint/issues/8681#issuecomment-2000411834
    errorOnTypeScriptSyntacticAndSemanticIssues: false,
    // comment, loc, range, and tokens should always be set for ESLint usage
    // https://github.com/typescript-eslint/typescript-eslint/issues/8347
    comment: true,
    loc: true,
    range: true,
    tokens: true,
  } satisfies TSESTreeOptions;

  const analyzeOptions: AnalyzeOptions = {
    globalReturn: parserOptions.ecmaFeatures.globalReturn,
    jsxFragmentName: parserOptions.jsxFragmentName,
    jsxPragma: parserOptions.jsxPragma,
    lib: parserOptions.lib,
    sourceType: parserOptions.sourceType,
  };

  const { ast, services } = parseAndGenerateServices(code, tsestreeOptions);
  ast.sourceType = parserOptions.sourceType;

  if (services.program) {
    // automatically apply the options configured for the program
    const compilerOptions = services.program.getCompilerOptions();
    if (analyzeOptions.lib == null) {
      analyzeOptions.lib = getLib(compilerOptions);
      log('Resolved libs from program: %o', analyzeOptions.lib);
    }
    if (
      // eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
      analyzeOptions.jsxPragma === undefined &&
      compilerOptions.jsxFactory != null
    ) {
      // in case the user has specified something like "preact.h"
      const factory = compilerOptions.jsxFactory.split('.')[0].trim();
      analyzeOptions.jsxPragma = factory;
      log('Resolved jsxPragma from program: %s', analyzeOptions.jsxPragma);
    }
    if (
      // eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
      analyzeOptions.jsxFragmentName === undefined &&
      compilerOptions.jsxFragmentFactory != null
    ) {
      // in case the user has specified something like "preact.Fragment"
      const fragFactory = compilerOptions.jsxFragmentFactory
        .split('.')[0]
        .trim();
      analyzeOptions.jsxFragmentName = fragFactory;
      log(
        'Resolved jsxFragmentName from program: %s',
        analyzeOptions.jsxFragmentName,
      );
    }
  }

  const scopeManager = analyze(ast, analyzeOptions);

  // if not defined - override from the parserOptions
  services.emitDecoratorMetadata ??=
    parserOptions.emitDecoratorMetadata === true;
  services.experimentalDecorators ??=
    parserOptions.experimentalDecorators === true;
  services.isolatedDeclarations ??= parserOptions.isolatedDeclarations === true;

  return { ast, scopeManager, services, visitorKeys };
}
```
</details>

- **Parameters**:
  - `code: string | ts.SourceFile`
  - `parserOptions: ParserOptions | null`
- **Return Type**: `ParseForESLintResult`
- **Calls**:
  - `validateBoolean`
  - `parseAndGenerateServices (from @typescript-eslint/typescript-estree)`
  - `services.program.getCompilerOptions`
  - `getLib`
  - `log`
  - `compilerOptions.jsxFactory.split('.')[0].trim`
  - `compilerOptions.jsxFragmentFactory
        .split('.')[0]
        .trim`
  - `analyze (from @typescript-eslint/scope-manager)`
- **Internal Comments**:
```
// https://eslint.org/docs/user-guide/configuring#specifying-parser-options
// if sourceType is not provided by default eslint expect that it will be set to "script"
/**
   * Allow the user to suppress the warning from typescript-estree if they are using an unsupported
   * version of TypeScript
   */ (x2)
// Override errorOnTypeScriptSyntacticAndSemanticIssues and set it to false to prevent use from user config (x2)
// https://github.com/typescript-eslint/typescript-eslint/issues/8681#issuecomment-2000411834 (x2)
// comment, loc, range, and tokens should always be set for ESLint usage (x2)
// https://github.com/typescript-eslint/typescript-eslint/issues/8347 (x2)
// automatically apply the options configured for the program (x2)
// eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish (x8)
// in case the user has specified something like "preact.h" (x2)
// in case the user has specified something like "preact.Fragment" (x2)
// if not defined - override from the parserOptions (x4)
```


---

## Classes

> No classes found in this file.


---

## Interfaces

### `ESLintProgram`

<details><summary>Interface Code</summary>

```ts
interface ESLintProgram extends AST<{ comment: true; tokens: true }> {
  comments: TSESTree.Comment[];
  range: [number, number];
  tokens: TSESTree.Token[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `comments` | `TSESTree.Comment[]` | ✗ |  |
| `range` | `[number, number]` | ✗ |  |
| `tokens` | `TSESTree.Token[]` | ✗ |  |

### `ParseForESLintResult`

<details><summary>Interface Code</summary>

```ts
interface ParseForESLintResult {
  ast: ESLintProgram;
  scopeManager: ScopeManager;
  services: ParserServices;
  visitorKeys: VisitorKeys;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `ast` | `ESLintProgram` | ✗ |  |
| `scopeManager` | `ScopeManager` | ✗ |  |
| `services` | `ParserServices` | ✗ |  |
| `visitorKeys` | `VisitorKeys` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---