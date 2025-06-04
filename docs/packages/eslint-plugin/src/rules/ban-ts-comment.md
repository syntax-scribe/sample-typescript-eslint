[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ban-ts-comment.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 8 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `defaultMinimumDescriptionLength` | `3` | const | `3` | ✗ |
| `singleLinePragmaRegEx` | `RegExp` | const | `/^\/\/\/?\s*@ts-(?<directive>check|nocheck)(?<description>.*)$/` | ✗ |
| `commentDirectiveRegExSingleLine` | `RegExp` | const | `/^\/*\s*@ts-(?<directive>expect-error|ignore)(?<description>.*)/` | ✗ |
| `commentDirectiveRegExMultiLine` | `RegExp` | const | `/^\s*(?:\/|\*)*\s*@ts-(?<directive>expect-error|ignore)(?<description>.*)/` | ✗ |
| `descriptionFormats` | `Map<string, RegExp>` | const | `new Map<string, RegExp>()` | ✗ |
| `option` | `any` | const | `options[directive]` | ✗ |
| `fullDirective` | `keyof OptionsShape` | const | ``ts-${directive}` as keyof OptionsShape` | ✗ |
| `option` | `any` | const | `options[fullDirective]` | ✗ |


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