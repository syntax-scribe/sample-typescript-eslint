[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `fixtures.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 120
- **Classes**: 0
- **Imports**: 13
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Functions

### `alignment(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `babel(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tsestree(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `alignment(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `babel(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tsestree(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `alignment(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `babel(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tsestree(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `alignment(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `babel(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tsestree(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `alignment(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `babel(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tsestree(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `alignment(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `babel(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tsestree(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `alignment(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `babel(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tsestree(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `alignment(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Alignment-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `babel(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-Babel-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tsestree(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
              path.join(snapshotPath, `${i.toString()}-TSESTree-Error.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

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
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-Babel-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `ast(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-AST.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`
### `tokens(i: number): any`

<details><summary>Code</summary>

```ts
(i: number) =>
                path.join(snapshotPath, `${i.toString()}-TSESTree-Tokens.shot`)
```
</details>

- **Parameters**:
  - `i: number`
- **Return Type**: `any`
- **Calls**:
  - `path.join`

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