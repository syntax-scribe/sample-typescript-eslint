[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `ast-converter.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 0 |
| 📦 Imports | 9 |
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
📂 **`packages/typescript-estree/src/ast-converter.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `SourceFile` | `typescript` |
| `ASTMaps` | `./convert` |
| `ParseSettings` | `./parseSettings` |
| `TSESTree` | `./ts-estree` |
| `Converter` | `./convert` |
| `convertError` | `./convert` |
| `convertComments` | `./convert-comments` |
| `convertTokens` | `./node-utils` |
| `simpleTraverse` | `./simple-traverse` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `instance` | `Converter` | const | `new Converter(ast, {
    allowInvalidAST: parseSettings.allowInvalidAST,
    errorOnUnknownASTType: parseSettings.errorOnUnknownASTType,
    shouldPreserveNodeMaps,
    suppressDeprecatedPropertyWarnings:
      parseSettings.suppressDeprecatedPropertyWarnings,
  })` | ✗ |


---

## Functions

### `astConverter(ast: SourceFile, parseSettings: ParseSettings, shouldPreserveNodeMaps: boolean): { astMaps: ASTMaps; estree: TSESTree.Program }`

<details><summary>Code</summary>

```ts
export function astConverter(
  ast: SourceFile,
  parseSettings: ParseSettings,
  shouldPreserveNodeMaps: boolean,
): { astMaps: ASTMaps; estree: TSESTree.Program } {
  /**
   * The TypeScript compiler produced fundamental parse errors when parsing the
   * source.
   */
  const { parseDiagnostics } = ast;
  if (parseDiagnostics.length) {
    throw convertError(parseDiagnostics[0]);
  }

  /**
   * Recursively convert the TypeScript AST into an ESTree-compatible AST
   */
  const instance = new Converter(ast, {
    allowInvalidAST: parseSettings.allowInvalidAST,
    errorOnUnknownASTType: parseSettings.errorOnUnknownASTType,
    shouldPreserveNodeMaps,
    suppressDeprecatedPropertyWarnings:
      parseSettings.suppressDeprecatedPropertyWarnings,
  });

  const estree = instance.convertProgram();

  /**
   * Optionally remove range and loc if specified
   */
  if (!parseSettings.range || !parseSettings.loc) {
    simpleTraverse(estree, {
      enter: node => {
        if (!parseSettings.range) {
          // eslint-disable-next-line @typescript-eslint/ban-ts-comment -- TS 4.0 made this an error because the types aren't optional
          // @ts-expect-error
          delete node.range;
        }
        if (!parseSettings.loc) {
          // eslint-disable-next-line @typescript-eslint/ban-ts-comment -- TS 4.0 made this an error because the types aren't optional
          // @ts-expect-error
          delete node.loc;
        }
      },
    });
  }

  /**
   * Optionally convert and include all tokens in the AST
   */
  if (parseSettings.tokens) {
    estree.tokens = convertTokens(ast);
  }

  /**
   * Optionally convert and include all comments in the AST
   */
  if (parseSettings.comment) {
    estree.comments = convertComments(ast, parseSettings.codeFullText);
  }

  const astMaps = instance.getASTMaps();

  return { astMaps, estree };
}
```
</details>

- **Parameters**:
  - `ast: SourceFile`
  - `parseSettings: ParseSettings`
  - `shouldPreserveNodeMaps: boolean`
- **Return Type**: `{ astMaps: ASTMaps; estree: TSESTree.Program }`
- **Calls**:
  - `convertError (from ./convert)`
  - `instance.convertProgram`
  - `simpleTraverse (from ./simple-traverse)`
  - `convertTokens (from ./node-utils)`
  - `convertComments (from ./convert-comments)`
  - `instance.getASTMaps`
- **Internal Comments**:
```
/**
   * The TypeScript compiler produced fundamental parse errors when parsing the
   * source.
   */ (x2)
/**
   * Recursively convert the TypeScript AST into an ESTree-compatible AST
   */ (x2)
/**
   * Optionally remove range and loc if specified
   */
// eslint-disable-next-line @typescript-eslint/ban-ts-comment -- TS 4.0 made this an error because the types aren't optional (x4)
// @ts-expect-error (x4)
/**
   * Optionally convert and include all tokens in the AST
   */
/**
   * Optionally convert and include all comments in the AST
   */
```

### `enter(node: TSESTree.Node): void`

<details><summary>Code</summary>

```ts
node => {
        if (!parseSettings.range) {
          // eslint-disable-next-line @typescript-eslint/ban-ts-comment -- TS 4.0 made this an error because the types aren't optional
          // @ts-expect-error
          delete node.range;
        }
        if (!parseSettings.loc) {
          // eslint-disable-next-line @typescript-eslint/ban-ts-comment -- TS 4.0 made this an error because the types aren't optional
          // @ts-expect-error
          delete node.loc;
        }
      }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `void`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/ban-ts-comment -- TS 4.0 made this an error because the types aren't optional (x4)
// @ts-expect-error (x4)
```

### `enter(node: TSESTree.Node): void`

<details><summary>Code</summary>

```ts
node => {
        if (!parseSettings.range) {
          // eslint-disable-next-line @typescript-eslint/ban-ts-comment -- TS 4.0 made this an error because the types aren't optional
          // @ts-expect-error
          delete node.range;
        }
        if (!parseSettings.loc) {
          // eslint-disable-next-line @typescript-eslint/ban-ts-comment -- TS 4.0 made this an error because the types aren't optional
          // @ts-expect-error
          delete node.loc;
        }
      }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `void`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/ban-ts-comment -- TS 4.0 made this an error because the types aren't optional (x4)
// @ts-expect-error (x4)
```


---