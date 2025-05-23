[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-ts-expect-error.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 5
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 1

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = 'preferExpectErrorComment';
```


---