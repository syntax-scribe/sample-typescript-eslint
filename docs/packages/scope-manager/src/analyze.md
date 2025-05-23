[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `analyze.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/src/analyze.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Lib` | `@typescript-eslint/types` |
| `SourceType` | `@typescript-eslint/types` |
| `TSESTree` | `@typescript-eslint/types` |
| `visitorKeys` | `@typescript-eslint/visitor-keys` |
| `ReferencerOptions` | `./referencer` |
| `Referencer` | `./referencer` |
| `ScopeManager` | `./ScopeManager` |


---

## Functions

### `analyze(tree: TSESTree.Node, providedOptions: AnalyzeOptions): ScopeManager`

<details><summary>Code</summary>

```ts
export function analyze(
  tree: TSESTree.Node,
  providedOptions?: AnalyzeOptions,
): ScopeManager {
  const options: Required<AnalyzeOptions> = {
    childVisitorKeys:
      providedOptions?.childVisitorKeys ?? DEFAULT_OPTIONS.childVisitorKeys,
    emitDecoratorMetadata: false,
    globalReturn: providedOptions?.globalReturn ?? DEFAULT_OPTIONS.globalReturn,
    impliedStrict:
      providedOptions?.impliedStrict ?? DEFAULT_OPTIONS.impliedStrict,
    jsxFragmentName:
      providedOptions?.jsxFragmentName ?? DEFAULT_OPTIONS.jsxFragmentName,
    jsxPragma:
      // eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
      providedOptions?.jsxPragma === undefined
        ? DEFAULT_OPTIONS.jsxPragma
        : providedOptions.jsxPragma,
    lib: providedOptions?.lib ?? ['esnext'],
    sourceType: providedOptions?.sourceType ?? DEFAULT_OPTIONS.sourceType,
  };

  // ensure the option is lower cased
  options.lib = options.lib.map(l => l.toLowerCase() as Lib);

  const scopeManager = new ScopeManager(options);
  const referencer = new Referencer(options, scopeManager);

  referencer.visit(tree);

  return scopeManager;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Takes an AST and returns the analyzed scopes.
 */
```

- **Parameters**:
  - `tree: TSESTree.Node`
  - `providedOptions: AnalyzeOptions`
- **Return Type**: `ScopeManager`
- **Calls**:
  - `options.lib.map`
  - `l.toLowerCase`
  - `referencer.visit`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish (x4)
// ensure the option is lower cased (x4)
```


---

## Classes

> No classes found in this file.


---

## Interfaces

### `AnalyzeOptions`

<details><summary>Interface Code</summary>

```ts
export interface AnalyzeOptions {
  /**
   * Known visitor keys.
   */
  childVisitorKeys?: ReferencerOptions['childVisitorKeys'];

  /**
   * Whether the whole script is executed under node.js environment.
   * When enabled, the scope manager adds a function scope immediately following the global scope.
   * Defaults to `false`.
   */
  globalReturn?: boolean;

  /**
   * Implied strict mode.
   * Defaults to `false`.
   */
  impliedStrict?: boolean;

  /**
   * The identifier that's used for JSX Element creation (after transpilation).
   * This should not be a member expression - just the root identifier (i.e. use "React" instead of "React.createElement").
   * Defaults to `"React"`.
   */
  jsxPragma?: string | null;

  /**
   * The identifier that's used for JSX fragment elements (after transpilation).
   * If `null`, assumes transpilation will always use a member on `jsxFactory` (i.e. React.Fragment).
   * This should not be a member expression - just the root identifier (i.e. use "h" instead of "h.Fragment").
   * Defaults to `null`.
   */
  jsxFragmentName?: string | null;

  /**
   * The lib used by the project.
   * This automatically defines a type variable for any types provided by the configured TS libs.
   * Defaults to ['esnext'].
   *
   * https://www.typescriptlang.org/tsconfig#lib
   */
  lib?: Lib[];

  /**
   * The source type of the script.
   */
  sourceType?: SourceType;

  // TODO - remove this in v10
  /**
   * @deprecated This option never did what it was intended for and will be removed in a future major release.
   */
  emitDecoratorMetadata?: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `childVisitorKeys` | `ReferencerOptions['childVisitorKeys']` | ✓ |  |
| `globalReturn` | `boolean` | ✓ |  |
| `impliedStrict` | `boolean` | ✓ |  |
| `jsxPragma` | `string | null` | ✓ |  |
| `jsxFragmentName` | `string | null` | ✓ |  |
| `lib` | `Lib[]` | ✓ |  |
| `sourceType` | `SourceType` | ✓ |  |
| `emitDecoratorMetadata` | `boolean` | ✓ |  |


---

## Type Aliases

> No type aliases found in this file.


---