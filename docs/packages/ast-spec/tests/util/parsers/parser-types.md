[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `parser-types.ts`

## 📚 Table of Contents

- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 5
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/ast-spec/tests/util/parsers/parser-types.ts`**

## 📦 Imports

> No imports found in this file.


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `SuccessSnapshotPaths`

<details><summary>Interface Code</summary>

```ts
interface SuccessSnapshotPaths {
  readonly ast: SnapshotPathFn;
  readonly tokens: SnapshotPathFn;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `ast` | `SnapshotPathFn` | ✗ |  |
| `tokens` | `SnapshotPathFn` | ✗ |  |

### `ASTFixtureConfig`

<details><summary>Interface Code</summary>

```ts
export interface ASTFixtureConfig {
  /**
   * Prevents the parser from throwing an error if it receives an invalid AST from TypeScript.
   * This case only usually occurs when attempting to lint invalid code.
   */
  readonly allowInvalidAST?: boolean;

  /**
   * Specifies that we expect that babel doesn't yet support the code in this fixture, so we expect that it will error.
   * This should not be used if we expect babel to throw for this feature due to a valid parser error!
   *
   * The value should be a description of why there isn't support - for example a github issue URL.
   */
  readonly expectBabelToNotSupport?: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `allowInvalidAST` | `boolean` | ✓ |  |
| `expectBabelToNotSupport` | `string` | ✓ |  |

### `Fixture`

<details><summary>Interface Code</summary>

```ts
export interface Fixture {
  readonly absolute: string;
  readonly babelParsed: ParserResponse;
  readonly config: ASTFixtureConfig;
  readonly contents: string;
  readonly errorLabel: ErrorLabel;
  readonly ext: string;
  readonly isBabelError: boolean;
  readonly isError: boolean;
  readonly isJSX: boolean;
  readonly isTSESTreeError: boolean;
  readonly name: string;
  readonly relative: string;
  readonly segments: string[];
  readonly TSESTreeParsed: ParserResponse;
  readonly snapshotFiles: {
    readonly error: {
      readonly alignment: SnapshotPathFn;
      readonly babel: SnapshotPathFn;
      readonly tsestree: SnapshotPathFn;
    };
    readonly success: {
      readonly alignment: SuccessSnapshotPaths;
      readonly babel: SuccessSnapshotPaths;
      readonly tsestree: SuccessSnapshotPaths;
    };
  };
  readonly snapshotPath: string;
  readonly vitestSnapshotHeader: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `absolute` | `string` | ✗ |  |
| `babelParsed` | `ParserResponse` | ✗ |  |
| `config` | `ASTFixtureConfig` | ✗ |  |
| `contents` | `string` | ✗ |  |
| `errorLabel` | `ErrorLabel` | ✗ |  |
| `ext` | `string` | ✗ |  |
| `isBabelError` | `boolean` | ✗ |  |
| `isError` | `boolean` | ✗ |  |
| `isJSX` | `boolean` | ✗ |  |
| `isTSESTreeError` | `boolean` | ✗ |  |
| `name` | `string` | ✗ |  |
| `relative` | `string` | ✗ |  |
| `segments` | `string[]` | ✗ |  |
| `TSESTreeParsed` | `ParserResponse` | ✗ |  |
| `snapshotFiles` | `{
    readonly error: {
      readonly alignment: SnapshotPathFn;
      readonly babel: SnapshotPathFn;
      readonly tsestree: SnapshotPathFn;
    };
    readonly success: {
      readonly alignment: SuccessSnapshotPaths;
      readonly babel: SuccessSnapshotPaths;
      readonly tsestree: SuccessSnapshotPaths;
    };
  }` | ✗ |  |
| `snapshotPath` | `string` | ✗ |  |
| `vitestSnapshotHeader` | `string` | ✗ |  |

### `ParserResponseSuccess`

<details><summary>Interface Code</summary>

```ts
export interface ParserResponseSuccess {
  readonly ast: unknown;
  // this exists for the error alignment test snapshots
  readonly error: 'NO ERROR';
  readonly tokens: unknown;
  readonly type: ParserResponseType.NoError;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `ast` | `unknown` | ✗ |  |
| `error` | `'NO ERROR'` | ✗ |  |
| `tokens` | `unknown` | ✗ |  |
| `type` | `ParserResponseType.NoError` | ✗ |  |

### `ParserResponseError`

<details><summary>Interface Code</summary>

```ts
export interface ParserResponseError {
  readonly error: unknown;
  readonly type: ParserResponseType.Error;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `error` | `unknown` | ✗ |  |
| `type` | `ParserResponseType.Error` | ✗ |  |


---

## Type Aliases

### `SnapshotPathFn`

```ts
type SnapshotPathFn = (i: number) => string;
```

### `ParserResponse`

```ts
type ParserResponse = ParserResponseError | ParserResponseSuccess;
```


---