[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-ts-expect-error.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 5 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 2 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-ts-expect-error.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `RuleFix` | `@typescript-eslint/utils/ts-eslint` |
| `RuleFixer` | `@typescript-eslint/utils/ts-eslint` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `tsIgnoreRegExpSingleLine` | `RegExp` | const | `/^\s*\/?\s*@ts-ignore/` | ✗ |
| `tsIgnoreRegExpMultiLine` | `RegExp` | const | `/^\s*(?:\/|\*)*\s*@ts-ignore/` | ✗ |


---

## Functions

### `isLineComment(comment: TSESTree.Comment): boolean`

<details><summary>Code</summary>

```ts
function isLineComment(comment: TSESTree.Comment): boolean {
      return comment.type === AST_TOKEN_TYPES.Line;
    }
```
</details>

- **Parameters**:
  - `comment: TSESTree.Comment`
- **Return Type**: `boolean`
### `getLastCommentLine(comment: TSESTree.Comment): string`

<details><summary>Code</summary>

```ts
function getLastCommentLine(comment: TSESTree.Comment): string {
      if (isLineComment(comment)) {
        return comment.value;
      }

      // For multiline comments - we look at only the last line.
      const commentlines = comment.value.split('\n');
      return commentlines[commentlines.length - 1];
    }
```
</details>

- **Parameters**:
  - `comment: TSESTree.Comment`
- **Return Type**: `string`
- **Calls**:
  - `isLineComment`
  - `comment.value.split`
- **Internal Comments**:
```
// For multiline comments - we look at only the last line. (x2)
```

### `isValidTsIgnorePresent(comment: TSESTree.Comment): boolean`

<details><summary>Code</summary>

```ts
function isValidTsIgnorePresent(comment: TSESTree.Comment): boolean {
      const line = getLastCommentLine(comment);
      return isLineComment(comment)
        ? tsIgnoreRegExpSingleLine.test(line)
        : tsIgnoreRegExpMultiLine.test(line);
    }
```
</details>

- **Parameters**:
  - `comment: TSESTree.Comment`
- **Return Type**: `boolean`
- **Calls**:
  - `getLastCommentLine`
  - `isLineComment`
  - `tsIgnoreRegExpSingleLine.test`
  - `tsIgnoreRegExpMultiLine.test`
### `lineCommentRuleFixer(fixer: RuleFixer): RuleFix`

<details><summary>Code</summary>

```ts
(fixer: RuleFixer): RuleFix =>
              fixer.replaceText(
                comment,
                `//${comment.value.replace('@ts-ignore', '@ts-expect-error')}`,
              )
```
</details>

- **Parameters**:
  - `fixer: RuleFixer`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.replaceText`
### `blockCommentRuleFixer(fixer: RuleFixer): RuleFix`

<details><summary>Code</summary>

```ts
(fixer: RuleFixer): RuleFix =>
              fixer.replaceText(
                comment,
                `/*${comment.value.replace(
                  '@ts-ignore',
                  '@ts-expect-error',
                )}*/`,
              )
```
</details>

- **Parameters**:
  - `fixer: RuleFixer`
- **Return Type**: `RuleFix`
- **Calls**:
  - `fixer.replaceText`

---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = 'preferExpectErrorComment';
```


---