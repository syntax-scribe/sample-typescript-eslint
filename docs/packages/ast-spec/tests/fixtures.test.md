[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `fixtures.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 240 |
| 🧱 Classes | 0 |
| 📦 Imports | 13 |
| 📊 Variables & Constants | 13 |
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
📂 **`packages/ast-spec/tests/fixtures.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `glob` | `glob` |
| `pathToFileURL` | `node:url` |
| `VitestSnapshotEnvironment` | `vitest/snapshot` |
| `ASTFixtureConfig` | `./util/parsers/parser-types.js` |
| `Fixture` | `./util/parsers/parser-types.js` |
| `getErrorLabel` | `./util/getErrorLabel.js` |
| `parseBabel` | `./util/parsers/babel.js` |
| `ErrorLabel` | `./util/parsers/parser-types.js` |
| `ParserResponseType` | `./util/parsers/parser-types.js` |
| `parseTSESTree` | `./util/parsers/typescript-estree.js` |
| `serializeError` | `./util/serialize-error.js` |
| `diffHasChanges` | `./util/snapshot-diff.js` |
| `snapshotDiff` | `./util/snapshot-diff.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `fixturesWithASTDifferences` | `Map<string, string>` | const | `new Map<string, string>()` | ✗ |
| `fixturesWithTokenDifferences` | `Map<string, string>` | const | `new Map<string, string>()` | ✗ |
| `fixturesConfiguredToExpectBabelToNotSupport` | `Map<string, string>` | const | `new Map<string, string>()` | ✗ |
| `fixturesWithErrorDifferences` | `{ readonly "Babel errored but TSESTree didn't": Set<string>; readonly "TSESTree errored but Babel didn't": Set<string>; }` | const | `{
  [ErrorLabel.Babel]: new Set<string>(),
  [ErrorLabel.TSESTree]: new Set<string>(),
} as const` | ✗ |
| `VALID_FIXTURES` | `any` | let/var | `await glob(
    ['**/fixtures/*/fixture.ts?(x)', '**/fixtures/_error_/*/fixture.ts?(x)'],
    {
      absolute: true,
      cwd: SRC_DIR,
    },
  )` | ✗ |
| `configModule` | `any` | let/var | `await import(pathToFileURL(configPath).href)` | ✗ |
| `config` | `ASTFixtureConfig` | let/var | `await (async (): Promise<ASTFixtureConfig> => {
        try {
          const configModule = await import(pathToFileURL(configPath).href);
          return configModule.default;
        } catch {
          return {};
        }
      })()` | ✗ |
| `vitestSnapshotEnvironment` | `any` | let/var | `new VitestSnapshotEnvironment({
        snapshotsDirName: snapshotPath,
      })` | ✗ |
| `contents` | `string` | let/var | `await fs.readFile(absolute, {
        encoding: 'utf-8',
      })` | ✗ |
| `isBabelError` | `boolean` | let/var | `babelParsed.type === ParserResponseType.Error` | ✗ |
| `isTSESTreeError` | `boolean` | let/var | `TSESTreeParsed.type === ParserResponseType.Error` | ✗ |
| `FIXTURES` | `readonly Fixture[]` | let/var | `await Promise.all(
    VALID_FIXTURES.map(async absolute => {
      const relativeToSrc = path.relative(SRC_DIR, absolute);
      const { base, dir, ext } = path.parse(relativeToSrc);
      const directorySegments = dir.split(path.sep);
      const segments = directorySegments.filter(
        segment => segment !== 'fixtures',
      );

      const name = segments.pop();

      assert.isDefined(name);

      const fixtureDir = path.join(SRC_DIR, dir);
      const configPath = path.join(fixtureDir, 'config.js');
      const snapshotPath = path.join(fixtureDir, 'snapshots');

      const config = await (async (): Promise<ASTFixtureConfig> => {
        try {
          const configModule = await import(pathToFileURL(configPath).href);
          return configModule.default;
        } catch {
          return {};
        }
      })();

      const isJSX = ext.endsWith('x');
      const isError = directorySegments.includes('_error_');
      const relative = path.posix.join(...directorySegments, base);

      const vitestSnapshotEnvironment = new VitestSnapshotEnvironment({
        snapshotsDirName: snapshotPath,
      });

      const vitestSnapshotHeader = vitestSnapshotEnvironment.getHeader();

      const contents = await fs.readFile(absolute, {
        encoding: 'utf-8',
      });

      await fs.mkdir(snapshotPath, { recursive: true });

      const TSESTreeParsed = parseTSESTree({ config, contents, isJSX });
      const babelParsed = parseBabel({ contents, isJSX });
      const isBabelError = babelParsed.type === ParserResponseType.Error;
      const isTSESTreeError = TSESTreeParsed.type === ParserResponseType.Error;

      const errorLabel = getErrorLabel(isBabelError, isTSESTreeError);

      if (
        errorLabel === ErrorLabel.TSESTree ||
        errorLabel === ErrorLabel.Babel
      ) {
        fixturesWithErrorDifferences[errorLabel].add(relative);
      }

      if (config.expectBabelToNotSupport != null) {
        fixturesConfiguredToExpectBabelToNotSupport.set(
          relative,
          config.expectBabelToNotSupport,
        );
      }

      if (
        TSESTreeParsed.type === ParserResponseType.NoError &&
        babelParsed.type === ParserResponseType.NoError
      ) {
        const diffAstResult = snapshotDiff(
          'TSESTree',
          TSESTreeParsed.ast,
          'Babel',
          babelParsed.ast,
        );

        const diffTokensResult = snapshotDiff(
          'TSESTree',
          TSESTreeParsed.tokens,
          'Babel',
          babelParsed.tokens,
        );

        if (diffHasChanges(diffAstResult)) {
          fixturesWithASTDifferences.set(relative, diffAstResult);
        }

        if (diffHasChanges(diffTokensResult)) {
          fixturesWithTokenDifferences.set(relative, diffTokensResult);
        }
      }

      return {
        absolute,
        babelParsed,
        config,
        contents,
        errorLabel,
        ext,
        isBabelError,
        isError,
        isJSX,
        isTSESTreeError,
        name,
        relative,
        segments,
        snapshotFiles: {
          error: {
            alignment: (i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`),

            babel: (i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`),

            tsestree: (i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`),
          },

          success: {
            alignment: {
              ast: (i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                ),

              tokens: (i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                ),
            },

            babel: {
              ast: (i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`),

              tokens: (i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`),
            },

            tsestree: {
              ast: (i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`),

              tokens: (i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`),
            },
          },
        },

        snapshotPath,
        TSESTreeParsed,
        vitestSnapshotHeader,
      } satisfies Fixture;
    }),
  )` | ✗ |
| `hasExpectBabelToNotSupport` | `boolean` | const | `config.expectBabelToNotSupport != null` | ✗ |


---

## Functions

### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `alignment(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `babel(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tsestree(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-AST.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(
                  snapshotPath,
                  `${i.toString()}-AST-Alignment-Tokens.shot`,
                )
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `ast(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `tokens(i: number): string`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `string`
- **Calls**:
  - `path.join`

---