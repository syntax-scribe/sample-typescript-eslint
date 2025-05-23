[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ban-ts-comment.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 2
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/ban-ts-comment.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getStringLength` | `../util` |
| `nullThrows` | `../util` |


---

## Functions

### `execDirectiveRegEx(regex: RegExp, str: string): MatchedTSDirective | null`

<details><summary>Code</summary>

```ts
function execDirectiveRegEx(
      regex: RegExp,
      str: string,
    ): MatchedTSDirective | null {
      const match = regex.exec(str);
      if (!match) {
        return null;
      }

      const { description, directive } = nullThrows(
        match.groups,
        'RegExp should contain groups',
      );
      return {
        description: nullThrows(
          description,
          'RegExp should contain "description" group',
        ),
        directive: nullThrows(
          directive,
          'RegExp should contain "directive" group',
        ),
      };
    }
```
</details>

- **Parameters**:
  - `regex: RegExp`
  - `str: string`
- **Return Type**: `MatchedTSDirective | null`
- **Calls**:
  - `regex.exec`
  - `nullThrows (from ../util)`
### `findDirectiveInComment(comment: TSESTree.Comment): MatchedTSDirective | null`

<details><summary>Code</summary>

```ts
function findDirectiveInComment(
      comment: TSESTree.Comment,
    ): MatchedTSDirective | null {
      if (comment.type === AST_TOKEN_TYPES.Line) {
        const matchedPragma = execDirectiveRegEx(
          singleLinePragmaRegEx,
          `//${comment.value}`,
        );
        if (matchedPragma) {
          return matchedPragma;
        }

        return execDirectiveRegEx(
          commentDirectiveRegExSingleLine,
          comment.value,
        );
      }

      const commentLines = comment.value.split('\n');
      return execDirectiveRegEx(
        commentDirectiveRegExMultiLine,
        commentLines[commentLines.length - 1],
      );
    }
```
</details>

- **Parameters**:
  - `comment: TSESTree.Comment`
- **Return Type**: `MatchedTSDirective | null`
- **Calls**:
  - `execDirectiveRegEx`
  - `comment.value.split`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `OptionsShape`

<details><summary>Interface Code</summary>

```ts
export interface OptionsShape {
  minimumDescriptionLength?: number;
  'ts-check'?: DirectiveConfig;
  'ts-expect-error'?: DirectiveConfig;
  'ts-ignore'?: DirectiveConfig;
  'ts-nocheck'?: DirectiveConfig;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `minimumDescriptionLength` | `number` | ✓ |  |
| `'ts-check'` | `DirectiveConfig` | ✓ |  |
| `'ts-expect-error'` | `DirectiveConfig` | ✓ |  |
| `'ts-ignore'` | `DirectiveConfig` | ✓ |  |
| `'ts-nocheck'` | `DirectiveConfig` | ✓ |  |

### `MatchedTSDirective`

<details><summary>Interface Code</summary>

```ts
interface MatchedTSDirective {
  description: string;
  directive: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `description` | `string` | ✗ |  |
| `directive` | `string` | ✗ |  |


---

## Type Aliases

### `DirectiveConfig`

```ts
type DirectiveConfig = | boolean
  | 'allow-with-description'
  | { descriptionFormat: string };
```

### `Options`

```ts
type Options = [OptionsShape];
```

### `MessageIds`

```ts
type MessageIds = | 'replaceTsIgnoreWithTsExpectError'
  | 'tsDirectiveComment'
  | 'tsDirectiveCommentDescriptionNotMatchPattern'
  | 'tsDirectiveCommentRequiresDescription'
  | 'tsIgnoreInsteadOfExpectError';
```


---