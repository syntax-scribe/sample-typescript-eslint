[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ban-tslint-comment.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/ban-tslint-comment.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ENABLE_DISABLE_REGEX` | `RegExp` | const | `/^\s*tslint:(enable|disable)(?:-(line|next-line))?(:|\s|$)/` | ✗ |


---

## Functions

### `toText(text: string, type: AST_TOKEN_TYPES.Block | AST_TOKEN_TYPES.Line): string`

<details><summary>Code</summary>

```ts
(
  text: string,
  type: AST_TOKEN_TYPES.Block | AST_TOKEN_TYPES.Line,
): string =>
  type === AST_TOKEN_TYPES.Line
    ? ['//', text.trim()].join(' ')
    : ['/*', text.trim(), '*/'].join(' ')
```
</details>

- **Parameters**:
  - `text: string`
  - `type: AST_TOKEN_TYPES.Block | AST_TOKEN_TYPES.Line`
- **Return Type**: `string`
### `create(context: any): { Program(): void; }`

<details><summary>Code</summary>

```ts
context => {
    return {
      Program(): void {
        const comments = context.sourceCode.getAllComments();
        comments.forEach(c => {
          if (ENABLE_DISABLE_REGEX.test(c.value)) {
            context.report({
              node: c,
              messageId: 'commentDetected',
              data: { text: toText(c.value, c.type) },
              fix(fixer) {
                const rangeStart = context.sourceCode.getIndexFromLoc({
                  column: c.loc.start.column > 0 ? c.loc.start.column - 1 : 0,
                  line: c.loc.start.line,
                });
                const rangeEnd = context.sourceCode.getIndexFromLoc({
                  column: c.loc.end.column,
                  line: c.loc.end.line,
                });
                return fixer.removeRange([rangeStart, rangeEnd + 1]);
              },
            });
          }
        });
      },
    };
  }
```
</details>

- **Parameters**:
  - `context: any`
- **Return Type**: `{ Program(): void; }`
- **Calls**:
  - `context.sourceCode.getAllComments`
  - `comments.forEach`
  - `ENABLE_DISABLE_REGEX.test`
  - `context.report`
  - `toText`
  - `context.sourceCode.getIndexFromLoc`
  - `fixer.removeRange`
### `create(context: any): { Program(): void; }`

<details><summary>Code</summary>

```ts
context => {
    return {
      Program(): void {
        const comments = context.sourceCode.getAllComments();
        comments.forEach(c => {
          if (ENABLE_DISABLE_REGEX.test(c.value)) {
            context.report({
              node: c,
              messageId: 'commentDetected',
              data: { text: toText(c.value, c.type) },
              fix(fixer) {
                const rangeStart = context.sourceCode.getIndexFromLoc({
                  column: c.loc.start.column > 0 ? c.loc.start.column - 1 : 0,
                  line: c.loc.start.line,
                });
                const rangeEnd = context.sourceCode.getIndexFromLoc({
                  column: c.loc.end.column,
                  line: c.loc.end.line,
                });
                return fixer.removeRange([rangeStart, rangeEnd + 1]);
              },
            });
          }
        });
      },
    };
  }
```
</details>

- **Parameters**:
  - `context: any`
- **Return Type**: `{ Program(): void; }`
- **Calls**:
  - `context.sourceCode.getAllComments`
  - `comments.forEach`
  - `ENABLE_DISABLE_REGEX.test`
  - `context.report`
  - `toText`
  - `context.sourceCode.getIndexFromLoc`
  - `fixer.removeRange`

---